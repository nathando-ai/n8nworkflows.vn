---
title: "🚀 Nhận Dữ Liệu Bitcoin, Ethereum, Solana & Binance Coin Từ CoinGecko & Gửi Gmail"
description: "Tự động lấy giá OHLC của 4 đồng tiền mã hóa từ CoinGecko, tổng hợp và gửi báo cáo qua Gmail chỉ với một workflow n8n."
slug: "nhan-du-lieu-crypto-coingecko-gmail"
tags: [n8n, automation, no-code, cryptocurrency, email, api]
keywords: [n8n workflow, tự động hóa, cryptocurrency, Gmail, CoinGecko, OHLC]
---

# 🚀 Nhận Dữ Liệu Bitcoin, Ethereum, Solana & Binance Coin Từ CoinGecko & Gửi Gmail

Bạn đã từng phải **điều tra giá thị trường** của các đồng tiền mã hoá mỗi ngày, sao chép dữ liệu từ website, rồi tự tay soạn email báo cáo?  
Công việc này **tiêu tốn thời gian**, dễ sai sót và không thể tự động hoá hoàn toàn nếu không có kỹ năng lập trình.

**Workflow này** sẽ giúp các sếp **lấy dữ liệu OHLC (Open‑High‑Low‑Close) của Bitcoin, Ethereum, Solana và Binance Coin** từ API miễn phí của **CoinGecko**, định dạng lại, gộp lại thành một báo cáo duy nhất và **gửi tự động qua Gmail** – mọi thứ diễn ra 100 % không cần viết code!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không còn phải mở nhiều trang web, sao chép dữ liệu thủ công.  
- **Độ chính xác 100 %**: Dữ liệu lấy trực tiếp từ API CoinGecko, giảm lỗi nhập liệu.  
- **Báo cáo cá nhân hoá**: Email được định dạng đẹp, chứa đầy đủ thông tin OHLC cho 4 đồng tiền.  
- **Hoạt động liên tục**: Workflow chạy tự động theo lịch, gửi báo cáo mỗi ngày/giờ tùy ý.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Gmail** (hoặc Google Workspace) để cấu hình node **Send Gmail**.  
- **API Key (không bắt buộc)**: CoinGecko cho phép truy cập không cần key, nhưng nếu bạn dùng proxy hoặc dịch vụ API khác, hãy chuẩn bị key tương ứng.  
- **n8n** đã được cài đặt và có quyền truy cập internet để gọi API CoinGecko.  
- **Quyền gửi email** cho tài khoản Gmail (bật “Less secure apps” hoặc tạo App Password nếu bật 2FA).  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập **n8n → Workflows → Import**.  
2. Tải file JSON từ link gốc: <https://n8n.io/workflows/4244> (hoặc sao chép nội dung JSON và dán vào ô **Import from Clipboard**).  
3. Nhấn **Import** → Workflow sẽ xuất hiện trong danh sách.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Dưới đây là **điểm danh các node** và **cách cấu hình** chi tiết:

| Node | Loại | Mô tả & Cấu hình cần chỉnh |
|------|------|-----------------------------|
| **Schedule** | scheduleTrigger | Đặt tần suất chạy (ví dụ: `Every day at 08:00` hoặc `Every hour`). |
| **Get BITCOIN OHLC** | httpRequest | - **Method**: GET <br> - **URL**: `https://api.coingecko.com/api/v3/coins/bitcoin/ohlc?vs_currency=usd&days=1` <br> - Không cần authentication. |
| **Get ETHEREUM OHLC** | httpRequest | - **URL**: `https://api.coingecko.com/api/v3/coins/ethereum/ohlc?vs_currency=usd&days=1` |
| **Get SOLANA OHLC** | httpRequest | - **URL**: `https://api.coingecko.com/api/v3/coins/solana/ohlc?vs_currency=usd&days=1` |
| **Get BINANCECOIN OHLC** | httpRequest | - **URL**: `https://api.coingecko.com/api/v3/coins/binancecoin/ohlc?vs_currency=usd&days=1` |
| **Format BTC** | code | JavaScript: chuyển mảng OHLC thành object có `open, high, low, close`. <br> **Lưu ý**: Đảm bảo `items[0]` là thời gian (timestamp) và `items[1..4]` là giá. |
| **Format ETH** | code | Tương tự như **Format BTC**, chỉ thay đổi tên biến. |
| **Format SOL** | code | Tương tự, đổi tên. |
| **Format BNB** | code | Tương tự, đổi tên. |
| **Merge 1 (BTC + ETH)** | merge | **Mode**: Append (hoặc Keep Key Order). Đầu vào: `Format BTC` và `Format ETH`. |
| **Merge 2 (+SOL)** | merge | **Mode**: Append. Đầu vào: output của **Merge 1** và **Format SOL**. |
| **Merge 3 (+BNB)** | merge | **Mode**: Append. Đầu vào: output của **Merge 2** và **Format BNB**. |
| **Combine All Coins** | code | Script tổng hợp 4 object thành một chuỗi HTML hoặc plain‑text để gửi email. <br> **Lưu ý**: Định dạng ngày giờ (UTC → local) nếu cần. |
| **Send Gmail** | gmail | - **Credentials**: Chọn tài khoản Gmail đã tạo. <br> - **To**: Địa chỉ nhận (có thể là danh sách). <br> - **Subject**: `📈 Báo cáo OHLC Crypto - {{ $now.format("DD/MM/YYYY") }}` <br> - **Body**: Dùng output của **Combine All Coins** (chọn **HTML** nếu muốn email đẹp). |

> **Tip**: Nếu bạn muốn nhận báo cáo qua nhiều người, nhập danh sách email cách nhau bằng dấu phẩy trong trường **To**.

#### 3. Kích hoạt ⚡️
1. **Test run**: Nhấn nút **Execute Workflow** → Kiểm tra log từng node, đặc biệt là các node `httpRequest` và `Send Gmail`.  
2. Nếu mọi thứ hiển thị dữ liệu đúng, **bật** công tắc **Active** ở góc phải màn hình.  
3. Kiểm tra hộp thư Gmail để xác nhận email đã tới.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo Slack/Telegram**: Thêm node **Slack** hoặc **Telegram** sau node **Combine All Coins** để gửi tin nhắn nhanh khi có biến động lớn (>5%).  
- **Lưu lịch sử**: Kết nối **Google Sheets** hoặc **Airtable** để ghi lại mỗi lần báo cáo, giúp phân tích xu hướng dài hạn.  
- **Alert giá ngưỡng**: Thêm node **IF** để so sánh `close` với mức ngưỡng tùy chỉnh, gửi email cảnh báo ngay lập tức.  
- **Chạy đa khu vực**: Sử dụng **Set** + **Timezone** để đồng bộ thời gian báo cáo theo múi giờ địa phương của các sếp.

### 📌 Kết luận
Với workflow này, các sếp sẽ **không còn phải tốn công sức thu thập và gửi báo cáo giá crypto**. Một lần thiết lập, n8n sẽ tự động lấy dữ liệu, định dạng và gửi email đúng giờ, giúp tập trung vào quyết định kinh doanh chứ không phải thao tác thủ công. Hãy **import ngay**, cấu hình Gmail và để n8n làm việc cho bạn! 🚀