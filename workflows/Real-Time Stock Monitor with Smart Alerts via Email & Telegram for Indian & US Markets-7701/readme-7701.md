---
title: "📈 Giám Sát Giá Cổ Phiếu Real-Time & Cảnh Báo Thông Minh (Email + Telegram)"
description: "Tự động hóa việc theo dõi giá cổ phiếu Ấn Độ & Mỹ, gửi cảnh báo tức thì qua Email và Telegram khi giá chạm ngưỡng, kèm cơ chế chống spam thông minh."
slug: "giam-sat-gia-co-phieu-real-time-va-canh-bao-thong-minh"
tags: [n8n, automation, stock-market, trading, telegram, email]
keywords: [n8n workflow, giám sát cổ phiếu, cảnh báo giá, tự động hóa trading, twelve data]
---

# 📈 Giám Sát Giá Cổ Phiếu Real-Time & Cảnh Báo Thông Minh (Email + Telegram)

Các sếp đang làm trading hay quản lý danh mục đầu tư chắc hẳn đều gặp phải nỗi đau: **phải mở liên tục 5-10 tab trình duyệt** để canh giá, hoặc cài đặt hàng loạt app riêng lẻ cho từng sàn (NSE, BSE, NYSE...). Khi giá biến động mạnh, việc phản ứng chậm 1-2 phút có thể đồng nghĩa với việc bỏ lỡ cơ hội hoặc cắt lỗ muộn.

Workflow này giải quyết triệt để vấn đề đó. Nó hoạt động như một "trợ lý giao dịch" không ngủ, tự động quét giá cổ phiếu theo thời gian thực, áp dụng logic thông minh để tránh spam thông báo, và đẩy cảnh báo ngay lập tức vào **Email** và **Telegram** của các sếp. Không cần code, không cần thuê server phức tạp, chỉ cần n8n là đủ.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 (đặc biệt quan trọng với trading), các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Phản ứng tức thì**: Nhận cảnh báo trong vòng vài giây khi giá chạm ngưỡng, nhanh hơn con người.
- **Chống Spam thông minh**: Cơ chế "Cooldown" tự động ngăn chặn việc gửi hàng chục email/telegram liên tục khi giá dao động quanh ngưỡng.
- **Đa thị trường**: Hỗ trợ đồng thời cổ phiếu Ấn Độ (NSE/BSE) và Mỹ (US Markets).
- **Đa kênh thông báo**: Kết hợp Email (chi tiết) và Telegram (nhanh gọn trên điện thoại).
- **Tự động hóa hoàn toàn**: Ghi lại lịch sử cảnh báo vào Google Sheets để các sếp dễ dàng review lại hiệu quả chiến lược.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản n8n**: Cloud hoặc Self-hosted.
2. **API Key Twelve Data**: Dùng để lấy dữ liệu giá cổ phiếu real-time. (Có gói free cho số lượng request nhất định).
3. **Tài khoản Google Sheets**: Để lưu danh sách cổ phiếu (Watchlist) và lịch sử cảnh báo.
4. **Tài khoản Telegram**: Tạo Bot và lấy Bot Token.
5. **Tài khoản Email (SMTP)**: Ví dụ Gmail, Outlook hoặc Mailgun để gửi cảnh báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n Editor.
2. Chọn **Import from File** hoặc **Import from URL**.
3. Dán link workflow gốc: `https://n8n.io/workflows/7701` hoặc import file JSON đã tải về.
4. Workflow sẽ hiển thị 12 nodes chính.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

Đây là phần quan trọng nhất. Các sếp cần cấu hình từng node sau:

**A. Cấu hình Google Sheets (Watchlist)**
Trước khi chạy, các sếp phải tạo một Google Sheet mới với các cột **đúng thứ tự** sau:
*   `A`: **symbol** (Mã cổ phiếu, ví dụ: `TCS`, `AAPL`, `RELIANCE.BSE`)
*   `B`: **upper_limit** (Ngưỡng giá trên, ví dụ: `4000`)
*   `C`: **lower_limit** (Ngưỡng giá dưới, ví dụ: `3600`)
*   `D`: **direction** (Loại cảnh báo: `both`, `above` hoặc `below`)
*   `E`: **cooldown_minutes** (Thời gian chờ phút, ví dụ: `15`)
*   `F`: **last_alert_price** (Để trống, hệ thống tự điền)
*   `G`: **last_alert_time** (Để trống, hệ thống tự điền)

