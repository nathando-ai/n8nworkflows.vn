---
title: "🚀 Tự động tạo bài đăng LinkedIn đỉnh cao bằng AI (Ollama, Hình ảnh & Gmail)"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa toàn bộ quy trình viết content LinkedIn, tạo hình ảnh minh họa bằng AI, gửi email kiểm duyệt và đăng bài tự động."
slug: "tu-dong-tao-bai-dang-linkedin-voi-ollama-va-ai"
tags: [n8n, automation, ai, marketing, ollama, linkedin]
keywords: [n8n workflow, tự động hóa linkedin, ollama ai, tạo bài đăng linkedin tự động, langchain n8n]
---

# 🚀 Tự động tạo bài đăng LinkedIn đỉnh cao bằng AI (Ollama, Hình ảnh & Gmail)

Việc duy trì sự hiện diện chuyên nghiệp trên LinkedIn đòi hỏi các nhà sáng tạo nội dung và marketer phải liên tục lên ý tưởng, viết bài hấp dẫn và thiết kế hình ảnh bắt mắt. Quy trình thủ công này tốn rất nhiều thời gian và năng lượng. 

Giải pháp là đây! Workflow n8n tích hợp AI này sẽ tự động hóa từ A-Z: từ việc nhận yêu cầu qua Form, sử dụng **Ollama AI** để viết bài chuẩn SEO/viral, tự động tạo hình ảnh minh họa, gửi email bản nháp để các sếp duyệt, cho đến việc tự động đăng lên LinkedIn.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không còn loay hoay nghĩ ý tưởng hay thiết kế ảnh.
- **Content chất lượng cao:** Ứng dụng AI thông minh (Ollama LangChain Agents) kết hợp tìm kiếm web (Tavily) để tạo ra nội dung có chiều sâu, cập nhật xu hướng.
- **Kiểm soát tuyệt đối:** Gửi email thông báo bản nháp kèm hình ảnh trước khi chính thức xuất bản.
- **Vận hành linh hoạt:** Kích hoạt dễ dàng qua Form biểu mẫu hoặc chạy thử thủ công bất cứ lúc nào.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Hệ thống n8n:** Đã cài đặt n8n (hỗ trợ các node LangChain và HTTP Request).
- **Ollama:** Đã cài đặt và chạy Local Ollama (hoặc qua cloud) để cung cấp model ngôn ngữ cho `Ollama Chat Model` và `Ollama Chat Model1`.
- **API Keys:** 
  - Tavily API Key (cho công cụ tìm kiếm `Tavily`).
  - API dịch vụ tạo ảnh (cho các node `Generate Image1` và `Generate Image2`).
  - Tài khoản LinkedIn (để cấp quyền đăng bài tự động qua node `LinkedIn`).
  - Cấu hình SMTP hoặc Gmail Credential (cho node `Send Email`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này từ n8n.io (Link gốc: [Workflow #4674](https://n8n.io/workflows/4674)) và import trực tiếp vào giao diện n8n của các sếp, hoặc copy/paste trực tiếp đoạn mã JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Khi đưa vào vận hành thực tế, các sếp cần chú ý cấu hình kỹ các node trọng điểm sau:
- **On form submission (`formTrigger`):** Thiết lập giao diện biểu mẫu nhận yêu cầu chủ đề bài đăng từ người dùng.
- **LinkedIn Post Agent & Image Prompt Agent (`agent`):** Kết nối đúng với `Ollama Chat Model` và `Ollama Chat Model1`. Đảm bảo các prompt hệ thống được tinh chỉnh theo văn phong thương hiệu cá nhân hoặc doanh nghiệp của các sếp.
- **Tavily (`toolHttpRequest`):** Điền chính xác Tavily API Key để Agent có thể tra cứu thông tin thực tế trên Internet khi cần viết bài phân tích chuyên sâu.
- **Generate Image1 & Generate Image2 (`httpRequest`):** Cấu hình endpoint API tạo ảnh (như DALL-E, Stable Diffusion hoặc dịch vụ tương đương) dựa trên câu lệnh (prompt) mà `Image Prompt Agent` vừa tạo ra.
- **Send Email (`emailSend`):** Cấu hình tài khoản gửi thư để nhận bản nháp bài viết kèm hình ảnh trực tiếp qua hộp thư cá nhân.
- **LinkedIn (`linkedIn`):** Xác thực tài khoản LinkedIn cá nhân hoặc doanh nghiệp để n8n có quyền đăng bài trực tiếp.

#### 3. Kích hoạt ⚡️
- Bấm **‘Test workflow’** bằng node `When clicking ‘Test workflow’` hoặc điền thử form ở `On form submission` để kiểm tra toàn bộ luồng chạy (từ tạo content -> tạo ảnh -> gửi email).
- Sau khi kiểm tra mọi thứ mượt mà, gạt công tắc sang **Active** để workflow chính thức tự động vận hành.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Chatbot:** Thay vì dùng Form Trigger, các sếp có thể đổi thành Telegram Trigger hoặc Slack Trigger để nhận yêu cầu viết bài nhanh chóng qua chat.
- **Lưu trữ dữ liệu:** Thêm node Google Sheets hoặc Airtable sau bước tạo bài viết để lưu lại lịch sử content phục vụ việc đo lường hiệu quả sau này.
- **Quy trình duyệt bài linh hoạt:** Thay vì chỉ gửi email, có thể tạo một bước chờ phê duyệt (Wait node) tích hợp nút bấm duyệt bài trực tiếp trên Slack/Telegram.

### 📌 Kết luận
Với workflow tự động hóa thông minh này, việc sản xuất nội dung chuyên nghiệp trên LinkedIn chưa bao giờ dễ dàng đến thế. Hãy cài đặt ngay hôm nay để tối ưu hóa hiệu suất làm marketing của các sếp!