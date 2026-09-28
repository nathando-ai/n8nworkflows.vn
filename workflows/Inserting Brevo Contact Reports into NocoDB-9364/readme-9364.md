---
title: "🚀 Tự Động Đồng Bộ Báo Cáo Liên Hệ Brevo Vào NocoDB Với n8n"
description: "Hướng dẫn chi tiết cách tự động trích xuất dữ liệu báo cáo chiến dịch email từ Brevo và cập nhật vào NocoDB bằng n8n, giúp tối ưu hóa quản lý dữ liệu marketing."
slug: "tu-dong-dong-bo-bao-cao-lien-he-brevo-vao-nocodb-n8n"
tags: [n8n, automation, no-code, brevo, nocodb, marketing-automation]
keywords: [n8n workflow, brevo to nocodb, tự động hóa marketing, đồng bộ dữ liệu email, n8n tutorial tieng viet]
---

# 🚀 Tự Động Đồng Bộ Báo Cáo Liên Hệ Brevo Vào NocoDB

Các sếp làm marketing chắc chắn hiểu cảm giác mệt mỏi thế nào khi phải thủ công xuất báo cáo từ các nền tảng gửi email (như Brevo) rồi ngồi lọc dữ liệu, cập nhật vào cơ sở dữ liệu hoặc Google Sheets để theo dõi tỷ lệ mở, click hay trạng thái blacklisted. Công việc lặp đi lặp lại này vừa ngốn thời gian, vừa dễ xảy ra sai sót dữ liệu.

Được thiết kế bởi chuyên gia tự động hóa **Nima Salimi**, workflow n8n này sẽ giải quyết trọn vẹn bài toán trên. Hệ thống sẽ tự động hóa 100% quá trình lấy báo cáo tương tác liên hệ từ **Brevo API**, xử lý, gom nhóm dữ liệu và cập nhật trực tiếp vào cơ sở dữ liệu **NocoDB** một cách mượt mà và chính xác.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không lo gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Không cần đụng tay xuất file CSV hay copy-paste thủ công hàng ngày.
- **Dữ liệu luôn thời gian thực:** Đồng bộ chính xác các chỉ số quan trọng (`messagesSent`, `delivered`, `opened`, `clicked`, `blacklisted`) từ Brevo sang NocoDB.
- **Xử lý thông minh:** Sử dụng các node Code và Split Out để gom nhóm và xử lý dữ liệu sạch sẽ trước khi ghi vào database.
- **Hoạt động bền bỉ:** Lên lịch chạy tự động định kỳ nhờ `Schedule Trigger` kết hợp hệ thống vòng lặp `Loop` (Split In Batches).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản Brevo (Sendinblue):** Cần lấy API Key / HTTP Header Auth để kết nối lấy báo cáo liên hệ.
- **Tài khoản NocoDB:** Đã thiết lập sẵn một bảng (Table) lưu trữ thông tin email với các cột tương ứng (`email`, `messagesSent`, `delivered`, `opened`, `clicked`, `done`, `blacklisted`). Cần chuẩn bị NocoDB API Token.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Các sếp copy mã JSON của workflow hoặc tải file JSON gốc từ n8n.
- Trong giao diện n8n Editor, chọn **Add workflow** -> **Import from File** (hoặc dùng tổ hợp phím `Ctrl+V` / `Cmd+V` để paste trực tiếp vào màn hình canvas).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 22 nodes được thiết kế tỉ mỉ. Các sếp cần chú ý cấu hình các điểm cốt lõi sau:

- **Schedule Trigger:** Node khởi chạy tự động. Các sếp có thể cấu hình thời gian chạy (ví dụ: chạy mỗi ngày một lần hoặc mỗi tuần tùy theo nhu cầu chiến dịch).
- **Insert Emails from NocoDB:** Node kết nối NocoDB (`getAll` operation). Cần chọn đúng Credentials (`nocoDbApiToken`), cấu hình chính xác Workspace, Project và Table chứa danh sách email cần theo dõi.
- **Get Brevo Contact Report:** Node gọi API của Brevo (`httpRequest`). Cần cấu hình đúng `httpHeaderAuth` với API Key của Brevo để hệ thống có quyền truy xuất báo cáo chi tiết.
- **Các node Code & Split Out:** Nhóm các node `Split Out - ...`, `Code`, `Edit Fields` có sẵn logic JavaScript giúp bóc tách và phân loại trạng thái (đã gửi, đã nhận, đã mở, đã click). Các sếp giữ nguyên logic này trừ khi muốn tùy biến thêm trường dữ liệu.
- **Update NocoDB & Update NocoDB - blacklisted:** Các node cập nhật dữ liệu vào bảng NocoDB. Đảm bảo ánh xạ (Mapping) chính xác giữa các trường dữ liệu đầu ra của workflow với tên cột trong bảng NocoDB của các sếp.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để chạy thử nghiệm thủ công với một vài dữ liệu mẫu, kiểm tra xem dữ liệu từ Brevo có được đẩy vào NocoDB thành công hay không.
- Sau khi kiểm tra mọi thứ hoạt động trơn tru, hãy bật công tắc **Active** ở góc trên bên phải để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa quy trình marketing hơn nữa, các sếp có thể mở rộng workflow này bằng cách:
- **Tích hợp Slack/Telegram:** Thêm node gửi thông báo về kênh chat nội bộ mỗi khi hoàn tất quá trình đồng bộ báo cáo hoặc khi có một lượng lớn liên hệ bị đưa vào danh sách đen (`blacklisted`).
- **Xử lý lỗi (Error Handling):** Thêm nhánh Error Trigger để tự động gửi cảnh báo nếu kết nối Brevo API hoặc NocoDB gặp sự cố.
- **Báo cáo định kỳ:** Kết hợp thêm các node tổng hợp số liệu để gửi email tóm tắt hiệu suất chiến dịch hàng tuần cho cấp quản lý.

### 📌 Kết luận
Việc tự động hóa đồng bộ dữ liệu từ Brevo sang NocoDB không chỉ giúp tiết kiệm hàng giờ đồng hồ thao tác tay mà còn đảm bảo dữ liệu chiến dịch của các sếp luôn minh bạch, chính xác để đưa ra các quyết định marketing kịp thời. Chúc các sếp cài đặt thành công và hẹn gặp lại ở các bài hướng dẫn automation tiếp theo!