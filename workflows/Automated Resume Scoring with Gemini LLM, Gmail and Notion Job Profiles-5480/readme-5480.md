---
title: "🚀 Tự Động Đánh Giá CV với Gemini AI, Gmail & Notion - Giải Pháp HR Không Cần Code"
description: "Workflow tự động hóa đánh giá phù hợp ứng viên dựa trên CV email, so sánh với mô tả công việc trên Notion, và ghi nhận kết quả vào Google Sheets - tiết kiệm thời gian tuyển dụng lên đến 80%."
slug: "tieu-dong-danh-gia-cv-voi-gemini-ai-gmail-notion"
tags: [n8n, automation, hr, ai-summarization, google-gemini, google-sheets, notion]
keywords: [tự động hóa tuyển dụng, đánh giá cv bằng ai, gemini llm n8n, workflow hr không code, tự động hóa gmail và notion]
---

# 🚀 **Tự Động Đánh Giá CV với Gemini AI, Gmail & Notion: Giải Pháp HR Không Cần Code**

### **🔍 Nỗi Đau Của Các Sếp Trong Tuyển Dụng**
Tuyển dụng là một quá trình tốn thời gian và dễ mắc sai lầm. Các sếp thường phải:
- **Lọc hàng trăm CV** thủ công, mất từ 3-5 giờ/ngày.
- **Đánh giá phù hợp ứng viên** dựa trên kinh nghiệm, kỹ năng và mô tả công việc, dễ bị chủ quan.
- **Trùng lặp dữ liệu** khi ghi chép thông tin vào Google Sheets hoặc Notion.
- **Quên theo dõi ứng viên** sau khi gửi phản hồi, dẫn đến mất cơ hội tuyển dụng.

