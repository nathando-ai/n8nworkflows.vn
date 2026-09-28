---
title: "🚀 Tự động trích xuất danh thiếp (Business Card) vào Google Sheets bằng AI GPT-4o trong n8n"
description: "Biến ảnh chụp danh thiếp thành dữ liệu khách hàng gọn gàng trên Google Sheets tự động 100% nhờ AI GPT-4o và n8n. Không cần gõ tay, loại bỏ sai sót."
slug: "trich-xuat-danh-thiep-google-sheets-gpt4o"
tags: [n8n, automation, ai, gpt-4o, google-sheets, lead-generation]
keywords: [n8n workflow, trích xuất danh thiếp, business card scanner AI, gpt-4o n8n, tự động hóa google sheets]
---

# 🚀 Tự động trích xuất danh thiếp vào Google Sheets với GPT-4o & n8n

Các sếp đi sự kiện, hội thảo về với mộtấp danh thiếp (business card) dày cộp và mất cả ngày để ngồi gõ lại thông tin thủ công vào Excel hoặc CRM? Việc này vừa nhàm chán, tẻ nhạt lại cực kỳ dễ sai sót. 

Đừng lo, bài toán này sẽ được giải quyết triệt để với workflow n8n cực kỳ thông minh do chuyên gia **Trung Tran** thiết kế. Workflow này sẽ tự động hóa từ khâu nhận ảnh chụp danh thiếp qua web form, quét thông tin bằng AI OCR (GPT-4o), làm sạch dữ liệu và lưu thẳng vào Google Sheets. Các sếp chỉ việc "upload và đi chơi"!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, xử lý các tệp ảnh mượt mà, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn cảnh cặm cụi gõ từng số điện thoại, email từ danh thiếp giấy.
- **Độ chính xác cao:** Ứng dụng sức mạnh thị giác máy tính của AI GPT-4o để đọc chuẩn xác thông tin ngay cả trên thiết kế phức tạp.
- **Lưu trữ tập trung:** Toàn bộ dữ liệu khách hàng được đẩy ngay vào Google Sheets, sẵn sàng cho các chiến dịch chăm sóc tiếp theo.
- **Hoạt động tự động 24/7:** Giao diện Form gọn gàng, có thể dùng trực tiếp trên điện thoại di động ngay tại sự kiện.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để vận hành trơn tru, các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **n8n Instance:** Đã kích hoạt môi trường n8n.
- **OpenAI API Key:** Có tích hợp model `gpt-4o` (hỗ trợ đọc hình ảnh đa phương thức - Multimodal AI).
- **Google Drive Account:** Nơi lưu trữ hình ảnh danh thiếp tải lên để tra cứu sau này.
- **Google Sheets Account:** Tạo sẵn 1 file Sheet để hứng dữ liệu contact (Tên, Số điện thoại, Email, Công ty...).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow hoặc tải file JSON từ link gốc, sau đó vào giao diện n8n chọn **Add workflow** -> **Import from File / Clipboard** và dán vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, hãy cấu hình các node cốt lõi sau đây:
- **On form submission**: Cấu hình form tải ảnh lên (định dạng JPG/PNG). Đặt tiêu đề thân thiện như *"Name Card Uploader"* để đội ngũ kinh doanh dễ sử dụng.
- **Upload file (Google Drive)**: Chọn tài khoản Google Drive credentials và trỏ tới thư mục (Folder ID) cụ thể để lưu trữ ảnh danh thiếp.
- **GPT4o & Neural assistant for contact extraction**: Cấu hình credentials cho OpenAI và chắc chắn model được chọn là `gpt-4o`. Node này sẽ dùng OCR để bóc tách tên, SĐT, email, chức vụ thành dạng JSON cấu trúc.
- **Structured Output Parser**: Định nghĩa rõ cấu trúc JSON đầu ra (Name, Phone, Email, Company, Position...) để AI trả về đúng định dạng chuẩn.
- **Transform Output (Code Node)**: Node này giúp làm sạch dữ liệu, ví dụ tự động lọc bỏ các ký tự thừa (như dấu `+` trong số điện thoại nếu cần) hoặc chuẩn hóa định dạng.
- **Filter bad data**: Lọc bỏ các bản ghi lỗi hoặc ảnh tải lên không chứa danh thiếp hợp lệ trước khi đẩy vào database.
- **Add contact to tracking sheet (Google Sheets)**: Kết nối tài khoản Google Sheets của các sếp, chọn đúng Spreadsheet và Worksheet, sau đó map các trường dữ liệu từ AI vào các cột tương ứng (Tên, Email, SĐT...).

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và test thử bằng cách upload một vài tấm ảnh danh thiếp mẫu qua Form.
- Kiểm tra kết quả trên Google Sheets xem dữ liệu đã được bóc tách và điền đúng cột hay chưa.
- Nếu mọi thứ mượt mà, gạt công tắc sang **Active** để bật chế độ chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
Để hệ thống thông minh hơn nữa, các sếp có thể mở rộng workflow với các ý tưởng sau:
- **Đồng bộ CRM:** Thay vì chỉ ghi vào Google Sheets, hãy nối thêm node đẩy dữ liệu trực tiếp sang HubSpot, Salesforce hoặc Zoho CRM.
- **Báo cáo thời gian thực:** Thêm node gửi thông báo qua **Slack** hoặc **Telegram** mỗi khi có danh thiếp mới được quét thành công kèm thông tin tóm tắt.
- **Xử lý hàng loạt:** Cho phép upload nhiều ảnh danh thiếp cùng một lúc trong một lần submit form để tối ưu tốc độ cho team Sales.

### 📌 Kết luận
Việc số hóa danh thiếp chưa bao giờ dễ dàng và chuyên nghiệp đến thế. Chỉ với một vài bước cài đặt đơn giản cùng sức mạnh của AI GPT-4o trong n8n, các sếp đã có ngay một trợ lý ảo đắc lực giúp tối ưu quy trình Lead Generation. Triển khai ngay thôi nào!