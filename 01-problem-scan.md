# 🔍 Phase 1 — SCAN & Phase 2 — QUICK-ASSESS (Cá nhân)

**Họ và tên:** Lê Nhật Linh  
**Mã sinh viên:** 2A202603514  
**Đơn vị giả định:** AI Product Engineer — Vin Smart Future (Vingroup)  
**Mảng trọng tâm:** GSM (Xanh SM) & Hệ sinh thái Vingroup  

---

# 🔍 Phase 1 — SCAN: Bảng quét cơ hội vận hành Vingroup

Quét qua hoạt động vận hành của các công ty thành viên Vingroup sử dụng **4 Lenses**:
1. **Lặp lại (Repetitive):** Tác vụ lặp đi lặp lại nhiều lần hằng ngày.
2. **Tốn thời gian (Time-consuming):** Tác vụ ngốn thời gian xử lý thủ công của nhân viên.
3. **AI có thể tốt hơn (AI-upgrade):** Dịch vụ khách hàng hiện tại còn chậm hoặc phản hồi rập khuôn.
4. **Pain từ người khác (Stakeholder Pain):** Bottleneck khiến khách hàng hoặc nhân viên thực địa phàn nàn.

### 📝 Bảng quét cơ hội (SCAN Table):

| # | Công ty thành viên | Phân loại Lens | Mô tả ngắn bài toán thực tế | Tác động vận hành hiện tại |
|---|--------------------|----------------|-----------------------------|----------------------------|
| 1 | **Xanh SM (GSM)** | Tốn thời gian / Cấp bách | **Điều phối cứu hộ khẩn cấp khi xe taxi điện cạn pin (< 5%) trên đường đón khách:** Điều phối viên tra cứu thủ công trụ sạc VinFast trống và toạ độ xe qua điện thoại/Zalo, mất 12-15 phút/lượt, gây ách tắc giao thông và tăng tỷ lệ khách hủy chuyến. | Thất thoát doanh thu, tài xế hoang mang, xe hết pin giữa đường gây ách tắc giao thông. |
| 2 | **VinFast** | AI-upgrade | **Chẩn đoán sơ bộ mã lỗi kỹ thuật EV từ mô tả tiếng Việt tự nhiên của chủ xe:** Khách hàng mô tả triệu chứng xe (tiếng kêu gầm, sụt pin nhanh, lỗi sạc), CSKH mất 15-20 phút tra cứu sổ tay kỹ thuật để phân luồng đến đúng xưởng dịch vụ. | Thời gian đặt hẹn kéo dài, chuyển sai xưởng kỹ thuật gây quá tải cục bộ. |
| 3 | **Vinhomes** | Lặp lại | **Phân loại và điều phối ticket sự cố kỹ thuật cư dân trên App Vinhomes Resident:** Hàng ngàn yêu cầu phản ánh mỗi ngày (hỏng bóng đèn hành lang, rò rỉ nước, bảo dưỡng điều hòa) đang được nhân viên lễ tân đọc và gán thủ công cho từng tổ kỹ thuật tòa nhà. | Chậm trễ SLA xử lý, cư dân phản ánh gay gắt trong các nhóm cộng đồng. |
| 4 | **Vinmec** | Tốn thời gian | **Soạn thảo tóm tắt hồ sơ xuất viện (Discharge Summary) từ bệnh án điện tử:** Bác sĩ mất 20-30 phút/bệnh nhân để tổng hợp kết quả xét nghiệm, chẩn đoán và đơn thuốc thành bản tóm tắt dễ hiểu cho bệnh nhân khi ra viện. | Bác sĩ quá tải hành chính, thời gian chờ làm thủ tục xuất viện của bệnh nhân lên tới nhiều giờ. |
| 5 | **Vinpearl / VinWonders** | Pain từ người khác | **Xử lý email đặt phòng đoàn phức tạp (B2B Group Booking):** Nhân viên sales phải đọc chuỗi email đặt phòng theo đoàn lữ hành, thủ công kiểm tra quỹ phòng trống theo từng hạng phòng và tính toán biểu giá chiết khấu. | Mất 2-4 giờ để phản hồi báo giá, dễ nhầm lẫn số lượng phòng trống vào mùa cao điểm. |
| 6 | **VinFast** | Lặp lại | **Đối chiếu hóa đơn sạc điện đối tác và trụ sạc nhượng quyền:** So khớp nhật ký giao dịch sạc điện hàng tuần giữa hệ thống lõi VinFast với dữ liệu báo cáo từ các trạm sạc đối tác công cộng. | Kế toán mất 3 ngày/tuần đối soát số liệu lệch do độ trễ truyền dữ liệu mạng. |

