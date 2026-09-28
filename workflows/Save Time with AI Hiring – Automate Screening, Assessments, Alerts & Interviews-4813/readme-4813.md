---
title: "🚀 Tiết Kiệm Thời Gian với AI Hiring – Tự Động Hóa Lọc, Đánh Giá, Cảnh Báo & Phỏng Vấn"
description: "Giải pháp tự động hóa 100% giúp doanh nghiệp tuyển dụng nhanh chóng, chính xác và tiết kiệm chi phí bằng cách kết hợp AI, Google Sheets, Slack, Email và Calendly."
slug: "ai-hiring-automation"
tags: [n8n, automation, no-code, HR, AI, recruitment]
keywords: [n8n workflow, tự động hóa, AI hiring, tuyển dụng, OpenAI, n8n automation]
---

# 🚀 Tiết Kiệm Thời Gian với AI Hiring – Tự Động Hóa Lọc, Đánh Giá, Cảnh Báo & Phỏng Vấn

Bạn đang phải mất hàng giờ để lọc hồ sơ, gửi email, lên lịch phỏng vấn và theo dõi tiến trình ứng viên? Mỗi bước thủ công không chỉ tốn thời gian mà còn dễ gây sai sót, làm giảm chất lượng tuyển dụng.  
Workflow **Save Time with AI Hiring** của Aayushman Sharma đã được thiết kế để **tự động hóa toàn bộ quy trình** từ khi ứng viên nộp đơn cho tới khi quyết định phỏng vấn, sử dụng AI để đánh giá hồ sơ, gửi thông báo qua email, Slack, và lên lịch phỏng vấn qua Calendly – **không cần viết một dòng code**.

