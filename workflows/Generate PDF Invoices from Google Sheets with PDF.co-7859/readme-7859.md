---
title: "🚀 Tự động tạo hóa đơn PDF chuyên nghiệp từ Google Sheets với PDF.co trên n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động trích xuất dữ liệu hóa đơn từ Google Sheets và tạo file PDF chuyên nghiệp thông qua dịch vụ PDF.co chỉ trong tích tắc."
slug: "tu-dong-tao-hoa-don-pdf-tu-google-sheets-pdfco-n8n"
tags: [n8n, automation, google-sheets, pdfco, invoice, no-code]
keywords: [n8n workflow, tao hoa don pdf, google sheets pdf.co, tu dong hoa don n8n, lap hoa don tu dong]
---

# 🚀 Tự động tạo hóa đơn PDF chuyên nghiệp từ Google Sheets với PDF.co

Các sếp có đang cảm thấy mệt mỏi khi mỗi cuối tháng phải thủ công copy dữ liệu từ Google Sheets, dán vào mẫu hóa đơn rồi xuất ra file PDF để gửi cho khách hàng? Công việc lặp đi lặp lại này không chỉ tốn hàng giờ đồng hồ mà còn dễ dẫn đến sai sót nhầm lẫn số liệu.

Đừng lo, bài viết này sẽ hướng dẫn các sếp thiết lập một workflow n8n tự động hóa 100 quy trình này: hệ thống tự động đọc dữ liệu từ Google Sheets, xử lý qua Code node và kết hợp với **PDF.co** để "phù phép" ra những chiếc hóa đơn PDF đẹp mắt, chuyên nghiệp sẵn sàng gửi khách. Giải pháp được thiết kế bởi chuyên gia Robert Breen!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn cảnh làm hóa đơn thủ công từng cái một.
- **Chính xác tuyệt đối:** Lấy trực tiếp dữ liệu chuẩn từ Google Sheets, loại bỏ sai sót do đánh máy.
- **Chuyên nghiệp hóa:** Tạo ra các file PDF chuẩn chỉnh, đồng bộ thương hiệu dựa trên HTML template của PDF.co.
- **Hoạt động linh hoạt:** Dễ dàng mở rộng để gửi email tự động hoặc lưu trữ lên Google Drive/Slack ngay sau khi tạo xong.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản Google** (để kết nối Google Sheets).
- **Tài khoản PDF.co** (Đăng ký miễn phí tại [pdf.co](https://pdf.co/) để lấy API Key và tạo Template ID).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trong n8n, sau đó copy toàn bộ mã JSON của workflow này và dán trực tiếp vào giao diện n8n Editor, hoặc import file JSON tải từ kho lưu trữ n8n (ID: 7859).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 4 nodes chính, các sếp cần cấu hình kỹ các điểm sau để chạy mượt mà:

- **Node `When clicking ‘Execute workflow’` (manualTrigger):** 
  - Node khởi chạy thủ công để test dữ liệu. Các sếp có thể thay thế bằng *Schedule Trigger* (chạy định kỳ hàng ngày/hàng tuần) hoặc *Webhook* nếu muốn tự động hóa hoàn toàn.
- **Node `Get Invoice Rows` (googleSheets):**
  - **Credentials:** Kết nối tài khoản Google Sheets của các sếp bằng OAuth2.
  - **Tham số:** Chọn bản sao của [Invoice Template Sheet](https://docs.google.com/spreadsheets/d/1a6QBIQkr7RsZtUZBi87NwhwgTbnr5hQl4J_ZOkr3F1U/edit?usp=drivesdk) vào Drive cá nhân, sau đó chọn đúng **Spreadsheet ID** và **Worksheet** (ví dụ: `Sheet1`).
- **Node `Convert to html import` (code):**
  - Node này nhận dữ liệu dòng từ Google Sheets và xử lý định dạng chuẩn bị đổ vào mẫu HTML. Các sếp có thể tùy chỉnh code JavaScript bên trong nếu muốn thay đổi cách hiển thị dữ liệu (định dạng tiền tệ, ngày tháng...).
- **Node `Create PDF` (n8n-nodes-pdfco.PDFco Api):**
  - **Operation:** Chọn `URL/HTML to PDF` (hoặc `HTML Template to PDF`).
  - **Credentials:** Nhập **PDF.co API Key** đã lấy từ dashboard của PDF.co.
  - **Tham số:** Điền `Template ID` mà các sếp đã thiết lập sẵn trong trang quản trị PDF.co vào cấu hình của node.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** ở node trigger để chạy thử nghiệm xem hệ thống đã xuất ra file PDF thành công chưa.
- Kiểm tra kết quả trả về, nếu mọi thứ xanh mướt (success), hãy gạt công tắc **Active** ở góc trên bên phải để bật workflow chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
Để hệ thống tự động hóa đạt hiệu quả tối đa, các sếp có thể mở rộng workflow này bằng cách:
1. **Gửi email tự động:** Thêm node *Gmail* hoặc *SendGrid* ngay sau node PDF.co để tự động gửi hóa đơn trực tiếp cho khách hàng.
2. **Lưu trữ file:** Thêm node *Google Drive* hoặc *Dropbox* để lưu bản sao lưu (backup) của tất cả hóa đơn đã tạo.
3. **Thông báo nội bộ:** Thêm node *Slack* hoặc *Telegram* để bắn một thông báo kèm link file PDF về nhóm kế toán mỗi khi có hóa đơn mới được tạo thành công.

### 📌 Kết luận
Việc tự động hóa tạo hóa đơn PDF từ Google Sheets với PDF.co và n8n là một bước tiến lớn giúp tối ưu hóa quy trình vận hành tài chính cho doanh nghiệp nhỏ và các freelancer. Hãy áp dụng ngay hôm nay để giải phóng sức lao động và nâng tầm chuyên nghiệp cho doanh nghiệp của các sếp!