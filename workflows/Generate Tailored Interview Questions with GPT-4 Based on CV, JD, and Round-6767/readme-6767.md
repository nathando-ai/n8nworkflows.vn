---
title: "🚀 Tự động tạo bộ câu hỏi phỏng vấn cá nhân hóa bằng AI (GPT-4) dựa trên CV, JD và Vòng phỏng vấn"
description: "Xây dựng hệ thống tuyển dụng thông minh với n8n và GPT-4: Tự động phân tích CV, đọc JD từ Google Drive/Sheets, tạo bộ câu hỏi phỏng vấn chuyên sâu theo từng vòng và gửi báo cáo qua email cho Hiring Team."
slug: "tu-dong-tao-cau-hoi-phong-van-bang-ai-cv-jd"
tags: [n8n, automation, ai, openai, hr, recruitment]
keywords: [n8n workflow, tao cau hoi phong van ai, gpt-4 hr automation, tu dong hoa tuyen dung, phan tich cv jd n8n]
---

# 🚀 Tự động tạo bộ câu hỏi phỏng vấn cá nhân hóa bằng AI (GPT-4) dựa trên CV, JD và Vòng phỏng vấn

Các sếp làm trong ngành nhân sự (HR) hay Hiring Manager chắc chắn hiểu cảm giác "ngợp" thế nào khi phải chuẩn bị câu hỏi phỏng vấn cho hàng chục ứng viên mỗi tuần. Việc đọc kỹ CV, đối chiếu với Job Description (JD) tốn hàng giờ đồng hồ, chưa kể mỗi vòng phỏng vấn (Sơ loại, Kỹ thuật, Vòng cuối) lại đòi hỏi những tiêu chí đánh giá hoàn toàn khác nhau.

Giải pháp thủ công này vừa tốn thời gian, vừa dễ dẫn đến việc đặt câu hỏi lan man, thiếu chuẩn hóa.

Đừng lo, bài viết này sẽ hướng dẫn các sếp triển khai một **Workflow n8n thông minh** tích hợp **GPT-4 (OpenAI)** giúp tự động hóa toàn bộ quy trình: Nhận CV từ form ứng tuyển $\rightarrow$ Đọc JD từ Google Drive $\rightarrow$ Phân tích chéo $\rightarrow$ Tạo bộ câu hỏi phỏng vấn chuyên sâu theo đúng vòng phỏng vấn $\rightarrow$ Gửi báo cáo chi tiết qua Email cho hội đồng tuyển dụng chỉ trong vài giây!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, xử lý mượt mà các file PDF nặng và các tác vụ AI, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian chuẩn bị:** Không còn phải đọc thủ công từng chiếc CV hay mất công nghĩ câu hỏi kỹ thuật.
- **Cá nhân hóa 100%:** Câu hỏi sinh ra bám sát điểm mạnh/yếu của ứng viên trên CV và yêu cầu cốt lõi của JD.
- **Chuẩn hóa quy trình phỏng vấn:** Phân loại rõ ràng câu hỏi theo từng vòng (Initial Screening, Technical Round, Final Interview).
- **Tự động hóa thông báo:** Gửi trọn bộ báo cáo phỏng vấn (bao gồm tóm tắt ứng viên, câu hỏi và đáp án gợi ý) trực tiếp đến email của Hiring Team.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **OpenAI API Key** (Sử dụng model `gpt-4.1-mini` hoặc GPT-4).
- **Google Drive & Google Sheets API** (Để lưu trữ JD dạng PDF và bảng ánh xạ vị trí tuyển dụng).
- **Cấu hình SMTP** (Gmail, SendGrid, hoặc các dịch vụ SMTP khác để gửi email báo cáo).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow này và dán trực tiếp vào n8n Editor của mình, hoặc import file JSON tải từ nguồn cấp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống vận hành trơn tru, các sếp cần cấu hình chính xác các node trọng điểm sau:

- **Node `Application form` (formTrigger):** Nơi ứng viên hoặc HR nộp thông tin gồm file CV (PDF), vị trí ứng tuyển (Dropdown) và vòng phỏng vấn.
- **Node `Get position JD` (googleSheets) & `Download file` (googleDrive):** Kết nối tài khoản Google để hệ thống tự động tìm link JD tương ứng trong file Sheet cấu hình và tải file PDF JD về.
- **Node `Extract profile` & `Extract Job Description` (extractFromFile):** Trích xuất toàn bộ văn bản từ file PDF CV của ứng viên và file PDF JD của công ty.
- **Node `gpt4-1 model` & `gpt-4-1 model 2` (lmChatOpenAi):** Thêm OpenAI Credentials và chọn model (`gpt-4.1-mini`). Đây là "bộ não" thực hiện phân tích profile và sinh câu hỏi.
- **Node `Interview round metadata` (set):** Thiết lập các thông tin bổ sung về ngữ cảnh vòng phỏng vấn (Sơ loại, Kỹ thuật, Vòng sếp tổng...).
- **Node `Send interview prep report to hiring team` (emailSend):** Cấu hình thông tin SMTP (Host, Port, User, Pass) để gửi báo cáo trực tiếp đến email người phỏng vấn.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và test thử bằng một form điền mẫu với file CV giả lập.
- Kiểm tra kết quả trả về trong email xem định dạng đã đẹp mắt chưa.
- Bật công tắc **Active** để đưa workflow vào vận hành thực tế 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Chatbot/Slack:** Thay vì gửi email, có thể cấu hình node gửi thẳng bộ câu hỏi phỏng vấn vào kênh Slack hoặc nhóm Telegram riêng của bộ phận tuyển dụng.
- **Lưu trữ kết quả đánh giá:** Kết nối thêm một node Google Sheets ở cuối luồng để tự động lưu lịch sử tạo câu hỏi, phục vụ cho việc tracking hiệu suất tuyển dụng.
- **Tinh chỉnh Prompt AI:** Tại các Agent node, các sếp có thể điều chỉnh System Prompt để AI đặt ra các câu hỏi dạng tình huống (behavioral questions) hoặc câu hỏi thực hành lập trình tùy theo đặc thù ngành nghề.

### 📌 Kết luận
Việc tự động hóa khâu chuẩn bị phỏng vấn với AI và n8n không chỉ giúp tiết kiệm thời gian mà còn nâng tầm chuyên nghiệp cho toàn bộ quy trình tuyển dụng của doanh nghiệp. Hãy áp dụng ngay hôm nay để đội ngũ HR và Hiring Manager tập trung hoàn toàn vào việc đánh giá con người thay vì tốn sức làm thủ công!