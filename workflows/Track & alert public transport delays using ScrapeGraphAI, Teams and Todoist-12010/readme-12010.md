---
title: "🚀 Theo dõi & cảnh báo chậm trễ giao thông công cộng bằng ScrapeGraphAI, Teams và Todoist"
description: "Hướng dẫn tự động hóa theo dõi lịch trình giao thông công cộng, cảnh báo chậm trễ qua Teams và lưu lịch trình vào Todoist - giải pháp tiết kiệm thời gian cho người đi lại thường xuyên"
slug: "theo-doi-lich-trinh-giao-thong-cong-cong"
tags: [n8n, automation, no-code, giao thông công cộng, Todoist, Microsoft Teams]
keywords: [n8n workflow, tự động hóa giao thông, theo dõi lịch trình, cảnh báo chậm trễ]
---

# 🚀 Theo dõi & cảnh báo chậm trễ giao thông công cộng bằng ScrapeGraphAI, Teams và Todoist

[Đoạn mở đầu: Phân tích nỗi đau thực tế của người đi lại thường xuyên khi phải kiểm tra lịch trình giao thông công cộng thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Nhận cảnh báo tức thì khi có chậm trễ giao thông
- Lịch trình giao thông được tự động cập nhật trong Todoist
- Tiết kiệm thời gian kiểm tra lịch trình thủ công
- Nhận thông báo qua Microsoft Teams khi có sự cố
- Lịch trình cá nhân hóa cho từng người dùng
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản ScrapeGraphAI (để trích xuất dữ liệu từ trang web giao thông)
- Tài khoản Microsoft Teams (để nhận cảnh báo)
- Tài khoản Todoist (để lưu lịch trình)
- API keys cho các dịch vụ trên
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/12010](https://n8n.io/workflows/12010)
2. Nhấn nút "Import" để thêm workflow vào n8n của bạn
3. Hoặc copy JSON từ trang web và paste vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Webhook – Incoming Request** (Node đầu tiên):
   - Đảm bảo đường dẫn "public-transport-tracker" là duy nhất trong hệ thống của bạn
   - Giữ phương thức HTTP là POST

2. **Scrape Schedules & Delays**:
   - Cấu hình credentials cho ScrapeGraphAI
   - Điền thông tin API key và endpoint cần thiết

3. **Send Teams Alert**:
   - Thay thế `{{YOUR_TEAM_ID}}` và `{{YOUR_CHANNEL_ID}}` bằng ID thực tế của bạn
   - Kiểm tra quyền truy cập của n8n vào Teams

4. **Create Todoist Task**:
   - Cấu hình credentials cho Todoist
   - Đảm bảo n8n có quyền tạo task trong Todoist của bạn

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu:
   ```json
   {
     "line": "A",
     "stop": "Central Station"
   }
   ```
2. Kiểm tra:
   - Có nhận được cảnh báo Teams khi có chậm trễ
   - Lịch trình được tạo trong Todoist
3. Bật Active workflow

### ✍️ Mẹo & gợi ý nâng cao
1. Kết hợp với Slack để nhận thông báo bổ sung
2. Thêm node lưu log để theo dõi lịch sử chậm trễ
3. Tạo báo cáo định kỳ về xu hướng chậm trễ
4. Kết nối với Google Calendar để đồng bộ lịch trình

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian đáng kể trong việc theo dõi lịch trình giao thông công cộng. Bằng cách tự động hóa quá trình này, các sếp có thể tập trung vào công việc quan trọng hơn và nhận thông báo tức thì khi có sự cố giao thông. Hãy thử ngay và trải nghiệm sự tiện lợi mà công nghệ tự động hóa mang lại!