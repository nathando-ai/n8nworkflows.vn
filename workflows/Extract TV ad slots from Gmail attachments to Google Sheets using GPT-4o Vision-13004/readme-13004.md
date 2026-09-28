---
title: "🚀 Trích xuất thông tin lịch chiếu TV & tài liệu từ Gmail vào Google Sheets tự động bằng GPT-4o Vision"
description: "Hướng dẫn xây dựng workflow n8n tự động giám sát Gmail, phân tích file đính kèm (Excel, PDF, PPTX, hình ảnh) bằng GPT-4o Vision và lưu trữ cấu trúc vào Google Sheets."
slug: "trich-xuat-thong-tin-tv-ad-slots-tu-gmail-bang-gpt-4o-vision"
tags: [n8n, automation, gpt-4o-vision, google-sheets, gmail, ai-extraction]
keywords: [n8n workflow, trích xuất dữ liệu gmail, gpt-4o vision n8n, tự động hóa google sheets, ai document processing]
---

# 🚀 Trích xuất thông tin lịch chiếu TV & tài liệu từ Gmail vào Google Sheets tự động bằng GPT-4o Vision

Các sếp có đang đau đầu mỗi khi nhận hàng tá email từ các đối tác chứa lịch phát sóng quảng cáo TV (TV ad slots), báo cáo chiến dịch dưới dạng file Excel, PDF, PowerPoint hay hình ảnh không? Việc tải xuống thủ công, đọc hiểu từng file rồi nhập liệu vào Google Sheets không chỉ tốn hàng giờ đồng hồ mà còn cực kỳ dễ nhầm lẫn.

Giải pháp ở đây là gì? Workflow n8n siêu cấp này sẽ thay các sếp làm toàn bộ từ A-Z: tự động quét Gmail, phân loại email, trích xuất dữ liệu thông minh bằng AI (GPT-4o Vision), đẩy thẳng kết quả có cấu trúc vào Google Sheets và tự động gắn nhãn (Label) quản lý email gọn gàng!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [An tâm chạy ngầm với VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Không cần động tay vào việc đọc email hay tải file đính kèm nữa.
- **Xử lý đa định dạng thông minh:** Cân mọi thể loại file từ Excel, PDF, PPTX cho tới hình ảnh hoặc nội dung text thông thường nhờ sức mạnh của GPT-4o Vision.
- **Đồng bộ hóa dữ liệu chuẩn xác:** Thông tin ngày giờ, tên chương trình, chi phí được bóc tách và lưu thẳng vào Google Sheets theo schema định sẵn.
- **Quản lý khoa học:** Tự động tạo và gắn nhãn (Label) phân loại email trong Gmail sau khi xử lý xong, tránh sót việc hoặc xử lý trùng lặp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động trơn tru, các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- **Gmail OAuth2:** Để đọc email và quản lý label.
- **OpenAI API Key:** Sử dụng mô hình GPT-4 Vision phân tích hình ảnh và tài liệu.
- **Google Sheets OAuth2:** Lưu trữ dữ liệu trích xuất.
- **AWS S3 Bucket:** Lưu trữ tạm thời các file hình ảnh/tài liệu phục vụ cho GPT Vision API.
- **ConvertAPI Account:** Dùng để chuyển đổi file PPTX/PDF sang định dạng hình ảnh (PNG) trước khi đưa vào AI phân tích.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này từ kho lưu trữ n8n (Link gốc: [Extract TV ad slots from Gmail attachments](https://n8n.io/workflows/13004)) và import trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import 40 nodes, các sếp cần chú ý cấu hình các điểm sau:
- **Schedule Trigger:** Thiết lập chu kỳ thời gian kiểm tra Gmail (ví dụ: chạy mỗi 30 phút hoặc 1 tiếng).
- **Domain Filter & Code Nodes:** Tùy chỉnh các từ khóa và tên miền đối tác trong các node code để hệ thống nhận diện đúng phân loại email (Category A, B, C...).
- **ConvertAPI (node HTTP Request):** Thay thế thông tin xác thực HTTP Header Auth bằng ConvertAPI Secret của sếp.
- **S3 Upload (PPTX & Image):** Kết nối tài khoản AWS S3 và cấu hình biến môi trường chứa tên Bucket.
- **Save to Google Sheets:** Kết nối tài khoản Google và điền `GOOGLE_SHEET_ID` chính xác vào node này (hoặc cấu hình trong phần Variables của n8n).
- **Parse All Results:** Tùy chỉnh lại cấu trúc schema dữ liệu đầu ra sao cho khớp với các cột trên Google Sheets của các sếp (Ví dụ: `email_type`, `date`, `time`, `name`, `amount`...).

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) bằng một email mẫu có chứa file đính kèm để kiểm tra luồng chạy qua các nhánh IF, ConvertAPI, S3 và GPT Vision.
- Kiểm tra xem dữ liệu đã được đẩy chuẩn vào Google Sheets chưa.
- Bật công tắc **Active** để workflow tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Slack/Telegram:** Thêm node gửi thông báo về kênh chat nội dung mỗi khi có một lịch quảng cáo TV mới được trích xuất và lưu thành công.
- **Tự động xóa file rác trên S3:** Sau khi GPT-4o Vision đã phân tích xong, có thể bổ sung một bước xóa file tạm trên AWS S3 để tiết kiệm dung lượng lưu trữ.
- **Mở rộng schema:** Tùy biến prompt trong các node gọi GPT để trích xuất thêm nhiều trường thông tin chuyên sâu khác phục vụ cho bộ phận kế toán hoặc vận hành.

### 📌 Kết luận
Với workflow n8n kết hợp GPT-4o Vision này, việc xử lý hàng loạt tài liệu và lịch quảng cáo từ email không còn là gánh nặng thủ công nữa. Triển khai ngay hôm nay để tối ưu hóa năng suất cho đội ngũ của các sếp!