:::info[Hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ vài giờ lên tới vài phút cho mỗi hồ sơ.  
- **Chính xác & nhất quán**: AI phân tích hồ sơ, giảm sai sót do con người.  
- **Tự động hóa liên tục**: Không cần can thiệp thủ công, workflow chạy 24/7.  
- **Tích hợp đa kênh**: Email, Slack, Calendly, Google Sheets – mọi thông tin luôn đồng bộ.  
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
| Dịch vụ | Tài khoản / Credential | Mô tả |
|---------|------------------------|-------|
| **Google Drive** | Google Drive API | Lưu trữ CV của ứng viên. |
| **Google Sheets** | Google Sheets API | Lưu trữ dữ liệu ứng viên, trạng thái, kết quả đánh giá. |
| **OpenAI** | API Key | Sử dụng mô hình GPT để trích xuất thông tin, tóm tắt, đánh giá. |
| **Email** | SMTP (Gmail, SendGrid, ... ) | Gửi email thông báo tới ứng viên và TA. |
| **Slack** | Incoming Webhook | Gửi thông báo tới kênh Slack. |
| **Calendly** | API Key | Lên lịch phỏng vấn tự động. |
| **Typeform** | API Key | Nhận kết quả đánh giá từ các bài kiểm tra. |
| **n8n** | Self-hosted VPS | Chạy workflow 24/7. |
:::

> **Lưu ý**: Đảm bảo các API key được bảo mật trong n8n Credentials, không chia sẻ công khai.

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥

1. Tải file JSON của workflow từ trang gốc: <https://n8n.io/workflows/4813>.  
2. Mở n8n Editor → **Import** → **Upload JSON** hoặc **Paste JSON**.  
3. Nhấn **Import** và workflow sẽ xuất hiện trong danh sách.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

| Node | Tên Node | Mô tả | Cài đặt cần chỉnh |
|------|----------|-------|--------------------|
| **Form Trigger** | `On form submission` | Nhận dữ liệu từ form (Google Forms, Typeform, ...). | URL form, mapping fields. |
| **Extract from File** | `Extract from File` | Trích xuất CV từ file đính kèm. | Đường dẫn file trong payload. |
| **Structured Output Parser** | `Structured Output Parser` | Chuyển dữ liệu thành JSON có cấu trúc. | Định dạng JSON schema. |
| **Google Drive** | `Upload CV` | Lưu CV vào thư mục đã định. | Credential Google Drive, thư mục ID. |
| **OpenAI (Chat)** | `OpenAI` | Gửi prompt tới GPT để trích xuất thông tin. | API Key, mô hình (gpt‑3.5‑turbo). |
| **Information Extractor** | `Applicant's Details` | Trích xuất tên, email, kinh nghiệm. | Mapping fields. |
| **Google Sheets** | `Add Applicant's Details in Google Sheet` | Ghi dữ liệu vào sheet. | Credential Google Sheets, ID sheet. |
| **Chain Summarization** | `Summarize Applicant's Profile` | Tóm tắt hồ sơ. | Prompt tùy chỉnh. |
| **Google Sheets** | `Get Job Description from Google Sheets` | Lấy mô tả công việc. | Sheet ID, range. |
| **Chain Summarization** | `Summarize Job Role Description` | Tóm tắt mô tả công việc. | Prompt tùy chỉnh. |
| **Chain LLM** | `Semantic Fit & Evaluation by HR Expert` | Đánh giá sự phù hợp. | Prompt, mô hình GPT. |
| **Google Sheets** | `Update Evaluation Results in Google Sheets` | Ghi kết quả đánh giá. | Sheet ID, range. |
| **EmailSend** | `Notify TA for Approval via Email` | Gửi email cho TA. | SMTP credentials, template. |
| **IF** | `Approval Check - IF Condition` | Kiểm tra trạng thái duyệt. | Điều kiện: `status == "Approved"`. |
| **EmailSend** | `Send Shortlist Email to Candidate` | Gửi email shortlist. | Template, recipient. |
| **EmailSend** | `Send Rejection Email to Candidate` | Gửi email từ chối. | Template, recipient. |
| **Google Sheets** | `Update Applicant's Status as REJECTED` | Cập nhật trạng thái. | Sheet ID, range. |
| **ScheduleTrigger** | `Run Daily at 09:00 AM` | Chạy hàng ngày. | Thời gian, múi giờ. |
| **Google Sheets** | `Fetch Records with Status "Resume Selected"` | Lấy danh sách ứng viên đã chọn CV. | Sheet ID, filter. |
| **SplitInBatches** | `Loop to Send Assessment Link to Each Candidate` | Gửi link đánh giá. | Batch size, payload. |
| **Google Sheets** | `Get Assessment Form URL` | Lấy URL form đánh giá. | Sheet ID, range. |
| **EmailSend** | `Send Assessment Submission Email` | Gửi email link đánh giá. | Template, recipient. |
| **Google Sheets** | `Update Status to Assessment Sent` | Cập nhật trạng thái. | Sheet ID, range. |
| **TypeformTrigger** | `Technical Support Engineer Assessment Trigger` | Nhận kết quả đánh giá. | API Key, form ID. |
| **TypeformTrigger** | `Technical Project Manager Assessment Trigger` | Nhận kết quả đánh giá. | API Key, form ID. |
| **Google Sheets** | `Update Applicant Status to Assessment Submitted` | Cập nhật trạng thái. | Sheet ID, range. |
| **EmailSend** | `Notify TA via Email for Assessment Submission` | Gửi email cho TA. | Template, recipient. |
| **Slack** | `Notify TA via Slack for Assessment Submission` | Gửi Slack. | Webhook URL, message. |
| **CalendlyTrigger** | `Trigger when Interview booked by applicant in calendly` | Nhận thông tin lịch phỏng vấn. | API Key, webhook. |
| **Google Sheets** | `Update Status to Interview Booked` | Cập nhật trạng thái. | Sheet ID, range. |
| **GoogleSheetsTrigger** | `Get Triggered when Applicant Status Update in Google Sheet` | Đánh giá thay đổi trạng thái. | Sheet ID, range. |
| **Switch** | `Route actions based on Status` | Chọn hành động theo trạng thái. | Mapping status → node. |
| **EmailSend** | `Send Interview Invite Email` | Gửi email mời phỏng vấn. | Template, recipient. |
| **EmailSend** | `Send Assessment Failed Email` | Gửi email thất bại đánh giá. | Template, recipient. |
| **EmailSend** | `Send Interview Cancelled Email` | Gửi email hủy phỏng vấn. | Template, recipient. |
| **EmailSend** | `Interview Reschedule Invite Email` | Gửi email tái lịch. | Template, recipient. |
| **EmailSend** | `Send Interview Passed/Shortlisted Email` | Gửi email shortlist. | Template, recipient. |
| **EmailSend** | `Send Interview Failed Email` | Gửi email từ chối. | Template, recipient. |
| **NoOp** | `No Operation, do nothing` | Dùng làm placeholder. | Không cần cấu hình. |
| **Google Sheets** | `Update Applicant's Status as RESUME SELECTED` | Cập nhật trạng thái cuối cùng. | Sheet ID, range. |

> **Tip**: Kiểm tra kỹ các trường `Sheet ID`, `Range`, `Prompt` và `Template` trước khi kích hoạt workflow.

### 3. Kích hoạt ⚡️

1. **Test run**: Chạy workflow với dữ liệu mẫu (đảm bảo các node “Test” hoạt động đúng).  
2. **Bật Active**: Đánh dấu workflow là “Active” để nó tự động chạy khi trigger xảy ra.  
3. **Theo dõi logs**: Kiểm tra logs trong n8n để phát hiện lỗi, điều chỉnh nếu cần.

## ✍️ Mẹo & gợi ý nâng cao

- **Gửi báo cáo định kỳ**: Thêm node `ScheduleTrigger` + `Google Sheets` + `EmailSend` để gửi báo cáo tuyển dụng hàng tuần tới HR.  
- **Lưu log vào Cloud Storage**: Thêm node `Google Drive` hoặc `S3` để lưu file log, giúp audit trail.  
- **Tích hợp Chatbot**: Sử dụng node `Telegram` hoặc `Discord` để gửi thông báo nhanh tới ứng viên.  
- **Phân tích dữ liệu**: Kết nối `Google Sheets` với `Data Studio` hoặc `Power BI` để trực quan hóa KPI tuyển dụng.  

## 📌 Kết luận

Workflow **Save Time with AI Hiring**