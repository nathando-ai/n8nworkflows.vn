---
title: "🚀 Chuyển dữ liệu Typeform thành Spreadsheet tự động"
description: "Tự động lấy dữ liệu từ Typeform, lưu vào file Excel trên NextCloud và cập nhật bảng tính ngay khi có phản hồi mới."
slug: "chuyen-du-lieu-typeform-vao-spreadsheet"
tags: [n8n, automation, no-code, typeform, nextcloud, spreadsheet]
keywords: [n8n workflow, tự động hóa, typeform, nextcloud, spreadsheet]
---

# 🚀 Chuyển dữ liệu Typeform thành Spreadsheet tự động

Bạn đang phải nhập dữ liệu thủ công từ các biểu mẫu Typeform vào bảng tính Excel? Mỗi lần có phản hồi mới, bạn phải tải file, chỉnh sửa, rồi tải lên lại – tốn thời gian, dễ sai sót và làm gián đoạn công việc.  
Workflow **Convert Typeform data into Spreadsheet** của Jan Oberhauser (Founder/CEO of n8n) giúp bạn **tự động 100%**: khi có câu trả lời mới, dữ liệu được ghi vào file Excel trên NextCloud ngay lập tức, không cần một dòng code nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần thao tác thủ công, dữ liệu cập nhật ngay khi có phản hồi.  
- **Chính xác**: Tránh sai sót khi nhập dữ liệu, mọi thay đổi đều được ghi lại chính xác.  
- **Cá nhân hóa**: Dễ dàng mở rộng thêm các trường dữ liệu, tính năng lọc, hoặc gửi báo cáo.  
- **Hoạt động liên tục**: Workflow chạy 24/7, tự động xử lý mọi câu trả lời mới.  
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
- **Tài khoản Typeform** với API key (`typeformApi`).  
- **Tài khoản NextCloud** với API key (`nextCloudApi`).  
- File Excel mẫu `Problems.xls` đã được lưu trong thư mục `examples/` trên NextCloud.  
- Đảm bảo quyền đọc/ghi file trên NextCloud.  
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥

1. Tải file JSON của workflow từ [link gốc](https://n8n.io/workflows/179) hoặc sao chép nội dung JSON.  
2. Mở n8n Editor → **Import** → **Upload JSON** hoặc **Paste JSON**.  
3. Nhấn **Import** để thêm workflow vào hệ thống.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

| Node | Tên Node | Mô tả | Tham số cần cấu hình |
|------|----------|-------|----------------------|
| 1 | **Typeform Trigger** | Nhận dữ liệu khi có câu trả lời mới | `typeformApi` (API key) |
| 2 | **NextCloud** | Tải file Excel mẫu `Problems.xls` | `nextCloudApi` (API key), `operation: download`, `path: examples/Problems.xls` |
| 3 | **Spreadsheet File** | Đọc dữ liệu Excel, chuẩn bị cho merge | Không cần tham số đặc biệt |
| 4 | **Merge** | Kết hợp dữ liệu mới vào bảng tính | Chỉ cần cấu hình trường `merge` (định dạng dữ liệu) |
| 5 | **Spreadsheet File1** | Chuyển dữ liệu đã merge thành file Excel | `operation: toFile` |
| 6 | **NextCloud1** | Upload file Excel đã cập nhật lên NextCloud | `nextCloudApi`, `path: {{$node["NextCloud"].parameter["path"]}}` |

> **Lưu ý**:  
> - Đảm bảo `typeformApi` và `nextCloudApi` đã được tạo trong **Credentials** của n8n.  
> - Kiểm tra lại đường dẫn `path` trong Node **NextCloud** và **NextCloud1** để tránh ghi đè file sai.  
> - Nếu muốn lưu file vào thư mục khác, thay đổi `path` tương ứng.

### 3. Kích hoạt ⚡️

1. Chạy **Test** với dữ liệu mẫu (bấm **Execute Node** ở Node **Typeform Trigger**).  
2. Kiểm tra file Excel trên NextCloud xem dữ liệu đã được cập nhật chưa.  
3. Khi mọi thứ ổn, bật **Active** cho workflow.  
4. Workflow sẽ tự động chạy mỗi khi có câu trả lời mới từ Typeform.

## ✍️ Mẹo & gợi ý nâng cao

- **Thông báo Slack**: Thêm Node **Slack** sau Node **NextCloud1** để gửi tin nhắn khi file được cập nhật.  
- **Email báo cáo**: Sử dụng Node **Email** để gửi bản sao file Excel tới danh sách email.  
- **Lưu log**: Thêm Node **Google Sheets** hoặc **Database** để ghi lại lịch sử cập nhật.  
- **Tự động backup**: Thêm Node **Dropbox** hoặc **Google Drive** để lưu bản sao lưu định kỳ.  

## 📌 Kết luận

Workflow **Convert Typeform data into Spreadsheet** là giải pháp tối ưu giúp các sếp tiết kiệm thời gian, giảm sai sót và duy trì dữ liệu luôn cập nhật. Hãy triển khai ngay trên môi trường n8n của mình, tận hưởng công việc tự động hóa không giới hạn!