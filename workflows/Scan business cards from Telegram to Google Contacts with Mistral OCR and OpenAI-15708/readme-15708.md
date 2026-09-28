---
title: "🤖 Tự Động Hoàn Hảo: Quét & Lưu Thông Tin Thẻ Doanh Nghiệp Telegram Vào Google Contacts Với AI OCR & OpenAI"
description: "Workflow này tự động quét, trích xuất và lưu thông tin từ thẻ doanh nghiệp gửi qua Telegram vào Google Contacts chỉ trong vài giây, giúp các sếp tiết kiệm thời gian và tránh sai sót khi nhập liệu thủ công. Sử dụng công nghệ OCR Mistral và AI OpenAI để đảm bảo độ chính xác cao."
slug: "tieu-thanh-thong-tin-the-doanh-nghiep-telegram-vao-google-contacts"
tags: [n8n, automation, no-code, ai-ocr, google-contacts, telegram-bot, openai]
keywords: [tự động hóa quét thẻ doanh nghiệp, lưu thông tin thẻ vào google contacts, ai ocr telegram, workflow n8n, tự động hóa liên lạc doanh nghiệp]
---

# 🚀 **Tự Động Quét Thẻ Doanh Nghiệp Telegram → Google Contacts Với AI OCR & OpenAI**

### **Giải pháp hoàn hảo cho các sếp muốn loại bỏ việc nhập liệu thủ công**
Hãy tưởng tượng: Một thẻ doanh nghiệp được gửi qua Telegram chỉ cần một cú nhấp chuột là thông tin đã tự động được trích xuất và lưu vào Google Contacts. Không cần copy-paste, không cần nhớ sai tên hoặc số điện thoại, và tất cả đều diễn ra trong thời gian thực. **Workflow này chính là giải pháp đó!**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động 24/7 mà không gặp lỗi, các sếp nên cài đặt n8n trên **VPS riêng** (Self-hosted) để đảm bảo tính ổn định và bảo mật cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần nhập liệu thủ công, giảm thiểu sai sót đến 90%.
- **Chính xác cao**: AI OCR và OpenAI tự động trích xuất thông tin chính xác từ thẻ doanh nghiệp.
- **Hoạt động liên tục**: Workflow chạy tự động 24/7, không cần can thiệp của con người.
- **Tích hợp hoàn hảo**: Thông tin được lưu trực tiếp vào Google Contacts, dễ dàng quản lý.
- **Cá nhân hóa**: Hỗ trợ thêm thông tin như website, địa chỉ, vai trò công việc vào contact.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Telegram**:
   - Tạo **bot Telegram** và lấy **API Token** (để n8n kết nối).
   - Thêm **ID Telegram** của người dùng được phép sử dụng workflow (để xác thực).
