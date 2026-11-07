# 📖 TỪ ĐIỂN THUẬT NGỮ CHUYÊN NGÀNH (GLOSSARY)
## Dự án: Vin Smart Future — AI Product Scoping Lab 02

Tài liệu này định nghĩa chuẩn hóa các thuật ngữ kỹ thuật, nghiệp vụ xe điện (EV) và kiến trúc hệ thống AI được sử dụng xuyên suốt trong các báo cáo của dự án.

---

### 🚗 1. Thuật ngữ Vận hành Xe điện & Điều vận (EV & Fleet Operations)

* **EV (Electric Vehicle):** Xe ô tô chạy hoàn toàn bằng điện năng lưu trữ trong cụm pin Lithium-ion.
* **SoC (State of Charge):** Mức dung lượng pin khả dụng hiện tại của xe, tính theo phần trăm (0% - 100%). Ngưỡng nguy cấp được quy định là `< 5%`.
* **GSM (Green & Smart Mobility - Xanh SM):** Công ty cổ phần Di chuyển Xanh và Thông minh thuộc hệ sinh thái Vingroup, vận hành đội xe taxi thuần điện (VF5, VF e34, VF8).
* **Dispatcher (Điều phối viên vận hành):** Nhân sự tại Trung tâm điều vận Xanh SM chịu trách nhiệm giám sát đội xe, xử lý sự cố thực địa, điều xe và hướng dẫn tài xế.
* **Fleet Telematics / GPS Tracking:** Hệ thống thiết bị phần cứng gắn trên xe gửi dữ liệu tọa độ vị trí thực tế, tốc độ và trạng thái xe về máy chủ thời gian thực qua sóng 4G/5G.
* **DC Fast Charger (Trụ sạc nhanh dòng một chiều):** Trụ sạc công suất lớn (60kW, 150kW, 250kW) của VinFast cho phép sạc từ 10% lên 70% pin trong vòng 20 - 30 phút.
* **Mobile Charging Vehicle (Xe sạc pin di động cứu hộ):** Xe cứu hộ chuyên dụng của VinFast trang bị hệ thống pin sạc lưu động công suất cao, có thể di chuyển tới tận nơi xe taxi chết máy để nạp điện khẩn cấp.

---

### 🤖 2. Thuật ngữ Kỹ thuật AI & An toàn (AI Architecture & Safety Guardrails)

* **AI Product Scoping:** Quy trình khảo sát, đánh giá độ khả thi, xác lập bài toán nghiệp vụ, xác định ranh giới vận hành và xây dựng bản mẫu kỹ thuật (Prototype) trước khi đầu tư phát triển hệ thống AI.
* **Co-Pilot (Trợ lý đồng hành):** Mô hình AI đóng vai trò hỗ trợ con người nâng cao năng suất (tự động tra cứu, tổng hợp, soạn thảo văn bản nháp) thay vì tự động hóa hoàn toàn không có giám sát.
* **HITL (Human-in-the-loop):** Cơ chế bắt buộc phải có sự kiểm duyệt, phê chuẩn của con người trước khi một hành động của hệ thống AI được thực thi ra môi trường thực tế.
* **Operational Boundaries (Ranh giới vận hành):** Các quy tắc an toàn nghiêm ngặt mà hệ thống AI bị nghiêm cấm vi phạm (ví dụ: cấm gửi tin trực tiếp mà không có nhãn `[DRAFT_ONLY]`, cấm chỉ dẫn xe đi xa khi pin `< 5%`).
* **Hard Guardrails (Rào cản an toàn cứng):** Các luật logic hoặc chỉ thị hệ thống cấp cao (System Instructions) được lập trình để ngăn chặn hoàn toàn mô hình vi phạm nguyên tắc bảo vệ doanh nghiệp.
* **Fallback Protocol (Kế hoạch dự phòng):** Quy trình xử lý thay thế khi hệ thống AI gặp lỗi, mất kết nối mạng hoặc không chắc chắn về kết quả (ví dụ: tự động chuyển cuộc gọi về hotline tổng đài viên truyền thống).
* **Hallucination (Ảo giác mô hình):** Hiện tượng mô hình ngôn ngữ lớn (LLM) tự tin tạo ra thông tin không có thật, sai lệch logic hoặc nguy hiểm (ví dụ: chỉ đường tới trạm sạc cách 8km khi xe chỉ còn 2% pin).
* **Adversarial Testing (Kiểm thử thù địch):** Kỹ thuật đưa ra các prompt tấn công, ép buộc hoặc lừa đảo mô hình (Jailbreak, Prompt Injection) nhằm kiểm tra độ vững chắc của các ranh giới an toàn.
