---
title: "🚀 Tự động trích xuất y lệnh bác sĩ từ tài liệu vào Google Sheets với VLM Run AI"
description: "Hướng dẫn tự động hóa quy trình đọc đơn thuốc, y lệnh y tế từ Google Drive, trích xuất dữ liệu thông minh bằng VLM Run AI và lưu trữ vào Google Sheets."
slug: "trich-xuat-y-lenh-bac-si-voi-vlm-run-ai-google-sheets"
tags: [n8n, automation, no-code, ai-summarization, multimodal-ai, google-workspace]
keywords: [n8n workflow, tự động hóa y lệnh, vlm run ai, google drive trigger, google sheets automation]
---

# 🚀 Tự động trích xuất y lệnh bác sĩ từ tài liệu vào Google Sheets với VLM Run AI

Các cơ sở y tế, phòng khám hay đơn vị cung cấp thiết bị y tế (DME) thường xuyên phải đối mặt với núi tài liệu thủ công: đơn thuốc, y lệnh bác sĩ, phiếu yêu cầu bảo hiểm dưới dạng ảnh chụp, PDF hoặc tài liệu quét. Việc nhập liệu thủ công không chỉ tốn hàng giờ đồng hồ mà còn dễ xảy ra sai sót, ảnh hưởng đến tiến độ xử lý đơn hàng và tuân thủ pháp lý.

Giải pháp? Workflow n8n này sẽ tự động hóa 100% quy trình: Phát hiện tài liệu mới trên Google Drive 👉 Tải xuống 👉 Đọc và bóc tách dữ liệu thông minh bằng **VLM Run AI** 👉 Lưu trữ gọn gàng vào **Google Sheets**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Không cần thao tác thủ công, cứ có tài liệu mới lên Drive là hệ thống tự chạy.
- **Trích xuất thông minh:** Biến các form y tế phức tạp, chữ viết tay hoặc bản scan thành dữ liệu JSON cấu trúc rõ ràng.
- **Quản lý tập trung:** Toàn bộ thông tin bệnh nhân, mã HCPCS, bác sĩ chỉ định... được cập nhật thẳng vào Google Sheets theo thời gian thực.
- **Tối ưu vận hành:** Phù hợp tuyệt vời cho đơn hàng Thiết bị Y tế Bền vững (DME), đơn thuốc, và quy trình bảo hiểm y tế.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n (Self-hosted hoặc Cloud).
- Tài khoản Google Drive & Google Sheets (Kết nối qua OAuth2).
- VLM Run API Key (Truy cập từ nền tảng VLM Run).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể copy mã JSON của workflow hoặc import trực tiếp file template vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động trơn tru, các sếp cần cấu hình chính xác 4 nodes quan trọng sau:

- **Google Drive Trigger:** 
  - Chọn tài khoản Google Drive (OAuth2).
  - Chỉ định thư mục (`Folder`) cụ thể trên Google Drive cần theo dõi. Khi có file mới (PDF, ảnh JPG/PNG, tài liệu scan) được tải lên thư mục này, workflow sẽ tự động kích hoạt.
- **Download file:** 
  - Liên kết với node Trigger phía trên để lấy ID file vừa tải lên và tiến hành tải nội dung file về bộ nhớ tạm của n8n.
- **VLM Run:** 
  - Cấu hình thông tin API Key của VLM Run.
  - Sử dụng danh mục (category) chuẩn `healthcare.physician-orders` để AI hiểu và bóc tách chính xác các thông tin quan trọng như:
    - Thông tin bệnh nhân: Tên, ngày sinh (DOB), mã Medicaid ID.
    - Chi tiết y lệnh: Mã HCPCS, số lượng, đơn giá, cờ phê duyệt.
    - Thông tin bác sĩ: Tên bác sĩ, số NPI, ngày ký.
- **Append row in sheet:** 
  - Chọn tài khoản Google Sheets và file Google Sheet đích.
  - Ánh xạ (Map) các trường dữ liệu JSON đã được VLM Run AI trích xuất vào đúng các cột trong Sheet (Ví dụ: Bệnh nhân, Ngày sinh, Mã HCPCS, Mô tả sản phẩm, Số lượng, Giá, Chẩn đoán, Bác sĩ, Ngày).

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và tải thử một file y lệnh mẫu lên thư mục Google Drive để kiểm tra dữ liệu trả về trong Google Sheets.
- Sau khi test ngon lành, gạt công tắc sang **Active** để hệ thống tự động chạy 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Thêm node Telegram hoặc Slack ở cuối workflow để bắn thông báo ngay về điện thoại cho đội ngũ vận hành mỗi khi có y lệnh mới được xử lý thành công.
- **Phân loại file lỗi:** Thêm nhánh `If` để kiểm tra nếu file tải lên không đúng định dạng hoặc AI không đọc được, tự động chuyển vào thư mục "Cần xem lại" trên Drive.
- **Sao lưu dữ liệu:** Kết hợp thêm các bước gửi email tự động xác nhận hoặc lưu trữ bản ghi vào cơ sở dữ liệu phụ.

### 📌 Kết luận
Việc tự động hóa trích xuất y lệnh với VLM Run AI và n8n giúp tiết kiệm hàng chục giờ nhập liệu thủ công mỗi tuần, loại bỏ sai sót và tăng tốc độ xử lý đơn hàng y tế. Lên đồ ngay thôi các sếp ơi!