---
title: "📚 **Hệ Thống Quản Lý Club Sách Tự Động + Công Cụ Gợi Ý Sách AI với Mistral & Gemini Vision (N8n)**
description: "Tự động hóa quản lý club sách, gợi ý sách thông minh dựa trên AI, và tương tác tự động với thành viên - giải pháp hoàn hảo cho các sếp quản lý nhóm đọc sách. Khắc phục thủ công, tiết kiệm thời gian và nâng cao trải nghiệm đọc cho thành viên."
slug: "quan-ly-club-sach-ai-mistral-gemini-n8n"
tags: [n8n, automation, no-code, ai-chatbot, market-research, self-hosted, google-gemini, mistral-ai]
keywords: [n8n workflow quản lý club sách, tự động hóa gợi ý sách AI, Mistral AI với n8n, Gemini Vision trong n8n, tự động hóa quản lý thành viên, tự động hóa club sách không code]
---

# 🚀 **Hệ Thống Quản Lý Club Sách Tự Động + AI Gợi Ý Sách với Mistral & Gemini Vision**

### **Giải pháp cuối cùng cho các sếp quản lý nhóm đọc sách**
Hãy tưởng tượng một hệ thống **tự động quản lý club sách**, trong đó:
- Thành viên có thể **đăng ký, gợi ý sách, chia sẻ phản hồi** một cách hoàn toàn tự động.
- AI **Mistral và Gemini Vision** phân tích sách, gợi ý sách phù hợp với sở thích cá nhân.
- **Email tự động** gửi thông báo sách mới, gợi ý, và tổng hợp ý kiến.
- **Dữ liệu được cập nhật liên tục**, không cần can thiệp thủ công.

