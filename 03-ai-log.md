# Lab 02 — AI Interaction Log & Reflection (Cá nhân)

**Đề tài:** AI hỗ trợ phân loại và điều phối phản ánh cư dân Vinhomes  
**Vai trò:** Thành viên nhóm, đóng vai AI Product Engineer tại Vin Smart Future  
**Công cụ hỗ trợ:** ChatGPT — sử dụng như một *thought-partner* để tìm vấn đề, phân tích và phản biện thiết kế sản phẩm AI.

> **Phạm vi và tính trung thực:** Nhật ký này **chỉ nói về quá trình lựa chọn và phân tích đề tài Vinhomes**. Tôi chưa khảo sát nhân viên Vinhomes, chưa có ticket thực tế và chưa kiểm thử mô hình phân loại phản ánh cư dân. Mọi số liệu vận hành trong bài là **giả định để scoping**, không phải kết quả đo thực tế.

## 1. Mục tiêu khi sử dụng AI

Tôi sử dụng ChatGPT để hỗ trợ bốn việc:

1. Đọc và hệ thống hóa các yêu cầu của Lab 02 từ worksheet, ví dụ bài nộp và inspiration kit.
2. Đề xuất nhiều vấn đề vận hành ở các công ty thành viên Vingroup trước khi chọn một bài toán có phạm vi phù hợp.
3. Phác thảo **Current-State Workflow, Problem Statement 6-field, Success Metrics, AI Fit, Future-State Flow** và các giới hạn vận hành.
4. Phản biện các giả định và xác định những bằng chứng còn thiếu trước khi có thể quyết định triển khai AI.

Tôi dùng AI để tăng tốc độ suy nghĩ và tổ chức ý tưởng, **không coi các ví dụ hoặc con số AI đưa ra là dữ liệu thực tế**.

## 2. Nhật ký các lần trao đổi về đề tài Vinhomes

| Lần | Câu hỏi/yêu cầu tôi đã đưa cho AI (tóm tắt) | AI hỗ trợ | Tôi kiểm tra hoặc điều chỉnh thế nào? |
|---|---|---|---|
| **1. Tìm đề tài** | “Hãy phác thảo 1 đề tài thực tế và có thể trả lời đủ yêu cầu bài.” | Đề xuất **AI phân loại và điều phối phản ánh cư dân Vinhomes**, kèm lý do chọn: đầu vào văn bản, workflow dễ mô tả, có thể đo thời gian và độ đúng phân loại. | Tôi đối chiếu với worksheet: đề tài có actor, bottleneck, metrics, ranh giới AI và khả năng so sánh Rule/LLM/Agent. Tôi lựa chọn đề tài này để tiếp tục. |
| **2. Làm rõ bằng chứng** | Tôi xác nhận: “Vai trò: Thành viên; phạm vi: Bài cá nhân; dữ liệu: Chưa có dữ liệu thực, dùng giả định có ghi chú.” | AI giữ đề tài Vinhomes và bắt đầu trình bày thời gian, sản lượng, KPI dưới dạng **giả định/mục tiêu**. | Đây là điều chỉnh quan trọng: không được viết rằng Vinhomes thật sự xử lý 120 ticket/ngày hay mất 11 phút/ticket khi chưa có dữ liệu chứng minh. |
| **3. Triển khai bản phân tích** | Tôi đồng ý tiếp tục hoàn thiện các file tài liệu cho đề tài đã chọn. | AI soạn danh sách 5 problems, 3 Quick Cards, workflow, 6-field, AI Fit, Future-State và đánh giá readiness. | Tôi đối chiếu với tinh thần **Problem First, AI Second** trong tài liệu: chỉ để AI đề xuất nhãn và tóm tắt; không tự chuyển ticket, không tự phản hồi hoặc quyết định bồi thường. |

## 3. AI đã giúp tôi cải thiện đề tài thế nào?

