---
title: "🚀 Tự động tạo đề xuất bán hàng AI với Gemini & Google Docs"
description: "Từ form nhập liệu, workflow n8n tính ROI, tạo nội dung đề xuất bằng Gemini và tự động điền vào mẫu Google Docs chỉ trong vài giây."
slug: "tu-dong-tao-de-xuat-ban-hang-ai-gemini-google-docs"
tags: [n8n, automation, no-code, AI, Google-Docs, Gemini]
keywords: [n8n workflow, tự động tạo đề xuất, AI sales, Gemini, Google Docs]
---

# 🚀 Tự động tạo đề xuất bán hàng AI với Gemini & Google Docs

Bạn đã bao giờ phải ngồi hàng giờ đồng hồ để viết một đề xuất bán hàng chuẩn SEO, chèn các con số ROI, và vẫn còn lo lắng về lỗi chính tả?  
Việc này không chỉ tốn thời gian mà còn gây mất cơ hội khi khách hàng chờ đợi.  

**Workflow này** sẽ giải quyết toàn bộ quy trình: từ việc nhận thông tin khách hàng qua form, tính toán các chỉ số tài chính, đến việc để Gemini AI viết nội dung đề xuất và tự động chèn vào mẫu Google Docs của bạn. Tất cả diễn ra **100 % không cần code** và chạy liên tục 24/7.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ vài phút thay vì vài giờ để hoàn thiện một đề xuất.  
- **Độ chính xác cao**: Các chỉ số ROI, tiết kiệm và thời gian hoàn vốn được tính tự động, không còn sai sót con số.  
- **Nội dung chuyên nghiệp, cá nhân hoá**: Gemini viết theo ngữ cảnh ngành, pain points và số liệu thực tế của khách hàng.  
- **Hoạt động liên tục**: Khi form được gửi, workflow tự động chạy mà không cần can thiệp thủ công.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Google**: Đã bật Google Drive API & Google Docs API, tạo OAuth2 credentials (`googleDriveOAuth2Api`, `googleDocsOAuth2Api`).  
- **API Gemini**: Key `googlePalmApi` (Gemini 1.5 Flash).  
- **Mẫu Google Doc**: Tài liệu mẫu chứa các placeholder như `{{client_name}}`, `{{executive_summary}}`, `{{key_challenges}}`, …  
- **n8n**: Đã cài đặt và truy cập được editor để import workflow.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n → **Workflows** → **Import**.  
2. Chọn **Upload JSON** và tải file JSON của workflow (hoặc copy toàn bộ JSON và dán vào ô **Paste JSON**).  
3. Nhấn **Import** → Workflow sẽ xuất hiện trên canvas.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Cấu hình cần chỉnh | Ghi chú |
|------|-------------------|---------|
| **Receive proposal details** (formTrigger) | Thêm các trường: `client_name`, `industry`, `pain_points`, `price`, `quantity`, `contract_term`… | Form sẽ được chia sẻ cho bộ phận sales. |
| **Calculate ROI metrics** (code) | Không cần thay đổi nếu bạn dùng script mặc định; chỉ cần chắc chắn các biến đầu vào khớp với tên trường form. | Script tính `roi`, `net_savings`, `break_even`. |
| **Generate proposal content** (agent) | System prompt: chỉnh sửa nội dung để phù hợp tone công ty (ví dụ: “Bạn là chuyên gia bán hàng B2B, viết đề xuất ngắn gọn, chuyên nghiệp”). | Prompt ảnh hưởng trực tiếp tới chất lượng văn bản AI. |
| **Gemini 1.5 Flash** (lmChatGoogleGemini) | Chọn **Credentials** → `googlePalmApi`. | Đảm bảo quota API còn đủ. |
| **Parse AI response** (code) | Không cần thay đổi; node này sẽ parse JSON trả về từ Gemini. |
| **Copy proposal template** (googleDrive) | Credentials → `googleDriveOAuth2Api`. <br>Operation: **copy**. <br>File ID: ID của mẫu Google Doc của bạn. | Kết quả là một bản sao mới sẽ được tạo ra cho mỗi đề xuất. |
| **Format bullet points** (code) | Không cần thay đổi; node này chuẩn hoá danh sách thành dạng markdown cho Docs. |
| **Populate proposal document** (googleDocs) | Credentials → `googleDocsOAuth2Api`. <br>Operation: **update**. <br>Document ID: để trống, sẽ được tự động lấy từ node **Copy proposal template** (output `documentId`). | Đảm bảo placeholder trong mẫu trùng khớp với tên trường trong node này. |

#### 3. Kích hoạt ⚡️
1. **Test run**: Mở form, nhập dữ liệu mẫu và submit. Kiểm tra log của từng node để chắc chắn không có lỗi.  
2. Kiểm tra **Google Doc** được tạo: nội dung các placeholder đã được thay thế đúng chưa.  
3. Khi mọi thứ ổn, bật **Active** ở góc phải của workflow để cho phép chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối Slack/Telegram**: Thêm node **Slack** hoặc **Telegram** để gửi thông báo khi đề xuất đã sẵn sàng.  
- **Lưu log vào Google Sheet**: Dùng node **Google Sheets** để ghi lại mọi đề xuất (client, ngày, ROI…) để phân tích hiệu suất bán hàng.  
- **Báo cáo định kỳ**: Tạo workflow phụ định kỳ (hàng tuần) tổng hợp các đề xuất đã gửi và gửi báo cáo PDF qua email.  
- **Tùy chỉnh AI**: Thêm **few‑shot examples** vào prompt để Gemini hiểu sâu hơn phong cách viết của công ty.

### 📌 Kết luận
Với workflow này, các sếp có thể **tự động hoá toàn bộ quy trình tạo đề xuất bán hàng** chỉ trong vài cú click, giảm thiểu lỗi và tăng tốc độ phản hồi khách hàng. Hãy import ngay, cấu hình các credential, và để AI Gemini làm việc cho bạn – **đừng để thời gian viết đề xuất làm chậm bước tiến của doanh nghiệp!**