Không cần viết một dòng code nào! **Workflow này tự động hóa toàn bộ quy trình**, giúp các sếp **tiết kiệm thời gian, tăng cường tương tác trong nhóm**, và **cải thiện trải nghiệm đọc sách** cho thành viên.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên một VPS chuyên dụng. Dưới đây là một số gợi ý:
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 **[VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ sức mạnh cho workflow này)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tự động hóa quản lý thành viên**: Đăng ký, xóa, cập nhật thông tin một cách tự động.
✅ **Gợi ý sách cá nhân hóa**: AI phân tích sở thích và gợi ý sách phù hợp.
✅ **Tương tác tự động**: Email tự động gửi thông báo sách mới, gợi ý, và tổng hợp ý kiến.
✅ **Quản lý dữ liệu toàn diện**: Lưu trữ sách đã đọc, phản hồi, ý tưởng mới, và tổng hợp thông tin.
✅ **Tiết kiệm thời gian**: Không cần can thiệp thủ công, hệ thống hoạt động **24/7**.
✅ **Tăng cường tương tác trong nhóm**: Thành viên có thể dễ dàng chia sẻ và tương tác với nhau.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
### **1. Tài khoản và API Keys**
| **Dịch vụ**               | **Thông tin cần thiết**                                                                 | **Lưu ý**                                                                 |
|---------------------------|-----------------------------------------------------------------------------------------|---------------------------------------------------------------------------|
| **Mistral AI**            | API Key từ [Mistral Cloud](https://mistral.ai/)                                         | Cần cấp phép cho model `mistral-tiny` hoặc `mistral-small`.               |
| **Google Gemini API**      | API Key từ [Google Cloud](https://cloud.google.com/vertex-ai)                            | Chọn model `gemini-pro-vision` hoặc `gemini-pro`.                        |
| **Gmail (nếu gửi email)** | Tài khoản Gmail và **App Password** (nếu sử dụng 2FA)                                  | Cần bật **Less Secure Apps** hoặc sử dụng App Password.                 |
| **Google Sheets**         | File Sheets đã chia sẻ và **API Key** (nếu sử dụng Google Drive API)                   | Workflow sử dụng Sheets để lưu trữ sách, phản hồi, và gợi ý.            |
| **Webhook (nếu cần)**    | URL webhook để nhận dữ liệu từ bên ngoài (nếu có)                                      | Nếu không cần, có thể bỏ qua.                                            |

### **2. Cấu trúc dữ liệu trong Google Sheets**
Workflow sử dụng **Google Sheets** để lưu trữ:
- **Sách đã đọc** (Book Archive)
- **Gợi ý sách** (Book Recommendations)
- **Phản hồi sách** (Book Feedback)
- **Yếu tố mới** (Book Ideas)
- **Thành viên club** (Members)
- **Tóm tắt sách** (Summaries)

Các sếp cần **tạo các sheet tương ứng** với tên:
- `Book Archive`
- `Book Recommendations`
- `Book Feedback`
- `Book Ideas`
- `Members`
- `Summaries`

Mỗi sheet cần **cột tiêu đề** như sau (ví dụ cho `Book Archive`):
| Cột tiêu đề          | Loại dữ liệu |
|----------------------|--------------|
| `title`              | Text         |
| `author`             | Text         |
| `cover_image_url`    | Text         |
| `description`        | Text         |
| `rating`             | Number       |
| `review`             | Text         |
| `currently_reading`  | Boolean      |

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Bước 1: Tải workflow từ n8n.io**
- Truy cập [link workflow gốc](https://n8n.io/workflows/11407).
- Nhấn **Export** để tải file `.json`.

#### **Bước 2: Import vào n8n**
- Mở **n8n Editor** trên VPS hoặc n8n.io.
- Nhấn **Import** và chọn file `.json` vừa tải.
- Chọn **Create new workflow** và nhấn **Import**.

#### **Bước 3: Cấu hình credentials**
Sau khi import, các sếp cần **cấu hình credentials** cho các node quan trọng:
- **Mistral AI**: Tạo credential mới trong **Settings > Credentials** với tên `Mistral API Key` và điền API Key.
- **Google Gemini**: Tạo credential mới với tên `Google Gemini API Key` và điền API Key.
- **Gmail**: Tạo credential mới với tên `Gmail Account` và điền:
  - **Email**: Tài khoản Gmail.
  - **Password**: App Password (nếu sử dụng 2FA).
- **Google Sheets**: Tạo credential mới với tên `Google Sheets` và điền:
  - **Spreadsheet ID**: ID của file Sheets (tham khảo [cách lấy Spreadsheet ID](https://support.google.com/docs/answer/10701263)).
  - **Range**: `Sheet1!A1` (hoặc tên sheet tương ứng).

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này **phức tạp** và có nhiều node cần cấu hình cẩn thận. Dưới đây là **các node quan trọng** cần chú ý:

#### **🔹 Node "Workflow Configuration" (Set)**
- Cần **cấu hình các biến môi trường** như:
  - `GOOGLE_SHEETS_SPREADSHEET_ID`
  - `MISTRAL_API_KEY`
  - `GOOGLE_GEMINI_API_KEY`
  - `GMAIL_ACCOUNT` (nếu sử dụng)

#### **🔹 Node "Book Recommendation Agent" (Agent)**
- **Prompt AI** đã được tối ưu hóa, nhưng các sếp có thể **cập nhật** nếu cần:
  ```json
  {
    "role": "user",
    "content": "You are a book recommendation agent. Analyze the user's reading history and preferences, then suggest 3 books that match their taste. Return the results in JSON format."
  }
  ```
- **Cấu hình model**: Chọn `mistral-tiny` hoặc `mistral-small` trong Mistral Cloud.

#### **🔹 Node "Analyze an image" (Google Gemini)**
- **Sử dụng khi upload ảnh bìa sách**.
- **Prompt AI** đã được thiết lập để phân tích bìa sách và trích xuất thông tin:
  ```json
  {
    "role": "user",
    "content": "Analyze this book cover image and extract the title, author, and description. Return the results in JSON format."
  }
  ```

#### **🔹 Node "Mistral Cloud Chat Model" (lmChatMistralCloud)**
- **Cấu hình model**: Chọn `mistral-tiny` hoặc `mistral-small`.
- **Prompt AI** đã được tối ưu hóa để:
  - Tóm tắt sách.
  - Trả lời câu hỏi về sách.
  - Gợi ý sách mới.

#### **🔹 Node "Google Sheets (DataTable)"**
- **Cấu hình sheet và range**:
  - `Book Archive`: `Book Archive!A1`
  - `Book Recommendations`: `Book Recommendations!A1`
  - `Book Feedback`: `Book Feedback!A1`
  - `Book Ideas`: `Book Ideas!A1`
  - `Members`: `Members!A1`
  - `Summaries`: `Summaries!A1`

#### **🔹 Node "Gmail" (gmail)**
- **Cấu hình email**:
  - **From**: Tài khoản Gmail của bạn.
  - **To**: Email của thành viên (có thể lấy từ sheet `Members`).
  - **Subject**: "Gợi ý sách mới từ Club Sách của bạn!"
  - **Body**: Nội dung email tự động (có thể chỉnh sửa trong node `Set Form Details`).

#### **🔹 Node "Webhook" (webhook)**
- Workflow hỗ trợ **API webhook** để:
  - Thêm sách mới (`POST /api/archive/add`).
  - Thêm gợi ý sách (`POST /api/ideas/add`).
  - Thêm phản hồi sách (`POST /api/feedback/add`).
  - Quản lý thành viên (`POST /api/members/add`, `POST /api/members/remove`).
- **Các sếp có thể mở rộng** bằng cách kết nối với **Slack, Telegram, hoặc ứng dụng khác**.

---

### **3. Kích hoạt ⚡️**
#### **Bước 1: Test Run**
- Chọn **node "Schedule Check"** (scheduleTrigger) và nhấn **Run Workflow**.
- Kiểm tra **log** để đảm bảo workflow hoạt động bình thường.

#### **Bước 2: Bật Active**
- Sau khi test thành công, chuyển workflow sang **Active**.

#### **Bước 3: Cấu hình lịch chạy**
- Node `Schedule Check` được cấu hình chạy **hàng tuần** (hoặc tùy chỉnh).
- Các sếp có thể **cập nhật lịch chạy** trong node `scheduleTrigger`:
  - **Cron expression**: `0 0 * * 0` (chạy vào Chủ Nhật lúc 00:00).

---

## ✍️ **Mẹo & gợi ý nâng cao**
### **1. Kết nối với Slack/Telegram**
- Sử dụng **node `httpRequest`** để gửi thông báo từ workflow đến Slack/Telegram.
- Ví dụ:
  ```json
  {
    "url": "https://api.telegram.org/bot<BOT_TOKEN>/sendMessage",
    "method": "POST",
    "body": {
      "chat_id": "<CHAT_ID>",
      "text": "📚 Gợi ý sách mới: {{ $node["Book Recommendation Agent"].json["title"] }}"
    }
  }
  ```

### **2. Lưu log hoạt động**
- Sử dụng **node `stickyNote`** để ghi log hoạt động:
  ```json
  {
    "text": `Workflow ran at {{ $node["Schedule Check"].date }}. Books added: {{ $node["Save Books"].json.length }}`
  }
  ```

### **3. Gửi báo cáo định kỳ**
- Tạo một **workflow riêng** để tổng hợp và gửi báo cáo tuần/month:
  - Lấy dữ liệu từ `Book Archive`, `Book Feedback`, `Book Recommendations`.
  - Gửi báo cáo qua **Gmail** hoặc **Slack**.

### **4. Cập nhật cover ảnh sách**
- Sử dụng **node `convertToFile`** để upload ảnh cover từ URL vào Google Drive và cập nhật vào sheet.

### **5. Tích hợp với Goodreads API**
- Sử dụng **node `httpRequest`** để lấy dữ liệu sách từ Goodreads và tự động cập nhật vào workflow.

---

## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp quản lý **club sách**, giúp tự động hóa toàn bộ quy trình từ **quản lý thành viên** đến **gợi ý sách AI**. Với **Mistral và Gemini Vision**, hệ thống không chỉ quản lý sách mà còn **tăng cường tương tác** và **cải thiện trải nghiệm đọc sách** cho thành viên.

### **Bước tiếp theo:**
1. **Import workflow** và cấu hình credentials.
2. **Test run** để đảm bảo hoạt động bình thường.
3. **Bật Active** và bắt đầu sử dụng!

🚀 **Hãy tự động hóa club sách của bạn ngay hôm nay!** Nếu có vấn đề, các sếp có thể tham khảo [community n8n](https://community.n8n.io/) hoặc liên hệ với tác giả [Jordan Hoyle](https://n8n.io/workflows/11407).