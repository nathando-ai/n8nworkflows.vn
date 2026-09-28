---
title: "🚀 Tự Động Hóa Giao Dịch Sàn Alpaca Với AI: Đóng Góp & Mua Sát Tích Theo Sentiment - Không Cần Code"
description: "Workflow này tự động phân tích sentiment từ Google Sheets, so sánh với danh sách cổ phiếu đang nắm giữ trên sàn Alpaca, và thực hiện giao dịch bán/ mua tự động để tối ưu hóa portfolio. Giúp các sếp tiết kiệm thời gian, giảm thiểu rủi ro và tối ưu hóa hiệu suất giao dịch 24/7."
slug: "tieu-dong-hoa-giao-dich-san-alpaca-voi-ai"
tags: [n8n, automation, trading, alpaca, google-sheets, ai, crypto-trading]
keywords: [tự động hóa giao dịch alpaca, sentiment analysis trading, n8n workflow giao dịch, tự động hóa sàn chứng khoán, trading bot không code]
---

# 🚀 **Tự Động Hóa Giao Dịch Sàn Alpaca Với AI: Đóng Góp & Mua Sát Tích Theo Sentiment**

## **📌 Nỗi Đau Của Các Sếp Trong Giao Dịch Tự Động Hóa**
Bạn đã bao giờ mệt mỏi vì phải:
- **Theo dõi sentiment** của thị trường hàng ngày để quyết định mua/bán?
- **Thủ công so sánh** danh sách cổ phiếu đang nắm giữ với những cổ phiếu có sentiment tích cực?
- **Lo lắng rủi ro** khi giao dịch không đồng bộ hoặc thiếu logic tự động?
- **Không có thời gian** để phân tích dữ liệu và tối ưu hóa portfolio?

Workflow này **giải quyết tất cả** bằng cách kết hợp **AI phân tích sentiment** (được cung cấp từ workflow khác) với **trading tự động trên sàn Alpaca**, giúp bạn:
✅ **Tự động đóng góp cổ phiếu không còn trong top sentiment** và mua những cổ phiếu có sentiment cao nhất.
✅ **Tối ưu hóa portfolio** bằng cách phân bổ vốn một cách logic.
✅ **Lưu trữ tất cả giao dịch** vào Google Sheets để theo dõi hiệu suất.
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm thời gian**: Không cần theo dõi thị trường hàng ngày.
- **Giảm thiểu rủi ro**: Giao dịch tự động theo logic AI, không phụ thuộc vào cảm xúc.
- **Tối ưu hóa hiệu suất**: Chỉ giữ những cổ phiếu có sentiment tích cực và bán những cổ phiếu không còn phù hợp.
- **Dữ liệu minh bạch**: Tất cả giao dịch được ghi lại trong Google Sheets, giúp phân tích hiệu suất dễ dàng.
- **Hoạt động liên tục**: Workflow chạy tự động hàng ngày (4:45 PM UTC+2), không cần can thiệp.
:::

