---
title: "🚀 Tự động cảnh báo giá giảm giày sneaker với Bright Data & n8n"
description: "Hướng dẫn chi tiết cách tự động theo dõi giá giày sneaker trên các trang resale và nhận thông báo email khi giá giảm dưới ngưỡng mong muốn"
slug: "tu-dong-canh-bao-gia-giam-giay-sneaker"
tags: [n8n, automation, no-code, sneaker, bright-data]
keywords: [n8n workflow, tự động hóa, theo dõi giá sneaker, cảnh báo giá giảm]
---

# 🚀 Tự động cảnh báo giá giảm giày sneaker với Bright Data & n8n

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Theo dõi giá hàng ngày mà không cần can thiệp thủ công
- Chính xác: Lấy dữ liệu trực tiếp từ trang web chính thức
- Cá nhân hóa: Thiết lập ngưỡng giá phù hợp với túi tiền của bạn
- Hoạt động liên tục: Nhận cảnh báo ngay khi giá giảm
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Gmail để nhận thông báo
- API Key từ Bright Data (đăng ký tại [đây](https://get.brightdata.com/1tndi4600b25))
- URL của trang sản phẩm sneaker bạn muốn theo dõi
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/5223](https://n8n.io/workflows/5223)
2. Nhấn nút "Import" ở góc trên bên phải
3. Chọn "Import from URL" và dán link trên vào ô nhập liệu
4. Nhấn "Import" để hoàn tất

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Schedule Trigger - Run Price Monitor Everyday"**:
   - Thiết lập thời gian chạy hàng ngày (ví dụ: 9:00 AM)
   - Có thể thay đổi tần suất theo nhu cầu

2. **Node "HTTP Request - Bright Data Scraper"**:
   - Thay đổi URL trong phần "URL" để theo dõi sản phẩm khác
   - Đảm bảo URL là của trang sản phẩm chính thức (StockX, GOAT, etc.)
   - Thêm API Key của Bright Data vào phần "Authentication"

3. **Node "IF - Check Price < Threshold"**:
   - Thay đổi giá trị trong điều kiện để phù hợp với ngưỡng giá mong muốn
   - Ví dụ: `{{ $node["Extract Title & Price"].json["price"] }} < 250` để cảnh báo khi giá dưới $250

4. **Node "Gmail - Send Price Drop Email Alert"**:
   - Thiết lập tài khoản Gmail để gửi và nhận email
   - Có thể tùy chỉnh nội dung email trong phần "Message"

#### 3. Kích hoạt ⚡️
1. Nhấn nút "Execute Node" để kiểm tra workflow với dữ liệu mẫu
2. Sau khi kiểm tra thành công, nhấn nút "Activate" để kích hoạt workflow
3. Workflow sẽ tự động chạy theo lịch trình đã thiết lập

### ✍️ Mẹo & gợi ý nâng cao
- Theo dõi nhiều sản phẩm: Sao chép node "HTTP Request" và thay đổi URL cho từng sản phẩm
- Kết hợp với Slack: Thêm node Slack để nhận thông báo trên kênh Slack
- Lưu log giá: Thêm node Google Sheets để lưu lịch sử giá
- Thiết lập cảnh báo giá tăng: Thêm một nhánh IF để cảnh báo khi giá tăng đột biến

### 📌 Kết luận
Workflow này giúp các sếp sneaker head tiết kiệm thời gian và tiền bạc bằng cách tự động theo dõi giá và nhận cảnh báo khi có deal hấp dẫn. Với việc tích hợp Bright Data, workflow có thể vượt qua các cơ chế chống bot của các trang resale phổ biến. Hãy thử ngay và bắt đầu săn deal sneaker như một chuyên gia!