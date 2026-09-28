---
title: "🚀 Tự động chụp ảnh website từ Google Sheets & lưu vào Drive với Dumpling AI"
description: "Workflow n8n giám sát Google Sheets, gửi URL tới Dumpling AI để chụp screenshot toàn trang, tải về và lưu tự động vào Google Drive."
slug: "tu-dong-chup-anh-website-google-sheets-drive-dumpling-ai"
tags: [n8n, automation, no-code, file-management, multimodal-ai]
keywords: [n8n workflow, tự động hóa, screenshot website, Google Sheets, Google Drive, Dumpling AI]
---

# 🚀 Tự động chụp ảnh website từ Google Sheets & lưu vào Drive với Dumpling AI

Bạn đã bao giờ phải mở từng tab trình duyệt, chụp màn hình thủ công, rồi lưu lại vào ổ đĩa mỗi khi có một URL mới trong bảng tính?  
Công việc này vừa tốn thời gian, vừa dễ sai sót, đặc biệt khi số lượng URL tăng nhanh.  

**Workflow này** sẽ giải quyết hoàn toàn vấn đề: mỗi khi một dòng mới (URL) được thêm vào Google Sheet, n8n sẽ tự động:

1. Gửi URL tới **Dumpling AI** để tạo screenshot toàn trang.  
2. Tải file ảnh về.  
3. Đưa ảnh lên **Google Drive** trong thư mục bạn chỉ định.  

Tất cả chỉ bằng một workflow, không cần viết code!

:::info[Gợi ý hạ tầng cho n8n]  
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]  
- **Tiết kiệm thời gian**: Không còn thao tác mở trình duyệt, chụp, lưu thủ công.  
- **Độ chính xác 100%**: Ảnh luôn được tạo từ URL chính xác, không bị nhầm lẫn.  
- **Tự động hoá 24/7**: Khi có URL mới, workflow tự động chạy ngay.  
- **Quản lý tập trung**: Tất cả screenshot được lưu trong một folder Google Drive, dễ tìm, dễ chia sẻ.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]  
- **Tài khoản Google** với quyền **Google Sheets** và **Google Drive** (OAuth2).  
- **API Key/Dumpling AI**: Đăng ký tại https://dumpling.ai và lấy `Authorization` token.  
- **n8n** đã cài đặt (Self‑hosted hoặc Cloud).  
- Google Sheet có cột chứa URL (ví dụ: cột `A`).  
- Thư mục Google Drive nơi sẽ lưu screenshot (cần ID folder).  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. **Tải file JSON** của workflow (từ link gốc hoặc file đính kèm).  
2. Vào n8n → **Workflows** → **Import** → Chọn file JSON → **Import**.  
   *Hoặc* copy toàn bộ JSON, vào **New Workflow** → **Import from Clipboard** → Dán và **Import**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Cấu hình cần chỉnh | Ghi chú |
|------|-------------------|---------|
| **Watch New Row in Google Sheets** | - Chọn **Credential** `googleSheetsTriggerOAuth2Api`.<br>- Chọn **Spreadsheet ID** và **Sheet Name**.<br>- Đánh dấu **Trigger on New Row**. | Đảm bảo cột chứa URL được xác định (ví dụ: `A`). |
| **Request Screenshot from Dumpling AI** | - Credential `httpHeaderAuth` → nhập **Authorization**: `Bearer <YOUR_DUMPLING_API_KEY>`.<br>- Method: `POST`.<br>- URL: `https://api.dumpling.ai/v1/screenshot`.<br>- Body (JSON): `{ "url": {{$json["URL"]}} }` (thay `URL` bằng tên trường trong Google Sheet). | Kiểm tra định dạng JSON, thêm header `Content-Type: application/json`. |
| **Download Screenshot** | - Method: `GET`.<br>- URL: `{{$json["data"]["screenshotUrl"]}}` (đường dẫn trả về từ node trước). | Không cần credential, chỉ cần truyền URL động. |
| **Upload Screenshot to Google Drive** | - Credential `googleDriveOAuth2Api`.<br>- **Folder ID**: ID của thư mục Drive muốn lưu.<br>- **File Name**: `{{$json["data"]["fileName"]}}.png` hoặc tự tạo tên dựa trên URL.<br>- **Binary Data**: Chọn **Binary Property** là `data` (được tạo ở node Download). | Đảm bảo quyền ghi vào folder đã chọn. |

> **Lưu ý:** Sau khi cấu hình, nhấn **Execute Workflow** để chạy thử với một URL mẫu, kiểm tra xem file screenshot có xuất hiện trong Drive chưa.

#### 3. Kích hoạt ⚡️
- Khi mọi thứ đã chạy ổn định, bật **Active** ở góc trên bên phải của workflow.  
- Đặt **Execution Mode** là **Manual** (để trigger tự động) hoặc **Cron** nếu muốn kiểm tra định kỳ.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo Slack/Telegram**: Thêm node Slack hoặc Telegram để gửi tin nhắn kèm link Drive mỗi khi screenshot mới được tạo.  
- **Lưu log vào Google Sheet**: Ghi lại thời gian, URL, link Drive vào một sheet phụ để theo dõi.  
- **Batch processing**: Nếu muốn xử lý nhiều URL cùng lúc, dùng node **SplitInBatches** trước khi gọi Dumpling AI.  
- **Chuyển đổi định dạng**: Thêm node **ImageMagick** (nếu có) để chuyển PNG → JPEG, giảm dung lượng.  

### 📌 Kết luận
Với workflow này, các sếp có thể biến việc quản lý hình ảnh website từ “công việc tẻ nhạt” thành một quy trình tự động, nhanh chóng và không lỗi. Hãy triển khai ngay, để tập trung vào những việc quan trọng hơn! 🚀