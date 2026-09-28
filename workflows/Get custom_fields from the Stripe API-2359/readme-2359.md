---
title: "🚀 Tự động lấy và lọc trường tùy chỉnh (Custom Fields) từ Stripe API trong n8n"
description: "Hướng dẫn chi tiết cách kết nối Stripe API qua n8n để trích xuất, phân tách và lọc các custom fields từ Checkout Sessions một cách tự động."
slug: "lay-va-loc-custom-fields-tu-stripe-api-trong-n8n"
tags: [n8n, automation, stripe, api, finance, no-code]
keywords: [n8n workflow, stripe api, custom fields stripe, checkout sessions, tu dong hoa stripe]
---

# 🚀 Tự động lấy và lọc trường tùy chỉnh (Custom Fields) từ Stripe API trong n8n

Việc trích xuất dữ liệu tùy chỉnh (`custom_fields`) từ các phiên thanh toán Checkout Sessions của Stripe để phục vụ cho việc chăm sóc khách hàng, đồng bộ CRM hoặc phân tích dữ liệu thường gặp nhiều khó khăn nếu làm thủ công. Các sếp thường phải mất nhiều thời gian xuất file báo cáo hoặc viết code riêng để gọi API.

Workflow n8n này sẽ giúp các sếp tự động hóa 100% quy trình gọi Stripe API, lấy dữ liệu trong 7 ngày gần nhất, phân tách và lọc các trường dữ liệu tùy chỉnh theo ý muốn mà không cần viết một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Lấy danh sách Checkout Sessions từ Stripe mà không cần thao tác thủ công.
- **Xử lý dữ liệu thông minh**: Tự động phân tách (`splitOut`) mảng dữ liệu phức tạp để dễ dàng trực quan hóa hoặc chuyển đổi.
- **Lọc chính xác**: Dễ dàng lọc ra các khách hàng có điền các trường tùy chỉnh cụ thể (như biệt danh, chức vụ, mã nhân viên...).
- **Tiết kiệm thời gian**: Thay vì tốn hàng giờ tra cứu trên Dashboard Stripe, dữ liệu sẽ sẵn sàng trong vài giây.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một tài khoản n8n (Cloud hoặc Self-hosted).
- Tài khoản Stripe và **Stripe API Key** (Secret Key) để cấu hình xác thực cho HTTP Request Node.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn JSON của workflow này và dán trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 4 nodes chính, các sếp cần chú ý cấu hình các điểm sau:

- **Node `Stripe | Get latest checkout sessions1` (HTTP Request Node)**:
  - Cần thiết lập **Credentials** để kết nối với Stripe API (sử dụng Header Auth với Bearer Token là Stripe Secret Key của các sếp).
  - Node này mặc định lấy dữ liệu checkout sessions trong 7 ngày qua. Các sếp có thể điều chỉnh tham số `created` trong URL nếu muốn lấy khoảng thời gian khác (Ví dụ: lấy dữ liệu từ một timestamp cụ thể). Chức năng phân trang (Pagination) đã được cấu hình sẵn ở dưới, các sếp nhớ giữ nguyên để lấy toàn bộ dữ liệu.
- **Node `split all data` & `split custom_fields` (SplitOut Nodes)**:
  - Các node này có nhiệm vụ bóc tách các mảng dữ liệu JSON phức tạp thành các dòng riêng biệt, giúp việc đọc hiểu và map dữ liệu ở các bước sau trở nên dễ dàng hơn.
- **Node `Filter by custom_field` (Filter Node)**:
  - Tại đây, các sếp thiết lập điều kiện lọc. Ví dụ: chỉ giữ lại những khách hàng có điền trường `nickname` hoặc `job title` theo ý đồ kinh doanh của mình.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** để chạy thử nghiệm (Test run) với dữ liệu thực tế từ Stripe.
- Kiểm tra kết quả ở từng node để đảm bảo dữ liệu trả về chính xác.
- Bật công tắc **Active** góc trên bên phải để workflow sẵn sàng chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối CRM / Google Sheets**: Sau bước lọc, các sếp có thể nối thêm node Google Sheets hoặc HubSpot để tự động lưu thông tin custom fields vào hệ thống quản lý khách hàng.
- **Gửi thông báo qua Telegram/Slack**: Thiết lập cảnh báo mỗi khi có một khách hàng mới hoàn tất checkout kèm theo các thông tin tùy chỉnh đặc biệt.
- **Chạy định kỳ (Cron)**: Thay vì chạy thủ công, hãy gắn một Schedule Trigger ở đầu workflow để tự động quét dữ liệu Stripe mỗi ngày một lần.

### 📌 Kết luận
Workflow `Get custom:fields from the Stripe API` là một giải pháp cực kỳ gọn nhẹ nhưng mạnh mẽ giúp các sếp khai thác tối đa dữ liệu tùy chỉnh từ cổng thanh toán Stripe. Hãy áp dụng ngay vào hệ thống của mình để tối ưu hóa quy trình vận hành kinh doanh!