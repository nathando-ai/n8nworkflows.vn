---
title: "🚀 So sánh ảnh lòng bàn tay LINE & ghi nhận sức khỏe Gemini vào Google Sheets"
description: "Tự động nhận ảnh lòng bàn tay qua LINE, so sánh với ảnh trước đó bằng Google Gemini và lưu kết quả vào Google Sheets chỉ trong vài giây."
slug: "so-sanh-anh-long-ban-tay-line-gemini-google-sheets"
tags: [n8n, automation, no-code, AI, LINE, GoogleSheets]
keywords: [n8n workflow, tự động hóa, AI health, LINE bot, Google Gemini, Google Drive]
---

# 🚀 So sánh ảnh lòng bàn tay LINE & ghi nhận sức khỏe Gemini vào Google Sheets

**Bạn có bao giờ nhận được tin nhắn từ khách hàng gửi ảnh lòng bàn tay, nhưng lại không biết làm sao để lưu trữ, so sánh và đưa ra lời khuyên nhanh chóng?**  
Việc thực hiện thủ công – tải ảnh, mở Google Sheet, sao chép‑dán, chạy AI – tốn hàng giờ và dễ sai sót.  

**Workflow này** sẽ tự động:

1. Nhận ảnh từ LINE qua webhook.  
2. Lưu ảnh vào Google Drive.  
3. Kiểm tra lịch sử ảnh trong Google Sheets.  
4. Nếu là lần đầu: thực hiện “đọc tay” bằng Google Gemini Vision.  
5. Nếu đã có ảnh cũ: so sánh 2 ảnh, đưa ra phân tích sức khỏe.  
6. Ghi lại toàn bộ kết quả (thời gian, link ảnh, lời khuyên) vào Google Sheets và trả lời ngay cho người dùng trên LINE.

> **Kết quả:** 100 % tự động, không cần viết code, luôn luôn sẵn sàng 24/7.

:::info[Gợi ý hạ tầng cho n8n]  
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]  
- **Tiết kiệm thời gian:** Từ vài phút xuống còn <10 giây mỗi lần.  
- **Độ chính xác cao:** AI phân tích hình ảnh, giảm lỗi con người.  
- **Lưu trữ lịch sử:** Mọi ảnh và lời khuyên đều được ghi lại, dễ dàng theo dõi tiến trình.  
- **Hoạt động liên tục:** Không cần can thiệp, workflow tự chạy 24/7.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]  
- **Tài khoản LINE Messaging API** (Channel Access Token).  
- **Google Cloud Project** với:  
  - Google Drive API (OAuth2 credentials).  
  - Google Sheets API (OAuth2 credentials).  
  - Google Gemini (Palm) API key (`googlePalmApi`).  
- **Google Spreadsheet** với các cột: `days (date)`, `pic (image ID)`, `url (link)`, `message (advice)`.  
- **Google Drive folder** để lưu ảnh lòng bàn tay.  
- **n8n** (cài trên VPS hoặc Docker).  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. **Tải file JSON** của workflow (từ trang gốc hoặc liên kết chia sẻ).  
2. Vào n8n → **Workflows → Import** → Chọn file JSON → **Import**.  
3. Hoặc **Copy/Paste** toàn bộ JSON vào **Editor → Import from Clipboard**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Dưới đây là danh sách các node quan trọng và cách cấu hình:

