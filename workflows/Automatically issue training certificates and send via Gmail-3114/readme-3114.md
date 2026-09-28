---
title: "🚀 Tự động cấp chứng chỉ đào tạo và gửi email qua Gmail"
description: "Workflow tự động tạo chứng chỉ đào tạo cá nhân hoá, chèn tên, UUID và gửi ngay qua Gmail, giảm 100% công việc thủ công."
slug: "tu-dong-cap-chung-chi-dao-tao-gui-gmail"
tags: [n8n, automation, no-code, email, certificate, training]
keywords: [n8n workflow, tự động hóa, chứng chỉ đào tạo, Gmail, tạo ảnh, crypto]
---

# 🚀 Tự động cấp chứng chỉ đào tạo và gửi email qua Gmail

Khi tổ chức các buổi đào tạo, việc **tạo chứng chỉ** cho từng học viên, **điền tên**, **mã số** và **gửi email** một cách thủ công thường tốn hàng giờ đồng hồ, dễ gây lỗi sai và làm giảm trải nghiệm chuyên nghiệp.  
Workflow **“Automatically issue training certificates and send via Gmail”** giải quyết toàn bộ quy trình này trong **giây lát**, không cần viết một dòng code nào – chỉ cần kéo thả các node trong n8n.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ vài giờ giảm còn vài giây.  
- **Độ chính xác 100%**: Không còn lỗi chính tả hay sai mã chứng chỉ.  
- **Cá nhân hoá**: Mỗi chứng chỉ có tên và UUID duy nhất.  
- **Hoạt động liên tục**: Tự động gửi ngay khi có học viên mới đăng ký.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Gmail** (có bật API Gmail) và **OAuth2 credentials** trong n8n.  
- **Datastore “n8n training”** đã được tạo sẵn (cung cấp dữ liệu học viên: tên, email).  
- **URL mẫu ảnh chứng chỉ** (PNG/JPEG) có thể truy cập công khai để `httpRequest` tải về.  
- **Quyền truy cập internet** cho node `httpRequest`.  
- **n8n** phiên bản mới nhất (đủ 9 node).  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n → **Workflows** → **Import**.  
2. Chọn **Upload JSON** và tải file `Automatically_issue_training_certificates_and_send_via_Gmail.json` (được cung cấp ở phần cuối).  
3. Hoặc **Copy/Paste** nội dung JSON vào ô **Import from Clipboard** và nhấn **Import**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Dưới đây là danh sách **9 node** trong workflow và các thiết lập quan trọng:

| Node | Loại | Cấu hình cần chỉnh |
|------|------|-------------------|
| **When clicking ‘Test workflow’** | `manualTrigger` | Không cần thay đổi, dùng để test. |
| **Customer Datastore (n8n training)** | `n8nTrainingCustomerDatastore` | Chọn **Datastore** “n8n training”. Đảm bảo **Credentials** có quyền **Read**. |
| **Write Text(name)** | `editImage` | - **Image**: Đầu vào từ node **Load Image**.<br>- **Text**: `{{$json["name"]}}` (lấy tên học viên).<br>- **Position**, **Font**, **Size**: tùy mẫu chứng chỉ. |
| **Write Text(uuid)** | `editImage` | - **Text**: `{{$json["uuid"]}}` (UUID được tạo ở node **Generate Crypto**).<br>- Đặt vị trí phù hợp trên ảnh. |
| **Get Email & Name** | `set` | - **Fields**: `email` ← `{{$json["email"]}}`<br>- **name** ← `{{$json["name"]}}`<br>- Dùng để truyền dữ liệu cho các node sau. |
| **Generate Crypto** | `crypto` | - **Operation**: **Generate UUID** (hoặc **Random String**).<br>- **Output Field**: `uuid`. |
| **Load Image** | `httpRequest` | - **Method**: **GET**.<br>- **URL**: Đường link tới mẫu ảnh chứng chỉ (ví dụ: `https://example.com/certificate-template.png`).<br>- **Response Format**: **File**. |
| **Get Info** | `editImage` | - **Input Image**: Kết quả từ **Write Text(uuid)**.<br>- **Add Text**: Kết hợp tên và UUID đã chèn.<br>- **Output**: Ảnh chứng chỉ hoàn chỉnh (binary). |
| **Send Email** | `gmail` | - **Credentials**: Chọn OAuth2 Gmail đã cấu hình.<br>- **To**: `{{$json["email"]}}`.<br>- **Subject**: “Chứng chỉ hoàn thành khóa đào tạo”.<br>- **Body**: Nội dung email tùy chỉnh.<br>- **Attachments**: `{{$node["Get Info"].binary.data}}` (ảnh chứng chỉ). |

**Lưu ý quan trọng**  
- Đảm bảo **Credentials** cho Gmail có quyền **Send email** và **Scope** `https://www.googleapis.com/auth/gmail.send`.  
- Kiểm tra **CORS** nếu mẫu ảnh được lưu trên CDN có giới hạn truy cập.  
- Nếu muốn lưu bản sao chứng chỉ vào Google Drive/Dropbox, thêm node **Google Drive** sau **Get Info**.

#### 3. Kích hoạt ⚡️
1. **Test run**: Nhấn nút **Execute Workflow** → **Run Node** từ node **When clicking ‘Test workflow’**. Kiểm tra email nhận được và hình ảnh chứng chỉ.  
2. Nếu mọi thứ ổn, bật **Active** (nút chuyển đổi ở góc trên bên phải).  
3. Đặt **Trigger** (ví dụ: webhook hoặc schedule) nếu muốn tự động chạy khi có học viên mới được thêm vào datastore.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối Slack/Telegram**: Thêm node **Slack** hoặc **Telegram** để thông báo “Cấp chứng chỉ thành công” cho admin.  
- **Lưu log**: Dùng node **Postgres/MySQL** hoặc **Google Sheets** để ghi lại `email`, `name`, `uuid`, thời gian gửi.  
- **Chuyển đổi PDF**: Thêm node **Convert Image to PDF** (hoặc dùng API bên ngoài) để gửi chứng chỉ dưới dạng PDF.  
- **Batch processing**: Thay `manualTrigger` bằng **Cron** (hàng ngày) + **Read from Datastore** để tự động xử lý tất cả học viên chưa có chứng chỉ.  
- **Tùy biến mẫu**: Sử dụng **Handlebars** trong node **Set** để tạo nội dung email đa ngôn ngữ.

### 📌 Kết luận
Với workflow này, các sếp có thể **tự động hoá toàn bộ quy trình cấp chứng chỉ** – từ tạo ảnh, chèn thông tin cá nhân, tới gửi email ngay lập tức. Không còn mất thời gian vào công việc lặp lại, giảm thiểu sai sót và nâng cao hình ảnh chuyên nghiệp của doanh nghiệp. Hãy **import ngay**, **cấu hình nhanh** và **bật hoạt động** để trải nghiệm tự động hoá 100%!

---