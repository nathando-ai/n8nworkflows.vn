---
title: "🚀 Xuất Metadata Icon từ Iconfinder ra HTML & CSV kèm Preview tự động bằng n8n"
description: "Hướng dẫn tự động hóa quy trình lấy toàn bộ icon, metadata, thẻ tag từ tài khoản Iconfinder và xuất ra file HTML có kèm hình ảnh preview cùng file CSV."
slug: "xuat-icon-metadata-iconfinder-html-csv-n8n"
tags: [n8n, automation, no-code, iconfinder, api-integration, data-export]
keywords: [n8n workflow, iconfinder api, xuất metadata icon, tự động hóa n8n, convertToFile n8n]
---

# 🚀 Xuất Metadata Icon từ Iconfinder ra HTML & CSV kèm Preview tự động

Các sếp làm thiết kế, quản lý tài nguyên số hoặc lập trình chắc chắn đã từng đau đầu khi muốn quản lý, lập danh mục (catalog) hoặc trích xuất toàn bộ thư viện icon từ **Iconfinder**. Việc copy thủ công từng đường dẫn, tên icon, tags hay tải ảnh về vừa mất thời gian, vừa dễ thiếu sót. 

Giải pháp là đây! Workflow n8n này sẽ giúp các sếp tự động kết nối với API của Iconfinder, gom toàn bộ thông tin chi tiết, tags, tên icon và tự động đóng gói thành 2 định dạng cực kỳ tiện lợi: **File HTML có hình ảnh xem trước (preview)** và **File CSV** để quản lý trên Excel/Google Sheets. Không cần code phức tạp, tự động hóa 100%!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 99% thời gian:** Thay vì thao tác thủ công hàng giờ, workflow hoàn thành việc quét và tổng hợp toàn bộ icon chỉ trong vài giây.
- **Dữ liệu trực quan:** Tạo sẵn file HTML có giao diện hiển thị hình ảnh preview sắc nét, dễ dàng trình bày hoặc chia sẻ cho team.
- **Quản lý chuyên nghiệp:** Xuất file CSV chứa đầy đủ metadata (tên, tag, iconset) sẵn sàng để import vào các công cụ quản lý tài nguyên.
- **Tự động hóa hoàn toàn:** Kích hoạt bằng một cú click, xử lý gọn gàng hàng loạt dữ liệu từ API của bên thứ ba.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n (Self-hosted hoặc Cloud).
- Tài khoản trên **Iconfinder** (có thể cần tài khoản developer để lấy API Key).
- Token API từ Iconfinder.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần tải file JSON của workflow này và import trực tiếp vào n8n Editor của mình, hoặc copy toàn bộ mã nguồn JSON và paste trực tiếp vào không gian làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần thực hiện lần lượt các bước cấu hình tương ứng với các node trong danh sách:

- **Node `Auth Settings` (Loại: Set):** 
  - Mở node này và cấu hình giá trị `authorization` thành: `Bearer YOUR_TOKEN_HERE` (thay token thật của các sếp vào).
  - Thay đổi giá trị `user` thành `user_id` thu được từ bước kiểm tra bên dưới.

- **Node `Check User ID` (Loại: HTTP Request):** 
  - *Bước 1:* Truy cập vào bất kỳ icon nào thuộc sở hữu của tài khoản trên Iconfinder và copy **icon id** từ URL: `https://www.iconfinder.com/icons/ICON-ID/icon-name`
  - *Bước 2:* Mở node này và nối tiếp `ICON-ID` vào trường URL: `https://api.iconfinder.com/v4/icons/ICON-ID`
  - *Bước 3:* Phần Authorization điền: `Bearer YOUR_TOKEN_HERE`.
  - *Bước 4:* Chạy thử node này để lấy mã số `user_id` hiển thị trong kết quả đầu ra.

- **Các node còn lại (`Get Iconsets`, `Split Iconsets`, `Get Icons Details`, `Extract Tags & Name`, `Create HTML`, `Create CSV`, `Merge`):**
  - Các node này đã được thiết lập sẵn logic thông qua code JavaScript bên trong và cấu hình gọi API (`httpRequest`), các sếp giữ nguyên cấu trúc và chỉ cần đảm bảo các bước xác thực ở trên đã chính xác.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute workflow** thủ công ở node `When clicking ‘Execute workflow’` để test chạy thử với dữ liệu thực tế.
- Kiểm tra các file đầu ra (HTML và CSV) xem đã đúng ý chưa nhé!

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Google Drive / OneDrive:** Thêm node lưu trữ cloud để tự động upload file HTML và CSV vừa xuất lên Google Drive ngay sau khi chạy xong.
- **Gửi thông báo qua Telegram/Slack:** Bắn một tin nhắn kèm file kết quả về group chat của team thiết kế để mọi người luôn cập nhật thư viện icon mới nhất.
- **Lên lịch chạy định kỳ (Cron):** Thay thế `Manual Trigger` bằng `Schedule Trigger` để tự động quét và cập nhật thư viện icon hàng tuần hoặc hàng tháng.

### 📌 Kết luận
Với workflow n8n này, việc quản lý và trích xuất dữ liệu từ Iconfinder không còn là nỗi ám ảnh thủ công nữa. Hãy "lên đồ" ngay cho hệ thống n8n của các sếp để tối ưu hóa năng suất làm việc thôi nào!