### 3.1. Từ ý tưởng rộng đến bài toán có thể đo

Ban đầu, “dùng AI cải thiện chăm sóc cư dân” là mục tiêu quá rộng. Qua trao đổi, tôi thu hẹp thành một tác vụ cụ thể: **đọc phản ánh dạng văn bản → phân loại vấn đề → tóm tắt → đề xuất nhóm tiếp nhận để nhân viên duyệt**.

Từ đó có thể xác định rõ:

- **Actor:** Nhân viên CSKH/Ban quản lý cụm tòa nhà.
- **Input:** Nội dung phản ánh tiếng Việt và mã tòa (giả định).
- **Output:** Nhãn vấn đề, mức ưu tiên, bản tóm tắt và nhóm phụ trách được đề xuất.
- **Bottleneck:** Nhân viên cần hiểu văn bản tự do và ghi lại tóm tắt; đây là giả thuyết cần khảo sát để xác minh.
- **Metric:** Thời gian tiếp nhận, độ chính xác nhãn và tỷ lệ đề xuất đúng bộ phận.

### 3.2. Phân biệt giải pháp Rule-based, LLM và Agent

AI giúp tôi nhận ra rằng không phải mọi bước đều cần mô hình ngôn ngữ:

| Công việc | Phương án hợp lý | Lý do |
|---|---|---|
| Kiểm tra định dạng, ánh xạ nhãn sang bộ phận | **Rule-based** | Quy tắc cố định, dễ kiểm toán và rẻ. |
| Hiểu phản ánh dài, mơ hồ hoặc chứa nhiều ý | **LLM Feature** | Có thể hỗ trợ diễn giải ngôn ngữ tự nhiên và tóm tắt. |
| Phê duyệt và chuyển xử lý chính thức | **Con người + hệ thống nghiệp vụ** | Tránh AI tự đưa ra quyết định sai có tác động tới cư dân. |
| Tự trị gọi nhiều công cụ theo vòng lặp | **Chưa chọn Agent** | Chưa chứng minh được giá trị bổ sung đủ lớn so với độ phức tạp/rủi ro. |

Nhờ vậy, giải pháp đề xuất không còn là “AI làm toàn bộ quy trình” mà là **LLM hỗ trợ + quy tắc kiểm soát + Human-in-the-loop**.

## 4. Những điểm AI chưa đủ chính xác hoặc thiếu bằng chứng

### Vấn đề 1 — Số liệu có vẻ hợp lý nhưng chưa có nguồn

Trong bản phác thảo, AI nêu ví dụ **120 ticket/ngày**, **11 phút xử lý thủ công/ticket**, mục tiêu **≤4 phút/ticket** và độ chính xác nhãn **≥90%**. Những con số này giúp hình dung Business Impact, nhưng **không có khảo sát hoặc log thật để xác nhận**.

**Tôi điều chỉnh:** Ghi chú rõ các con số là giả định hoặc mục tiêu pilot. Đề xuất thu thập ticket đã ẩn danh, đo baseline thực tế, sau đó mới tính lợi ích. Nếu trình bày 120 ticket/ngày như số liệu của Vinhomes, đó sẽ là kết luận không có chứng cứ.

### Vấn đề 2 — Chưa chứng minh LLM tốt hơn rule thông thường

AI có thể đề xuất LLM rất nhanh, nhưng những phản ánh đơn giản như “đèn hành lang hỏng” có thể phân loại bằng từ khóa. Chưa có cơ sở để nói LLM chắc chắn hiệu quả hơn với mọi ticket.

**Tôi điều chỉnh:** Chọn kiến trúc kết hợp. Khi có dữ liệu, cần so sánh độ chính xác, thời gian và chi phí của **keyword/rule baseline** với LLM, đặc biệt ở những phản ánh có phủ định, nhiều chủ đề hoặc cách diễn đạt không chuẩn.