---
### **🔧 Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ**]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Alpaca** (đang sử dụng chế độ **Paper Trading** để tránh rủi ro thực tế).
   - **API Key & Secret Key** của Alpaca (đăng ký tại [Alpaca Marketplace](https://alpaca.markets/)).
   - **Base URL**: Chọn `https://paper-api.alpaca.markets` (hoặc `https://api.alpaca.markets` nếu dùng chế độ thực).
2. **Google Sheets** với cấu trúc sau:
   - **Sheet "balance"**: Để ghi lại số dư và biến động hàng ngày.
   - **Sheet "sentiments"**: Được cung cấp bởi workflow **Sentiment Analysis Bot** ([liên kết](https://n8n.io/workflows/5369-automated-stock-sentiment-analysis-with-google-gemini-and-eodhd-news-api/)).
   - **Sheet "positions"**: Để ghi lại lịch sử giao dịch (mua/bán).
3. **n8n Self-hosted** (không dùng phiên bản miễn phí trên cloud để đảm bảo hoạt động 24/7).

---
### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [liên kết gốc](https://n8n.io/workflows/5711) hoặc copy toàn bộ mã JSON từ trang này.
- Mở **n8n Editor**, nhấn **"Import"** và dán JSON vào.
- **Lưu workflow** với tên **"Alpaca AI Trading"** (hoặc tên tùy ý).

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **14 node**, nhưng các node quan trọng nhất cần cấu hình cẩn thận:

##### **🔹 Node "Schedule Trigger" (Động cơ Khởi Động)**
- **Thời gian chạy**: Đặt thành **4:45 PM (UTC+2)** để chạy sau khi thị trường Mỹ mở cửa.
- **Lịch trình**: Chọn **"Daily"** (hàng ngày).
- **Lưu ý**: Nếu dùng VPS ở khu vực khác, điều chỉnh múi giờ phù hợp.

##### **🔹 Node "Alpaca-get-account-info" (Lấy Thông Tin Tài Khoản)**
- **URL**: `https://paper-api.alpaca.markets/v2/account`
- **Headers**:
  - `APCA-API-KEY-ID`: Điền **API Key** của Alpaca.
  - `APCA-API-SECRET-KEY`: Điền **Secret Key** của Alpaca.
- **Method**: `GET`

##### **🔹 Node "read_sentiments_score_today" (Đọc Sentiment Từ Google Sheets)**
- **Google Sheets OAuth 2.0 Credentials**: Cấu hình từ **n8n Credentials Manager** (nếu chưa có, tạo mới).
- **Sheet Name**: `"sentiments"` (phải trùng với sheet trong Google Sheets của bạn).
- **Range**: `"Today"` (hoặc `"Sheet1!A1:Z1000"` nếu cần điều chỉnh).

##### **🔹 Node "write_account_balace_today" (Ghi Số Dư Hàng Ngày)**
- **Google Sheets OAuth 2.0 Credentials**: Cùng với node trên.
- **Sheet Name**: `"balance"`.
- **Range**: `"A1"` (để ghi dữ liệu từ ô A1).
- **Operation**: `"appendOrUpdate"` (để cập nhật số dư mới).

##### **🔹 Node "Alpaca-post-order-sell" & "Alpaca-post-order-buy" (Giao Dịch)**
- **URL**:
  - **Sell**: `https://paper-api.alpaca.markets/v2/order`
  - **Buy**: `https://paper-api.alpaca.markets/v2/order`
- **Headers**: Cùng với node `Alpaca-get-account-info`.
- **Body (JSON)**:
  ```json
  {
    "symbol": "{{$node["positions_to_close"].json["symbol"]}}",
    "qty": "{{$node["positions_to_close"].json["qty"]}}",
    "side": "sell",  // hoặc "buy"
    "type": "market",
    "time_in_force": "gtc"
  }
  ```
  - **Lưu ý**: Node **`create_positions_to_close_and_positions_two_open`** (Code) sẽ tự động tính toán `qty` và `symbol` dựa trên logic.

##### **🔹 Node "Google Sheets (Append)" (Ghi Lịch Sử Giao Dịch)**
- **Google Sheets OAuth 2.0 Credentials**: Cùng với các node trước.
- **Sheet Name**: `"positions"`.
- **Range**: `"A1"` (để ghi dữ liệu từ ô A1).
- **Operation**: `"append"` (thêm mới mỗi giao dịch).

##### **🔹 Node "Wait" (Chờ 2 Phút Trước Giao Dịch Mua)**
- **Thời gian**: `120000` ms (2 phút) để đảm bảo tiền từ giao dịch bán đã được cập nhật.

---
#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **"Execute Workflow"** để kiểm tra các node hoạt động như thế nào.
   - Kiểm tra **Google Sheets** xem dữ liệu có được ghi lại không.
2. **Bật Active**:
   - Sau khi test thành công, chuyển trạng thái workflow sang **"Active"**.

---
### **✍️ Mẹo & Gợi Ý Nâng Cao**
:::info[**CÁC Ý TƯỞNG MỞ RỘNG**]
1. **Kết Nối Slack/Telegram** để nhận thông báo khi giao dịch thành công/bất thành công:
   - Sử dụng node **`n8n-nodes-base.slack`** hoặc **`n8n-nodes-base.telegram`** sau node **"Google Sheets (Append)"**.
   - Ví dụ: Gửi tin nhắn `"📈 Giao dịch thành công: Bán {{symbol}} với giá {{price}}"` khi sell hoặc buy.

2. **Lưu Log Chi Tiết** vào Google Drive hoặc AWS S3:
   - Sử dụng node **`n8n-nodes-base.googleDrive`** hoặc **`n8n-nodes-base.awsS3`** để lưu file log hàng ngày.

3. **Tối Ưu Hóa Thời Gian Chạy**:
   - Nếu thị trường mở cửa sớm hơn, điều chỉnh **Schedule Trigger** để workflow chạy trước khi thị trường bắt đầu.

4. **Thêm Logic Stop-Loss**:
   - Sử dụng node **`n8n-nodes-base.code`** để thêm điều kiện dừng lỗ (ví dụ: bán nếu giá xuống dưới ngưỡng nhất định).

5. **Kết Hợp Với Binance/Bybit**:
   - Nếu muốn mở rộng sang sàn khác, thay thế node **`Alpaca-post-order-sell/buy`** bằng API của Binance/Bybit.
---
### **📌 Kết Luận**
Workflow này **không chỉ tự động hóa giao dịch**, mà còn **tối ưu hóa portfolio** dựa trên sentiment thị trường, giúp các sếp:
✔ **Tiết kiệm thời gian** với giao dịch tự động.
✔ **Giảm thiểu rủi ro** bằng logic AI.
✔ **Theo dõi hiệu suất** một cách minh bạch.

**🚀 Hãy áp dụng ngay và bắt đầu giao dịch thông minh hơn!**
Nếu có vấn đề, hãy để lại **comment** bên dưới hoặc liên hệ với tác giả [Raz Hadas](https://www.linkedin.com/in/raz-hadas/) để hỗ trợ.

---
:::info[**Gợi Ý Hạ Tầng Cho n8n**]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**🔗 [Tải Workflow Nguyên Bản](https://n8n.io/workflows/5711)** | **📖 [Workflow Sentiment Analysis](https://n8n.io/workflows/5369)**