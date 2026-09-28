---
title: "🚀 Tự động hóa lấy báo cáo thanh toán Telr, lưu vào SQL và gửi email tổng hợp"
description: "Hướng dẫn thiết lập workflow n8n tự động kết nối Telr API, đồng bộ báo cáo giao dịch vào SQL Server và gửi email báo cáo hàng ngày."
slug: "tu-dong-hoa-bao-cao-thanh-toan-telr-sql-email"
tags: [n8n, automation, no-code, telr, sql, email, payment-reports]
keywords: [n8n workflow, tự động hóa thanh toán, Telr API, lưu báo cáo vào SQL, gửi email tự động n8n]
---

# 🚀 Tự động hóa lấy báo cáo thanh toán Telr, lưu vào SQL và gửi email tổng hợp

Đối với các nhà bán hàng (Merchants) và doanh nghiệp sử dụng cổng thanh toán **Telr**, việc đối soát giao dịch thủ công mỗi ngày là một công việc tẻ nhạt, mất thời gian và dễ xảy ra sai sót. Phải tải file báo cáo, xử lý định dạng, đẩy vào cơ sở dữ liệu rồi gửi email tổng hợp cho cấp trên làm tiêu tốn rất nhiều nguồn lực.

Workflow n8n này sẽ giúp các sếp **tự động hóa 100% quy trình**: Tự động gọi API lấy báo cáo, xử lý và giải nén file, lưu trữ trực tiếp vào cơ sở dữ liệu SQL, đồng thời gửi email thông báo kết quả thành công mà không cần can thiệp thủ công.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Không cần thao tác thủ công, lịch trình tự động kích hoạt lấy báo cáo mỗi ngày.
- **Đồng bộ dữ liệu chính xác**: Chuyển đổi dữ liệu từ file XLS sang SQL một cách mượt mà, tránh sai sót dữ liệu.
- **Báo cáo kịp thời**: Nhận email thông báo kết quả và tóm tắt giao dịch ngay sau khi hoàn thành.
- **Vận hành 24/7**: Giúp đội ngũ tài chính kế toán có số liệu chính xác ngay từ đầu ngày làm việc.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance**: Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Telr Account**: Tài khoản Telr có quyền truy cập API và thông tin xác thực (HTTP Basic Auth).
- **Database**: Microsoft SQL Server (hoặc tương thích) để lưu trữ dữ liệu giao dịch.
- **SMTP Server**: Thông tin tài khoản SMTP (Gmail, SendGrid, Office365...) để gửi email thông báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow từ nguồn cung cấp.
- Trên giao diện n8n Editor, chọn **Add workflow** -> **Import from File** và chọn file JSON vừa tải. Hoặc copy toàn bộ JSON và dán trực tiếp vào màn hình n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các thông số tại các node sau:
- **Schedule Trigger**: Thiết lập lịch chạy tự động (ví dụ: Chạy mỗi ngày vào 1:00 sáng).
- **TELR API** & **TELR API WITH DATE**: Cấu hình thông tin xác thực `httpBasicAuth` với API key/thông tin tài khoản Telr của các sếp.
- **Logic for date**: Node code JavaScript tính toán khoảng thời gian cần lấy báo cáo (ví dụ: ngày hôm qua).
- **Extract from File**: Cấu hình đọc file định dạng `xls` đã được giải nén từ node **Compression**.
- **Data Insert SQL**: Chọn credential `microsoftSql` kết nối đến database của các sếp, kiểm tra lại tên bảng (table) và câu lệnh SQL INSERT.
- **Success Condition**: Node IF kiểm tra xem việc insert dữ liệu có thành công hay không để quyết định nhánh chạy tiếp theo.
- **Send email**: Cấu hình thông tin kết nối `smtp` và địa chỉ email nhận báo cáo tổng hợp.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để test thủ công lần đầu với dữ liệu thực tế.
- Kiểm tra kết quả trong Database và hộp thư đến.
- Nếu mọi thứ chạy mượt mà, hãy bật công tắc **Active** ở góc trên cùng bên phải để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh chat**: Thay vì chỉ gửi email, các sếp có thể nối thêm node **Telegram** hoặc **Slack** để bắn thông báo ngay vào nhóm chat của công ty khi hoàn tất báo cáo.
- **Xử lý lỗi (Error Handling)**: Thêm nhánh Error Trigger để nếu quá trình gọi API Telr hoặc Insert SQL bị lỗi, hệ thống sẽ tự động cảnh báo ngay lập tức.
- **Lưu file backup**: Lưu trữ file XLS tải về vào Google Drive hoặc S3 để làm kho lưu trữ lịch sử lâu dài.

### 📌 Kết luận
Workflow này là một "vũ khí" cực kỳ lợi hại giúp tự động hóa khâu đối soát tài chính cho các doanh nghiệp sử dụng cổng thanh toán Telr. Hãy cài đặt ngay hôm nay để giải phóng thời gian cho đội ngũ kế toán và vận hành!