---
title: "🤖 Tự Động Hóa Quá Trình Phỏng Vấn HR Với AI TruGen + OpenAI & Google Sheets (Không Cần Code)"
description: "Workflow tự động hóa toàn bộ quy trình phỏng vấn video AI, từ tạo ra AI phỏng vấn dựa trên mô tả công việc, ghi lại phản hồi ứng viên, đến phân tích sâu bằng AI và lưu kết quả vào Google Sheets. Giúp HR tiết kiệm 80% thời gian đánh giá ứng viên và giảm thiểu thiên kiến."
slug: "tự-dộng-hoa-phỏng-van-hr-ai-trugen-openai-google-sheets"
tags: [n8n, automation, hr, ai-chatbot, trugen-ai, openai, google-sheets, no-code]
keywords: [n8n workflow phỏng vấn, tự động hóa HR, AI phỏng vấn video, TruGen AI, OpenAI API, Google Sheets tự động hóa]
---

# 🚀 **Tự Động Hóa Quá Trình Phỏng Vấn HR Với AI TruGen + OpenAI & Google Sheets**

## **Giải Phóng Tay HR: Từ Phỏng Vấn Thủ Công Đến AI Tự Động Hóa 24/7**
Hiện nay, quá trình phỏng vấn ứng viên vẫn còn nhiều bước thủ công tốn thời gian: **ghi chép phản hồi, đánh giá một cách chủ quan, lưu trữ kết quả rải rác**. Kết quả là HR phải mất **gần 3-5 tiếng** để đánh giá một ứng viên, và dễ mắc sai lầm do thiên kiến cá nhân.

**Workflow này giải quyết tất cả:**
✅ **Tạo AI phỏng vấn** dựa trên mô tả công việc của bạn (chỉ cần copy/paste).
✅ **Ghi lại toàn bộ cuộc phỏng vấn** dưới dạng văn bản thời gian thực.
✅ **Phân tích sâu bằng AI** (OpenAI) để đánh giá kỹ năng, điểm mạnh/điểm yếu, và đưa ra kết quả khách quan.
✅ **Lưu kết quả vào Google Sheets** với định dạng chuyên nghiệp, sẵn sàng chia sẻ với team.

