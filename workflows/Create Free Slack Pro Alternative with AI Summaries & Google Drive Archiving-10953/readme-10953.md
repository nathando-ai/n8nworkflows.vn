---
title: "🤖 Tự Động Hóa Slack Pro: Tóm Tắt AI + Lưu Lịch Sử Đơn Vị Theo Dõi Google Drive (Miễn Phí)"
description: "Workflow này giúp các sếp tự động hóa việc tóm tắt AI cho các cuộc trò chuyện Slack và lưu trữ lịch sử kênh hàng tháng vào Google Drive, thay thế chức năng Slack Pro. Tiết kiệm thời gian, đảm bảo tuân thủ và tối ưu hóa công việc nhóm."
slug: "tieu-dong-hoa-slack-pro-ai-summary-google-drive"
tags: [n8n, automation, slack, google-drive, ai-chatbot, no-code, ai-summarization]
keywords: [tự động hóa slack, lưu lịch sử slack google drive, ai tóm tắt cuộc trò chuyện, workflow n8n slack, giải pháp miễn phí thay thế slack pro]
---

# 🚀 **Tự Động Hóa Slack Pro: Tóm Tắt AI + Lưu Lịch Sử Đơn Vị Theo Dõi Google Drive**

## **🔥 Nỗi Đau Của Các Sếp Và Giải Pháp N8N**
Các sếp và quản lý thường gặp phải những vấn đề sau khi làm việc với Slack:
- **Tốn thời gian** để tóm tắt cuộc trò chuyện dài hàng giờ, ngày.
- **Không tuân thủ** vì không lưu trữ lịch sử kênh một cách tự động.
- **Không có AI hỗ trợ** để tổng hợp thông tin quan trọng trong cuộc hội thoại.
- **Chi phí cao** khi sử dụng Slack Pro với tính năng tóm tắt và lưu trữ.

