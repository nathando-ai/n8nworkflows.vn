---
title: "🚀 Tự động cảnh báo List & Delist Coin lên Telegram, X và Discord với n8n"
description: "Xây dựng hệ thống tự động quét và phát hiện các thông báo niêm yết (listing) và hủy niêm yết (delisting) tiền điện tử, sau đó phát thông báo tức thì lên Telegram, X (Twitter) và Discord."
slug: "tu-dong-canh-bao-crypto-listing-delisting-n8n"
tags: [n8n, automation, crypto, telegram, twitter, discord, supabase]
keywords: [n8n workflow, crypto listing alerts, bot telegram crypto, auto post twitter discord, tự động hóa crypto]
keywords: [n8n workflow, crypto listing alerts, bot telegram crypto, auto post twitter discord, tự động hóa crypto]
---

# 🚀 Tự động cảnh báo List & Delist Coin lên Telegram, X và Discord

Trong thị trường tiền điện tử (crypto) đầy biến động, tốc độ chính là tiền bạc. Việc nắm bắt thông tin một đồng coin chuẩn bị được niêm yết (listing) hay hủy niêm yết (delisting) trên các sàn giao dịch lớn có thể mang lại lợi thế giao dịch cực kỳ lớn. Tuy nhiên, việc "cắm chốt" 24/7 trên các kênh thông báo là bất khả thi đối với con người. 

Giải pháp hoàn hảo cho các nhà đầu tư và trader là đây: Workflow n8n tự động hoàn toàn giúp quét dữ liệu thị trường, kiểm tra trùng lặp qua **Supabase** và phát thông báo chớp nhoáng lên **Telegram**, **X (Twitter)**, và **Discord** mà không cần tốn một dòng code thủ công nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không lo gián đoạn kết nối, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tốc độ chớp nhoáng:** Phát hiện sự kiện listing/delisting gần như theo thời gian thực nhờ tính năng `Schedule Trigger`.
- **Đa kênh tiếp cận:** Đồng thời phát thông báo đến cộng đồng trên Telegram, X (Twitter) và Discord mà không bỏ sót bất kỳ nền tảng nào.
- **Chống trùng lặp thông minh:** Sử dụng cơ sở dữ liệu **Supabase** để lưu trữ các ID đã thông báo, đảm bảo không gửi thông tin rác hay lặp lại các tin cũ.
- **Vận hành 24/7 tự động:** Hoạt động bền bỉ ngày đêm, giúp các sếp thảnh thơi tận hưởng cuộc sống mà không bỏ lỡ cơ hội vàng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **n8n Instance:** Đã cài đặt sẵn sàng (Self-hosted hoặc Cloud).
- **Supabase Account:** Tạo một database để lưu lịch sử các token đã được thông báo.
- **Telegram Bot Token:** Tạo sẵn qua `@BotFather` và thêm bot vào channel/group mong muốn.
- **X (Twitter) Developer Account:** API keys để đăng tweet tự động.
- **Discord Webhook / Bot:** Quyền gửi tin nhắn vào kênh Discord chỉ định.
- **HTTP API nguồn dữ liệu:** API endpoints cung cấp thông tin về listing và delisting.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã JSON của workflow này, vào giao diện n8n Editor, chọn **Add workflow** -> bấm dấu `...` ở góc trên bên phải -> chọn **Import from JSON** và dán vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 19 nodes được chia thành 2 luồng chính (Listing và Delisting). Các sếp cần cấu hình kỹ các node sau:

- **Schedule Trigger:** Thiết lập chu kỳ thời gian chạy quét (ví dụ: chạy mỗi 5 phút hoặc 15 phút tùy nhu cầu).
- **Http request (Delistings) & HTTP Request (listings):** Trỏ đường dẫn API endpoint lấy dữ liệu cập nhật từ các sàn giao dịch hoặc nguồn cung cấp dữ liệu crypto.
- **Get a row / Store ID for future Updates / Store ID for future updates1 (Supabase):** Kết nối tài khoản Supabase của sếp, cấu hình bảng (table) dùng để lưu trữ ID nhằm lọc các tin đã được thông báo trước đó.
- **Split Items & Split Items1 (Code):** Các node xử lý dữ liệu JavaScript thuần túy giúp tách các mảng dữ liệu thành từng item riêng lẻ để hệ thống dễ dàng xử lý tiếp.
- **Send Delisting Alert To Telegram & Send Listing Alert To Telegram:** Nhập `Bot Token` và `Chat ID` của kênh Telegram nhận tin.
- **Create Tweet Delisting & Create Tweet Listing:** Kết nối tài khoản X thông qua OAuth2 hoặc API keys để tạo nội dung tweet tự động.
- **Send a message(Delistings) & Send a message (new listings) (Discord):** Cấu hình Webhook URL của kênh Discord để đẩy thông báo vào phòng chat cộng đồng.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** chạy thử thủ công (Test run) với dữ liệu mẫu để kiểm tra xem tin nhắn có bắn thành công lên Telegram, Discord và Twitter hay chưa.
- Kiểm tra lại data trong Supabase xem ID đã được lưu đúng chưa.
- Nếu mọi thứ mượt mà, gạt công tắc **Active** sang màu xanh để workflow chính thức tự động chiến đấu!

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Có thể tích hợp thêm node **Slack** hoặc **Zalo ZNS** nếu đội ngũ của các sếp hoạt động trên các nền tảng này.
- **Lưu log chi tiết:** Tích hợp thêm một node **Google Sheets** hoặc gửi email báo cáo tổng kết cuối ngày về số lượng token đã list/delist.
- **Lọc thông minh bằng AI:** Chèn thêm một node **OpenAI / LangChain** trước khi gửi tin để viết lại nội dung (rewrite) theo phong cách hài hước hoặc chuyên nghiệp hơn cho từng mạng xã hội.

### 📌 Kết luận
Hệ thống cảnh báo Crypto Listing & Delisting tự động này là trợ thủ đắc lực giúp các sếp tiết kiệm hàng giờ theo dõi thủ công và đón đầu mọi con sóng thị trường. Hãy triển khai ngay trên n8n để tối ưu hóa chiến lược đầu tư crypto của mình nhé! Chúc các sếp thao tác thành công!