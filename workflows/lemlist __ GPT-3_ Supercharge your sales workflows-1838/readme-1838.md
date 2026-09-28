---
title: "🚀 Tự động hóa Sales Outbound: Phân loại email phản hồi từ Lemlist bằng OpenAI & Đồng bộ HubSpot, Slack"
description: "Hướng dẫn xây dựng workflow n8n tự động phân loại phản hồi chiến dịch cold email trên Lemlist bằng OpenAI GPT, đồng thời cập nhật dữ liệu lên HubSpot và Slack."
slug: "tu-dong-hoa-sales-outbound-lemlist-openai-hubspot-slack"
tags: [n8n, automation, no-code, sales, ai, lemlist, openai, hubspot, slack]
keywords: [n8n workflow, lemlist automation, openai gpt sales, hubspot crm sync, slack notification, tự động hóa sales outbound]
---

# 🚀 Tự động hóa Sales Outbound: Phân loại email phản hồi từ Lemlist bằng OpenAI & Đồng bộ HubSpot, Slack

Trong quy trình Sales Outbound (cold email), việc phải đọc hàng trăm email phản hồi mỗi ngày để phân loại xem khách hàng quan tâm, từ chối, hay xin nghỉ phép thực sự ngốn rất nhiều thời gian của đội ngũ sales. Chưa kể nếu phản hồi chậm, bạn có thể bỏ lỡ cơ hội chốt deal nóng hổi.

Giải pháp là gì? Workflow n8n này sẽ tự động hóa 100% quy trình: Lắng nghe phản hồi từ **Lemlist**, gọi **OpenAI** để phân loại ý định (intent) của khách hàng, sau đó tự động thực hiện các hành động tương ứng trên **HubSpot CRM**, hủy đăng ký nếu cần, và bắn thông báo tức thì lên **Slack** cho đội ngũ sales. Không cần viết một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không còn cảnh sales phải đọc thủ công từng email trả lời chiến dịch.
- **Phản ứng tức thì (Real-time):** Khách vừa reply "Tôi quan tâm" là Deal được tạo ngay trên HubSpot và thông báo đỏ rực trên Slack.
- **Chính xác cao:** AI (OpenAI) tự động phân loại chuẩn xác các nhóm: Quan tâm (interested), Nghỉ phép (out of office), Hủy đăng ký (unsubscribe), và Khác (other).
- **Vận hành liền mạch:** Tự động hóa toàn bộ vòng đời từ Lead phản hồi đến cập nhật CRM và phân luồng tác vụ cho sale.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API Keys sau:
1. **Tài khoản n8n** (Cloud hoặc Self-hosted).
2. **Tài khoản Lemlist** kèm Lemlist API Key (để nhận trigger khi lead reply và quản lý lead).
3. **Tài khoản OpenAI** kèm OpenAI API Key (để sử dụng mô hình GPT phân loại nội dung email).
4. **Tài khoản HubSpot** (Kết nối qua HubSpot OAuth2 API để tạo contact, deal và task).
5. **Workspace Slack** (Kết nối Bot Slack để nhận thông báo tự động).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này, sau đó vào giao diện n8n chọn **Add workflow** -> Click vào menu ba chấm (...) ở góc trên bên phải -> Chọn **Import from JSON** và dán đoạn mã vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà không lỗi, các sếp cần cấu hình chính xác các node sau:

- **Lemlist - Lead Replied (Trigger):** 
  - Chọn Credentials Lemlist của các sếp.
  - Node này sẽ lắng nghe sự kiện khi có một lead trả lời email trong chiến dịch Lemlist.
- **OpenAI:** 
  - Chọn Credentials OpenAI.
  - Prompt đã được cấu hình sẵn để phân loại email thành 4 nhóm (`interested`, `Out of office`, `unsubscribe`, `other`). Các sếp có thể tùy chỉnh lại prompt nếu muốn phân loại chi tiết hơn.
- **Switch:** 
  - Node này đóng vai trò "ngã rẽ" dựa trên kết quả trả về từ OpenAI (`Category`). Các sếp nhớ kiểm tra các nhánh điều kiện để đảm bảo luồng đi đúng (ví dụ: `interested` đi sang tạo deal HubSpot, `unsubscribe` đi sang Lemlist Unsubscribe...).
- **HubSpot - Get contact ID / Create Deal / follow up task:** 
  - Cần kết nối HubSpot OAuth2.
  - Đảm bảo ánh xạ (mapping) đúng các trường thông tin email từ Lemlist sang HubSpot để hệ thống tìm đúng contact hoặc tạo mới chính xác.
- **Lemlist - Unsubscribe & Lemlist - Mark as interested (HTTP Request):** 
  - Xử lý việc cập nhật trạng thái lead trực tiếp trên hệ thống Lemlist dựa theo ý định của khách hàng.
- **Slack & Slack1:** 
  - Chọn channel Slack nhận thông báo. Các sếp có thể tùy chỉnh nội dung tin nhắn để đội sales đọc phát hiểu ngay nội dung khách phản hồi.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và test thử bằng cách gửi một phản hồi giả lập hoặc kích hoạt một chiến dịch nhỏ trên Lemlist.
- Kiểm tra các nhánh chạy xem dữ liệu đã qua HubSpot và Slack thành công chưa.
- Sau khi test ngon nghẻ, gạt công tắc sang **Active** để hệ thống tự động chạy 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm AI soạn thảo:** Có thể mở rộng workflow bằng cách nếu khách hàng `interested`, gọi thêm một node OpenAI nữa để tự động soạn draft email trả lời gửi cho sales duyệt.
- **Ghi log vào Google Sheets:** Thêm một node Google Sheets ở cuối luồng để lưu toàn bộ lịch sử phản hồi và kết quả phân loại của AI phục vụ việc làm báo cáo hàng tuần.
- **Thêm kênh thông báo Telegram/Zalo:** Bên cạnh Slack, nếu đội sales của các sếp thích dùng Telegram, hãy gắn thêm một node Telegram Bot để nhận ping tiện lợi hơn.

### 📌 Kết luận
Tự động hóa phân loại email outbound với n8n và OpenAI là bước tiến lớn giúp tối ưu hóa đội ngũ Sales, giúp sales tập trung vào việc chốt deal thay vì làm các tác vụ thủ công nhàm chán. Chúc các sếp cài đặt thành công và chốt thật nhiều đơn hàng!