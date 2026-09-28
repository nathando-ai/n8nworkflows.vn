---
title: "🚀 **Tự Động Hóa Xét Duyệt CV Bulk + Matching Với GPT-4: Giải Pháp AI Cho Đội Ngũ HR & TA**"
description: "Workflow này tự động hóa quá trình xét duyệt CV bulk, so sánh hồ sơ ứng viên với mô tả công việc (JD) bằng GPT-4, và tự động cập nhật kết quả vào Google Sheets/Slack. Giúp HR tiết kiệm 80% thời gian trong tuyển dụng, giảm thiểu sai sót và tăng độ chính xác trong việc lựa chọn ứng viên phù hợp."
slug: "tieu-duyet-cv-bulk-voi-gpt4-hr-ta"
tags: [n8n, automation, hr, ai, gpt-4, google-sheets, google-drive, slack, sendgrid, no-code]
keywords: [tự động hóa tuyển dụng, xét duyệt cv bulk, gpt-4 trong hr, n8n workflow hr, ai cho tuyển dụng, so sánh cv với mô tả công việc]
---

# 🚀 **Tự Động Hóa Xét Duyệt CV Bulk + Matching Với GPT-4: Giải Pháp AI Cho Đội Ngũ HR & TA**

### **Giải pháp nào giúp HR/TA:**
- **Xét duyệt hàng trăm CV trong vài phút** thay vì mất ngày tháng thủ công?
- **So sánh hồ sơ ứng viên với mô tả công việc (JD) một cách chính xác** bằng trí tuệ nhân tạo?
- **Tự động cập nhật kết quả** vào Google Sheets, Slack và gửi email phản hồi cho ứng viên?
- **Giảm thiểu sai sót và bias** trong tuyển dụng?

Nếu các sếp đang gặp phải những vấn đề trên, **workflow này là giải pháp hoàn hảo**! Dưới đây là hướng dẫn chi tiết để **cài đặt, cấu hình và vận hành** workflow **Bulk Resume Screening & JD Matching with GPT-4** trên n8n, giúp đội ngũ HR/TA tự động hóa toàn bộ quy trình tuyển dụng từ đầu đến cuối.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính riêng tư và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Xét duyệt **hàng trăm CV trong vài phút** thay vì mất ngày tháng thủ công.
- **Chính xác cao**: AI so sánh hồ sơ ứng viên với mô tả công việc (JD) theo **mẫu cấu trúc chuẩn**, giảm thiểu sai sót.
- **Tự động hóa hoàn chỉnh**: Kết quả được **cập nhật tự động** vào Google Sheets, Slack và gửi email phản hồi cho ứng viên.
- **Giảm thiểu bias**: AI đánh giá dựa trên **điểm số và phân tích khách quan**, không phụ thuộc vào cảm nhận cá nhân.
- **Dễ dàng mở rộng**: Thêm các tính năng như **báo cáo định kỳ**, **gửi thông báo Slack cho team tuyển dụng**, hoặc **kết nối với ATS**.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản và API Key**:
   - **OpenAI API** (để sử dụng GPT-4.1-mini).
   - **Google Drive OAuth 2.0** (để upload/download CV và JD).
   - **Google Sheets OAuth 2.0** (để lưu kết quả và quản lý JD).
   - **Slack OAuth 2.0** (để gửi thông báo cho team tuyển dụng).
   - **(Tùy chọn)** **SendGrid API** (để gửi email phản hồi cho ứng viên).

