---
title: "🤖 **Explorium AI Assistant: Bot Trợ Lý BI Tự Động Hóa Trên Slack Với Claude AI & Explorium MCP**"
description: "Tự động hóa việc trả lời các câu hỏi Business Intelligence (BI) phức tạp trên Slack bằng AI Claude 4.5 và công cụ Explorium MCP, giúp các sếp tiết kiệm thời gian tìm kiếm thông tin và cải thiện hiệu suất hỗ trợ khách hàng. Workflow này hoạt động 24/7, trả lời chính xác và cá nhân hóa dựa trên dữ liệu thực tế."
slug: "explorium-ai-assistant-slack-claude-ai"
tags: [n8n, automation, ai-chatbot, business-intelligence, slack-bot, claude-ai, explorium-mcp]
keywords: [n8n workflow slack bot, tự động hóa hỗ trợ khách hàng, AI Claude 4.5 cho Slack, Explorium MCP API, chatbot BI tự động, giải pháp hỗ trợ 24/7]
---

# 🚀 **Explorium AI Assistant: Bot Trợ Lý BI Tự Động Hóa Trên Slack**

## **🔍 Nỗi Đau Của Các Sếp Và Giải Pháp Tự Động Hóa**
Các sếp thường phải mất **giờ đồng hồ** để trả lời các câu hỏi liên quan đến **Business Intelligence (BI)** như:
- *"Tìm các công ty tech ở SF có từ 50-200 nhân viên"*
- *"Hiển thị công nghệ stack của Microsoft"*
- *"Lấy danh sách CMO của các công ty y tế"*

Thông thường, việc này đòi hỏi phải **quét qua nhiều bảng Excel, CRM, hoặc API** trước khi có được kết quả chính xác. **Explorium AI Assistant** là giải pháp **tự động hóa 100% không cần code**, kết hợp **AI Claude 4.5** và **Explorium MCP** để trả lời nhanh chóng, chính xác và **cá nhân hóa** dựa trên dữ liệu thực tế.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
✅ **Tiết kiệm thời gian** – Trả lời ngay lập tức thay vì mất giờ tìm kiếm.
✅ **Chính xác 100%** – Dữ liệu từ **Explorium MCP** (công cụ BI chuyên nghiệp).
✅ **Hỗ trợ 24/7** – Bot hoạt động liên tục, không cần nhân viên.
✅ **Cá nhân hóa** – Trả lời dựa trên **bối cảnh hội thoại** (thread) trên Slack.
✅ **Tích hợp AI Claude 4.5** – Trả lời thông minh, logic và chi tiết.
:::

---
### **🔧 Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI LẮP ĐẶT**]
✔ **Tài khoản Slack Workspace** (có quyền admin để tạo Bot).
✔ **API Key Anthropic** (để sử dụng Claude AI).
✔ **API Key Explorium** (để truy cập **Explorium MCP**).
✔ **n8n Self-hosted** (để workflow chạy 24/7 ổn định).
:::

---
## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/9935](https://n8n.io/workflows/9935).
- **Mở n8n Editor** → **Import Workflow** → Chọn file JSON.
- **Hoặc copy/paste** JSON vào **Create New Workflow** → **Import JSON**.

---
### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
#### **🔹 1. Cấu Hình Slack Trigger (Node "Slack Trigger")**
- **Tạo Slack App** theo hướng dẫn dưới đây.
- **Thêm Credential Slack**:
  - **Token**: Dùng **Bot User OAuth Token** (xoxb-...) từ Slack App.
  - **Webhook URL**: Dùng URL từ **Slack Trigger** trong n8n để đăng ký trong **Event Subscriptions** của Slack.

