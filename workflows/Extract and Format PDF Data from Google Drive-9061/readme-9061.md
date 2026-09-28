---
title: "🚀 Tự động trích xuất và làm sạch dữ liệu PDF từ Google Drive với n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động tìm kiếm, tải xuống, trích xuất văn bản từ file PDF trên Google Drive và làm sạch dữ liệu bằng JavaScript."
slug: "trich-xuat-va-lam-sach-du-lieu-pdf-tu-google-drive-voi-n8n"
tags: [n8n, automation, google-drive, pdf-extraction, javascript]
keywords: [n8n workflow, trích xuất pdf google drive, tự động hóa n8n, parse pdf n8n, code node n8n]
---

# 🚀 Tự động trích xuất và làm sạch dữ liệu PDF từ Google Drive

Các sếp có thường xuyên phải đối mặt với hàng đống tài liệu, hóa đơn hay báo cáo dạng PDF nằm rải rác trên Google Drive? Việc mở từng file, copy nội dung thủ công rồi chỉnh sửa lại định dạng chắc chắn ngốn rất nhiều thời gian và cực kỳ nhàm chán. 

Đừng lo, bài viết này sẽ hướng dẫn các sếp thiết lập một workflow n8n tự động hóa 100% giúp tìm kiếm, tải về, trích xuất toàn bộ văn bản từ file PDF và làm sạch dữ liệu theo ý muốn chỉ trong một nốt nhạc!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Tự động quét và xử lý tất cả file `.pdf` trong một thư mục chỉ định trên Google Drive.
- **Trích xuất thông minh:** Đọc và bóc tách toàn bộ dữ liệu văn bản thô từ file PDF mà không cần copy thủ công.
- **Tùy biến linh hoạt:** Sử dụng Code Node (JavaScript) để làm sạch khoảng trắng, xóa dòng thừa hoặc tái cấu trúc dữ liệu thành JSON chuẩn chỉnh.
- **Tiết kiệm thời gian tối đa:** Vận hành nhanh chóng, sẵn sàng kết nối tiếp với các hệ thống CRM, Database hoặc AI LLM.
:::

### Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản **n8n** (Cloud hoặc Self-hosted).
- Tài khoản **Google Drive** để lưu trữ và quản lý file PDF.
:::

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể sử dụng mã JSON của workflow (từ nguồn ID: `9061` do tác giả *EoCi - Mr.Eo* phát triển) và tiến hành import trực tiếp vào giao diện n8n Editor của mình. Workflow bao gồm 7 nodes chính: *Start (Manual Trigger)*, *Get PDF Files/File*, *Get PDF Data Only*, *Download Retrieval Files/File*, *Extract Files/File's Data*, *Data Parser & Cleaner (Code)* và *Done! (NoOp)*.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Chuẩn bị Google Drive:** Tạo một thư mục riêng biệt trên Google Drive (ví dụ: *"PDFs for n8n"*) và tải lên một vài file PDF mẫu để test.
- **Cấu hình Google Drive Credentials:** 
  - Click vào node **Get PDF Files/File**. Tại mục *Credential*, chọn *Create New*, điền Client ID và Client Secret từ Google Cloud Console, sau đó thực hiện cấp quyền đăng nhập tài khoản Google.
  - Sử dụng chung credential này cho node **Download Retrieval Files/File**.
- **Cấu hình node Get PDF Files/File:** 
  - Đảm bảo *Operation* là `Search`.
  - Mục *Search Query* điền `*.pdf`.
  - Thêm Filter chọn thư mục Google Drive mà các sếp vừa tạo ở bước chuẩn bị.
- **Cấu hình node Download Retrieval Files/File:** Đảm bảo *Operation* là `Download` và trường *File ID* đã được gán sẵn biểu thức động `{{ $json.id }}`.
- **Cấu hình node Data Parser & Cleaner (Code):** Mở trình soạn thảo JavaScript, tùy chỉnh đoạn code để làm sạch dữ liệu đầu vào (`items[0].json.text`) theo định dạng mà sếp mong muốn (cắt khoảng trắng, dùng Regex lọc thông tin...).

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** ở góc trên cùng để chạy thử với dữ liệu mẫu. Kiểm tra từng node xem đã hiện dấu tích xanh chưa.
- Kiểm tra kết quả đầu ra tại node cuối cùng (**Done !**).
- Sau khi mọi thứ chạy mượt mà, gạt công tắc sang chế độ **Active** để hoàn tất.

---

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp AI (LLM):** Nối tiếp đầu ra của node *Data Parser & Cleaner* vào các node OpenAI / Anthropic để tóm tắt văn bản, phân tích hóa đơn hoặc trích xuất thông tin có cấu trúc (Entity Extraction).
- **Lưu trữ dữ liệu:** Đẩy dữ liệu sau khi làm sạch vào Google Sheets, Notion hoặc Airtable để dễ dàng quản lý.
- **Gửi thông báo:** Thêm node Telegram hoặc Slack để nhận thông báo ngay khi workflow xử lý xong một tài liệu PDF mới.

### 📌 Kết luận
Với workflow n8n cực kỳ gọn gàng và mạnh mẽ này, việc xử lý tài liệu PDF không còn là cơn ác mộng thủ công. Hãy áp dụng ngay vào hệ thống của các sếp để tối ưu hóa năng suất làm việc!