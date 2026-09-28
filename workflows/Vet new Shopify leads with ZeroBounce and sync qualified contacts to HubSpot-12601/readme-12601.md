---
title: "🚀 Tự động hóa Shopify: Xác thực khách hàng bằng ZeroBounce và đồng bộ với HubSpot"
description: "Hướng dẫn tự động hóa quy trình xác thực email khách hàng từ Shopify bằng ZeroBounce và đồng bộ thông tin hợp lệ vào HubSpot, giúp tiết kiệm thời gian và tăng tỷ lệ chuyển đổi."
slug: "tu-dong-hoa-shopify-xac-thuc-khach-hang-zero-bounce-hubspot"
tags: [n8n, automation, no-code, shopify, hubspot, zerobounce, lead-generation, ai-scoring]
keywords: [n8n workflow, tự động hóa shopify, xác thực email, hubspot, zerobounce, lead generation]
---

# 🚀 Tự động hóa Shopify: Xác thực khách hàng bằng ZeroBounce và đồng bộ với HubSpot

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **✨ Zero-Waste Sync:** Chỉ những lead "Valid" hoặc "High-Scoring" mới được đồng bộ vào CRM của bạn.
- **🛡️ Credit Safety:** Kiểm tra tín dụng nội bộ để đảm bảo bạn không bao giờ gọi API mà không có tín dụng.
- **📊 Detailed Suppressions:** Mỗi lead bị từ chối đều được phân loại theo lý do (ví dụ: Email Missing, Invalid, Low Score, hoặc Insufficient credits).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Shopify:** Kết nối qua OAuth2 để theo dõi sự kiện "Customer Created" (Topic: `customers/create`).
- **ZeroBounce:** Kết nối qua API Key. *[Tạo một tại đây](https://www.zerobounce.net/members/API)*.
- **HubSpot:** Kết nối qua OAuth2 để tạo/cập nhật liên hệ cho lead chất lượng cao.
- **Google Sheets:** Kết nối qua OAuth2 để thêm/cập nhật hàng trong bảng tính Google Sheets. Hoặc thay thế các node này bằng bất kỳ node lưu trữ dữ liệu nào khác, ví dụ: **n8n Data Table** hoặc **Microsoft Excel**. Các bảng/tệp có thể được tạo với các cột sau:
    - *Accepted* columns:
`ID,Email,First Name,Last Name,Accepted At,Accepted Reason,ZB Status,ZB Sub Status,ZB Free Email,ZB Did You Mean,ZB Account,ZB Domain,ZB Domain Age Days,ZB SMTP Provider,ZB MX Found,ZB MX Record,ZB Score`
    - *Rejected* columns
`ID,Email,First Name,Last Name,Rejected At,Rejected Reason,ZB Status,ZB Sub Status,ZB Free Email,ZB Did You Mean,ZB Account,ZB Domain,ZB Domain Age Days,ZB SMTP Provider,ZB MX Found,ZB MX Record,ZB Score`
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:
- **Shopify customer created**: Cấu hình credentials Shopify OAuth2 và chọn topic `customers/create`.
- **Validate email**: Cấu hình credentials ZeroBounce API.
- **Score email**: Cấu hình credentials ZeroBounce API.
- **Create Hubspot contact**: Cấu hình credentials HubSpot OAuth2.
- **Add to Accepted/Rejected**: Cấu hình credentials Google Sheets OAuth2 và điền tên bảng tính, tên sheet, và các cột tương ứng.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để thông báo khi có lead mới được đồng bộ.
- Lưu log các hoạt động vào Google Sheets hoặc cơ sở dữ liệu để theo dõi hiệu suất.
- Gửi báo cáo định kỳ về số lượng lead được xác thực và đồng bộ.

### 📌 Kết luận
Workflow này giúp tự động hóa quy trình xác thực email khách hàng từ Shopify, giảm thiểu thời gian và công sức thủ công, đồng thời tăng tỷ lệ chuyển đổi bằng cách chỉ đồng bộ những lead chất lượng cao vào HubSpot. Hãy áp dụng ngay để tối ưu hóa quy trình làm việc của bạn!