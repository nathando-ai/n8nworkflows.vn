---
title: "🚀 Tự động hóa tạo chứng chỉ hàng loạt từ Google Slides, xuất PDF và gửi Email qua Gmail với n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động đọc danh sách từ Google Sheets, tạo chứng chỉ cá nhân hóa hàng loạt dưới dạng PDF qua Google Slides và gửi email tự động."
slug: "tu-dong-hoa-tao-chung-chi-hang-loat-google-slides-pdf-gmail"
tags: [n8n, automation, no-code, google-workspace, google-sheets, gmail]
keywords: [n8n workflow, tạo chứng chỉ tự động, google slides to pdf, tự động gửi email gmail, google sheets automation]
---

# 🚀 Tự động hóa tạo chứng chỉ hàng loạt từ Google Slides, xuất PDF và gửi Email qua Gmail

Các sếp có tổ chức khóa học, sự kiện, hội thảo (webinar) và đau đầu mỗi khi phải ngồi làm thủ công hàng trăm chiếc chứng chỉ (certificate)? Việc copy tên từng học viên vào file thiết kế, xuất ra PDF rồi mò mẫm gửi email thủ công không chỉ tốn hàng giờ đồng hồ mà còn rất dễ sai sót.

Đừng lo, workflow n8n này sẽ thay các sếp "cân" trọn gói quy trình từ A-Z một cách tự động 100%: Đọc dữ liệu từ Google Sheets 👉 Nhân bản template Google Slides 👉 Điền thông tin cá nhân hóa 👉 Xuất file PDF 👉 Lưu Google Drive 👉 Gửi email qua Gmail 👉 Dọn dẹp file tạm và cập nhật trạng thái!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 99% thời gian:** Xử lý hàng loạt hàng trăm học viên chỉ trong vài phút mà không cần đụng tay.
- **Cá nhân hóa chính xác:** Tự động điền tên, ngày tháng, mã chứng chỉ riêng biệt cho từng người.
- **Lưu trữ khoa học & Tự động dọn dẹp:** Tự động lưu bản PDF vào Google Drive và xóa file Google Slides tạm để giữ Drive luôn gọn gàng.
- **Hoạt động ổn định:** Tích hợp bộ đếm lô (Batch processing) và thời gian chờ để tránh bị Google API giới hạn tốc độ (Rate Limit).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản **n8n** (Cloud hoặc Self-hosted).
- Tài khoản **Google** có quyền truy cập: Google Sheets, Google Drive, Google Slides và Gmail.
- File danh sách học viên mẫu trên Google Sheets ([Xem mẫu tại đây](https://docs.google.com/spreadsheets/d/1fHcfilCPpI4aAiJFQC3cPIAdJMmctMubz3kcOeai1yA/edit?usp=sharing)).
- File Template Google Slides mẫu với các placeholder: `[Name]`, `[Date]`, và `[N]` ([Xem mẫu tại đây](https://docs.google.com/presentation/d/1YWYsNfq4FeHP03MSYFz1cobVczBHWxwEW95BE4w0FHc/edit?slide=id.p#slide=id.p)).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Copy mã JSON của workflow hoặc tải file từ nguồn cung cấp.
- Mở n8n Editor, chọn **Add workflow** -> **Import from File** hoặc dán trực tiếp vào màn hình làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình các node quan trọng sau để hệ thống chạy mượt mà:

- **Node `Read File` (Google Sheets):** 
  - Kết nối `googleSheetsOAuth2Api`.
  - Trỏ tới file Google Sheets chứa danh sách người nhận của các sếp.
  - Cấu hình chỉ lấy các dòng chưa được đánh dấu là đã gửi (để chạy lặp lại không bị trùng).
- **Node `Copy Slides Template` & `Replace Template Placeholders` (HTTP Request / Google Slides):**
  - Kết nối `googleDriveOAuth2Api` và `googleSlidesOAuth2Api`.
  - Thay thế ID file template mẫu trong yêu cầu HTTP bằng ID file Google Slides của các sếp.
  - Đảm bảo các placeholder trong template khớp với dữ liệu (ví dụ: `[Name]`, `[Date]`, `[N]`).
- **Node `Save PDF to Drive` (Google Drive):**
  - Chọn thư mục đích trên Google Drive nơi các sếp muốn lưu trữ các file PDF chứng chỉ đã xuất.
- **Send a message (Gmail):**
  - Kết nối `gmailOAuth2`.
  - Cấu hình tiêu đề, nội dung email chúc mừng và đính kèm file PDF vừa được xuất từ bước trước.
- **Node `Mark as Processed` (Google Sheets):**
  - Cập nhật lại trạng thái dòng dữ liệu trên Google Sheets thành "Sent" (Đã gửi) sau khi email đã đi thành công.
- **Node `Delete Temp Slide` & `Wait 10s`:**
  - Giúp xóa các file slide nháp sinh ra trong quá trình xử lý và chờ 10 giây giữa mỗi batch để không chạm trán giới hạn API của Google.

#### 3. Kích hoạt ⚡️
- Nhấn **Test workflow** để chạy thử với một vài dòng dữ liệu mẫu.
- Kiểm tra lại kết quả trên Google Drive, Gmail và Google Sheets.
- Nếu mọi thứ mượt mà, hãy bật công tắc **Active** để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Telegram/Slack:** Thêm một node thông báo về kênh chat nội bộ (Telegram/Slack) mỗi khi hệ thống hoàn tất phát hành chứng chỉ cho toàn bộ danh sách.
- **Tạo bảng Log lỗi:** Thêm nhánh xử lý lỗi (Error Trigger) để nếu gửi mail thất bại, hệ thống sẽ ghi lại lỗi vào một tab riêng trên Google Sheets giúp dễ dàng kiểm tra lại.

### 📌 Kết luận
Quy trình thủ công rườm rà nay đã được tự động hóa hoàn toàn với n8n. Triển khai ngay workflow này để nâng tầm chuyên nghiệp cho các khóa học, sự kiện của các sếp ngay hôm nay!