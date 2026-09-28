---
title: "🤖 **Tự Động Học Sàng Lọc & Đánh Giá Ứng Viên CV với AI (Gmail + Google Drive + OpenAI + Sheets)**"
description: "Workflow tự động hóa hoàn toàn cho HR/Recruiter: Nhận CV qua email → Trích xuất nội dung → AI đánh giá ứng viên (điểm số 1-10) → Lưu kết quả vào Google Sheets. Giảm 80% thời gian sàng lọc thủ công!"
slug: "tieu-dong-hoa-sang-loc-cv-voi-ai"
tags: [n8n, automation, hr, ai-summarization, google-drive, openai, google-sheets]
keywords: [tự động hóa sàng lọc cv, ai đánh giá ứng viên, n8n workflow hr, tự động hóa recruting, sàng lọc cv với openai]
---

# 🚀 **Tự Động Học Sàng Lọc & Đánh Giá Ứng Viên CV với AI (Không Cần Code)**

### **Nỗi Đau Của Các Sếp HR**
Mỗi ngày, bộ phận HR phải:
- **Quét hàng chục CV** qua email, Google Drive, hoặc Dropbox.
- **Đọc lại và lại** những CV dài dòng, không có cấu trúc.
- **Phán đoán chủ quan** về phù hợp của ứng viên với vị trí.
- **Lưu trữ thủ công** kết quả sàng lọc vào Excel/Sheets, dễ bị lỗi hoặc mất mát.

**Kết quả?** Thời gian và năng suất bị "chôn vùi" trong công việc lặp đi lặp lại, trong khi ứng viên tiềm năng bị bỏ qua vì thiếu tiêu chí khách quan.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian sàng lọc**: AI tự động trích xuất và đánh giá CV trong vài giây.
- **Đánh giá khách quan**: Điểm số 1-10 dựa trên kỹ năng, kinh nghiệm và phù hợp với vị trí.
- **Lưu trữ tự động**: Kết quả được ghi vào Google Sheets, dễ dàng theo dõi và phân tích.
- **Cá nhân hóa**: AI cung cấp **báo cáo chi tiết** về ưu điểm, nhược điểm và giá trị tiềm năng của ứng viên.
- **Hoạt động 24/7**: Không cần can thiệp thủ công, workflow chạy liên tục ngay cả khi các sếp nghỉ ngơi.
:::

---
### **🔧 Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài Khoản Gmail** (để nhận CV từ ứng viên).
2. **Google Drive** (để lưu trữ CV tạm thời).
3. **Google Sheets** (để lưu kết quả đánh giá).
4. **API Key OpenAI** (để sử dụng mô hình AI `o4-mini`).
5. **N8n Self-hosted** (để workflow chạy ổn định 24/7).

