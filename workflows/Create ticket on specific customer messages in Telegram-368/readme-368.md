---
title: "🚀 Tự động tạo ticket từ tin nhắn Telegram cho khách hàng"
description: "Workflow tự động tạo ticket trên Freshdesk và đồng bộ vào Monday.com khi nhận tin nhắn từ Telegram, giúp bộ phận hỗ trợ giảm tải công việc và phản hồi nhanh chóng."
slug: "tu-dong-tao-ticket-tu-thong-diep-telegram"
tags: [n8n, automation, no-code, support, telegram, freshdesk, monday.com]
keywords: [n8n workflow, tự động hóa, ticket, telegram, freshdesk, monday.com]
---

# 🚀 Tự động tạo ticket từ tin nhắn Telegram cho khách hàng

Khi khách hàng gửi tin nhắn qua Telegram, đội ngũ hỗ trợ thường phải **đọc thủ công**, **sao chép nội dung**, rồi **tạo ticket** trên hệ thống quản lý (Freshdesk) và **đồng bộ** thông tin vào công cụ quản lý dự án (Monday.com).  
Quá trình này tốn thời gian, dễ sai sót và làm chậm tốc độ phản hồi.  

**Workflow này** sẽ tự động:

1. **Lắng nghe** mọi tin nhắn mới trên Telegram.  
2. **Kiểm tra** nội dung tin nhắn (ví dụ: chứa từ khóa “hỗ trợ”).  
3. **Tạo ticket** trên Freshdesk.  
4. **Tạo item** tương ứng trên Monday.com để theo dõi tiến độ.  
5. **Thông báo** lại cho khách hàng qua Telegram rằng ticket đã được tạo.

Kết quả: **tự động 100%**, không cần viết code, giảm tải công việc và nâng cao độ chính xác.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không còn nhập liệu thủ công, ticket được tạo ngay trong giây lát.  
- **Độ chính xác cao**: Nội dung tin nhắn được sao chép nguyên vẹn, giảm lỗi nhập sai.  
- **Theo dõi toàn diện**: Ticket trên Freshdesk và item trên Monday.com đồng bộ, dễ quản lý.  
- **Phản hồi nhanh**: Khách hàng nhận thông báo ngay khi ticket được tạo.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Telegram Bot API token** (để cấu hình `telegramApi` credential).  
- **Freshdesk API key** và **Domain** (để cấu hình `freshdeskApi` credential).  
- **Monday.com API token** và **Board ID** (để cấu hình `mondayComApi` credential).  
- Quyền **admin** trên n8n để tạo và kích hoạt workflow.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Vào **n8n → Workflows → Import**.  
2. Chọn **Upload JSON** và tải file JSON của workflow (hoặc copy toàn bộ JSON và dán vào ô “Import from Clipboard”).  
3. Nhấn **Import** → Workflow sẽ xuất hiện trong danh sách.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Vai trò | Cấu hình cần chỉnh |
|------|----------|-------------------|
| **Telegram Trigger** | Lắng nghe tin nhắn mới trên Telegram | - Chọn credential **telegramApi** (Bot Token). <br> - Đặt **Chat Type** = `private` hoặc `group` tùy nhu cầu. |
| **IF1** | Kiểm tra nội dung tin nhắn có chứa từ khóa “hỗ trợ” (hoặc tùy chỉnh) | - Trong **Conditions**, dùng **Expression**: `{{$json["message"]["text"]?.toLowerCase().includes("hỗ trợ")}}` |
| **Freshdesk** | Tạo ticket mới trên Freshdesk | - Credential **freshdeskApi** (API Key + Domain). <br> - **Subject**: `{{$json["message"]["text"]}}` <br> - **Description**: `Tin nhắn từ Telegram: {{$json["message"]["text"]}}` |
| **Freshdesk1** | (Optional) Thêm comment hoặc cập nhật trạng thái nếu cần | - Cấu hình tương tự, tùy mục đích. |
| **Monday.com** | Tạo item trên board “Support Tickets” | - Credential **mondayComApi**. <br> - **Board ID**: ID của board chứa cột ticket. <br> - **Item Name**: `Ticket - {{$json["message"]["from"]["username"]}}`. <br> - **Column Values**: Map nội dung tin nhắn vào cột mô tả. |
| **Monday.com1** | (Optional) Cập nhật trạng thái hoặc thêm cột phụ | - Cấu hình tùy nhu cầu. |
| **Telegram** | Gửi tin nhắn xác nhận tới người dùng | - Credential **telegramApi**. <br> - **Chat ID**: `{{$json["message"]["chat"]["id"]}}`. <br> - **Message**: “✅ Ticket của bạn đã được tạo, chúng tôi sẽ sớm phản hồi!” |
| **Telegram1** | (Optional) Gửi thông báo nội bộ cho nhóm hỗ trợ | - Chọn **Chat ID** của nhóm hỗ trợ. <br> - Nội dung: “🆕 Ticket mới từ {{$json["message"]["from"]["username"]}}”. |

> **Lưu ý:** Đảm bảo **credential** đã được tạo trước khi gán vào node. Vào **Credentials → New Credential** để nhập API token, domain, v.v.

#### 3. Kích hoạt ⚡️
1. Nhấn **Execute Workflow** lần đầu để kiểm tra với một tin nhắn mẫu.  
2. Kiểm tra kết quả trên Freshdesk, Monday.com và Telegram.  
3. Khi mọi thứ ổn, bật **Active** (nút chuyển đổi ở góc trên bên phải). Workflow sẽ tự động chạy 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Gửi báo cáo hàng ngày**: Thêm node **Schedule** + **Google Sheets** để lưu danh sách ticket đã tạo.  
- **Kết hợp Slack**: Thêm node **Slack** để thông báo ticket mới tới kênh hỗ trợ nội bộ.  
- **Xử lý đa ngôn ngữ**: Dùng node **Function** để dịch nội dung tin nhắn qua API Google Translate trước khi tạo ticket.  
- **Tự động gán ưu tiên**: Dựa trên từ khóa (ví dụ: “khẩn cấp”) trong tin nhắn, set trường **Priority** trên Freshdesk.

### 📌 Kết luận
Với workflow **“Create ticket on specific customer messages in Telegram”**, các sếp có thể **tự động hoá toàn bộ quy trình nhận hỗ trợ**, giảm thiểu công việc lặp lại, nâng cao tốc độ phản hồi và độ chính xác. Hãy **import ngay**, **cấu hình credential**, **kiểm tra** và **bật Active** – để đội ngũ hỗ trợ của bạn luôn sẵn sàng, không bỏ lỡ bất kỳ yêu cầu nào!