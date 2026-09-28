---
title: "🚀 Tự Động Hóa Tạo & Đăng Bài LinkedIn Từ URL Với Telegram, AI Gemini & Google Sheets (Không Cần Code)"
description: "Workflow n8n này giúp các marketer tự động chuyển đổi nội dung từ URL thành bài LinkedIn chuyên nghiệp, kiểm duyệt bằng AI, và đăng trực tiếp từ Telegram - tiết kiệm thời gian lên đến 80% so với cách làm thủ công."
slug: "tu-dong-hoa-tao-dang-bai-linkedin-tu-url-voi-telegram-ai-gemini"
tags: [n8n, automation, content-creation, ai-gemini, linkedin-automation, telegram-bot, google-sheets]
keywords: [tự động hóa bài LinkedIn, tạo bài LinkedIn từ URL, AI Gemini cho LinkedIn, tự động đăng bài LinkedIn, workflow n8n content marketing, tự động hóa marketing không code]
---

# 🚀 **Tự Động Hóa Tạo & Đăng Bài LinkedIn Từ URL Với Telegram, AI Gemini & Google Sheets**

## **Giải Pháp Cho Những Người Bận Rộn: Đăng Bài LinkedIn Chỉ Với Một Câu Lệnh Telegram!**

Hãy tưởng tượng: Bạn chỉ cần gửi một URL hoặc đoạn văn bản lên Telegram, workflow tự động:
✅ **Trích xuất & tổng hợp nội dung** từ trang web (nếu có URL).
✅ **Tạo bài LinkedIn hoàn chỉnh** bằng AI Gemini (hoặc Groq làm backup).
✅ **Kiểm duyệt chất lượng** bằng AI để đảm bảo bài viết phù hợp với brand.
✅ **Yêu cầu phê duyệt cuối cùng** từ bạn qua Telegram.
✅ **Đăng bài tự động** lên LinkedIn và cập nhật trạng thái trong Google Sheets.

