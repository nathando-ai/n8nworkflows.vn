---
title: "🔍 Xác minh nhà cung cấp dịch vụ qua Telegram với BrowserAct và Google Gemini"
description: "Tự động hóa kiểm tra uy tín nhà cung cấp dịch vụ bằng cách so sánh dữ liệu từ Google với cơ sở dữ liệu công ty chính thức. Nhận báo cáo xác thực qua Telegram chỉ trong vài giây."
slug: "xac-minh-nha-cung-cap-dich-vu-qua-telegram"
tags: [n8n, automation, no-code, telegram, google-gemini, browseract]
keywords: [n8n workflow, tự động hóa, xác minh nhà cung cấp, kiểm tra uy tín, google gemini, browseract]
---

# 🔍 Xác minh nhà cung cấp dịch vụ qua Telegram với BrowserAct và Google Gemini

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Xác minh uy tín nhà cung cấp chỉ trong vài giây thay vì vài giờ làm thủ công.
- Chính xác: So sánh dữ liệu từ Google với cơ sở dữ liệu công ty chính thức.
- Cá nhân hóa: Nhận báo cáo xác thực chi tiết cho từng nhà cung cấp.
- Hoạt động liên tục: Kiểm tra bất kỳ lúc nào trong ngày, không phụ thuộc vào giờ làm việc.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Telegram và API key.
- Tài khoản BrowserAct với template **Vendor Vetting and verification bot**.
- API key Google Gemini (PaLM).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/12432](https://n8n.io/workflows/12432)
2. Nhấn nút "Import" để tải workflow về máy.
3. Trong n8n Editor, nhấn vào "Import from File" và chọn file JSON đã tải về.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "User Sends Message to Bot"**:
   - Cấu hình credentials Telegram.
   - Đảm bảo bot Telegram của bạn đã được kích hoạt và có thể nhận tin nhắn.

2. **Node "Get Vendor Data & Stats"**:
   - Cấu hình credentials BrowserAct.
   - Đảm bảo bạn đã lưu template **Vendor Vetting and verification bot** trong tài khoản BrowserAct.

3. **Node "Validation bot" và "Verify Data"**:
   - Cấu hình credentials Google Gemini (PaLM).
   - Đảm bảo bạn đã kích hoạt API Google Gemini và có API key.

4. **Node "Process Initialization Alert"**:
   - Cấu hình thông báo khởi động quá trình xác minh.
   - Đảm bảo bot Telegram của bạn đã được cấu hình để gửi tin nhắn.

5. **Node "Answer the User"**:
   - Cấu hình thông báo kết quả xác minh.
   - Đảm bảo bot Telegram của bạn đã được cấu hình để gửi tin nhắn.

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu:
   - Gửi tin nhắn đến bot Telegram với nội dung: "Can I trust Mr Rooter Plumbing in Michigan?"
2. Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Teams để nhận thông báo xác minh.
- Lưu log các lần xác minh để theo dõi lịch sử.
- Gửi báo cáo xác minh định kỳ cho khách hàng.
- Tích hợp với hệ thống CRM để lưu trữ thông tin nhà cung cấp.

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian và công sức trong việc xác minh uy tín nhà cung cấp dịch vụ. Với sự kết hợp của BrowserAct và Google Gemini, các sếp có thể nhận được báo cáo xác thực chi tiết chỉ trong vài giây. Hãy áp dụng ngay để nâng cao hiệu quả kinh doanh của mình!