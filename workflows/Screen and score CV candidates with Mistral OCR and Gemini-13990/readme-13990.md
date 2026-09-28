---
title: "🚀 **Tự Động Hóa Xét Duyệt & Đánh Giá CV Tự Động Với Mistral OCR + Gemini AI (Không Cần Code!)**"
description: "Workflow tự động hóa hoàn toàn cho doanh nghiệp HR: Nhận CV qua email → Trích xuất nội dung PDF (đã quét hoặc kỹ thuật số) → Đánh giá tự động bằng AI → Phân loại ứng viên vào danh sách shortlist hoặc từ chối một cách chuyên nghiệp. Tiết kiệm 80% thời gian xét duyệt CV!"
slug: "tieu-dong-hoa-xet-duyet-cv-voi-mistral-ocr-gemini"
tags: [n8n, automation, hr, ai-summarization, mistral-ocr, google-gemini, email-automation]
keywords: [tự động hóa xét duyệt cv, mistral ocr n8n, gemini ai đánh giá cv, workflow hr không code, tự động hóa nhắn tin email cv]
---

# 🚀 **Tự Động Hóa Xét Duyệt CV: Từ Nhận Email Đến Phân Loại Ứng Viên Với AI (Mistral + Gemini)**

### **Nỗi Đau Của Các Sếp HR**
Hàng ngày, các sếp HR phải:
- **Quét và trích xuất** hàng trăm CV từ PDF (đặc biệt là CV đã quét).
- **Đọc lặp đi lặp lại** cùng một thông tin để so sánh với yêu cầu công việc (JD).
- **Phân loại ứng viên** một cách chủ quan, dẫn đến rủi ro bỏ lỡ tài năng hoặc chọn sai người.
- **Gửi email phản hồi** cho từng ứng viên, mất thời gian và dễ gây nhầm lẫn.

**Workflow này giải quyết tất cả!** Với **AI OCR + Gemini AI**, các sếp chỉ cần **nhấn một nút** để:
✅ **Trích xuất toàn bộ nội dung** từ CV PDF (đã quét hoặc kỹ thuật số).
✅ **Đánh giá tự động** CV so với yêu cầu công việc (JD) và trả về **điểm số, quyết định shortlist/reject**.
✅ **Gửi email tự động** cho HR và ứng viên (mời phỏng vấn hoặc từ chối một cách chuyên nghiệp).
✅ **Tiết kiệm 8+ giờ/ngày** cho đội HR!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng. Đây là giải pháp an toàn, không phụ thuộc vào cloud và có thể mở rộng dễ dàng.

👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ sức mạnh cho workflow AI)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** trong quá trình xét duyệt CV.
- **Chính xác cao** với AI đánh giá theo tiêu chí cụ thể (không phụ thuộc vào cảm xúc).
- **Cá nhân hóa email** cho từng ứng viên (mời phỏng vấn hoặc từ chối một cách chuyên nghiệp).
- **Hoạt động liên tục 24/7** (không cần can thiệp thủ công).
- **Giảm rủi ro bỏ lỡ tài năng** nhờ AI phân tích toàn diện.
- **Dễ dàng mở rộng** cho nhiều vị trí tuyển dụng khác nhau.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Email IMAP** (để n8n theo dõi hộp thư nhận CV).
   - **Thông tin cần thiết**:
     - Host IMAP (ví dụ: `imap.gmail.com`).
     - Port (thường là `993`).
     - Username & Password (hoặc App Password nếu sử dụng Gmail).
     - Folder INBOX (để workflow theo dõi).

