---
title: "🚀 Tự Động Hóa Trích Xuất & Đăng Tin Việc Làm từ URL sang WordPress với AI RAG, Jina & OpenAI"
description: "Workflow tự động hóa hoàn toàn không cần code giúp các sếp HR trích xuất thông tin tuyển dụng từ URL, xử lý bằng AI RAG, Jina AI và OpenAI, sau đó tự động đăng lên WordPress với logo công ty. Giảm thời gian thủ công từ 30 phút xuống 5 phút/việc làm!"
slug: "tieu-dong-hoa-trich-xuat-dang-tin-viec-lam-wordpress"
tags: [n8n, automation, hr, ai-rag, openai, wordpress, jina-ai, telegram-notification]
keywords: [n8n workflow tuyển dụng, tự động hóa tuyển dụng, ai chatbot tuyển dụng, trích xuất tin việc làm từ URL, đăng tin việc làm wordpress tự động]
---

# 🚀 **Tự Động Hóa Trích Xuất & Đăng Tin Việc Làm từ URL sang WordPress với AI RAG**

## **🔥 Nỗi Đau Của Các Sếp HR Hiện Nay**
Hàng ngày, các sếp HR phải:
- **Tìm kiếm và sao chép** thông tin tuyển dụng từ các trang web khác nhau (LinkedIn, Indeed, Glassdoor...).
- **Chuyển đổi dữ liệu** sang định dạng phù hợp cho WordPress (tiêu đề, mô tả, yêu cầu, logo công ty...).
- **Xử lý lỗi thủ công** khi thông tin không đầy đủ hoặc sai định dạng.
- **Cập nhật liên tục** để không bỏ lỡ tin tuyển dụng mới.

**Kết quả?** Tốn **30-60 phút/việc làm**, dễ sai sót, và không thể hoạt động 24/7.