**Không cần viết code, không cần kiến thức kỹ thuật - chỉ cần một workflow n8n được cài đặt sẵn!**

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tạo và đăng bài chỉ trong vài phút thay vì 30-60 phút thủ công.
- **Chất lượng bài viết cao**: AI Gemini tự động tối ưu nội dung, tránh lỗi ngữ pháp và nội dung nhạt nhẽo.
- **Kiểm soát hoàn toàn**: Phê duyệt bài viết cuối cùng qua Telegram trước khi đăng.
- **Danh sách bài viết quản lý**: Tất cả bài viết được lưu trong Google Sheets với trạng thái (chờ, đã đăng, bị từ chối).
- **Hoạt động 24/7**: Workflow chạy tự động, không phụ thuộc vào giờ làm việc của bạn.
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Telegram**:
   - Bot Telegram với **Token API** (đăng ký tại [@BotFather](https://t.me/BotFather)).
   - Chat riêng với bot để gửi lệnh (ví dụ: `/start` để bắt đầu).

2. **Google Sheets**:
   - Một bảng Google Sheets với **các cột sau** (cần tạo trước):
     - `URL` (địa chỉ bài viết nguồn)
     - `Draft` (nội dung bài LinkedIn)
     - `Status` (trạng thái: `unpublished`, `published`, `rejected`)
     - `PublishedAt` (thời gian đăng, dạng timestamp).
   - **Chia sẻ quyền** cho n8n với vai trò "Editor" trên bảng này.
   - **ID Sheet** (tham khảo [hướng dẫn lấy ID Google Sheets](https://support.google.com/docs/answer/10731637)).

3. **Tài khoản LinkedIn**:
   - Tài khoản LinkedIn cá nhân hoặc doanh nghiệp (n8n sẽ đăng bài với quyền này).
   - **OAuth 2.0 API Key** của LinkedIn (cần đăng ký tại [LinkedIn Developer Portal](https://www.linkedin.com/developers/)).

4. **API Keys cho AI**:
   - **Google Gemini API** (miễn phí với giới hạn 1M token/tháng):
     - Đăng ký tại [Google AI Studio](https://aistudio.google/).
     - Lấy `API Key` từ [Google Cloud Console](https://console.cloud.google.com/).
   - **Groq API** (làm backup cho Gemini, miễn phí với giới hạn 50k token/tháng):
     - Đăng ký tại [Groq](https://groq.com/).
     - Lấy `API Key` từ Dashboard.

5. **n8n Self-Hosted**:
   :::info[Gợi ý hạ tầng cho n8n]
   Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
   :::
---
---

## 🚀 **Cách Import & Cấu Hình Workflow**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/15926](https://n8n.io/workflows/15926) (chọn "Download JSON").
2. **Mở n8n Editor** (trang chủ của n8n sau khi cài đặt).
3. Nhấn **"Import"** và chọn file JSON vừa tải.
4. Chọn **"Create Workflow"** để tạo bản sao.

#### **Phương pháp 2: Copy/Paste JSON**
1. Mở n8n Editor.
2. Nhấn **"Create Workflow"** → **"Import Workflow"** → **"Paste JSON"**.
3. Dán toàn bộ JSON từ [n8n.io/workflows/15926](https://n8n.io/workflows/15926) (chọn "Raw" trên trang workflow).
4. Nhấn **"Import"** để tạo workflow.

---
### **2. Các Bước Cấu Hình BẮT BUỘC 📌**

#### **A. Cấu Hình Credentials (Tài Khoản)**
Workflows sử dụng **7 loại credentials** chính. Các sếp cần thiết lập chúng trong **n8n Settings → Credentials**:

| **Loại Credentials**       | **Tham Số Cần Điền**                          | **Hướng Dẫn Lấy**                                                                 |
|----------------------------|-----------------------------------------------|-----------------------------------------------------------------------------------|
| `telegramApi`              | `token` (Token API của bot Telegram)          | [@BotFather](https://t.me/BotFather) → `/gettoken`                                  |
| `googleSheetsOAuth2Api`    | `clientId`, `clientSecret`, `refreshToken`   | [Google Sheets API](https://developers.google.com/sheets/api/quickstart/nodejs)   |
| `linkedInOAuth2Api`        | `clientId`, `clientSecret`, `refreshToken`   | [LinkedIn Developer Portal](https://www.linkedin.com/developers/)                 |
| `googlePalmApi`            | `apiKey` (Google Gemini API)                 | [Google Cloud Console](https://console.cloud.google.com/)                         |
| `groqApi`                  | `apiKey` (Groq API)                          | [Groq Dashboard](https://groq.com/)                                               |

**Lưu ý**:
- Đối với **Google Sheets** và **LinkedIn**, các sếp cần **refresh token** sau khi đăng ký OAuth 2.0.
- Đối với **Google Gemini**, các sếp cần **bật API** trong Google Cloud Console và tạo `apiKey`.

---

#### **B. Cấu Hình Node Quản Lý Google Sheets**
Workflows sử dụng **Google Sheets** để lưu trữ danh sách bài viết. Các sếp cần chỉnh sửa **2 node quan trọng**:

1. **Node `Fetch Unpublished Records`** (trong branch Database Queue Processing):
   - **Tham số `sheetId`**: Điền **ID Sheet** của bảng Google Sheets (ví dụ: `1AbCdEfGhIjKlMnOpQrStUvWxYz`).
   - **Tham số `sheetName`**: Điền tên tab trong Sheet (ví dụ: `LinkedIn_Posts`).

2. **Node `Insert Sheet Record`** và `Update Sheet Record`:
   - **Tham số `sheetId` và `sheetName`**: Giống như trên.
   - **Cột bắt buộc**:
     - `URL` (địa chỉ bài viết nguồn).
     - `Draft` (nội dung bài LinkedIn).
     - `Status` (trạng thái: `unpublished`, `published`, `rejected`).

**Hướng dẫn lấy ID Sheet**:
1. Mở Google Sheets của bạn.
2. Trong URL, ID Sheet là chuỗi số và chữ cái giữa `/d/` và `/edit` (ví dụ: `https://docs.google.com/spreadsheets/d/1AbCdEfGhIjKlMnOpQrStUvWxYz/edit` → ID là `1AbCdEfGhIjKlMnOpQrStUvWxYz`).

---

#### **C. Cấu Hình Node Telegram**
Workflows sử dụng **Telegram** để:
- Nhận lệnh từ người dùng (ví dụ: `/start`, `/generate`).
- Gửi thông báo phản hồi (thành công/thất bại).

**Các node cần chú ý**:
1. **Node `Listen For Telegram`**:
   - **Tham số `chatId`**: Điền **ID Chat** của bot (lấy từ Telegram: `@username` → mở chat → nhấn `Copy chat ID`).
   - **Tham số `token`**: Điền Token API từ `telegramApi` (đã cấu hình ở trên).

2. **Node `Request URL Input`** và `Ask Execution Approval`:
   - **Tham số `message`**: Có thể chỉnh sửa để phù hợp với brand (ví dụ: thay `Nhập URL bài viết` thành `Gửi link bài viết cần chuyển đổi`).

---

#### **D. Cấu Hình Node LinkedIn**
Workflows sử dụng **LinkedIn API** để đăng bài. Các sếp cần:
1. **Đăng ký OAuth 2.0** tại [LinkedIn Developer Portal](https://www.linkedin.com/developers/).
2. **Cấu hình `linkedInOAuth2Api`** trong n8n với:
   - `clientId`, `clientSecret`, `refreshToken`.
3. **Node `Publish LinkedIn Post`**:
   - **Tham số `text`**: Nội dung bài viết (tự động lấy từ `Draft` trong Google Sheets).
   - **Tham số `imageUrl` (nếu có)**: Nếu muốn thêm hình ảnh, điền URL hình.

---
### **3. Kích Hoạt Workflow ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Gửi lệnh `/start` đến bot Telegram.
   - Chọn **branch "Direct Draft Generation"** để thử tạo bài từ URL hoặc văn bản.
   - Kiểm tra các thông báo phản hồi trên Telegram.

2. **Bật Active**:
   - Nhấn **"Active"** trên workflow trong n8n Editor.

---
---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**

### **1. Tối Ưu Hóa AI với Prompt Cụ Thể**
Workflows sử dụng **AI Gemini** để tạo bài viết. Các sếp có thể **cải thiện chất lượng** bằng cách:
- **Chỉnh sửa Prompt** trong node `Primary Post Creation Model`:
  ```json
  {
    "prompt": "Tạo một bài LinkedIn chuyên nghiệp về chủ đề [TITLE] từ nội dung trang web [URL]. Bài viết phải:
    - Có độ dài 500-800 từ.
    - Có tiêu đề hấp dẫn và mô tả ngắn (meta description).
    - Sử dụng từ khóa: [KEYWORDS].
    - Có cấu trúc: Mở đầu (hook), nội dung chi tiết, kết luận (CTA).
    - Tránh lặp lại, viết tự nhiên như người viết bài."
  }
  ```
- **Thêm ví dụ** trong Prompt để AI hiểu rõ hơn về phong cách viết của brand.

### **2. Kết Nối Với Slack/Email**
Ngoài Telegram, các sếp có thể **thêm thông báo đến Slack hoặc Email**:
- **Thêm node `slack`** sau các node `Notify Publish Success` hoặc `Alert QC Failure`.
- **Cấu hình Webhook Slack** tại [API Slack](https://api.slack.com/messaging/composing).

### **3. Lưu Log Chi Tiết**
Để theo dõi hoạt động của workflow, các sếp có thể:
- **Thêm node `stickyNote`** để ghi chú lỗi hoặc thành công.
- **Cập nhật Google Sheets** với thêm cột `Log` để lưu trữ chi tiết.

### **4. Chạy Batch Processing**
Đối với **danh sách bài viết lớn**, các sếp có thể:
1. **Chọn branch "Database Queue Processing"**.
2. **Cập nhật Google Sheets** với danh sách URL cần xử lý.
3. **Gửi lệnh `/process`** đến Telegram để workflow tự động xử lý tất cả.

### **5. Sử Dụng Fallback AI**
Nếu **Gemini API bị lỗi**, workflow sẽ tự động chuyển sang **Groq API** (node `Fallback Post Generation Model`). Các sếp có thể:
- **Điều chỉnh thứ tự ưu tiên** trong node `switch` để Groq hoạt động trước nếu muốn.
- **Cập nhật API Key Groq** để đảm bảo fallback hoạt động.

---
---

## 📌 **Kết Luận: Đăng Bài LinkedIn Chỉ Với Một Câu Lệnh!**

Workflow này **giải phóng thời gian** cho các sếp từ việc viết bài thủ công, đồng thời **đảm bảo chất lượng** nhờ AI Gemini và kiểm duyệt tự động. Với **Telegram làm trung tâm điều khiển**, bạn có thể:
✅ **Tạo bài từ URL** chỉ trong vài giây.
✅ **Phê duyệt cuối cùng** qua Telegram.
✅ **Đăng bài tự động** lên LinkedIn.
✅ **Quản lý danh sách bài viết** trong Google Sheets.

**Hành động ngay hôm nay!**
1. **Cài đặt n8n Self-Hosted** trên VPS (dùng mã giảm giá **VPSN8N**).
2. **Import workflow** và cấu hình credentials.
3. **Gửi lệnh `/start`** đến Telegram và bắt đầu tự động hóa!

**🚀 Câu hỏi thường gặp:**
- **Workflow có chạy được với API miễn phí không?**
  ✅ Có, với giới hạn của Google Gemini (1M token/tháng) và Groq (50k token/tháng).
- **Có thể thay đổi AI khác không?**
  ✅ Có, chỉ cần thay thế `googlePalmApi` và `groqApi` với OpenAI hoặc Anthropic.
- **Làm sao