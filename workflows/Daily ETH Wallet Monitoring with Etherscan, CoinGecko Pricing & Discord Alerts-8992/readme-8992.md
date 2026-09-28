---
title: "🚀 Tự Động Hóa Theo Dõi Ngân Hàng ETH Hàng Ngày: Giá Trị Wallet + Giá ETH + Cảnh Báo Discord (Không Cần Code)"
description: "Workflow tự động theo dõi số dư ETH hàng ngày từ Etherscan, giá thị trường từ CoinGecko và gửi cảnh báo tự động lên Discord. Giúp các sếp quản lý tài sản DeFi một cách hiệu quả, tiết kiệm thời gian và tránh bỏ lỡ cơ hội."
slug: "tieu-dong-hoa-theo-doi-ngan-hang-eth-hang-ngay"
tags: [n8n, automation, blockchain, etherscan, coingecko, discord, crypto, no-code]
keywords: [tự động hóa theo dõi ETH, n8n workflow crypto, cảnh báo giá ETH Discord, theo dõi số dư wallet ETH tự động, tự động hóa DeFi]
---

# 🚀 **Tự Động Hóa Theo Dõi Ngân Hàng ETH Hàng Ngày: Giá Trị Wallet + Giá ETH + Cảnh Báo Discord**

### **🔥 Nỗi Đau Của Các Sếp Trong Thời Đại DeFi**
Hàng ngày, các sếp phải:
- **Tra cứu số dư ETH** trên Etherscan để kiểm tra tài sản.
- **Theo dõi giá ETH** trên CoinGecko để đánh giá thị trường.
- **Bỏ lỡ cơ hội** vì không nhận được cảnh báo kịp thời khi giá dao động mạnh.
- **Tốn thời gian** phải làm thủ công mỗi ngày, đặc biệt khi quản lý nhiều wallet.

