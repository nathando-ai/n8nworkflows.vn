---
title: "🚀 Tự Động Hóa Tạo & Đăng Bài Nội Dung Tiếng Thái Trên Telegram & Website Với Ollama, Gemini & AI Multimodal"
description: "Workflow tự động hóa hoàn toàn không cần code để tạo nội dung bài viết tiếng Thái chất lượng cao, tự động sinh ảnh minh họa, và đăng tải lên website hoặc Telegram. Giúp các sếp tiết kiệm thời gian lên đến 80% trong việc content marketing."
slug: "tieu-dong-hoa-tao-dang-bai-noi-dung-thai-voi-ollama-gemini-telegram"
tags: [n8n, automation, content-creation, ai-multimodal, ollama, google-gemini, telegram-bot]
keywords: [tự động hóa tạo bài viết tiếng Thái, n8n workflow content marketing, AI sinh ảnh tự động, đăng bài tự động Telegram, Ollama Gemini tự động hóa]
---

# 🚀 **Tự Động Hóa Tạo & Đăng Bài Nội Dung Tiếng Thái Với AI Ollama, Gemini & Telegram**

### **Giải pháp cho các sếp muốn:**
- **Tạo nội dung bài viết tiếng Thái chất lượng cao** mà không cần viết tay.
- **Tự động sinh ảnh minh họa** phù hợp với bài viết.
- **Đăng tải tự động lên website hoặc Telegram** mà không cần can thiệp thủ công.
- **Tiết kiệm thời gian lên đến 80%** trong việc content marketing.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính riêng tư và hiệu suất tối ưu.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tạo nội dung bài viết tiếng Thái tự động** với chất lượng cao, phù hợp SEO và marketing.
✅ **Sinh ảnh minh họa AI** (cả ảnh thực và ảnh sinh tổng hợp) phù hợp với nội dung bài viết.
✅ **Đăng tải tự động lên website hoặc Telegram** mà không cần can thiệp thủ công.
✅ **Tiết kiệm thời gian lên đến 80%** so với cách làm thủ công.
✅ **Hoạt động liên tục 24/7** mà không cần giám sát.
✅ **Cá nhân hóa nội dung** dựa trên dữ liệu từ Google Sheets.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Ollama** (để sử dụng mô hình AI `llama3:latest`).
2. **API Key Ollama** (để kết nối với `ollamaApi`).
3. **Tài khoản Telegram Bot** (để gửi thông báo tự động).
4. **Token Telegram API** (để kết nối với `telegramApi`).
5. **Tài khoản Google Sheets** (để đọc dữ liệu tin tức từ `googleSheetsTriggerOAuth2Api`).
6. **API Key Google Gemini** (để sinh ảnh từ mô hình AI).
7. **URL Website** (để đăng tải bài viết tự động).
8. **File cấu hình (nếu có)** cho việc sinh ảnh (ví dụ: kích thước, phong cách).

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Mở **n8n Workflow Editor**.
2. Nhấn **Import Workflow** và chọn file JSON từ [đây](https://n8n.io/workflows/5818) (hoặc copy JSON từ link trên).
3. Hoặc **copy/paste** JSON từ link trên vào ô **Import Workflow**.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Sau khi import, các sếp cần cấu hình các node quan trọng sau:

#### **A. Cấu hình Ollama (`ollamaApi`)**
- Đi đến **Credentials** → **Add Credential** → **Ollama API**.
- Nhập **API Key** từ tài khoản Ollama của mình.
- Chọn mô hình `llama3:latest` trong các node `lmOllama`.

#### **B. Cấu hình Telegram (`telegramApi`)**
- Đi đến **Credentials** → **Add Credential** → **Telegram**.
- Nhập **Token API** từ tài khoản Telegram Bot.
- Nhập **Chat ID** của nhóm hoặc cá nhân muốn nhận thông báo.

#### **C. Cấu hình Google Sheets (`googleSheetsTriggerOAuth2Api`)**
- Đi đến **Credentials** → **Add Credential** → **Google Sheets OAuth2**.
- Theo hướng dẫn của Google để cấp quyền truy cập.
- Chọn **Sheet Name** và **Range** trong node `googleSheetsTrigger`.

#### **D. Cấu hình API Google Gemini**
- Trong node `HTTP Request` (đối với `Google Gemini: Generate Photo` và `Google Gemini: Generate Risoprint Image`), nhập:
  - **URL API**: `https://generativeai.googleapis.com/v1beta/models/gemini-pro:generateContent`
  - **Headers**:
    ```json
    {
      "Content-Type": "application/json",
      "Authorization": "Bearer YOUR_GEMINI_API_KEY"
    }
    ```
  - **Body**:
    ```json
    {
      "contents": [
        {
          "parts": [
            {
              "text": "Generate a high-quality image for a blog post about [topic]. Style: professional, modern, and visually appealing."
            }
          ]
        }
      ]
    }
    ```

#### **E. Cấu hình HTTP Request (Đăng tải lên Website)**
- Trong node `HTTP Request: Post to Website`, nhập:
  - **URL API** của website (ví dụ: `https://website.com/api/posts`).
  - **Headers** (nếu cần):
    ```json
    {
      "Content-Type": "application/json",
      "Authorization": "Bearer YOUR_WEBSITE_API_KEY"
    }
    ```
  - **Body** (dữ liệu bài viết):
    ```json
    {
      "title": "{{ $node["Function: Prepare Post Data"].json()["title"] }}",
      "content": "{{ $node["Function: Prepare Post Data"].json()["content"] }}",
      "imageUrl": "{{ $node["Function: Attach Image Binary"].json()["imageUrl"] }}"
    }
    ```

#### **F. Cấu hình File Handling (Local)**
- Nếu lưu ảnh vào **local disk**, cần cấu hình node `readWriteFile`:
  - **File Path**: `/path/to/your/folder/images/`
  - **File Name**: `{{ $node["Function: Image Type Analyzer"].json()["imageName"] }}.png`

---

### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **Run Workflow** và kiểm tra kết quả.
   - Đảm bảo bài viết và ảnh được sinh thành công.
2. **Bật Active Workflow**:
   - Sau khi kiểm tra thành công, chuyển trạng thái workflow thành **Active**.

---

## ✍️ **Mẹo & gợi ý nâng cao**
1. **Tích hợp với Slack/Email**:
   - Thêm node `n8n-nodes-base.slack` hoặc `n8n-nodes-base.email` để gửi thông báo khi bài viết được đăng tải.

2. **Lưu log hoạt động**:
   - Thêm node `n8n-nodes-base.writeFile` để lưu lịch sử hoạt động vào file CSV hoặc JSON.

3. **Tự động gửi báo cáo định kỳ**:
   - Sử dụng node `n8n-nodes-base.cron` để chạy workflow hàng ngày/tuần và gửi báo cáo qua Telegram/Email.

4. **Cải thiện chất lượng ảnh**:
   - Thêm node `n8n-nodes-base.imageProcessing` để điều chỉnh kích thước, chất lượng ảnh trước khi đăng tải.

5. **Duy trì dữ liệu tin tức**:
   - Cập nhật thường xuyên dữ liệu trong Google Sheets để workflow luôn có nội dung mới.

---

## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa toàn bộ quy trình tạo và đăng bài nội dung tiếng Thái. Với sự hỗ trợ của **Ollama, Gemini và Telegram**, các sếp có thể:
✔ **Tiết kiệm thời gian** lên đến 80%.
✔ **Tăng hiệu suất content marketing** với nội dung chất lượng cao.
✔ **Hoạt động liên tục 24/7** mà không cần giám sát.

**Hãy áp dụng ngay workflow này và bắt đầu tự động hóa content của mình!** 🚀

---
**Ghi chú:** Nếu gặp vấn đề trong quá trình cấu hình, các sếp có thể tham khảo [hướng dẫn chi tiết của tác giả](https://n8n.io/workflows/5818) hoặc liên hệ cộng đồng n8n để hỗ trợ.