---
title: "🤖 **Tự Động Đánh Giá Ứng Viên Và Tạo Phản Hồi AI Cho CV (PDF/DOCX) Với OpenAI + Notion - Không Cần Code!**"
description: "Workflow tự động hóa đánh giá ứng viên dựa trên mô tả công việc, phân tích CV (PDF/DOCX) bằng AI, và cập nhật kết quả vào Notion với điểm số, kỹ năng top và lý do loại bỏ - tiết kiệm thời gian tuyển dụng lên đến 80%."
slug: "tieu-dong-danh-gia-ung-vien-ai-notion-openai"
tags: [n8n, automation, no-code, ai, notion, openai, tuyển dụng, cv, pdf, docx]
keywords: [n8n workflow tuyển dụng, tự động hóa đánh giá ứng viên, ai phân tích cv, notion + openai, tự động hóa tuyển dụng không code, đánh giá ứng viên bằng ai]
---

# 🚀 **Tự Động Đánh Giá Ứng Viên Và Tạo Phản Hồi AI Cho CV (PDF/DOCX) Với OpenAI + Notion**

### **Giải pháp nào giúp các sếp:**
- **Tiết kiệm 80% thời gian** trong quá trình đánh giá ứng viên?
- **Đảm bảo khách quan** với điểm số và phân tích kỹ năng dựa trên AI?
- **Cập nhật tự động** kết quả vào Notion với phản hồi chi tiết?
- **Loại bỏ ứng viên không phù hợp** ngay từ đầu?

Workflow này **không cần code**, kết nối **Notion + OpenAI** để tự động:
1. **Nhận ứng viên mới** từ Notion.
2. **Tải và phân tích CV** (PDF/DOCX) bằng AI.
3. **Đánh giá phù hợp** với mô tả công việc.
4. **Cập nhật điểm số, kỹ năng top và lý do loại bỏ** vào Notion.

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[**LỢI ÍCH CỐT LÕI**]
✅ **Tiết kiệm thời gian**: AI tự động đánh giá hàng trăm CV trong vài phút thay vì ngày.
✅ **Chính xác cao**: Phân tích kỹ năng và điểm số dựa trên mô tả công việc chính xác.
✅ **Cá nhân hóa phản hồi**: AI tạo feedback chi tiết cho từng ứng viên.
✅ **Hoạt động 24/7**: Không cần can thiệp thủ công, tự động cập nhật Notion.
✅ **Giảm thiểu sai sót**: Loại bỏ ứng viên không phù hợp từ đầu quy trình.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[**CHUẨN BỊ**]
Trước khi chạy workflow, các sếp cần:
- **Tài khoản Notion** với:
  - Database "TD Careers" (để lưu ứng viên).
  - Database "Open Jobs" (để lưu mô tả công việc).
  - Các trường cần thiết:
    - `AI Comments` (Text) – Lưu phản hồi AI.
    - `Resume Score` (Text) – Điểm số phù hợp (0-100).
    - `Top Skills Detected` (Text) – Kỹ năng top của ứng viên.
    - `Feedback` (Select) – Lý do loại bỏ (nếu có).