👉 **🎁 Đăng ký VPS TinoHost (Self-hosted n8n) với mã giảm giá VPSN8N (giảm tới 39%)**:
🔗 [https://tino.vn/vps-n8n?affid=388](https://tino.vn/vps-n8n?affid=388)
:::

---
## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Cách 1: Import từ file JSON**
1. Tải workflow từ [n8n.io/workflows/13970](https://n8n.io/workflows/13970) (chọn **Export JSON**).
2. Trên **n8n Editor**, nhấn **Import** → Chọn file JSON vừa tải.
3. Chọn **Create Workflow** để hoàn tất.

#### **Cách 2: Copy/Paste JSON**
1. Copy toàn bộ mã JSON từ [n8n.io/workflows/13970](https://n8n.io/workflows/13970).
2. Trên **n8n Editor**, nhấn **Import** → Chọn **Paste JSON**.
3. Chọn **Create Workflow**.

---
### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **5 phần chính**, các sếp cần chú ý cấu hình các node sau:

#### **A. Cấu Hình Gmail Trigger (Nhận CV từ Email)**
- **Node**: `On New Candidate Email` (gmailTrigger)
- **Cấu hình**:
  - Chọn **credentials**: `gmailOAuth2` (đã cấu hình trước khi import).
  - **Label**: `CV` (để workflow chỉ nhấn vào email có nhãn "CV").
  - **Attachments**: Bật **Include attachments** (để workflow lấy được file CV).

#### **B. Cấu Hình Google Drive (Lưu CV Tạm Thời)**
- **Node**: `New CV` (googleDrive)
- **Cấu hình**:
  - **Credentials**: `googleDriveOAuth2Api`.
  - **Folder ID**: Thêm ID của folder Google Drive bạn muốn lưu CV (một folder riêng cho CV tạm).
  - **File Name**: Đặt tên theo định dạng: `CV_[Candidate Name]_[Date]`.

#### **C. Cấu Hình OpenAI API (AI Đánh Giá CV)**
- **Node**: `OpenAI Chat Model` (lmChatOpenAi)
- **Cấu hình**:
  - **Credentials**: `openAiApi` (đã cấu hình API Key OpenAI).
  - **Model**: Chọn `o4-mini` (mô hình hiệu quả cho đánh giá CV).
  - **Prompt**: Đảm bảo prompt đã được cấu hình để AI đánh giá:
    ```json
    "prompt": "Analyze the candidate's CV and provide a structured evaluation including:
    - Strengths (3 points)
    - Weaknesses (3 points)
    - Skills and experience (bullet points)
    - Suitability score (1-10)
    - Potential value for the company"
    ```

#### **D. Cấu Hình Google Sheets (Lưu Kết Quả)**
- **Node**: `new candidate created` (googleSheets)
- **Cấu hình**:
  - **Credentials**: `googleSheetsOAuth2Api`.
  - **Sheet Name**: Đặt tên sheet (ví dụ: `Candidate Evaluations`).
  - **Headers**: Đảm bảo cột trong Sheets phù hợp với dữ liệu AI trả về (ví dụ: `Candidate Name`, `Score`, `Strengths`, `Weaknesses`).

#### **E. Cấu Hình File Type Detection (Xác Định Loại File CV)**
- **Node**: `Route by File Type` (switch)
- **Cấu hình**:
  - **Condition**: Kiểm tra `file.type` (PDF, DOCX, TXT).
  - **Route**:
    - Nếu PDF → `Parse PDF Content`.
    - Nếu DOCX → `Parse Word Content`.
    - Nếu TXT → `Parse Text Content`.

---
### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run** với một CV mẫu:
   - Gửi một CV mẫu (PDF/DOCX/TXT) đến email đã cấu hình.
   - Kiểm tra **Google Sheets** xem kết quả có xuất hiện không.
2. **Bật Active**:
   - Nhấn **Active** trên workflow để nó bắt đầu chạy tự động.

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**
### **1. Tích Hợp Slack/Telegram để Báo Lệch**
- Thêm **node Slack/Telegram** sau khi AI đánh giá để thông báo kết quả cho team:
  ```json
  {
    "name": "Notify Team",
    "type": "slackWebhook",
    "credentials": ["slackWebhookApi"],
    "keyParameters": {
      "text": "New candidate evaluated! Score: {{ $json["score"] }}"
    }
  }
  ```

### **2. Lưu Log Lịch Sử Đánh Giá**
- Thêm **node Google Drive** để lưu file CV đã đánh giá vào một folder riêng:
  ```json
  {
    "name": "Save Evaluated CV",
    "type": "googleDrive",
    "credentials": ["googleDriveOAuth2Api"],
    "keyParameters": {
      "operation": "upload",
      "folderId": "FOLDER_ID_EVALUATED"
    }
  }
  ```

### **3. Gửi Báo Cáo Định Kỳ cho HR**
- Sử dụng **node Google Sheets** để tạo báo cáo tổng hợp hàng tuần/month:
  ```json
  {
    "name": "Generate Weekly Report",
    "type": "googleSheets",
    "credentials": ["googleSheetsOAuth2Api"],
    "keyParameters": {
      "operation": "append",
      "sheetName": "Weekly Reports",
      "headers": ["Week", "Total Candidates", "Avg Score"]
    }
  }
  ```

### **4. Cập Nhật Prompt AI cho Đánh Giá Chuyên Nghiệp**
- Nếu cần đánh giá cho vị trí cụ thể (ví dụ: Developer, Designer), cập nhật prompt:
  ```json
  "prompt": "Evaluate this CV for a [Job Title] position. Focus on:
  - Technical skills (for developers: Python, JavaScript, etc.)
  - Portfolio/Projects (for designers: UI/UX, branding)
  - Cultural fit (teamwork, communication)"
  ```

---
## **📌 Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp HR khỏi công việc lặp đi lặp lại, đồng thời **cung cấp đánh giá khách quan** dựa trên AI. Với **Google Drive, OpenAI và Google Sheets**, bạn có thể:
✅ **Nhận CV tự động** từ email.
✅ **AI trích xuất và đánh giá** trong vài giây.
✅ **Lưu kết quả** vào Sheets để theo dõi dễ dàng.
✅ **Tích hợp thêm Slack/Telegram** để thông báo kết quả.

**🚀 Hãy áp dụng ngay và bắt đầu tự động hóa sàng lọc CV của bạn!**
Nếu có vấn đề, các sếp có thể tham khảo [hướng dẫn chi tiết của Stefan Joulien](https://n8n.io/workflows/13970) hoặc liên hệ với cộng đồng n8n trên [Discord](https://discord.gg/n8n).

---
**🎁 Đăng ký VPS TinoHost để self-host n8n (chạy 24/7):**
🔗 [https://tino.vn/vps-n8n?affid=388](https://tino.vn/vps-n8n?affid=388) (Mã giảm giá: **VPSN8N**)