**Workflow này giải quyết tất cả!** Với **n8n**, các sếp có thể tự động:
✅ **Lấy số dư ETH** từ Etherscan hàng ngày.
✅ **Lấy giá ETH** từ CoinGecko.
✅ **Tính toán giá trị USD** của wallet.
✅ **Gửi cảnh báo tự động** lên Discord vào sáng và tối.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần tra cứu thủ công hàng ngày.
- **Tính chính xác cao**: Dữ liệu từ Etherscan và CoinGecko được cập nhật tự động.
- **Cảnh báo kịp thời**: Nhận thông báo giá trị wallet và biến động giá ETH trên Discord.
- **Hoạt động 24/7**: Workflow chạy tự động theo lịch trình, không cần can thiệp.
- **Dễ dàng mở rộng**: Thêm wallet hoặc thay đổi thông báo theo nhu cầu.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **API Key Etherscan**:
   - Đăng ký tại [Etherscan API](https://etherscan.io/apis) và lấy **API Key**.
   - **Lưu ý**: API Key này sẽ được sử dụng trong **2 node HTTP Request** đầu tiên.
2. **Wallet Address**:
   - Điền **địa chỉ ETH** của mình vào **Code Block** (node `Code ETH Balance`).
3. **Webhook Discord**:
   - Tạo một **webhook** trên Discord và sao chép **URL Webhook**.
   - Thiết lập trong node **Discord** để nhận cảnh báo.
4. **API Key CoinGecko** (nếu muốn lấy giá ETH chính xác hơn):
   - Đăng ký tại [CoinGecko API](https://www.coingecko.com/en/api) và lấy **API Key**.
   - **Lưu ý**: Workflow hiện tại sử dụng **HTTP Request** để lấy giá ETH từ CoinGecko, nhưng nếu muốn tối ưu, các sếp có thể thêm API Key vào node `HTTP Request ETH Price`.

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/8992](https://n8n.io/workflows/8992) và import vào n8n Editor.
- **Cách 2**: Sao chép toàn bộ JSON từ trang trên và dán vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
##### **A. Cấu Hình Node `HTTP Request` (Etherscan)**
- **Node 1 (`HTTP Request`)**:
  - **Method**: `GET`
  - **URL**: `https://api.etherscan.io/api?module=account&action=balance&address={WALLET_ADDRESS}&tag=latest&apikey={ETHERSCAN_API_KEY}`
  - **Thay thế `{WALLET_ADDRESS}`** bằng địa chỉ ETH của mình.
  - **Thay thế `{ETHERSCAN_API_KEY}`** bằng API Key từ Etherscan.
- **Node 2 (`HTTP Request1`)**:
  - **Method**: `GET`
  - **URL**: `https://api.etherscan.io/api?module=account&action=txlist&address={WALLET_ADDRESS}&startblock=0&endblock=99999999&sort=asc&apikey={ETHERSCAN_API_KEY}`
  - **Thay thế `{WALLET_ADDRESS}` và `{ETHERSCAN_API_KEY}`** tương tự.

##### **B. Cấu Hình Node `Code ETH Balance`**
- Mở node **`Code ETH Balance`** và thay thế:
  ```javascript
  // Thay thế WALLET_ADDRESS bằng địa chỉ ETH của bạn
  const walletAddress = "0xYOUR_WALLET_ADDRESS_HERE";
  ```
- **Lưu ý**: Node này sẽ **tính toán số dư ETH** và chuyển đổi thành **ETH** (không phải wei).

##### **C. Cấu Hình Node `HTTP Request ETH Price` (CoinGecko)**
- **Method**: `GET`
- **URL**: `https://api.coingecko.com/api/v3/simple/price?ids=ethereum&vs_currencies=usd`
- **Lưu ý**: Nếu muốn sử dụng API Key, thêm vào URL:
  `https://api.coingecko.com/api/v3/simple/price?ids=ethereum&vs_currencies=usd&x_cg_demo_api_key={YOUR_API_KEY}`.

##### **D. Cấu Hình Node `Discord`**
- **Webhook URL**: Dán **URL Webhook** từ Discord vào trường `Webhook URL`.
- **Message Format**: Workflow sẽ tự động tạo thông báo với nội dung:
  ```
  **ETH Wallet Balance Update**
  - **Wallet**: {WALLET_ADDRESS}
  - **ETH Balance**: {ETH_BALANCE}
  - **USD Value**: ${ETH_BALANCE * ETH_PRICE}
  - **ETH Price**: ${ETH_PRICE} USD
  ```

##### **E. Cấu Hình Schedule Trigger**
- **Cron Expression**: `0 0 * * *` (chạy vào **giờ 00:00** mỗi ngày).
- **Lưu ý**: Workflow sẽ chạy **hai lần/ngày** (sáng và tối) do có **Schedule Trigger** và **Code Block** điều khiển.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Chạy **Manual Trigger** để kiểm tra dữ liệu đầu ra.
   - Kiểm tra **Discord** có nhận được thông báo không.
2. **Bật Active**:
   - Sau khi kiểm tra thành công, **bật Active** cho workflow.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[MỞ RỘNG THÊM TÍNH NĂNG]
1. **Thêm Wallet Khác**:
   - Sao chép và thay đổi **Wallet Address** trong node `Code ETH Balance` để theo dõi nhiều wallet.
2. **Gửi Báo Cáo Định Kỳ**:
   - Thêm node **Google Sheets** hoặc **Email** để lưu lịch sử giá trị wallet.
3. **Cảnh Báo Giá Threshold**:
   - Sử dụng node **Code** để so sánh giá ETH với ngưỡng nhất định (ví dụ: `if (ethPrice > 3000) { sendAlert() }`).
4. **Kết Nối Telegram**:
   - Thay thế node **Discord** bằng **Telegram Bot** để nhận cảnh báo trên Telegram.
5. **Lưu Log Dữ Liệu**:
   - Thêm node **Sticky Note** hoặc **Database** để lưu trữ lịch sử số dư và giá ETH.
:::

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn **tự động hóa quản lý tài sản DeFi** một cách đơn giản, không cần code. Với **n8n**, các sếp có thể:
✔ **Tiết kiệm thời gian** tra cứu hàng ngày.
✔ **Nhận cảnh báo kịp thời** khi giá ETH thay đổi.
✔ **Quản lý nhiều wallet** một cách dễ dàng.

**Hãy áp dụng ngay và bắt đầu tự động hóa cuộc sống DeFi của mình!** 🚀

---
:::note[CHÚ Ý]
- **Etherscan API Free** có giới hạn gọi API (1000/ngày). Nếu vượt quá, cần nâng cấp lên **API Pro**.
- **CoinGecko API Free** cũng có giới hạn. Nếu muốn sử dụng API Key, đăng ký tại [CoinGecko](https://www.coingecko.com/en/api).
- **N8n Self-Hosted** được khuyến cáo để workflow chạy ổn định 24/7.
:::