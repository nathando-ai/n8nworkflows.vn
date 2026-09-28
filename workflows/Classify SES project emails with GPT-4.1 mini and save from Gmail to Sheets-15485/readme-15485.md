---
title: "🚀 Tự động phân loại email dự án SES bằng GPT‑4.1 mini → Google Sheets"
description: "Workflow n8n giám sát Gmail, dùng AI GPT‑4.1 mini phân loại email dự án SES và lưu chi tiết vào Google Sheets chỉ trong vài giây."
slug: "tu-dong-phan-loai-email-du-an-ses-gpt4-mini"
tags: [n8n, automation, no-code, gmail, google-sheets, openai]
keywords: [n8n workflow, tự động hóa, email classification, GPT-4, Google Sheets integration]
---

# 🚀 Tự động phân loại email dự án SES bằng GPT‑4.1 mini → Google Sheets

Bạn có bao giờ phải **lướt qua hàng trăm email tuyển dụng**, tìm kiếm những dự án SES (System Engineering Service) phù hợp, rồi mới copy‑paste thông tin vào bảng tính?  
Công việc này không chỉ **tốn thời gian**, mà còn **dễ sai sót** và **không đồng bộ** khi nhiều người cùng làm.  

**Workflow n8n này** sẽ giải quyết 100% vấn đề trên: mỗi phút, nó sẽ **đọc Gmail**, **đánh giá bằng GPT‑4.1 mini** xem email có phải là dự án SES không, **trích xuất dữ liệu** thành JSON, rồi **đưa vào Google Sheets** tự động. Không cần viết một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động xử lý email trong vòng vài giây.  
- **Độ chính xác cao**: AI phân loại và trích xuất dữ liệu dựa trên mô hình GPT‑4.1 mini.  
- **Dữ liệu luôn đồng bộ**: Mỗi dự án mới ngay lập tức xuất hiện trong Google Sheets.  
- **Hoạt động 24/7**: Không cần giám sát, workflow chạy liên tục trên server.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Gmail** với **OAuth2 credentials** (để n8n có thể đọc inbox).  
- **OpenAI API key** (để sử dụng GPT‑4.1 mini).  
- **Google Sheets OAuth2 credentials** (để ghi dữ liệu vào bảng tính).  
- **Google Spreadsheet** đã tạo sẵn, có sheet tên `Projects` (hoặc tên khác, sẽ cấu hình ở node *Set Spreadsheet Config*).  
- **n8n** đã được cài đặt và có thể truy cập internet để gọi API OpenAI.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. **Tải file JSON** của workflow (từ link gốc https://n8n.io/workflows/15485) hoặc sao chép toàn bộ JSON.  
2. Vào **n8n Editor → Workflows → Import** → Dán JSON → **Import**.  
3. Đặt tên cho workflow (mặc định: *Classify SES project emails with GPT‑4.1 mini and save from Gmail to Sheets*).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Dưới đây là **các node quan trọng** và cách cấu hình chi tiết:

| Node | Loại | Cấu hình cần chỉnh |
|------|------|-------------------|
| **Gmail Trigger** | `gmailTrigger` | - Chọn **Credentials**: `gmailOAuth2` đã tạo.<br>- **Poll Interval**: mặc định 1 phút (có thể tăng/giảm).<br>- (Tùy chọn) Thêm **Label** hoặc **From** để lọc email giảm noise. |
| **AI Project Classifier** | `openAi` (GPT‑4.1 mini) | - **Credentials**: `openAiApi`.<br>- **Model**: `gpt-4o-mini` (hoặc `gpt-4.1-mini` tùy phiên bản).<br>- **Prompt**: Đưa vào **Subject** + **Body** của email, yêu cầu trả về JSON có các trường: `isProject`, `project_name`, `category`, `rate`, `skills`, `location`, … (prompt mẫu có trong node). |
| **Parse JSON** | `code` | - **Code**: `return JSON.parse($json["aiResponse"]);` (hoặc script đã có). Không cần chỉnh nếu bạn giữ định dạng JSON chuẩn. |
| **Is Project Email?** | `if` | - **Condition**: `{{$json["isProject"]}}` **equals** `true`.<br>- **True** → **Append to Spreadsheet**.<br>- **False** → **Skip (Non-Project Email)**. |
| **Set Spreadsheet Config** | `set` | - Thêm 2 fields: `spreadsheetId` và `sheetName`.<br>- **spreadsheetId**: ID của Google Sheet (phần sau `/d/` trong URL).<br>- **sheetName**: Tên sheet, mặc định `Projects`. |
| **Append to Spreadsheet** | `googleSheets` | - **Credentials**: `googleSheetsOAuth2Api`.<br>- **Operation**: `Append` (đã được set trong *keyParameters*).<br>- **Spreadsheet ID**: lấy từ **Set Spreadsheet Config** (`{{$json["spreadsheetId"]}}`).<br>- **Sheet Name**: `{{$json["sheetName"]}}`.<br>- **Columns**: map các trường JSON (`project_name`, `category`, `details`, `client_company`, `rate`, `remote`, `location`, `working_hours`, `required_skills`, `preferred_skills`, `notes`). |
| **Skip (Non-Project Email)** | `noOp` | Không cần cấu hình, chỉ để “bỏ qua” email không phải dự án. |

> **Lưu ý:** Đảm bảo **Google Sheet** có **các header** trùng khớp với các trường trên ở dòng đầu tiên, nếu không dữ liệu sẽ bị ghi sai cột.

#### 3. Kích hoạt ⚡️
1. **Test run**: Gửi một email mẫu có nội dung dự án SES vào hộp thư Gmail đã kết nối.  
2. Kiểm tra **Execution Log** của n8n, xác nhận node *AI Project Classifier* trả về JSON hợp lệ và dữ liệu đã được **append** vào Google Sheet.  
3. Nếu mọi thứ ổn, bật **Active** (nút toggle ở góc trên bên phải) để workflow chạy liên tục.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo Slack/Telegram**: Thêm node Slack hoặc Telegram ngay sau *Append to Spreadsheet* để gửi tin nhắn báo dự án mới cho team.  
- **Lưu log chi tiết**: Dùng node *Google Drive* hoặc *S3* để lưu toàn bộ phản hồi AI dưới dạng file JSON, phục vụ audit.  
- **Báo cáo định kỳ**: Kết hợp node *Cron* + *Google Sheets* → *Email* để gửi báo cáo tổng hợp dự án mỗi tuần.  
- **Tối ưu prompt**: Thêm ví dụ mẫu trong prompt để AI hiểu rõ định dạng JSON mong muốn, giảm lỗi parse.  

### 📌 Kết luận
Với workflow này, các sếp sẽ **không còn mất công đọc và sao chép email dự án** nữa. Từ khi email tới, AI sẽ tự động phân loại, trích xuất và ghi vào Google Sheets, giúp **tiết kiệm thời gian**, **đảm bảo độ chính xác** và **đồng bộ dữ liệu** cho toàn bộ đội ngũ. Hãy **import ngay**, cấu hình vài thông tin cơ bản và để n8n làm việc cho bạn! 🚀