- **API Key OpenAI** (để sử dụng GPT-4 Turbo).
- **VPS n8n** (để chạy workflow 24/7).
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/12323](https://n8n.io/workflows/12323) (hoặc copy JSON từ đây).
- **Mở n8n Editor** → Nhấn **"Import"** → Dán JSON → Chọn **"Import"**.
- **Hoặc** copy/paste JSON vào **n8n Editor** → Nhấn **"Create Workflow"**.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **2 phần chính**:
- **Phần 1: Nhận ứng viên mới** (Trigger + Kiểm tra trạng thái).
- **Phần 2: Phân tích CV + Cập nhật Notion** (PDF/DOCX).

#### **A. Cấu hình Notion**
1. **Trigger "On New Candidate"**:
   - Điền `databaseId` của **"TD Careers"** (tìm trong URL Notion của database).
   - Chọn **credentials Notion** (cài đặt trước trong n8n).
   - **Lưu ý**: Trigger chỉ hoạt động với ứng viên **chưa được xử lý** (AI Comments trống).

2. **Nodes "Fetch Job Description"**:
   - Điền `databaseId` của **"Open Jobs"** (database lưu mô tả công việc).
   - Chọn **credentials Notion** tương ứng.

3. **Nodes "Update Notion (DOCX/PDF)"**:
   - Chọn **credentials Notion** để cập nhật kết quả.
   - **Kiểm tra lại trường** trong Notion (nếu có thay đổi).

#### **B. Cấu hình OpenAI**
1. **Nodes "OpenAI PDF Model" & "OpenAI DOCX Model"**:
   - Chọn **credentials OpenAI** (đã cài đặt API Key).
   - **Model**: Chọn `"gpt-4-turbo"` (đã được cài đặt mặc định).
   - **Prompt**: Workflow tự động cấu hình, **không cần chỉnh sửa** (nếu muốn tùy chỉnh, xem phần **Mẹo nâng cao**).

#### **C. Xử lý file CV**
Workflow tự động:
- **Tải CV** từ Notion (đường dẫn trong trường `Resume URL`).
- **Phân loại file** (PDF/DOCX) và xử lý riêng.
- **Chuyển đổi DOCX → Text** (nếu cần).
- **Trích xuất nội dung PDF** (nếu cần).

#### **D. Cấu hình AI Agent**
Nodes **"Analyze Candidate (PDF/DOCX)"** sử dụng **LangChain Agent** để:
- Đánh giá phù hợp với mô tả công việc.
- Trích xuất **kỹ năng top** của ứng viên.
- Đánh giá **điểm số (0-100)**.
- Tạo **phản hồi chi tiết** (lý do loại bỏ nếu có).

**Lưu ý**:
- **Không cần chỉnh sửa mã trong nodes Code** (nếu muốn tùy chỉnh, xem phần **Mẹo nâng cao**).
- **Nodes "Format DOCX Data" & "Format PDF Data"** tự động định dạng dữ liệu trước khi gửi cho AI.

---
### **3. Kích hoạt ⚡️**
1. **Test Run** với 1 ứng viên mẫu:
   - Chọn **1 ứng viên mới** trong Notion (chưa có AI Comments).
   - Nhấn **"Run Workflow"** trong n8n Editor.
   - Kiểm tra kết quả trong Notion:
     - `Resume Score` (điểm số).
     - `Top Skills Detected` (kỹ năng top).
     - `AI Comments` (phản hồi chi tiết).
     - `Feedback` (nếu loại bỏ).

2. **Bật Active**:
   - Sau khi test thành công, **bật "Active"** trong n8n Editor.
   - Workflow sẽ **hoạt động tự động** khi có ứng viên mới.

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::info[**TỰ CẢI TIẾN WORKFLOW**]
1. **Tùy chỉnh Prompt cho AI**:
   - Mở nodes **"Analyze Candidate (PDF/DOCX)"** → Nhấn **"Edit"** → Chỉnh sửa **prompt** trong LangChain Agent.
   - Ví dụ: Yêu cầu AI **trọng tâm hơn vào kỹ năng cụ thể** của công việc.

2. **Gửi báo cáo định kỳ**:
   - Thêm **node Email/Slack** sau "Update Notion" để gửi **tóm tắt ứng viên mới** cho team.

3. **Lưu log xử lý**:
   - Thêm **node "Set"** sau "Analyze Candidate" để lưu **thời gian xử lý** và **status** vào Notion.

4. **Kết hợp với Google Sheets**:
   - Thay vì Notion, sử dụng **Google Sheets** để lưu kết quả (cài đặt node `n8n-nodes-base.googleSheets`).

5. **Phân loại ứng viên tự động**:
   - Thêm **node "Switch"** sau "Analyze Candidate" để **chuyển ứng viên điểm cao sang Slack/Email** của HR.
:::

---
## 📌 **Kết luận**
Workflow này **giải phóng thời gian** của các sếp trong quá trình tuyển dụng, đồng thời **tăng chất lượng tuyển chọn** nhờ AI. **Không cần code**, chỉ cần **cấu hình Notion + OpenAI**, workflow sẽ tự động:
✔ **Nhận ứng viên mới**.
✔ **Phân tích CV (PDF/DOCX)**.
✔ **Đánh giá phù hợp với mô tả công việc**.
✔ **Cập nhật kết quả vào Notion**.

**👉 Hãy import ngay và thử nghiệm với 1 ứng viên mẫu!**
Nếu có vấn đề, **hãy comment bên dưới** hoặc liên hệ với cộng đồng n8n để hỗ trợ.

---
:::info[**Gợi ý hạ tầng cho n8n**]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::