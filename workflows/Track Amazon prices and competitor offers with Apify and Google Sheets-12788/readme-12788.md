---
title: "🚀 Theo dõi giá Amazon và các ưu đãi của đối thủ với Apify và Google Sheets"
description: "Tự động hóa theo dõi giá sản phẩm Amazon và các ưu đãi của đối thủ, đồng bộ dữ liệu trực tiếp vào Google Sheets để đưa ra quyết định định giá thông minh."
slug: "theo-doi-gia-amazon-voi-apify-google-sheets"
tags: [n8n, automation, no-code, market-research, e-commerce]
keywords: [n8n workflow, tự động hóa, theo dõi giá, Amazon, Apify, Google Sheets]
---

# 🚀 Theo dõi giá Amazon và các ưu đãi của đối thủ với Apify và Google Sheets

[Các sếp đang làm việc thủ công để theo dõi giá sản phẩm Amazon và các ưu đãi của đối thủ? Hãy để workflow này giúp các sếp tiết kiệm thời gian và đưa ra quyết định định giá thông minh hơn!]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa theo dõi giá hàng ngày mà không cần can thiệp thủ công.
- Dữ liệu chính xác: Đồng bộ dữ liệu trực tiếp từ Amazon vào Google Sheets.
- Quản lý đối thủ: Theo dõi các ưu đãi của đối thủ một cách dễ dàng.
- Tự động hóa hoàn toàn: Không cần lập trình, chỉ cần cấu hình.
- Dễ dàng mở rộng: Thêm sản phẩm và đối thủ mới chỉ với vài bước đơn giản.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với Google Sheets đã được kích hoạt API.
- Tài khoản Apify với API key (yêu cầu gói trả phí để sử dụng scraper Amazon).
- Dữ liệu sản phẩm và đối thủ đã được nhập vào Google Sheets.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:
- **Schedule Trigger**: Cấu hình lịch chạy hàng ngày.
- **Get row(s) in sheet**: Cấu hình Google Sheets OAuth2 API và chỉ định Sheet ID, phạm vi dữ liệu.
- **Loop Over Items**: Cấu hình số lượng sản phẩm xử lý trong mỗi batch.
- **Run an Actor**: Cấu hình Apify API và chọn actor phù hợp để scrape dữ liệu từ Amazon.
- **HTTP Request1**: Cấu hình endpoint để lấy kết quả từ Apify.
- **Append or update row in sheet**: Cấu hình Google Sheets OAuth2 API và chỉ định Sheet ID, phạm vi dữ liệu.
- **Code in JavaScript**: Chỉnh sửa mã JavaScript để xử lý dữ liệu đầu ra từ Apify.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node để gửi thông báo qua Slack hoặc Email khi giá sản phẩm thay đổi đáng kể.
- Lưu log hoạt động của workflow để theo dõi lịch sử thay đổi.
- Tự động gửi báo cáo định kỳ về tình hình giá và đối thủ.

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian và đưa ra quyết định định giá thông minh hơn. Hãy áp dụng ngay để tối ưu hóa chiến lược kinh doanh của các sếp!