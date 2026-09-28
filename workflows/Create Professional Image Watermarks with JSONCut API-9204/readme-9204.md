---
title: "🚀 Tạo watermark chuyên nghiệp cho ảnh bằng JsonCut API – Không cần code"
description: "Giải pháp tự động tải lên ảnh, áp watermark và tải về kết quả chỉ trong vài bước, giúp doanh nghiệp tiết kiệm thời gian và giảm lỗi thủ công."
slug: "tạo-watermark-ảnh-jsoncut-api"
tags: [n8n, automation, no-code, AI, watermark]
keywords: [n8n workflow, tự động hóa, watermark ảnh, JsonCut API, tạo watermark, no-code]
---

# 🚀 Tạo watermark chuyên nghiệp cho ảnh bằng JsonCut API – Không cần code

Bạn đang phải mất hàng giờ để tải lên ảnh, chèn watermark thủ công và tải về kết quả?  
Workflow này sẽ giúp bạn **tự động**:
- Tải lên ảnh gốc và watermark từ form
- Gửi yêu cầu tới JsonCut API để tạo job
- Kiểm tra trạng thái job và tải về ảnh đã watermark
- Xử lý lỗi một cách thông minh

Kết quả: **Tiết kiệm thời gian, giảm sai sót, hoàn thành công việc 100% tự động**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ vài phút tới vài giờ thành vài giây.  
- **Chính xác**: Không còn lỗi thủ công khi chèn watermark.  
- **Cá nhân hóa**: Dễ dàng thay đổi watermark, vị trí, độ trong suốt.  
- **Hoạt động liên tục**: Chạy 24/7 mà không cần giám sát.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
| Tài khoản / Dịch vụ | Mô tả | Ghi chú |
|---------------------|-------|---------|
| **JsonCut API key** | API key để truy cập JsonCut. | Đăng ký tại https://jsoncut.com |
| **n8n** | Self-hosted hoặc n8n.cloud | Đảm bảo phiên bản >= 0.200 |
| **Form Trigger** | Đường dẫn `/b355dccf-d9fa-46e0-9c3c-8d3c743aa037` | Tạo form upload 2 file (Main Image, Watermark) |
| **HTTP Header Auth** | Credentials cho các node HTTP Request | Cấu hình `Authorization: Bearer <API_KEY>` |
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập n8n editor.  
2. Chọn **Import** → **Upload JSON** và tải file `workflow-9204.json` (điểm từ link gốc).  
3. Hoặc copy toàn bộ JSON và dán vào tab **Raw JSON**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Tên node | Cấu hình cần chỉnh | Ghi chú |
|------|----------|---------------------|---------|
| **Form Trigger** | `Form Trigger` | `path` = `b355dccf-d9fa-46e0-9c3c-8d3c743aa037` | Đảm bảo form có 2 file: `mainImage`, `watermarkImage` |
| **Upload Main Image** | `Upload Main Image` | `URL` = `https://api.jsoncut.com/v1/upload`<br>`Headers` → `Authorization: Bearer <API_KEY>`<br>`Body` → `formData` với file `mainImage` | |
| **Upload Watermark** | `Upload Watermark` | Tương tự như trên, file `watermarkImage` | |
| **Merge Uploads** | `Merge Uploads` | `Mode` = `Merge` | Kết hợp 2 file upload thành 1 payload |
| **Create JsonCut Job** | `Create JsonCut Job` | `URL` = `https://api.jsoncut.com/v1/jobs`<br>`Method` = `POST`<br>`Body` → JSON chứa `imageId` và `watermarkId` | |
| **Check JsonCut job Status** | `Check JsonCut job Status` | `URL` = `https://api.jsoncut.com/v1/jobs/{jobId}`<br>`Method` = `GET` | |
| **Wait** | `Wait` | `Duration` = `30s` (hoặc tùy chỉnh) | Đợi job xử lý |
| **If Success** | `If Success` | `Condition` = `{{ $json["status"] === "completed" }}` | |
| **If Error** | `If Error` | `Condition` = `{{ $json["status"] !== "completed" }}` | |
| **Download Image** | `Download Image` | `URL` = `https://api.jsoncut.com/v1/download/{{ $json["imageUrl"] }}`<br>`Method` = `GET` | |
| **Error Stop** | `Error Stop` | Không cần chỉnh | Dừng workflow khi lỗi |
| **Aggregate** | `Aggregate` | `Mode` = `Merge` | Gộp dữ liệu cuối cùng để trả về |
| **StickyNote** | `StickyNote` | Không cần chỉnh | Ghi chú nội bộ |

> **Lưu ý**: Mỗi node HTTP Request cần có **Credentials** `httpHeaderAuth`.  
> Ở **n8n** → **Credentials** → **Create New** → **HTTP Header Auth** → nhập `Authorization: Bearer <API_KEY>` và lưu.

#### 3. Kích hoạt ⚡️
1. **Test run**: Chạy workflow với dữ liệu mẫu (đăng tải 2 file qua form).  
2. Kiểm tra log: Đảm bảo `If Success` được kích hoạt và `Download Image` trả về file.  
3. Khi mọi thứ ổn, bật **Active** cho workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo Slack**: Thêm node `Slack` sau `If Success` để gửi link tải về.  
- **Lưu log vào Google Sheets**: Thêm node `Google Sheets` trong `Aggregate` để ghi lại thông tin job.  
- **Tự động gửi email**: Thêm node `Email` để gửi ảnh đã watermark tới khách hàng.  
- **Định kỳ chạy**: Sử dụng node `Cron` để tự động tạo watermark cho ảnh trong thư mục nhất định.  

### 📌 Kết luận
Workflow “Create Professional Image Watermarks with JSONCut API” là công cụ mạnh mẽ giúp doanh nghiệp **tự động hóa quy trình watermark** mà không cần viết code.  
Hãy triển khai ngay trên VPS của mình, kết nối với JsonCut API, và trải nghiệm sự tiện lợi, chính xác, và tiết kiệm thời gian mà workflow mang lại.  

> **Cùng nhau nâng cao hiệu suất làm việc!** 🚀