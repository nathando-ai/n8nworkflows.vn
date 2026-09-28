---
title: "🚀 Tự động kiểm tra font chữ email từ Gmail với Google Sheets - Workflow n8n"
description: "Tự động hóa quy trình kiểm tra font chữ email bằng n8n, so sánh font chữ thực tế với font chữ mong đợi từ Google Sheets, tiết kiệm thời gian QA và đảm bảo tính nhất quán với hướng dẫn thiết kế."
slug: "tu-dong-kiem-tra-font-chu-email-gmail-google-sheets"
tags: [n8n, automation, no-code, email-marketing, qa-automation]
keywords: [n8n workflow, tự động hóa email, kiểm tra font chữ, qa automation]
---

# 🚀 Tự động kiểm tra font chữ email từ Gmail với Google Sheets

[Các sếp] có bao giờ phải kiểm tra thủ công font chữ của hàng trăm email mỗi ngày không? Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình kiểm tra font chữ email bằng cách so sánh font chữ thực tế trong email với font chữ mong đợi được lưu trong Google Sheets. Không cần phải mở từng email và kiểm tra thủ công nữa!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa quy trình kiểm tra font chữ email, giảm thời gian QA từ hàng giờ xuống vài phút.
- **Chính xác cao**: So sánh font chữ thực tế với font chữ mong đợi, đảm bảo tính nhất quán với hướng dẫn thiết kế.
- **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công, đảm bảo kiểm tra được thực hiện liên tục và chính xác.
- **Dễ dàng quản lý**: Lưu kết quả kiểm tra vào Google Sheets, giúp quản lý và theo dõi dễ dàng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Gmail với quyền truy cập vào email cần kiểm tra.
- Tài khoản Google Sheets với bảng dữ liệu chứa font chữ mong đợi.
- Quyền truy cập vào n8n để import và cấu hình workflow.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Để import workflow, các sếp có thể thực hiện theo các bước sau:

1. Truy cập vào n8n Editor.
2. Nhấn vào nút "Import from URL" và nhập URL sau: [https://n8n.io/workflows/13566](https://n8n.io/workflows/13566).
3. Hoặc, các sếp có thể tải file JSON từ liên kết trên và import trực tiếp vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm các node chính sau:

- **When clicking ‘Execute workflow’**: Node này kích hoạt workflow khi các sếp nhấn nút "Execute workflow".
- **Get many messages**: Node này lấy danh sách email từ Gmail. Các sếp cần cấu hình credentials cho Gmail OAuth2.
- **Extract Content Font Family from HTML**: Node này trích xuất font chữ từ HTML của email. Các sếp cần kiểm tra và cập nhật logic JavaScript để phù hợp với cấu trúc HTML của email.
- **Combine Font Inputs**: Node này kết hợp font chữ mong đợi và font chữ thực tế.
- **Extract Actual Font Family and Results**: Node này trích xuất font chữ thực tế và so sánh với font chữ mong đợi.
- **Load Expected Content and Font Family**: Node này tải font chữ mong đợi từ Google Sheets. Các sếp cần cấu hình credentials cho Google Sheets OAuth2 API và chỉ định ID của bảng dữ liệu.
- **Log Font Checks to Excel**: Node này lưu kết quả kiểm tra vào Google Sheets. Các sếp cần cấu hình credentials cho Google Sheets OAuth2 API và chỉ định ID của bảng dữ liệu.

#### 3. Kích hoạt ⚡️
Sau khi cấu hình các node, các sếp cần thực hiện các bước sau để kích hoạt workflow:

1. Kiểm tra kết nối và cấu hình các node.
2. Thực hiện test run với dữ liệu mẫu để đảm bảo workflow hoạt động đúng.
3. Bật Active workflow để chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Telegram**: Các sếp có thể cấu hình workflow để gửi thông báo kết quả kiểm tra qua Slack hoặc Telegram.
- **Lưu log kiểm tra**: Các sếp có thể lưu log kiểm tra vào Google Sheets hoặc cơ sở dữ liệu để theo dõi lịch sử kiểm tra.
- **Gửi báo cáo định kỳ**: Các sếp có thể cấu hình workflow để gửi báo cáo kiểm tra định kỳ qua email hoặc Slack.

### 📌 Kết luận
Workflow "Validate email font families from Gmail with Google Sheets" giúp các sếp tự động hóa quy trình kiểm tra font chữ email, tiết kiệm thời gian và đảm bảo tính nhất quán với hướng dẫn thiết kế. Các sếp chỉ cần import workflow, cấu hình các node và kích hoạt workflow để bắt đầu kiểm tra font chữ email một cách tự động và chính xác.