**Workflow này giải quyết tất cả đó!** Với **Gemini AI**, nó tự động **trích xuất thông tin CV**, **so sánh với mô tả công việc trên Notion**, và **đánh giá phù hợp ứng viên** chỉ trong vài giây. Kết quả được **ghi vào Google Sheets** và **dán nhãn vào email** để tránh trùng lặp.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Lọc và đánh giá **50+ CV/ngày** chỉ trong vài phút.
✅ **Độ chính xác cao**: Gemini AI trích xuất thông tin chính xác hơn so với con người.
✅ **Tránh trùng lặp**: Ghi nhãn tự động vào email và cập nhật Google Sheets.
✅ **Tối ưu tuyển dụng**: So sánh ứng viên với mô tả công việc trên Notion.
✅ **Hoạt động liên tục**: Workflow chạy tự động mỗi khi có email CV mới.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google** (Gmail + Google Sheets + Google Gemini API).
2. **Tài khoản Notion** (Database chứa mô tả công việc).
3. **API Keys**:
   - **Google Gemini API** (đăng ký tại [Google AI Studio](https://makersuite.google.com/)).
   - **LlamaParse API** (đăng ký tại [LlamaParse](https://llamaparse.com/)).
4. **Credentials trong n8n**:
   - `gmailOAuth2` (để lấy email CV).
   - `googleSheetsOAuth2Api` (cập nhật kết quả).
   - `notionApi` (truy cập mô tả công việc).
   - `googlePalmApi` (đối với Gemini).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/5480](https://n8n.io/workflows/5480).
- **Mở n8n Editor** → Nhấn **"Import"** → Chọn file JSON.
- **Hoặc copy/paste** JSON vào ô **"Import Workflow"** trong Editor.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow gồm **16 node**, nhưng các node **quan trọng nhất** cần cấu hình kỹ:

##### **🔹 Node "Gmail Trigger" (gmailTrigger)**
- **Chọn credentials**: `gmailOAuth2`.
- **Cấu hình**:
  - **Subject**: Đặt tên chủ đề email nhận CV (ví dụ: *"CV - [Tên Ứng Viên]"*).
  - **Label**: Đặt nhãn để phân loại email (ví dụ: *"CV_Received"*).

##### **🔹 Node "Upload to LlamaParse" & "Get Parsed Resume" (httpRequest)**
- **Credentials**: `httpBearerAuth` (API Key của LlamaParse).
- **Headers**:
  - `Authorization: Bearer YOUR_LLAMAPARSE_API_KEY`
  - `Content-Type: application/json`
- **Body (Upload to LlamaParse)**:
  ```json
  {
    "url": "https://docs.google.com/document/d/{{$node["Gmail Trigger"].json["url"]}}/export?format=pdf",
    "outputFormat": "pdf"
  }
  ```
  *(Thay `{{$node["Gmail Trigger"].json["url"]}}` bằng đường dẫn file PDF từ email.)*

##### **🔹 Node "Get Job Profile" (notion)**
- **Credentials**: `notionApi`.
- **Database Name**: Đặt tên database Notion chứa mô tả công việc (ví dụ: *"Job Descriptions"*).
- **Page ID**: Lấy từ URL Notion (ví dụ: `{{$node["Get Job Profile"].json["id"]}}`).

##### **🔹 Node "Google Gemini Chat Model" (lmChatGoogleGemini)**
- **Credentials**: `googlePalmApi`.
- **Prompt mẫu** (cần tùy chỉnh):
  ```plaintext
  Analyze the candidate's resume and compare it with the job profile from Notion.
  Score the candidate on a scale of 1-10 based on:
  - Professional Experience (40%)
  - Education (30%)
  - Skills (20%)
  - Soft Skills (10%)
  Return the result in JSON format: {"score": X, "matchPercentage": Y, "recommendation": "HIGH/MID/LOW"}
  ```

##### **🔹 Node "Update Gsheet" (googleSheets)**
- **Credentials**: `googleSheetsOAuth2Api`.
- **Sheet Name**: Đặt tên sheet (ví dụ: *"Candidate Scores"*).
- **Columns**: Cần có cột `Email`, `Name`, `Score`, `Match%`, `Recommendation`.

##### **🔹 Node "Add label to message" (gmail)**
- **Credentials**: `gmailOAuth2`.
- **Label**: Đặt nhãn tự động (ví dụ: *"SCORED_HIGH"* hoặc *"SCORED_LOW"*).

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Gửi email CV mẫu với chủ đề đã cấu hình.
  - Kiểm tra **Google Sheets** và **Notion** có cập nhật dữ liệu không.
- **Bật Active**:
  - Nhấn **"Active"** trên workflow.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tích Hợp Slack/Telegram**:
   - Thêm node **Slack Webhook** để thông báo kết quả đánh giá.
   - Ví dụ: *"CV của [Tên] đã được đánh giá: Score 8.5/10 (HIGH)"*.

2. **Lưu Log Tất Cả Các Lần Đánh Giá**:
   - Sử dụng node **StickyNote** để ghi lại lịch sử đánh giá.
   - Cập nhật vào **Google Sheets** với cột `Last Updated`.

3. **Tự Động Gửi Email Phản Hồi**:
   - Thêm node **Gmail Send Email** để tự động gửi phản hồi cho ứng viên.
   - Nội dung: *"Chúng tôi đã đánh giá CV của bạn và kết quả là [Score]. Chúng tôi sẽ liên hệ lại trong 24h."*

4. **Cập Nhật Mô Hình Gemini**:
   - Nếu muốn cải thiện độ chính xác, thử **Prompt Engineering** với Gemini.
   - Ví dụ: *"Hãy so sánh kỹ hơn về kỹ năng cụ thể trong mô tả công việc."*

5. **Tự Động Xóa Email Sau Đánh Giá**:
   - Thêm node **Gmail Delete Email** để xóa email CV sau khi xử lý.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc lặp lại trong tuyển dụng, đồng thời **tăng độ chính xác** nhờ AI. **Chỉ cần import, cấu hình và bật chạy** - workflow sẽ tự động:
✔ **Lấy CV từ email**.
✔ **Trích xuất thông tin** (thông tin cá nhân, chuyên môn, học vấn).
✔ **Đánh giá phù hợp ứng viên** so với mô tả công việc.
✔ **Ghi kết quả vào Google Sheets** và **dán nhãn vào email**.

**🚀 Hãy áp dụng ngay và bắt đầu tự động hóa tuyển dụng của bạn!**
Nếu có vấn đề, hãy để lại comment dưới đây hoặc liên hệ **Agentick AI** qua [n8n.io](https://n8n.io/).

---