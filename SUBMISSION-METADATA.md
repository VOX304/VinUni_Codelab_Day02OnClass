# 📋 BẢNG THÔNG TIN NỘP BÀI (SUBMISSION METADATA)
## Lab 02: AI Product Scoping (Vin Smart Future)

---

### 👤 1. Thông tin sinh viên & Nhánh làm bài
* **Họ và tên:** Lê Nhật Linh
* **Mã sinh viên:** 2A202603514
* **Email:** lun19881408@gmail.com
* **Git Branch cá nhân:** `lenhatlinh`
* **Vai trò trong dự án giả định:** AI Product Engineer — Vin Smart Future (Vingroup)

---

### 🏢 2. Thông tin Dự án Scoping
* **Tên dự án:** Trợ lý Điều phối Thông minh Xanh SM (Xanh SM Smart Emergency & Charging Dispatcher)
* **Công ty thành viên trọng tâm:** **GSM (Xanh SM) & VinFast**
* **Bài toán giải quyết:** Hỗ trợ điều phối viên ra quyết định điều hướng trạm sạc khả dụng và tự động kích hoạt xe sạc pin di động cứu hộ khi taxi điện cạn pin khẩn cấp (< 5%).
* **Kiến trúc giải pháp:** LLM Co-Pilot Feature (`gemini-3.5-flash`) kết hợp Hard Operational Guardrails & Human-in-the-loop (`[DRAFT_ONLY]`).

---

### 📦 3. Danh mục các Deliverables nộp bài

| STT | Tên file / Deliverable | Loại tài liệu | Trạng thái |
| :---: | :--- | :--- | :---: |
| 1 | `01-problem-scan.md` | Phase 1 (SCAN 6 problems) + Phase 2 (3 Quick Cards) | ✅ Hoàn thành |
| 2 | `02-deep-dive-report.md` | Phase 3 (6-field Statement, Future Flow) + Phase 5 (Evaluate GO) | ✅ Hoàn thành |
| 3 | `03-ai-log.md` | Phase 6 (AI Reflection, Hallucination Analysis & Boundary Fixes) | ✅ Hoàn thành |
| 4 | `04-workflow-diagram.png` | Sơ đồ Current-State Workflow (Bottlenecks 🔴 & Handoffs 🔄) | ✅ Hoàn thành |
| 5 | `starter-code/prompt_prototype.py` | Mã nguồn Prompt Engineering & Adversarial Unit Tests | ✅ Hoàn thành |
| 6 | `GLOSSARY.md` | Thuật ngữ chuyên ngành AI Product & EV Fleet Operations | ✅ Hoàn thành |
| 7 | `requirements-lock.txt` | Khóa chính xác phiên bản môi trường thực thi Python | ✅ Hoàn thành |

---

### 🧪 4. Kết quả Tự đánh giá qua Autograder

```text
[REPORT] KET QUA CHAM DIEM TONG HOP CHO CA NHOM:
[PASS] File ton tai: 01-problem-scan.md (Scan & Quick Cards) (+1.25d)
[PASS] File ton tai: 02-deep-dive-report.md (Deep-Dive Report) (+1.25d)
[PASS] File ton tai: 03-ai-log.md (AI Log & Reflection) (+1.25d)
[PASS] File ton tai: 04-workflow-diagram (.png/.jpg/.pdf) (+1.25d)
[PASS] Code - Tieu chi 1: SYSTEM_PROMPT hop le va co chi thi ranh gioi. (+1.0d)
[PASS] Code - Tieu chi 2: Ham evaluate_prompt() su dung Gemini SDK chinh xac. (+1.0d)
[PASS] Code - Tieu chi 3: Da khai bao it nhat 2 Adversarial test cases hop le. (+1.0d)
[PASS] Code - Tieu chi 4: Script chay thanh cong (code 0, khong crash). (+1.0d)
[PASS] Code - Tieu chi 5: Vot qua toan bo assertion test ve ranh gioi. (+1.0d)
============================================================
[SCORE] TONG DIEM: 10.00 / 10.00 (TUYỆT ĐỐI)
```
