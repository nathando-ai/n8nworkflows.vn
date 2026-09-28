---
title: "🚀 Tự động phát hành chứng chỉ PDF chuyên nghiệp từ Google Sheets, TemplateFox và Gmail"
description: "Hướng dẫn tự động hóa quy trình tạo và gửi chứng chỉ PDF chuẩn lưu trữ ngay khi có học viên hoàn thành khóa học trên Google Sheets, kết hợp TemplateFox, Google Drive và Gmail."
slug: "tu-dong-phat-hanh-chung-chi-pdf-google-sheets-templatefox-gmail"
tags: [n8n, automation, no-code, google-sheets, templatefox, gmail, google-drive]
keywords: [n8n workflow, tự động hóa chứng chỉ, templatefox n8n, gửi chứng chỉ tự động, google sheets gmail automation]
---

# 🚀 Tự động phát hành chứng chỉ PDF chuyên nghiệp từ Google Sheets, TemplateFox và Gmail

Các sếp có đang đau đầu vì mỗi khi có học viên hoàn thành khóa học, đội ngũ vận hành lại phải lọ mọ điền tên thủ công lên file thiết kế, xuất PDF, lưu vào Google Drive rồi soạn email gửi từng người? Quá mất thời gian, dễ sai sót và trông thiếu chuyên nghiệp đúng không ạ?

Đừng lo! Bài viết này sẽ hướng dẫn các sếp thiết lập một workflow n8n tự động hóa 100% quy trình này: Ngay khi có dòng dữ liệu mới xuất hiện trên Google Sheets, hệ thống sẽ tự động tạo chứng chỉ PDF chuẩn chất lượng cao, lưu trữ an toàn trên Google Drive, gửi email chúc mừng kèm chứng chỉ cho học viên, đồng thời cập nhật ngược lại link chứng chỉ vào Google Sheets để quản lý. Không cần code, chỉ cần "lên đồ" và chạy!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Chứng chỉ được phát hành ngay lập tức (real-time) khi học viên hoàn thành khóa học.
- **Chất lượng chuyên nghiệp:** Sử dụng định dạng PDF/A chuẩn lưu trữ dài hạn từ TemplateFox.
- **Lưu trữ minh bạch:** Tự động lưu file vào Google Drive và ghi lại link vĩnh viễn vào Google Sheets để làm audit trail (dấu vết kiểm toán).
- **Trải nghiệm học viên đỉnh cao:** Nhận ngay email chúc mừng kèm chứng chỉ cá nhân hóa chỉ trong tích tắc.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản **n8n** (Cloud hoặc Self-hosted).
- Tài khoản **Google Sheets** và **Google Drive**.
- Tài khoản **Gmail** để gửi email tự động.
- Tài khoản **TemplateFox** (lấy API Key miễn phí tại [app.templatefox.com](https://app.templatefox.com)).
- Cài đặt Community Node **TemplateFox** (`n8n-nodes-templatefox`) trên n8n của các sếp.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể sử dụng file JSON của workflow này, copy và paste trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node sau:

- **New Completion Row (`googleSheetsTrigger`):** 
  - Kết nối tài khoản Google Sheets OAuth2.
  - Chọn file Google Sheets và Sheet chứa dữ liệu học viên hoàn thành khóa học. 
  - Chuẩn bị sẵn các cột trong sheet: `Participant Name`, `Email`, `Course`, `Completion Date`, `Instructor`, kèm theo 2 cột để ghi nhận kết quả: `Certificate URL` và `Issued At`.
  
- **TemplateFox (`n8n-nodes-templatefox.templateFox`):**
  - Nhập **TemplateFox API Key** của các sếp.
  - Chọn mẫu (template) chứng chỉ đã tạo sẵn trên TemplateFox.
  - Map (ánh xạ) các trường dữ liệu từ Google Sheets (Tên, Tên khóa học, Ngày hoàn thành, Giảng viên...) vào các trường tương ứng trên template.

- **Download PDF (`httpRequest`):**
  - Node này nhận output từ TemplateFox để tải file PDF về. Thường node này đã được cấu hình sẵn, các sếp chỉ cần giữ nguyên hoặc kiểm tra lại đường dẫn trả về từ TemplateFox.

- **Archive to Google Drive (`googleDrive`):**
  - Kết nối tài khoản Google Drive OAuth2.
  - Chọn thư mục (`Folder ID`) trên Drive nơi các sếp muốn lưu trữ toàn bộ chứng chỉ của học viên.

- **Email Certificate (`gmail`):**
  - Kết nối tài khoản Gmail OAuth2.
  - Soạn nội dung email chúc mừng, chèn link vĩnh viễn của file PDF từ Google Drive vào nội dung email để học viên có thể tải về bất cứ lúc nào.

- **Update Sheet Row (`googleSheets`):**
  - Cấu hình ở chế độ `update`.
  - Ghi đè đường dẫn file PDF trên Google Drive (`Certificate URL`) và thời gian phát hành (`Issued At`) trở lại dòng tương ứng trong Google Sheets.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và thêm một dòng dữ liệu test trên Google Sheets để kiểm tra toàn bộ luồng chạy.
- Sau khi test thành công, gạt công tắc sang **Active** để hệ thống tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo qua Slack/Telegram:** Thêm một node Slack hoặc Telegram ngay sau bước lưu Google Drive để bắn thông báo về nhóm nội bộ (ví dụ: *"Vừa phát hành chứng chỉ cho học viên Nguyễn Văn A"*).
- **Bộ lọc điểm số:** Thêm node `IF` trước node TemplateFox để kiểm tra điều kiện (ví dụ: `Score` >= 80 mới cấp chứng chỉ, tránh cấp nhầm).
- **Chạy định kỳ hàng loạt (Batch):** Thay vì dùng Google Sheets Trigger theo thời gian thực, các sếp có thể đổi thành `Schedule Trigger` kết hợp với `Get Many Rows` để gom lại phát hành chứng chỉ hàng loạt vào cuối ngày.

### 📌 Kết luận
Việc tự động hóa quy trình cấp chứng chỉ không chỉ giúp tiết kiệm hàng tá giờ làm việc thủ công mà còn tạo ấn tượng cực kỳ chuyên nghiệp với học viên ngay từ điểm chạm cuối cùng. Chúc các sếp ứng dụng thành công và "lên đồ" mượt mà cho hệ thống của mình!