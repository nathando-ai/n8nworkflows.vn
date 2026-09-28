---
title: "🚀 Tự động lọc và lưu trữ Feedback từ Typeform vào Google Sheets bằng n8n"
description: "Hướng dẫn chi tiết xây dựng workflow n8n tự động bắt sự kiện từ Typeform, lọc nội dung thông minh và phân loại lưu trữ vào Google Sheets giúp tối ưu hóa quy trình Product, Marketing và Sales."
slug: "tu-dong-loc-va-luu-tru-feedback-typeform-google-sheets-n8n"
tags: [n8n, automation, no-code, typeform, google-sheets, marketing, product, sales]
keywords: [n8n workflow, tự động hóa typeform, lưu feedback google sheets, n8n typeform trigger, lọc dữ liệu n8n]
---

# 🚀 Tự động hóa quy trình thu thập và phân loại Feedback từ Typeform

Các sếp có đang gặp tình trạng mỗi khi có khách hàng điền form khảo sát trên Typeform, đội ngũ Sales, Product hay Marketing lại phải thủ công copy/paste dữ liệu, lọc xem feedback nào tích cực, feedback nào tiêu cực rồi phân bổ vào các file báo cáo khác nhau? Việc làm thủ công này không chỉ tốn thời gian, dễ bỏ sót khách hàng tiềm năng mà còn làm chậm trễ phản ứng của doanh nghiệp.

Giải pháp ở đây là gì? Hãy để n8n lo! Workflow **"Filter the feedback from Typeform and store in Google Sheets"** do tác giả *Lorena* thiết kế sẽ giúp các sếp tự động hóa 100% quy trình này: Lắng nghe phản hồi từ Typeform ngay lập tức, lọc dữ liệu theo điều kiện thông minh và tự động ghi nhận vào các Google Sheets tương ứng mà không cần chạm tay vào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Nhận dữ liệu real-time từ Typeform ngay khi khách hàng bấm nút Submit.
- **Phân loại thông minh:** Sử dụng điều kiện (IF node) để phân tách các loại feedback (ví dụ: đánh giá tốt cho vào một bảng, đánh giá cần cải thiện xử lý riêng).
- **Lưu trữ khoa học:** Tự động append (thêm dòng) vào Google Sheets đúng danh mục mà không sợ loạn data.
- **Tiết kiệm thời gian:** Giải phóng đội ngũ vận hành khỏi các tác vụ thủ công lặp đi lặp lại.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản Typeform** đã tạo sẵn ít nhất một Form thu thập phản hồi.
- **Tài khoản Google Drive / Google Sheets** với các file Google Sheets đã được định dạng sẵn cột nhận dữ liệu.
- **Credentials** kết nối Typeform API và Google Sheets OAuth2 API trên n8n.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải mã JSON của workflow từ [n8n Template gốc](https://n8n.io/workflows/1075), sau đó copy đoạn JSON đó và dán trực tiếp vào màn hình n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node sau:

- **Typeform Trigger:** 
  - Chọn Credentials Typeform của các sếp.
  - Chọn đúng Form cần lắng nghe sự kiện submit trong danh sách Form có sẵn của tài khoản Typeform.
- **IF Node:** 
  - Thiết lập điều kiện lọc (ví dụ: điểm số đánh giá từ form > 4, hoặc theo từ khóa trong câu trả lời). Node này sẽ chia dòng dữ liệu thành 2 nhánh: thỏa mãn điều kiện (`true`) và không thỏa mãn (`false`).
- **Set Node:** 
  - Dùng để biến đổi, chuẩn hóa lại cấu trúc dữ liệu hoặc trích xuất các trường thông tin cần thiết trước khi đẩy vào Google Sheets.
- **Google Sheets & Google Sheets1:** 
  - Kết nối tài khoản Google Sheets OAuth2 API.
  - Chọn đúng File Spreadsheet ID và Sheet Name (Tên tab) tương ứng cho từng nhánh dữ liệu (ví dụ: Nhánh 1 lưu feedback tích cực, nhánh 2 lưu feedback cần cải thiện).
  - Đảm bảo mapping đúng các cột (Columns) giữa dữ liệu từ Typeform với các tiêu đề cột trên Google Sheets.

#### 3. Kích hoạt ⚡️
- Bấm nút **Execute Workflow** và thử điền một bản nháp trên Typeform để test dữ liệu chạy qua các node.
- Kiểm tra lại Google Sheets xem dữ liệu đã được ghi nhận chính xác chưa.
- Nếu mọi thứ xanh mướt, hãy bật công tắc **Active** góc trên bên phải để workflow chính thức trực chiến 24/7.

### ✍️ Mẹo & gợi ý nâng cao
Để hệ thống xịn sò hơn nữa, các sếp có thể mở rộng workflow này bằng cách:
- **Tích hợp thông báo:** Thêm node Telegram hoặc Slack ở mỗi nhánh để ngay khi có feedback (đặc biệt là feedback tiêu cực/khẩn cấp), đội ngũ CSKH hoặc Product nhận được thông báo ngay lập tức.
- **Gửi email cảm ơn tự động:** Kết hợp thêm node Gmail hoặc SendGrid để gửi voucher/lời cảm ơn tự động đến khách hàng vừa điền form.
- **Lưu log lỗi:** Thiết lập Error Trigger để bắt các lỗi phát sinh (như mất kết nối Google Sheets) và gửi cảnh báo về Telegram cá nhân của sếp.

### 📌 Kết luận
Workflow **Filter the feedback from Typeform and store in Google Sheets** là một mẩu "LEGO" tự động hóa cực kỳ cơ bản nhưng mang lại giá trị thực chiến cao cho mọi doanh nghiệp số. Hãy cài đặt ngay để tối ưu hóa quy trình quản trị trải nghiệm khách hàng của các sếp từ hôm nay!