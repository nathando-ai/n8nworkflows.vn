---
title: "🚀 Tự động hóa tạo và gửi tài liệu kinh doanh PDF hàng loạt với Google Sheets, CraftMyPDF & Gmail"
description: "Hướng dẫn chi tiết workflow n8n tự động lấy dữ liệu từ Google Sheets, tạo file PDF hàng loạt qua CraftMyPDF, lưu trữ Google Drive và gửi email qua Gmail cho từng nhân sự hoặc khách hàng."
slug: "tu-dong-hoa-tao-va-gui-tai-lieu-kinh-doanh-pdf-hang-loat"
tags: [n8n, automation, craftmypdf, google-sheets, google-drive, gmail]
keywords: [n8n workflow, tự động tạo PDF, craftmypdf n8n, google sheets to pdf, gửi email tự động n8n]
---

# 🚀 Tự động hóa tạo và gửi tài liệu kinh doanh PDF hàng loạt

Các sếp có bao giờ cảm thấy mệt mỏi khi phải thủ công copy/paste thông tin từ Google Sheets vào các mẫu hợp đồng, thỏa thuận, bảng lương hay hóa đơn cho hàng chục, hàng trăm nhân sự hoặc khách hàng? Việc làm thủ công này không chỉ ngốn hàng giờ đồng hồ mà còn cực kỳ dễ xảy ra sai sót dữ liệu nhạy cảm.

Giải pháp ở đây là gì? Workflow n8n này sẽ giúp các sếp tự động hóa 100% quy trình: Lấy dữ liệu từ Google Sheets 👉 Tạo file PDF chuyên nghiệp qua CraftMyPDF 👉 Lưu trữ bản sao vào Google Drive 👉 Tự động gửi email đính kèm file PDF qua Gmail. Tất cả diễn ra mượt mà mà không cần một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Xử lý hàng loạt tài liệu (hợp đồng, thỏa thuận, hóa đơn) chỉ với một cú click hoặc lịch chạy định kỳ.
- **Không sai sót:** Dữ liệu được đổ trực tiếp từ Google Sheets sang mẫu PDF với độ chính xác tuyệt đối.
- **Chuyên nghiệp hóa:** File PDF được thiết kế đẹp mắt qua CraftMyPDF và gửi tự động đến đúng người nhận qua Gmail.
- **Lưu trữ khoa học:** Tự động sao lưu toàn bộ tài liệu đã tạo lên Google Drive để dễ dàng tra cứu về sau.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản sau:
- **n8n (Self-hosted version):** Workflow này yêu cầu phiên bản tự host của n8n.
- **Google Sheets & Google Drive:** Tài khoản Google có quyền truy cập Sheets và Drive.
- **CraftMyPDF:** Tạo tài khoản miễn phí tại [CraftMyPDF](https://app.craftmypdf.com/) và tạo sẵn một Template PDF.
- **Gmail Account:** Tài khoản Gmail đã kết nối OAuth2 với n8n để gửi email.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow hoặc copy đoạn JSON từ nguồn, sau đó dán trực tiếp vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các node quan trọng sau:

- **Node `Get employees` (Google Sheets):**
  - Kết nối tài khoản Google Sheets OAuth2 của các sếp.
  - Clone mẫu Google Sheet tại [đây](https://docs.google.com/spreadsheets/d/1YQPuoEubRHJepRKdquks69Iqf2XdGVKfpWOdYwk3RMg/edit?usp=sharing) và trỏ node này đến bảng tính của các sếp để lấy dữ liệu nhân sự/khách hàng.

- **Node `Loop Over Items` (Split InBatches):**
  - Giúp duyệt qua từng dòng dữ liệu trong Google Sheets một cách mượt mà mà không sợ bị nghẽn hệ thống.

- **Node `Create agreement` (CraftMyPDF):**
  - Kết nối CraftMyPDF API Key.
  - Nhập **Template ID** của mẫu PDF mà các sếp đã tạo sẵn trên trang quản trị CraftMyPDF.
  - Map các trường dữ liệu từ Google Sheets vào các biến trong Template của CraftMyPDF.

- **Node `Get agreement` (HTTP Request):**
  - Node này dùng để tải file PDF vừa được CraftMyPDF tạo ra thông qua đường dẫn URL trả về.

- **Node `Upload agreement` (Google Drive):**
  - Kết nối Google Drive OAuth2.
  - Chọn thư mục trên Drive để lưu trữ các file PDF hợp đồng/tài liệu được tạo tự động.

- **Node `Update row` (Google Sheets):**
  - Cập nhật lại trạng thái (Ví dụ: "Đã gửi", "Hoàn thành") vào dòng tương ứng trong Google Sheet sau khi tài liệu đã được tạo và gửi thành công.

- **Node `Send email with PDF` (Gmail):**
  - Kết nối tài khoản Gmail OAuth2.
  - Cấu hình tiêu đề, nội dung email và đính kèm file PDF nhị phân từ bước trước để gửi thẳng đến người nhận.

#### 3. Kích hoạt ⚡️
- Bấm nút **‘Execute workflow’** để chạy thử nghiệm (Test Run) với một vài dòng dữ liệu mẫu đầu tiên.
- Kiểm tra lại Google Drive, Gmail và Google Sheets xem dữ liệu đã đồng bộ chính xác chưa.
- Nếu mọi thứ chạy mượt mà, gạt công tắc sang **Active** để bật chế độ tự động chạy thật!

### ✍️ Mẹo & gợi ý nâng cao
- **Thay đổi Triggers:** Thay vì dùng nút `Manual Trigger`, các sếp có thể đổi thành `Webhook` (nhận dữ liệu từ CRM/Web form) hoặc `Schedule Trigger` (chạy tự động vào một giờ cố định mỗi tháng để làm bảng lương).
- **Thông báo qua Telegram/Slack:** Thêm một node thông báo vào kênh Telegram hoặc Slack mỗi khi hệ thống tạo và gửi thành công một tài liệu để team dễ dàng theo dõi.
- **Xử lý lỗi (Error Handling):** Thêm nhánh xử lý ở node `Success?` để nếu gửi email thất bại, hệ thống sẽ tự động ghi log lỗi vào một cột riêng trong Google Sheets.

### 📌 Kết luận
Tự động hóa quy trình tạo và gửi tài liệu kinh doanh không chỉ giúp các sếp tiết kiệm hàng đống thời gian mà còn nâng tầm chuyên nghiệp cho doanh nghiệp trong mắt khách hàng và nhân viên. Hãy áp dụng ngay workflow này vào hệ thống của các sếp để tối ưu hóa vận hành ngay hôm nay!