Kết quả? **HR tiết kiệm 80% thời gian, giảm thiểu sai sót, và có quyết định tuyển dụng dựa trên dữ liệu chứ không phải cảm xúc.**

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** đánh giá ứng viên (không cần ghi chép thủ công).
- **Đánh giá khách quan** với AI phân tích kỹ năng, điểm mạnh/điểm yếu, và đưa ra kết quả số liệu (fit score 0-100).
- **Lưu trữ kết quả chuyên nghiệp** vào Google Sheets, sẵn sàng chia sẻ với team hoặc hệ thống HRM.
- **Hoạt động 24/7** – ứng viên có thể phỏng vấn bất kỳ thời gian nào, không phụ thuộc vào lịch HR.
- **Giảm thiên kiến** – AI đánh giá dựa trên nội dung chứ không phải cảm xúc cá nhân.
- **Tích hợp với TruGen AI** – ứng viên phỏng vấn qua video/voice thời gian thực, không cần HR trực tiếp.
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **TruGen API Key**
   - Đăng ký tại [TruGen AI](https://app.trugen.ai/) và lấy **API Key** từ **Dashboard → Settings**.
   - Thêm vào **Credentials** của n8n với tên: `trugenApi`.

2. **OpenAI API Key**
   - Đăng ký tại [OpenAI](https://platform.openai.com/) và lấy **API Key** từ **Account → API Keys**.
   - Thêm vào **Credentials** của n8n với tên: `openAiApi`.

3. **Google Sheets OAuth 2.0**
   - Tạo một **Google Workspace** (Gmail + Google Drive).
   - Thêm vào **Credentials** của n8n với tên: `googleSheetsOAuth2Api`.

4. **Mô Tả Công Việc (Job Description)**
   - Chuẩn bị **mô tả công việc chi tiết** (tên vị trí, nhiệm vụ, yêu cầu kỹ năng, tiêu chí đánh giá).
   - Sẽ được sử dụng để tạo AI phỏng vấn.

5. **Google Sheet Template**
   - Sử dụng **template đã cung cấp** (link trong hướng dẫn) hoặc tạo mới với **2 sheet**:
     - **Interview Agents** (lưu thông tin AI phỏng vấn).
     - **Interview Results** (lưu kết quả phân tích ứng viên).
:::

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/16033](https://n8n.io/workflows/16033) và import vào n8n Editor.
- **Cách 2:** Copy toàn bộ JSON từ link trên và **paste** vào **Import Workflow** trong n8n.

:::note[LƯU Ý]
- **Không** sử dụng phiên bản n8n cũ (n8n 1.x). Workflow này yêu cầu **n8n 2.x**.
- Nếu import lỗi, **xóa và tạo lại** các node `Set` và `Code` (nếu có).
:::

---

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**

#### **🔹 Node 1: 📝 Your Job Description (Code)**
- **Điền mô tả công việc** vào phần `javascript` của node:
  ```javascript
  return {
    jobDescription: "Tên vị trí: [Ví dụ: Developer Backend]\n
    Công ty: [Tên công ty]\n
    Nhiệm vụ chính: [Danh sách nhiệm vụ]\n
    Yêu cầu kỹ năng: [Python, SQL, Docker, ...]\n
    Tiêu chí đánh giá: [Cần có kinh nghiệm 2+ năm, khả năng giải quyết vấn đề, ...]"
  };
  ```
- **Lưu ý:** Mô tả càng chi tiết, AI phỏng vấn càng phù hợp.

#### **🔹 Node 2: ▶️ Click to Start Setup (Manual Trigger)**
- **Chỉ cần click 1 lần** để tạo AI phỏng vấn.
- Sau khi click, node **Save Agent Info** sẽ lưu **Agent ID** và **Job Description** vào Google Sheets.

#### **🔹 Node 3 & 4: Prepare Interview Agent & Save Agent Info (Set & Code)**
- **Không cần chỉnh sửa** nếu đã import từ file JSON.
- Node này tự động tạo **AI phỏng vấn** và lưu thông tin vào Google Sheets.

#### **🔹 Node 5 & 7: Save to Google Sheets (GoogleSheets)**
- **Chọn sheet đúng:**
  - **Save Agent Info** → Sheet **Interview Agents**.
  - **Save to Google Sheets (Analysis)** → Sheet **Interview Results**.
- **Cấu hình:**
  - **Spreadsheet ID:** Copy từ URL Google Sheets (ví dụ: `1_hqZsoN92-F7teX5sBkvb-BJ8U_6jTsJP90hOQKUE4c`).
  - **Sheet Name:** Đảm bảo đúng tên (`Interview Agents` hoặc `Interview Results`).
  - **Operation:** Chọn `append` (thêm mới).

#### **🔹 Node 6: Analyze Interview (OpenAI)**
- **Không cần chỉnh sửa** nếu đã có `openAiApi` trong Credentials.
- AI sẽ phân tích:
  - **Fit Score (0-100)** – Đánh giá phù hợp với vị trí.
  - **Hiring Recommendation** – Gợi ý tuyển dụng (strong_hire, hire, borderline, reject).
  - **Điểm mạnh/điểm yếu** với bằng chứng từ cuộc phỏng vấn.
  - **Suggested Next Steps** – Gợi ý bước tiếp theo trong quy trình tuyển dụng.

#### **🔹 Node 8: Format for Sheets (Code)**
- **Không cần chỉnh sửa** (node này tự động định dạng kết quả thành JSON phù hợp với Google Sheets).

#### **🔹 Node 9 & 10: TruGen (TruGen AI)**
- **Không cần chỉnh sửa** nếu đã có `trugenApi` trong Credentials.
- Node này:
  - **TruGen (Node 9):** Tạo cuộc phỏng vấn mới.
  - **TruGen1 (Node 10):** Lấy lại cuộc phỏng vấn đã kết thúc (quan trọng cho phân tích).

#### **🔹 Node 11: Webhook (Webhook)**
- **Cấu hình Webhook trong TruGen:**
  1. Mở **TruGen Dashboard → Create Agent**.
  2. Trong **Callback URL**, paste URL từ node Webhook (ví dụ: `https://your-n8n-server/webhook/a5b6faad-8f40-4639-8a10-af4d939c88e3`).
  3. Chọn **Callback Event:** `Call Ended`.
- **Lưu ý:** Nếu không cấu hình Webhook, cuộc phỏng vấn sẽ **không được phân tích tự động**.

---

### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run (Nếu cần):**
   - Click **Run Workflow** với dữ liệu mẫu để kiểm tra.
2. **Bật Active:**
   - Chuyển trạng thái workflow thành **Active**.
3. **Chia Sẻ Link Phỏng Vấn:**
   - Sau khi setup xong, **AI phỏng vấn** sẽ có link như:
     `https://app.trugen.ai/agent/[agent-id]`
   - Chia sẻ link này cho ứng viên.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**

### **🔹 Tích Hợp Slack/Telegram để Báo Cáo Kết Quả**
- Sử dụng node **Slack** hoặc **Telegram Bot** để gửi **tin nhắn tự động** khi:
  - AI phỏng vấn được tạo thành công.
  - Cuộc phỏng vấn kết thúc và kết quả phân tích sẵn sàng.
- **Cách làm:**
  1. Thêm node **Slack** hoặc **Telegram Bot** vào workflow.
  2. Kết nối với **Credentials** của Slack/Telegram.
  3. Sử dụng **Set** node để định dạng tin nhắn:
     ```json
     {
       "text": "🚀 Kết quả phỏng vấn ứng viên [Tên Ứng Viên] đã sẵn sàng!\n
       - Fit Score: [Score]\n
       - Gợi ý: [strong_hire/hire/borderline/reject]\n
       - Link kết quả: [Google Sheets Link]"
     }
     ```

### **🔹 Lưu Log Phỏng Vấn vào Database (Ngoài Google Sheets)**
- Nếu muốn **lưu trữ lâu dài**, thêm node **Database** (MySQL, PostgreSQL) hoặc **Airtable** để lưu:
  - Thông tin ứng viên.
  - Kết quả phỏng vấn.
  - Lịch sử tương tác.

### **🔹 Tự Động Gửi Báo Cáo Định Kỳ cho Team**
- Sử dụng **n8n Scheduler** để:
  - **Tạo báo cáo tuần/month** về số lượng ứng viên phỏng vấn.
  - **Tổng hợp kết quả** từ Google Sheets.
  - **Gửi email** hoặc **Slack notification** cho team HR.

### **🔹 Cập Nhật Mô Tả Công Việc Mới**
- Khi có **mô tả công việc mới**, chỉ cần:
  1. Chỉnh sửa node **📝 Your Job Description**.
  2. Click lại **▶️ Click to Start Setup**.
  3. AI phỏng vấn sẽ **cập nhật tự động** với mô tả mới.

---

## 📌 **Kết Luận: Áp Dụng Ngay Để Tiết Kiệm Thời Gian & Tăng Chất Lượng Tuyển Dụng**

Workflow này **giải phóng HR khỏi công việc thủ công tẻ nhạt**, giúp:
✔ **Tiết kiệm 80% thời gian** đánh giá ứng viên.
✔ **Giảm thiên kiến** với AI phân tích khách quan.
✔ **Lưu trữ kết quả chuyên nghiệp** vào Google Sheets.
✔ **Hoạt động 24/7** – ứng viên phỏng vấn bất kỳ thời gian nào.

**Bước đầu tiên:**
1. **Import workflow** từ [n8n.io/workflows/16033](https://n8n.io/workflows/16033).
2. **Cấu hình API Keys** (TruGen, OpenAI, Google Sheets).
3. **Chia sẻ link phỏng vấn** cho ứng viên và **nhận kết quả tự động**!

**👉 [Đăng ký VPS TinoHost để self-host n8n 24/7](https://tino.vn/vps-n8n?affid=388) (Mã giảm giá: **VPSN8N** - giảm tới 39%)**

---
**Hỏi gì về workflow này, các sếp có thể comment bên dưới!** 🚀