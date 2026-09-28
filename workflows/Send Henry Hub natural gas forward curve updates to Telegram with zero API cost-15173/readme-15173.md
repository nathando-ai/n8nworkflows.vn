---
title: "🚀 Tự động cập nhật biểu đồ giá khí tự nhiên Henry Hub lên Telegram hoàn toàn miễn phí"
description: "Hướng dẫn cài đặt workflow n8n tự động cào dữ liệu giá khí tự nhiên Henry Hub (Spot & Futures) và gửi báo cáo định kỳ qua Telegram mà không mất đồng chi phí API nào."
slug: "tu-dong-cap-nhat-gia-khi-tu-nhien-henry-hub-len-telegram"
tags: [n8n, automation, trading, telegram, scraping, no-code]
keywords: [n8n workflow, henry hub natural gas, tu dong hoa telegram, trading automation, free api trading]
---

# 🚀 Tự động cập nhật biểu đồ giá khí tự nhiên Henry Hub lên Telegram hoàn toàn miễn phí

Các sếp làm trong lĩnh vực tài chính, năng lượng hay giao dịch hàng hóa chắc chắn hiểu được cảm giác mệt mỏi khi phải liên tục theo dõi biến động giá khí tự nhiên Henry Hub thủ công. Việc bỏ lỡ các mốc giá Spot hoặc hợp đồng tương lai (Futures) quan trọng có thể khiến các sếp hụt mất những cơ hội giao dịch đắt giá. 

Thay vì tốn thời gian canh bảng điện tử hoặc mua các gói dữ liệu API đắt đỏ, workflow n8n này sẽ giúp các sếp tự động cào dữ liệu, xử lý và bắn thông báo trực tiếp về Telegram theo lịch hẹn hoàn toàn tự động và **0 đồng chi phí API**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% chi phí:** Không cần thuê các dịch vụ API dữ liệu thị trường đắt đỏ.
- **Cập nhật thời gian thực:** Tự động lấy dữ liệu giá Spot và 12 hợp đồng tương lai hàng tháng (forward curve) theo giờ giao dịch.
- **Trực quan, dễ đọc:** Dữ liệu được định dạng thành bảng HTML sạch sẽ, gọn gàng gửi thẳng vào Telegram Channel hoặc Chat cá nhân.
- **Hoạt động 24/7:** Chạy ngầm liên tục trên server riêng, đảm bảo các sếp không bao giờ bỏ lỡ thông tin thị trường.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một hệ thống n8n đang hoạt động (Self-hosted hoặc n8n Cloud).
- **Telegram Bot Token**: Tạo bot thông qua `@BotFather` trên Telegram để lấy API Token.
- **Telegram Chat ID**: ID của kênh, nhóm hoặc chat cá nhân mà bot sẽ gửi tin nhắn đến.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này và dán trực tiếp vào n8n Editor của mình, hoặc import từ file JSON có sẵn. Workflow bao gồm các node chính sau:
- **Market Hours Trigger1** (`scheduleTrigger`): Lên lịch chạy tự động trong khung giờ giao dịch thị trường.
- **Fetch Natural Gas Page1** (`httpRequest`): Gọi và tải mã nguồn trang web chứa dữ liệu giá Henry Hub.
- **Extract Spot & Futures1** (`code`): Node xử lý Javascript để bóc tách giá Spot và 12 hợp đồng tương lai.
- **Build HTML Table1** (`code`): Định dạng dữ liệu thô thành bảng HTML chuyên nghiệp.
- **Send Telegram Update1** (`telegram`): Gửi bản tin hoàn chỉnh tới Telegram.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node `MarketHoursTrigger1`**: Điều chỉnh lại múi giờ (Time Zone) và lịch chạy cho phù hợp với giờ địa phương hoặc khung giờ thị trường năng lượng mà các sếp muốn theo dõi.
- **Node `SendTelegramUpdate1`**: 
  - Kết nối tài khoản của các sếp bằng cách điền **Telegram Bot API Token**.
  - Thay thế chuỗi `YOUR_TELEGRAM_CHAT_ID` bằng Chat ID thật của kênh hoặc nhóm Telegram nhận thông tin.

#### 3. Kích hoạt ⚡️
- Nhấn nút **'Test Workflow'** để chạy thử thủ công và kiểm tra xem tin nhắn đã bắn về Telegram thành công chưa.
- Nếu mọi thứ hiển thị đẹp mắt, gạt công tắc sang **Active** để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh nhận tin:** Các sếp có thể kết hợp thêm node Slack, Discord hoặc gửi email tự động bên cạnh Telegram.
- **Lưu lịch sử giá:** Thêm một node Google Sheets hoặc Database (PostgreSQL/Supabase) để lưu lại lịch sử biến động giá qua từng khung giờ, phục vụ cho việc phân tích kỹ thuật sau này.
- **Cảnh báo biến động mạnh:** Tách logic trong code node để nếu giá thay đổi vượt mức % nhất định, bot sẽ gửi tin nhắn khẩn cấp (Alert) thay vì bản tin thông thường.

### 📌 Kết luận
Một giải pháp tuyệt vời, tinh gọn và hoàn toàn miễn phí để theo dõi sát sao thị trường khí tự nhiên ngay trên chiếc điện thoại của mình. Hãy setup ngay hôm nay để tối ưu hóa quy trình cập nhật thông tin tài chính của các sếp!