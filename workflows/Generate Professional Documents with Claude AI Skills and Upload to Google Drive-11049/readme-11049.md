---
title: "🚀 Tự động tạo tài liệu chuyên nghiệp (PDF, DOCX, XLSX, PPTX) bằng Claude AI và Google Drive trong n8n"
description: "Hướng dẫn xây dựng hệ thống tự động hóa tạo tài liệu chuyên nghiệp đa định dạng bằng Claude AI Skills và tự động lưu trữ lên Google Drive thông qua n8n."
slug: "tu-dong-tao-tai-lieu-claude-ai-google-drive-n8n"
tags: [n8n, automation, no-code, claude-ai, google-drive, document-automation]
keywords: [n8n workflow, Claude AI skills, tự động tạo tài liệu, Google Drive automation, n8n document generation]
---

# 🚀 Tự động tạo tài liệu chuyên nghiệp (PDF, DOCX, XLSX, PPTX) bằng Claude AI và Google Drive

Chào các sếp! Việc soạn thảo các tài liệu, báo cáo, bảng tính hay slide thuyết trình thủ công thường ngốn rất nhiều thời gian và công sức của đội ngũ nhân sự. Thay vì làm thủ công từng file, tại sao chúng ta không tự động hóa hoàn toàn quy trình này?

Bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ mạnh mẽ do chuyên gia Davide xây dựng. Workflow này sẽ tiếp nhận yêu cầu từ người dùng qua Form, sử dụng sức mạnh của **Anthropic Claude AI (với tính năng Agent Skills)** để tạo ra các định dạng file chuyên nghiệp (PDF, Word, Excel, PowerPoint), sau đó tự động tải về và lưu trữ gọn gàng lên **Google Drive**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Biến một ý tưởng/prompt thô thành tài liệu hoàn chỉnh (PDF, DOCX, XLSX, PPTX) chỉ bằng vài cú click.
- **Đa dạng định dạng:** Hỗ trợ mọi loại tài liệu văn phòng phổ biến mà không cần cài đặt phần mềm phức tạp trên máy tính.
- **Lưu trữ thông minh:** File được tạo xong sẽ tự động phân loại và lưu thẳng vào Google Drive cá nhân hoặc doanh nghiệp.
- **Tiết kiệm thời gian:** Giảm thiểu 90% thời gian thiết kế slide, định dạng báo cáo hay bảng tính cho đội ngũ marketing và sales.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Anthropic API Key** (tài khoản Anthropic có bật tính năng Claude API / Agent Skills).
- **Tài khoản Google Drive** để cấp quyền kết nối (OAuth2).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ thư viện n8n (ID: `11049`) hoặc copy trực tiếp mã JSON và paste vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 19 nodes được thiết kế mạch lạc. Các sếp cần chú ý cấu hình các điểm mấu chốt sau:

- **Node `Get All Skills` & Các node tạo file (`Create PDF`, `Create DOCX`, `Create XLSX`, `Create PPTX`):**
  - Đây là các node gọi **Anthropic API** (kiểu `httpRequest`).
  - Các sếp cần cấu hình **Credential** kiểu `httpHeaderAuth` với thông tin:
    - Name: `x-api-key`
    - Value: `YOUR_ANTHROPIC_API_KEY` (Điền API Key thực tế của các sếp từ Anthropic).
- **Node `Switch`:**
  - Định tuyến yêu cầu dựa trên định dạng file mà người dùng chọn trên Form (Excel, Word, PDF, PowerPoint).
- **Các node Code (`Extract PDF file_id`, `Extract DOCX file_id`, ...):**
  - Trích xuất mã định danh `file_id` từ phản hồi của Claude API để chuẩn bị cho bước tải file xuống.
- **Các node Download (`Download PDF`, `Download DOCX`, ...):**
  - Tải file từ hệ thống lưu trữ tạm thời của API về n8n.
- **Các node Upload Google Drive (`Upload PDF`, `Upload DOCX`, `Upload XLSX`, `Upload PPTX`):**
  - Cần kết nối tài khoản Google Drive qua `googleDriveOAuth2Api`.
  - Chọn thư mục đích (`Parent Folder ID`) trên Google Drive nơi các sếp muốn lưu trữ file tạo ra.

#### 3. Kích hoạt ⚡️
- Mở node **`On form submission`** để lấy đường dẫn URL của Form.
- Thực hiện một lượt **Test run** bằng cách điền form mẫu để kiểm tra xem file có được tạo và đẩy lên Google Drive thành công hay không.
- Nếu mọi thứ mượt mà, gạt công tắc sang **Active** để đưa vào vận hành chính thức.

### ✍️ Gợi ý nâng cao để tối ưu hóa
Để hệ thống xịn sò hơn nữa, các sếp có thể mở rộng workflow này bằng cách:
1. **Thêm thông báo Telegram/Slack:** Gửi tin nhắn thông báo kèm link Google Drive ngay lập tức cho sếp hoặc nhóm phụ trách khi tài liệu được tạo xong.
2. **Quản lý dữ liệu đầu vào:** Lưu thông tin các yêu cầu tạo tài liệu vào Google Sheets để dễ dàng kiểm tra lịch sử prompt của người dùng.
3. **Cá nhân hóa Agent Skills:** Tùy chỉnh các bộ hướng dẫn (Skills) trên tài khoản Anthropic của các sếp để tài liệu tạo ra mang đúng nhận diện thương hiệu (font chữ, màu sắc, phong cách văn bản).

### 📌 Kết luận
Việc tích hợp Claude AI Skills với n8n và Google Drive mở ra một kỷ nguyên tự động hóa hoàn toàn mới cho việc sản xuất nội dung và tài liệu doanh nghiệp. Chúc các sếp thiết lập thành công và tối ưu hóa tối đa hiệu suất công việc! Nếu gặp khó khăn gì, đừng ngần ngại trao đổi nhé.