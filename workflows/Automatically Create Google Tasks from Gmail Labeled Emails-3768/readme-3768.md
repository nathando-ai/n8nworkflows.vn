---
title: "🚀 Tự động tạo Google Tasks từ email Gmail có nhãn “To-Do”"
description: "Tự động chuyển email mới có nhãn “To-Do” trong Gmail thành công việc trong Google Tasks, tiết kiệm thời gian và giảm lỗi nhập tay."
slug: "tu-dong-tao-google-tasks-tu-gmail-nhanh"
tags: [n8n, automation, no-code, gmail, google-tasks]
keywords: [n8n workflow, tự động hóa, Gmail, Google Tasks, tạo task từ email]
---

# 🚀 Tự động tạo Google Tasks từ email Gmail có nhãn “To-Do”

Khi các sếp phải xử lý khối lượng email khổng lồ, việc **sao chép nội dung email sang Google Tasks** để theo dõi công việc thường mất thời gian, dễ sai sót và gây lãng phí năng suất.  
Workflow này sẽ **nghe ngay khi có email mới được gắn nhãn “To-Do”**, tự động tạo một task trong Google Tasks chỉ với một cú click “run”. Không cần viết code, không cần thao tác thủ công – mọi thứ diễn ra 100 % tự động.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không còn phải copy‑paste tiêu đề và nội dung email sang Tasks.  
- **Độ chính xác 100 %**: Thông tin được truyền thẳng từ Gmail → Google Tasks.  
- **Cá nhân hoá công việc**: Mỗi email trở thành một task riêng, dễ dàng gắn nhãn, ưu tiên.  
- **Hoạt động liên tục 24/7**: Workflow tự động chạy ngay khi email tới, kể cả ngoài giờ làm.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
1. **Tài khoản Google** có quyền truy cập Gmail và Google Tasks.  
2. **Credentials trong n8n**  
   - `googleApi` → OAuth2 cho Gmail (scope: `https://www.googleapis.com/auth/gmail.readonly`).  
   - `googleTasksOAuth2Api` → OAuth2 cho Google Tasks (scope: `https://www.googleapis.com/auth/tasks`).  
3. **Nhãn Gmail “To-Do”** phải tồn tại. Tạo nhãn này trong Gmail → Settings → Labels nếu chưa có.  
4. **n8n** được cài đặt và có thể truy cập internet để gọi API Google.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Tải file JSON của workflow (từ trang gốc hoặc file đính kèm).  
2. Mở n8n → **Workflows** → **Import** → Chọn file JSON → **Import**.  
   *Hoặc* copy toàn bộ JSON, vào **New Workflow**, nhấn **Import from Clipboard** và dán.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Cấu hình quan trọng | Hướng dẫn chi tiết |
|------|--------------------|--------------------|
| **Gmail Trigger** | **Credentials** | Chọn credential `googleApi` đã tạo. |
| | **Label** | Trong mục **Label**, nhập chính xác tên nhãn: `To-Do`. (Không có dấu cách thừa). |
| | **Trigger on** | Để mặc định “New Email”. Workflow sẽ kích hoạt mỗi khi email mới có nhãn này xuất hiện. |
| **Google Tasks** | **Credentials** | Chọn credential `googleTasksOAuth2Api`. |
| | **Task List ID** | Nếu bạn có nhiều danh sách tasks, chọn ID của danh sách muốn lưu. Để trống sẽ dùng danh sách mặc định. |
| | **Title** | `{{$json["subject"]}}` – tiêu đề email sẽ làm tiêu đề task. |
| | **Notes** | `{{$json["body"]["text"]}}` – nội dung email (định dạng text) sẽ được đưa vào mô tả task. |
| | **Due Date (optional)** | Nếu muốn tự động đặt hạn chót, có thể dùng `{{$json["date"]}}` hoặc tính toán dựa trên `{{ $now.add(2, "day") }}`. |

> **Lưu ý:** Đảm bảo rằng node **Gmail Trigger** được đặt ở đầu workflow và **Google Tasks** nhận dữ liệu từ node này (kết nối “output” → “input”).

#### 3. Kích hoạt ⚡️
1. **Test run**: Nhấn **Execute Workflow** → gửi một email mẫu có nhãn “To-Do”. Kiểm tra trong Google Tasks xem task mới đã xuất hiện chưa.  
2. Nếu mọi thứ ổn, bật **Active** (nút chuyển trạng thái ở góc trên bên phải). Workflow sẽ bắt đầu lắng nghe email 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo Slack/Telegram**: Thêm node Slack hoặc Telegram ngay sau node Google Tasks để gửi tin nhắn “Task mới đã được tạo”.  
- **Ghi log vào Google Sheets**: Dùng node Google Sheets để lưu lại ID task, thời gian tạo, và link email, giúp audit sau này.  
- **Tự động gắn due date**: Dựa trên tiêu đề email (ví dụ “Due: 2024-10-01”) hoặc ngày nhận email + số ngày nhất định.  
- **Archive email sau khi tạo task**: Thêm node Gmail → “Move to Archive” để giữ hộp thư sạch sẽ.  
- **Đánh dấu task đã hoàn thành**: Sử dụng webhook từ Google Tasks để cập nhật trạng thái email (đánh dấu “Done”) khi task được hoàn thành.

### 📌 Kết luận
Với chỉ **2 node** đơn giản, workflow này giúp các sếp **tự động hoá quy trình chuyển email thành task** trong vòng vài giây, giảm tải công việc thủ công và tăng độ chính xác. Hãy **import ngay**, cấu hình credentials, và để n8n làm việc cho bạn 24/7! 🚀