---
title: "🚀 Tự Động Học Viên Tiềm Năng với AI GPT-4, Airtable & Google Drive - Hiring Smarter, Not Harder"
description: "Workflow tự động hóa tuyển dụng HR sử dụng AI GPT-4 để đánh giá ứng viên, trích xuất CV từ PDF, so khớp kỹ năng với yêu cầu công việc và tự động thông báo cho HR. Giúp tiết kiệm 80% thời gian đánh giá thủ công và giảm thiểu sai sót trong quá trình tuyển dụng."
slug: "tuyen-dung-voi-ai-gpt4-airtable-google-drive"
tags: [n8n, automation, hr, ai, gpt-4, airtable, google-drive, no-code, hiring]
keywords: [tự động hóa tuyển dụng n8n, ai tuyển dụng gpt-4, đánh giá ứng viên tự động, airtable n8n, google drive n8n, workflow tuyển dụng no-code]
---

# 🚀 **Tự Động Học Viên Tiềm Năng với AI GPT-4, Airtable & Google Drive**

### **Giải pháp AI tự động hóa tuyển dụng cho HR: Từ ứng viên đến quyết định tuyển dụng chỉ trong vài giây**

Hiện nay, quá trình tuyển dụng tại các doanh nghiệp thường gặp phải những vấn đề như:
- **Tốn thời gian**: Phải đọc hàng trăm CV, so khớp kỹ năng với yêu cầu công việc thủ công.
- **Sai sót cao**: Nhận diện không chính xác ứng viên phù hợp do chủ quan.
- **Không thống nhất**: Quy trình đánh giá khác nhau giữa các thành viên HR.
- **Không lưu trữ hiệu quả**: CV và hồ sơ ứng viên phân tán, khó theo dõi.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động trích xuất nội dung từ CV PDF** (không cần OCR).
✅ **AI GPT-4 đánh giá ứng viên** so với yêu cầu công việc, tính điểm phù hợp (0-100%).
✅ **Lưu trữ hồ sơ vào Airtable** (cập nhật động) và **Google Drive** (để bảo mật).
✅ **Gửi email tự động cho HR** khi tìm thấy ứng viên phù hợp.
✅ **Tiết kiệm 80% thời gian** so với cách làm thủ công.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted) để đảm bảo bảo mật và không bị giới hạn API.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: AI tự động đánh giá ứng viên trong vài giây thay vì mất hàng giờ.
- **Chính xác cao**: GPT-4 so khớp kỹ năng và kinh nghiệm với yêu cầu công việc một cách khách quan.
- **Lưu trữ thông minh**: Hồ sơ ứng viên được lưu vào Airtable (dễ quản lý) và Google Drive (bảo mật).
- **Tự động hóa hoàn chỉnh**: Từ nhận ứng viên đến thông báo cho HR, toàn bộ quy trình tự động.
- **Cải thiện trải nghiệm ứng viên**: Form đăng ký đơn giản, phản hồi nhanh chóng.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Airtable API Key**:
   - Tạo một **Airtable Base** từ [mẫu này](https://airtable.com/appgVjZcaRP8BsKf0/tblla4rBCW3BhPtRO/viw19l5BlEW7NnZJQ) (sao chép và tạo bản sao).
   - Tạo **API Key** từ **Settings > API > Generate API Key** trong Airtable.

2. **OpenAI API Key (GPT-4)**:
   - Đăng ký tài khoản tại [OpenAI](https://platform.openai.com/), chọn mô hình **GPT-4o-mini** (rẻ hơn GPT-4 nhưng hiệu quả).
   - Tạo **API Key** từ **Settings > View API Keys**.

3. **Google Drive OAuth2**:
   - Tạo **Google Cloud Project** và bật **Google Drive API**.
   - Tạo **OAuth2 Client ID** và đăng ký trong n8n.

4. **Gmail OAuth2**:
   - Tạo **OAuth2 Client ID** trong [Google Cloud Console](https://console.cloud.google.com/).
   - Cấu hình trong n8n để gửi email tự động.

5. **VPS n8n (khuyến nghị)**:
   - Cài đặt n8n trên VPS để tránh giới hạn API và đảm bảo hoạt động 24/7.
   - [Hướng dẫn cài n8n trên VPS](https://docs.n8n.io/hosting/installation/installation-on-a-vps/) (tự host).
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/4481) hoặc sao chép mã JSON từ trang này.
- Mở **n8n Editor** → Nhấn **Import Workflow** → Chọn file JSON hoặc dán mã JSON.
- **Lưu ý**: Không thay đổi tên node (nếu không muốn lỗi).

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **13 node chính**, các sếp cần cấu hình kỹ lưỡng như sau:

##### **A. Cấu hình Airtable**
- **Node "Search Job Posting"**:
  - Chọn **Airtable Base** đã tạo từ mẫu.
  - Điền **API Key** vào **Credentials** (tạo từ Airtable).
  - **Table Name**: `Job Postings` (đã có sẵn trong mẫu).

- **Node "Create Candidate"**:
  - Chọn **Airtable Base** cùng với node trên.
  - **Table Name**: `Candidates` (đã có sẵn trong mẫu).
  - **Fields**:
    - `Status` (Suitable/Not Suitable/Under Review)
    - `Match Percentage` (số liệu từ AI)
    - `Screening Notes` (ghi chú chi tiết từ AI)

##### **B. Cấu hình OpenAI (AI Agent)**
- **Node "OpenAI Chat Model"**:
  - Chọn **Credentials**: `openAiApi` (đã tạo API Key).
  - **Model**: `gpt-4o-mini` (rẻ hơn GPT-4 nhưng hiệu quả).
  - **Prompt**: Workflow tự động cấu hình, không cần chỉnh sửa.

- **Node "Candidate Screener AI Agent"**:
  - Đây là **AI Agent** sử dụng LangChain để phân tích:
    - **So khớp kỹ năng** với yêu cầu công việc.
    - **Đánh giá chất lượng cover letter**.
    - **Tính điểm phù hợp** (0-100%).
  - **Lưu ý**: Không cần chỉnh sửa, chỉ cần cung cấp **API Key OpenAI** đúng.

##### **C. Cấu hình Google Drive**
- **Node "Upload File"**:
  - Chọn **Credentials**: `googleDriveOAuth2`.
  - **Folder ID**: Tạo một folder mới trong Google Drive để lưu CV ứng viên.

- **Node "Set File Permission"**:
  - Chọn **Credentials**: `googleDriveOAuth2`.
  - **Permission**: `anyone` (để Airtable có thể truy cập file).

##### **D. Cấu hình Email (Gmail)**
- **Node "Send email to HR"**:
  - Chọn **Credentials**: `gmailOAuth2`.
  - **Email Template**:
    ```plaintext
    Subject: New Suitable Candidate Found - {{ $node["Check if candidate is suitable"].json["$.status"] }}

    Hi Team,

    A new candidate has been identified as suitable for the position: {{ $node["Search Job Posting"].json["$.name"] }}.

    Details:
    - Name: {{ $node["Candidate Application Form"].json["$.fullName"] }}
    - Email: {{ $node["Candidate Application Form"].json["$.email"] }}
    - Match Percentage: {{ $node["Structured Output Parser"].json["$.matchPercentage"] }}%
    - Status: {{ $node["Structured Output Parser"].json["$.status"] }}

    View full details: [Airtable Link](https://airtable.com/...)
    View resume: [Google Drive Link]({{ $node["Set File Permission"].json["$.webViewLink"] }})

    Best regards,
    Your HR Automation System
    ```
  - **Lưu ý**: Thay thế `Airtable Link` bằng liên kết thực tế của bảng `Candidates`.

##### **E. Cấu hình Form (Candidate Application Form)**
- **Node "Candidate Application Form"**:
  - **Fields bắt buộc**:
    - Full Name (text)
    - Email Address (email validation)
    - Position Applied For (dropdown, liên kết với Airtable)
    - Relevant Skills (textarea)
    - Cover Letter (textarea)
    - Resume (PDF upload only)
  - **Lưu ý**:
    - Sử dụng **Form Trigger** để nhận dữ liệu từ ứng viên.
    - Cấu hình **validation** cho email và file PDF.

##### **F. Cấu hình AI Output Parser**
- **Node "Structured Output Parser"**:
  - Workflow tự động cấu hình, không cần chỉnh sửa.
  - **Output**:
    ```json
    {
      "status": "Suitable/Not Suitable/Under Review",
      "matchPercentage": 85,
      "screeningNotes": "Candidate has 5+ years of Python experience, matches 85% of requirements."
    }
    ```

#### **3. Kích hoạt ⚡️**
- **Test Run**:
  - Nhấn **Run Workflow** và nhập dữ liệu mẫu (tải CV PDF và điền form).
  - Kiểm tra **Airtable** và **Google Drive** để xác nhận dữ liệu được lưu trữ.
- **Bật Active**:
  - Sau khi test thành công, nhấn **Active** để workflow chạy tự động khi có ứng viên mới.

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Kết nối với Slack/Telegram**:
   - Thêm **Slack Webhook** hoặc **Telegram Bot** để thông báo ứng viên phù hợp ngay khi tìm thấy.

2. **Lưu log hoạt động**:
   - Sử dụng **Sticky Note** hoặc **Google Sheets** để ghi lại lịch sử đánh giá ứng viên.

3. **Báo cáo định kỳ**:
   - Tạo **Google Sheets** hoặc **Airtable Dashboard** để theo dõi số lượng ứng viên, tỷ lệ phù hợp, và thời gian phản hồi.

4. **Tích hợp với Zoom/Teams**:
   - Khi ứng viên phù hợp, tự động tạo cuộc gọi video với HR (sử dụng **Zoom API** hoặc **Microsoft Teams API**).

5. **Cập nhật yêu cầu công việc động**:
   - Sử dụng **Webhook** từ Airtable để cập nhật yêu cầu công việc khi có thay đổi.
:::

---

### 📌 **Kết luận**
Workflow này **tự động hóa toàn bộ quy trình tuyển dụng**, từ nhận ứng viên đến thông báo cho HR, chỉ trong vài giây. **AI GPT-4** đảm bảo đánh giá khách quan, **Airtable** giúp quản lý hồ sơ hiệu quả, và **Google Drive** đảm bảo bảo mật.

**Hành động ngay hôm nay:**
1. **Chuẩn bị các API Key** (Airtable, OpenAI, Google Drive, Gmail).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Test với dữ liệu mẫu** trước khi bật chế độ tự động.
4. **Tích hợp vào quy trình tuyển dụng** của doanh nghiệp!

**🚀 Cùng tự động hóa tuyển dụng, tiết kiệm thời gian và nâng cao chất lượng tuyển dụng!**