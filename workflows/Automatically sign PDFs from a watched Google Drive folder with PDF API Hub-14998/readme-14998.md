---
title: "🚀 Tự Động Ký PDF Từ Thư Mục Google Drive Với PDF API Hub"
description: "Giải pháp tự động ký PDF ngay khi file được tải lên Google Drive, không cần viết code, tiết kiệm thời gian và giảm lỗi."
slug: "tu-dong-ky-pdf-tu-google-drive"
tags: [n8n, automation, no-code, pdf, google-drive, api-integration]
keywords: [n8n workflow, tự động ký PDF, PDF API Hub, Google Drive, no-code automation]
---

# 🚀 Tự Động Ký PDF Từ Thư Mục Google Drive Với PDF API Hub

Khi doanh nghiệp phải xử lý hàng chục, hàng trăm tài liệu PDF mỗi ngày, việc ký tay thủ công trên mỗi file không chỉ tốn thời gian mà còn dễ gây sai sót. Các sếp thường phải chờ đợi, mất năng suất và khó duy trì tính nhất quán trong quy trình ký tài liệu.  

**Workflow này** sẽ tự động phát hiện file PDF mới trong một thư mục Google Drive, ký điện tử bằng PDF API Hub và lưu lại file đã ký vào cùng thư mục (hoặc thư mục khác) – **hoàn toàn không cần viết một dòng code nào**.

:::info[Gợi ý hạ tầng cho n8n]  
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]  
- **Tiết kiệm thời gian**: Tự động ký ngay khi PDF được tải lên, không cần thao tác thủ công.  
- **Độ chính xác 100 %**: Không còn lỗi “quên ký” hay ký sai tài liệu.  
- **Tính liên tục**: Workflow chạy 24/7, luôn sẵn sàng xử lý mọi file mới.  
- **Dễ mở rộng**: Có thể thêm thông báo Slack, email hoặc lưu log chi tiết.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]  
- **Tài khoản Google** với quyền **Google Drive API** (OAuth2 credentials).  
- **API Key** của **PDF API Hub** (đăng ký tại https://pdfapihub.com).  
- Thư mục Google Drive mà các sếp muốn “giám sát”.  
- (Tùy chọn) Email hoặc Slack webhook nếu muốn nhận thông báo sau khi ký.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Đăng nhập vào n8n Dashboard.  
2. Click **Import** → **Upload JSON** và chọn file `pdf-sign-from-gdrive.json` (được đính kèm trong mục **Resources** của bài viết).  
   *Hoặc* copy toàn bộ JSON và dán vào **Import from Clipboard**.  

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Dưới đây là danh sách các node chính trong workflow và hướng dẫn cấu hình chi tiết:

| Node | Mô tả | Cấu hình quan trọng |
|------|------|----------------------|
| **Google Drive Trigger** | Lắng nghe sự kiện **New File** trong thư mục được chỉ định. | - **Folder ID**: ID của thư mục Google Drive muốn giám sát.<br>- **Credentials**: Chọn Google OAuth2 credentials đã tạo. |
| **IF** | Kiểm tra file có phải là PDF không. | - **Condition**: `{{$json["mimeType"]}}` **equals** `application/pdf`. |
| **Set** (optional) | Đặt các biến tạm thời như `fileId`, `fileName`, `signerName`. | - Thêm trường `signerName` (tên người ký) hoặc `signatureImageUrl` nếu muốn ký bằng hình ảnh. |
| **PDF API Hub – PDF Split/Merge** (sử dụng **Sign**) | Gửi file PDF tới PDF API Hub để ký điện tử. | - **Operation**: `Sign PDF`.<br>- **File Binary**: Chọn `binaryData` từ node trigger.<br>- **Signature Text / Image**: Nhập nội dung ký hoặc URL ảnh ký.<br>- **API Key**: Chọn credential PDF API Hub. |
| **Google Drive (Upload)** | Lưu file PDF đã ký trở lại Google Drive. | - **Folder ID**: Thư mục đích (có thể là cùng thư mục hoặc thư mục “Signed”).<br>- **File Name**: `{{$json["name"]}}_signed.pdf`.<br>- **Binary Data**: Kết nối output của node PDF API Hub. |
| **Sticky Note** | Ghi chú hướng dẫn hoặc thông tin bổ sung cho người dùng. | Không cần cấu hình, chỉ dùng để hiển thị thông tin trong editor. |

**Bước cấu hình chi tiết:**

1. **Google Drive Trigger**  
   - Vào **Credentials** → **Create New** → Chọn **Google OAuth2 API** → Điền `Client ID`, `Client Secret`, `Redirect URI` (theo hướng dẫn n8n).  
   - Chọn **Folder ID** bằng cách mở thư mục trên Drive, sao chép phần cuối URL (`https://drive.google.com/drive/folders/<FOLDER_ID>`).  

2. **IF Node**  
   - Ở tab **Conditions**, nhập: `{{$json["mimeType"]}}` → `equals` → `application/pdf`.  

3. **Set Node** (nếu cần)  
   - Thêm trường `signerName` = “Công ty XYZ”.  
   - Thêm trường `signatureImageUrl` = URL công khai của ảnh chữ ký (nếu ký bằng hình).  

4. **PDF API Hub – PDF Split/Merge**  
   - Chọn **Operation**: `Sign PDF`.  
   - Đối với **Signature Type**, chọn `Text` hoặc `Image` tùy nhu cầu.  
   - Điền **Signature Text** (ví dụ: “Approved by {{ $json["signerName"] }}”) hoặc **Signature Image URL**.  
   - Đảm bảo **API Key** được gắn vào credential `PDF API Hub`.  

5. **Google Drive (Upload)**  
   - Chọn **Folder ID** (có thể tạo thư mục “Signed PDFs”).  
   - Đặt **File Name**: `{{$json["name"]}}_signed.pdf`.  
   - Đảm bảo **Binary Data** được kéo từ node PDF API Hub (`binaryData`).  

6. **Lưu & Kích hoạt**  
   - Nhấn **Save** ở góc trên bên phải.  

#### 3. Kích hoạt ⚡️
- **Test run**: Thêm một file PDF mẫu vào thư mục Google Drive đã chỉ định. Kiểm tra log của n8n để xem workflow chạy thành công và file ký được tạo trong thư mục đích.  
- Khi mọi thứ ổn, bật **Active** ở góc trên cùng của workflow.  

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo Slack/Telegram**: Thêm node **Slack** hoặc **Telegram** sau node Upload để gửi tin nhắn “PDF đã ký thành công” kèm link file.  
- **Lưu log chi tiết**: Dùng node **Google Sheets** hoặc **Airtable** để ghi lại thời gian ký, tên file, người ký.  
- **Ký đa chữ ký**: Sử dụng nhiều node **PDF API Hub – Sign PDF** nối tiếp nhau để thêm nhiều chữ ký (ví dụ: người ký 1, người ký 2).  
- **Xử lý lỗi**: Thêm node **Error Trigger** để gửi email khi workflow gặp lỗi (ví dụ: API key hết hạn).  

### 📌 Kết luận
Với workflow này, các sếp có thể **tự động ký PDF** ngay khi tài liệu được tải lên Google Drive, giảm thiểu công việc thủ công, tăng độ chính xác và duy trì quy trình làm việc liên tục. Hãy triển khai ngay để trải nghiệm hiệu quả tự động hoá thực sự! 🚀