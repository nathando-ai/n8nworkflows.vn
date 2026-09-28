---
title: "🔍 Tự động hóa tìm kiếm thông tin LinkedIn với UniPile - Workflow n8n"
description: "Tự động hóa việc tìm kiếm thông tin người dùng và tổ chức trên LinkedIn bằng UniPile trong n8n. Tiết kiệm thời gian và nâng cao hiệu quả làm việc."
slug: "tu-dong-hoa-tim-kiem-thong-tin-linkedin-voi-unipile"
tags: [n8n, automation, no-code, LinkedIn, UniPile]
keywords: [n8n workflow, tự động hóa, LinkedIn, UniPile, tìm kiếm thông tin]
---

# 🔍 Tự động hóa tìm kiếm thông tin LinkedIn với UniPile - Workflow n8n

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp thường gặp khó khăn khi phải tìm kiếm thông tin chi tiết về người dùng hoặc tổ chức trên LinkedIn một cách thủ công. Quá trình này tốn thời gian, không hiệu quả và dễ gây lỗi. Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình tìm kiếm thông tin từ UniPile, giúp tiết kiệm thời gian và nâng cao hiệu quả làm việc.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa toàn bộ quá trình tìm kiếm thông tin.
- Chính xác: Giảm thiểu lỗi do nhập liệu thủ công.
- Cá nhân hóa: Lấy thông tin chi tiết về người dùng hoặc tổ chức trên LinkedIn.
- Hoạt động liên tục: Chạy 24/7 mà không cần can thiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản UniPile và API Key để truy cập dữ liệu.
- Thông tin về người dùng hoặc tổ chức cần tìm kiếm.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Để import workflow này vào n8n, các sếp có thể làm theo các bước sau:

1. Truy cập vào n8n Editor.
2. Nhấn vào nút "Import from URL" và dán link sau: [https://n8n.io/workflows/4890](https://n8n.io/workflows/4890).
3. Hoặc, các sếp có thể tải file JSON từ link trên và import trực tiếp vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

- **When Executed by Another Workflow**: Node này được sử dụng để kích hoạt workflow từ một workflow khác. Các sếp cần đảm bảo rằng workflow này được kích hoạt đúng cách từ workflow chính.

- **Get Linkedin User Data from Unipile**: Node này thực hiện yêu cầu HTTP để lấy thông tin người dùng từ UniPile. Các sếp cần cấu hình credentials cho node này bằng cách thêm API Key của UniPile.

- **Set User Data from Unipile**: Node này thiết lập dữ liệu người dùng từ UniPile. Các sếp cần đảm bảo rằng dữ liệu được lấy từ node trước đó được xử lý đúng cách.

- **Group in one object - User**: Node này nhóm dữ liệu người dùng thành một đối tượng duy nhất. Các sếp cần kiểm tra dữ liệu đầu ra để đảm bảo rằng nó được nhóm đúng cách.

- **Get Linkedin Org Data from Unipile**: Node này thực hiện yêu cầu HTTP để lấy thông tin tổ chức từ UniPile. Các sếp cần cấu hình credentials cho node này bằng cách thêm API Key của UniPile.

- **Set Linkedin Org Data from Unipile**: Node này thiết lập dữ liệu tổ chức từ UniPile. Các sếp cần đảm bảo rằng dữ liệu được lấy từ node trước đó được xử lý đúng cách.

- **Group in one object - Org**: Node này nhóm dữ liệu tổ chức thành một đối tượng duy nhất. Các sếp cần kiểm tra dữ liệu đầu ra để đảm bảo rằng nó được nhóm đúng cách.

- **Set unable to find data object**: Node này thiết lập đối tượng không tìm thấy dữ liệu. Các sếp cần đảm bảo rằng đối tượng này được thiết lập đúng cách khi không tìm thấy thông tin người dùng hoặc tổ chức.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để thông báo kết quả tìm kiếm.
- Lưu log các lần tìm kiếm để theo dõi hiệu suất.
- Gửi báo cáo định kỳ về các thông tin tìm kiếm quan trọng.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa việc tìm kiếm thông tin người dùng và tổ chức trên LinkedIn một cách hiệu quả và chính xác. Với các bước cấu hình đơn giản và các lưu ý quan trọng, các sếp có thể áp dụng ngay workflow này để nâng cao hiệu quả làm việc.