---

# 🃏 Phase 2 — QUICK-ASSESS: 3 Thẻ bài toán nhanh (Quick Problem Cards)

Từ 6 bài toán trên, nhóm tiến hành lọc và đánh giá 3 bài toán có tiềm năng ứng dụng AI khả thi nhất:

---

### 📇 QUICK PROBLEM CARD #1 (Lựa chọn Deep-Dive)

```text
┌─────────────────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                                       │
│                                                                             │
│ Bài toán: Hỗ trợ điều phối viên Xanh SM ra quyết định khẩn cấp khi xe taxi  │
│           điện cạn pin (< 5%) hoặc gặp sự cố trạm sạc trên thực địa.        │
│ Công ty thành viên: [x] Xanh SM (GSM)   [ ] VinFast   [ ] Vinhomes          │
│                     [ ] Vinmec          [ ] Khác: ___________________       │
│                                                                             │
│ Ai đang đau (Actor)? Tài xế Xanh SM (lo xe chết máy) & Điều phối viên       │
│                      (quá tải thao tác đa màn hình giờ cao điểm).           │
│                                                                             │
│ Workflow thủ công hiện tại (5 bước):                                        │
│   1. Tài xế gọi Hotline/bấm nút SOS báo pin dưới 5%                         │
│   ──> 2. Điều phối viên tra cứu vị trí GPS trên hệ thống giám sát xe       │
│   ──> 3. Tra cứu ứng dụng VinFast tìm trạm sạc trống gần nhất (bán kính 5km)│
│   ──> 4. Soạn thảo tin nhắn hướng dẫn hoặc gọi đội xe sạc di động cứu hộ    │
│   ──> 5. Xác nhận lộ trình di chuyển an toàn với tài xế                    │
│                                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 3 & 4 (⏱ 10-12 phút/lượt xử lý).      │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 3 & 4: Phân tích toạ độ, lọc     │
│ trạm sạc trống hoặc tự động kích hoạt điều xe cứu hộ sạc di động tức thì.    │
│                                                                             │
│ Đo thành công bằng gì (Metric có số)?                                       │
│ - Giảm thời gian ra quyết định & gửi hướng dẫn: từ 12 phút ──> dưới 2 phút. │
│ - 100% cuốc sự cố pin < 5% được điều xe sạc di động cứu hộ kịp thời.       │
│                                                                             │
│ Quick Architecture: [x] LLM Feature (Co-pilot sinh phản hồi có Guardrail)   │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

### 📇 QUICK PROBLEM CARD #2

```text
┌─────────────────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                                       │
│                                                                             │
│ Bài toán: Tự động phân loại mã lỗi kỹ thuật xe điện VinFast từ phản ánh     │
│           bằng tiếng Việt tự nhiên của khách hàng qua App/Hotline.          │
│ Công ty thành viên: [ ] Xanh SM   [x] VinFast   [ ] Vinhomes                │
│                     [ ] Vinmec    [ ] Khác: ___________________             │
│                                                                             │
│ Ai đang đau (Actor)? Nhân viên CSKH VinFast (thiếu kiến thức chuyên sâu về  │
│                      cơ khí/điện tử) & Chủ xe (chờ chẩn đoán lâu).          │
│                                                                             │
│ Workflow thủ công hiện tại (4 bước):                                        │
│   1. Tiếp nhận mô tả tự do của khách (âm thanh lạ, đèn taplo, lỗi sạc)      │
│   ──> 2. CSKH dò tìm từ khóa trong file tài liệu kỹ thuật PDF nội bộ        │
│   ──> 3. Đoán nhóm lỗi (Hệ thống truyền động / Pin / Phần mềm điều khiển)   │
│   ──> 4. Tạo lịch hẹn và chuyển phiếu sang Xưởng dịch vụ phù hợp            │
│                                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2 & 3 (⏱ 12-15 phút/cuộc gọi).        │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2 & 3: Phân tích ngữ nghĩa       │
│ tiếng Việt, ánh xạ mô tả dân dã sang mã lỗi DTC kỹ thuật chuẩn xác.         │
│                                                                             │
│ Đo thành công bằng gì (Metric có số)?                                       │
│ - Tăng độ chính xác phân luồng xưởng dịch vụ từ 72% ──> trên 92%.           │
│ - Giảm thời gian chẩn đoán tiếp nhận ban đầu từ 15 phút ──> dưới 3 phút.    │
│                                                                             │
│ Quick Architecture: [x] LLM Feature (RAG tra cứu sổ tay dịch vụ kỹ thuật)   │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

