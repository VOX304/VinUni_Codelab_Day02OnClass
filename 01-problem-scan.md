# Lab 02 — Problem Scan & Quick Problem Cards

**Vai trò:** AI Product Engineer (bài làm cá nhân, bối cảnh Vin Smart Future)  
**Đề tài được lựa chọn:** AI hỗ trợ phân loại và điều phối phản ánh cư dân Vinhomes  
**Phạm vi:** Scoping và thiết kế thử nghiệm; chưa triển khai lên hệ thống thực tế.

> **Nguyên tắc dữ liệu:** Đây là bài tập mô phỏng. Chưa có khảo sát nhân viên, ticket thật hoặc log của Vinhomes. Tất cả thời gian, sản lượng và mục tiêu định lượng bên dưới là **giả định làm việc để thiết kế pilot**, không phải số liệu vận hành đã xác minh.

## Phase 1 — SCAN: Quét cơ hội bằng 4 lenses

| # | Công ty thành viên | Lens | Bài toán / bottleneck được đề xuất |
|---|---|---|---|
| 1 | **Vinhomes** | **Lặp lại (Repetitive)** | Nhân viên CSKH đọc phản ánh cư dân, phân loại chủ đề và chuyển ticket sang đúng bộ phận. Nội dung tự do có nhiều cách diễn đạt, đôi khi chứa nhiều vấn đề trong một tin. |
| 2 | **Vinpearl** | **Tốn thời gian (Time-consuming)** | Nhân viên quản lý chất lượng đọc từng đánh giá khách sạn, ghi nhận phàn nàn và tổng hợp nguyên nhân tiêu cực theo tuần. |
| 3 | **Xanh SM** | **Pain từ người khác (Stakeholder Pain)** | Ghi chú của tài xế về cuốc bị hủy không thống nhất, khiến bộ phận vận hành khó tổng hợp nguyên nhân và phản hồi cải tiến. |
| 4 | **VinFast** | **AI-upgrade** | Khách mô tả triệu chứng xe bằng ngôn ngữ đời thường; nhân viên tiếp nhận phải làm rõ và gắn nhãn vấn đề kỹ thuật sơ bộ trước khi chuyển kỹ thuật viên. |
| 5 | **Vinmec** | **Tốn thời gian (Time-consuming)** | Bác sĩ tổng hợp thông tin từ nhiều ghi chú để soạn bản nháp tóm tắt xuất viện; khâu rà soát thủ công cần độ chính xác cao. |

**Nhận xét sau SCAN:** Năm vấn đề bao phủ đủ bốn lenses của worksheet. Tình huống VinFast và Vinmec có rủi ro an toàn/y tế cao, nên chỉ thích hợp cho AI hỗ trợ có chuyên gia phê duyệt. Bài toán Vinhomes có đầu vào văn bản tương đối dễ mô phỏng và ranh giới AI có thể thiết kế rõ ràng.

## Phase 2 — QUICK-ASSESS: Top 3 Quick Problem Cards

### Quick Problem Card #1 — Vinhomes: Phân loại và điều phối phản ánh cư dân

| Trường | Nội dung |
|---|---|
| **Bài toán (1 câu)** | Hỗ trợ CSKH tự động hiểu, phân loại và tóm tắt phản ánh bằng tiếng Việt, sau đó đề xuất bộ phận tiếp nhận để nhân viên duyệt. |
| **Công ty thành viên** | Vinhomes |
| **Actor đang đau** | Nhân viên CSKH/Ban quản lý cụm tòa nhà; cư dân chịu ảnh hưởng khi ticket được chuyển chậm hoặc sai nhóm. |
| **Workflow thủ công (5 bước)** | (1) Đọc ticket **2 phút** → (2) Xác định chủ đề/ưu tiên **3 phút** → (3) Tìm nhóm phụ trách **2 phút** → (4) Tóm tắt, ghi chú **3 phút** → (5) Chuyển ticket **1 phút**. |
| **Bottleneck** | Bước 2 và 4, tổng **6 phút/ticket**, do phải hiểu văn bản tự do và viết lại nội dung. |
| **AI can thiệp ở đâu?** | LLM đề xuất `category`, `priority`, `summary`; quy tắc cố định ánh xạ sang `suggested_team`; CSKH kiểm tra trước khi chuyển. |
| **Success metric có số** | Giảm thời gian xử lý đầu vào từ **11 xuống ≤4 phút/ticket**; độ chính xác phân loại trên tập thử có nhãn đạt **≥90%**. |
| **Quick Architecture** | **LLM Feature + Rule-based**, không cần Agent tự trị. |
| **Rủi ro & ranh giới ban đầu** | Không tự gửi trả lời/đóng ticket; phát hiện dấu hiệu khẩn cấp và chuyển nhân viên; không tự quyết định bồi thường hoặc phí. |

