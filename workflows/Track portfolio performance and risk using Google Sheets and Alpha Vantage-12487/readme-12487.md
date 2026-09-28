---
title: "📈 Tự động theo dõi hiệu suất và rủi ro danh mục đầu tư bằng Google Sheets và Alpha Vantage"
description: "Hướng dẫn chi tiết cách tự động hóa việc theo dõi hiệu suất danh mục đầu tư, tính toán chỉ số rủi ro và phân loại cổ phiếu bằng n8n, Google Sheets và Alpha Vantage"
slug: "tu-dong-theo-doi-hieu-suat-danh-muc-dau-tu"
tags: [n8n, automation, no-code, crypto, trading, google-sheets, alpha-vantage]
keywords: [n8n workflow, tự động hóa, theo dõi danh mục đầu tư, phân tích rủi ro, Alpha Vantage, Google Sheets]
---

# 📈 Tự động theo dõi hiệu suất và rủi ro danh mục đầu tư bằng Google Sheets và Alpha Vantage

[Các sếp] có bao giờ phải tốn hàng giờ mỗi ngày để theo dõi hiệu suất danh mục đầu tư, tính toán các chỉ số rủi ro và phân loại cổ phiếu không? Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình này chỉ trong vài bước đơn giản.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động cập nhật dữ liệu hàng ngày mà không cần can thiệp thủ công
- **Chính xác cao**: Tính toán các chỉ số tài chính theo tiêu chuẩn tài chính
- **Phân loại tự động**: Phân loại cổ phiếu thành Healthy, Watch hoặc Risk
- **Hoạt động liên tục**: Theo dõi hiệu suất danh mục 24/7 mà không bị gián đoạn
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với Google Sheets API đã được kích hoạt
- API Key từ Alpha Vantage (miễn phí)
- Tài khoản Gmail để nhận thông báo lỗi
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/12487](https://n8n.io/workflows/12487)
2. Click vào nút "Download" để tải file JSON
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Read portfolio holdings"**:
   - Chọn credentials "googleSheetsOAuth2Api"
   - Điền thông tin Sheet ID và tên sheet chứa danh mục đầu tư
   - Đảm bảo sheet có các cột: Symbol, Buy Price, Quantity, Buy Date

2. **Node "Fetch daily stock prices"**:
   - Thay thế API Key trong URL bằng API Key của các sếp từ Alpha Vantage
   - URL mẫu: `https://www.alphavantage.co/query?function=TIME_SERIES_DAILY&symbol={{$node["Read portfolio holdings"].json["Symbol"]}}&apikey=YOUR_API_KEY`

3. **Node "Update portfolio performance"**:
   - Chọn credentials "googleSheetsOAuth2Api"
   - Điền thông tin Sheet ID và tên sheet để lưu kết quả
   - Đảm bảo sheet có các cột: Symbol, Invested Value, Current Value, PnL, Return %, CAGR, Max Drawdown, Status

4. **Node "Send error notification email"**:
   - Chọn credentials "gmailOAuth2"
   - Điền địa chỉ email nhận thông báo lỗi

#### 3. Kích hoạt ⚡️
1. Click vào nút "Test Workflow" để kiểm tra dữ liệu mẫu
2. Sau khi kiểm tra thành công, click vào nút "Activate" để kích hoạt workflow
3. Workflow sẽ chạy tự động theo lịch trình đã cài đặt

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack**: Thêm node Slack để nhận thông báo khi danh mục có cổ phiếu ở trạng thái Risk
- **Lưu log**: Thêm node Google Sheets để lưu log các lần chạy workflow
- **Gửi báo cáo định kỳ**: Thêm node Gmail để gửi báo cáo hiệu suất danh mục hàng tuần
- **Kết hợp với Telegram**: Thêm node Telegram để nhận thông báo khi giá cổ phiếu có biến động lớn

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quá trình theo dõi hiệu suất danh mục đầu tư, tính toán các chỉ số rủi ro và phân loại cổ phiếu. Với việc tự động hóa toàn bộ quá trình này, các sếp có thể tập trung vào việc ra quyết định đầu tư thay vì mất thời gian cho công việc lặp đi lặp lại. Hãy áp dụng ngay workflow này để nâng cao hiệu quả quản lý danh mục đầu tư của các sếp!