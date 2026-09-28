---
title: "🚀 Tự động sàng lọc và xếp hạng CV bằng Llama 4 AI & Google Workspace"
description: "Giải pháp tự động sàng lọc hồ sơ ứng viên, xếp hạng, di chuyển vào thư mục phù hợp, cập nhật bảng theo dõi và gửi thông báo email – hoàn toàn không cần code."
slug: "tang-dong-sang-loc-va-xep-hang-cv-lam-4-ai-google-workspace"
tags: [n8n, automation, no-code, HR, AI, Google Workspace]
keywords: [tự động hóa, sàng lọc CV, Llama 4, n8n workflow, AI, Google Drive, Gmail, Google Sheets]
---

# 🚀 Tự động sàng lọc và xếp hạng CV bằng Llama 4 AI & Google Workspace

Bạn đang phải xử lý hàng trăm CV mỗi ngày?  
Mỗi lần đọc, đánh giá và phân loại hồ sơ là một công việc tốn kém thời gian, dễ sai sót và không nhất quán.  
Workflow này sẽ **đưa AI Llama 4 vào quá trình sàng lọc**, tự động **đánh giá, xếp hạng** và **đưa CV vào thư mục phù hợp** (Shortlisted / KIV / Reject). Đồng thời **cập nhật bảng theo dõi** và **gửi email thông báo** cho nhà tuyển dụng – hoàn toàn không cần viết code.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ vài giờ xuống vài phút cho mỗi CV.  
- **Chính xác nhất định**: AI đánh giá dựa trên mô tả công việc, giảm sai sót con người.  
- **Cá nhân hóa**: Đánh giá theo tiêu chí riêng của từng vị trí.  
- **Hoạt động liên tục**: 24/7, không cần giám sát thủ công.  
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
| Dịch vụ | Credential cần thiết | Mô tả |
|---------|----------------------|-------|
| Google Drive | `googleDriveOAuth2Api` | Truy cập thư mục “Unfiltered”, “Shortlisted”, “KIV”, “Reject”. |
| Gmail | `gmailOAuth2` | Gửi email thông báo. |
| Google Docs | `googleDocsOAuth2Api` | Đọc mô tả công việc (Job Description). |
| Google Sheets | `googleSheetsOAuth2Api` | Cập nhật bảng theo dõi ứng viên. |
| Groq | `groqApi` | Truy cập mô hình Llama 4. |
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥

1. Tải file JSON từ link gốc: <https://n8n.io/workflows/3838> hoặc copy nội dung JSON.  
2. Mở n8n Editor → **Import** → **Import JSON** → dán nội dung hoặc tải file.  
3. Nhấn **Import** và workflow sẽ xuất hiện trong danh sách.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

| Node | Tên Node | Cấu hình cần chỉnh | Ghi chú |
|------|----------|---------------------|---------|
| Google Docs – Get Job Desc | `GDocs - Get Job Desc` | `Document ID` (ID của Google Doc chứa Job Description) | Đặt ID trong **Parameters**. |
| Google Drive Trigger | `Google Drive - Resume CV File Created` | `Folder ID` (ID thư mục “Unfiltered”) | Đặt ID trong **Parameters**. |
| Google Drive – Download | `Download Resume File From Gdrive` | `File ID` (được truyền từ trigger) | Đặt trong **Parameters**. |
| Extract from File | `Extract from File` | `File Content` (được truyền từ download) | Đặt trong **Parameters**. |
| Groq – Llama 4 | `Groq - llama 4 AI MODEL` | `API Key` (từ credential `groqApi`), `Prompt` (định dạng câu hỏi cho AI) | Đặt trong **Parameters**. |
| AI Agent | `AI Agent` | `Agent Name`, `Steps` (định nghĩa logic: đánh giá, phân loại) | Tùy chỉnh theo nhu cầu. |
| Google Drive Tool – Move | `Gdrive:Move-To-*` | `Source File ID`, `Destination Folder ID` | Đặt ID thư mục “Shortlisted”, “KIV”, “Reject”. |
| Google Sheets Tool – Update | `Gsheet: Update Candidate Tracker` | `Spreadsheet ID`, `Sheet Name`, `Data` (được truyền từ AI Agent) | Đặt ID bảng và sheet. |
| Gmail Tool – Notification | `Gmail:Notification` | `To`, `Subject`, `Body` (được truyền từ AI Agent) | Đặt email nhận thông báo. |

> **Lưu ý**: Mỗi node cần **Credentials** đã được cấu hình trong n8n (đăng nhập Google, Groq, v.v.). Nếu chưa có, vào **Credentials** → **New Credential** → chọn loại và điền thông tin.

### 3. Kích hoạt ⚡️

1. **Test run**: Chọn một CV mẫu trong thư mục “Unfiltered”, chạy workflow thủ công để kiểm tra.  
2. Kiểm tra:  
   - CV đã được chuyển vào thư mục phù hợp.  
   - Bảng Google Sheets đã cập nhật điểm số.  
   - Email đã được gửi.  
3. Khi mọi thứ ổn, bật **Active** cho workflow.

## ✍️ Mẹo & gợi ý nâng cao

- **Thêm Slack/Telegram**: Sử dụng node `Slack` hoặc `Telegram` để gửi thông báo ngay khi CV được xếp hạng.  
- **Lưu log**: Dùng node `Write Binary File` để ghi log vào Google Drive, giúp theo dõi lịch sử xử lý.  
- **Báo cáo định kỳ**: Thêm node `Cron` + `Google Sheets` để xuất báo cáo hàng ngày/tuần.  
- **Tùy chỉnh prompt AI**: Thêm các tiêu chí đánh giá cụ thể (kỹ năng, kinh nghiệm, học vấn) vào prompt để AI đưa ra điểm số chính xác hơn.  

## 📌 Kết luận

Workflow “Tự động sàng lọc và xếp hạng CV bằng Llama 4 AI & Google Workspace” giúp các sếp HR tiết kiệm thời gian, giảm sai sót và tăng tính nhất quán trong quá trình tuyển dụng.  
Hãy **đưa AI vào công việc** ngay hôm nay – bạn sẽ ngạc nhiên với hiệu quả mà không cần viết dòng code nào!