### 📇 QUICK PROBLEM CARD #3

```text
┌─────────────────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                                       │
│                                                                             │
│ Bài toán: Tự động trích xuất thực thể và định tuyến ticket phản ánh sự cố   │
│           kỹ thuật căn hộ từ cư dân Vinhomes tới đúng đội kỹ thuật tòa nhà. │
│ Công ty thành viên: [ ] Xanh SM   [ ] VinFast   [x] Vinhomes                │
│                     [ ] Vinmec    [ ] Khác: ___________________             │
│                                                                             │
│ Ai đang đau (Actor)? Lễ tân/Ban quản lý Vinhomes (ngập trong hàng nghìn tin │
│                      nhắn mỗi ngày) & Cư dân (bực bội vì xử lý chậm).       │
│                                                                             │
│ Workflow thủ công hiện tại (4 bước):                                        │
│   1. Tiếp nhận ticket từ App Vinhomes Resident                              │
│   ──> 2. Nhân viên đọc nội dung, xác định tòa/căn/vấn đề (Điện/Nước/PCCC)   │
│   ──> 3. Nhắn tin trên Zalo đội ngũ kỹ thuật ca trực tương ứng              │
│   ──> 4. Cập nhật trạng thái phản hồi hẹn giờ cho cư dân                    │
│                                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2 & 3 (⏱ 8-10 phút/ticket).           │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2: Tự động trích xuất vị trí     │
│ căn hộ, phân loại độ khẩn cấp (P1 khẩn cấp - mất nước vs P3 - hỏng đèn ban công). │
│                                                                             │
│ Đo thành công bằng gì (Metric có số)?                                       │
│ - 90% ticket thường được định tuyến tự động trong vòng dưới 30 giây.        │
│ - 100% sự cố khẩn cấp (cháy, ngập nước) được cảnh báo tức thì cho kỹ sư.   │
│                                                                             │
│ Quick Architecture: [x] Rule + LLM Classifier                               │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

### 🎯 Quyết định chọn bài toán Deep-Dive của nhóm:
Nhóm quyết định chọn **Quick Problem Card #1: Điều phối cứu hộ khẩn cấp sạc pin taxi điện Xanh SM** vì:
1. **Tính cấp thiết và an toàn thực tế:** Xe điện cạn pin giữa đường gây tắc nghẽn giao thông đô thị và nguy cơ mất an toàn giao thông nghiêm trọng cho thương hiệu Xanh SM.
2. **Operational Boundary rõ ràng:** Có thể áp đặt các ranh giới cứng (Hard Guardrails) như thẻ `[DRAFT_ONLY]` cho Human-in-the-loop và quy tắc pin `< 5%` bắt buộc điều xe cứu hộ di động thay vì mạo hiểm cho tài xế chạy tìm trạm sạc xa.
