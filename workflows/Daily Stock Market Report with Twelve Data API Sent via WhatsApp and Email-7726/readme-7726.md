---
title: "🚀 Tự động hóa Báo cáo Thị trường Chứng khoán hàng ngày qua WhatsApp và Email với n8n và Twelve Data"
description: "Hướng dẫn xây dựng workflow n8n tự động lấy dữ liệu chứng khoán từ Twelve Data API, phân tích biến động và gửi báo cáo qua WhatsApp, Email mỗi ngày."
slug: "tu-dong-hoa-bao-cao-chung-khoan-hang-ngay-whatsapp-email"
tags: [n8n, automation, no-code, finance, twelve-data, whatsapp, email]
keywords: [n8n workflow, báo cáo chứng khoán tự động, twelve data api, gui whatsapp email n8n, tu dong hoa giao dịch]
---

# 🚀 Tự động hóa Báo cáo Thị trường Chứng khoán hàng ngày qua WhatsApp và Email

Việc theo dõi biến động thị trường chứng khoán thủ công mỗi ngày tốn rất nhiều thời gian, đặc biệt khi các nhà đầu tư và nhà giao dịch cần nhanh chóng nắm bắt các mã tăng/giảm mạnh nhất (top gainers/losers) ngay sau khi thị trường đóng cửa. Nếu bạn phải tự tra cứu từng mã và soạn tin nhắn gửi đi, công việc này vừa nhàm chán vừa dễ bỏ lỡ cơ hội.

Được phát triển bởi **Oneclick AI Squad**, workflow n8n này sẽ giải quyết triệt để vấn đề trên bằng cách tự động hóa 100% quy trình: lấy dữ liệu từ Twelve Data API, xử lý số liệu, tổng hợp xu hướng và gửi báo cáo chi tiết đến điện thoại (qua WhatsApp) và hộp thư (Email) của bạn đúng giờ hẹn.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian tuyệt đối:** Không cần mở bảng giá hay tra cứu thủ công cuối ngày.
- **Cập nhật chính xác 100%:** Dữ liệu thời gian thực được lấy trực tiếp từ nguồn uy tín Twelve Data API vào lúc 5:00 chiều (Thứ Hai - Thứ Sáu).
- **Đa kênh tiếp nhận:** Báo cáo được gửi đồng thời qua WhatsApp để xem nhanh trên điện thoại và Email để lưu trữ hoặc xem chi tiết trên máy tính.
- **Phân tích thông minh:** Tự động lọc và làm nổi bật các mã có biến động mạnh nhất (top gainers/losers).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Twelve Data API Key:** Đăng ký tài khoản miễn phí tại [Twelve Data](https://twelvedata.com/) để lấy khóa API.
- **SMTP Credentials:** Thông tin kết nối SMTP để gửi email (Gmail, SendGrid, Resend, v.v.).
- **WhatsApp Cloud API Credentials:** Tài khoản Facebook Developer / Meta Business đã cấu hình WhatsApp Business API để gửi tin nhắn.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ nguồn cung cấp hoặc tạo mới canvas và copy/paste cấu trúc 8 nodes vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 8 nodes hoạt động tuần tự. Các sếp cần cấu hình kỹ các node sau:

- **Daily Market Close Trigger (Cron):** Node này mặc định kích hoạt vào lúc 5:00 chiều (giờ đóng cửa thị trường) từ Thứ Hai đến Thứ Sáu. Các sếp có thể điều chỉnh lại múi giờ (timezone) cho khớp với khu vực của mình.
- **Set Configuration Variables (Set):** Nơi các sếp cấu hình các biến quan trọng như **Twelve Data API Key**, danh sách các mã chứng khoán theo dõi (stock symbols), và thông tin người nhận.
- **Fetch Stock Data from Twelve Data (HTTP Request):** Node này gọi API của Twelve Data. Đảm bảo endpoint và header truyền API key từ node `Set Configuration Variables` chính xác.
- **Process Stock Movements, Format WhatsApp Message, Format Email Content (Code):** Các node JavaScript xử lý logic tính toán, lọc mã tăng/giảm mạnh nhất và định dạng nội dung hiển thị (markdown cho WhatsApp, HTML/Text cho Email). Không cần sửa code trừ khi các sếp muốn đổi giao diện hiển thị.
- **Send Email Alert (EmailSend):** Chọn credential **SMTP** đã chuẩn bị sẵn, điền email người gửi, người nhận và tiêu đề phù hợp.
- **Send message (WhatsApp):** Chọn credential **WhatsAppApi** (Meta Cloud API), điền Phone Number ID và số điện thoại người nhận để nhận tin nhắn báo cáo.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để chạy thử nghiệm (Test Run) và kiểm tra dữ liệu trả về ở từng node.
- Sau khi kiểm tra mọi thứ hoạt động trơn tru, hãy chuyển trạng thái workflow sang **Active** để hệ thống tự động chạy theo lịch hẹn.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm Telegram / Slack:** Ngoài WhatsApp và Email, các sếp có thể nối thêm node Telegram Bot để nhận báo cáo ngay trong nhóm chat công việc.
- **Lưu trữ lịch sử:** Thêm node **Google Sheets** hoặc **PostgreSQL** để lưu lại dữ liệu giá cổ phiếu mỗi ngày nhằm phục vụ việc backtest hoặc phân tích kỹ thuật dài hạn.
- **Cảnh báo ngưỡng (Threshold Alert):** Thêm điều kiện (If node) để nếu có mã nào biến động quá ±5%, hệ thống sẽ lập tức gửi tin nhắn khẩn cấp thay vì đợi đến cuối ngày.

### 📌 Kết luận
Workflow Daily Stock Market Report là trợ đắc lực giúp các nhà đầu tư nắm bắt thị trường mà không tốn công sức theo dõi bảng điện tử liên tục. Hãy cài đặt ngay lên hệ thống n8n của các sếp để tối ưu hóa quy trình đầu tư tài chính từ hôm nay!