**Ví dụ giả lập:** “Hành lang tầng 12 có nước rò xuống gần ổ cắm, nhờ kiểm tra sớm.” Đây là tin nhắn có cả vấn đề nước lẫn nguy cơ điện, khó xử lý bằng một bộ từ khóa đơn giản mà không có quy tắc ưu tiên an toàn.

### Quick Problem Card #2 — Vinpearl: Tổng hợp review tiêu cực

| Trường | Nội dung |
|---|---|
| **Bài toán (1 câu)** | Rút ngắn thời gian đọc và gắn nhãn đánh giá tiêu cực để quản lý khách sạn nắm các vấn đề lặp lại. |
| **Công ty thành viên** | Vinpearl |
| **Actor đang đau** | Nhân viên quản lý chất lượng và quản lý khách sạn. |
| **Workflow thủ công (4 bước)** | (1) Lấy review **1 phút** → (2) Đọc, phân tích **3 phút** → (3) Gắn nhãn vấn đề **2 phút** → (4) Ghi vào báo cáo **2 phút**. |
| **Bottleneck** | Đọc, xác định chủ đề và ghi báo cáo: khoảng **5 phút/review**. |
| **AI can thiệp ở đâu?** | LLM tóm tắt và gắn nhãn `cleanliness`, `service`, `facilities`, `other`; quản lý rà soát đánh giá nhạy cảm. |
| **Success metric có số** | Giảm xử lý từ **8 xuống ≤3 phút/review**; tỷ lệ gắn nhãn đúng **≥90%** trên mẫu kiểm tra. |
| **Quick Architecture** | **LLM Feature** để phân loại/tóm tắt; rule chỉ dùng cho lọc từ khóa rõ ràng. |
| **Rủi ro & ranh giới ban đầu** | Không đăng trả lời công khai hoặc hứa hoàn tiền nếu chưa có nhân viên duyệt. |

### Quick Problem Card #3 — Xanh SM: Phân loại nguyên nhân hủy chuyến

| Trường | Nội dung |
|---|---|
| **Bài toán (1 câu)** | Chuẩn hóa ghi chú tự do của tài xế về lý do hủy chuyến để hỗ trợ báo cáo vận hành. |
| **Công ty thành viên** | Xanh SM (GSM) |
| **Actor đang đau** | Chuyên viên phân tích vận hành; tài xế cần nguyên nhân hủy chuyến được hiểu đúng. |
| **Workflow thủ công (4 bước)** | (1) Thu thập ghi chú **1 phút** → (2) Đọc, đối chiếu bối cảnh **2 phút** → (3) Gắn nhãn nguyên nhân **2 phút** → (4) Cập nhật thống kê **1 phút**. |
| **Bottleneck** | Đọc và gắn nhãn: khoảng **4 phút/trường hợp**. |
| **AI can thiệp ở đâu?** | LLM phân loại ghi chú thành các nguyên nhân chuẩn; nhân viên kiểm tra các trường hợp thiếu thông tin. |
| **Success metric có số** | Giảm từ **6 xuống ≤2 phút/trường hợp**; độ chính xác gắn nhãn **≥90%**. |
| **Quick Architecture** | **LLM Feature** với tập nhãn cố định; không cần Agent. |
| **Rủi ro & ranh giới ban đầu** | Không tự sửa trạng thái cuốc, đánh giá lỗi tài xế hoặc điều chỉnh thu nhập. |

## Quyết định chọn bài toán để Deep-Dive

**Chọn Card #1 — Vinhomes: AI hỗ trợ phân loại và điều phối phản ánh cư dân.**

**Lý do:**

1. **Vấn đề đủ hẹp:** Chỉ xử lý phân loại/tóm tắt văn bản đầu vào, không giải quyết sự cố thay con người.
2. **AI có vai trò hợp lý:** Từ khóa cứng không xử lý tốt cách diễn đạt tự do, phủ định hoặc nhiều chủ đề; LLM có thể hỗ trợ hiểu ngữ nghĩa.
3. **Metric dễ đo:** Thời gian tiếp nhận, độ đúng nhãn, tỷ lệ gợi ý đúng bộ phận và tỷ lệ fallback đều có thể đánh giá trên ticket mô phỏng hoặc dữ liệu đã ẩn danh.
4. **Ranh giới rõ:** Chỉ tạo bản nháp và đề xuất; mọi thao tác chuyển ticket chính thức yêu cầu nhân viên duyệt.

**Vì sao chưa chọn hai card còn lại?** Vinpearl phù hợp nhưng cần thống nhất cách gán nhãn review đa ngôn ngữ; Xanh SM cần log cuốc và định nghĩa nguyên nhân chuẩn mới tránh nhầm lẫn giữa ghi chú chủ quan và nguyên nhân đã được xác thực.

**Phạm vi tiếp theo:** Xem `02-deep-dive-report.md` và sơ đồ `04-workflow-diagram.png`.