**Workflow này giải quyết tất cả bằng:**
✅ **Tóm tắt AI tự động** khi nhắc bot trong Slack (ví dụ: `@bot summarize past 3days`).
✅ **Lưu lịch sử kênh hàng tháng** vào Google Drive (thay thế Slack Pro).
✅ **Tự động hóa 100%** không cần code.
✅ **Miễn phí** (chỉ cần Slack API, Google Drive và một API LLM miễn phí).

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: AI tự động tóm tắt cuộc trò chuyện trong giây lát.
- **Tuân thủ pháp lý**: Lưu trữ lịch sử kênh hàng tháng vào Google Drive.
- **Cá nhân hóa**: Bot hiểu yêu cầu của bạn (ví dụ: "tóm tắt 3 ngày qua").
- **Hoạt động liên tục**: Dữ liệu được lưu trữ tự động mỗi tháng.
- **Miễn phí**: Không cần mua Slack Pro.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Slack**:
   - **Slack App/Bot** với quyền:
     - `channels:history` (đọc lịch sử kênh).
     - `chat:write` (gửi tin nhắn).
   - Bot đã được **thêm vào các kênh** muốn tóm tắt/luu trữ.
   - **Slack API Token** (tạo tại [Slack API](https://api.slack.com/apps)).

2. **Google Drive**:
   - **Tài khoản Google** và **API Key** (tạo tại [Google Cloud Console](https://console.cloud.google.com/)).
   - **Folder "Slack History"** (để lưu trữ file JSON lịch sử kênh).

3. **API LLM (AI)**:
   - **Google Gemini API** (miễn phí trong giới hạn) hoặc **DeepSeek API** (nếu muốn thay thế).
   - **API Key** của Google Gemini (tạo tại [Google AI Studio](https://ai.google.dev/)).

4. **n8n Instance**:
   - **Self-hosted n8n** (khuyến nghị) hoặc n8n Cloud (miễn phí cho thử nghiệm).
   - **Nodes bổ sung**:
     - `@n8n/n8n-nodes-langchain` (để sử dụng AI Agent).
     - `@n8n/n8n-nodes-base.googleDrive` (để lưu file).
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. Tải file JSON của workflow từ [n8n.io/workflows/10953](https://n8n.io/workflows/10953).
2. Mở **n8n Editor** → Nhấn **"Import"** → Chọn file JSON vừa tải.
3. Chọn **"Import"** để hoàn tất.

#### **Phương pháp 2: Copy/Paste JSON**
1. Mở **n8n Editor** → Nhấn **"Import"** → Chọn **"Paste JSON"**.
2. Copy toàn bộ nội dung JSON từ [n8n.io/workflows/10953](https://n8n.io/workflows/10953) và dán vào.
3. Nhấn **"Import"** để hoàn tất.

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **2 phần chính**:
- **Phần AI Tóm Tắt** (khi nhắc bot trong Slack).
- **Phần Lưu Lịch Sử Hàng Tháng** (scheduled).

#### **A. Cấu Hình Slack API**
1. **Tạo Credential Slack**:
   - Trong n8n Editor → **"Credentials"** → **"Add"** → Chọn **"Slack"**.
   - Điền:
     - **API Token**: Token từ Slack App (tạo tại [Slack API](https://api.slack.com/apps)).
     - **Bot Token**: Token của bot (nếu khác với API Token).
     - **Workspace URL**: `https://<tên-tài-khoản>.slack.com`.

2. **Kiểm tra quyền**:
   - Bot phải có quyền `channels:history` và `chat:write`.
   - Bot phải được thêm vào **tất cả kênh** muốn tóm tắt.

#### **B. Cấu Hình Google Drive**
1. **Tạo Credential Google Drive**:
   - Trong n8n Editor → **"Credentials"** → **"Add"** → Chọn **"Google Drive"**.
   - Điền:
     - **Client ID** và **Client Secret**: Từ [Google Cloud Console](https://console.cloud.google.com/).
     - **Refresh Token**: Lấy từ [Google OAuth Playground](https://developers.google.com/oauthplayground/).
     - **Folder ID**: ID của folder "Slack History" (lấy từ liên kết Google Drive).

2. **Kiểm tra quyền**:
   - Folder "Slack History" phải được chia sẻ với tài khoản n8n.

#### **C. Cấu Hình AI (Google Gemini)**
1. **Tạo Credential Google Palm API**:
   - Trong n8n Editor → **"Credentials"** → **"Add"** → Chọn **"Google Palm API"**.
   - Điền:
     - **API Key**: Từ [Google AI Studio](https://ai.google.dev/).

2. **Cấu hình AI Agent**:
   - Trong node **"Slack Channel Summary AI Agent"**:
     - Chọn **Model**: `gemini-pro` (hoặc model khác của Google).
     - Điền **Prompt** (nếu cần chỉnh sửa):
       ```plaintext
       You are a helpful assistant that summarizes Slack channel conversations.
       When given a Slack channel history, extract key points, decisions, and action items.
       Format the summary in a clear, bullet-point style.
       ```

#### **D. Cấu Hình Schedule (Lưu Lịch Sử Hàng Tháng)**
1. Trong node **"Monthly Export Schedule Trigger"**:
   - Chọn **Schedule**: `0 0 1 * *` (lưu vào ngày 1 hàng tháng).
   - **Timezone**: Chọn timezone phù hợp (ví dụ: `Asia/Ho_Chi_Minh`).

2. **Kiểm tra folder Google Drive**:
   - Đảm bảo folder "Slack History" đã được tạo và chia sẻ.

---

### **3. Kích Hoạt ⚡️**
1. **Test Run Phần AI Tóm Tắt**:
   - Nhắn tin trong Slack: `@<tên-bot> summarize past 3days`.
   - Kiểm tra nếu bot trả lời tóm tắt AI.

2. **Test Run Phần Lưu Lịch Sử**:
   - Chạy **Manual Trigger** của node **"Monthly Export Schedule Trigger"**.
   - Kiểm tra Google Drive có file JSON lịch sử kênh không.

3. **Bật Active Workflow**:
   - Nhấn **"Active"** trên workflow để nó hoạt động tự động.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Thêm Slack Notifications**:
   - Sau khi lưu lịch sử vào Google Drive, gửi thông báo Slack thông báo:
     ```json
     {
       "text": "📁 Lịch sử kênh đã được lưu vào Google Drive: [LINK]",
       "attachments": [
         {
           "title": "Slack History Backup",
           "text": "File đã được lưu vào folder 'Slack History'",
           "color": "#36a64f"
         }
       ]
     }
     ```

2. **Lưu Log Lịch Sử**:
   - Sử dụng node **Sticky Note** để lưu log các lỗi hoặc thành công:
     ```json
     {
       "channel": "$channel",
       "message": "🔄 Lịch sử kênh {{ $node["Get Slack Channel History for Export"].json["channel"]["name"] }} đã được lưu thành công!"
     }
     ```

3. **Kết hợp với Telegram/Email**:
   - Sử dụng node **HTTP Request** để gửi báo cáo hàng tháng về Telegram hoặc Email:
     ```json
     {
       "url": "https://api.telegram.org/bot<BOT_TOKEN>/sendMessage",
       "method": "POST",
       "body": {
         "chat_id": "<CHAT_ID>",
         "text": "📊 Báo cáo lưu lịch sử Slack tháng {{ $date.now("YYYY-MM") }}"
       }
     }
     ```

4. **Chỉnh sửa Prompt AI**:
   - Nếu muốn AI tóm tắt theo cách riêng, chỉnh sửa **Prompt** trong node **"LLM for Message Summaries"**:
     ```plaintext
     Tóm tắt cuộc trò chuyện Slack này với các yêu cầu sau:
     1. Trích xuất các quyết định quan trọng.
     2. Danh sách nhiệm vụ cần thực hiện.
     3. Các link và tài liệu tham khảo.
     ```

---

## 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** để tự động hóa Slack Pro, giúp các sếp:
✔ **Tiết kiệm thời gian** với AI tóm tắt tự động.
✔ **Tuân thủ pháp lý** bằng việc lưu lịch sử kênh hàng tháng.
✔ **Không cần chi phí** (so với Slack Pro).

**Hành động ngay!**
1. Import workflow vào n8n.
2. Cấu hình Slack, Google Drive và AI.
3. Bật **Active** và bắt đầu tự động hóa!

**Nếu gặp vấn đề, liên hệ tác giả:**
📧 **OwenLee**: [owenlzyxg@gmail.com](mailto:owenlzyxg@gmail.com)

---
**🚀 Cùng tự động hóa công việc Slack của bạn ngay hôm nay!**