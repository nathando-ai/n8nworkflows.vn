---
title: "🚀 Tự động hóa cập nhật thực đơn nhà hàng và thông báo đa kênh với n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động phát hiện thay đổi thực đơn từ Google Sheets và gửi thông báo cho khách hàng qua WhatsApp, Email hoặc SMS."
slug: "tu-dong-hoa-cap-nhat-thuc-don-nha-hang-va-thong-bao-da-kenh-n8n"
tags: [n8n, automation, no-code, google-sheets, whatsapp, email, twilio]
keywords: [n8n workflow, tự động hóa nhà hàng, thông báo thực đơn, google sheets, whatsapp automation, twilio sms]
---

# 🚀 Tự động hóa cập nhật thực đơn nhà hàng và thông báo đa kênh với n8n

Các sếp làm trong ngành F&B ( nhà hàng, quán ăn, quán cafe) chắc chắn hiểu cảm giác đau đầu mỗi khi thay đổi thực đơn đặc biệt (special menu) hoặc có món mới. Việc phải thủ công thông báo cho từng nhóm khách hàng qua WhatsApp, Email hay SMS vừa tốn thời gian, dễ sót khách lại vừa thiếu tính chuyên nghiệp.

Đừng lo, bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ xịn sò do **Oneclick AI Squad** thiết kế: **Food Menu Update Notifier**. Workflow này sẽ tự động hóa toàn bộ quy trình: kiểm tra thay đổi thực đơn trên Google Sheets, soạn nội dung thông báo hấp dẫn và gửi đúng kênh mà khách hàng yêu cầu (WhatsApp, Email hoặc SMS) mà không cần tốn một phút thao tác thủ công nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động 100%:** Định kỳ kiểm tra thực đơn, phát hiện thay đổi và kích hoạt gửi thông báo ngay lập tức.
- **Cá nhân hóa đa kênh:** Khách thích nhận tin qua kênh nào (WhatsApp, Email, SMS), hệ thống phục vụ đúng kênh đó.
- **Minh bạch dữ liệu:** Tự động ghi log trạng thái gửi tin (thành công/thất bại) trực tiếp vào Google Sheets để dễ dàng kiểm tra.
- **Tiết kiệm nguồn lực:** Thay vì tốn hàng giờ nhân sự trực nhắn tin, hệ thống tự động làm việc trơn tru 24/7.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Google Sheets:** 2 bảng tính (1 bảng chứa thực đơn đặc biệt và 1 bảng chứa danh sách khách hàng kèm kênh liên lạc ưu tiên).
- **Cổng gửi tin nhắn/Email:** 
  - API WhatsApp (hoặc dịch vụ bên thứ ba tích hợp qua HTTP Request).
  - Tài khoản SMTP (để gửi Email).
  - Tài khoản Twilio (để gửi SMS).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow Food Menu Update Notifier và dán trực tiếp vào n8n Editor của mình, hoặc import file JSON thông qua giao diện quản lý workflow.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 17 nodes được sắp xếp logic từ quét dữ liệu, xử lý logic, đến gửi tin và ghi log. Các sếp cần cấu hình kỹ các điểm sau:

- **Daily Menu Update Scheduler:** Cấu hình thời gian chạy định kỳ (mỗi ngày một lần hoặc theo giờ nhà hàng mở cửa).
- **Fetch Special Menu Data & Fetch Customer Contact List:** Kết nối tài khoản `googleSheetsOAuth2Api` của các sếp, sau đó trỏ đúng đến File ID và Sheet Name chứa dữ liệu thực đơn và danh sách khách hàng.
- **Detect Menu Changes & Generate Menu Alert Message:** Hai node `code` này dùng JavaScript để so sánh trạng thái thực đơn cũ/mới và tạo ra thông điệp chào mời hấp dẫn. Các sếp có thể tùy biến lại mẫu câu chữ cho phù hợp với văn phong quán của mình.
- **Merge Menu with Customer Data & Split by Notification Preference:** Xử lý ghép nối dữ liệu và chia nhỏ batch để gửi tin nhắn hàng loạt mà không sợ quá tải.
- **Filter WhatsApp Users, Filter Email Users, Filter SMS Users:** Các node điều kiện (`if`) giúp phân loại đúng kênh mà khách hàng đã đăng ký nhận tin.
- **Send WhatsApp Notification & Send Twilio SMS Alert:** Cấu hình thông tin API endpoint, Header và Credentials (`httpBasicAuth` đối với Twilio) để bắn tin đi.
- **Send Menu Email:** Kết nối credentials `smtp` để gửi email hàng loạt.
- **Log WhatsApp Status, Log Email Status1, Log SMS Status:** Các node ghi log ngược lại vào Google Sheets (sử dụng thao tác `append`) giúp các sếp lưu vết lịch sử gửi tin cực kỳ chuyên nghiệp.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) thủ công với một vài dòng dữ liệu mẫu để kiểm tra luồng chạy xem tin nhắn có bắn đúng hay không.
- Sau khi mọi thứ mượt mà, gạt công tắc sang **Active workflow** để hệ thống tự động vận hành.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Telegram/Slack:** Các sếp có thể mở rộng thêm một nhánh gửi thông báo về group nội bộ nhân viên bếp/quản lý để họ nắm được khi hệ thống phát thực đơn mới.
- **Xử lý lỗi (Error Handling):** Thêm node Error Trigger để nếu tin nhắn SMS hay WhatsApp lỗi, hệ thống sẽ tự động gửi email dự phòng hoặc bắn alert cho quản lý.
- **Cải tiến AI:** Kết hợp thêm các mô hình ngôn ngữ lớn (LLM) để tự động viết lại mô tả món ăn thật kích thích vị giác dựa trên nguyên liệu có sẵn trong Google Sheets.

### 📌 Kết luận
Workflow **Food Menu Update Notifier** là một trợ thủ đắc lực giúp số hóa hoàn toàn quy trình chăm sóc khách hàng F&B. Chỉ với vài bước cấu hình, các sếp đã có ngay một hệ thống thông báo tự động chuyên nghiệp không thua kém các thương hiệu lớn. Chúc các sếp cài đặt thành công và bùng nổ doanh số!