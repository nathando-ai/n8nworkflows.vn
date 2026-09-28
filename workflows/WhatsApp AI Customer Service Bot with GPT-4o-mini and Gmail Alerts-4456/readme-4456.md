---
title: "🤖 [Tự động hóa CSKH WhatsApp với GPT-4o-mini + Gmail Alerts] - Giải pháp AI không cần code"
description: "Hướng dẫn chi tiết cách tự động hóa CSKH WhatsApp bằng AI GPT-4o-mini và gửi thông báo Gmail tự động - hoàn toàn không cần lập trình"
slug: "tu-dong-hoa-cskh-whatsapp-voi-gpt-4o-mini-va-gmail-alerts"
tags: [n8n, automation, no-code, ai, whatsapp, gmail]
keywords: [n8n workflow, tự động hóa CSKH, AI WhatsApp, GPT-4o-mini, tự động hóa không code]
---

# 🤖 Tự động hóa CSKH WhatsApp với GPT-4o-mini và Gmail Alerts - Giải pháp AI không cần code

[Các sếp đang gặp khó khăn khi phải trả lời hàng trăm tin nhắn WhatsApp hàng ngày một cách thủ công. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình CSKH bằng AI GPT-4o-mini và nhận thông báo Gmail tức thì - hoàn toàn không cần lập trình.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động trả lời khách hàng 24/7 bằng AI GPT-4o-mini
- Nhận thông báo Gmail tức thì khi có tin nhắn mới
- Tiết kiệm thời gian xử lý CSKH lên tới 80%
- Giữ lịch sử hội thoại để cung cấp dịch vụ tốt hơn
- Hoạt động liên tục không cần giám sát
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản WhatsApp Business API (hoặc Business Solution)
- Tài khoản Gmail để nhận thông báo
- API Key từ OpenAI (để sử dụng GPT-4o-mini)
- Tài khoản n8n đã cài đặt các node cần thiết (LangChain, WhatsApp, Gmail)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/4456)
2. Copy toàn bộ JSON workflow
3. Trong n8n Editor, nhấn "Import from Clipboard" và dán JSON vào

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Input Submissions" (whatsAppTrigger)**:
   - Cấu hình WhatsApp Business API credentials
   - Đảm bảo đã kích hoạt webhook trên tài khoản WhatsApp

2. **Node "OpenAI Chat Model" (lmChatOpenAi)**:
   - Thêm OpenAI API Key
   - Chọn model "gpt-4o-mini"
   - Tùy chỉnh prompt theo nhu cầu CSKH của doanh nghiệp

3. **Node "Send Gmail Notifications" (gmail)**:
   - Cấu hình Gmail credentials
   - Đặt địa chỉ email nhận thông báo
   - Tùy chỉnh nội dung email theo template

4. **Node "WhatsApp Reply Sender" (whatsApp)**:
   - Đảm bảo cùng credentials với node đầu vào
   - Kiểm tra quyền gửi tin nhắn tự động

#### 3. Kích hoạt ⚡️
1. Chạy test với dữ liệu mẫu để kiểm tra toàn bộ chuỗi
2. Kích hoạt workflow bằng cách nhấn "Active"
3. Kiểm tra hoạt động bằng cách gửi tin nhắn thử từ WhatsApp

### ✍️ Mẹo & gợi ý nâng cao
1. **Tích hợp Slack/Telegram**: Thêm node để nhận thông báo trên các nền tảng khác
2. **Lưu log hội thoại**: Thêm node lưu trữ lịch sử hội thoại vào Google Sheets/Notion
3. **Phân loại tin nhắn**: Sử dụng node "Signpost" để phân loại các loại tin nhắn khác nhau
4. **Tự động hóa báo cáo**: Thêm node gửi báo cáo hàng ngày về số lượng tin nhắn đã xử lý

### 📌 Kết luận
Workflow này mang lại giải pháp toàn diện cho việc tự động hóa CSKH trên WhatsApp bằng AI GPT-4o-mini và thông báo Gmail tức thì. Với chỉ 10 nodes đơn giản, các sếp có thể triển khai ngay mà không cần kiến thức lập trình. Hãy áp dụng ngay để nâng cao trải nghiệm khách hàng và tiết kiệm thời gian cho đội ngũ CSKH!