2. **Tài khoản Mistral OCR**:
   - Đăng ký API key tại [Mistral AI](https://mistral.ai/) để trích xuất văn bản từ ảnh.
3. **Tài khoản OpenAI**:
   - API Key của OpenAI để sử dụng **Information Extractor** (cần chọn mô hình `gpt-5.4-mini`).
4. **Tài khoản Google**:
   - **Google OAuth 2.0** để truy cập và cập nhật **Google Contacts**.
5. **n8n Self-hosted**:
   - Cài đặt n8n trên VPS để workflow hoạt động 24/7 (không phụ thuộc vào phiên bản cloud miễn phí).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Bước 1**: Tải file JSON của workflow từ [n8n.io/workflows/15708](https://n8n.io/workflows/15708).
- **Bước 2**: Mở **n8n Editor** và chọn **Import Workflow** → Chọn file JSON vừa tải.
- **Bước 3**: Nếu copy/paste JSON, đảm bảo **không có lỗi cú pháp** (sử dụng công cụ kiểm tra JSON online nếu cần).

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **12 node** quan trọng, các sếp cần cấu hình kỹ lưỡng:

##### **🔹 Node "Code" (Xác thực Telegram)**
- **Cần thay đổi**:
  - Thay thế `authorizedUserId` bằng **ID Telegram của người dùng được phép** (lấy từ `@username` hoặc `/getme` trong Telegram Bot API).
  - **Cú pháp**: `authorizedUserId: "123456789"` (thay số này bằng ID thực tế).

##### **🔹 Node "Get Message" (Telegram Trigger)**
- **Cấu hình**:
  - Chọn **credentials**: `telegramApi` (đã cấu hình trước khi import).
  - **Lưu ý**: Workflow chỉ hoạt động khi **caption bắt đầu bằng `/business`**.

##### **🔹 Node "Get image file" (Lấy ảnh từ Telegram)**
- **Cần thiết**: Chọn **credentials**: `telegramApi`.
- **Kiểm tra**: Đảm bảo ảnh được gửi cùng với tin nhắn có caption `/business`.

##### **🔹 Node "Extract from File" (Chuyển ảnh thành Base64)**
- **Không cần chỉnh**: Node này tự động chuyển ảnh thành định dạng Base64 để Mistral OCR xử lý.

##### **🔹 Node "Mistral OCR" (Trích xuất văn bản từ ảnh)**
- **Cần thiết**:
  - **Credentials**: `httpBearerAuth` (API Key Mistral) và `httpHeaderAuth` (thường là `Content-Type: application/json`).
  - **URL API Mistral**: Thay thế trong **HTTP Request** bằng URL chính thức của Mistral (ví dụ: `https://api.mistral.ai/ocr`).
  - **Payload**:
    ```json
    {
      "image": "{{$json.base64}}",
      "language": "en" // hoặc "vi" nếu thẻ là tiếng Việt
    }
    ```
  - **Lưu ý**: Nếu Mistral không hỗ trợ, có thể thay thế bằng **Tesseract OCR** (node `extractFromFile` với `operation: "ocr"`).

##### **🔹 Node "Information Extractor" (OpenAI AI)**
- **Cần thiết**:
  - **Credentials**: `openAiApi` (API Key OpenAI).
  - **Model**: Đã cấu hình mặc định là `gpt-5.4-mini` (nếu muốn thay đổi, chỉnh trong `keyParameters`).
  - **Prompt**: Node này tự động cấu hình để trích xuất:
    - Tên, công ty, vai trò, số điện thoại, email, website, địa chỉ.
  - **Lưu ý**: Nếu OpenAI không hỗ trợ mô hình này, có thể sử dụng `gpt-4` hoặc `gpt-3.5-turbo`.

##### **🔹 Node "Create a contact" (Google Contacts)**
- **Cần thiết**:
  - **Credentials**: `googleContacts` (cấu hình OAuth 2.0 trước).
  - **Tham số**:
    - `name`: `{{$json.name}}` (tên từ AI trích xuất).
    - `emails`: `{{$json.email}}` (danh sách email).
    - `phones`: `{{$json.phone}}` (danh sách số điện thoại).
    - `organizations`: `{{$json.company}}` (công ty).
    - `addresses`: `{{$json.address}}` (địa chỉ).
  - **Lưu ý**: Nếu Google Contacts không nhận dữ liệu, kiểm tra **cấu trúc JSON** từ node `Information Extractor`.

##### **🔹 Node "Success?" & "Validate message" (Xác thực kết quả)**
- **Không cần chỉnh**: Node này tự động kiểm tra:
  - Nếu trích xuất thành công → Gửi tin nhắn **"OK"** qua Telegram.
  - Nếu lỗi → Gửi tin nhắn **"KO"** và log lỗi.

---

#### **3. Kích hoạt ⚡️**
- **Bước 1**: **Test Run** với một ảnh mẫu (đảm bảo có caption `/business`).
- **Bước 2**: Nếu không có lỗi, **bật Active** workflow.
- **Bước 3**: Gửi thẻ doanh nghiệp qua Telegram Bot để test thực tế.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tích hợp Slack/Telegram thông báo**:
   - Thêm node **Slack** hoặc **Telegram** sau node `Create a contact` để gửi thông báo thành công/lỗi.
   - **Cú pháp**:
     ```json
     {
       "text": "📞 Contact created: {{$json.name}} ({{$json.company}})"
     }
     ```

2. **Lưu log vào Google Sheets**:
   - Thêm node **Google Sheets** sau node `Create a contact` để ghi lại lịch sử.
   - **Cấu hình**:
     - Sheet Name: `Business Card Logs`
     - Dữ liệu: `{{$json}}` (tất cả thông tin trích xuất).

3. **Sử dụng AI Chatbot phản hồi**:
   - Thêm node **OpenAI Chat** để bot trả lời tự động khi người dùng gửi tin nhắn `/business`.
   - **Prompt**:
     ```
     "Xin chào! Tôi là bot quét thẻ doanh nghiệp. Gửi ảnh thẻ của bạn với caption /business để tôi tự động lưu thông tin vào Google Contacts của bạn."
     ```

4. **Xử lý lỗi tự động**:
   - Thêm node **Code** sau node `KO` để gửi lại tin nhắn yêu cầu người dùng thử lại.
   - **Cú pháp**:
     ```javascript
     return [
       {
         telegram: {
           chatId: "{{$node["Get Message"].json().chat.id}}",
           text: "❌ Lỗi khi quét thẻ. Vui lòng gửi lại ảnh với caption /business và đảm bảo ảnh rõ nét."
         }
       }
     ];
     ```

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** của các sếp khỏi việc nhập liệu thủ công, đồng thời **tăng độ chính xác** nhờ công nghệ AI. **Chỉ cần một cú nhấp chuột**, thông tin thẻ doanh nghiệp đã tự động được lưu vào Google Contacts, sẵn sàng sử dụng cho các cuộc gọi, email hoặc hợp tác tương lai.

**Hành động ngay hôm nay**:
1. **Cài đặt n8n trên VPS** (để workflow hoạt động 24/7).
2. **Cấu hình Telegram Bot, Mistral OCR và OpenAI**.
3. **Import workflow** và test với một thẻ doanh nghiệp mẫu.
4. **Tích hợp thêm Slack/Google Sheets** để quản lý dễ dàng hơn.

👉 **Bắt đầu tự động hóa ngay bây giờ!** Nếu có vấn đề, hãy để lại bình luận dưới đây, các sếp sẽ được hỗ trợ chi tiết. 🚀