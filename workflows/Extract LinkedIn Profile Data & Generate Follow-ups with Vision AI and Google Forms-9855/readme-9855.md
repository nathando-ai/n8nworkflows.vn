---
title: "🚀 Tự động trích xuất thông tin LinkedIn & Viết tin nhắn Follow-up bằng Vision AI và Google Forms"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình phân tích ảnh chụp màn hình profile LinkedIn bằng AI, trích xuất dữ liệu và soạn tin nhắn chăm sóc khách hàng cá nhân hóa."
slug: "tu-dong-trich-xuat-linkedin-vision-ai-google-forms"
tags: [n8n, automation, openai, google-sheets, google-drive, crm]
keywords: [n8n workflow, linkedin automation, vision ai, openai, google forms, chăm sóc khách hàng]
---

# 🚀 Tự động trích xuất thông tin LinkedIn & Viết tin nhắn Follow-up bằng Vision AI và Google Forms

Việc nghiên cứu profile LinkedIn của khách hàng tiềm năng, trích xuất thông tin thủ công và ngồi nghĩ ra một tin nhắn follow-up phù hợp, tự nhiên luôn ngốn rất nhiều thời gian của đội ngũ Sales và tuyển dụng. 

Workflow n8n này sinh ra để giải quyết triệt để nỗi đau đó! Các sếp chỉ cần upload ảnh chụp màn hình profile LinkedIn kèm ghi chú nhanh vào Google Form, phần còn lại hãy để AI lo: từ việc "nhìn" ảnh trích xuất dữ liệu, cấu trúc thông tin, cập nhật CRM cho đến việc tự động soạn sẵn một tin nhắn kết nối/chăm sóc siêu cá nhân hóa.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Bỏ hoàn toàn thao tác copy-paste thông tin profile thủ công từ LinkedIn sang Google Sheets/CRM.
- **Sức mạnh Vision AI:** Khả năng đọc hiểu ảnh chụp màn hình profile đỉnh cao từ OpenAI, lấy chính xác chức danh, công ty, kỹ năng...
- **Cá nhân hóa đỉnh cao:** Tạo ra các tin nhắn follow-up dựa trên đúng ngữ cảnh profile và ghi chú thực tế của các sếp.
- **Lưu trữ đồng bộ:** Tự động cập nhật toàn bộ thông tin và nội dung tin nhắn vào Google Sheets ngay khi có Form phản hồi mới.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Google Account:** 
  - Google Forms & Google Sheets (chứa form phản hồi và lưu database).
  - Google Drive (lưu trữ ảnh chụp màn hình LinkedIn tải lên từ form).
- **OpenAI API Key:** Tài khoản OpenAI có quyền sử dụng Vision Model (như GPT-4o) để phân tích ảnh và sinh văn bản.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này hoặc tải file từ nguồn cung cấp, sau đó paste trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp cần cấu hình chính xác các node sau:

- **Node `trigger: form submission` (Google Sheets Trigger):** 
  - Kết nối tài khoản Google của các sếp.
  - Chọn đúng file Google Sheet được liên kết với Google Form (Form này nhận 2 trường dữ liệu chính: ảnh chụp màn hình LinkedIn và ghi chú cá nhân).
- **Node `get screenshot` (Google Drive):**
  - Cấu hình thao tác `Download` file ảnh từ đường dẫn mà Google Form đẩy lên Google Drive.
- **Node `Analyze image` (OpenAI Vision):**
  - Chọn credentials OpenAI.
  - Thiết lập resource là `Image` và operation là `Analyze`, đưa prompt hướng dẫn AI trích xuất các thông tin quan trọng từ ảnh profile LinkedIn (Họ tên, vị trí, công ty, kinh nghiệm...).
- **Node `structure info` (Code):**
  - Node này dùng đoạn mã Javascript nhỏ để làm sạch và định dạng lại dữ liệu thô mà OpenAI Vision vừa trả về thành dạng cấu trúc gọn gàng.
- **Node `update crm` (Google Sheets):**
  - Cấu hình operation `Append or Update` để lưu thông tin đã trích xuất của khách hàng vào bảng Google Sheets quản lý CRM.
- **Node `Message a model` (OpenAI):**
  - Dùng OpenAI để viết tin nhắn follow-up dựa trên dữ liệu profile đã cấu trúc kết hợp với ghi chú ban đầu của các sếp.
- **Node `update crm with message` (Google Sheets):**
  - Cập nhật tiếp nội dung tin nhắn vừa được AI sinh ra vào đúng dòng tương ứng trong Google Sheets.

#### 3. Kích hoạt ⚡️
- Bấm nút **Execute Workflow** và test thử bằng cách điền một phản hồi mới trên Google Form.
- Kiểm tra kết quả trên Google Sheets xem dữ liệu và tin nhắn đã hiển thị đầy đủ chưa.
- Gạt công tắc sang **Active** để bật chế độ chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh chat:** Thay vì chỉ lưu vào Google Sheets, các sếp có thể nối thêm node Telegram hoặc Slack để bot bắn thẳng tin nhắn follow-up vừa tạo về máy, giúp các sếp duyệt và gửi ngay lập tức.
- **Đa dạng hóa mẫu tin nhắn:** Tùy biến prompt trong node OpenAI để tạo ra nhiều phong cách tin nhắn khác nhau (trang trọng, thân thiện, hài hước) tùy thuộc vào đối tượng khách hàng.
- **Lưu log lỗi:** Thêm nhánh xử lý lỗi (Error Trigger) để cảnh báo qua email nếu quá trình gọi API OpenAI gặp sự cố.

### 📌 Kết luận
Workflow này là trợ thủ đắc lực giúp tối ưu hóa quy trình sales-prospecting và networking trên LinkedIn. Hãy cài đặt ngay hôm nay để tiết kiệm hàng chục giờ làm việc thủ công mỗi tuần!