---
title: "🚀 Xử lý Form Liên Hệ tự động: Xác thực & Lưu trữ MongoDB"
description: "Tự động nhận, kiểm tra và lưu trữ dữ liệu form liên hệ vào MongoDB Atlas, giảm rủi ro lỗi và tăng tốc độ phản hồi."
slug: "xu-ly-form-lien-he-tu-dong-xac-thuc-luu-tru-mongodb"
tags: [n8n, automation, no-code, lead-generation, mongodb, form-validation]
keywords: [n8n workflow, tự động hóa, lưu trữ MongoDB, xác thực form, lead generation]
---

# 🚀 Xử lý Form Liên Hệ tự động: Xác thực & Lưu trữ MongoDB

Khi doanh nghiệp thu thập thông tin khách hàng qua **form liên hệ**, việc nhập liệu thủ công thường gây ra:

* **Lỗi dữ liệu** – sai chính tả, định dạng không đồng nhất.  
* **Rủi ro bảo mật** – dữ liệu chưa được lọc, dễ bị tấn công SQL/NoSQL injection.  
* **Chi phí thời gian** – nhân viên phải kiểm tra, sao chép vào hệ thống CRM hoặc DB.

Workflow **“Process Contact Form Submissions with Validation and MongoDB Storage”** giải quyết 100 % các vấn đề trên mà **không cần viết một dòng code nào**. Từ lúc người dùng bấm “Gửi” trên form, dữ liệu sẽ được:

1. **Kiểm tra** tính hợp lệ và loại bỏ các ký tự nguy hiểm.  
2. **Chuyển đổi** sang chuẩn `snake_case` để đồng nhất với MongoDB.  
3. **Lưu trữ** an toàn vào MongoDB Atlas.  
4. **Thông báo** kết quả thành công ngay cho người dùng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không còn nhập liệu thủ công, giảm 80 % thời gian xử lý.  
- **Độ chính xác cao**: Dữ liệu đã được lọc và chuẩn hoá, giảm lỗi nhập sai.  
- **Bảo mật nâng cao**: Loại bỏ mọi ký tự nguy hiểm trước khi lưu vào DB.  
- **Hoạt động liên tục**: Workflow chạy 24/7, không phụ thuộc vào nhân sự.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
1. **Tài khoản n8n** (Self‑hosted hoặc n8n.cloud).  
2. **MongoDB Atlas** – tạo Cluster, Database và Collection (ví dụ: `lead_db.contacts`). Lấy **Connection String** và **API Key** (nếu dùng IAM).  
3. **Form Front‑end** – có thể là HTML thuần, Webflow, hoặc bất kỳ công cụ nào hỗ trợ webhook.  
4. **Credentials trong n8n**:  
   - `mongoDb` – nhập Connection String, Database, Collection.  
   - `formTrigger` – không cần credential, chỉ cần URL webhook được tạo.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n → **Workflows** → **Import**.  
2. Chọn **Upload JSON** và tải file `process-contact-form.json` (được cung cấp ở phần cuối).  
3. Hoặc **Copy/Paste** toàn bộ JSON vào ô **Import from Clipboard** và nhấn **Import**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Vai trò | Cấu hình cần chỉnh |
|------|---------|--------------------|
| **On form submission** (`formTrigger`) | Đầu vào của workflow, nhận dữ liệu từ form. | - Copy URL webhook được tạo → dán vào `action` của form `<form action="YOUR_WEBHOOK_URL" method="POST">`. |
| **Validate Pattern** (`code`) | Kiểm tra và làm sạch dữ liệu. | - Không cần thay đổi code nếu muốn giữ nguyên logic mặc định. <br> - Nếu muốn tùy chỉnh regex, chỉnh sửa phần `const phoneRegex = ...` trong code. |
| **Edit Fields** (`set`) | Đổi tên trường sang `snake_case`. | - Kiểm tra mapping: `first_name`, `last_name`, `email`, `phone_number`. <br> - Thêm/đổi trường nếu form của bạn có thêm dữ liệu (ví dụ: `company`). |
| **Insert documents** (`mongoDb`) | Lưu dữ liệu vào MongoDB. | - Chọn **Credentials → mongoDb** đã tạo. <br> - **Operation**: `Insert`. <br> - **Collection**: nhập tên collection (ví dụ: `contacts`). <br> - **Document**: để mặc định `{{ $json }}` (dữ liệu đã qua `set`). |
| **Form Ending** (`form`) | Trả về thông báo cho người dùng. | - `Message` (hoặc `HTML`) → “Cảm ơn bạn! Thông tin đã được ghi nhận.” <br> - Có thể tùy chỉnh ngôn ngữ, thêm nút “Quay lại”. |

> **Lưu ý:** Đảm bảo **Credentials** được bật “Allow Access from Anywhere” (hoặc whitelist IP server n8n) để MongoDB chấp nhận kết nối.

#### 3. Kích hoạt ⚡️
1. **Test**: Mở form, nhập dữ liệu mẫu, nhấn “Gửi”. Kiểm tra log của node `Validate Pattern` và `Insert documents`.  
2. Nếu mọi thứ ổn → bật **Active** (nút chuyển đổi ở góc trên bên phải).  
3. Theo dõi **Execution List** để chắc chắn không có lỗi.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo Slack/Telegram**: Thêm node `Slack` hoặc `Telegram` sau `Insert documents` để gửi tin nhắn “🟢 New contact: {{ $json.first_name }} {{ $json.last_name }}”.  
- **Kiểm tra trùng lặp**: Trước khi `Insert`, dùng node `MongoDB` với `Find` để kiểm tra email đã tồn tại chưa, nếu có thì cập nhật (`Update`) thay vì chèn mới.  
- **Ghi log vào Google Sheet**: Thêm node `Google Sheets → Append` để lưu bản sao dữ liệu cho báo cáo nhanh.  
- **Báo cáo định kỳ**: Dùng node `Cron` + `MongoDB → Find` → `Email` để gửi báo cáo danh sách liên hệ mỗi tuần.  

### 📌 Kết luận
Với workflow này, các sếp có thể **tự động hoá toàn bộ quy trình thu thập và lưu trữ lead** chỉ trong vài phút, giảm rủi ro bảo mật và tăng tốc độ phản hồi khách hàng. Hãy **import ngay**, cấu hình MongoDB, và để n8n làm việc cho bạn 24/7! 🚀