**Giải pháp?** **Workflow này tự động hóa toàn bộ quy trình** bằng AI RAG, Jina AI và OpenAI, chỉ cần **nhập URL** là hệ thống sẽ:
✅ **Trích xuất** thông tin tuyển dụng chính xác từ URL.
✅ **Xử lý bằng AI** để hoàn thiện dữ liệu (định dạng, bổ sung thông tin).
✅ **Tải và upload logo** công ty từ URL.
✅ **Đăng tự động lên WordPress** với định dạng chuẩn.
✅ **Gửi thông báo kết quả** qua Telegram (thành công/thất bại).

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian** so với thủ công (5 phút/việc làm thay vì 30-60 phút).
- **Chính xác 100%** nhờ AI RAG và Jina AI xử lý dữ liệu.
- **Hoạt động 24/7** mà không cần can thiệp người dùng.
- **Logo tự động tải và upload** từ URL công ty.
- **Thông báo ngay lập tức** qua Telegram khi có lỗi hoặc thành công.
- **Cập nhật liên tục** mọi tin tuyển dụng mới mà không bỏ lỡ.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow này hoạt động, các sếp cần chuẩn bị:
#### **1. Tài Khoản & API Keys**
| Dịch vụ               | API Key / Credentials          | Ghi Chú                                  |
|------------------------|--------------------------------|------------------------------------------|
| **Google Drive**       | `googleDriveOAuth2Api`        | Cho phép đọc file và upload logo.       |
| **OpenAI**             | `openAiApi`                    | API Key từ [OpenAI](https://platform.openai.com/). |
| **Supabase**           | `supabaseApi`                  | Database vector store cho AI RAG.        |
| **PostgreSQL**         | `postgres`                     | Database lưu trữ bộ nhớ chat.          |
| **Jina AI**            | `jinaAiApi`                    | API Key từ [Jina AI](https://jina.ai/).   |
| **Telegram**           | `telegramApi`                  | Token bot Telegram để gửi thông báo.    |
| **WordPress**          | `wordpressApi`                 | Username, Password, URL API WordPress.   |
| **Jina AI (nếu dùng)** | `jinaAiApi`                     | (Nếu không dùng, có thể thay bằng OpenAI). |

#### **2. File & Thiết Lập Trước**
- **File CSV chứa danh sách loại việc làm và danh mục** (nếu có).
- **Folder Google Drive** để lưu tạm các file trích xuất.
- **Trang WordPress** đã cấu hình API REST cho đăng bài.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/6299](https://n8n.io/workflows/6299) (chọn "Export").
2. **Mở n8n Editor** trên VPS hoặc n8n.io.
3. **Nhấp vào "Import"** và chọn file JSON vừa tải.
4. **Chọn "Import"** để hoàn tất.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Copy toàn bộ mã JSON** từ [n8n.io/workflows/6299](https://n8n.io/workflows/6299) (chọn "Export").
2. **Mở n8n Editor** và nhấp vào **"..."** → **"Import"** → **"Paste JSON"**.
3. **Chọn "Import"** để hoàn tất.

---

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này **phức tạp** và có **nhiều node cần cấu hình cẩn thận**. Dưới đây là **các bước quan trọng**:

#### **🔹 1. Cấu Hình Credentials (API Keys)**
- **OpenAI**:
  - Đi đến **Settings → Credentials** → Tạo mới `openAiApi`.
  - Nhập `API Key` từ [OpenAI](https://platform.openai.com/).
  - Chọn **model**: `gpt-4.1-mini` (hoặc `gpt-3.5-turbo` nếu không có).

- **Supabase**:
  - Tạo `supabaseApi` với:
    - `URL`: `https://<your-project-ref>.supabase.co`
    - `Key`: `your-supabase-key`
  - Cấu hình **table vector store** trong **Sticky Note** (nút ghim) có tên **"RAG DATA"**.

- **PostgreSQL**:
  - Tạo `postgres` với:
    - `Host`, `Port`, `Database`, `Username`, `Password`.
  - Dùng để lưu **bộ nhớ chat** cho AI.

- **Jina AI** (nếu dùng):
  - Tạo `jinaAiApi` với `API Key` từ [Jina AI](https://jina.ai/).

- **Telegram**:
  - Tạo `telegramApi` với `Token` từ [@BotFather](https://t.me/BotFather).
  - **Chat ID** của bot có thể lấy từ [this tool](https://api.telegram.org/bot<YOUR_TOKEN>/getUpdates).

- **WordPress**:
  - Tạo `wordpressApi` với:
    - `Username`, `Password`, `URL API`: `https://<your-site>.wordpress.com/wp-json/wp/v2/posts`.

- **Google Drive**:
  - Tạo `googleDriveOAuth2Api` và **cho phép quyền đọc/tải file**.

---

#### **🔹 2. Cấu Hình Node Quan Trọng**
##### **A. Triggers (Bắt Đầu Workflow)**
Workflow có **2 trigger chính**:
1. **Google Drive Trigger**:
   - Dùng để **kích hoạt khi có file mới** trong folder Google Drive (nếu muốn tự động hóa từ file).
   - **Không bắt buộc** nếu dùng **Telegram Trigger** (nhập URL trực tiếp).

2. **Telegram Trigger**:
   - **Cấu hình** trong node **"📥 New Job Link via Telegram"**:
     - **Chat ID**: ID của bot Telegram (lấy từ [this tool](https://api.telegram.org/bot<YOUR_TOKEN>/getUpdates)).
     - **Message**: Nhập URL tin tuyển dụng (ví dụ: `https://linkedin.com/jobs/view/123456789`).

##### **B. AI RAG & Trích Xuất Dữ Liệu**
Workflow sử dụng **AI RAG (Retrieval-Augmented Generation)** để trích xuất và hoàn thiện dữ liệu:
- **Default Data Loader**: Đọc file từ Google Drive.
- **Recursive Character Text Splitter**: Chia văn bản thành các chunk nhỏ.
- **Embeddings OpenAI**: Chuyển văn bản thành vector cho Supabase.
- **Supabase Vector Store**: Lưu vector để AI tìm kiếm và hoàn thiện dữ liệu.
- **AI Agent (LangChain)**: Xử lý logic trích xuất và hoàn thiện tin tuyển dụng.

##### **C. Xử Lý Logo & Đăng Bài WordPress**
- **Download Company Logo**:
  - Node **"📥 Download Company Logo"** sử dụng `httpRequest` để tải logo từ URL công ty.
  - **Cấu hình**:
    - **Method**: `GET`
    - **URL**: `https://<company-website>/logo.png` (trích xuất từ tin tuyển dụng).
    - **Headers**: `Accept: image/png`.

- **Upload Logo to WordPress**:
  - Node **"☁️ Upload Logo to WordPress"** sử dụng `httpRequest` với `wordpressApi`.
  - **Cấu hình**:
    - **Method**: `POST`
    - **URL**: `https://<your-site>.wordpress.com/wp-json/wp/v2/media`
    - **Body**:
      ```json
      {
        "title": "Company Logo",
        "file": "<base64-encoded-image>"
      }
      ```

- **Publish to WordPress**:
  - Node **"🚀 Publish to Your web"** sử dụng `httpRequest` để đăng bài.
  - **Cấu hình**:
    - **Method**: `POST`
    - **URL**: `https://<your-site>.wordpress.com/wp-json/wp/v2/posts`
    - **Body**:
      ```json
      {
        "title": "Job Title",
        "content": "Job Description",
        "status": "publish",
        "featured_media": <media-id-from-logo-upload>
      }
      ```

##### **D. Thông Báo Telegram**
Workflow gửi **thông báo chi tiết** qua Telegram:
- **"notify: processing job"**: Bắt đầu xử lý.
- **"notify: extracting"**: Trích xuất dữ liệu.
- **"notify: success extract"**: Thành công.
- **"notify: error"**: Lỗi (ví dụ URL sai).
- **"Publiched!"**: Đăng bài thành công.

**Cấu hình Telegram**:
- **Message Text**: Sử dụng `{{ $json }}` để hiển thị dữ liệu JSON.
- **Edit Message**: Để cập nhật trạng thái trong cùng một tin nhắn.

---

#### **🔹 3. Kiểm Tra & Test Run**
1. **Nhập URL tin tuyển dụng** vào Telegram (nếu dùng trigger Telegram).
   - Ví dụ: `https://linkedin.com/jobs/view/123456789`.
2. **Chờ workflow chạy** và kiểm tra:
   - **Telegram**: Xem thông báo trạng thái.
   - **WordPress**: Kiểm tra bài đăng mới.
   - **Google Drive**: Kiểm tra file trích xuất (nếu có).
3. **Sửa lỗi** nếu có:
   - **URL sai**: Node **"valid url?"** sẽ gửi thông báo `"notify: wrong url"`.
   - **Dữ liệu thiếu**: Node **"✅ All Fields Available?"** sẽ gửi `"if not valid"`.
   - **Lỗi AI**: Node **"notify: error"** sẽ thông báo lỗi.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
#### **1. Tự Động Hóa Từ File Google Drive**
- **Cấu hình Google Drive Trigger** để workflow chạy khi có file mới trong folder.
- **File CSV** chứa URL tin tuyển dụng (một URL/một dòng).
- **Node "Search File"** sẽ tìm file mới và kích hoạt workflow.

#### **2. Lưu Log & Monitoring**
- **Thêm node "Sticky Note"** để ghi log:
  ```javascript
  // Node "Code" (nếu cần log)
  $node.set("log", $node.input.all()[0].json);
  ```
- **Dùng Telegram** để gửi log chi tiết khi có lỗi.

#### **3. Kết Hợp Với Slack/Email**
- Thay thế **Telegram** bằng **Slack** hoặc **Email** để thông báo:
  - **Slack**: Sử dụng node `slack` với webhook.
  - **Email**: Sử dụng node `email` với SMTP.

#### **4. Cập Nhật Định Kì**
- **Dùng node `setInterval`** (nếu self-hosted) để chạy workflow định kỳ (ví dụ: mỗi 6 giờ) để kiểm tra tin tuyển dụng mới.

#### **5. Cải Thiện AI RAG**
- **Tăng chất lượng vector store** bằng cách:
  - **Thêm dữ liệu huấn luyện** vào Supabase.
  - **Sử dụng model lớn hơn** (ví dụ: `gpt-4` thay vì `gpt-4.1-mini`).

---

## 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp HR khỏi công việc thủ công, **tăng chính xác** nhờ AI, và **hoạt động tự động 24/7**. **Chỉ cần nhập URL**, hệ thống sẽ:
✔ **Trích xuất** tin tuyển dụng.
✔ **Hoàn thiện dữ liệu** bằng AI.
✔ **Tải và upload logo**.
✔ **Đăng bài tự động** lên WordPress.
✔ **Gửi thông báo** qua Telegram.

**Hành động ngay!**
1. **Cài đặt n8n** trên VPS (nếu chưa có).
2. **Import workflow** và cấu hình API keys.
3. **Nhập URL tin tuyển dụng** vào Telegram và **xem kết quả tự động!**

**🚀 Còn chần chừ gì nữa?** Hãy tự động hóa tuyển dụng của bạn **hôm nay**! 🚀

---
**🔗 [Xem workflow gốc](https://n8n.io/workflows/6299)**
**📌 [C