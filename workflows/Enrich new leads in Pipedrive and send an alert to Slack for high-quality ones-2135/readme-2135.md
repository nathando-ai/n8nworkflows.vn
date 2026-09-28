---
title: "🚀 Tự động làm giàu dữ liệu Lead từ Pipedrive với Clearbit và Cảnh báo Slack cực đỉnh"
description: "Hướng dẫn xây dựng workflow n8n tự động lấy lead mới từ Pipedrive, bổ sung thông tin doanh nghiệp qua Clearbit, lọc lead chất lượng cao và bắn thông báo tức thì lên Slack."
slug: "tu-dong-lam-giac-lead-pipedrive-clearbit-slack"
tags: [n8n, automation, pipedrive, clearbit, slack, crm, sales]
keywords: [n8n workflow, tự động hóa pipedrive, clearbit enrichment, slack notification, crm automation]
---

# 🚀 Tự động làm giàu dữ liệu Lead từ Pipedrive với Clearbit và Cảnh báo Slack

Các sếp làm sales chắc hẳn đều hiểu cảm giác tốn hàng giờ mỗi ngày chỉ để tra cứu thông tin công ty của từng Lead mới trên Google, LinkedIn hay các trang vàng để đánh giá xem họ có "tiềm năng" hay không. Việc làm thủ công này vừa nhàm chán, vừa chậm trễ, khiến đội ngũ sales bỏ lỡ thời điểm vàng để chốt đơn.

Đừng lo, bài toán đó sẽ được giải quyết triệt để với workflow n8n cực kỳ thông minh này. Được thiết kế bởi **Niklas Hatje** (Product Manager tại n8n), hệ thống sẽ tự động hóa 100% quy trình: Quét lead mới từ **Pipedrive** ➔ Làm giàu thông tin doanh nghiệp qua **Clearbit** ➔ Lọc theo tiêu chí chất lượng ➔ Gửi cảnh báo ngay lập tức vào **Slack** cho đội ngũ sales và đánh dấu "Đã làm giàu" trên Pipedrive. Các sếp chỉ việc ngồi chờ lead chất lượng tự động "gõ cửa"!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 không bị gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian nghiên cứu:** Đội ngũ Sales không cần phải tra cứu thủ công thông tin doanh nghiệp của lead nữa.
- **Tập trung vào khách hàng tiềm năng:** Tự động lọc ra các lead đạt chuẩn (theo doanh thu, số lượng nhân viên, quy mô...) để ưu tiên chăm sóc trước.
- **Phản hồi tức thì:** Thông báo chi tiết về lead chất lượng cao đổ thẳng vào kênh Slack của team sales ngay sau mỗi 5 phút.
- **Đồng bộ dữ liệu minh bạch:** Tự động cập nhật trạng thái "Enriched" trên Pipedrive để tránh trùng lặp công sức xử lý.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow này "lên đồ" mượt mà, các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- **Pipedrive Account:** Tài khoản CRM có quyền tạo custom fields và truy cập API.
- **Clearbit Account:** Tài khoản và API Key dùng để truy xuất dữ liệu doanh nghiệp (Company Enrichment).
- **Slack Workspace:** Kênh Slack để nhận thông báo (cần quyền cấu hình Bot/Webhook).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã JSON của workflow này, dán trực tiếp vào n8n Editor (hoặc import file JSON) để bắt đầu.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 16 nodes hoạt động nhịp nhàng, các sếp cần chú ý cấu hình kỹ các điểm sau:

- **Thiết lập Custom Fields trên Pipedrive (Rất quan trọng):**
  1. Vào Pipedrive -> *Company Settings* -> *Data fields* -> *Organization*, thêm một trường tùy chỉnh (Custom field) dạng chuỗi (Text) với tên là **`Domain`**.
  2. Vào *Company Settings* -> *Data fields* -> *Leads*, thêm một trường tùy chỉnh dạng ngày tháng (Date) với tên là **`Enriched at`**.
- **Cấu hình Credentials:** Kết nối tài khoản `Pipedrive`, `Clearbit` và `Slack` vào các node tương ứng trong workflow.
- **Node `Setup` (Set):** Điền các tham số cấu hình hệ thống vào đây. Để lấy ID của các trường custom domain và enriched at vừa tạo:
  - Chạy thử node `Get all organization keys` và `Show only custom organization fields` để lấy ID trường Domain.
  - Chạy thử node `Get all lead keys` và `Show only custom lead fields` để lấy ID trường Enriched at. Sau đó dán các ID này vào node `Setup`.
- **Node `Keep leads that match the criteria` (Filter):** Tùy chỉnh lại điều kiện lọc lead theo mong muốn của doanh nghiệp (ví dụ: theo doanh thu của công ty, số lượng nhân viên, ngành nghề,... lấy từ dữ liệu Clearbit trả về).

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** chạy thử thủ công lần đầu tiên với dữ liệu mẫu để kiểm tra kết nối giữa Pipedrive ➔ Clearbit ➔ Slack.
- Kiểm tra kết quả trên Slack và Pipedrive xem dữ liệu đã đồng bộ chuẩn chưa.
- Nếu mọi thứ mượt mà, gạt công tắc sang **Active** để workflow tự động chạy định kỳ mỗi 5 phút (được kích hoạt bởi node `Trigger every 5 minutes`).

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Ngoài Slack, các sếp có thể nối thêm node Telegram hoặc Email để gửi thông báo khẩn cấp cho các sếp quản lý khi có một "Cá mập" (Lead quy mô lớn) xuất hiện.
- **Lưu lịch sử vào Google Sheets:** Thêm một node Google Sheets để lưu lại toàn bộ lịch sử các lead đã được enrich nhằm phục vụ cho việc đo lường hiệu suất marketing sau này.
- **Tích hợp AI đánh giá Lead (Lead Scoring):** Kết hợp thêm OpenAI/Claude node để phân tích mô tả công ty từ Clearbit và chấm điểm tiềm năng (từ 1-10) trước khi đẩy lên Slack.

### 📌 Kết luận
Tự động hóa quy trình quản lý lead chính là chìa khóa giúp đội ngũ sales bứt phá doanh thu mà không bị ngập chìm trong các tác vụ thủ công. Hãy áp dụng ngay workflow này vào hệ thống của doanh nghiệp các sếp để tối ưu hóa hiệu suất sales ngay hôm nay!