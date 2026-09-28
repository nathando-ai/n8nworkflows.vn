---
title: "🚀 Giám sát độ tươi dữ liệu Postgres & Cảnh báo Email tự động"
description: "Theo dõi thời gian cập nhật của các bảng Postgres, tự động gửi email khi dữ liệu cũ hơn ngưỡng cho phép."
slug: "giamsat-postgres-data-freshness-email-alert"
tags: [n8n, automation, no-code, postgres, monitoring, email]
keywords: [n8n workflow, tự động hóa, giám sát postgres, cảnh báo email, dữ liệu tươi]
---

# 🚀 Giám sát độ tươi dữ liệu Postgres & Cảnh báo Email tự động

Các **sếp** thường phải mở công cụ quản trị DB, chạy truy vấn thủ công để kiểm tra xem các bảng quan trọng có được cập nhật thường xuyên hay không.  
Việc này tốn thời gian, dễ bỏ sót và khi dữ liệu cũ gây ra lỗi downstream, hậu quả có thể rất nghiêm trọng.  

**Workflow** này giải quyết hoàn toàn vấn đề: mỗi ngày (hoặc theo lịch bạn định nghĩa) nó sẽ tự động:

1. Lấy bản ghi mới nhất của từng bảng được giám sát.  
2. Tính khoảng thời gian trễ so với thời điểm hiện tại.  
3. Loại bỏ các bảng “tươi” (được cập nhật trong vòng 3 ngày, hoặc ngưỡng bạn đặt).  
4. Gửi email báo cáo danh sách các bảng **stale** (cũ) tới người nhận.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không còn phải chạy query kiểm tra mỗi ngày.  
- **Độ chính xác 100 %**: Kết quả dựa trên dữ liệu thực tế, không phụ thuộc vào con người.  
- **Cảnh báo kịp thời**: Email được gửi ngay khi bảng vượt ngưỡng, ngăn ngừa lỗi downstream.  
- **Hoạt động liên tục**: Workflow chạy tự động 24/7 trên server của bạn.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Postgres**: Một database có ít nhất một bảng cần giám sát.  
- **Cột thời gian**: Mỗi bảng phải có cột `timestamp`, `last_updated` hoặc bất kỳ cột kiểu `date/time` nào ghi thời điểm dữ liệu được ghi/được cập nhật.  
- **Credentials**:  
  - `Postgres` credential (host, port, database, user, password).  
  - `Email` credential (SMTP hoặc dịch vụ email mà node `Execute Workflow` sẽ gọi).  
- **Node “Send alerts”**: Đã được cấu hình để gọi workflow gửi email (có thể dùng workflow mẫu của Kevin hoặc tự xây dựng).  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Tải file JSON của workflow (từ trang gốc hoặc copy nội dung JSON).  
2. Vào **n8n → Workflows → Import** → Chọn file hoặc dán JSON → **Import**.  
3. Đặt tên cho workflow (mặc định: *Postgres Data Freshness Monitoring with Email Alerts*).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Mô tả | Cấu hình cần thay đổi |
|------|------|-----------------------|
| **Schedule Trigger** | Đặt lịch chạy (mặc định mỗi ngày). | Thay `Cron Expression` hoặc `Every X minutes` tùy nhu cầu giám sát. |
| **Loop Over Items** (splitInBatches) | Duyệt qua danh sách các bảng. | Không cần thay đổi nếu danh sách bảng được tạo ở node `Produce tables + date columns`. |
| **Aggregate Stale Tables** | Gom lại danh sách các bảng cũ. | Đảm bảo `Aggregation Mode` là *Append* để tạo mảng kết quả. |
| **Get most recent row from table** (Postgres) | Lấy bản ghi mới nhất của từng bảng. | - Chọn credential `Postgres` đã tạo.<br>- Query mẫu: `SELECT * FROM "{{ $json["table"] }}" ORDER BY "{{ $json["date_column"] }}" DESC LIMIT 1;` <br>- Tham số `table` và `date_column` được truyền từ node trước. |
| **Calculate lag** (dateTime) | Tính số ngày trễ. | `Operation` = *Get Time Between Dates*.<br>Input: `Start Date` = `{{$json["{{date_column}}"]}}`, `End Date` = `{{$now}}`.<br>Output: `lagDays`. |
| **Add back table name** (set) | Gắn lại tên bảng vào kết quả. | Thêm field `table` = `{{$json["table"]}}`. |
| **Remove fresh tables** (filter) | Loại bỏ các bảng còn “tươi”. | Điều kiện: `{{$json["lagDays"]}} > 3` (hoặc giá trị ngưỡng bạn muốn). |
| **Produce tables + date columns** (code) | Tạo mảng các cặp `[table, date_column]` cần giám sát. | Sửa đoạn code JavaScript để trả về danh sách bảng và cột thời gian tương ứng, ví dụ: <br>```js\nreturn [\n  { table: \"orders\", date_column: \"created_at\" },\n  { table: \"users\", date_column: \"last_updated\" }\n];\n``` |
| **Send alerts** (executeWorkflow) | Gọi workflow gửi email. | - Chọn workflow alert (có thể dùng workflow mẫu `6189`).<br>- Đảm bảo truyền `staleTables` (danh sách bảng cũ) vào workflow con. |

#### 3. Kích hoạt ⚡️
1. **Test run**: Chạy workflow một lần với dữ liệu mẫu để kiểm tra output ở mỗi node (sử dụng “Execute Node”).  
2. Nếu mọi thứ ổn, bật **Active** ở góc trên bên phải.  
3. Kiểm tra hộp thư nhận để xác nhận email báo cáo được gửi đúng.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp Slack/Telegram**: Thay node `Execute Workflow` bằng `Slack` hoặc `Telegram` để nhận cảnh báo ngay trên kênh nhóm.  
- **Lưu log chi tiết**: Thêm node `Write Binary File` hoặc `Google Sheets` để ghi lại lịch sử các bảng stale theo thời gian.  
- **Đa môi trường**: Sử dụng `Environment Variables` cho thông tin DB và ngưỡng ngày trễ, giúp dễ dàng chuyển đổi giữa dev, staging và prod.  
- **Tự động mở ticket**: Kết nối với Jira hoặc Asana để tự động tạo ticket khi bảng cũ được phát hiện.

### 📌 Kết luận
Với workflow này, các sếp sẽ **không còn lo lắng** về việc dữ liệu trong Postgres bị treo lâu ngày nữa.  
Chỉ cần một lần cấu hình, hệ thống sẽ tự động giám sát, tính toán và gửi cảnh báo kịp thời, giúp duy trì độ tin cậy cao cho các pipeline downstream.  

👉 **Áp dụng ngay** để bảo vệ dữ liệu và giảm thiểu rủi ro vận hành!