*   **Node `Read Stock Watchlist`**: Chọn credentials Google API, điền tên Sheet và ID Sheet.
*   **Node `Update Alert History`**: Chọn cùng một Sheet để cập nhật lại cột F và G sau mỗi lần cảnh báo.

**B. Cấu hình API Giá (Twelve Data)**
*   **Node `Fetch Live Stock Price`**:
    *   Chọn credentials HTTP Request (hoặc tạo mới).
    *   Trong phần URL/Query, các sếp cần điền **API Key** của Twelve Data.
    *   Đảm bảo mã cổ phiếu trong query string khớp với định dạng của Twelve Data (ví dụ: `AAPL` cho Mỹ, `TCS.NS` cho NSE Ấn Độ - *Lưu ý: Workflow mặc định có thể cần chỉnh sửa logic parse symbol nếu dùng mã chuẩn khác*).

**C. Cấu hình Kênh Thông Báo**
*   **Node `Send Telegram Alert`**:
    *   Chọn credentials Telegram API.
    *   Điền **Chat ID** của các sếp (hoặc nhóm).
    *   Chỉnh sửa nội dung tin nhắn nếu muốn (mặc định đã khá tốt).
*   **Node `Send Email Alert`**:
    *   Chọn credentials SMTP.
    *   Điền địa chỉ email nhận cảnh báo.
    *   Chỉnh tiêu đề và nội dung email nếu cần.

**D. Logic & Trigger**
*   **Node `Market Hours Trigger`**: Mặc định chạy mỗi 2 phút. Các sếp có thể chỉnh tần suất (ví dụ: 1 phút cho day trading, 5 phút cho swing).
*   **Node `Smart Alert Logic`**: Đây là node Code chứa logic so sánh giá và cooldown. Nếu các sếp muốn thay đổi logic (ví dụ: cảnh báo khi biến động > 2% thay vì chạm ngưỡng cố định), hãy chỉnh sửa code tại đây.

#### 3. Kích hoạt ⚡️
1. Nhấn **Execute Workflow** để test với dữ liệu mẫu.
2. Kiểm tra xem có nhận được email/telegram không (có thể đặt ngưỡng giá ảo để test).
3. Nếu ổn, bật công tắc **Active** ở góc trên bên phải.

### ✍️ Mẹo & gợi ý nâng cao

1. **Tích hợp Trading Bot**: Thay vì chỉ gửi cảnh báo, các sếp có thể thêm node `HTTP Request` để gọi API của sàn giao dịch (ví dụ: Zerodha, Interactive Brokers) để tự động đặt lệnh khi nhận cảnh báo.
2. **Cảnh báo theo % thay vì giá tuyệt đối**: Sửa node `Smart Alert Logic` để tính toán phần trăm thay đổi so với giá đóng cửa hôm trước thay vì so với số cứng.
3. **Gửi báo cáo cuối ngày**: Thêm một Cron Trigger chạy lúc 15:30 (đóng cửa thị trường) để tổng hợp lại tất cả các lần cảnh báo trong ngày và gửi email báo cáo tuần hoàn.
4. **Hỗ trợ Crypto**: Workflow này hoàn toàn có thể áp dụng cho Crypto bằng cách thay đổi API source (ví dụ: CoinGecko, Binance API) và điều chỉnh logic market hours (Crypto chạy 24/7).

### 📌 Kết luận

Việc canh giá thủ công là một trong những cách tiêu tốn thời gian và gây stress nhất cho trader. Với workflow **Real-Time Stock Monitor** này, các sếp đã có một hệ thống giám sát tự động, chính xác và không bao giờ ngủ quên. Hãy dành thời gian để phân tích thị trường và ra quyết định chiến lược, để n8n lo phần "canh giá".

Chúc các sếp giao dịch thành công và lời nhuận cao! 🚀