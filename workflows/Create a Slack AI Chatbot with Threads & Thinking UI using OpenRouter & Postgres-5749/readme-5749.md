---
title: "🤖 Tạo Chatbot AI Trả Lời Trên Slack Với Giao diện 'Đang suy nghĩ' & Nhớ Lịch Sử Chat (Postgres) - Miễn phí 100%"
description: "Workflow tự động hóa tạo chatbot AI trả lời tin nhắn DM trên Slack với giao diện 'đang suy nghĩ' (thinking UI) và nhớ lịch sử chat qua Postgres. Giúp hỗ trợ khách hàng 24/7, cá nhân hóa tương tác và tối ưu hóa thời gian phản hồi."
slug: tao-chatbot-ai-slack-thinking-ui-postgres
tags: [n8n, automation, ai-chatbot, slack, postgresql, openrouter, no-code]
keywords: [n8n workflow slack chatbot, tự động hóa hỗ trợ khách hàng, chatbot ai trả lời tin nhắn dm, thinking ui slack, lưu lịch sử chat postgresql]
---

# 🚀 **Tạo Chatbot AI Trả Lời Trên Slack Với Giao diện 'Đang suy nghĩ' & Nhớ Lịch Sử Chat (Postgres)**

Hiện nay, doanh nghiệp nào cũng cần một giải pháp hỗ trợ khách hàng nhanh chóng và cá nhân hóa. Tuy nhiên, việc quản lý tin nhắn DM trên Slack thủ công không chỉ tốn thời gian mà còn dễ gây mất trải nghiệm cho khách hàng. **Workflow này giúp bạn tự động hóa hoàn toàn quá trình này bằng một chatbot AI thông minh**, có thể:
- Trả lời tin nhắn DM trên Slack với giao diện "đang suy nghĩ" (thinking UI) để khách hàng không cảm thấy chờ đợi.
- Nhớ lịch sử chat của từng khách hàng (dữ liệu lưu trên Postgres) để trả lời liên tục và logic hơn.
- Sử dụng mô hình AI OpenRouter để trả lời chính xác và tự động hóa các câu hỏi thường gặp.

Không cần viết một dòng code nào cả! Bạn chỉ cần **cài đặt n8n trên VPS** và cấu hình một vài thông tin cơ bản là xong.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động 24/7 mà không bị gián đoạn, các sếp nên **self-host n8n trên VPS** thay vì dùng phiên bản cloud. Với VPS, bạn có thể tùy chỉnh tài nguyên và đảm bảo độ tin cậy cao.

👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ sức mạnh cho workflow này)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần phải trả lời DM thủ công, chatbot AI làm việc 24/7.
- **Trải nghiệm khách hàng tốt hơn**: Giao diện "đang suy nghĩ" làm giảm cảm giác chờ đợi.
- **Lịch sử chat được lưu trữ**: Chatbot nhớ được các cuộc trò chuyện trước đó, trả lời logic và cá nhân hóa.
- **Tối ưu hóa chi phí**: Không cần thuê nhân viên hỗ trợ khách hàng ngoài giờ.
- **Dễ dàng mở rộng**: Có thể tùy chỉnh mô hình AI và logic agent theo nhu cầu.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Slack**:
   - Một **Slack App** đã được tạo và có **Bot Token** (xem [hướng dẫn tạo Slack App](https://api.slack.com/apps)).
   - **Slack API Credentials** (để n8n kết nối với Slack).
2. **API Key của OpenRouter**:
   - Đăng ký tại [OpenRouter](https://openrouter.ai/) và lấy **API Key**.
3. **PostgreSQL Database**:
   - Một cơ sở dữ liệu Postgres để lưu trữ lịch sử chat (có thể dùng **Neon**, **Supabase**, hoặc Postgres trên VPS).
   - **Credentials Postgres** (host, port, username, password, database name).
4. **n8n Self-hosted**:
   - Cài đặt n8n trên VPS (hướng dẫn tại [n8n.io](https://n8n.io/)).

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Bước 1: Tải file JSON của workflow từ [đây](https://n8n.io/workflows/5749) hoặc copy toàn bộ JSON từ trang này.

Bước 2: Mở **n8n Editor** và nhấn **Import Workflow** (hoặc paste JSON vào ô Import).

---
### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **A. Cấu hình Slack Trigger (`On Message Received`)**
- **Node**: `On Message Received` (type: `slackTrigger`)
- **Cấu hình**:
  - **Channel to Watch**: Nhập **ID của Slack App** (không phải #channel).
  - **Credentials**: Chọn `slackApi` (đã cấu hình trước khi import).
  - **Filter**: Chỉ lọc tin nhắn từ **user** (không phải bot hoặc message từ Slack).

#### **B. Cấu hình OpenRouter (`OpenRouter Chat Model`)**
- **Node**: `OpenRouter Chat Model` (type: `lmChatOpenRouter`)
- **Cấu hình**:
  - **Credentials**: Chọn `openRouterApi` (đã lưu API Key trước).
  - **Model**: Chọn mô hình AI phù hợp (ví dụ: `mistral-tiny`, `llama3`).
  - **Prompt**: Tùy chỉnh theo logic chatbot (ví dụ: *"You are a helpful customer support bot. Answer in Vietnamese."*).

#### **C. Cấu hình Agent (`AI Agent`)**
- **Node**: `AI Agent` (type: `agent`)
- **Cấu hình**:
  - **Memory**: Kết nối với `Postgres Chat Memory` (node sau).
  - **Tools**: Thêm các công cụ cần thiết (ví dụ: API kết nối với CRM, tìm kiếm knowledge base).
  - **Prompt**: Tùy chỉnh logic trả lời (ví dụ: *"If user asks about product X, reply with detailed info from Postgres memory."*).

#### **D. Cấu hình Thinking UI (`Set Thinking Status`)**
- **Node**: `Set Thinking Status` (type: `httpRequest`)
- **Cấu hình**:
  - **Credentials**: Chọn `httpBearerAuth` (nếu cần).
  - **URL**: Slack API endpoint để kích hoạt thinking UI:
    ```
    https://slack.com/api/chat.postEphemeral
    ```
  - **Headers**: Thêm `Authorization: Bearer <slack-bot-token>`.
  - **Body**: JSON với thông tin message ID và text "Đang suy nghĩ...".

#### **E. Cấu hình Lưu Lịch Sử Chat (`Postgres Chat Memory`)**
- **Node**: `Postgres Chat Memory` (type: `memoryPostgresChat`)
- **Cấu hình**:
  - **Credentials**: Chọn `postgres` (đã cấu hình trước).
  - **Table Name**: Tên bảng lưu trữ (ví dụ: `slack_chat_history`).
  - **Columns**: Cấu trúc bảng (ví dụ: `user_id, message, timestamp`).

#### **F. Cấu hình Trả Lời Slack (`Send Reply`)**
- **Node**: `Send Reply` (type: `slack`)
- **Cấu hình**:
  - **Credentials**: Chọn `slackApi`.
  - **Channel**: Chọn `#general` hoặc DM với user.
  - **Text**: Dữ liệu từ `AI Agent` (trả lời tự động).

---
### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Gửi tin nhắn DM từ Slack đến bot và kiểm tra:
     - Chatbot có trả lời không?
     - Giao diện "đang suy nghĩ" có hoạt động không?
     - Lịch sử chat có lưu trên Postgres không?
2. **Bật Active**:
   - Nhấn **Active** trên workflow.

---

## ✍️ **Mẹo & gợi ý nâng cao**
1. **Tùy chỉnh mô hình AI**:
   - Thay đổi mô hình OpenRouter để cải thiện chất lượng trả lời (ví dụ: `llama3-8b` cho độ chính xác cao).
2. **Kết nối với CRM**:
   - Thêm node `httpRequest` để chatbot lấy thông tin khách hàng từ CRM (Zoho, HubSpot).
3. **Gửi báo cáo định kỳ**:
   - Sử dụng node `email` hoặc `slack` để gửi báo cáo thống kê chatbot hàng ngày.
4. **Lọc tin nhắn không cần thiết**:
   - Thêm node `if` để bỏ qua tin nhắn từ bot hoặc spam.
5. **Cập nhật knowledge base**:
   - Sử dụng node `fileSystem` để chatbot đọc từ các file FAQ và trả lời chính xác hơn.

---
## 📌 **Kết luận**
Workflow này giúp **tự động hóa hoàn toàn quá trình hỗ trợ khách hàng trên Slack**, giảm thiểu thời gian phản hồi và cải thiện trải nghiệm. **Không cần code, chỉ cần cấu hình vài bước đơn giản** là chatbot AI của bạn đã sẵn sàng hoạt động 24/7!

👉 **Bắt đầu ngay bằng cách import workflow và cấu hình theo hướng dẫn trên!** Nếu có vấn đề, các sếp có thể liên hệ với tác giả [James Francis](https://n8n.io/workflows/5749) để hỗ trợ.

---
**🚀 Cần hỗ trợ cài đặt n8n trên VPS?** [Liên hệ TinoHost](https://tino.vn/vps-n8n?affid=388) để được tư vấn miễn phí!