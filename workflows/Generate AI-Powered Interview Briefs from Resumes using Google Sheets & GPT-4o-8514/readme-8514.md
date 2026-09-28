---
title: "🚀 Tự động tạo Hồ sơ phỏng vấn AI từ CV ứng viên với Google Sheets và GPT-4o"
description: "Tối ưu hóa quy trình tuyển dụng nhân sự bằng cách tự động đọc CV từ Google Drive/Sheets, phân tích bằng Azure OpenAI GPT-4o và gửi bản tóm tắt phỏng vấn qua Gmail một cách thông minh."
slug: "tao-ho-so-phong-van-ai-tu-cv-google-sheets-gpt-4o"
tags: [n8n, automation, no-code, hr-automation, ai-summarization, openai, google-sheets]
keywords: [n8n workflow, tự động hóa nhân sự, lọc CV tự động, AI interview briefs, google sheets automation, azure openai n8n]
---

# 🚀 Tự động tạo Hồ sơ phỏng vấn AI từ CV ứng viên với Google Sheets và GPT-4o

Trong các quy trình tuyển dụng hiện đại, việc HR phải đọc hàng trăm CV, chắt lọc thông tin và chuẩn bị câu hỏi phỏng vấn cho từng ứng viên chiếm rất nhiều thời gian thủ công. Quá trình này không chỉ mệt mỏi mà đôi khi còn bỏ sót những điểm sáng quan trọng trong hồ sơ. 

Giải pháp? Workflow n8n này sẽ tự động hóa 100% quy trình: lấy danh sách ứng viên từ **Google Sheets**, tải CV từ **Google Drive**, phân tích nội dung chuyên sâu bằng **Azure OpenAI (GPT-4o)** và tự động gửi hồ sơ phỏng vấn (Interview Brief) hoàn chỉnh trực tiếp qua **Gmail** cho hội đồng tuyển dụng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian tuyển dụng:** Không cần phải đọc thủ công từng file PDF CV ứng viên.
- **Bản tóm tắt chuyên nghiệp:** AI tự động phân tích kinh nghiệm, kỹ năng cốt lõi và gợi ý câu hỏi phỏng vấn sắc sảo cho từng vị trí.
- **Tự động hóa đa nền tảng:** Kết hợp mượt mà giữa Google Sheets, Google Drive, Azure OpenAI và Gmail trong một luồng duy nhất.
- **Hoạt động liên tục:** Có thể kích hoạt thủ công hoặc cấu hình để chạy tự động ngay khi có ứng viên mới điền form.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động trơn tru, các sếp cần chuẩn bị trước các tài khoản và API keys sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Google Sheets & Google Drive:** File Google Sheets chứa thông tin ứng viên và link file CV (PDF/Word) lưu trên Google Drive.
- **Azure OpenAI API Key:** Tài khoản Azure OpenAI đã triển khai model GPT-4o.
- **Gmail Account / Credentials:** Để gửi email tự động các bản tóm tắt phỏng vấn.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tạo một workflow mới trong n8n Editor, sau đó copy toàn bộ mã JSON của workflow (hoặc import file JSON tải từ nguồn) và dán trực tiếp vào giao diện làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các nodes cốt lõi sau để hệ thống chạy không lỗi:

- **Get row(s) in sheet (`googleSheets`):** Kết nối tài khoản Google của bạn, chọn đúng file Google Sheets chứa danh sách ứng viên và chỉ định sheet name / range chứa dữ liệu thông tin ứng viên (tên, email, link CV...).
- **Download file (`googleDrive`):** Thiết lập node này để lấy ID file CV từ cột tương ứng trong Google Sheets tải xuống hệ thống n8n.
- **Extract from File (`extractFromFile`):** Node này giúp bóc tách toàn bộ văn bản (text) từ file PDF hoặc Word của CV ứng viên để chuẩn bị feed vào AI.
- **Azure OpenAI Chat Model1 (`lmChatAzureOpenAi`) & Basic LLM Chain (`chainLlm`):** 
  - Điền thông tin kết nối Azure OpenAI (Endpoint, API Key, Deployment Name cho model GPT-4o).
  - Tùy chỉnh System Prompt trong `Basic LLM Chain` để yêu cầu AI trích xuất thông tin theo đúng định dạng mong muốn (ví dụ: Tóm tắt kinh nghiệm, điểm mạnh, điểm yếu, bộ câu hỏi phỏng vấn gợi ý).
- **Code (`code`):** Xử lý dữ liệu đầu ra từ AI hoặc định dạng lại cấu trúc dữ liệu JSON trước khi đẩy sang bước gửi email.
- **Send Follow-up Email1 (`gmail`):** Cấu hình tài khoản Gmail gửi đi, thiết lập người nhận (có thể là HR Manager hoặc Hội đồng phỏng vấn) và chèn nội dung kết quả phân tích từ AI vào phần thân email (Body).

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** tại node `When clicking ‘Execute workflow’` để chạy thử với dữ liệu mẫu (Test Run).
- Kiểm tra kết quả trả về ở Gmail xem email đã được soạn và gửi đúng chuẩn chưa.
- Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để workflow chính thức đi vào vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Webhook/Form:** Thay vì dùng nút bấm thủ công (`manualTrigger`), các sếp có thể đổi thành `Webhook` hoặc `Google Forms Trigger` để mỗi khi có ứng viên mới nộp đơn, hệ thống tự động chạy ngay lập tức.
- **Lưu log kết quả:** Thêm một node `Google Sheets` phía cuối luồng để ghi lại trạng thái "Đã tạo Brief thành công" kèm thời gian vào file quản lý tuyển dụng.
- **Mở rộng kênh thông báo:** Kết hợp thêm node `Slack` hoặc `Telegram` để bắn thông báo nhanh cho trưởng bộ phận (Hiring Manager) vào xem ngay bản tóm tắt CV khi vừa xử lý xong.

### 📌 Kết luận
Việc ứng dụng AI và tự động hóa vào quy trình tuyển dụng không chỉ giúp tiết kiệm nguồn lực mà còn nâng cao chất lượng trải nghiệm của đội ngũ nhân sự. Hãy "lên đồ" ngay workflow này để tối ưu hóa khâu lọc hồ sơ ngay hôm nay các sếp nhé!