| Node | Loại | Mục đích | Cấu hình cần chỉnh |
|------|------|----------|--------------------|
| **LINE_trigger** | webhook | Nhận POST từ LINE | `path` = `8b88a8c6-b25c-43c1-b7fd-351dbf0311bd` (không thay đổi) |
| **config** | set | Lưu **Channel Access Token** và các biến môi trường | Thêm trường `LINE_CHANNEL_ACCESS_TOKEN` (giá trị token) và `BASE_URL` (URL webhook công khai). |
| **Google Gemini Chat Model** | lmChatGoogleGemini | Phân tích ảnh (đọc tay) | Chọn credential **googlePalmApi** → Dán API Key. |
| **PIC_check** | if | Kiểm tra loại tin nhắn (image vs non‑image) | Điều kiện: `{{$json["message"]["type"]}} === "image"` |
| **LINE_input** | httpRequest | Lấy nội dung ảnh từ LINE (download) | Header `Authorization: Bearer {{ $node["config"].json["LINE_CHANNEL_ACCESS_TOKEN"] }}` |
| **LINE_output** | httpRequest | Gửi tin nhắn trả lời cho người dùng | URL: `https://api.line.me/v2/bot/message/reply` + Header Authorization. |
| **Analyze** | chainLlm | Gọi Gemini Vision để “đọc tay” (lần đầu) | Prompt mẫu trong node (được cung cấp sẵn). |
| **PIC_upload** | googleDrive | Lưu ảnh mới lên Drive | Chọn credential **googleDriveOAuth2Api**, folder ID của thư mục lưu ảnh. |
| **Massege_check** | code | Kiểm tra nội dung tin nhắn (đảm bảo là ảnh) | Không cần thay đổi, chỉ kiểm tra `if (!msg)` → trả lời yêu cầu gửi ảnh. |
| **DATA_upload** | googleSheets | Ghi kết quả vào Sheet | Chọn credential **googleSheetsOAuth2Api**, Spreadsheet ID, Sheet Name, `operation: append`. |
| **PIC_Search** | googleDrive | Tải ảnh cũ nhất (nếu có) | `operation: download`, truyền `fileId` từ node trước. |
| **DATA_download** | googleSheets | Đọc toàn bộ lịch sử | Chọn credential, Spreadsheet ID, Sheet Name. |
| **Get latest DATA** | code | Lấy bản ghi mới nhất (dòng cuối) | Trả về `lastRow`. |
| **Check Previous Record Exists** | if | Kiểm tra có bản ghi cũ không | Điều kiện: `{{$node["Get latest DATA"].json.length > 0}}`. |
| **Google Gemini Chat Model1** | lmChatGoogleGemini | So sánh 2 ảnh (hiện tại vs cũ) | Cũng dùng credential **googlePalmApi**, prompt so sánh. |
| **First_Analyze** | chainLlm | Phân tích “đọc tay” lần đầu | Prompt chi tiết cho Gemini Vision. |
| **Reply_Text_Instructions** | httpRequest | Gửi lời khuyên cuối cùng qua LINE | Cấu hình giống **LINE_output**. |
| **DATA_counting** | code | Đếm số ảnh đã lưu (để quyết định có so sánh) | Không cần thay đổi. |
| **Validate Image Pair** | merge | Gộp dữ liệu ảnh hiện tại & cũ cho AI | Đảm bảo cả 2 ảnh đều tồn tại. |
| **image_counting** | code | Đếm số ảnh trong cặp (đảm bảo =2) | Nếu <2 → bỏ qua so sánh. |

> **Lưu ý:**  
> - Tất cả **credential** phải được tạo trong n8n → **Credentials** và gán cho node tương ứng.  
> - Đảm bảo **Google Drive folder** có quyền **Anyone with the link can view** để lấy link công khai (node `PIC_upload` sẽ trả về `webViewLink`).  
> - Đặt **environment variables** trong node `config` để không lộ token trong workflow.

#### 3. Kích hoạt ⚡️
1. **Test run**: Gửi một tin nhắn ảnh thử từ LINE tới webhook URL (được hiển thị trong node `LINE_trigger`).  
2. Kiểm tra:  
   - Ảnh đã được lưu trên Drive.  
   - Dòng mới xuất hiện trong Google Sheet.  
   - Người dùng nhận được tin nhắn trả lời.  
3. Khi mọi thứ ổn → **Bật “Active”** trên thanh công cụ của workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm Slack/Telegram**: Dùng node `httpRequest` để gửi báo cáo hàng ngày tới kênh Slack.  
- **Lưu log chi tiết**: Thêm node `Google Cloud Logging` hoặc `Webhook` để ghi lại toàn bộ payload vào hệ thống giám sát.  
- **Phân tích xu hướng**: Dùng Google Data Studio kết nối với Sheet để vẽ biểu đồ thay đổi “độ khô” theo thời gian.  
- **Giới hạn người dùng**: Thêm node `IF` kiểm tra `userId` để chỉ cho phép một danh sách khách hàng đã đăng ký.

### 📌 Kết luận
Với workflow **“Compare LINE palm images and log Gemini health insights to Google Sheets”**, các sếp có thể biến việc nhận và phân tích ảnh lòng bàn tay thành một quy trình tự động, nhanh chóng và chuẩn xác. Không cần viết một dòng code nào, chỉ cần cấu hình một lần và để n8n chạy suốt ngày đêm. Hãy triển khai ngay hôm nay để nâng cao trải nghiệm khách hàng và tạo dựng dữ liệu sức khỏe lâu dài! 🚀