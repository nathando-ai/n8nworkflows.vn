---
title: "🚀 Tự động trích xuất và làm giàu danh sách khách hàng tiềm năng từ bình luận LinkedIn bằng Apify và Google Sheets"
description: "Biến các bài viết LinkedIn viral thành mỏ vàng khách hàng tiềm năng. Workflow n8n tự động cào bình luận, làm giàu thông tin profile và đồng bộ vào Google Sheets."
slug: "trich-xuat-linkedin-comments-thanh-leads-apify-google-sheets"
tags: [n8n, automation, no-code, linkedin, apify, lead-generation, google-sheets]
keywords: [n8n workflow, cào bình luận linkedin, apify linkedin scraper, làm giàu dữ liệu khách hàng, google sheets automation]
---

# 🚀 Tự động trích xuất và làm giàu danh sách khách hàng tiềm năng từ bình luận LinkedIn

Các sếp có bao giờ tự hỏi làm sao để tận dụng lượng tương tác khủng từ các bài viết LinkedIn (cả bài của mình lẫn đối thủ) mà không phải copy-paste thủ công từng bình luận? Việc ngồi lọc danh sách người tương tác, tra cứu thông tin từng người tốn hàng giờ đồng hồ và cực kỳ nhàm chán.

Giải pháp đây rồi! Workflow n8n này sẽ tự động hóa 100% quy trình: cào toàn bộ bình luận từ một bài viết LinkedIn bất kỳ (không cần đăng nhập tài khoản cá nhân nhờ công cụ mạnh mẽ từ **Apify**), làm giàu (enrich) thông tin profile chi tiết, lọc ra danh sách lead duy nhất và đẩy thẳng lên **Google Sheets** hoặc xuất file CSV gọn gàng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- 🔍 **Không cần Login**: Cào dữ liệu LinkedIn an toàn tuyệt đối mà không sợ bị khóa tài khoản (banned).
- 💰 **Tiết kiệm chi phí**: Tận dụng tầng miễn phí (Free tier) của Apify cho 1,000 bình luận đầu tiên.
- 📊 **Làm giàu dữ liệu tự động**: Tự động kết hợp thông tin bình luận với dữ liệu profile chi tiết (Chức vụ, công ty, ngành nghề, v.v.).
- 📈 **Linh hoạt đầu ra**: Hỗ trợ đồng thời xuất dữ liệu trực tiếp lên Google Sheets hoặc tải về file CSV.
:::

### yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Apify**: Lấy `APIFY_TOKEN` tại [Apify Console](https://apify.com/account#/integrations). (Tích hợp các scraper: *LinkedIn Post Comments Scraper* và *LinkedIn Profile Batch Scraper*).
- **Tài khoản Google Sheets**: Cấu hình OAuth2 API để n8n có thể tự động tạo và ghi dữ liệu vào bảng tính.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này và import trực tiếp vào n8n Editor của các sếp, hoặc sử dụng tính năng copy/paste JSON.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node `Set APIFY Token`**: Nhập Apify API Token của các sếp vào phần cấu hình biến.
- **Node `Create Google Sheet` & `Add Leads`**: Chọn đúng credential Google Sheets OAuth2 để hệ thống có quyền truy cập tài khoản Google Drive/Sheets.
- **Lựa chọn chế độ chạy (Form-based vs Manual)**:
  - *Chế độ Form (Mặc định)*: Giữ nguyên trigger `On form submission` để tạo giao diện nhập URL bài viết LinkedIn dễ dàng.
  - *Chế độ Manual/CSV*: Nếu muốn chạy thủ công và lấy file CSV, hãy disable các node Form, enable node `Trigger manually` và cấu hình URL bài viết tại node `Set manual fields`.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (Test run) với một bài viết LinkedIn công khai có ít bình luận trước để kiểm tra luồng dữ liệu.
- Bật công tắc **Active** để đưa workflow vào trạng thái vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp CRM/Email Outreach**: Nối tiếp bước ghi vào Google Sheets bằng các node gửi dữ liệu sang Instantly, Clay hoặc HubSpot để tự động hóa chuỗi email chăm sóc (Cold Email).
- **Nhận thông báo qua Telegram/Slack**: Thêm node thông báo mỗi khi hệ thống quét xong và tạo thành công một danh sách lead mới.
- **Lọc data trùng lặp**: Tận dụng các node code JavaScript có sẵn trong workflow để giữ lại unique leads, tránh spam khách hàng.

### 📌 Kết luận
Biến những lượt tương tác mạng xã hội thành khách hàng tiềm năng chưa bao giờ dễ dàng đến thế. Hãy cài đặt ngay workflow này để tối ưu hóa phễu Sales Automation cho doanh nghiệp của các sếp!