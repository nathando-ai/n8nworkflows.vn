---
title: "🤖 Tạo Chatbot Telegram AI Cảm Biến với GPT-4o-mini + Google Sheets - Hỗ Trợ Tự Động Hóa Hỗ Trợ Khách Hàng 24/7"
description: "Workflow này tự động hóa việc xây dựng một chatbot Telegram AI có quản lý phiên (session) thông minh, giúp doanh nghiệp hỗ trợ khách hàng cá nhân hóa, tiết kiệm thời gian và tối ưu hóa trải nghiệm. Sử dụng GPT-4o-mini và Google Sheets để lưu trữ lịch sử hội thoại, tạo ra một giải pháp tự động hóa hoàn chỉnh không cần code."
slug: "chatbot-telegram-ai-gpt-4o-mini-google-sheets"
tags: [n8n, automation, ai, telegram, google-sheets, no-code, chatbot]
keywords: [chatbot telegram tự động hóa, n8n workflow ai, quản lý phiên hội thoại, gpt-4o-mini, hỗ trợ khách hàng 24/7, google sheets tự động hóa]
---

# 🚀 **Chatbot Telegram AI Cảm Biến với GPT-4o-mini: Hỗ Trợ Khách Hàng Cá Nhân Hóa Miễn Phí**

## **💡 Giới Thiệu: Tại Sao Các Sếp Cần Một Chatbot Telegram AI?**
Hiện nay, việc hỗ trợ khách hàng qua Telegram đang trở thành **trend không thể bỏ qua**, nhưng làm thủ công sẽ khiến các sếp:
- **Mất thời gian** để trả lời từng tin nhắn một.
- **Không nhớ lịch sử** của từng khách hàng, dẫn đến trải nghiệm không mượt mà.
- **Không thể hoạt động 24/7**, khiến khách hàng cảm thấy bỏ rơi.

**Workflow này giải quyết tất cả vấn đề trên bằng cách:**
✅ **Tự động hóa hoàn toàn** với GPT-4o-mini (mô hình AI mạnh mẽ của OpenAI).
✅ **Quản lý phiên (session) thông minh** trên Google Sheets, giúp lưu trữ và tiếp nối hội thoại.
✅ **Cá nhân hóa trải nghiệm** cho từng khách hàng, như họ đã từng trò chuyện trước đó.
✅ **Hoạt động liên tục 24/7** mà không cần can thiệp của con người.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính riêng tư và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian** lên đến **90%** trong việc hỗ trợ khách hàng.
- **Cá nhân hóa trải nghiệm** với mỗi khách hàng, như họ đã từng trò chuyện trước đó.
- **Hoạt động 24/7** mà không cần can thiệp của con người.
- **Lưu trữ lịch sử hội thoại** trên Google Sheets, dễ dàng theo dõi và phân tích.
- **Tăng trải nghiệm khách hàng** với phản hồi nhanh chóng và chính xác.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Telegram Bot** (đăng ký tại [@BotFather](https://t.me/BotFather)).
2. **API Key OpenAI** (đăng ký tại [OpenAI](https://platform.openai.com/)).
3. **Google Sheets OAuth 2.0** (đăng ký tại [Google Cloud Console](https://console.cloud.google.com/)).
4. **File Google Sheets mẫu** (clone từ [đây](https://docs.google.com/spreadsheets/d/1MCJLAqKP0Y7Qr68ZYoSSBeEVyKI1QgAAZnlEiyqkzXo/edit?usp=sharing)).
5. **n8n Self-hosted** (cài đặt tại [n8n.io](https://n8n.io/)).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải file JSON** từ [n8n.io/workflows/3798](https://n8n.io/workflows/3798).
- **Nhấn "Import"** trong n8n Editor và chọn file JSON.
- **Hoặc copy toàn bộ JSON** và dán vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **31 node** và được chia thành **5 chức năng chính**:
- **Bắt đầu phiên mới** (`/new`).
- **Kiểm tra phiên hiện tại** (`/current`).
- **Tiếp tục phiên cũ** (`/resume`).
- **Lấy tóm tắt hội thoại** (`/summary`).
- **Hỏi câu hỏi** (`/question`).

##### **🔹 Cấu hình Telegram Bot**
- **Node `Get message` (telegramTrigger)**:
  - Điền **Token Bot** từ `@BotFather` vào **credentials `telegramApi`**.
  - Chọn **Chat ID** của bot (có thể lấy từ [@userinfobot](https://t.me/userinfobot)).

##### **🔹 Cấu hình OpenAI**
- **Node `OpenAI Chat Model` (lmChatOpenAi)**:
  - Điền **API Key OpenAI** vào **credentials `openAiApi`**.
  - Chọn mô hình **gpt-4o-mini** (đã được thiết lập mặc định).

##### **🔹 Cấu hình Google Sheets**
- **Node `Get session` (googleSheets)**:
  - Đăng ký **Google Sheets OAuth 2.0** và điền vào **credentials `googleSheetsOAuth2Api`**.
  - Chọn **Sheet ID** từ file Google Sheets mẫu (đã clone trước đó).
  - Đặt **Sheet Name** là `Sessions` (đã được thiết lập trong file mẫu).

##### **🔹 Cấu hình Prompt & Logic**
- **Node `Trim resume` (code)** và `Prompt + Resume` (code)**:
  - Các sếp có thể chỉnh sửa **Prompt** trong **code node** để phù hợp với ngành nghề của mình.
  - Ví dụ:
    ```javascript
    // Trong node "Trim resume":
    return { text: $input.all().text.trim() };
    ```
    ```javascript
    // Trong node "Prompt + Resume":
    return {
      prompt: `You are a customer support assistant. Here is the user's resume:\n${$input.all().text}\n\nAnswer the question: ${$input.all().question.trim()}`
    };
    ```

##### **🔹 Kích hoạt Workflow**
- **Test Run**:
  - Gửi tin nhắn `/new` đến bot Telegram để bắt đầu phiên mới.
  - Kiểm tra **Google Sheets** để xác nhận phiên đã được tạo.
- **Bật Active**:
  - Nhấn **Active** trên workflow để bắt đầu tự động hóa.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Slack/Telegram Alert**:
   - Thêm **node Slack** hoặc **Telegram** để thông báo khi có tin nhắn mới.
2. **Lưu log hoạt động**:
   - Sử dụng **node StickyNote** để ghi lại lịch sử hoạt động của bot.
3. **Tự động gửi báo cáo hàng tuần**:
   - Thêm **node Set** và **node Google Sheets** để tự động cập nhật báo cáo.
4. **Cải thiện Prompt**:
   - Tối ưu hóa **Prompt** trong node `code` để bot trả lời chính xác hơn.

---

### 📌 **Kết luận**
Workflow này không chỉ **giải phóng thời gian** cho các sếp mà còn **tăng trải nghiệm khách hàng** với một chatbot AI thông minh, cá nhân hóa và hoạt động 24/7. **Hãy thử ngay và tự động hóa hỗ trợ khách hàng của mình!**

👉 **Bắt đầu từ bây giờ:**
1. **Clone file Google Sheets** và cài đặt **n8n Self-hosted**.
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Bật Active** và bắt đầu tự động hóa!

**Nếu có vấn đề, hãy liên hệ với tác giả Davide tại [LinkedIn](https://www.linkedin.com/in/davideboizza) hoặc email [info@n3w.it](mailto:info@n3w.it).** 🚀