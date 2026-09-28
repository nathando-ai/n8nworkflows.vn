---
title: "🚀 Tự động giữ sống project Supabase Free Plan bằng n8n Database Ping"
description: "Hướng dẫn thiết lập workflow n8n tự động gọi API và ghi dữ liệu định kỳ vào Supabase, giúp giữ cho các project miễn phí không bị tạm ngưng do không hoạt động."
slug: "tu-dong-giu-song-supabase-free-plan-voi-n8n"
tags: [n8n, automation, supabase, devops, no-code, free-plan]
keywords: [n8n workflow, supabase free plan keep alive, tu dong hoa supabase, giu song supabase, n8n supabase tutorial]
---

# 🚀 Tự động giữ sống project Supabase Free Plan bằng n8n Database Ping

Các sếp có đang sử dụng gói Miễn phí (Free Plan) của Supabase cho các dự án cá nhân hoặc MVP không? Chắc hẳn các sếp đã từng gặp tình cảnh "dở khóc dở cười" khi Supabase tự động tạm ngưng (pause) project sau một thời gian không có hoạt động (inactivity), khiến ứng dụng sập nguồn đột ngột. 

Thay vì phải nhớ thủ công vào dashboard bấm nút hoặc tốn kém nâng cấp lên gói trả phí, workflow n8n này sẽ giải quyết triệt để bài toán trên bằng cách tự động "ping" database định kỳ một cách thông minh và tự nhiên nhất!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Không lo bị khóa project**: Tự động gửi tín hiệu hoạt động định kỳ (mặc định 4 ngày/lần), qua mặt hoàn toàn cơ chế quét "inactivity" của Supabase.
- **Mô phỏng hoạt động tự nhiên**: Sử dụng cơ chế vòng lặp kết hợp độ trễ ngẫu nhiên (random wait từ 20-60 giây) giữa các lần ghi dữ liệu, tạo lưu lượng truy cập giống hệt người dùng thật.
- **Hoạt động hoàn toàn tự động**: Cài một lần và quên đi, tiết kiệm chi phí duy trì cơ sở hạ tầng cho các dự án nhỏ.
- **Dễ dàng mở rộng**: Có thể áp dụng cho nhiều project Supabase khác nhau chỉ với vài thao tác nhân bản workflow.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n đang hoạt động.
- Tài khoản Supabase và thông tin kết nối API (Supabase URL và Service Role / Anon Key).
- Chuẩn bị sẵn một bảng (table) tên là `ping` trong database Supabase với một cột `created_at` (kiểu dữ liệu timestamp).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy mã JSON của workflow này, vào giao diện n8n Editor, chọn **New Workflow**, sau đó nhấn `Ctrl + V` (hoặc `Cmd + V`) để dán toàn bộ các node vào màn hình làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần chú ý cấu hình các node quan trọng sau:

- **Node `Create a row` (Supabase)**:
  - Chọn hoặc tạo mới **Supabase Credentials**. Điền thông tin `Supabase URL` và `Supabase API Key` lấy từ cài đặt project Supabase của các sếp.
  - Chọn đúng bảng (Table) đã tạo là `ping` và ánh xạ trường thời gian vào cột `created_at`.
- **Node `Schedule Trigger`**:
  - Mặc định lịch chạy được thiết lập là cứ mỗi 4 ngày. Các sếp có thể thay đổi tần suất này nếu muốn (ví dụ: 2 hoặc 3 ngày/lần để đảm bảo an toàn tuyệt đối).
- **Node `Code in JavaScript` (Đầu tiên)**:
  - Node này chịu trách nhiệm tạo ra 25 items giả lập để kích hoạt vòng lặp ghi dữ liệu. Các sếp có thể tăng giảm số lượng này tùy ý.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** (hoặc dùng node `When clicking ‘Execute workflow’`) để test thử nghiệm xem dữ liệu có được đẩy thành công vào Supabase hay không.
- Sau khi test xanh mượt, gạt công tắc **Active** góc trên bên phải để n8n tự động vận hành ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp cảnh báo Telegram/Slack**: Thêm một node Telegram hoặc Slack vào cuối chuỗi vòng lặp để nhận thông báo mỗi khi workflow thực hiện xong chu kỳ "keep-alive".
- **Quản lý đa project**: Nhân bản node Supabase để một workflow duy nhất có thể "ping" đồng thời nhiều database Supabase khác nhau của các sếp.
- **Dọn dẹp dữ liệu tự động**: Viết một câu lệnh SQL Cron Job nhỏ trong Supabase để tự động xóa bớt các dòng rác trong bảng `ping` sau mỗi 30 ngày, tránh việc bảng bị phình to không cần thiết.

### 📌 Kết luận
Một giải pháp nhỏ nhưng cực kỳ hữu ích cho các lập trình viên, indie hacker và doanh nghiệp tinh gọn chi phí. Hãy cài đặt ngay workflow này để các project Supabase Free Plan của các sếp luôn sống khỏe 24/7 mà không tốn một xu!