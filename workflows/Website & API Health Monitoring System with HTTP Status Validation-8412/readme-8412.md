---
title: "🚀 Hệ thống giám sát website & API với xác thực trạng thái HTTP"
description: "Tự động kiểm tra website/API của bạn 24/7 với xác thực trạng thái HTTP và phân tích sức khỏe JSON. Nhận cảnh báo tức thì khi có vấn đề."
slug: "he-thong-giam-sat-website-api-voi-xac-thuc-trang-thai-http"
tags: [n8n, automation, devops, monitoring, api]
keywords: [n8n workflow, giám sát website, xác thực HTTP, tự động hóa, devops]
---

# 🚀 Hệ thống giám sát website & API với xác thực trạng thái HTTP

[Các sếp đang gặp khó khăn khi phải theo dõi thủ công tình trạng hoạt động của website/API của mình. Với workflow này, các sếp có thể tự động hóa quá trình giám sát 24/7, nhận cảnh báo tức thì khi có vấn đề và đảm bảo uptime của dịch vụ quan trọng.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Giám sát liên tục website/API của bạn 24/7
- Nhận cảnh báo tức thì khi có vấn đề về uptime
- Xác thực chính xác trạng thái HTTP và sức khỏe JSON
- Tự động hóa quá trình giám sát mà không cần can thiệp thủ công
- Đảm bảo uptime của dịch vụ quan trọng cho doanh nghiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n đã cài đặt và cấu hình
- URL của website/API bạn muốn giám sát
- (Tùy chọn) Cấu hình SMTP để gửi email cảnh báo
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấn vào "Import from URL" và nhập URL sau: `https://n8n.io/workflows/8412`
3. Hoặc tải file JSON về và chọn "Import from File"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Trigger (Webhook)** node:
   - Đảm bảo đường dẫn webhook là duy nhất và bảo mật
   - Cấu hình timeout phù hợp với yêu cầu của bạn

2. **Set Defaults** node:
   - Cấu hình các giá trị mặc định cho timeout và expected status code

3. **HTTP (Ping)** node:
   - Cấu hình URL của website/API bạn muốn giám sát
   - Đặt timeout phù hợp (thường từ 5-30 giây)

4. **IF Status < expect** node:
   - Cấu hình điều kiện kiểm tra trạng thái HTTP

5. **Health Check (Auto)** node:
   - Cấu hình các trường JSON cần kiểm tra (status, health, ok)

6. **IF Health passes** node:
   - Cấu hình điều kiện kiểm tra sức khỏe

7. **Respond (JSON)** node:
   - Cấu hình phản hồi JSON cho từng trường hợp thành công/lỗi

#### 3. Kích hoạt ⚡️
1. Test run với dữ liệu mẫu:
   ```json
   {
     "url": "https://your-site.com",
     "timeout": 10,
     "expectedStatus": 200
   }
   ```
2. Kiểm tra kết quả ở tab "Execution" để đảm bảo workflow hoạt động đúng
3. Bật Active workflow để bắt đầu giám sát liên tục

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Slack/Teams**: Thêm node gửi thông báo đến Slack/Teams khi có vấn đề
2. **Lưu log lịch sử**: Thêm node lưu kết quả giám sát vào Google Sheets hoặc cơ sở dữ liệu
3. **Cảnh báo định kỳ**: Thiết lập gửi báo cáo sức khỏe định kỳ qua email
4. **Giám sát nhiều website**: Sao chép workflow và cấu hình cho các website/API khác

### 📌 Kết luận
Hệ thống giám sát website/API này giúp các sếp tự động hóa quá trình giám sát quan trọng, giảm thiểu thời gian downtime và đảm bảo uptime của dịch vụ quan trọng. Hãy áp dụng ngay để nâng cao hiệu suất vận hành của doanh nghiệp!