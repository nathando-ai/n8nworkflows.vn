---
title: "🚀 Gửi báo cáo thời gian hàng tuần từ TMetric đến nhân viên qua Slack"
description: "Hướng dẫn tự động hóa gửi báo cáo thời gian hàng tuần từ TMetric đến nhân viên qua Slack, tiết kiệm thời gian và tăng hiệu quả làm việc"
slug: "gui-bao-cao-thoi-gian-hang-tuan-tu-tmetric-den-slack"
tags: [n8n, automation, no-code, hr, tmetric, slack]
keywords: [n8n workflow, tự động hóa, báo cáo thời gian, tmetric, slack]
---

# 🚀 Gửi báo cáo thời gian hàng tuần từ TMetric đến nhân viên qua Slack

[Các sếp đang gặp khó khăn khi phải theo dõi và báo cáo thời gian làm việc của nhân viên hàng tuần một cách thủ công. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình này chỉ trong vài bước đơn giản.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa quy trình báo cáo hàng tuần
- Tăng hiệu quả: Nhân viên nhận được báo cáo cá nhân hóa ngay lập tức
- Giảm lỗi: Dữ liệu được xử lý chính xác và kịp thời
- Hoạt động liên tục: Báo cáo được gửi tự động mỗi tuần
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản TMetric với API key
- Tài khoản Slack với quyền gửi tin nhắn
- N8N Data Table (sẽ được tạo tự động trong quá trình setup)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấn vào "Import from URL" và dán link sau: https://n8n.io/workflows/14511
3. Hoặc tải file JSON về và chọn "Import from File"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Globals"**:
   - Điền `tmAccountId`: ID tài khoản TMetric của bạn (tìm trong URL khi truy cập TMetric)
   - Đặt `Allow hours missing percentage`: Ngưỡng phần trăm thời gian thiếu cho phép (ví dụ: 10)
   - Đặt `tmetricToSlackUserDataTableName`: Tên bảng dữ liệu (ví dụ: "TMetric_Slack_Users")

2. **Node "Get TMetric Users" và các node HTTP Request khác**:
   - Tạo mới credential "Header Auth" với:
     - Name: Authorization
     - Value: <Your Tmetric API Key> (thay bằng API key của bạn)

3. **Node "Get many users"**:
   - Đảm bảo đã chọn đúng credential Slack OAuth2 API

4. **Node "Send a message"**:
   - Tùy chỉnh nội dung tin nhắn theo nhu cầu của công ty
   - Chọn gửi tin nhắn trực tiếp hoặc vào channel

#### 3. Kích hoạt ⚡️
1. Chạy "Setup" node một lần để tạo bảng dữ liệu và thiết lập mapping giữa TMetric và Slack
2. Sau khi setup hoàn tất, kích hoạt node "Run Once a Week" để bắt đầu gửi báo cáo hàng tuần
3. Test run dữ liệu mẫu trước khi kích hoạt hoàn toàn

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node "Email" để gửi bản sao báo cáo đến email quản lý
- Kết hợp với Google Sheets để lưu trữ lịch sử báo cáo
- Tùy chỉnh báo cáo theo bộ phận hoặc dự án cụ thể
- Thêm cảnh báo khi phát hiện thời gian làm việc bất thường

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quy trình báo cáo thời gian hàng tuần, giảm thiểu công việc thủ công và tăng tính chính xác của dữ liệu. Bằng cách tích hợp TMetric và Slack, các sếp có thể theo dõi hiệu suất làm việc của nhân viên một cách hiệu quả hơn. Hãy áp dụng ngay để nâng cao hiệu quả quản lý nhân sự của bạn!