2. **API Key Mistral Cloud** (để trích xuất văn bản từ PDF).
   - **Lấy tại**: [Mistral AI Developer Portal](https://console.mistral.ai/).
   - **Model sử dụng**: `mistral-ocr-latest` (hoạt động với cả PDF kỹ thuật số và đã quét).

3. **API Key Google Palm API** (để Gemini AI đánh giá CV).
   - **Lấy tại**: [Google Cloud Console](https://console.cloud.google.com/).
   - **Model sử dụng**: `gemini-3.1-flash-lite-preview` (nhẹ và hiệu quả).

4. **Thông tin SMTP** (để gửi email phản hồi).
   - **Thông tin cần thiết**:
     - Host SMTP (ví dụ: `smtp.gmail.com`).
     - Port (thường là `587`).
     - Username & Password (hoặc App Password).
     - Sender Email (địa chỉ email gửi phản hồi).

5. **Yêu cầu công việc (Job Description - JD)**:
   - **Định dạng**: Văn bản hoặc file PDF (n8n sẽ tự động trích xuất).
   - **Nội dung**: Mô tả chi tiết vị trí tuyển dụng (kỹ năng, kinh nghiệm, tiêu chí đánh giá).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow này:
- **Tải file JSON** từ [n8n.io/workflows/13990](https://n8n.io/workflows/13990) và import vào **n8n Editor**.
- **Copy toàn bộ JSON** từ link trên và **dán vào Editor** của n8n (tab "Import").

🔹 **Lưu ý**:
- Mở **n8n Editor** (trang chủ của n8n).
- Chọn **"Import"** và chọn file JSON hoặc dán JSON từ link.
- **Không cần chỉnh sửa** cấu trúc node, chỉ cần **cấu hình credentials** (xem phần sau).

---

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **8 node chính**, nhưng **các node sau cần cấu hình kỹ lưỡng**:

##### **📧 Node 1: Watch Inbox for CV Emails (emailReadImap)**
- **Cấu hình**:
  - **Credentials**: Chọn `imap` (đã tạo trước).
  - **Folder**: Chọn `INBOX`.
  - **Attachments**: Bật `ON` (để lưu CV làm file đính kèm).
  - **Action**: Bật `Mark as Read` (để email không bị lặp lại).
- **Test**: Gửi một email mẫu (có đính kèm CV PDF) và kiểm tra node này có hoạt động không.

##### **📄 Node 2: OCR: Extract CV Text (mistralAi)**
- **Cấu hình**:
  - **Credentials**: Chọn `mistralCloudApi`.
  - **Model**: Đặt là `mistral-ocr-latest`.
  - **Input**: Chọn `attachment_0` (CV từ node trước).
  - **Output**: Bật `ON` (để lưu kết quả trích xuất).
- **Test**: Kiểm tra node này có trích xuất được văn bản từ PDF không.

##### **🤖 Node 3: AI Score CV (googleGemini)**
- **Cấu hình**:
  - **Credentials**: Chọn `googlePalmApi`.
  - **Model**: Đặt là `gemini-3.1-flash-lite-preview`.
  - **Input**:
    - Chọn `json` từ node OCR (nội dung trích xuất).
    - **Thêm JD** (Job Description) vào prompt (ví dụ: `"Evaluate this CV against the following JD: [nội dung JD]"`).
  - **Output**: Bật `JSON Output mode` (để AI trả về định dạng JSON).
- **Test**: Kiểm tra AI có trả về kết quả như:
  ```json
  {
    "score": 85,
    "decision": "shortlisted",
    "name": "Nguyễn Văn A",
    "summary": "Kỹ sư Fullstack với 5 năm kinh nghiệm...",
    "key_skills": ["React", "Node.js", "AWS"]
  }
  ```

##### **⚙️ Node 4: Parse AI Response + Pass Binary (code)**
- **Lưu ý quan trọng**:
  - Node này **xóa dấu nháy Markdown** (` ```json `) từ output của Gemini.
  - **Phân tích JSON** thành các trường riêng biệt (`score`, `decision`, `name`, ...).
  - **Giữ nguyên file đính kèm** (`binary`) từ node IMAP để sử dụng trong email sau.
- **Mã mẫu** (nếu cần chỉnh sửa):
  ```javascript
  // Xóa dấu nháy Markdown
  const jsonStr = $input.all().json.markdown_fenced ? $input.all().json.markdown_fenced.replace(/```json\n|\n```/g, '') : $input.all().json;

  // Parse JSON
  const parsedJson = JSON.parse(jsonStr);

  // Trả về các trường riêng biệt
  return {
    json: parsedJson,
    binary: $input.all().binary // Giữ file đính kèm
  };
  ```

##### **🔀 Node 5: Shortlisted or Rejected? (if)**
- **Cấu hình**:
  - **Condition**: `$json.decision === "shortlisted"`.
  - **True Branch**: Chạy node HR notification + candidate invite.
  - **False Branch**: Chạy node decline email.

##### **📧 Node 6-8: Email Notification (emailSend)**
- **Cấu hình chung**:
  - **Credentials**: Chọn `smtp`.
  - **Subject**:
    - **HR Notification**: `"[HR] CV Shortlisted: [Tên ứng viên] - Score: [điểm]`".
    - **Candidate Invite**: `"Mời phỏng vấn cho vị trí [Tên vị trí]"`.
    - **Decline Email**: `"Cảm ơn vì sự quan tâm - Vị trí đã được đóng"`.
  - **Body**:
    - **HR Notification**: Gồm `summary`, `key_skills`, `score`, và **đính kèm CV**.
    - **Candidate Invite**: Gồm `summary`, `key_skills`, và **link lịch phỏng vấn** (cập nhật `YOUR_CALENDLY_OR_CAL_LINK_HERE`).
    - **Decline Email**: Tôn trọng và khuyến khích ứng viên theo dõi vị trí khác.
  - **Test**: Gửi email mẫu để kiểm tra định dạng.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Gửi một email mẫu (có CV PDF) vào INBOX.
   - Kiểm tra từng node có hoạt động không (đặc biệt là **OCR, AI Scoring, và Email**).
2. **Bật Active**:
   - Sau khi test thành công, **bật workflow** và **để nó chạy tự động**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tích Hợp với Calendly/Google Calendar**:
   - Thay thế `YOUR_CALENDLY_OR_CAL_LINK_HERE` bằng **link lịch phỏng vấn tự động** từ Calendly hoặc Google Calendar.
   - **Cách làm**:
     - Tạo một **link lịch** trong Calendly/Google Calendar.
     - Thêm link này vào email mời phỏng vấn.

2. **Lưu Log Tất Cả Các CV**:
   - Thêm node **`stickyNote`** hoặc **`database`** (n8n Database) để lưu tất cả CV đã xử lý.
   - **Ưu điểm**: Dễ dàng theo dõi lịch sử và phân tích dữ liệu.

3. **Tự Động Gửi Báo Cáo Định Kỳ**:
   - Thêm node **`emailSend`** mới để gửi **báo cáo hàng tuần** cho HR:
     - Danh sách ứng viên shortlist/reject.
     - Số lượng CV đã xử lý.
     - Thống kê điểm số trung bình.

4. **Cập Nhật JD Tự Động**:
   - Nếu JD thay đổi, **cập nhật lại prompt** trong node Gemini.
   - **Mẹo**: Sử dụng **`stickyNote`** để lưu JD và gọi lại trong node AI.

5. **Kết Hợp với Slack/Telegram**:
   - Thêm node **`slackSend`** hoặc **`telegramSend`** để thông báo kết quả ngay khi có CV mới.
   - **Cách làm**:
     - Tạo một **webhook** từ Slack/Telegram.
     - Thêm node `slackSend` sau node `if` để gửi tin nhắn khi có quyết định.

---

### 📌 **Kết Luận**
Workflow này **giải phóng đội HR khỏi công việc lặp lại**, giúp các sếp:
✔ **Tiết kiệm thời gian** để tập trung vào việc phỏng vấn và xây dựng văn hóa công ty.
✔ **Tăng chất lượng tuyển dụng** nhờ AI đánh giá khách quan.
✔ **Cải thiện trải nghiệm ứng viên** với email phản hồi chuyên nghiệp.

**Hành động ngay!**
1. **Import workflow** và cấu hình credentials.
2. **Test với email mẫu** để đảm bảo hoạt động.
3. **Bật workflow** và **nhận CV tự động**!

👉 **[Tải workflow này ngay](https://n8n.io/workflows/13990)** và bắt đầu tự động hóa tuyển dụng của bạn!

---
**Cần hỗ trợ?** Đừng ngần ngại liên hệ với [AppStoneLab Technologies](https://appstonelab.com/) để được tư vấn chi tiết! 🚀