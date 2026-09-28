---
title: "🚀 Tự Động Hóa Xử Lý CV Từ Email: OCR + AI GPT → Cập Nhật Notion (Không Cần Code)"
description: "Giải pháp tự động hóa hoàn toàn cho HR nhận email CV PDF, trích xuất thông tin bằng OCR + AI, và tự động cập nhật vào Notion Database. Tiết kiệm 100% thời gian thủ công, giảm sai sót, và duy trì cơ sở dữ liệu ứng viên chuyên nghiệp 24/7."
slug: "tieu-ly-cv-tu-email-ocr-gpt-notion"
tags: [n8n, automation, hr, ai-summarization, notion, ocr, openai, gmail]
keywords: [tự động hóa cv từ email, ocr cv pdf, ai trích xuất cv, notion database hr, workflow n8n hr, giải pháp tuyển dụng tự động]
---

# 🚀 **Tự Động Hóa Xử Lý CV Từ Email: OCR + AI GPT → Cập Nhật Notion (Không Cần Code)**

### **📌 Nỗi Đau Của Các Sếp HR**
Hàng ngày, các sếp HR phải:
- **Lọc và tải** hàng chục CV PDF từ email.
- **Nhập thủ công** thông tin vào Notion/Excel, tốn thời gian và dễ sai sót.
- **Bị quên** hoặc **trùng lặp** dữ liệu ứng viên.
- **Không có cách nào** để tự động trích xuất thông tin chi tiết (trình độ, kinh nghiệm, kỹ năng) từ CV.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Nhận email** có CV PDF từ ứng viên.
✅ **Trích xuất văn bản** bằng OCR (dành cho CV quét).
✅ **Phân tích AI** bằng GPT để trích xuất thông tin chi tiết (tên, email, kinh nghiệm, kỹ năng, liên kết LinkedIn...).
✅ **Kiểm tra trùng lặp** bằng số điện thoại.
✅ **Cập nhật tự động** vào Notion Database, giúp HR quản lý ứng viên một cách chuyên nghiệp.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm 10+ giờ/tuần** cho việc nhập liệu thủ công.
- **Chính xác 100%** với AI trích xuất thông tin chi tiết từ CV.
- **Không bị trùng lặp** dữ liệu ứng viên.
- **Hoạt động 24/7** mà không cần can thiệp của con người.
- **Cơ sở dữ liệu Notion** được cập nhật tự động, dễ dàng theo dõi và phân tích.
- **Tối ưu quy trình tuyển dụng** với dữ liệu sạch và hệ thống hóa.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI LẮP ĐỘNG**]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Gmail** (để nhận email CV từ ứng viên).
   - **OAuth2 Gmail** đã kết nối trong n8n (cài đặt ở **Credentials** → **Gmail OAuth2**).
