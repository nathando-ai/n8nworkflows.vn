---
title: "🤖 **Tự Động Hóa Xét Lựa CV + Phỏng Vấn Hành Vi với AI (Gemini, ElevenLabs & Notion ATS) – Giảm 90% Thời Gian Làm CV**"
description: "Workflow này tự động phân tích CV, so sánh với mô tả công việc, tiến hành phỏng vấn hành vi bằng AI, và cập nhật hồ sơ ứng viên vào Notion ATS – giúp các sếp tiết kiệm 90% thời gian làm CV và đánh giá ứng viên chính xác hơn."
slug: "tieu-dong-hoa-xet-lua-cv-voi-gemini-elevenlabs-notion-ats"
tags: [n8n, automation, hr, ai, gemini, elevenlabs, notion, google-sheets, no-code]
keywords: [tự động hóa tuyển dụng, gemini ai tuyển dụng, phỏng vấn hành vi bằng ai, notion ats, n8n workflow tuyển dụng, giảm thời gian làm cv]
---

# 🚀 **Tự Động Hóa Xét Lựa CV + Phỏng Vấn Hành Vi với AI (Gemini, ElevenLabs & Notion ATS)**

## **Giải Pháp Cho Nỗi Đau Của Các Sếp Tuyển Dụng**
Làm thủ công việc tuyển dụng là một **công việc mệt mỏi, tốn thời gian và dễ sai sót**:
- **Làm CV**: Phải đọc hàng trăm CV, tóm tắt kinh nghiệm, so sánh với mô tả công việc.
- **Phỏng vấn hành vi**: Phải thiết kế câu hỏi, ghi âm, đánh giá và so sánh ứng viên.
- **Quản lý hồ sơ**: Phải cập nhật Notion, Google Sheets, và theo dõi tiến độ.

**Workflow này tự động hóa toàn bộ quy trình từ nhận CV đến phỏng vấn hành vi bằng AI**, giúp các sếp:
✅ **Tiết kiệm 90% thời gian** so với làm thủ công.
✅ **Đánh giá ứng viên chính xác** bằng AI Gemini và mô hình phỏng vấn hành vi.
✅ **Cập nhật hồ sơ tự động** vào Notion ATS và Google Sheets.
✅ **Giảm thiểu sai sót** trong quá trình tuyển dụng.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính riêng tư và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động phân tích CV**: AI tóm tắt kinh nghiệm, kỹ năng và so sánh với mô tả công việc.
- **Phỏng vấn hành vi bằng AI**: Ứng viên được phỏng vấn qua giọng nói, AI đánh giá và ghi âm.
- **Cập nhật hồ sơ tự động**: Thông tin ứng viên được lưu vào Notion ATS và Google Sheets.
- **Đánh giá khách quan**: AI cấp điểm từ 1-10 cho CV và phỏng vấn hành vi.
- **Tiết kiệm thời gian**: Từ hàng giờ làm CV thủ công xuống còn **vài phút**.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản và API Keys**:
   - **Google Drive OAuth 2.0** (để upload CV và audio).
   - **Google Sheets OAuth 2.0** (để lưu dữ liệu ứng viên).
   - **Notion API** (để quản lý hồ sơ ứng viên).
   - **Google Gemini API** (để phân tích CV và phỏng vấn).
   - **ElevenLabs API** (để tạo giọng nói AI và ghi âm phỏng vấn).

2. **Dữ liệu ban đầu**:
   - **Mô tả công việc** (được lưu trong Notion ATS).
   - **Mẫu phỏng vấn hành vi** (câu hỏi chuẩn bị sẵn).
   - **CV ứng viên** (được upload qua Google Drive hoặc Notion).

