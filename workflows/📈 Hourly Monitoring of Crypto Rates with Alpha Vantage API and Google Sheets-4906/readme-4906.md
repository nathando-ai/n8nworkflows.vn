---
title: "📈 Theo dõi giá Bitcoin và Ethereum hàng giờ với Alpha Vantage và Google Sheets"
description: "Tự động hóa theo dõi giá BTC và ETH hàng giờ, lưu vào Google Sheets và nhận thông báo Telegram - Giải pháp hoàn hảo cho nhà đầu tư và nhà phân tích thị trường"
slug: "theo-doi-gia-btc-eth-hang-gio-voi-alpha-vantage-google-sheets"
tags: [n8n, automation, no-code, cryptocurrency, finance]
keywords: [n8n workflow, tự động hóa giá crypto, Alpha Vantage, Google Sheets, Telegram]
---

# 📈 Theo dõi giá Bitcoin và Ethereum hàng giờ với Alpha Vantage và Google Sheets

[Đoạn mở đầu: Phân tích nỗi đau thực tế của nhà đầu tư và nhà phân tích thị trường khi phải theo dõi giá BTC và ETH hàng giờ. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Không cần theo dõi giá thủ công hàng giờ
- Chính xác: Dữ liệu được cập nhật tự động từ API đáng tin cậy
- Cá nhân hóa: Nhận thông báo Telegram theo định dạng cá nhân hóa
- Hoạt động liên tục: Theo dõi giá 24/7 mà không cần can thiệp
- Dữ liệu sẵn sàng: Lưu trữ lịch sử giá trong Google Sheets cho phân tích
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Alpha Vantage (API Key)
- Tài khoản Google với quyền truy cập Google Sheets
- Tài khoản Telegram và Bot Token
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/4906)
2. Click vào nút "Download" để tải file JSON
3. Trong n8n Editor, click vào "Import from File" và chọn file vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

**Node "BTC Exchange Rate" và "ETH Exchange Rate" (httpRequest):**
- Cấu hình credentials:
  1. Click vào tab "Credentials"
  2. Thêm mới credential "httpQueryAuth"
  3. Điền API Key từ Alpha Vantage vào trường "Query Parameters"
  4. Thêm các tham số:
     - `function=CURRENCY_EXCHANGE_RATE`
     - `from_currency=BTC` (cho node BTC) hoặc `from_currency=ETH` (cho node ETH)
     - `to_currency=EUR`
     - `apikey=[API_KEY_CỦA_BẠN]`

**Node "Save Rate BTC" và "Save Rate ETH" (googleSheets):**
- Cấu hình credentials:
  1. Click vào tab "Credentials"
  2. Thêm mới credential "googleSheetsOAuth2Api"
  3. Theo dõi hướng dẫn để xác thực tài khoản Google
- Cấu hình node:
  1. Chọn "Append" trong trường "Operation"
  2. Chọn file Google Sheets đích
  3. Chọn sheet đích
  4. Mapping các trường dữ liệu:
     - `From_Currency_Code`
     - `From_Currency_Name`
     - `To_Currency_Code`
     - `To_Currency_Name`
     - `Exchange_Rate`
     - `Bid_Price`
     - `Ask_Price`
     - `Last_Refreshed`
     - `Time_Zone`

**Node "Notification BTC" và "Notification ETH" (telegram):**
- Cấu hình credentials:
  1. Click vào tab "Credentials"
  2. Thêm mới credential "telegramApi"
  3. Điền Bot Token và Chat ID
- Cấu hình node:
  1. Điền nội dung thông báo (có thể sử dụng các biến động như `{{$node["BTC Exchange Rate"].json["Realtime Currency Exchange Rate"]["5. Exchange Rate"]}}`)

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu bằng cách click vào nút "Execute Workflow"
2. Kiểm tra kết quả trên Google Sheets và Telegram
3. Bật Active workflow bằng cách click vào nút "Activate" ở góc trên bên phải

### ✍️ Mẹo & gợi ý nâng cao
- Thêm các đồng tiền khác: Sao chép các node BTC/ETH và thay đổi tham số `from_currency`
- Thiết lập cảnh báo giá: Thêm node "If" để kiểm tra giá và gửi thông báo khi đạt ngưỡng
- Tích hợp với Google Data Studio: Kết nối Google Sheets với Data Studio để tạo báo cáo trực quan
- Thêm lịch sử giá: Thiết lập workflow chạy hàng ngày để lưu trữ dữ liệu lịch sử
- Kết hợp với các dịch vụ khác: Gửi dữ liệu đến Slack, Email hoặc các hệ thống CRM khác

### 📌 Kết luận
Workflow này cung cấp giải pháp hoàn chỉnh cho việc theo dõi giá Bitcoin và Ethereum hàng giờ, giúp các nhà đầu tư và nhà phân tích thị trường tiết kiệm thời gian và có được dữ liệu chính xác. Bằng cách tích hợp với Google Sheets và Telegram, workflow này không chỉ cung cấp dữ liệu mà còn giúp người dùng nhận thông báo tức thời và lưu trữ lịch sử giá cho phân tích dài hạn. Hãy áp dụng ngay để nâng cao hiệu suất làm việc của bạn!