# 🏗️ Báo Cáo Phân Tích Sâu (Deep-Dive Report) — Lab 02: AI Product Scoping

**Dự án:** Trợ lý Điều phối Thông minh Xanh SM (Xanh SM Smart Emergency & Charging Dispatcher)  
**Đơn vị phát triển:** Vin Smart Future (Vingroup)  
**Tác giả:** Lê Nhật Linh (2A202603514)  
**Đối tượng phục vụ:** Điều phối viên (Dispatcher) và Đội xe taxi điện Xanh SM (GSM)  

---

# 🏗️ Phase 3 — DEEP-DIVE

## 3.1. Current-State Workflow Mapping (Sơ đồ vận hành hiện tại)

Quy trình xử lý thủ công hiện tại khi tài xế Xanh SM báo động khẩn cấp về sự cố pin cạn kiệt hoặc trạm sạc:

```text
┌─────────────────┐       ┌─────────────────┐       ┌─────────────────┐       ┌─────────────────┐
│     Bước 1      │       │     Bước 2      │       │     Bước 3      │       │     Bước 4      │
│ Tiếp nhận cuộc  │  ──>  │ Tra cứu định vị │  ──>  │ Tra cứu trạm    │  ──>  │ Soạn thảo tin   │
│ gọi/SOS tài xế  │ (🔄)  │ GPS xe trên map │ (🔄)  │ sạc VinFast còn │ (🔴)  │ nhắn hướng dẫn  │
│                 │       │                 │       │ trụ trống       │       │ gửi tài xế      │
│ Actor: Dispatch │       │ Actor: Dispatch │       │ Actor: Dispatch │       │ Actor: Dispatch │
│ ⏱: 1.5 phút     │       │ ⏱: 1.5 phút     │       │ ⏱: 5.0 phút 🔴  │       │ ⏱: 4.0 phút 🔴  │
│ In: Cuộc gọi    │       │ In: Biển số xe  │       │ In: Toạ độ GPS  │       │ In: Địa chỉ     │
│ Out: Log ticket │       │ Out: Toạ độ GPS │       │ Out: Trạm sạc ID│       │ Out: SMS/Notif  │
└─────────────────┘       └─────────────────┘       └─────────────────┘       └─────────────────┘
                                                                                       │
                                                                                       ▼ (🔄)
                                                                              ┌─────────────────┐
                                                                              │     Bước 5      │
                                                                              │ Liên hệ xe sạc  │
                                                                              │ di động cứu hộ  │
                                                                              │ (khi pin < 5%)  │
                                                                              │ Actor: Dispatch │
                                                                              │ ⏱: 3.0 phút     │
                                                                              │ Out: Dispatch ID│
                                                                              └─────────────────┘
```

* **Tổng thời gian xử lý trung bình:** **15.0 phút / ca sự cố.**
* 🔄 **Điểm chuyển giao (Handoffs):** 
  - Handoff 1: Từ Tài xế qua Tổng đài điều vận (Điện thoại/App).
  - Handoff 2: Từ Màn hình giám sát định vị xe (Fleet Tracking) sang Cổng tra cứu trụ sạc VinFast.
  - Handoff 3: Từ Hệ thống dữ liệu sạc sang Ứng dụng điều phối tài xế và Bộ đàm cứu hộ cơ động.
* 🔴 **Điểm nghẽn cổ chai (Bottlenecks):**
  - **Bước 3 (5 phút):** Điều phối viên phải kiểm tra chéo giữa bán kính di chuyển thực tế, tình trạng kẹt xe giờ cao điểm và số lượng trụ sạc nhanh (DC 60kW/150kW/250kW) còn trống thực tế.
  - **Bước 4 (4 phút):** Soạn thảo tin nhắn thủ công có lộ trình rẽ, giải thích cho tài xế trong tình trạng căng thẳng, dễ xảy ra sai sót chỉ dẫn đến trạm sạc đang hỏng hoặc đã kín chỗ.

---