#### **🔹 2. Cấu Hình Anthropic Claude AI (Node "Anthropic Chat Model")**
- **Thêm Credential Anthropic**:
  - **API Key**: Nhập **API Key** từ [Anthropic Dashboard](https://www.anthropic.com/api).
  - **Model**: Chọn **claude-haiku-4-5-20251001** (hoặc thay thế bằng model khác).

#### **🔹 3. Cấu Hình Explorium MCP (Node "Explorium MCP")**
- **Endpoint**: `https://mcp.explorium.ai/mcp`
- **Header Auth**:
  - **Key**: `Authorization`
  - **Value**: `Bearer <API_KEY_EXPLORIUM>` (nhập từ Explorium).

#### **🔹 4. Kiểm Tra Node "Send a message" (Slack)**
- **Chọn Credential Slack** tương tự như **Slack Trigger**.
- **Channel/Thread**: Bot sẽ tự động trả lời trên **thread** hoặc **channel** tương ứng.

---
### **3. Kích Hoạt ⚡️**
- **Test Run** với dữ liệu mẫu:
  - Gửi tin nhắn `@Bot` trong Slack với câu hỏi như:
    - `@Bot tìm công ty tech ở SF có 50-200 nhân viên`
    - `@Bot hiển thị công nghệ stack của Microsoft`
- **Bật Active** workflow sau khi kiểm tra thành công.

---
## **📌 Hướng Dẫn Tạo Slack App (Bắt Buộc)**
:::note[**BƯỚC 1: Tạo Slack App**]
1. Truy cập [api.slack.com/apps](https://api.slack.com/apps).
2. Nhấn **Create New App** → **From scratch**.
3. Đặt tên (ví dụ: **"Explorium AI Assistant"**) và chọn **Workspace**.
:::

:::note[**BƯỚC 2: Cấu Hình Bot Permissions**]
- Vào **OAuth & Permissions** → **Bot Token Scopes**.
- Thêm các **scope** sau:
  ```plaintext
  app_mentions:read
  channels:history
  channels:read
  chat:write
  emoji:read
  groups:history
  groups:read
  im:history
  im:read
  mpim:history
  mpim:read
  reactions:read
  users:read
  ```
:::

:::note[**BƯỚC 3: Enable Event Subscriptions**]
1. Vào **Event Subscriptions** → **Enable Events**.
2. Nhập **Request URL** từ node **Slack Trigger** trong n8n.
3. Chọn **Subscribe to bot events**:
   - `app_mention`
   - `message.channels`
   - `message.groups`
   - `message.im`
   - `message.mpim`
   - `reaction_added`
:::

:::note[**BƯỚC 4: Install App**]
1. Vào **Install App** → **Install to Workspace**.
2. **Copy Bot User OAuth Token** (dạng `xoxb-...`) → Dùng trong n8n.
:::

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**
:::tip[**1. Tích Hợp Log & Monitoring**]
- Sử dụng **n8n-nodes-base.stickyNote** để ghi log các câu hỏi và phản hồi.
- **Kết hợp với Google Sheets** để lưu lịch sử hội thoại.

:::tip[**2. Cải Thiện Trải Nghiệm với Slack**]
- **Tạo shortcut** cho Bot trong Slack (ví dụ: `/explorium`).
- **Tích hợp với Notion/Confluence** để cập nhật dữ liệu mới.

:::tip[**3. Sử Dụng AI Khác Nhau**]
- Thay thế **Claude AI** bằng **GPT-4** (OpenAI) hoặc **Gemini** (Google).
- Cấu hình **multi-model** để bot linh hoạt hơn.

:::tip[**4. Tự Động Gửi Báo Cáo**]
- Sử dụng **n8n-nodes-base.email** để gửi báo cáo hàng tuần về **câu hỏi phổ biến** cho team.

---
## **📌 Kết Luận**
**Explorium AI Assistant** là **giải pháp hoàn hảo** để tự động hóa việc trả lời **câu hỏi BI phức tạp** trên Slack, giúp các sếp **tiết kiệm thời gian, tăng hiệu suất và cải thiện trải nghiệm khách hàng**.

**👉 Bắt đầu ngay!**
1. **Tạo Slack App** và **cấu hình n8n**.
2. **Import workflow** và **kích hoạt**.
3. **Test với câu hỏi mẫu** và **cải tiến liên tục**.

**🎁 Đăng ký VPS TinoHost để self-host n8n ổn định 24/7:**
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)

---
**🚀 Chúc các sếp thành công với AI Automation!** 🚀