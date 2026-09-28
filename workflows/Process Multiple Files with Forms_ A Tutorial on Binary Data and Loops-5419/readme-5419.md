---
title: "🚀 Xử lý nhiều tệp tin từ Form trong n8n: Vòng lặp & Binary Data"
description: "Hướng dẫn chi tiết cách tự động lưu từng tệp tin được tải lên qua Form trong n8n, sử dụng vòng lặp và binary data mà không cần viết code."
slug: "xu-ly-nhieu-tep-tin-form-n8n-vong-lap-binary-data"
tags: [n8n, automation, no-code, file-management, binary-data, loops]
keywords: [n8n workflow, tự động hóa, xử lý file, binary data, vòng lặp]
---

# 🚀 Xử lý nhiều tệp tin từ Form trong n8n: Vòng lặp & Binary Data

Khi doanh nghiệp thu thập tài liệu, hình ảnh hoặc video qua một **Form** duy nhất, thường gặp phải vấn đề:

* **Một sự kiện duy nhất** chứa toàn bộ các tệp tin trong một mảng → khó xử lý từng tệp một.  
* **Thiếu khả năng lưu trữ tự động** → phải tải xuống thủ công, tốn thời gian và dễ sai sót.  
* **Không thể theo dõi tiến độ** khi có hàng chục, hàng trăm file.

Workflow **“Process Multiple Files with Forms”** giải quyết 100 % những đau đầu trên bằng cách:

1. **Tách (Split Out) từng file** thành một sự kiện riêng.  
2. **Vòng lặp (Loop) qua từng binary** để lưu từng file vào ổ đĩa hoặc cloud.  
3. **Đảm bảo dữ liệu binary luôn được truyền** qua các node mà không mất mát.  

Kết quả: **Tự động lưu từng file một cách chính xác, nhanh chóng và có thể mở rộng** mà không cần viết một dòng code nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động lưu hàng loạt file trong giây lát.  
- **Độ chính xác 100 %**: Không còn lỗi “file bị mất” khi truyền binary.  
- **Khả năng mở rộng**: Dễ dàng tích hợp Slack/Telegram để thông báo mỗi khi có file mới.  
- **Hoạt động liên tục 24/7**: Không cần can thiệp thủ công sau khi thiết lập.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n** (phiên bản mới nhất) được cài đặt và chạy.  
- **Quyền ghi** vào thư mục lưu file trên server (hoặc bucket cloud nếu dùng `readWriteFile` với S3).  
- **Form Trigger**: URL của form đã được tạo (có thể dùng n8n Form hoặc tích hợp Google Form).  
- Không cần API key hay credential đặc biệt cho các node trong workflow này.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Vào **n8n → Workflows → Import**.  
2. Chọn **“Import from JSON”**, dán nội dung JSON của workflow (tải từ [link gốc](https://n8n.io/workflows/5419)) hoặc **Upload file** nếu đã lưu dưới dạng `.json`.  
3. Nhấn **Import** → workflow sẽ xuất hiện trên canvas.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Dưới đây là các node quan trọng và cách cấu hình chi tiết:

| Node | Loại | Mô tả & Cấu hình cần chỉnh |
|------|------|----------------------------|
| **Form - Load Multiple Files** | `formTrigger` | - Đặt **Form Name** (ví dụ: “Upload Files”). <br> - Bật **“Allow multiple files”**. <br> - Không cần credentials. |
| **Split Out Files** | `splitOut` | - Để mặc định, node sẽ tách mảng `files` thành các item riêng. <br> - Kiểm tra **“Binary Property Name”** (mặc định là `data`). |
| **Loop Over Items** | `splitInBatches` | - **Batch Size**: `1` (đảm bảo mỗi batch chỉ chứa 1 file). <br> - **Continue On Fail**: `false`. |
| **Save Each File** | `readWriteFile` | - **Operation**: `Write`. <br> - **File Path**: Đường dẫn lưu, ví dụ `/data/uploads/{{ $json["filename"] }}` hoặc `{{ $binary["data"].fileName }}`. <br> - **Binary Property**: `data` (hoặc tên binary được Split Out tạo ra). |
| **Continue Once** | `noOp` | - Đặt **Mode**: `Run Once`. <br> - Node này chỉ để “đóng gói” các item lại thành một sự kiện duy nhất sau khi lưu file. Không cần cấu hình thêm. |

> **Lưu ý quan trọng**: Đảm bảo **binary data** được truyền từ `Split Out` → `Loop Over Items` → `Save Each File`. Kiểm tra trong **Execution > Output** của mỗi node để xác nhận thuộc tính binary (`data`) vẫn tồn tại.

#### 3. Kích hoạt ⚡️
1. **Test run**: Gửi một form mẫu với 2‑3 file. Kiểm tra log của `Save Each File` để xác nhận file đã được ghi vào đúng thư mục.  
2. Khi mọi thứ ổn, bật **Active** (nút chuyển đổi góc trên bên phải). Workflow sẽ tự động xử lý mọi file mới được tải lên.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo Slack/Telegram**: Thêm node `Slack` hoặc `Telegram` ngay sau `Save Each File` để gửi tin nhắn kèm link file.  
- **Lưu log vào Google Sheet**: Dùng node `Google Sheets` để ghi lại `filename`, `size`, `upload time`.  
- **Xử lý ảnh**: Kết hợp node `Image` để resize hoặc watermark trước khi lưu.  
- **Chạy định kỳ cleanup**: Thêm `Cron` + `Delete Files` để xóa file cũ sau N ngày, giảm chi phí lưu trữ.

### 📌 Kết luận
Với workflow này, các sếp có thể **tự động hoá toàn bộ quy trình nhận và lưu trữ file từ Form** chỉ trong vài phút, không cần viết code, không lo mất dữ liệu binary. Hãy **import ngay**, **cấu hình đường lưu**, và **bật Active** – để n8n làm việc thay bạn 24/7! 🚀