2. **Cấu trúc Google Drive và Sheets**:
   - **Google Drive**:
     - Thư mục `/cv` (để lưu CV của ứng viên).
     - Thư mục `/jd` (để lưu mô tả công việc PDF).
   - **Google Sheets**:
     - **Sheet "Positions"** (mapping giữa tên vị trí và link JD).
     - **Sheet "Evaluation form"** (để lưu kết quả xét duyệt).

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể **import workflow từ file JSON** hoặc **copy/paste JSON** vào n8n Editor:
1. Tải file JSON từ [n8n.io/workflows/6680](https://n8n.io/workflows/6680).
2. Trong n8n Editor, nhấn **Import** và chọn file JSON.
3. Hoặc copy toàn bộ JSON và paste vào **Import Workflow** trong n8n.

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này gồm **21 node**, các sếp cần chú ý cấu hình các node quan trọng sau:

#### **A. Cấu hình API và Credentials**
- **OpenAI API**:
  - Đăng ký tại [OpenAI](https://platform.openai.com/) và lấy **API Key**.
  - Trong n8n, tạo **credentials mới** với tên `openAiApi` và điền API Key.
- **Google Drive & Sheets**:
  - Tạo **credentials OAuth 2.0** với tên `googleDriveOAuth2Api` và `googleSheetsOAuth2Api`.
  - Cấu hình quyền truy cập cho **Google Drive** và **Google Sheets**.
- **Slack**:
  - Tạo **credentials OAuth 2.0** với tên `slackOAuth2Api`.
  - Chọn quyền `chat:write` để gửi thông báo.
- **(Tùy chọn) SendGrid**:
  - Tạo **credentials API** với tên `sendGridApi` và điền **API Key**.

#### **B. Cấu hình Google Sheets**
- **Sheet "Positions"**:
  - Cột `Job Role` (tên vị trí tuyển dụng).
  - Cột `JD File Link` (link PDF mô tả công việc trong Google Drive).
- **Sheet "Evaluation form"**:
  - Các cột cần có: `Candidate Name`, `Job Role`, `Fit Score`, `Strengths`, `Gaps`, `Recommendation`, `Status`.

#### **C. Cấu hình Google Drive**
- Tạo **thư mục `/cv`** để lưu CV của ứng viên.
- Tạo **thư mục `/jd`** để lưu mô tả công việc PDF.

#### **D. Cấu hình Node quan trọng**
| **Node** | **Lưu ý cấu hình** |
|----------|---------------------|
| **Application form** | Node này nhận dữ liệu từ form (có thể là form Google Form hoặc webhook). |
| **Extract profile** | Chọn **operation: pdf** để extract thông tin từ CV PDF. |
| **gpt4-1 model** | Đảm bảo chọn **model: gpt-4.1-mini** và điền **credentials: openAiApi**. |
| **Get position JD** | Chọn **Google Sheets** và cấu hình **credentials: googleSheetsOAuth2Api**. |
| **Download file** | Chọn **Google Drive** và cấu hình **credentials: googleDriveOAuth2Api**. |
| **HR Expert Agent** | Node này sử dụng **chainLlm** để phân tích hồ sơ ứng viên. |
| **Profile Analyzer Agent** | Node này sử dụng **agent** để so sánh hồ sơ với JD. |
| **Candidate qualified?** | Đặt **threshold fit score** (ví dụ: <8 là không phù hợp). |
| **Update evaluation sheet** | Cấu hình **Google Sheets** và chọn **operation: append** để thêm dữ liệu mới. |
| **Send email to candidate** | Cấu hình **SendGrid** và điền nội dung email mẫu. |
| **Send message via Slack** | Cấu hình **Slack** và chỉnh sửa nội dung thông báo. |

---

### **3. Kích hoạt ⚡️**
1. **Test run dữ liệu mẫu**:
   - Tải một CV mẫu lên Google Drive và chọn vị trí tuyển dụng trong form.
   - Chạy workflow để kiểm tra kết quả.
2. **Bật Active workflow**:
   - Sau khi kiểm tra thành công, nhấn **Active** để workflow chạy tự động.

---

## ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁC Ý TƯỞNG MỞ RỘNG]
- **Gửi báo cáo định kỳ**: Sử dụng **node `schedule`** để tự động gửi báo cáo kết quả xét duyệt hàng tuần/month.
- **Kết nối với ATS**: Thêm **webhook trigger** để workflow tự động chạy khi có CV mới từ hệ thống ATS.
- **Lưu log hoạt động**: Sử dụng **node `stickyNote`** để ghi lại lịch sử xét duyệt.
- **Tùy chỉnh AI**: Thay đổi **prompt** trong node `chainLlm` để AI đánh giá theo tiêu chí riêng của công ty.
- **Gửi thông báo Telegram**: Thêm **node `telegram`** để gửi kết quả xét duyệt qua Telegram.
- **Tích hợp với Zoom**: Sử dụng **node `zoom`** để tự động tạo cuộc gọi phỏng vấn với ứng viên phù hợp.
:::

---

## 📌 **Kết luận**
Workflow **Bulk Resume Screening & JD Matching with GPT-4** là **giải pháp hoàn hảo** để tự động hóa quy trình tuyển dụng, giúp HR/TA:
✅ **Tiết kiệm thời gian** (xét duyệt hàng trăm CV trong vài phút).
✅ **Tăng độ chính xác** (AI so sánh hồ sơ với JD theo mẫu cấu trúc).
✅ **Tự động hóa hoàn chỉnh** (cập nhật kết quả vào Sheets, Slack và gửi email phản hồi).

**Hãy áp dụng ngay workflow này và nâng cao hiệu quả tuyển dụng của công ty!** 🚀

---
**📌 Lưu ý cuối cùng**:
- Nếu gặp vấn đề, các sếp có thể **xem log hoạt động** trong n8n để debug.
- **Mở rộng workflow** bằng cách thêm các node mới như **node `webhook`** để tự động nhận CV từ website hoặc **node `database`** để lưu kết quả lâu dài.