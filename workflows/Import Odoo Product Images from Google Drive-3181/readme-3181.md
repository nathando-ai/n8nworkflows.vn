---
title: "🚀 Tự Động Nhập Hình Ảnh Sản Phẩm Odoo Từ Google Drive Bằng n8n"
description: "Hướng dẫn chi tiết cách tự động hóa quy trình cập nhật ảnh sản phẩm và template lên hệ thống Odoo trực tiếp từ Google Drive, tiết kiệm hàng giờ thao tác thủ công."
slug: "tu-dong-nhap-hinh-anh-san-pham-odoo-tu-google-drive"
tags: [n8n, automation, odoo, google-drive, no-code, e-commerce]
keywords: [n8n workflow, odoo product images, google drive n8n, tự động hóa odoo, quản lý sản phẩm odoo]
---

# 🚀 Tự Động Nhập Hình Ảnh Sản Phẩm Odoo Từ Google Drive Bằng n8n

Việc quản lý và cập nhật hình ảnh hàng loạt cho hàng trăm, hàng ngàn sản phẩm trên hệ thống ERP Odoo luôn là "nỗi ám ảnh" của các đội ngũ vận hành và quản lý kho. Thao tác thủ công tải ảnh lên, đặt tên theo mã SKU, rồi gắn vào từng sản phẩm vừa tốn thời gian, dễ nhầm lẫn lại vừa làm giảm năng suất làm việc. 

Workflow n8n này sinh ra để giải quyết triệt để bài toán đó! Nó giúp tự động hóa 100% quy trình quét ảnh từ thư mục Google Drive, xử lý, định dạng và đẩy trực tiếp vào các Product Template hoặc Product Variant trên Odoo một cách mượt mà, chính xác.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Không cần kéo thả thủ công từng bức ảnh lên Odoo nữa, hệ thống tự động nhận diện và cập nhật.
- **Đồng bộ chuẩn xác**: Dựa trên mã SKU hoặc ID sản phẩm, workflow tự động khớp ảnh đúng vào sản phẩm tương ứng trên Odoo.
- **Xử lý linh hoạt**: Hỗ trợ đồng thời cả cập nhật ảnh cho Template sản phẩm và Sản phẩm chi tiết (Products).
- **Báo cáo tức thì**: Tự động tổng hợp số lượng ảnh đã xử lý và gửi thông báo qua Google Chat ngay sau khi hoàn thành.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance**: Đã cài đặt n8n (Self-hosted hoặc Cloud).
- **Google Drive Account**: Cần cấp quyền truy cập để n8n quét, tải xuống và quản lý file ảnh trong các thư mục chỉ định.
- **Odoo ERP**: Đã có tài khoản và quyền kết nối API (XML-RPC) với Odoo để đọc/ghi dữ liệu sản phẩm.
- **Google Chat Webhook / Credentials**: Để nhận thông báo trạng thái chạy workflow.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp tiến hành copy mã JSON của workflow này, sau đó vào giao diện n8n Editor, chọn **Add workflow** -> **Import from Clipboard** và dán vào là xong.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy trơn tru, các sếp cần cấu hình chính xác các node trọng điểm sau:

- **Schedule Trigger / Click Manual**: 
  - Nơi thiết lập thời gian tự động chạy ngầm (ví dụ: chạy định kỳ hàng đêm) hoặc bấm chạy thủ công bằng nút `Click Manual`.
- **Find Files & Find Templates / Find Products**:
  - Kết nối tài khoản Google Drive và Odoo của các sếp.
  - Tại node Google Drive (`Find Files`), trỏ đến đúng **Folder ID** chứa ảnh sản phẩm trên Drive của các sếp.
  - Tại các node Odoo (`Find Templates`, `Find Products`), cấu hình đúng Domain/Filter để tìm kiếm chính xác bản ghi sản phẩm cần cập nhật hình ảnh.
- **Convert Base64 Images Templates & Products**:
  - Các node `extractFromFile` này chịu trách nhiệm chuyển đổi tệp nhị phân (binary) sang chuỗi Base64 phù hợp với định dạng đầu vào của API Odoo.
- **Update Images Templates & Update Images Products**:
  - Gửi dữ liệu ảnh đã được mã hóa Base64 vào các trường tương ứng trên Odoo để hoàn tất việc cập nhật hình ảnh sản phẩm.
- **Announce (Google Chat)**:
  - Cấu hình credentials để workflow bắn tin nhắn báo cáo kết quả (số lượng ảnh đã cập nhật thành công, thất bại) về kênh Google Chat của team.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** chạy thử với một vài sản phẩm mẫu để kiểm tra xem ảnh đã bay thẳng vào Odoo chưa.
- Sau khi test ngon nghẻ, bật công tắc **Active** ở góc trên cùng bên phải để workflow tự động chạy ngầm theo lịch trình.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo**: Thay vì chỉ dùng Google Chat, các sếp có thể gắn thêm node Telegram, Slack hoặc Email để nhận báo cáo linh hoạt hơn.
- **Lưu lịch sử (Log)**: Thêm một node Google Sheets hoặc Database ở cuối luồng để lưu lại lịch sử mỗi lần cập nhật ảnh, tiện cho việc kiểm tra đối soát.
- **Tự động dọn dẹp**: Tận dụng các node như `Move Images` hoặc `Drop Old Images` để di chuyển hoặc xóa ảnh trên Google Drive sau khi đã đồng bộ thành công lên Odoo, giúp thư mục luôn gọn gàng.

### 📌 Kết luận
Tự động hóa quy trình cập nhật ảnh sản phẩm Odoo từ Google Drive là bước tiến nhỏ nhưng giúp tiết kiệm cực kỳ nhiều thời gian cho đội ngũ vận hành e-commerce. Hãy triển khai ngay hôm nay để tối ưu hóa hiệu suất làm việc của các sếp nhé!