### Vấn đề 3 — Rủi ro của các phản ánh khẩn cấp

Phân loại nhầm một phản ánh bình thường có thể gây chậm trễ; nhưng bỏ sót nội dung như **cháy, kẹt người trong thang máy hoặc nguy cơ điện giật** có hậu quả nghiêm trọng hơn nhiều.

**Tôi điều chỉnh:** Giới hạn AI ở bản nháp. Những trường hợp có dấu hiệu nguy hiểm phải được đưa tới nhân viên và quy trình khẩn cấp hiện có. Nếu AI không rõ nội dung hoặc kết quả không hợp lệ, chuyển sang **fallback thủ công**, không tự quyết định.

## 5. Sự thay đổi trong cách đặt yêu cầu cho AI

| Giai đoạn | Cách yêu cầu | Bài học |
|---|---|---|
| Ban đầu | “Phác thảo một đề tài thực tế.” | Prompt rộng giúp brainstorm nhưng chưa đủ chặt để đánh giá tính khả thi. |
| Sau khi xem đề xuất | Xác nhận đề tài Vinhomes và ranh giới của bài lab. | Giữ một pain point cụ thể thay vì mở rộng sang mọi hoạt động CSKH. |
| Sau khi làm rõ dữ liệu | Yêu cầu **dùng giả định có ghi chú** vì không có dữ liệu thực. | Tách số liệu minh họa khỏi sự thật có thể kiểm chứng. |
| Khi phát triển giải pháp | Giữ phạm vi AI là **phân loại/tóm tắt/đề xuất**, có nhân viên duyệt. | Operational Boundary phải là một phần của thiết kế, không chỉ là câu nhắc trong prompt. |
| Khi hoàn thiện reflection | Chỉ lưu các trao đổi liên quan trực tiếp đến đề tài Vinhomes. | Nhật ký cần tập trung và phản ánh đúng quá trình học của cá nhân. |

## 6. Reflection cá nhân

Tôi học được rằng **AI Product Scoping không phải chỉ là chọn một ý tưởng có thể dùng AI**. Một đề tài tốt cần chỉ ra ai đang làm công việc gì, bước nào chậm, ảnh hưởng kinh doanh ra sao, cách đo cải thiện và AI không được phép vượt qua ranh giới nào.

AI hữu ích trong việc gợi ý và tổ chức khung phân tích, nhưng tôi cần tự đánh giá độ tin cậy của từng nội dung. Điểm quan trọng nhất là nhận ra **một con số hợp lý không có nghĩa là một con số đã được xác minh**. Vì chưa có dữ liệu thực và chưa tham vấn nhân viên vận hành, tôi đồng ý với quyết định **NOT YET cho triển khai thực tế**; chỉ nên cân nhắc prototype offline để kiểm chứng giả thuyết.

Nếu được tiếp tục, tôi sẽ thực hiện các bước: (1) hỏi nhân viên CSKH về workflow và bottleneck; (2) thu thập ticket đã ẩn danh và gán nhãn; (3) đo baseline; (4) so sánh Rule-based với LLM; (5) kiểm thử tình huống khẩn cấp và đánh giá Human-in-the-loop. Tôi sẽ không báo cáo rằng mô hình Vinhomes đã đạt KPI khi chưa chạy thử.

## 7. Giới hạn của nhật ký hiện tại

- **Đã có:** Quá trình chọn đề tài, làm rõ phạm vi, xây dựng giả thuyết, nhận diện điểm thiếu bằng chứng và sửa cách trình bày.
- **Chưa có:** Dữ liệu Vinhomes thực tế, kết quả phân loại bằng mô hình, thống kê thời gian thực nghiệm, phản hồi của nhân viên CSKH.
- **Cần cập nhật nếu được thực hiện sau này:** Prompt thử nghiệm, các ví dụ đúng/sai, kết quả đo chất lượng và lần chỉnh sửa theo bằng chứng.