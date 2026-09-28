---
title: "🚀 Tự động phân tích và lọc CV bằng Multimodal Vision AI trong n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động tải CV PDF từ Google Drive, chuyển đổi thành hình ảnh và phân tích bằng Google Gemini Vision AI để chống gian lận ATS."
slug: "cv-resume-pdf-parsing-multimodal-vision-ai-n8n"
tags: [n8n, automation, ai, google-gemini, hr, vision-ai]
keywords: [n8n workflow, cv parsing, multimodal ai, google gemini, tự động hóa nhân sự, ats bypass]
---

# 🚀 Tự động phân tích và lọc CV bằng Multimodal Vision AI trong n8n

Trong kỷ nguyên tuyển dụng số, các hệ thống ATS (Applicant Tracking System) truyền thống thường dễ bị qua mặt bởi những chiêu trò "nhúng prompt ẩn" (hidden prompts) do ứng viên cài cắm vào file PDF nhằm đánh lừa AI. Làm thế nào để giải quyết bài toán này? 

Workflow n8n này chính là giải pháp tự động hóa 100% không cần code, tận dụng sức mạnh của **Multimodal Vision AI (Google Gemini)**. Thay vì trích xuất văn bản thuần túy (dễ bị thao túng), workflow sẽ chụp ảnh trang CV và để AI "nhìn" và đọc nó như một con người thực thụ, đảm bảo tính khách quan và bảo mật tối đa cho doanh nghiệp.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Chống gian lận tuyệt đối:** Vượt qua các mẹo nhúng prompt ẩn trong CV để tự động đổi kết quả tuyển dụng.
- **Hiểu layout như con người:** AI đọc CV dưới dạng hình ảnh, không lo lỗi font, lệch bảng hay mất định dạng khi trích xuất text.
- **Tiết kiệm 90% thời gian:** Tự động hóa hoàn toàn quy trình từ tải file, chuyển đổi, phân tích đến trích xuất dữ liệu có cấu trúc.
- **Hoạt động liên tục 24/7:** Xử lý hàng trăm hồ sơ tự động ngay khi ứng viên nộp đơn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Google Drive Credentials** (OAuth2 API) để tải file CV của ứng viên.
- **Google Gemini API Key** (Google Palm/Gemini API Credentials) cho mô hình ngôn ngữ đa phương thức.
- **Stirling PDF API** (hoặc dịch vụ tương đương) để thực hiện chuyển đổi từ PDF sang Image qua HTTP API.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã JSON của workflow này và dán trực tiếp vào n8n Editor, hoặc import file JSON thông qua giao diện n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node sau:
- **Node `Download Resume` (Google Drive):** Kết nối tài khoản Google Drive của các sếp và trỏ đến thư mục chứa CV cần test (hoặc cấu hình nhận file động từ Email/Webhook tuyển dụng).
- **Node `PDF-to-Image API` (HTTP Request):** Cấu hình endpoint gọi tới dịch vụ Stirling PDF để chuyển file PDF thành định dạng hình ảnh. *(Lưu ý: Bản demo đang dùng public API công khai, khi chạy thật nên tự dựng một instance Stirling PDF riêng tư).*
- **Node `Resize Converted Image` (Edit Image):** Tối ưu hóa kích thước hình ảnh (khuyên dùng khoảng 75% kích thước A4 gốc) để tăng tốc độ xử lý của AI mà vẫn giữ được độ sắc nét.
- **Node `Google Gemini Chat Model` & `Candidate Resume Analyser`:** Điền Google Gemini API Key và thiết lập Prompt chấm điểm, đánh giá năng lực ứng viên dựa trên hình ảnh CV đầu vào.
- **Node `Structured Output Parser`:** Thiết lập schema dữ liệu đầu ra mong muốn (Ví dụ: Tên ứng viên, Kinh nghiệm, Điểm đánh giá, Có phù hợp hay không...).

#### 3. Kích hoạt ⚡️
- Nhấn **‘Test workflow’** để chạy thử với mẫu CV kiểm tra (có thể tải CV test mẫu từ link Google Drive trong ghi chú canvas của workflow).
- Kiểm tra kết quả trả về ở các node. Nếu mọi thứ xanh mướt, hãy bật nút **Active workflow** để hệ thống tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm node Slack hoặc Telegram để bắn tin nhắn thông báo ngay lập tức về HR khi có ứng viên đạt điểm số phù hợp.
- **Lưu trữ dữ liệu:** Tự động đẩy kết quả phân tích từ AI vào Google Sheets hoặc Notion để đội ngũ nhân sự dễ dàng theo dõi và phỏng vấn.
- **Email tự động:** Kết hợp điều kiện `Should Proceed To Stage 2?`, nếu ứng viên đạt điểm cao, tự động gửi email mời phỏng vấn.

### 📌 Kết luận
Việc ứng dụng Multimodal Vision AI vào quy trình sàng lọc CV không chỉ giúp doanh nghiệp tiết kiệm thời gian mà còn vô hiệu hóa hoàn toàn các chiêu trò gian lận kỹ thuật số tinh vi. Hãy import ngay workflow này và nâng cấp hệ thống tuyển dụng của các sếp lên một tầm cao mới!