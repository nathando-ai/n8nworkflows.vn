---
title: "🚀 Tự Động Hóa Phân Tích CV & LINKEDIN Với Gemini AI + Google Workspace (Không Cần Code)"
description: "Workflow tự động thu thập thông tin ứng viên từ LinkedIn, phân tích CV bằng AI Gemini, tạo phản hồi cá nhân hóa và gửi báo cáo tự động qua email. Giúp HR tiết kiệm 80% thời gian đánh giá ứng viên."
slug: "tu-dong-hoa-phan-tich-cv-linkedin-voi-gemini"
tags: [n8n, automation, ai-summarization, hr-automation, google-workspace, gemini-ai]
keywords: [n8n workflow tự động hóa HR, phân tích CV bằng AI, LinkedIn feedback tự động, Gemini AI + Google Sheets, tự động hóa tuyển dụng không code]
---

# 🚀 **Tự Động Hóa Phân Tích CV & LinkedIn: Từ Form Đến Báo Cáo AI (Không Cần Code)**

### **🔥 Nỗi Đau Của HR & Đội Tuyển Dụng**
Các sếp HR và đội tuyển dụng thường phải:
- **Tốn thời gian** để đánh giá hàng chục CV mỗi ngày.
- **Không nhất quán** trong việc phản hồi ứng viên (một người đánh giá cao, người khác lại đánh giá thấp).
- **Không khai thác được LinkedIn** để đánh giá toàn diện ứng viên.
- **Phải làm thủ công** việc tổng hợp phản hồi và gửi báo cáo.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Thu thập** thông tin ứng viên từ form (LinkedIn, CV, email, điện thoại).
✅ **Phân tích CV** bằng AI Gemini để rút ra điểm mạnh/điểm yếu.
✅ **So sánh LinkedIn** với CV để đề xuất cải thiện hồ sơ.
✅ **Tạo báo cáo** dưới dạng Google Docs và gửi tự động qua email.
✅ **Lưu trữ** tất cả dữ liệu trong Google Sheets để theo dõi.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** đánh giá CV so với cách làm thủ công.
- **Phản hồi chính xác & cá nhân hóa** nhờ AI Gemini.
- **So sánh LinkedIn vs CV** để đề xuất cải thiện hồ sơ.
- **Báo cáo tự động** gửi qua email với link Google Docs chi tiết.
- **Lưu trữ dữ liệu** trong Google Sheets để theo dõi ứng viên.
- **Hoạt động 24/7** mà không cần can thiệp của con người.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Workspace** (Gmail, Google Sheets, Google Drive, Google Docs).
2. **API Key Google Gemini** (từ [Google AI Studio](https://aistudio.google.com/)).
3. **Credentials OAuth2** cho:
   - Google Sheets (`googleSheetsOAuth2Api`).
   - Google Drive (`googleDriveOAuth2Api`).
   - Google Docs (`googleDocsOAuth2Api`).
   - Gmail (`gmailOAuth2`).
4. **Form n8n** (để ứng viên nhập LinkedIn URL, tên, email, điện thoại và upload CV).

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/12888](https://n8n.io/workflows/12888).
- **Import vào n8n Editor**:
  - Mở n8n Dashboard → **Import Workflow** → Chọn file JSON.
  - **Hoặc** copy toàn bộ JSON vào **Create Workflow** → Paste.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow gồm **13 node**, các sếp cần chú ý cấu hình sau:

##### **📌 Node 1: "On form submission" (formTrigger)**
- **Cấu hình**:
  - Thiết lập **form fields** theo mẫu:
    - `linkedinUrl` (URL LinkedIn của ứng viên).
    - `name` (Tên ứng viên).
    - `email` (Email liên lạc).
    - `phone` (Số điện thoại).
    - `cv` (File upload CV - PDF/Docx).
  - **Lưu ý**: Các sếp có thể **copy form này** từ n8n Editor → **Create Form** → Chỉnh sửa.

##### **📌 Node 2 & 3: "Append row in sheet" + "Extract from File"**
- **Google Sheets**:
  - Chọn **Sheet Name** (ví dụ: `CV_Applications`).
  - Cấu hình **credentials** (`googleSheetsOAuth2Api`).
- **Extract from File**:
  - Chọn **operation: pdf** (nếu CV là PDF).
  - Nếu CV là Word, thay đổi thành `operation: docx`.

##### **📌 Node 4 & 6: "Google Gemini Chat Model" (AI Phân Tích)**
- **Cấu hình Prompt** (để AI trả lời):
  - **Node "Google Gemini Chat Model"**:
    ```plaintext
    Analyze this CV and provide structured feedback:
    1. Strengths (3 points)
    2. Weaknesses (3 points)
    3. Suggestions for improvement
    4. LinkedIn vs CV comparison
    ```
  - **Node "Google Gemini Chat Model1"** (để AI viết cover letter):
    ```plaintext
    Write a professional cover letter for this candidate based on their CV and LinkedIn profile.
    Keep it concise (2-3 paragraphs) and tailored to their experience.
    ```

##### **📌 Node 5, 7, 8, 9: "Google_Docs" (Tạo & Cập Nhật Báo Cáo)**
- **Cấu hình credentials**: `googleDocsOAuth2Api`.
- **Node "Google_Docs_Title"**: Đặt tiêu đề báo cáo (ví dụ: `CV Feedback for {{$node["On form submission"].json()["name"]}}`).
- **Node "Google_Docs_Body"**: Chèn nội dung từ AI vào body Google Docs.
- **Node "Google_Docs_Update"**: Cập nhật nội dung cuối cùng.

##### **📌 Node 10: "Upload file" (Lưu CV lên Google Drive)**
- Chọn **Folder** trong Google Drive để lưu CV.
- **Lưu ý**: Các sếp nên tạo **1 folder riêng** cho CV ứng viên.

##### **📌 Node 11: "Send a message" (Gửi Email Tự Động)**
- **Cấu hình**:
  - **From Email**: Địa chỉ email của HR (ví dụ: `hr@company.com`).
  - **To Email**: `$node["On form submission"].json()["email"]` (email ứng viên).
  - **Subject**: `Your CV Feedback & LinkedIn Analysis ({{$node["On form submission"].json()["name"]}})`.
  - **Body Email**:
    ```plaintext
    Dear {{$node["On form submission"].json()["name"]}},

    Thank you for applying! We’ve analyzed your CV and LinkedIn profile. Below is your feedback:

    [Google Docs Link]: {{$node["Google_Docs"].json()["documentUrl"]}}

    Best regards,
    [Your Company Name]
    ```

##### **📌 Node 12 & 13: "LinkedIn Analyst" & "Recruiter / HR" (Agent AI)**
- **Không cần chỉnh sửa** (n8n sẽ tự động gọi API Gemini thông qua node `lmChatGoogleGemini` đã cấu hình trước).

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhập **LinkedIn URL**, **tên**, **email**, **số điện thoại** và upload **CV**.
   - Kiểm tra **Google Docs** và **email** có được tạo không.
2. **Bật Active workflow**:
   - Click **Active** trên n8n Dashboard.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack Webhook** hoặc **Telegram Bot** để thông báo khi có phản hồi mới.
2. **Lưu Log Dữ Liệu**:
   - Thêm node **StickyNote** để ghi lại lịch sử phản hồi.
3. **Báo Cáo Định Kỳ**:
   - Sử dụng **Google Sheets + Apps Script** để tự động gửi báo cáo tổng hợp cho HR hàng tuần.
4. **Cải Thiện AI Prompt**:
   - Thử các **Prompt khác** cho Gemini để phù hợp với ngành nghề cụ thể (IT, Marketing, Y tế...).

---
### 📌 **Kết Luận**
Workflow này **giải phóng HR khỏi công việc lặp lại**, giúp đánh giá ứng viên **nhanh chóng, chính xác và cá nhân hóa** nhờ AI Gemini. **Không cần code**, chỉ cần **cấu hình vài bước** là có thể tự động hóa toàn bộ quy trình từ form đến báo cáo.

**🚀 Hãy thử ngay!**
1. Import workflow.
2. Cấu hình Google Workspace + API Gemini.
3. **Bật Active** và bắt đầu tự động hóa tuyển dụng!

---
**💡 Cần hỗ trợ?** Đăng ký **VPS n8n** từ [TinoHost](https://tino.vn/vps-n8n?affid=388) để workflow chạy 24/7 mà không ngừng!