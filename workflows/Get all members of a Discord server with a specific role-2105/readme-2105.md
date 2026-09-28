---
title: "🚀 Tự động quét và lấy danh sách thành viên Discord theo Role với n8n"
description: "Hướng dẫn chi tiết cách sử dụng workflow n8n để tự động lấy danh sách toàn bộ thành viên trong server Discord sở hữu một Role cụ thể, xử lý phân trang và lưu trữ."
slug: "lay-danh-sach-thanh-vien-discord-theo-role-n8n"
tags: [n8n, automation, discord, google-sheets, no-code, api-integration]
keywords: [n8n workflow, discord bot api, lay thanh vien discord, google sheets automation, tu dong hoa discord]
---

# 🚀 Tự động quét và lấy danh sách thành viên Discord theo Role

Các sếp có bao giờ gặp khó khăn khi muốn thống kê, gửi tin nhắn chăm sóc hoặc phân tích danh sách hàng ngàn thành viên sở hữu một Role cụ thể trên server Discord chưa? Việc lọc thủ công bằng cơm chắc chắn là "bất khả thi" khi server lớn dần. 

Đừng lo, bài viết này sẽ hướng dẫn các sếp cách "lên đồ" một workflow n8n cực kỳ thông minh, tự động phân trang (pagination) qua API của Discord, lưu vết tiến độ bằng Google Sheets và lọc chính xác những người dùng có Role mong muốn mà không cần tốn một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Không giới hạn số lượng thành viên (vượt qua giới hạn 100 member/request của Discord nhờ thuật toán phân trang thông minh).
- **Lưu trữ thông minh**: Sử dụng Google Sheets làm bộ nhớ tạm để ghi nhớ vị trí quét (last ID), giúp tránh lỗi timeout hoặc quá giới hạn API.
- **Lọc chuẩn xác**: Chỉ định chính xác Role cần tìm kiếm trên server Discord.
- **Hoạt động linh hoạt**: Có thể kích hoạt thủ công qua Test run hoặc gọi thông qua Webhook URL.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance**: Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Discord Bot**: Cần tạo một Bot trên Discord Developer Portal, cấp quyền `Server Members Intent` và thêm Bot vào server với quyền phù hợp.
- **Google Account**: Chuẩn bị sẵn một Google Sheet để workflow lưu trữ dữ liệu phân trang.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này và paste trực tiếp vào n8n Editor của mình, hoặc import file JSON theo cách thông thường.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình kỹ các node sau:

- **Node `Setup: Edit this to get started`**: 
  - Đây là nơi các sếp khai báo các thông số cơ bản như **Server ID** và **Role ID** cần lọc. 
  - *(Gợi ý: Bật Developer Mode trong Discord để dễ dàng copy các ID này).*
- **Node `Get First 100 Members` & `Get next 100 Members after last ID` (Discord)**:
  - Chọn Credentials loại `discordBotApi` đã kết nối với Bot Discord của các sếp.
  - Trỏ đến đúng Server ID của các sếp.
- **Node `Get ID`, `SaveID`, `Delete ID` (Google Sheets)**:
  - Kết nối tài khoản Google Sheets thông qua `googleSheetsOAuth2Api`.
  - Trỏ tới file Google Sheet chuẩn bị sẵn. File này cần có sẵn một cột tên là **`ID`** để workflow ghi nhớ ID của thành viên cuối cùng trong mỗi lần quét.
- **Node `Webhook` & `Send Response`**:
  - Dùng để kích hoạt workflow thông qua HTTP Request bên ngoài (hoặc trình duyệt). Các sếp có thể đổi đường dẫn tại `path: discord-template` nếu muốn.

#### 3. Kích hoạt ⚡️
- Nhấn **"Test workflow"** hoặc gọi Webhook URL trên trình duyệt để kiểm tra kết quả mẫu.
- Sau khi test thành công, gạt nút **Active** để đưa workflow vào trạng thái vận hành tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng quy trình**: Sau khi lọc được danh sách thành viên có Role, các sếp có thể nối thêm các node như Gửi tin nhắn trực tiếp (Discord DM), gửi thông báo về kênh Telegram/Slack nội bộ, hoặc đồng bộ danh sách này vào CRM/Database.
- **Lưu lịch sử**: Thay vì chỉ ghi nhớ ID cuối cùng, các sếp có thể mở rộng Google Sheets để lưu toàn bộ Username, Discriminator và Joined Date của thành viên phục vụ cho việc thống kê định kỳ.

### 📌 Kết luận
Workflow này là một "vũ khí" cực kỳ mạnh mẽ giúp các Community Manager hoặc nhà quản lý server Discord tiết kiệm hàng giờ đồng hồ làm việc thủ công. Hãy áp dụng ngay vào hệ thống của các sếp để tối ưu hóa vận hành cộng đồng nhé!