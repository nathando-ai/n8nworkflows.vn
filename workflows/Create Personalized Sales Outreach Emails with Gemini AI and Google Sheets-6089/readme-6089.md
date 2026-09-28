---
title: "🚀 Tạo Email Tiếp Cận Bán Hàng Cá Nhân Hóa Bằng Gemini AI & Google Sheets"
description: "Tự động tạo email outreach cho từng lead dựa trên dữ liệu trong Google Sheets, sử dụng Gemini AI để viết nội dung chuẩn SEO và lưu lại kết quả ngay trong Sheet."
slug: "tao-email-tiep-can-ban-hang-ca-nhan-hoa-gemini-ai-google-sheets"
tags: [n8n, automation, no-code, lead-nurturing, AI, email-marketing]
keywords: [n8n workflow, tự động hóa, email bán hàng, Gemini AI, Google Sheets]
---

# 🚀 Tạo Email Tiếp Cận Bán Hàng Cá Nhân Hóa Bằng Gemini AI & Google Sheets

Bạn đã từng mất hàng giờ để **soạn email** cho từng khách hàng tiềm năng?  
Việc copy‑paste thông tin từ Google Sheet, viết nội dung sao cho vừa ngắn gọn, vừa thu hút, rồi lại phải quay lại Sheet để cập nhật kết quả – **đây là công việc tẻ nhạt, dễ sai sót và tiêu tốn tài nguyên**.  

Workflow này sẽ **giải quyết 100%** những rắc rối trên: mỗi khi có lead mới trong Google Sheet, Gemini AI sẽ tự động tạo một email outreach cá nhân hoá, sau đó ghi lại nội dung email ngay vào cùng một dòng của Sheet. Không cần viết code, không cần mở Excel, chỉ cần một lần cài đặt và để nó chạy 24/7.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động tạo email trong vòng vài giây cho mỗi lead.  
- **Độ chính xác cao**: Dữ liệu lấy trực tiếp từ Google Sheet, không còn lỗi nhập tay.  
- **Cá nhân hoá**: Nội dung email dựa trên thông tin cụ thể của từng lead (tên, công ty, nhu cầu).  
- **Hoạt động liên tục**: Workflow chạy tự động theo lịch, không cần can thiệp thủ công.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Google** với quyền **Google Sheets API** (OAuth2) để đọc/ghi dữ liệu.  
- **API Key Google Palm (Gemini)** – tạo tại Google Cloud > Vertex AI > “Gemini API”.  
- **n8n** (cài đặt trên VPS hoặc dùng n8n.cloud).  
- Google Sheet chứa danh sách leads với các cột: `Name`, `Company`, `Industry`, `Email`, `Generated Email` (cột này sẽ được workflow cập nhật).  
- Đảm bảo **cron schedule** phù hợp với tần suất cập nhật (hàng ngày, 2‑3 lần/giờ, …).  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở **n8n Editor**.  
2. Click **“Import” → “From File”** và tải file JSON của workflow (hoặc **Copy/Paste** toàn bộ JSON vào ô import).  
3. Nhấn **“Import”**, workflow sẽ xuất hiện trong danh sách.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Mô tả | Cấu hình cần chỉnh |
|------|------|--------------------|
| **Schedule Trigger** | Kích hoạt workflow theo lịch định sẵn. | Chọn **Cron** → đặt tần suất (ví dụ: `0 */2 * * *` = mỗi 2 giờ). |
| **Read Leads from Sheet** | Đọc dữ liệu lead từ Google Sheet. | - **Credentials**: chọn `googleSheetsOAuth2Api`. <br> - **Spreadsheet ID**: ID của file Sheet chứa lead.<br> - **Range**: ví dụ `Leads!A2:E` (bắt đầu từ dòng 2, cột A‑E). |
| **Prepare Data for Sheet** | Định dạng dữ liệu cho LLM (tạo JSON). | Không cần credentials. Đảm bảo **Set** các trường: `name`, `company`, `industry`, `email`. |
| **Basic LLM Chain** | Kết nối chuỗi các node LLM. | Không cần thay đổi, chỉ đảm bảo **Input** là dữ liệu từ node `Prepare Data for Sheet`. |
| **Google Gemini Chat Model** | Gọi Gemini AI để sinh nội dung email. | - **Credentials**: chọn `googlePalmApi`. <br> - **Model**: `gemini-pro`. <br> - **Prompt** (ví dụ): <br>```text\nBạn là một chuyên gia sales. Viết email ngắn gọn, cá nhân hoá cho lead {{name}} làm việc tại {{company}} (ngành {{industry}}). Nội dung phải có lời chào, giới thiệu ngắn gọn về sản phẩm và CTA.``` |
| **Structured Output Parser** | Chuyển kết quả Gemini thành JSON có trường `emailBody`. | - **Schema**: `{ "emailBody": "string" }`. <br> - Đảm bảo **Output** được map sang `emailBody`. |
| **Update Sheet with Email** | Ghi email đã sinh vào cột `Generated Email`. | - **Credentials**: `googleSheetsOAuth2Api`. <br> - **Spreadsheet ID**: giống như node đọc. <br> - **Range**: dùng **Dynamic** để cập nhật đúng dòng (sử dụng `{{ $json["rowNumber"] }}` hoặc `{{ $node["Read Leads from Sheet"].json["row"] }}`). |
| **If** | Kiểm tra xem có lead mới chưa (để tránh ghi đè). | - **Condition**: `{{ $json["emailBody"] !== "" }}` hoặc kiểm tra `{{ $node["Read Leads from Sheet"].json["Generated Email"] === "" }}`. |

> **Lưu ý:** Đối với node **Update Sheet with Email**, cần bật **“Append”** hoặc **“Update”** tùy theo cách bạn muốn ghi. Thông thường dùng **Update** dựa trên **Row Number** để ghi đè vào cùng một dòng.

#### 3. Kích hoạt ⚡️
1. **Test run**: Click **“Execute Workflow”**, chọn **“Run Once”** và kiểm tra log để chắc chắn email được sinh và ghi lại đúng cột.  
2. Nếu mọi thứ ổn, bật **“Active”** (nút chuyển đổi ở góc trên bên phải).  
3. Kiểm tra Google Sheet – cột `Generated Email` phải chứa nội dung email mới.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo Slack/Telegram**: Thêm node **Slack** hoặc **Telegram** sau node `Update Sheet` để gửi thông báo “Email cho {{name}} đã được tạo”.  
- **Lưu log chi tiết**: Dùng **Google Drive** hoặc **Airtable** để lưu toàn bộ log chạy, giúp audit và phân tích hiệu suất.  
- **Đa ngôn ngữ**: Thêm tham số ngôn ngữ vào prompt và sử dụng **Gemini** để tạo email tiếng Anh, tiếng Nhật, … tùy nhu cầu khách hàng quốc tế.  
- **Error handling**: Đặt node **Error Trigger** để gửi email báo lỗi cho admin khi Gemini trả về lỗi hoặc khi Google Sheets không phản hồi.  

### 📌 Kết luận
Với workflow **“Create Personalized Sales Outreach Emails with Gemini AI and Google Sheets”**, các sếp có thể **tự động hoá toàn bộ quy trình tạo email bán hàng**, giảm thiểu công sức, tăng độ chính xác và nâng cao tỷ lệ phản hồi từ khách hàng. Hãy **import ngay**, cấu hình các credentials và để n8n làm việc thay bạn – thời gian quý báu sẽ được tái đầu tư vào những chiến lược tăng trưởng thực sự! 🚀