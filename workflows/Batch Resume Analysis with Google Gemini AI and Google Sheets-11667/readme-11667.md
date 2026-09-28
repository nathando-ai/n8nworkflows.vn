---
title: "🚀 Phân Tích Hàng Loạt Hồ Sơ Ứng Việc với Google Gemini AI & Google Sheets"
description: "Tự động trích xuất, tóm tắt và lưu kết quả phân tích 20 hồ sơ PDF cùng lúc, giảm 90% thời gian tuyển dụng."
slug: "phan-tich-ho-so-ung-viec-google-gemini"
tags: [n8n, automation, no-code, HR, AI, GoogleSheets]
keywords: [n8n workflow, tự động hóa, phân tích hồ sơ, AI summarization, Google Gemini]
---

# 🚀 Phân Tích Hàng Loạt Hồ Sơ Ứng Việc với Google Gemini AI & Google Sheets

Bạn đang phải **đọc hàng chục, hàng trăm hồ sơ PDF** mỗi ngày? Việc này không chỉ tốn thời gian mà còn dễ gây sai sót khi đánh giá thủ công.  
Workflow **Batch Resume Analysis** giúp bạn **tự động tải lên tới 20 file PDF**, AI (Google Gemini) sẽ **trích xuất nội dung, tóm tắt các kỹ năng, kinh nghiệm** và **đưa kết quả vào Google Sheets** chỉ trong vài giây. Không cần viết một dòng code nào – chỉ cần cấu hình nhẹ nhàng và chạy!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Xử lý 20 hồ sơ trong < 1 phút.  
- **Độ chính xác cao**: AI phân tích dựa trên mô hình Gemini, giảm lỗi con người.  
- **Báo cáo tự động**: Kết quả được ghi vào Google Sheets, dễ dàng chia sẻ và lọc.  
- **Hoạt động liên tục**: Workflow chạy 24/7, không cần giám sát liên tục.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Google** với **Google Sheets API** và **Google Palm (Gemini) API** đã bật.  
- **Credentials** trong n8n:  
  - `googleSheetsOAuth2Api` (OAuth2 cho Google Sheets)  
  - `googlePalmApi` (API key cho Gemini)  
- **Google Sheet mẫu** (đã có sẵn các cột: Tên, Email, Kỹ năng, Kinh nghiệm, Điểm AI).  
- **n8n** (cài đặt trên VPS hoặc Docker) với các node: `formTrigger`, `extractFromFile`, `code`, `agent`, `lmChatGoogleGemini`, `aggregate`, `googleSheets`.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập **n8n > Workflows > Import**.  
2. Tải file JSON của workflow (được cung cấp ở phần cuối) hoặc **Copy/Paste** toàn bộ JSON vào ô import.  
3. Nhấn **Import** → workflow sẽ xuất hiện trên canvas.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Vai trò | Cấu hình cần thay đổi |
|------|----------|-----------------------|
| **On form submission** (formTrigger) | Thu thập file PDF từ người dùng | - Bật **“Allow multiple files”**.<br>- Đặt tên trường `files` (hoặc tùy ý) để truyền danh sách file. |
| **Extract from File** (extractFromFile) | Trích xuất nội dung PDF | - `Operation` = **pdf** (đã mặc định).<br>- Đảm bảo **“Binary Property”** trỏ tới file PDF từ form. |
| **map files independently** (code) | Duyệt từng file, chuẩn bị dữ liệu cho AI | ```js\nconst items = $input.all();\nreturn items.map(item => ({ json: { fileContent: item.binary.data.file.data } }));\n```<br>- Đảm bảo **output** trả về `json.fileContent`. |
| **Resume analysis Agent** (agent) | Định nghĩa “system message” cho AI | - **System Message**: nhập mô tả công việc & yêu cầu (VD: “Bạn là chuyên gia tuyển dụng, hãy tóm tắt kỹ năng, kinh nghiệm và đưa ra điểm đánh giá cho mỗi hồ sơ dựa trên mô tả công việc …”). |
| **Google Gemini Chat Model** (lmChatGoogleGemini) | Gọi API Gemini để tóm tắt | - Chọn **Credential** `googlePalmApi`.<br>- **Model**: `gemini-pro` (hoặc phiên bản mới nhất).<br>- **Prompt**: để trống, vì prompt được cung cấp bởi **Agent**. |
| **Aggregate** (aggregate) | Gom lại kết quả từ các file | - **Operation**: `Merge` (hoặc `Append`).<br>- Đặt **Key** là `json` để hợp nhất các đối tượng kết quả. |
| **Append row in sheet** (googleSheets) | Ghi kết quả vào Google Sheet | - Chọn **Credential** `googleSheetsOAuth2Api`.<br>- **Spreadsheet ID**: ID của sheet mẫu (copy từ URL).<br>- **Sheet Name**: tên sheet (VD: `Results`).<br>- **Values**: ánh xạ các trường `json` (Tên, Email, Kỹ năng, Kinh nghiệm, Điểm AI). |

> **Lưu ý:** Sau khi cấu hình, nhấn **Execute Node** từng bước để kiểm tra dữ liệu đầu ra, đặc biệt là node **Extract from File** và **Google Gemini Chat Model**.

#### 3. Kích hoạt ⚡️
1. **Test run**: Điền mẫu form, tải lên 1‑2 file PDF mẫu, chạy workflow và kiểm tra Google Sheet.  
2. Khi mọi thứ ổn, bật **Active** (nút chuyển đổi ở góc trên bên phải).  
3. Đặt **Cron** hoặc **Webhook** nếu muốn tự động kích hoạt từ nguồn khác.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối Slack/Telegram**: Thêm node `Slack` hoặc `Telegram` để gửi thông báo khi phân tích xong.  
- **Lưu log chi tiết**: Dùng node `Write Binary File` để lưu bản sao PDF + kết quả AI vào Google Drive.  
- **Báo cáo định kỳ**: Sử dụng node `Schedule` + `Google Sheets` để tổng hợp số lượng hồ sơ đã xử lý mỗi tuần và gửi email báo cáo.  
- **Tùy chỉnh điểm AI**: Thêm công thức tính điểm dựa trên số từ khóa xuất hiện trong tóm tắt (node `Function`).

### 📌 Kết luận
Với **Batch Resume Analysis**, các sếp có thể **tự động hoá quy trình tuyển dụng**, giảm tải công việc lặp đi lặp lại và đưa ra quyết định nhanh chóng, chính xác. Hãy **import workflow ngay**, cấu hình các credentials và bắt đầu trải nghiệm AI trong tuyển dụng ngay hôm nay! 🚀