## 3.2. Problem Statement (Khung 6 trường thông tin chuẩn hóa)

| Trường thông tin (Field) | Nội dung chi tiết |
|---|---|
| **1. Actor / Operator** | Điều phối viên Trung tâm Điều vận Xanh SM (GSM Dispatcher) phối hợp cùng Đội xe cứu hộ sạc pin lưu động VinFast. |
| **2. Current Workflow** | Nhận báo động khẩn từ tài xế ➔ Tra cứu thủ công toạ độ xe trên bản đồ ➔ Tra cứu số cổng sạc trống trên portal đối tác ➔ Gõ tay tin nhắn hướng dẫn hoặc gọi điện thoại điều xe cứu hộ sạc di động. |
| **3. Bottleneck** | Thao tác chuyển đổi qua lại giữa 3 màn hình nghiệp vụ độc lập; mất quá nhiều thời gian tính toán thủ công khoảng cách khả dụng khi pin xe rơi vào mức nguy cấp (< 5%). |
| **4. Business Impact** | Mỗi lượt chậm trễ khiến tài xế có nguy cơ chết máy giữa giao lộ giờ cao điểm, gây tắc đường, khách hủy chuyến (tổn thất doanh thu trung bình ~150.000 VNĐ/cuốc), giảm điểm NPS dịch vụ của Xanh SM và tốn chi phí kéo xe cứu hộ cẩu xe (~800.000 VNĐ/lần). |
| **5. Success Metric** | - **Thời gian xử lý:** Rút ngắn thời gian từ lúc nhận sự cố đến khi phát lệnh hướng dẫn/cứu hộ từ **15 phút ──> dưới 2 phút** (giảm 86%).<br>- **Độ an toàn tuyệt đối:** 100% xe có mức pin dưới 5% được tự động kích hoạt điều xe sạc di động tới tận nơi, không để xảy ra trường hợp nào chết máy trên đường tìm trạm xa. |
| **6. Operational Boundary** | - **AI được làm:** Phân tích dữ liệu toạ độ, lọc trạm sạc khả dụng, tự động draft sẵn kịch bản chỉ dẫn hoặc lệnh điều xe cứu hộ dạng JSON chuẩn hóa.<br>- **AI TUYỆT ĐỐI KHÔNG được làm:** Không tự ý gửi trực tiếp tin nhắn cho tài xế mà chưa qua phê duyệt (bắt buộc gắn tag `[DRAFT_ONLY]`); tuyệt đối không đề xuất trạm sạc xa > 5km khi pin < 5%.<br>- **Human-in-the-loop (HITL):** Điều phối viên bấm nút "Approve & Send" để xác nhận lệnh. |

---

## 3.3. Future-State Flow & AI Fit (Quy trình tương lai)

### 📊 Đánh giá AI Fit (AI-Fit Matrix):
* **Lựa chọn kiến trúc:** **LLM Co-Pilot Feature kết hợp Rule-based Guardrails**.
* **Lý do không dùng Pure Rule-based:** Cần hiểu và tổng hợp ngữ cảnh ngôn ngữ tự nhiên từ tin nhắn cầu cứu khẩn cấp của tài xế (mô tả địa danh, tình trạng xe, cảm xúc hoảng loạn).
* **Lý do không dùng Autonomous Multi-Agent:** Môi trường vận hành xe chở khách liên quan trực tiếp đến an toàn tính mạng và giao thông đô thị, rủi ro ảo giác tự hành quá cao, do đó bắt buộc phải có sự kiểm soát của con người (HITL).

### 🔄 Sơ đồ quy trình tương lai tích hợp AI:

