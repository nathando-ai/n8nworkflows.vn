---
title: "🚀 Tự động gửi bảng giá tiền điện tử hàng giờ lên Telegram với n8n và CoinGecko"
description: "Hướng dẫn cài đặt workflow n8n tự động cập nhật giá crypto mỗi giờ từ CoinGecko và gửi báo cáo chi tiết trực quan thẳng vào Telegram Channel."
slug: "tu-dong-gui-gia-crypto-hang-gio-telegram-coingecko"
tags: [n8n, automation, crypto, telegram, coingecko, no-code]
keywords: [n8n workflow, tự động hóa crypto, giá coin telegram, coingecko api, bot telegram crypto]
---

# 🚀 Tự động gửi bảng giá tiền điện tử hàng giờ lên Telegram với n8n và CoinGecko

Các sếp đang đầu tư hoặc làm cộng đồng về crypto chắc chắn hiểu cảm giác mệt mỏi khi phải liên tục check giá coin, hay việc cập nhật thủ công các biến động thị trường lên kênh Telegram mất nhiều thời gian thế nào. 

Bài viết này sẽ hướng dẫn các sếp thiết lập một siêu trợ lý tự động 100% không cần code bằng **n8n**, giúp lấy dữ liệu thị trường từ CoinGecko và gửi bảng tổng hợp giá chuẩn chỉnh, đẹp mắt lên Telegram đều đặn mỗi giờ.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian tuyệt đối:** Không còn cảnh canh bảng điện tử hay cập nhật thủ công từng đồng coin.
- **Cập nhật liên tục 24/7:** Bot tự động cào và bắn tin nhắn báo cáo giá theo đúng mốc thời gian cài sẵn (mỗi giờ hoặc tùy chỉnh).
- **Trình bày chuyên nghiệp:** Báo cáo định dạng HTML sạch sẽ, kèm emoji sinh động, dễ nhìn trên cả điện thoại lẫn máy tính.
- **Tùy biến linh hoạt:** Dễ dàng thêm bớt danh sách các đồng coin muốn theo dõi chỉ với vài dòng code cơ bản.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n đang hoạt động.
- Tài khoản Telegram để tạo Bot.
- Telegram Chat ID của Channel hoặc Group mà các sếp muốn bot gửi tin nhắn.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này và paste trực tiếp vào giao diện n8n Editor, hoặc import file JSON thông qua menu tuỳ chọn.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình chính xác các node sau:

- **Run Hourly (`scheduleTrigger`):** Node này mặc định chạy định kỳ mỗi giờ. Các sếp có thể đổi tần suất (ví dụ: 30 phút/lần hoặc theo khung giờ cụ thể) tùy nhu cầu.
- **Define Coins (`code`):** Mở node này để chỉnh sửa danh sách các đồng crypto muốn theo dõi trong đối tượng `coinIds` sử dụng slug chuẩn của CoinGecko (ví dụ: `bitcoin`, `ethereum`, `solana`...).
- **Fetch Market Data (`coinGecko`):** Node này gọi Public API của CoinGecko để lấy dữ liệu thời gian thực (giá, biến động...). **Không cần cấu hình API Key** cho node này.
- **Generate Telegram Message (`code`):** Node JavaScript xử lý dữ liệu thô thành báo cáo HTML gọn gàng. Các sếp có thể vào đây đổi ngôn ngữ (Tiếng Anh sang Tiếng Việt), chỉnh sửa emoji hoặc cách hiển thị định dạng tiền tệ.
- **Send to Telegram (`telegram`):** 
  - Tạo Bot Telegram mới thông qua [@BotFather](https://t.me/botfather) để lấy **Bot API Token**.
  - Thêm Bot làm Admin của Channel/Group Telegram và lấy **Chat ID**.
  - Kết nối Credentials cho node Telegram bằng cách điền Bot Token và cấu hình Chat ID nhận tin nhắn.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** để chạy thử thủ công và kiểm tra xem tin nhắn đã bắn về Telegram chuẩn chỉnh chưa.
- Nếu mọi thứ mượt mà, gạt công tắc sang **Active** để hệ thống tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
Để hệ thống xịn xò hơn nữa, các sếp có thể phát triển thêm:
- **Cảnh báo giá sốc:** Thêm điều kiện (If Node), nếu coin nào biến động trên ±10% trong giờ thì gửi thêm cảnh báo khẩn cấp sang một nhóm Telegram riêng.
- **Lưu lịch sử:** Kết nối thêm Google Sheets hoặc Supabase để lưu trữ lịch sử giá hàng giờ phục vụ việc phân tích xu hướng sau này.
- **Đa kênh:** Nhân bản node Telegram để bắn đồng thời tin nhắn lên nhóm Slack hoặc Discord của cộng đồng.

### 📌 Kết luận
Chỉ với vài bước cấu hình đơn giản trên n8n, các sếp đã sở hữu ngay một hệ thống tracking giá crypto tự động chuyên nghiệp như các quỹ đầu tư lớn. Triển khai ngay để tối ưu hóa công việc quản lý tài sản và xây dựng nội dung cộng đồng nào các sếp!