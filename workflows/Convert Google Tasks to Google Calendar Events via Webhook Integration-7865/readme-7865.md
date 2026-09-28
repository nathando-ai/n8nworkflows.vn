---
title: "🚀 Chuyển Google Tasks sang Google Calendar tự động qua Webhook"
description: "Tự động tạo sự kiện Google Calendar từ các task Google Tasks chỉ bằng một webhook, tiết kiệm thời gian và tránh lỗi nhập liệu."
slug: "chuyen-google-tasks-sang-google-calendar"
tags: [n8n, automation, no-code, google-tasks, google-calendar, webhook]
keywords: [n8n workflow, tự động hóa, Google Tasks, Google Calendar, webhook integration]
---

# 🚀 Chuyển Google Tasks sang Google Calendar tự động qua Webhook

Bạn có bao giờ phải mở Google Tasks, sao chép tiêu đề, thời gian và dán vào Google Calendar thủ công?  
Việc này không chỉ tốn thời gian mà còn dễ gây sai sót, đặc biệt khi số lượng task ngày càng tăng.  
Workflow **Convert Google Tasks to Google Calendar Events via Webhook Integration** sẽ giải quyết vấn đề này 100% không cần viết code: chỉ cần gửi một payload JSON tới webhook, các task sẽ được chuyển thành sự kiện lịch ngay lập tức và (tùy chọn) xóa bỏ task gốc.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không còn thao tác copy‑paste giữa hai ứng dụng.  
- **Độ chính xác 100%**: Thông tin ngày giờ được chuyển đổi tự động, không bị lỗi nhập sai.  
- **Cá nhân hoá**: Có thể tùy chỉnh màu sắc, thời lượng sự kiện và danh sách task nguồn.  
- **Hoạt động liên tục**: Khi webhook nhận payload, workflow tự động chạy ngay, 24/7.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Google** có quyền truy cập **Google Tasks** và **Google Calendar**.  
- **Credentials** trong n8n:  
  - `googleTasksOAuth2Api` (cho node Google Tasks).  
  - `googleCalendarOAuth2Api` (cho node Google Calendar).  
- **Webhook URL** được cấu hình trong node **Webhook** (đường dẫn `task-to-calendar`).  
- **Tasklist ID** và **Calendar ID** (có thể là `primary`) để điền vào node **Configuration**.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Tải file JSON của workflow từ link gốc: <https://n8n.io/workflows/7865>.  
2. Trong n8n Editor, nhấn **Import** → **Upload JSON** → chọn file vừa tải.  
3. Hoặc copy toàn bộ JSON, vào **New Workflow** → **Import from Clipboard** → dán và **Import**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Cấu hình cần chỉnh | Ghi chú |
|------|-------------------|--------|
| **Webhook** | `path`: `task-to-calendar` <br> `httpMethod`: `POST` | Đảm bảo URL công khai hoặc qua reverse proxy (ngrok, Cloudflare Tunnel). |
| **Configuration (Set)** | `tasklistId` – ID của danh sách Google Tasks <br> `calendarId` – ID Calendar đích (ví dụ `primary`) <br> `defaultMinutes` – thời lượng mặc định (phút) <br> `eventColor` – chỉ số màu trong Google Calendar (0‑11) | Các giá trị này sẽ được dùng cho toàn bộ workflow. |
| **Google Tasks** (node “Google Tasks”) | Chọn **Credentials** `googleTasksOAuth2Api`. <br> Operation: `getAll` (mặc định). | Đảm bảo tài khoản đã cấp quyền **Tasks**. |
| **Date & Time** | Không cần thay đổi nếu muốn dùng định dạng ISO. | Node này chuyển `DueDateTimeSeconds` (epoch) thành chuỗi datetime chuẩn. |
| **If1** | Thiết lập điều kiện **Duplicate Guard**: so sánh tiêu đề và thời gian với các sự kiện gần đây trong Calendar. | Có thể tùy chỉnh thời gian tìm kiếm (ví dụ 1 ngày). |
| **Google Calendar** (node “Google Calendar”) | Chọn **Credentials** `googleCalendarOAuth2Api`. <br> Operation: `create` (tạo sự kiện). | Đảm bảo quyền **Calendar** được cấp. |
| **Google Calendar9** | Operation: `getAll` – dùng để kiểm tra trùng lặp. | Không cần thay đổi nếu dùng default. |
| **Google Tasks1** (node “Google Tasks1”) | Operation: `delete` – xóa task gốc (tùy chọn). | Nếu muốn giữ lại task, tắt node này bằng cách **Deactivate**. |

#### 3. Kích hoạt ⚡️
1. **Test run**: Dùng công cụ Postman hoặc curl để POST payload mẫu:  

   ```bash
   curl -X POST https://your-n8n-domain/webhook/task-to-calendar \
        -H "Content-Type: application/json" \
        -d '{"TaskName":"Pay invoice","DueDateTimeSeconds":1735179600}'
   ```

2. Kiểm tra Google Calendar xem có sự kiện mới được tạo không.  
3. Khi mọi thứ ổn, bật **Active** trên workflow để nó chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo Slack/Telegram**: Thêm node Slack hoặc Telegram ngay sau node tạo sự kiện để gửi tin nhắn báo thành công.  
- **Lưu log vào Google Sheet**: Dùng node Google Sheets để ghi lại mỗi lần chuyển đổi (Task ID, Event ID, thời gian).  
- **Định kỳ đồng bộ**: Kết hợp node **Cron** để mỗi ngày tự động lấy toàn bộ tasks chưa chuyển và tạo sự kiện.  
- **Xử lý đa ngôn ngữ**: Nếu payload chứa tiêu đề bằng tiếng khác, dùng node **Function** hoặc **LLM** để chuẩn hoá trước khi tạo sự kiện.  

### 📌 Kết luận
Với workflow này, các sếp có thể biến việc quản lý công việc cá nhân hoặc đội nhóm thành một quy trình tự động, nhanh chóng và không lỗi. Hãy triển khai ngay trên môi trường n8n của mình, thử nghiệm với payload thực tế và cảm nhận sự khác biệt! 🚀