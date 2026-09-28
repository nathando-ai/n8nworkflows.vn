---
title: "🚀 Xây dựng Trợ lý HR AI cho Telegram: Báo cáo điểm danh & lương"
description: "Giải pháp tự động hóa 100% không cần code, giúp doanh nghiệp quản lý điểm danh và báo cáo lương qua Telegram, tích hợp OpenAI và Google Sheets."
slug: "xay-dung-tro-ly-hr-ai-cho-telegram"
tags: [n8n, automation, no-code, HR, AI, chatbot, telegram, google-sheets, openai]
keywords: [n8n workflow, tự động hóa, trợ lý HR, báo cáo lương, điểm danh, Telegram, OpenAI, LangChain]
---

# 🚀 Xây dựng Trợ lý HR AI cho Telegram: Báo cáo điểm danh & lương

Bạn đang phải mất hàng giờ mỗi ngày để thu thập điểm danh, tính lương và gửi báo cáo cho nhân viên? Đừng lo, workflow này sẽ giúp bạn tự động hóa toàn bộ quy trình, chỉ cần một vài cú click và không cần viết code. Trợ lý AI của chúng ta sẽ nhận lệnh qua Telegram, lấy dữ liệu từ Google Sheets, tính toán lương, gửi báo cáo và thậm chí trả lời các câu hỏi thường gặp của nhân viên.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).  
👉 <https://tino.vn/vps-n8n?affid=388> (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 <https://my.bnix.one/aff.php?aff=172> (VPS Xeon 4GB chỉ 50k/tháng)  
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ vài giờ lên còn vài phút.  
- **Chính xác 100%**: Tự động tính lương, tránh sai sót do tính toán thủ công.  
- **Cá nhân hóa**: Gửi báo cáo riêng cho từng nhân viên qua Telegram.  
- **Hoạt động liên tục**: Được chạy 24/7, không cần giám sát liên tục.  
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
- **Telegram Bot**: Tạo bot qua BotFather, lấy `BOT_TOKEN`.  
- **Google Sheets**: Tạo bảng dữ liệu điểm danh & lương, bật API, lấy `CLIENT_ID`, `CLIENT_SECRET`, `REFRESH_TOKEN`.  
- **OpenAI API Key**: Đăng ký tại <https://platform.openai.com> và lấy `OPENAI_API_KEY`.  
- **Google Gemini API Key** (tùy chọn): Nếu muốn dùng Gemini, lấy `GEMINI_API_KEY`.  
- **Webhook URL** (nếu dùng TelegramTrigger): Đăng ký URL công khai (nginx, ngrok, hoặc VPS).  
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
1. Tải file JSON của workflow từ <https://n8n.io/workflows/13441> hoặc sao chép nội dung JSON.  
2. Mở n8n Editor → `Import` → `Upload file` hoặc `Paste JSON`.  
3. Nhấn `Import` và workflow sẽ xuất hiện trong danh sách.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Mô tả | Tham số cần cấu hình |
|------|-------|----------------------|
| **TelegramTrigger** | Nhận lệnh từ người dùng | `Bot Token` (đã tạo), `Chat ID` (tùy chọn) |
| **ScheduleTrigger** | Chạy tự động vào giờ cố định | `Cron` expression (vd: `0 8 * * *` để chạy lúc 08:00 mỗi ngày) |
| **Code** | Xử lý dữ liệu, tính lương | Đoạn JavaScript lấy dữ liệu từ Google Sheets, tính lương, trả về JSON |
| **If / Switch** | Kiểm tra điều kiện (vd: lệnh `/report` hay `/attendance`) | `Conditions` (định nghĩa lệnh) |
| **Filter** | Lọc dữ liệu cần gửi | `Conditions` (vd: lọc nhân viên cụ thể) |
| **Merge** | Kết hợp dữ liệu từ nhiều nguồn | `Merge Mode` (Union, Intersect, etc.) |
| **GoogleSheets** | Đọc/ghi dữ liệu | `Sheet ID`, `Range`, `Credentials` (OAuth2) |
| **@n8n/n8n-nodes-langchain.agent** | Tạo agent AI (LangChain) | `Model`, `Prompt`, `Memory` (MemoryBufferWindow) |
| **@n8n/n8n-nodes-langchain.lmChatOpenAi** | Gửi prompt tới OpenAI | `API Key`, `Model` (gpt-4o, gpt-3.5-turbo) |
| **@n8n/n8n-nodes-langchain.lmChatGoogleGemini** | Gửi prompt tới Gemini (tùy chọn) | `API Key`, `Model` |
| **@n8n/n8n-nodes-langchain.memoryBufferWindow** | Lưu trữ lịch sử hội thoại | `Window Size` (vd: 5) |
| **Telegram** | Gửi tin nhắn, báo cáo | `Bot Token`, `Chat ID`, `Message` |

> **Lưu ý**: Mỗi node cần được cấu hình Credentials trong phần **Credentials** của n8n. Đừng quên bật `Use OAuth2` cho Google Sheets và nhập `Client ID/Secret/Refresh Token`.

### 3. Kích hoạt ⚡️
1. **Test run**: Chọn một node (vd: `TelegramTrigger`) và nhấn `Execute Node` để xem dữ liệu đầu vào.  
2. Kiểm tra log, đảm bảo không có lỗi.  
3. Khi mọi thứ ổn, bật `Active` cho workflow.  
4. Đảm bảo webhook URL đã được cập nhật trong BotFather (nếu dùng TelegramTrigger).

## ✍️ Mẹo & gợi ý nâng cao
- **Slack/Telegram kết hợp**: Thêm node `Slack` để gửi báo cáo tới kênh công ty.  
- **Lưu log**: Dùng node `GoogleSheets` hoặc `Database` để ghi lại lịch sử lệnh và phản hồi.  
- **Báo cáo định kỳ**: Sử dụng `ScheduleTrigger` để gửi báo cáo lương hàng tháng tự động.  
- **Tùy biến prompt**: Thêm biến `{{employee_name}}` vào prompt để AI trả lời cá nhân hóa.  
- **Quản lý lỗi**: Thêm node `Error Trigger` để gửi email cảnh báo khi workflow gặp lỗi.

## 📌 Kết luận
Workflow này giúp các sếp chuyển từ quy trình thủ công sang tự động hoàn toàn, giảm thiểu sai sót và tăng năng suất. Hãy thử ngay, cài đặt trên VPS, và cảm nhận sự khác biệt! Nếu gặp khó khăn, hãy mở issue hoặc liên hệ với cộng đồng n8n để được hỗ trợ. Happy automating!