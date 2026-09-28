---
title: "🚀 Theo dõi giá Crypto & tỷ giá ngoại tệ tự động với CoinGecko & ExchangeRate-API lên Notion"
description: "Tự động hóa việc theo dõi giá Bitcoin, Ethereum và tỷ giá ngoại tệ hàng giờ lên Notion, tiết kiệm thời gian và nâng cao hiệu quả làm việc"
slug: "theo-doi-gia-crypto-ty-gia-ngoai-te-len-notion"
tags: [n8n, automation, no-code, notion, api]
keywords: [n8n workflow, tự động hóa, theo dõi giá crypto, tỷ giá ngoại tệ, Notion]
---

# 🚀 Theo dõi giá Crypto & tỷ giá ngoại tệ tự động với CoinGecko & ExchangeRate-API lên Notion

[Các sếp đang làm việc với dữ liệu tài chính và thị trường crypto chắc hẳn đã từng gặp tình trạng này: Mỗi ngày phải mở nhiều tab trình duyệt để kiểm tra giá Bitcoin, Ethereum và tỷ giá ngoại tệ, sau đó phải ghi chép lại vào Notion để theo dõi. Việc này không chỉ tốn thời gian mà còn dễ gây lỗi khi phải nhập tay. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình này chỉ trong 15 phút!]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần mở nhiều tab trình duyệt hàng giờ
- **Chính xác 100%**: Dữ liệu được lấy trực tiếp từ API đáng tin cậy
- **Theo dõi dễ dàng**: Tất cả dữ liệu được lưu trữ trong Notion với định dạng dễ đọc
- **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công sau khi cài đặt
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Notion đã tạo Database với các trường:
  - Title (text)
  - BTC (number)
  - BTC_24h (number)
  - ETH (number)
  - ETH_24h (number)
  - USD_EUR (number)
  - USD_NGN (number)
- API Key từ [ExchangeRate-API](https://www.exchangerate-api.com/) (miễn phí)
- Tài khoản CoinGecko (không cần API key cho dữ liệu công khai)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/8387](https://n8n.io/workflows/8387)
2. Chọn "Import" và sao chép JSON workflow
3. Trong n8n Editor, chọn "Import from Clipboard" và dán JSON

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node "Get Fiat Exchange Rates"**:
  - Thêm API Key từ ExchangeRate-API vào credentials
  - Đảm bảo chọn đúng cặp tiền tệ (USD→EUR và USD→NGN)

- **Node "Get Crypto Prices"**:
  - Không cần cấu hình thêm, dữ liệu được lấy từ API công khai của CoinGecko

- **Node "Build Notion Page"**:
  - Chỉnh sửa code để phù hợp với cấu trúc Database của các sếp
  - Đảm bảo các trường dữ liệu khớp với tên trường trong Notion

- **Node "Create in Notion"**:
  - Thêm Database ID từ Notion vào credentials
  - Kiểm tra kết nối trước khi kích hoạt workflow

#### 3. Kích hoạt ⚡️
1. Chạy test với dữ liệu mẫu để kiểm tra kết quả
2. Sau khi xác nhận dữ liệu đúng, bật Active workflow
3. Đặt lịch chạy hàng giờ (hoặc theo nhu cầu) trong node "Every 60 Minutes"

### ✍️ Mẹo & gợi ý nâng cao
- Thêm cảnh báo khi giá vượt ngưỡng nhất định bằng cách kết nối với Slack/Telegram
- Lưu log các thay đổi giá lớn vào Google Sheets để phân tích dài hạn
- Tự động gửi báo cáo hàng ngày qua email với dữ liệu tổng hợp
- Kết nối với các API khác để theo dõi thêm các loại tiền điện tử khác

### 📌 Kết luận
Với workflow này, các sếp có thể tự động hóa hoàn toàn việc theo dõi giá crypto và tỷ giá ngoại tệ hàng giờ, giúp tiết kiệm thời gian quý giá và giảm thiểu lỗi nhập liệu. Hãy thử ngay và trải nghiệm sự khác biệt trong cách làm việc của mình!