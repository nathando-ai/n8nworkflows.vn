---
title: "🚀 Tự động phát hiện Influencer tham gia sự kiện từ Eventbrite với Influencers.club, OpenAI và SendGrid"
description: "Workflow n8n giúp tự động quét danh sách người tham gia Eventbrite, tra cứu thông tin mạng xã hội qua Influencers.club, phân loại bằng AI và gửi email cá nhân hóa qua SendGrid."
slug: "tu-dong-phat-hien-influencer-tu-eventbrite-influencers-club-openai-sendgrid"
tags: [n8n, automation, eventbrite, influencers-club, openai, sendgrid]
keywords: [n8n workflow, tự động hóa eventbrite, influencers club api, openai gpt-4o-mini, gửi email sendgrid, influencer marketing]
---

# 🚀 Tự động phát hiện Influencer tham gia sự kiện từ Eventbrite với Influencers.club, OpenAI và SendGrid

Việc tổ chức sự kiện thường thu hút rất nhiều người tham gia, nhưng làm thế nào để bạn **nhận diện ngay lập tức những Influencer, Content Creator hoặc KOL** ẩn mình trong danh sách đăng ký? Việc lọc thủ công hàng trăm, hàng nghìn email thực sự là một cơn ác mộng tốn thời gian và dễ bỏ sót cơ hội hợp tác vàng.

Workflow n8n này chính là giải pháp tự động hóa 100% không cần code (No-code): Khi có người đăng ký sự kiện trên **Eventbrite**, hệ thống sẽ tự động gọi API của **Influencers.club** để quét toàn bộ dữ liệu mạng xã hội (Instagram, TikTok, YouTube, Twitter...), sử dụng **OpenAI (GPT-4o-mini)** để phân tích chuyên sâu và phân loại Influencer, sau đó tự động gửi một email chào mừng cá nhân hóa cực kỳ chuyên nghiệp qua **SendGrid**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không lo gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://vpx.vn/vps-n8n) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%**: Phát hiện creator ngay khi họ bấm đăng ký/check-in trên Eventbrite mà không cần nhân sự can thiệp.
- **Dữ liệu mạng xã hội toàn diện**: Biết chính xác họ làm nội dung gì, số lượng followers, nền tảng chính (Instagram, TikTok, YouTube...) thông qua Influencers.club.
- **Phân loại thông minh bằng AI**: GPT-4o-mini sẽ đánh giá tier (nano, micro, macro), niche (AI, tech, marketing...) và mức độ tiềm năng.
- **Cá nhân hóa trải nghiệm VIP**: Tự động gửi email chăm sóc, mời vào khu vực VIP lounge hoặc tặng quyền lợi riêng biệt tùy theo tầm ảnh hưởng của họ.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động trơn tru, các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản Eventbrite** (để cấu hình Eventbrite Trigger).
- **Tài khoản Influencers.club** (lấy API Key / Header Auth để gọi Enrichment API).
- **Tài khoản OpenAI API Key** (dùng model `gpt-4o-mini` cho các Agent AI).
- **Tài khoản SendGrid** (để gửi email tự động).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy toàn bộ JSON từ nguồn gốc.
- Trong giao diện n8n Editor, chọn **Add workflow** -> Nhấn vào dấu `...` ở góc trên bên phải -> Chọn **Import from File** hoặc **Paste Workflow JSON**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các credentials và tham số cho các node cốt lõi sau:
- **Eventbrite Trigger1**: Kết nối tài khoản Eventbrite qua OAuth2. Node này sẽ bắt sự kiện (`attendee.registered`, `attendee.updated`, hoặc `attendee.checked_in`).
- **Influencers.club - Enrichment API by Email**: Điền Header Auth API Key của Influencers.club để hệ thống tra cứu profile mạng xã hội dựa trên email của người tham gia.
- **OpenAI (Classificator)** & **OpenAI (Email Agent)1**: Chọn credential `openAiApi` và kiểm tra model `gpt-4o-mini`.
- **AI Classificator** & **Email Personalization Agent**: Tinh chỉnh `systemMessage` trong AI Agent để phù hợp với văn phong thương hiệu và chiến lược chăm sóc khách hàng của sự kiện.
- **Send an email**: Cấu hình tài khoản SendGrid (`sendGridApi`) và thiết lập địa chỉ email người gửi (`From Email`) chính xác.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và test thử bằng một bản ghi giả lập hoặc đăng ký thử trên Eventbrite để kiểm tra luồng dữ liệu qua từng node (`Extract Attendee` -> `Enrichment API` -> `AI Classificator` -> `IS - Creator?` -> `Send an email`).
- Sau khi test thành công, gạt công tắc sang **Active** để hệ thống tự động chạy 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa kênh thông báo**: Kết hợp thêm node **Telegram** hoặc **Slack** để gửi tin nhắn thông báo tức thì về nhóm nội bộ mỗi khi có một Macro Influencer đăng ký tham gia sự kiện.
- **Lưu trữ dữ liệu**: Thêm node **Google Sheets** hoặc **Notion** sau bước phân loại AI để lưu danh sách toàn bộ Creator vào database phục vụ cho các chiến dịch marketing sau sự kiện.
- **Mở rộng phân khúc VIP**: Tùy biến logic trong node `IS - Creator?` và hệ thống phân cấp VIP routing để đưa ra các đặc quyền riêng biệt (như vé mời phòng chờ riêng, tặng quà, hoặc đặt lịch hẹn gặp 1-1).

### 📌 Kết luận
Workflow tích hợp Eventbrite, Influencers.club, OpenAI và SendGrid là một "vũ khí bí mật" giúp các nhà tổ chức sự kiện tối ưu hóa quy trình chăm sóc khách hàng, biến việc tìm kiếm và kết nối với các Influencer tiềm năng trở nên tự động, chuyên nghiệp và mượt mà hơn bao giờ hết. Hãy import workflow ngay và nâng cấp chất lượng sự kiện của các sếp lên một tầm cao mới!