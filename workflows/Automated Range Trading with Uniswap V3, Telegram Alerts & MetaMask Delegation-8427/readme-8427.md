---
title: "🚀 Tự Động Hóa Giao Dịch Range Trading trên Uniswap V3 với Telegram Alert & MetaMask Delegation"
description: "Workflow tự động hóa giao dịch range trading trên Uniswap V3, gửi cảnh báo Telegram và quản lý MetaMask thông qua MetaMask Delegation - giúp các sếp tối ưu hóa thời gian và giảm thiểu rủi ro trong trading 24/7."
slug: "tieu-dong-hoa-giao-dich-range-trading-uniswap-v3-telegram-alert"
tags: [n8n, automation, blockchain, trading, uniswap, telegram, metamask, 1shot-api, no-code]
keywords: [tự động hóa giao dịch crypto, range trading uniswap v3, telegram alert trading, metamask delegation n8n, 1shot api n8n, tự động hóa trading 24/7]
---

# 🚀 **Tự Động Hóa Giao Dịch Range Trading trên Uniswap V3 với Telegram Alert & MetaMask Delegation**

Hiện nay, các sếp và nhà đầu tư crypto thường phải theo dõi thị trường 24/7 để bắt được cơ hội giao dịch range trading, đồng thời phải thủ công xác nhận giao dịch trên MetaMask và quản lý thông báo. Điều này không chỉ tốn thời gian mà còn dễ mắc lỗi do mệt mỏi hoặc thiếu tập trung.

**Workflow này giải quyết tất cả vấn đề đó bằng cách:**
- **Tự động hóa giao dịch range trading** trên Uniswap V3 với logic mua/bán tự động dựa trên ngưỡng giá đã thiết lập.
- **Gửi cảnh báo Telegram** để các sếp được thông báo ngay khi giao dịch thành công hoặc thất bại.
- **Sử dụng MetaMask Delegation** để thực hiện giao dịch mà không cần phải mở MetaMask liên tục.
- **Kiểm tra và cập nhật số dư** tự động trước khi thực hiện giao dịch.
- **Hỗ trợ giao dịch ETH/USDC** (có thể mở rộng cho các cặp token khác).

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần theo dõi thị trường liên tục, workflow chạy tự động theo lịch trình.
- **Tăng chính xác**: Tránh lỗi do thủ công, giao dịch được thực hiện theo logic đã lập trình.
- **Cảnh báo tức thời**: Nhận thông báo Telegram ngay khi giao dịch thành công/thất bại.
- **An toàn và tự động hóa**: MetaMask Delegation cho phép giao dịch mà không cần xác nhận thủ công.
- **Dễ mở rộng**: Có thể điều chỉnh ngưỡng giá, token và logic giao dịch theo nhu cầu.
:::

---

## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản 1Shot API**:
   - [Đăng ký tài khoản 1Shot API](https://1shotapi.com/) và tạo **API Key**.
   - Cài đặt **credentials** cho n8n bằng cách thêm `oneShotOAuth2Api` với API Key và Secret Key từ 1Shot API.
2. **Tài khoản Telegram**:
   - Tạo **bot Telegram** và lấy **chatID** của bot (có thể sử dụng [@userinfobot](https://t.me/userinfobot) để lấy chatID).
   - Thêm **credentials** cho n8n với API Token của bot và chatID.
3. **MetaMask Delegation**:
   - Cài đặt **MetaMask** và tạo một ví mới (hoặc sử dụng ví hiện có).
   - Cung cấp **wallet address** (địa chỉ MetaMask) trong node `Swap Configs` để workflow thực hiện giao dịch thay mặt.
4. **Số dư USDC và ETH**:
   - Đảm bảo ví MetaMask có đủ **USDC** để mua ETH hoặc **ETH** để bán (tùy thuộc vào logic giao dịch).
5. **Uniswap V3 Pool**:
   - Workflow mặc định sử dụng pool **ETH/USDC** trên Uniswap V3. Nếu muốn sử dụng pool khác, cần cập nhật các tham số như `token0`, `token1`, `fee`, và `SwapRouter` address.
6. **VPS cho n8n**:
   - Để workflow chạy 24/7, các sếp nên cài n8n trên **VPS** (Self-hosted).
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### 1. **Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Tải file JSON từ [link gốc](https://n8n.io/workflows/8427) hoặc copy toàn bộ JSON từ đây.
2. Mở **n8n Editor** và nhấn **Import Workflow** (hoặc nhấn `Ctrl + I`).
3. Chọn file JSON và nhấn **Import**.

### 2. **Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **37 node** và có nhiều bước cần cấu hình chi tiết. Dưới đây là hướng dẫn cụ thể:

#### **A. Cấu hình Swap Configs (Node Code)**
Node này quyết định logic giao dịch của workflow. Các sếp cần điền các tham số sau:
- **`amountUSDC`**: Số lượng USDC sẽ được sử dụng để mua ETH (ví dụ: `100`).
- **`upperPrice`**: Giá ETH cao nhất để bán (ví dụ: `2000`).
- **`lowerPrice`**: Giá ETH thấp nhất để mua (ví dụ: `1800`).
- **`delegator`**: Địa chỉ MetaMask sẽ được sử dụng để thực hiện giao dịch (copy từ ví MetaMask).
- **`telegramChatID`**: ChatID của bot Telegram để nhận cảnh báo.

**Tham số tùy chọn (nếu muốn thay đổi token hoặc chain):**
- **`SwapRouter`**: Địa chỉ hợp đồng SwapRouterV2 (mặc định là [0xE592427A0AEce92De3Edee1F18E0157C05861564](https://docs.uniswap.org/contracts/v3/reference/deployments)).
- **`token0` và `token1`**: Địa chỉ token (ETH và USDC mặc định).
- **`token0Decimals` và `token1Decimals`**: Số chữ số thập phân của token (ETH: 18, USDC: 6).
- **`fee`**: Phí pool (ví dụ: `500` cho 0.5%).
- **`slippage`**: Phí trượt (ví dụ: `1` cho 1%).

#### **B. Cấu hình 1Shot API Credentials**
Workflow sử dụng **1Shot API** để tương tác với Uniswap V3 và MetaMask. Các sếp cần:
1. Tạo **credentials** trong n8n với tên `oneShotOAuth2Api`.
2. Điền **API Key** và **Secret Key** từ tài khoản 1Shot API.
3. Cập nhật các node `oneShot` theo hướng dẫn trong phần **Ghi chú từ tác giả** (xem dưới đây).

#### **C. Cấu hình Telegram**
1. Tạo **bot Telegram** và lấy **API Token** (từ [@BotFather](https://t.me/BotFather)).
2. Tạo **credentials** trong n8n với tên `telegramApi`.
3. Điền **API Token** và **chatID** của bot.
4. Các node Telegram sẽ tự động gửi cảnh báo khi giao dịch thành công/thất bại.

#### **D. Cấu hình MetaMask Delegation**
Workflow sử dụng **MetaMask Delegation** để thực hiện giao dịch thay mặt. Các sếp không cần làm gì thêm ngoài việc cung cấp **wallet address** trong `Swap Configs`.

#### **E. Cập nhật các node 1Shot**
Theo ghi chú từ tác giả, các sếp cần cập nhật các node `oneShot` như sau:
1. **`Fetch Pool TWA Observations`**:
   - Đặt `operation` = `read` và chỉ định pool Uniswap V3 (ví dụ: [ETH/USDC Base](https://app.uniswap.org/explore/pools/base/0xfBB6Eed8e7aa03B138556eeDaF5D271A5E1e43ef)).
2. **`Get Sell Quote` và `Get Buy Quote`**:
   - Đặt `operation` = `simulate` và chỉ định `quoteExactInputSingle` trên hợp đồng **QuoterV2**.
3. **`Give Approval to Router (Buy)`**:
   - Đặt `operation` = `executeAsDelegator` và gọi `approve` trên **USDC**.
4. **`Give Approval to Router (Sell)`**:
   - Đặt `operation` = `executeAsDelegator` và gọi `approve` trên **WETH**.
5. **`Sell ETH` và `Buy ETH`**:
   - Đặt `operation` = `executeAsDelegator` và gọi `exactInputSingle` trên hợp đồng **SwapRouterV2**.
6. **`Check New Funds` và `Check Remaining Funds`**:
   - Đặt `operation` = `read` và gọi `balanceOf` trên hợp đồng **USDC**.

#### **F. Khởi tạo Wallet và Methods**
1. Chạy node **`When clicking ‘Execute workflow’`** (Manual Trigger) để khởi tạo wallet và các method cần thiết.
2. Workflow sẽ tự động:
   - Tạo wallet mới (nếu chưa có).
   - Đảm bảo các method cần thiết của hợp đồng (WETH, USDC, QuoterV2, SwapRouterV2, ETH/USDC Pool) được kích hoạt.

---

### 3. **Kích hoạt ⚡️**
1. **Test Run**:
   - Chạy workflow với **test mode** để kiểm tra logic và cảnh báo Telegram.
   - Đảm bảo các node như `Buy or Cancel?`, `Sell or Cancel?`, và `Confirm Buy/Sell` hoạt động như mong đợi.
2. **Bật Active**:
   - Sau khi kiểm tra xong, chuyển workflow sang **Active** và chọn **Schedule Trigger** để chạy theo lịch trình (ví dụ: mỗi 15 phút).

---

## ✍️ **Mẹo & gợi ý nâng cao**
:::info[MỞ RỘNG THÊM TÍNH NĂNG]
1. **Gửi báo cáo định kỳ**:
   - Sử dụng node **Telegram** để gửi báo cáo tổng hợp giao dịch hàng ngày/tuần.
   - Ví dụ: "Hôm nay đã mua 2 lần ETH và bán 1 lần, tổng lợi nhuận: +$50".
2. **Kết hợp với Discord**:
   - Thay vì Telegram, các sếp có thể cấu hình node **Discord Webhook** để nhận cảnh báo trên Discord.
3. **Lưu log giao dịch**:
   - Sử dụng node **Google Sheets** hoặc **Airtable** để lưu lịch sử giao dịch.
4. **Cập nhật ngưỡng giá tự động**:
   - Sử dụng node **Code** để tính toán ngưỡng giá dựa trên chỉ số RSI hoặc MACD từ API như CoinGecko.
5. **Hỗ trợ nhiều ví**:
   - Sử dụng node **List wallets** để quản lý nhiều ví MetaMask và phân bổ giao dịch cho từng ví.
6. **Cảnh báo giá đột biến**:
   - Thêm node **Code** để kiểm tra biến động giá và gửi cảnh báo nếu giá thay đổi quá nhanh.
:::

---

## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa giao dịch range trading trên Uniswap V3 mà không cần code. Bằng cách kết hợp **Telegram Alert**, **MetaMask Delegation** và **1Shot API**, workflow sẽ giúp các sếp:
- **Tiết kiệm thời gian** và tập trung vào chiến lược đầu tư.
- **Giảm thiểu rủi ro** do giao dịch thủ công.
- **Cập nhật tức thời** thông qua Telegram.

**Hãy import workflow ngay hôm nay và bắt đầu tự động hóa giao dịch của mình!** 🚀

---
**🔗 [Tải workflow JSON](https://n8n.io/workflows/8427)**
**📺 [Hướng dẫn chi tiết trên YouTube](https://www.youtube.com/watch?v=Hppd04sM4xE)**