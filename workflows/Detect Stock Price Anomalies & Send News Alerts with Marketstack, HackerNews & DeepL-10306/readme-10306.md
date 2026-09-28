---
title: "🚀 Tự động phát hiện biến động giá cổ phiếu và gửi cảnh báo tin tức với Marketstack, HackerNews & DeepL"
description: "Hướng dẫn xây dựng workflow n8n tự động kiểm tra giá cổ phiếu mỗi ngày, phát hiện bất thường qua ±2σ, quét tin tức liên quan, dịch thuật AI và bắn cảnh báo về Slack."
slug: "tu-dong-phat-hien-bien-dong-gia-co-phieu-va-tin-tuc"
tags: [n8n, automation, trading, stock-market, deepl, slack]
keywords: [n8n workflow, phát hiện biến động giá, marketstack, deepl n8n, slack alert, tự động hóa tài chính]
---

# 🚀 Tự động phát hiện biến động giá cổ phiếu & Cảnh báo tin tức thông minh

Các nhà đầu tư và nhà giao dịch thường tốn rất nhiều thời gian mỗi ngày để theo dõi biểu đồ giá, kiểm tra các khoản đầu tư và tìm kiếm nguyên nhân đằng sau những cú sập hoặc tăng giá đột biến. Việc làm thủ công này không chỉ mệt mỏi mà còn dễ bỏ lỡ các cơ hội vàng.

Bài viết này sẽ hướng dẫn các sếp thiết lập một workflow n8n tự động hóa toàn bộ quy trình: Từ việc lấy dữ liệu giá cổ phiếu qua Marketstack, tính toán độ lệch chuẩn (±2σ), phát hiện bất thường, quét tin tức liên quan từ Hacker News, dịch thuật thông minh bằng DeepL cho đến việc bắn thông báo song ngữ trực tiếp về Slack. Không cần code phức tạp, tự động 100%!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động 24/7:** Chạy đều đặn mỗi sáng theo lịch hẹn mà không cần can thiệp thủ công.
- **Phát hiện thông minh:** Tự động tính toán đường trung bình 20 ngày và biên độ lệch chuẩn (±2σ) để lọc ra các phiên giao dịch bất thường.
- **Cập nhật tin tức & Dịch thuật:** Tự động tìm kiếm tin tức liên quan và dịch sang ngôn ngữ mong muốn (mặc định tiếng Nhật hoặc tùy chỉnh).
- **Cảnh báo tức thì:** Gửi báo cáo chi tiết về Slack cho cả trường hợp thị trường bình thường hay có biến động mạnh.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Marketstack API Key**: Để lấy dữ liệu giá đóng cửa cổ phiếu (EOD).
- **DeepL API Key**: Để dịch nội dung tin tức tự động.
- **Slack OAuth2 (Bot Token)**: Để gửi tin nhắn cảnh báo vào channel chỉ định.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow trống trong n8n, sau đó copy toàn bộ mã JSON của workflow (từ ID 10306) và paste trực tiếp vào giao diện n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 12 nodes phối hợp nhịp nhàng. Các sếp cần chú ý cấu hình các điểm sau:
- **Daily Check (`scheduleTrigger`)**: Mặc định đặt lịch chạy lúc 09:00 JST (Giờ Nhật Bản). Các sếp nhớ điều chỉnh múi giờ hoặc giờ chạy cho phù hợp với nhu cầu thực tế.
- **Get Stock Data (`marketstack`)**: Kết nối **Marketstack API Credentials** của sếp. Điền mã cổ phiếu (Ticker symbol) muốn theo dõi và giữ giới hạn limit ≥ 20 để thuật toán tính toán độ lệch chuẩn chính xác.
- **Calculate Deviation (`code`)**: Node này thực hiện tính toán giá trị trung bình 20 ngày và độ lệch chuẩn ($\pm2\sigma$). Có thể tinh chỉnh hệ số $k$ bên trong code nếu muốn thắt chặt hoặc nới lỏng biên độ cảnh báo.
- **Translate News (`deepL`)**: Kết nối **DeepL API Credentials** để dịch tiêu đề/tóm tắt tin tức sang ngôn ngữ đích (mặc định là tiếng Nhật `JA`, có thể đổi thành `VI` nếu thích).
- **Send Alert to Slack / Send Normal Report to Slack (`slack`)**: Kết nối tài khoản Slack và chọn channel (`slackChannel`) nhận thông báo cho cả 2 node này.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** để chạy thử nghiệm (Test run) với dữ liệu hiện tại và kiểm tra xem tin nhắn đã bắn về Slack chuẩn form chưa.
- Nếu mọi thứ mượt mà, bật công tắc **Active** ở góc trên bên phải để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa dạng hóa mã cổ phiếu:** Nhân bản node **Get Stock Data** và dùng node **Merge** để theo dõi nhiều mã cổ phiếu cùng lúc (ví dụ: AAPL, TSLA, BTC...).
- **Mở rộng nguồn tin:** Thay thế hoặc kết hợp **Hacker News** với **NewsAPI** hoặc **Google News RSS** để quét được nhiều bài báo tài chính chất lượng hơn.
- **Đa kênh thông báo:** Thay vì chỉ gửi Slack, các sếp có thể tích hợp thêm node **Telegram Bot** hoặc **Discord** để nhận cảnh báo ngay trên điện thoại cá nhân.
- **Tối ưu chi phí DeepL:** Thêm một điều kiện IF để chỉ dịch tin tức khi ngôn ngữ bài viết gốc khác với ngôn ngữ mục tiêu.

### 📌 Kết luận
Với workflow n8n này, các sếp đã sở hữu ngay một "trợ lý tài chính" tự động theo dõi sức khỏe thị trường mỗi ngày, giúp tiết kiệm hàng giờ soi biểu đồ và nắm bắt tin tức nóng hổi ngay lập tức. Lên đồ và áp dụng ngay thôi các sếp!