```text
[Tài xế bấm SOS / Báo sự cố pin]
               │
               ▼
   [Đọc toạ độ GPS & Mức % Pin xe]
               │
               ├──────────────────────────────────────────┐
               │ (Pin >= 5%)                              │ (Pin < 5% — Nguy cấp)
               ▼                                          ▼
   🔵 [AI Step: LLM Co-Pilot]                 🔵 [AI Step: Emergency Guardrail]
   - Tra cứu trạm sạc trống < 5km             - Kích hoạt lệnh điều xe sạc di động:
   - Tự động sinh nội dung chỉ dẫn              {"action": "dispatch_mobile_charger"}
   - Bắt buộc gắn tiền tố [DRAFT_ONLY]        - Bắt buộc gắn tiền tố [DRAFT_ONLY]
               │                                          │
               └────────────────────┬─────────────────────┘
                                    │
                                    ▼
                     🟢 [HITL Step: Human Dispatcher Review]
                     - Điều phối viên duyệt nội dung hiển thị
                     - Bấm [Phê duyệt & Gửi] hoặc chỉnh sửa
                                    │
                    ┌───────────────┴───────────────┐
                    │ (Hệ thống LLM Timeout/Lỗi)    │ (Duyệt thành công)
                    ▼                               ▼
     ↩️ [Fallback: Cứu hộ truyền thống]      [Gửi lệnh cứu hộ / chỉ đường]
     - Chuyển cuộc gọi Hotline trực tiếp      - Tài xế nhận tin trên Driver App
     - Tổng đài viên xử lý thủ công           - Xe sạc di động xuất phát
```

* 🔵 **AI Step:** Tự động tổng hợp thông tin trạm sạc, toạ độ, sinh tin nhắn chuẩn hóa và phân luồng cứu hộ.
* 🟢 **HITL Step:** Nhân viên điều vận bấm 1 chạm để phê duyệt sau khi xem xét bản nháp `[DRAFT_ONLY]`.
* ↩️ **Fallback Step:** Nếu API Gemini gặp sự cố timeout (> 3s) hoặc lỗi mạng, hệ thống tự động fallback về quy trình gọi thoại cứu hộ hotline truyền thống.

---

# 🏁 Phase 5 — EVALUATE (Đánh giá độ sẵn sàng & Quyết định)

### 📋 AI Readiness Checklist:
1. **Dữ liệu mẫu/logs sạch:** [x] **SẴN SÀNG.** Dữ liệu telemetry của VinFast/GSM (vị trí GPS xe, trạng thái pin SoC, API trạng thái trụ sạc VinFast) đã được số hóa theo thời gian thực trên hệ thống IoT nội bộ.
2. **Kiểm soát rủi ro:** [x] **SẴN SÀNG.** Có cơ chế HITL (`[DRAFT_ONLY]`), ngưỡng an toàn pin cứng (`< 5%`), và quy trình fallback thoại dự phòng.
3. **Độ sẵn sàng của Stakeholders:** [x] **SẴN SÀNG.** Ban lãnh đạo Khối Vận hành GSM và Tổng đài cam kết thử nghiệm giải pháp Co-pilot để giảm tải 80% áp lực cho điều phối viên.

### 🏆 Quyết định của Ban Giám Đốc Vin Smart Future:
**[x] GO (Bắt đầu xây dựng Prototype MVP)**

### 💡 Justification (Lý giải quyết định dựa trên bằng chứng kỹ thuật và chi phí):
1. **Lợi ích kinh tế vượt trội:** Chi phí vận hành mô hình `gemini-3.5-flash` cực kỳ rẻ (~0.0001 USD/lần gọi API) so với chi phí tổn thất một chuyến xe bị chết máy giữa đường (~150.000 VNĐ doanh thu + ~800.000 VNĐ chi phí cẩu xe).
2. **Khả thi kỹ thuật cao:** Không cần huấn luyện lại mô hình nền (no fine-tuning required); chỉ cần áp dụng System Prompting với kỹ thuật Guardrail ranh giới cứng đã có thể giải quyết dứt điểm 95% tình huống lặp lại.
3. **An toàn kiểm soát được:** Quy định thẻ `[DRAFT_ONLY]` đảm bảo quyền quyết định cuối cùng luôn thuộc về con người, ngăn ngừa tuyệt đối rủi ro AI tự gửi tin sai lệch cho tài xế.
