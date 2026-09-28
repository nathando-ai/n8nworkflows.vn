---
title: "🚀 Tự Động Trích Xuất Dữ Liệu CV Từ Đính Kèm Email & Lưu Trữ Trên Supabase (Không Code)"
description: "Workflow tự động hóa trích xuất thông tin CV từ file PDF/Word trong email, xử lý bằng AI (LLM), và lưu trữ sạch sẽ vào cơ sở dữ liệu Supabase. Giúp HR tiết kiệm 80% thời gian đánh giá ứng viên."
slug: "tieu-chuyen-du-lieu-cv-tu-email-luu-tren-supabase"
tags: [n8n, automation, hr, ai, supabase, pdf-processing, no-code]
keywords: [tự động hóa cv, trích xuất dữ liệu cv từ email, supabase n8n, ai trong hr, xử lý file đính kèm email]
---

# 🚀 **Tự Động Trích Xuất Dữ Liệu CV Từ Email & Lưu Trữ Trên Supabase**

### **Giải pháp cho HR: Từ "Đọc CV" sang "Tự Động Hiểu CV"**
Các sếp HR đã từng phải mất **giờ đồng hồ** để đọc từng CV, trích xuất thông tin như **kinh nghiệm, kỹ năng, trường đại học, và liên lạc**? Với workflow này, **AI sẽ làm việc thay bạn** – tự động:
✅ **Trích xuất** thông tin chi tiết từ file CV (PDF/Word) trong email
✅ **Xử lý bằng LLM** (Meta Llama 4) để phân loại và chuẩn hóa dữ liệu
✅ **Lưu trữ** vào **Supabase** (cơ sở dữ liệu cloud miễn phí) với cấu trúc sạch sẽ
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công

---
### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian**: Không còn phải đọc từng CV thủ công.
- **Chính xác cao**: AI phân loại kỹ năng, kinh nghiệm theo cấu trúc chuẩn.
- **Dữ liệu sạch**: Thông tin được lưu trữ hệ thống vào Supabase, dễ dàng truy xuất và phân tích.
- **Hoạt động liên tục**: Workflow chạy tự động ngay khi email mới có CV đính kèm.
- **Cải thiện trải nghiệm ứng viên**: Các sếp có thể phản hồi nhanh chóng dựa trên dữ liệu đã chuẩn hóa.
:::

