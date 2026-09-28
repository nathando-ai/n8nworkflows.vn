---
title: "💳 Tự động hóa đơn hàng Stripe: Lấy thông tin khách hàng & sản phẩm mua hàng"
description: "Hướng dẫn tự động hóa quy trình lấy thông tin khách hàng và sản phẩm mua hàng từ Stripe bằng n8n, tiết kiệm thời gian và nâng cao trải nghiệm khách hàng."
slug: "tu-dong-hoa-don-hang-stripe-lay-thong-tin-khach-hang-san-pham"
tags: [n8n, automation, no-code, stripe, payment]
keywords: [n8n workflow, tự động hóa, stripe payment, lấy thông tin khách hàng, sản phẩm mua hàng]
---

# 💳 Tự động hóa đơn hàng Stripe: Lấy thông tin khách hàng & sản phẩm mua hàng

[Các sếp bán hàng và quản lý IT đang gặp khó khăn khi phải theo dõi thủ công các đơn hàng từ Stripe. Với workflow này, các sếp có thể tự động lấy thông tin khách hàng và sản phẩm mua hàng ngay khi có giao dịch thành công.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động lấy thông tin khách hàng và sản phẩm mua hàng ngay khi có giao dịch thành công.
- Tiết kiệm thời gian và công sức cho đội ngũ bán hàng và CSKH.
- Nâng cao trải nghiệm khách hàng với thông tin chi tiết và nhanh chóng.
- Hoạt động liên tục 24/7 mà không cần can thiệp thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Stripe đã kích hoạt và có quyền truy cập API.
- API Key của Stripe để cấu hình trong n8n.
- Quyền truy cập vào n8n Editor để import và cấu hình workflow.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor.
2. Nhấn vào nút "Import from URL" và dán link sau: [https://n8n.io/workflows/3391](https://n8n.io/workflows/3391).
3. Hoặc tải file JSON từ link trên và import vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Stripe Trigger on Payment Event**:
  - Chọn credentials là `stripeApi`.
  - Điền các tham số cần thiết như `Event Type` (ví dụ: `checkout.session.completed`).

- **Extract Session Information**:
  - Chọn credentials là `stripeApi` và `httpHeaderAuth`.
  - Điền tham số `URL` với giá trị `https://api.stripe.com/v1/checkout/sessions/{{$node["Stripe Trigger on Payment Event"].json["data"]["object"]["id"]}}`.

- **Filter Information**:
  - Cấu hình các trường dữ liệu cần lấy từ kết quả trả về của node trước đó.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng.
- Bật Active workflow để bắt đầu tự động hóa quy trình.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack hoặc Telegram để thông báo ngay khi có đơn hàng mới.
- Lưu log các đơn hàng vào Google Sheets hoặc cơ sở dữ liệu để theo dõi.
- Gửi báo cáo định kỳ về các đơn hàng mới đến email của quản lý.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa quy trình lấy thông tin khách hàng và sản phẩm mua hàng từ Stripe, tiết kiệm thời gian và nâng cao hiệu quả kinh doanh. Hãy áp dụng ngay để tối ưu hóa quy trình bán hàng của các sếp!