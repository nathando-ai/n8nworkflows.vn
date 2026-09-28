---
title: "🚀 Tự động tải lên tệp lớn vào Kommo-AmoCRM với chia nhỏ tự động"
description: "Hướng dẫn chi tiết cách tự động tải lên tệp lớn vào Kommo-AmoCRM bằng n8n, giải quyết vấn đề giới hạn dung lượng tải lên và tối ưu hóa quy trình làm việc."
slug: "tu-dong-tai-len-tep-lon-vao-kommo-amocrm"
tags: [n8n, automation, no-code, amocrm, file-upload]
keywords: [n8n workflow, tự động hóa, tải lên tệp lớn, amocrm, chia nhỏ tệp]
---

# 🚀 Tự động tải lên tệp lớn vào Kommo-AmoCRM với chia nhỏ tự động

[Các sếp đang gặp khó khăn khi tải lên tệp lớn vào Kommo-AmoCRM vì giới hạn dung lượng tải lên. Workflow này sẽ giúp các sếp tự động chia nhỏ tệp lớn thành các phần nhỏ hơn, tải lên từng phần và kết hợp chúng lại thành tệp hoàn chỉnh trong Kommo-AmoCRM.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động chia nhỏ tệp lớn thành các phần nhỏ hơn để vượt qua giới hạn dung lượng tải lên của Kommo-AmoCRM.
- Tiết kiệm thời gian và công sức cho các sếp khi không cần phải tải lên từng phần thủ công.
- Tăng tính chính xác và hiệu quả trong quá trình tải lên tệp lớn.
- Tự động hóa toàn bộ quy trình tải lên, giảm thiểu lỗi do con người gây ra.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Kommo-AmoCRM với quyền truy cập API.
- API Key của Kommo-AmoCRM.
- Tài khoản n8n đã được cài đặt và cấu hình.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Để import workflow, các sếp có thể tải file JSON từ [đây](https://n8n.io/workflows/3922) và import vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

- **loadFile (httpRequest)**: Cấu hình URL của tệp cần tải lên.
- **getUrl (set)**: Cấu hình URL của tệp cần tải lên.
- **getFileSizeInBytes (code)**: Kiểm tra kích thước tệp.
- **createSession (httpRequest)**: Tạo phiên tải lên trong Kommo-AmoCRM.
- **isGraterThenMax (if)**: Kiểm tra xem tệp có vượt quá dung lượng tối đa không.
- **No free disk space (stopAndError)**: Hiển thị lỗi nếu không có dung lượng trống.
- **SplitFileToChunks (code)**: Chia nhỏ tệp thành các phần nhỏ hơn.
- **Loop Over File Chunks (splitInBatches)**: Lặp qua từng phần của tệp.
- **Convert to File (convertToFile)**: Chuyển đổi từng phần thành tệp.
- **hasFile (if)**: Kiểm tra xem tệp có tồn tại không.
- **No file Error (stopAndError)**: Hiển thị lỗi nếu tệp không tồn tại.
- **Convert file to base64 string (extractFromFile)**: Chuyển đổi tệp thành chuỗi base64.
- **Get file (httpRequest)**: Lấy tệp từ URL.
- **Upload file (executeWorkflow)**: Tải lên từng phần của tệp.
- **Get drive url (httpRequest)**: Lấy URL của tệp trong Kommo-AmoCRM.
- **Convert parts to File (convertToFile)**: Chuyển đổi các phần của tệp thành tệp hoàn chỉnh.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để thông báo khi quá trình tải lên hoàn tất.
- Lưu log các hoạt động tải lên để theo dõi và kiểm tra.
- Gửi báo cáo định kỳ về các tệp đã tải lên thành công và thất bại.

### 📌 Kết luận
Workflow này giúp các sếp tự động tải lên tệp lớn vào Kommo-AmoCRM một cách hiệu quả và chính xác. Các sếp chỉ cần cấu hình các node quan trọng và kích hoạt workflow, hệ thống sẽ tự động xử lý toàn bộ quy trình tải lên.