---
title: "🚀 Tự động hóa quy trình tuyển dụng và đánh giá ứng viên bằng AI với n8n"
description: "Xây dựng hệ thống tuyển dụng thông minh hoàn toàn tự động từ khâu nộp hồ sơ, AI chấm điểm CV, tạo bộ câu hỏi, đặt lịch phỏng vấn đến gửi email chăm sóc ứng viên."
slug: "tu-dong-hoa-tuyen-dung-va-danh-gia-ung-vien-ai"
tags: [n8n, automation, no-code, hr-automation, ai-agent, openai]
keywords: [n8n workflow, tuyển dụng tự động, ai chấm điểm cv, airtable hr automation, openai n8n]
---

# 🚀 Tự động hóa quy trình tuyển dụng và đánh giá ứng viên bằng AI với n8n

Việc tuyển dụng nhân sự thủ công thường khiến các bộ phận HR ngập trong biển hồ sơ (CV), tốn hàng giờ liền để đọc, chấm điểm, sàng lọc, gửi email từ chối hay lên lịch phỏng vấn. Điều này không chỉ làm mất thời gian mà còn dễ bỏ lỡ các ứng viên tài năng.

Workflow **HR Job Posting and Evaluation with AI** này chính là giải pháp tự động hóa toàn diện giúp các sếp tối ưu hóa 100% quy trình tuyển dụng. Hệ thống sẽ tự động tiếp nhận hồ sơ qua form, dùng AI (OpenAI) để phân tích, chấm điểm CV dựa trên Mô tả công việc (Job Description - JD), tự động phân loại ứng viên, tạo câu hỏi phỏng vấn, lên lịch hẹn và gửi email cá nhân hóa.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian:** Không còn phải đọc thủ công từng chiếc CV hay loay hoay soạn email từ chối/mời phỏng vấn.
- **Đánh giá khách quan, chuẩn xác:** AI Agent chấm điểm CV dựa sát vào yêu cầu thực tế của JD và đưa ra lý do chi tiết.
- **Trải nghiệm ứng viên xuất sắc:** Phản hồi nhanh chóng, cá nhân hóa nội dung email và tự động hóa việc đặt lịch phỏng vấn mượt mà.
- **Quản lý tập trung:** Toàn bộ thông tin ứng viên, điểm số, trạng thái đều được lưu trữ và cập nhật đồng bộ trên Airtable.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động trơn tru, các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **OpenAI API Key** (Sử dụng cho AI Agent, tạo câu hỏi và viết email).
- **Tài khoản Airtable** (Sử dụng template *Simple Applicant Tracker* để đồng bộ dữ liệu).
- **Google Drive & Google Calendar** (Để lưu trữ CV tải lên và đồng bộ lịch phỏng vấn).
- **SMTP Server / Email Service** để gửi email tự động cho ứng viên.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ nguồn cung cấp, sau đó vào giao diện n8n Editor chọn **Import from File** hoặc copy trực tiếp mã JSON và dán vào workspace của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình các thành phần sau để hệ thống khớp với dữ liệu thực tế:
- **Node `On form submission` (Form Trigger):** Thay đổi `Form Description` thành mô tả công việc thực tế mà công ty đang tuyển dụng để ứng viên nắm rõ thông tin.
- **Các Node Airtable (`Airtable`, `Rejected`, `Potential Hire`, `update questionnaires`, v.v.):** Kết nối với tài khoản Airtable của sếp, chọn đúng Base và Table dựa trên template *Simple Applicant Tracker*.
- **Node `Upload CV to google drive` & `download CV`:** Kết nối tài khoản Google Drive qua OAuth2 để hệ thống tự động lưu trữ và đọc file PDF CV của ứng viên.
- **Các Node OpenAI (`AI Agent`, `generate questionnaires`, `Personalize email`, `Book Meeting`, `Screening Questions`):** Điền OpenAI API Key và kiểm tra lại các prompt trong node nếu cần tinh chỉnh phong cách phản hồi cho phù hợp với văn hóa công ty.
- **Node `Send Email` (SMTP):** Cấu hình thông tin máy chủ gửi mail để hệ thống tự động gửi thông báo cho ứng viên.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) bằng một vài dữ liệu mẫu (gửi form thử, upload 1 CV giả lập) để kiểm tra luồng dữ liệu chạy qua các nhánh `shortlisted?` (nếu điểm > 0.7).
- Sau khi test thành công, gạt công tắc sang **Active** để đưa hệ thống vào vận hành thực tế 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Slack/Telegram:** Thêm node thông báo vào kênh HR nội bộ ngay khi có ứng viên tiềm năng (Potential Hire) đạt điểm số cao từ AI.
- **Mở rộng bộ câu hỏi phỏng vấn tự động:** Kết hợp thêm Google Sheets hoặc Notion để lưu trữ ngân hàng câu hỏi tùy biến theo từng vị trí chuyên môn sâu.
- **Tự động gửi bài test năng lực:** Gửi ngay đường dẫn bài kiểm tra kỹ thuật (Google Form / Typeform) tự động cho ứng viên lọt vòng shortlist.

### 📌 Kết luận
Workflow **HR Job Posting and Evaluation with AI** là một vũ khí tối tân giúp tự động hóa khâu sàng lọc nhân sự đầu vào, giúp bộ phận tuyển dụng tập trung hoàn toàn vào việc phỏng vấn và đánh giá trực tiếp con người. Hãy thiết lập ngay hôm nay để nâng cấp hệ thống HR của doanh nghiệp lên một tầm cao mới!