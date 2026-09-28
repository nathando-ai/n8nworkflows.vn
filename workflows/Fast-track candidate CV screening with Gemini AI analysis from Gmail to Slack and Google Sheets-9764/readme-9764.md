---
title: "🚀 Tự động hóa sàng lọc CV ứng viên với Gemini AI, Gmail, Slack và Google Sheets"
description: "Xây dựng trợ lý tuyển dụng AI thông minh giúp tự động đọc CV từ Gmail, khớp với mô tả công việc (JD), phân tích bằng Gemini AI và gửi báo cáo chốt đơn qua Slack."
slug: "tu-dong-hoa-sang-loc-cv-ung-vien-gemini-ai"
tags: [n8n, automation, no-code, ai-agent, gemini, recruitment]
keywords: [n8n workflow, loc cv tu dong, gemini ai tuyen dung, google sheets, slack automation]
---

# 🚀 Trợ lý Tuyển dụng AI Tự động Sàng lọc CV (Fast-Track CV Screening)

Các sếp có đang cảm thấy ngộp thở mỗi mùa tuyển dụng khi phải hàng giờ đồng hồ mở từng email, tải từng file CV, đọc lướt qua xem ứng viên có hợp với Job Description (JD) hay không, rồi lại thủ công copy dữ liệu vào Excel? Công việc lặp đi lặp lại này ngốn hàng đống thời gian quý báu mà lẽ ra đội ngũ nhân sự nên dùng để phỏng vấn những nhân tài thực thụ.

Workflow n8n này chính là giải pháp tự động hóa 100% không cần code, giúp các sếp biến quy trình tuyển dụng vòng đầu (First-round screening) thành một cỗ máy tự động: **CV gửi tới → Khớp JD → AI phân tích đa chiều → Lưu vết Google Sheets → Báo cáo trực quan qua Slack với nút bấm ra quyết định tức thì**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 20+ giờ mỗi tuần**: Loại bỏ hoàn toàn khâu đọc, phân loại và nhập liệu CV thủ công.
- **Xử lý linh hoạt mọi định dạng**: Tự động nhận diện và xử lý mượt mà cả file PDF lẫn Word (Doc/Docx).
- **AI thông minh hai lớp**: Tự động khớp CV với đúng JD dựa vào ngữ cảnh email hoặc nội dung kỹ năng của ứng viên.
- **Tương tác nhanh chóng**: Gửi ngay bảng tóm tắt điểm mạnh, điểm yếu kèm điểm số (0-10) và nút bấm Phê duyệt/Từ chối trực tiếp lên Slack của team.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ TRƯỚC KHI "LÊN ĐỒ"]
- **Tài khoản Gmail** có bật quyền API.
- **Google Drive** (OAuth2) với 2 thư mục: "Candidate CVs" (lưu CV ứng viên) và "Job Descriptions" (lưu các file JD dạng PDF hoặc Google Docs).
- **Google Sheets** (OAuth2) để lưu trữ toàn bộ dữ liệu ứng viên.
- **Slack Workspace** với quyền Bot để gửi thông báo.
- **Google Gemini API Key** ([Lấy key miễn phí tại đây](https://makersuite.google.com/app/apikey)).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần tải file JSON của workflow này, vào giao diện n8n Editor chọn **Import from File** hoặc copy toàn bộ mã JSON và dán trực tiếp vào màn hình làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp cần cấu hình chính xác các điểm sau trên các node tương ứng:
- **Node `Receive CV via Email`**: Chọn tài khoản Gmail OAuth2 và thiết lập nhãn (Label) Gmail cần lọc (ví dụ: `CV-Screening`).
- **Node `Upload CV - PDF` & `Stream Doc/Docx File`**: Cập nhật Folder ID của Google Drive trỏ đến thư mục **"Candidate CVs"**.
- **Node `Access JD Files`**: Cập nhật Folder ID trỏ đến thư mục chứa các file Job Description (**"Job Descriptions"**).
- **Node `Append row in sheet`**: Kết nối tài khoản Google Sheets, chọn file Google Sheet có tên tiêu đề khớp với [mẫu AI Candidate Screening sheet chuẩn](https://docs.google.com/spreadsheets/d/16HebkHqsM2ZE_IdJzQk1mDE3i2-HwsUqa5gEwXaF-7A/edit?usp=sharing).
- **Node `Send Candidate Screening Confirmation`**: Chọn channel Slack nhận thông báo và cấu hình lại ID Google Sheet trong phần Blocks của tin nhắn.
- **Các node AI Agent (Gemini)**: Nhập Google Gemini API Key và tùy chỉnh lại đoạn mô tả công ty (Company Description) trong System Message của các node `JD Matching Agent`, `Detailed JD Matching Agent`, và `Recruiter Scoring Agent` cho phù hợp với doanh nghiệp của sếp.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và gửi thử một email chứa CV mẫu có gắn nhãn tương ứng để test luồng chạy.
- Sau khi kiểm tra dữ liệu đã vào Google Sheets và Slack hiển thị đẹp mắt, các sếp chỉ cần gạt công tắc **Active** là xong!

### ✍️ Mẹo & gợi ý nâng cao
- **Tự động hóa quyết định**: Thêm một node `If` sau bước AI Scoring để tự động gửi email cảm ơn hoặc lên lịch phỏng vấn ngay cho những ứng viên đạt điểm số cao (ví dụ: từ 8/10 trở lên).
- **Mở rộng lưu trữ đa nền tảng**: Kết nối thêm các node Notion, Airtable hoặc các hệ thống ATS chuyên dụng để lưu trữ dữ liệu ứng viên song song.
- **Tích hợp lịch phỏng vấn**: Gắn thêm link Cal.com hoặc Calendly vào tin nhắn Slack hoặc email tự động để ứng viên tự book lịch phỏng vấn khi được duyệt.

### 📌 Kết luận
Với workflow n8n cực kỳ thông minh này, các sếp đã có thể xây dựng một hệ thống sơ tuyển nhân sự tự động hóa đỉnh cao, vừa tiết kiệm chi phí vận hành, vừa không bỏ lỡ bất kỳ nhân tài nào. Triển khai ngay thôi các sếp ơi!