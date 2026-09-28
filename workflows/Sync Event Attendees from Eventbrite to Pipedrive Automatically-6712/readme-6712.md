---
title: "🚀 Tự động đồng bộ danh sách người tham gia sự kiện từ Eventbrite sang Pipedrive"
description: "Hướng dẫn chi tiết cách tự động đồng bộ danh sách người tham gia sự kiện từ Eventbrite sang Pipedrive bằng n8n, tiết kiệm thời gian và tránh lỗi thủ công"
slug: "tu-dong-dong-bo-danh-sach-nguoi-tham-gia-tu-eventbrite-sang-pipedrive"
tags: [n8n, automation, no-code, eventbrite, pipedrive]
keywords: [n8n workflow, tự động hóa, eventbrite, pipedrive, đồng bộ dữ liệu]
---

# 🚀 Tự động đồng bộ danh sách người tham gia sự kiện từ Eventbrite sang Pipedrive

[Các sếp] có biết rằng việc đồng bộ thủ công danh sách người tham gia sự kiện giữa Eventbrite và Pipedrive là một công việc tẻ nhạt và dễ gây lỗi? Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình này trong vòng chưa đầy 10 phút, đảm bảo dữ liệu luôn đồng bộ và chính xác.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động đồng bộ dữ liệu mà không cần can thiệp thủ công
- **Chính xác**: Loại bỏ rủi ro lỗi khi nhập liệu thủ công
- **Tối ưu hóa quy trình**: Tự động hóa toàn bộ quá trình từ Eventbrite đến Pipedrive
- **Dữ liệu luôn cập nhật**: Đồng bộ liên tục theo lịch trình đã thiết lập
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Eventbrite với quyền truy cập API
- Tài khoản Pipedrive với quyền truy cập API
- Token OAuth cá nhân của Eventbrite
- ID tổ chức Eventbrite
- Các sếp cần có kiến thức cơ bản về n8n và cách thiết lập credentials
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể import workflow này bằng cách:
1. Truy cập vào n8n Editor
2. Chọn "Workflows" → "Import from File" (hoặc "Paste JSON")
3. Copy nội dung JSON của workflow và dán vào hoặc tải file JSON lên
4. Lưu workflow với tên phù hợp

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần thực hiện các bước sau để workflow hoạt động đúng:

1. **Cập nhật node "Extract Eventbrite Signups"**:
   - Mở node Code đầu tiên trong workflow
   - Thay thế `ZZZZZZZZZZZZZZZZZZZZ` bằng **token OAuth cá nhân của Eventbrite**
   - Thay thế `1111111111111` bằng **ID tổ chức Eventbrite**
   - Tùy chỉnh danh sách các trường dữ liệu được truyền xuống (event_name, email, ticket_class) theo nhu cầu

2. **Thiết lập Pipedrive**:
   - Truy cập Pipedrive → *Personal preferences → API* → sao chép **API token**
   - Dán token này vào các node Pipedrive trong workflow:
     - "Extract current leads in pipedrive"
     - "Add New Leads to Pipedrive"

3. **Cập nhật lịch chạy**:
   - Mở node "Schedule Daily"
   - Thiết lập khoảng thời gian chạy phù hợp (mặc định là mỗi 10 phút)

4. **Tùy chỉnh ánh xạ trường Pipedrive**:
   - Mở node "Add New Leads to Pipedrive"
   - Cập nhật các ID customProperties để trỏ đến các trường tùy chỉnh trong tài khoản Pipedrive
   - Ánh xạ thêm các trường dữ liệu người tham gia nếu cần (company, ticket type)

#### 3. Kích hoạt ⚡️
- Các sếp nên chạy thử workflow trước bằng cách nhấn "Test or Manually run workflow"
- Theo dõi log thực thi để đảm bảo không có lỗi xảy ra
- Kích hoạt workflow bằng cách bật chế độ "Active" để chạy tự động theo lịch trình

### ✍️ Mẹo & gợi ý nâng cao
- Các sếp có thể kết hợp workflow này với Slack/Telegram để nhận thông báo khi có người tham gia mới
- Thiết lập lưu log các thay đổi để theo dõi lịch sử đồng bộ
- Tạo báo cáo định kỳ về số lượng người tham gia mới để theo dõi hiệu suất sự kiện
- Kết hợp với các công cụ khác như Google Sheets để lưu trữ dữ liệu dự phòng

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quá trình đồng bộ danh sách người tham gia sự kiện từ Eventbrite sang Pipedrive, tiết kiệm thời gian và giảm thiểu rủi ro lỗi. Với chỉ 10 phút thiết lập, các sếp có thể triển khai ngay và tận hưởng lợi ích của tự động hóa. Hãy áp dụng ngay để tối ưu hóa quy trình làm việc của mình!