---
title: "🚀 Tự động giám sát IP xác thực từ SaaS Alerts và gửi báo cáo qua SMTP2Go"
description: "Hướng dẫn xây dựng workflow n8n giúp tự động truy vấn dữ liệu đăng nhập, lọc IP trùng lặp, chuyển đổi sang file CSV và gửi báo cáo bảo mật qua SMTP2Go một cách chuyên nghiệp."
slug: "tu-dong-giam-sat-ip-xac-thuc-saas-alerts-smtp2go"
tags: [n8n, automation, secops, devops, smtp2go, saas-alerts]
keywords: [n8n workflow, tự động hóa bảo mật, SaaS Alerts API, SMTP2Go email, quản lý IP đăng nhập]
---

# 🚀 Tự động giám sát IP xác thực từ SaaS Alerts và gửi báo cáo qua SMTP2Go

Việc theo dõi thủ công các sự kiện đăng nhập, kiểm tra địa chỉ IP từ các nền tảng SaaS đối với đội ngũ IT và SecOps thường rất mất thời gian và dễ bỏ sót các dấu hiệu bất thường. Nếu các sếp đang đau đầu vì phải gom log, lọc IP thủ công rồi mới gửi báo cáo cho ban quản lý, thì đây chính là giải pháp tự động hóa 100% không cần code dành cho các sếp.

Workflow n8n này sẽ giúp tự động hóa toàn bộ quy trình: thu thập dữ liệu xác thực từ **SaaS Alerts API**, xử lý, lọc bỏ IP trùng lặp, chuyển đổi dữ liệu thành file CSV và tự động gửi báo cáo chi tiết qua **SMTP2Go**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Gom nhóm sự kiện đăng nhập thành công, OAuth, Office365 Shell mà không cần thao tác tay.
- **Dữ liệu sạch & chuẩn xác:** Tự động lọc bỏ các địa chỉ IP trùng lặp để tập trung vào các điểm truy cập thực tế.
- **Báo cáo chuyên nghiệp:** Tự động đóng gói dữ liệu thành file CSV và gửi email đính kèm thông qua SMTP2Go API.
- **Chủ động bảo mật:** Giúp đội ngũ SecOps nắm bắt nhanh chóng danh sách IP truy cập hệ thống theo yêu cầu hoặc lịch trình.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n đang hoạt động.
- Tài khoản và API Key của **SaaS Alerts** (tham khảo tài liệu API [tại đây](https://app.swaggerhub.com/apis/SaaS_Alerts/functions)).
- Tài khoản **SMTP2Go** kèm thông tin xác thực API/Header Auth để gửi email (xem thêm [tài liệu SMTP2Go](https://developers.smtp2go.com/docs/send-an-email)).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc sao chép mã nguồn JSON.
- Trong giao diện n8n Editor, chọn **Add workflow** -> Nhấn vào dấu `...` ở góc trên bên phải -> Chọn **Import from File** hoặc **Import from Clipboard** và dán mã JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 11 nodes liên kết chặt chẽ với nhau. Các sếp cần chú ý cấu hình các điểm mấu chốt sau:

- **Authentication Request Form (`formTrigger`):** Điểm khởi đầu của workflow, dùng để nhập các biến ngày tháng hoặc tham số truy vấn khi cần chạy thủ công.
- **Set Date and Form Variables (`set`):** Thiết lập các biến thời gian và tham số cần thiết cho các request tiếp theo.
- **Các node gọi API SaaS Alerts (`httpRequest`):**
  - `GET Events - Login Successful`
  - `GET Events - OAuth Authentication`
  - `GET Events - Office365 Shell WCSS`
  *Lưu ý:* Các sếp cần cấu hình Header chứa API Token/Key hợp lệ của SaaS Alerts để kết nối thành công.
- **Combine all Authentication Events (`merge`):** Gom dữ liệu từ các luồng sự kiện khác nhau thành một luồng thống nhất.
- **Filter IP Information (`set`) & Remove Duplicate IPs (`removeDuplicates`):** Lọc thông tin IP cần thiết và tiến hành loại bỏ các IP bị trùng lặp trong danh sách.
- **Convert to CSV (`convertToFile`) & Convert CSV to Base64 (`moveBinaryData`):** Chuyển đổi dữ liệu JSON thành định dạng file CSV và mã hóa dưới dạng Base64 để chuẩn bị đính kèm email.
- **Send Email Upon Completion (SMTP2Go) (`httpRequest`):** 
  - Cấu hình thông tin kết nối sử dụng `httpHeaderAuth` với thông tin tài khoản SMTP2Go.
  - Điền địa chỉ email người nhận, tiêu đề và nội dung thông báo kèm file đính kèm.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** với dữ liệu mẫu trên form để kiểm tra toàn bộ luồng chạy từ đầu đến cuối.
- Kiểm tra hòm thư nhận báo cáo xem file CSV đã hiển thị chính xác chưa.
- Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để workflow sẵn sàng hoạt động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp lịch chạy tự động:** Thay vì dùng `formTrigger`, các sếp có thể đổi thành node `Schedule Trigger` để n8n tự động quét log SaaS Alerts mỗi ngày/mỗi tuần.
- **Cảnh báo qua Telegram/Slack:** Kết nối thêm node Telegram hoặc Slack để gửi thông báo nhanh khi phát hiện số lượng IP lạ vượt ngưỡng.
- **Lưu trữ backup:** Thêm node Google Drive hoặc OneDrive để lưu trữ file CSV báo cáo tự động vào mây phục vụ kiểm toán lâu dài.

### 📌 Kết luận
Workflow **Monitor Authentication IPs from SaaS Alerts & Email Reports via SMTP2Go** là một công cụ cực kỳ đắc lực giúp tự động hóa quy trình SecOps, tiết kiệm thời gian tổng hợp log và nâng cao năng lực giám sát bảo mật cho doanh nghiệp. Hãy import ngay vào hệ thống n8n của các sếp và tối ưu hóa vận hành ngay hôm nay!