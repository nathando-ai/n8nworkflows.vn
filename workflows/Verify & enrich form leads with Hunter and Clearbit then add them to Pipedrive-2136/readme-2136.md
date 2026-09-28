---
title: "🚀 Tự động hóa thu thập & xử lý leads từ form với Hunter, Clearbit và Pipedrive"
description: "Hướng dẫn tự động hóa quy trình xử lý leads từ form với Hunter.io (kiểm tra email), Clearbit (enrich thông tin) và Pipedrive (lưu trữ). Tiết kiệm 80% thời gian thủ công."
slug: "tu-dong-hoa-thu-thap-leads-hunter-clearbit-pipedrive"
tags: [n8n, automation, no-code, sales, marketing]
keywords: [n8n workflow, tự động hóa leads, Hunter.io, Clearbit, Pipedrive]
---

# 🚀 Tự động hóa thu thập & xử lý leads từ form với Hunter, Clearbit và Pipedrive

[Các sếp] có biết rằng mỗi ngày mất tới 2-3 tiếng để xử lý leads từ form? Từ việc kiểm tra email hợp lệ, tìm thông tin công ty, đến lưu vào CRM - quá nhiều công việc thủ công. Workflow này sẽ giúp các sếp tự động hóa hoàn toàn quy trình này với 3 công cụ mạnh mẽ:

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian**: Tự động kiểm tra email hợp lệ với Hunter.io
- **Thông tin đầy đủ**: Enrich thông tin leads với Clearbit
- **Lưu trữ tự động**: Tạo lead trong Pipedrive ngay lập tức
- **Hoạt động liên tục**: Không cần can thiệp thủ công
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Hunter.io (API Key)
- Tài khoản Clearbit (API Key)
- Tài khoản Pipedrive (API Key)
- Bất kỳ form nào (Typeform, Google Forms, Survey Monkey...)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/2136](https://n8n.io/workflows/2136)
2. Click "Import" và chọn "Import from URL"
3. Dán URL trên vào ô nhập liệu
4. Click "OK" để hoàn tất import

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node n8n Form Trigger**:
   - Thay đổi `path` trong keyParameters thành một chuỗi ngẫu nhiên duy nhất (ví dụ: `your-unique-path-123`)

2. **Node Verify email with Hunter**:
   - Thêm credentials Hunter.io (tạo mới trong n8n nếu chưa có)
   - Đảm bảo API Key Hunter.io còn hạn sử dụng

3. **Node Clearbit**:
   - Thêm credentials Clearbit (tạo mới trong n8n nếu chưa có)
   - Đảm bảo API Key Clearbit còn hạn sử dụng

4. **Các node Pipedrive**:
   - Thêm credentials Pipedrive (tạo mới trong n8n nếu chưa có)
   - Đảm bảo API Key Pipedrive còn hạn sử dụng
   - Đối với node "Create Person":
     - Thiết lập `owner_id` là ID của người dùng Pipedrive sẽ quản lý lead này
     - Thiết lập `org_id` để liên kết lead với công ty (nếu có)

#### 3. Kích hoạt ⚡️
1. Click "Test Workflow" để kiểm tra kết nối và dữ liệu mẫu
2. Sau khi test thành công, click "Activate" để kích hoạt workflow
3. Sử dụng URL được tạo ra từ node Form Trigger để thu thập leads

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Slack/Telegram**: Thêm node gửi thông báo khi có lead mới
2. **Lưu log hoạt động**: Thêm node lưu log vào Google Sheets hoặc Notion
3. **Xử lý lead trùng lặp**: Thêm node kiểm tra lead trùng lặp trước khi tạo mới
4. **Tự động gửi email cảm ơn**: Kết nối với node Mailchimp để gửi email tự động

### 📌 Kết luận
Workflow này sẽ giúp các sếp tự động hóa hoàn toàn quy trình xử lý leads từ form, từ kiểm tra email đến lưu trữ trong CRM. Với thời gian tiết kiệm được, các sếp có thể tập trung vào những công việc có giá trị hơn. Hãy thử ngay và trải nghiệm sự khác biệt!