2. **API Key OCR.space** (dùng để trích xuất văn bản từ PDF).
   - Mua tại: [https://ocr.space/ocrapi](https://ocr.space/ocrapi) (miễn phí 500 trang/tháng).
3. **API Key OpenAI** (để sử dụng GPT-4/3.5 để phân tích CV).
   - Cài đặt tại: [https://platform.openai.com/api-keys](https://platform.openai.com/api-keys).
   - **Lưu ý**: Nếu không muốn đặt API Key trong workflow, có thể đặt trong **System Variables** của n8n.
4. **Notion Database** đã sẵn sàng với các trường dữ liệu sau (có thể điều chỉnh):
   - `Name` (Tên ứng viên)
   - `Email` (Email liên lạc)
   - `Phone` (Số điện thoại)
   - `Location` (Địa chỉ)
   - `Experience` (Kinh nghiệm)
   - `Education` (Trình độ học vấn)
   - `Skills` (Kỹ năng)
   - `LinkedIn` (Liên kết LinkedIn)
   - `Resume` (Lưu trích liệu CV)
   - `Status` (Trạng thái: "Chờ gọi", "Đã phỏng vấn", "Từ chối")
5. **n8n Self-hosted** (để workflow chạy 24/7).
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải workflow** từ [n8n.io/workflows/6326](https://n8n.io/workflows/6326).
- **Import vào n8n Editor**:
  - Nhấn **Import** → Chọn file JSON hoặc **Copy/Paste** JSON từ trang workflow.
  - **Hoặc** sử dụng link trực tiếp:
    ```bash
    https://n8n.io/workflows/6326
    ```
  - Chọn **Import** và chờ workflow hoàn tất.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow gồm **10 node** chính, nhưng có **3 node quan trọng nhất** cần cấu hình cẩn thận:

##### **A. Node "Gmail Trigger" (n8n-nodes-base.gmailTrigger)**
- **Cấu hình**:
  - **Credentials**: Chọn `gmailOAuth2` (đã cài đặt trước).
  - **Label**: Đặt tên dễ nhận biết (ví dụ: "CV Inbox").
  - **Filter**: Chỉ lấy email có **PDF attachment**.
    - Thêm **Filter Expression**:
      ```json
      {{ $json.body.attachments && $json.body.attachments.some(a => a.filename.endsWith('.pdf')) }}
      ```
  - **Test Run**: Gửi email mẫu có CV PDF để kiểm tra.

##### **B. Node "HTTP Request" (n8n-nodes-base.httpRequest)**
- **Đây là node gọi API OCR.space để trích xuất văn bản từ PDF**.
- **Cấu hình**:
  - **Method**: `POST`
  - **URL**: `https://api.ocr.space/parse/file`
  - **Headers**:
    ```json
    {
      "apikey": "{{ $credentials.ocrSpaceApiKey }}",
      "Content-Type": "multipart/form-data"
    }
    ```
  - **Body (Form Data)**:
    - `file`: Chọn `{{ $node["Gmail Trigger"].json.body.attachments[0].data }}` (dữ liệu PDF từ email).
    - `OCREngine**: `3` (OCR Engine 3 cho kết quả tốt nhất).
    - `Language**: `eng` (tiếng Anh, thay đổi nếu CV là tiếng Việt).
  - **Lưu ý**:
    - Nếu không có `ocrSpaceApiKey` trong credentials, **thêm vào System Variables** của n8n.

##### **C. Node "Message a model" (openAi)**
- **Đây là node sử dụng GPT để phân tích CV và trích xuất thông tin**.
- **Cấu hình**:
  - **Credentials**: Chọn `openAiApi`.
  - **Model**: Chọn `gpt-4` (hoặc `gpt-3.5-turbo` nếu tiết kiệm chi phí).
  - **Prompt**:
    ```plaintext
    You are a professional CV parser. Extract structured data from the following resume text:

    [{{ $node["HTTP Request"].json.OCRResults.parsedResults[0].parsedText }}]

    Return JSON with these fields:
    {
      "name": "",
      "email": "",
      "phone": "",
      "location": "",
      "skills": [],
      "experience": [],
      "education": [],
      "linkedin": ""
    }
    ```
  - **Lưu ý**:
    - Nếu GPT trả về JSON không đúng định dạng, **sửa lại Prompt** hoặc thêm **node Code** để xử lý.
    - **Test Run**: Gửi một CV mẫu để kiểm tra kết quả trích xuất.

##### **D. Node "Create entry" (n8n-nodes-base.notion)**
- **Đây là node tạo bản ghi mới trong Notion Database**.
- **Cấu hình**:
  - **Credentials**: Chọn `notionApi`.
  - **Database ID**: Lấy từ URL Notion Database (ví dụ: `https://www.notion.so/workspace/.../Database?v=...` → phần sau `?v=`).
  - **Properties**:
    - Điền theo cấu trúc của Database Notion (ví dụ: `Name` → `{{ $node["Message a model"].json.name }}`).
    - **Lưu ý**: Nếu trường `Resume` (lưu trích liệu CV), sử dụng:
      ```json
      {
        "type": "rich_text",
        "rich_text": [
          {
            "type": "text",
            "text": {
              "content": "{{ $node["HTTP Request"].json.OCRResults.parsedResults[0].parsedText }}"
            }
          }
        ]
      }
      ```
  - **Test Run**: Kiểm tra bản ghi mới được tạo trong Notion.

##### **E. Node "Get many entries" (n8n-nodes-base.notion)**
- **Đây là node kiểm tra trùng lặp bằng số điện thoại**.
- **Cấu hình**:
  - **Credentials**: Chọn `notionApi`.
  - **Database ID**: Cùng với node `Create entry`.
  - **Filter**: Lọc theo trường `Phone`:
    ```json
    {
      "property": "Phone",
      "operator": "equals",
      "value": "{{ $node["Message a model"].json.phone }}"
    }
    ```
  - **Lưu ý**:
    - Nếu tìm thấy bản ghi trùng, **node "If"** sau đó sẽ **bỏ qua** việc tạo mới.

---

#### **3. Kích Hoạt ⚡️ Workflow**
- **Test Run**:
  - Gửi email mẫu có CV PDF vào Gmail đã cấu hình.
  - Kiểm tra:
    - Email có được nhận không?
    - OCR có trích xuất văn bản không?
    - GPT có trích xuất thông tin không?
    - Notion có cập nhật bản ghi mới không?
- **Bật Active**:
  - Sau khi test thành công, nhấn **Active** để workflow chạy tự động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[**TIẾP CẬN HƠN**]
1. **Gửi thông báo Slack/Telegram khi có CV mới**:
   - Thêm node `Slack` hoặc `Telegram Bot` sau node `Create entry` để thông báo cho team.
   - **Cấu hình**:
     ```json
     {
       "text": "📩 CV mới từ {{ $node["Message a model"].json.name }} đã được cập nhật vào Notion!"
     }
     ```
2. **Lưu log hoạt động**:
   - Thêm node `StickyNote` hoặc `Google Sheets` để ghi lại lịch sử xử lý CV.
3. **Tự động gửi email xác nhận**:
   - Thêm node `Gmail Send Email` sau node `Create entry` để gửi email cho ứng viên:
     ```json
     {
       "to": "{{ $node["Message a model"].json.email }}",
       "subject": "Xác nhận CV của bạn đã được nhận!",
       "text": "Chúng tôi đã nhận và xử lý CV của bạn thành công. Hãy chờ tin tức từ chúng tôi!"
     }
     ```
4. **Tối ưu Prompt GPT**:
   - Nếu GPT không trích xuất được thông tin chính xác, **cập nhật Prompt** để rõ ràng hơn:
     ```plaintext
     Extract ONLY these fields from the resume:
     - Name: Full name of the candidate.
     - Email: Personal email address.
     - Phone: Mobile number.
     - Location: City and country.
     - Skills: List of skills in array format.
     - Experience: Work history with company name, position, and duration.
     - Education: Degree, university, and graduation year.
     - LinkedIn: LinkedIn profile URL.
     ```
5. **Sử dụng OCR Engine 4 (OCR.space)**:
   - Nếu CV có nhiều hình ảnh, thử **OCR Engine 4** (tốc độ chậm hơn nhưng chính xác hơn).

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp HR muốn **tự động hóa quy trình nhận và xử lý CV**, tiết kiệm thời gian và giảm sai sót. Với **OCR + AI GPT + Notion**, bạn có thể:
✔ **Nhận email CV** từ ứng viên.
✔ **Trích xuất thông tin chi tiết** một cách chính xác.
✔ **Cập nhật tự động** vào Notion Database.
✔ **Kiểm tra trùng lặp** bằng số điện thoại.
✔ **Hoạt động 24/7** mà không cần can thiệp.

**🚀 Hãy áp dụng ngay và tự động hóa quy trình tuyển dụng của bạn!**
Nếu có vấn đề, hãy **comment bên dưới** hoặc liên hệ với **Blue Code** (tác giả workflow) để hỗ trợ.

---
**🔗 [Tải workflow gốc tại n8n.io](https://n8n.io/workflows/6326)** | **🛠 [Cài đặt n8n Self-hosted](https://docs.n8n.io/)**