---
### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Gmail** (để kích hoạt trigger nhận email mới).
2. **API Key của OpenRouter** (để sử dụng mô hình AI Meta Llama 4).
   - Đăng ký tại: [https://openrouter.ai/](https://openrouter.ai/)
3. **Supabase Project** (để lưu trữ dữ liệu trích xuất).
   - Tạo tại: [https://supabase.com/](https://supabase.com/)
   - **Bảng dữ liệu cần tạo trước**:
     - Tên bảng: `resumes` (hoặc tùy chỉnh)
     - Cột cần thiết: `email`, `name`, `phone`, `skills`, `experience`, `education`, `linkedin`, `created_at`
4. **Credentials cho n8n**:
   - **Gmail**: Cài đặt OAuth 2.0 cho n8n (hướng dẫn tại [n8n Gmail Docs](https://docs.n8n.io/integrations/builtins/nodes/n8n-nodes-base.gmailTrigger/)).
   - **Supabase**: Thêm credential mới trong n8n với `URL`, `anon key`, và `service role key`.
   - **OpenRouter**: Thêm credential với `API Key` từ OpenRouter.
:::

---
### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. **Tải file JSON** từ [n8n Workflow Library](https://n8n.io/workflows/4106) (hoặc sử dụng link trên).
2. Trong **n8n Editor**, nhấn **Import** và chọn file JSON.
3. **Hoặc copy/paste JSON** vào tab **JSON** của workflow mới.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow được chia thành **4 phần chính**, các sếp cần chú ý cấu hình sau:

##### **📬 Email Trigger (Gmail Trigger)**
- **Cấu hình**:
  - Chọn **OAuth 2.0** (đã thiết lập trước).
  - **Label**: Chọn nhãn email chứa CV (ví dụ: `cv-applications`).
  - **Attachments**: Chọn **Only files** để chỉ lấy file đính kèm.
  - **Operation**: Chọn **Create** (lắng nghe email mới).
- **Lưu ý**:
  - Nếu không có OAuth, các sếp phải **bật "Less Secure Apps"** trên Gmail (không khuyến nghị cho môi trường sản xuất).

##### **📄 Extract from File (Trích xuất từ PDF/Word)**
- **Cấu hình**:
  - **Operation**: Chọn `pdf` (hoặc `docx` nếu CV là Word).
  - **File Path**: Sử dụng `$node["Gmail Trigger"].json["attachments"][0].fileName` (đường dẫn đến file đính kèm).
- **Lưu ý**:
  - Nếu file không phải PDF, các sếp phải **cài đặt node `extractFromFile` hỗ trợ DOCX** (hoặc chuyển đổi file trước).

##### **🤖 AI Processing (Basic LLM Chain)**
- **Cấu hình**:
  - **Model**: Sử dụng `meta-llama/llama-4-scout:free` (miễn phí).
  - **Prompt**: Workflow đã định sẵn prompt để trích xuất:
    ```json
    "Extract structured data from the resume. Return in JSON format with keys: name, phone, email, skills, experience, education, linkedin."
    ```
  - **Credentials**: Chọn credential OpenRouter đã thiết lập trước.
- **Lưu ý**:
  - Nếu prompt không hiệu quả, các sếp có thể **cập nhật lại** trong node `Edit Fields` trước khi gửi vào LLM.

##### **🗃️ Supabase Storage (Lưu trữ dữ liệu)**
- **Cấu hình**:
  - **Table**: Chọn `resumes` (hoặc tên bảng đã tạo).
  - **Insert/Update**: Chọn `Insert` (hoặc `Upsert` nếu muốn cập nhật dữ liệu cũ).
  - **Columns**:
    - `email`: `$node["Gmail Trigger"].json["payload"]["from"]`
    - `name`: `$json["name"]` (trích xuất từ LLM)
    - `skills`: `$json["skills"]`
    - `experience`: `$json["experience"]`
    - `created_at`: `$node["Gmail Trigger"].json["timestamp"]`
- **Lưu ý**:
  - Các sếp cần **kiểm tra cấu trúc bảng** trong Supabase để trùng khớp với cột trong workflow.
  - Nếu cần **lọc email trùng lặp**, thêm node `If` để kiểm tra `email` đã tồn tại trong Supabase.

---
#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Gửi một email mẫu có CV đính kèm (PDF/Word) đến địa chỉ email đã cấu hình.
   - Kiểm tra **n8n Execution Log** để xác nhận dữ liệu trích xuất và lưu trữ thành công.
2. **Bật Active**:
   - Sau khi test thành công, chuyển workflow sang **Active**.

---
### ✍️ **Mẹo & gợi ý nâng cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Gửi thông báo Slack/Telegram**:
   - Thêm node `Slack` hoặc `Telegram Bot` sau `Supabase` để thông báo khi CV mới được xử lý.
   - Ví dụ: `CV mới từ [email] đã được lưu trữ!`.

2. **Lưu log vào Google Sheets**:
   - Sử dụng node `Google Sheets` để ghi lại lịch sử trích xuất (email, thời gian, trạng thái).

3. **Phân loại ứng viên tự động**:
   - Sau khi lưu vào Supabase, thêm workflow phụ để **phân loại ứng viên** (ví dụ: "Phù hợp", "Không phù hợp") dựa trên kỹ năng.

4. **Tích hợp với CRM**:
   - Sử dụng node `HubSpot` hoặc `Salesforce` để chuyển dữ liệu CV vào hệ thống quản lý ứng viên.

5. **Cập nhật liên tục**:
   - Nếu ứng viên gửi CV mới, workflow sẽ tự động **cập nhật** thông tin cũ trong Supabase.
:::

---
### 📌 **Kết luận**
Workflow này **giải phóng HR khỏi công việc thủ công** và đưa dữ liệu CV vào **cấu trúc sạch sẽ**, dễ dàng phân tích. Các sếp có thể:
✔ **Tiết kiệm thời gian** để tập trung vào phỏng vấn.
✔ **Tăng cường chính xác** trong đánh giá ứng viên.
✔ **Hoạt động 24/7** mà không cần can thiệp.

**Bắt đầu ngay!** Import workflow, cấu hình các credential, và **đón chờ AI làm việc thay bạn**.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**Chia sẻ & phản hồi**: Các sếp có thể **tùy chỉnh prompt** hoặc **thêm node** để phù hợp với quy trình HR của mình. Hãy **like và chia sẻ** nếu workflow này hữu ích! 🚀