3. **Cấu hình Notion ATS**:
   - Sử dụng **template Notion ATS** (có sẵn trong workflow).
   - Cấu hình **database ứng viên** và **đánh giá tiêu chí**.

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Tải file JSON từ [n8n.io/workflows/3765](https://n8n.io/workflows/3765).
2. Mở **n8n Editor** và nhấn **Import Workflow**.
3. Chọn file JSON và nhấn **Import**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **33 node**, các sếp cần chú ý cấu hình các node quan trọng sau:

##### **A. Cấu Hình API & Credentials**
| **Node**               | **Lưu Ý Cần Chỉnh**                                                                 | **Tham Số Cần Điền**                          |
|------------------------|------------------------------------------------------------------------------------|-----------------------------------------------|
| **Google Drive**       | Đăng ký OAuth 2.0 cho Google Drive.                                               | `googleDriveOAuth2Api`                       |
| **Google Sheets**      | Đăng ký OAuth 2.0 cho Google Sheets.                                             | `googleSheetsOAuth2Api`                      |
| **Notion API**         | Đăng ký API từ Notion và tạo `integration` trong Notion.                          | `notionApi`                                  |
| **Google Gemini**      | Tạo API Key từ [Google AI Studio](https://makersuite.google.com/).                | `googlePalmApi`                               |
| **ElevenLabs**         | Tạo API Key từ [ElevenLabs](https://elevenlabs.io/).                              | `elevenLabsApi` (nếu sử dụng node webhook)   |

##### **B. Cấu Hình Form Trigger (Bắt Đầu Workflow)**
- **Application Form 1 of 3, 2 of 3, 3 of 3**:
  - Cấu hình **hidden field "Job Code"** để match ứng viên với mô tả công việc.
  - Thêm **mô tả công việc** vào Notion ATS trước khi chạy workflow.

##### **C. Cấu Hình AI Gemini & Phân Tích CV**
- **Node "HR Expert" (chainLlm)**:
  - Cấu hình **prompt** để AI so sánh CV với mô tả công việc.
  - Ví dụ:
    ```json
    "prompt": "So sánh CV của ứng viên với mô tả công việc {jobDescription}. Đánh giá kỹ năng, kinh nghiệm và cấp điểm từ 1-10."
    ```
- **Node "Applicant Summary" (chainSummarization)**:
  - AI tóm tắt **kinh nghiệm, giáo dục và kỹ năng** của ứng viên.

##### **D. Cấu Hình Phỏng Vấn Hành Vi (ElevenLabs)**
- **Node "ElevenLabs Web Hook"**:
  - Cấu hình **webhook** để nhận audio từ ElevenLabs.
  - Thiết lập **câu hỏi phỏng vấn hành vi** trong prompt.
- **Node "AI Agent" (agent)**:
  - AI đánh giá **câu trả lời ứng viên** và cấp điểm từ 1-5.

##### **E. Cập Nhật Notion ATS & Google Sheets**
- **Node "Create Applicant Record" (notion)**:
  - Cập nhật **hồ sơ ứng viên** vào Notion ATS.
- **Node "Applicant Data Backup" (googleSheets)**:
  - Lưu **dữ liệu ứng viên** vào Google Sheets cho báo cáo.

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với một CV mẫu:
   - Upload CV vào Google Drive.
   - Điền thông tin ứng viên vào **Application Form**.
   - Chạy workflow và kiểm tra kết quả.
2. **Bật Active**:
   - Sau khi test thành công, nhấn **Active** để workflow chạy tự động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack/Telegram** để thông báo kết quả phỏng vấn cho team.
2. **Lưu Log & Báo Cáo**:
   - Sử dụng **Google Sheets** để tạo báo cáo định kỳ về ứng viên.
3. **Tự Động Gửi Email**:
   - Thêm node **Email** để thông báo kết quả phỏng vấn cho ứng viên.
4. **Cập Nhật Mô Hình AI**:
   - Cập nhật **prompt** của Gemini để cải thiện độ chính xác.

---

### 📌 **Kết Luận**
Workflow này **tự động hóa toàn bộ quy trình tuyển dụng**, từ **phân tích CV** đến **phỏng vấn hành vi bằng AI**, giúp các sếp:
✔ **Tiết kiệm thời gian** (90% so với làm thủ công).
✔ **Đánh giá ứng viên chính xác** bằng AI.
✔ **Quản lý hồ sơ hiệu quả** trên Notion và Google Sheets.

**Hãy áp dụng ngay và tự động hóa tuyển dụng của mình!** 🚀

---
**🔗 [Tải workflow từ n8n.io](https://n8n.io/workflows/3765)**
**💡 Cần hỗ trợ? Hãy comment bên dưới!**