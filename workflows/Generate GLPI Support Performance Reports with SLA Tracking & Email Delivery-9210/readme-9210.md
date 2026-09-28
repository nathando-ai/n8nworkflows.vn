---
title: "🚀 Tự Động Tạo Báo Cáo Hiệu Suất Hỗ Trợ GLPI & Theo Dõi SLA Qua Email"
description: "Hướng dẫn xây dựng workflow n8n tự động kết nối GLPI, tính toán chỉ số hiệu suất, theo dõi SLA chuẩn xác và gửi báo cáo định kỳ qua Gmail."
slug: "tu-dong-tao-bao-cao-hieu-suat-glpi-sla-n8n"
tags: [n8n, automation, no-code, glpi, it-helpdesk, report]
keywords: [n8n workflow, GLPI automation, tự động hóa GLPI, theo dõi SLA, báo cáo IT helpdesk, n8n gmail]
---

# 🚀 Tự Động Tạo Báo Cáo Hiệu Suất Hỗ Trợ GLPI & Theo Dõi SLA

Việc tổng hợp dữ liệu thủ công từ hệ thống IT Helpdesk (GLPI) để làm báo cáo hàng tháng thường ngốn rất nhiều thời gian của quản lý. Đặc biệt, việc tính toán thời gian phản hồi, tuân thủ SLA (Service Level Agreement) theo giờ hành chính, loại trừ ngày nghỉ cuối tuần và giờ nghỉ trưa lại cực kỳ dễ xảy ra sai sót. 

Workflow n8n này sẽ giải quyết triệt để vấn đề đó bằng cách tự động hóa 100% quy trình: lấy dữ liệu từ GLPI, tính toán các chỉ số thông minh, tổng hợp theo từng kỹ thuật viên và gửi báo cáo chuyên nghiệp qua Email định kỳ hàng tháng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Chạy định kỳ hàng tháng mà không cần sự can thiệp thủ công.
- **Tính toán SLA chuẩn xác:** Hệ thống tự động tính giờ làm việc thực tế (bỏ qua cuối tuần, giờ nghỉ trưa) để đo lường độ chính xác của SLA.
- **Báo cáo đa chiều:** Cung cấp cả Báo cáo Tổng quan (General Report) và Báo cáo chi tiết theo từng Kỹ thuật viên (Report by Technician).
- **Giao diện trực quan:** Báo cáo được định dạng HTML đẹp mắt và gửi thẳng đến hòm thư người quản lý qua Gmail.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Hệ thống GLPI** đang hoạt động (có bật API).
- **Tài khoản Gmail** để cấu hình node gửi email (hoặc OAuth2 credentials).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trong n8n, sau đó copy toàn bộ mã JSON của workflow (từ nguồn cấp) và dán trực tiếp vào giao diện làm việc của n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống kết nối mượt mà với GLPI và Gmail của các sếp, hãy chú ý cấu hình kỹ các node sau:

- **Node `Variables` (Set):**
  Cập nhật các thông số kết nối đến server GLPI của các sếp:
  - `GLPI server URL`: Đường dẫn tới server (ví dụ: `https://server_glpi.com/`)
  - `GLPI API App-Token`: App-Token được cấp từ GLPI.
  - `GLPI entity name`: Tên entity cần lấy dữ liệu.
  - Thiết lập giờ làm việc (`WORK_START`, `LUNCH_START`, `LUNCH_END`, `WORK_END`) và giới hạn SLA tính bằng giờ (`SLA_LIMIT_HOURS`, mặc định 24h).

- **Node `Get session token` & `Get tickets` (HTTP Request):**
  - Cấu hình Credentials: Tạo một `Generic Credential Type` dạng **Basic Auth**.
  - `Username`: Tên đăng nhập API GLPI của các sếp.
  - `Password`: Mật khẩu API GLPI.

- **Node `Schedule Trigger`:**
  - Mặc định workflow được cấu hình chạy vào ngày mùng 6 hàng tháng. Lý do: Tránh trường hợp chốt sổ vào ngày cuối tháng khiến các ticket phát sinh sát ngày chưa được tính toán chính xác SLA.

- **Node `Send a message` (Gmail):**
  - Kết nối tài khoản Gmail cá nhân hoặc doanh nghiệp của các sếp thông qua OAuth2 để hệ thống có quyền gửi email báo cáo tự động.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (Test step-by-step hoặc Execute Workflow) để kiểm tra luồng dữ liệu từ GLPI qua các node tính toán `Metrics`, `Generate report`.
- Sau khi kiểm tra email nhận được hiển thị chính xác, các sếp bật nút **Active** ở góc trên cùng bên phải để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh chat:** Thay vì chỉ gửi email, các sếp có thể nối thêm node **Telegram** hoặc **Slack** để bắn thông báo tổng quan số lượng ticket và tỷ lệ SLA ngay vào nhóm chat của bộ phận IT.
- **Lưu lịch sử báo cáo:** Thêm một node **Google Sheets** hoặc **Airtable** ở cuối luồng để lưu trữ lại các chỉ số hiệu suất hàng tháng, giúp dễ dàng vẽ biểu đồ tăng trưởng theo quý/năm.

### 📌 Kết luận
Workflow tạo báo cáo GLPI tự động này sẽ giúp các nhà quản lý IT tiết kiệm hàng chục giờ làm việc mỗi tháng, đồng thời kiểm soát chất lượng dịch vụ (SLA) một cách minh bạch và chuyên nghiệp nhất. Hãy cài đặt ngay để tối ưu hóa quy trình IT Helpdesk của doanh nghiệp!