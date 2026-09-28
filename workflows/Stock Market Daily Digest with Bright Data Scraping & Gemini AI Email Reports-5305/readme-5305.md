---
title: "📈 Tự động hóa báo cáo thị trường chứng khoán hàng ngày với Bright Data và AI Gemini"
description: "Hướng dẫn tự động hóa báo cáo thị trường chứng khoán hàng ngày bằng n8n, Bright Data và Google Gemini. Tiết kiệm thời gian, nhận thông tin chính xác và cá nhân hóa."
slug: "tu-dong-hoa-bao-cao-thi-truong-chung-khoan-hang-ngay"
tags: [n8n, automation, no-code, Bright Data, Google Gemini]
keywords: [n8n workflow, tự động hóa, báo cáo thị trường chứng khoán, Bright Data, Google Gemini]
---

# 📈 Tự động hóa báo cáo thị trường chứng khoán hàng ngày với Bright Data và AI Gemini

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp khi phải theo dõi thị trường chứng khoán thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa toàn bộ quy trình từ thu thập dữ liệu đến gửi báo cáo.
- Thông tin chính xác: Sử dụng Bright Data để thu thập dữ liệu từ Financial Times.
- Cá nhân hóa: Nhận báo cáo được tổng hợp và phân tích bởi AI Gemini.
- Hoạt động liên tục: Workflow chạy tự động hàng ngày theo lịch trình.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Workspace (cho Google Sheets và Gmail).
- API Key từ Google Gemini.
- Tài khoản Bright Data (để sử dụng scraper).
- Danh sách mã chứng khoán cần theo dõi.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/5305).
2. Click vào nút "Import" và chọn "Import from URL".
3. Dán link workflow vào ô nhập liệu và nhấn "Import".

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "SAMPLE DATA"**:
   - Thay đổi danh sách mã chứng khoán trong node "set keyword" để theo dõi các mã chứng khoán mong muốn.

2. **Node "Financial times scraper"**:
   - Đảm bảo tài khoản Bright Data đã được cấu hình đúng trong credentials.
   - Thiết lập node để chạy một lần (one-time run).

3. **Node "Google Sheets"**:
   - Cấu hình credentials "googleSheetsOAuth2Api".
   - Chỉnh sửa tên sheet và phạm vi dữ liệu cần lưu.

4. **Node "Google Gemini Chat Model"**:
   - Cấu hình credentials "googlePalmApi".
   - Đảm bảo API key có quyền truy cập đầy đủ.

5. **Node "Gmail1"**:
   - Cấu hình credentials "gmailOAuth2".
   - Thiết lập địa chỉ email người nhận báo cáo.

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng.
2. Bật Active workflow và thiết lập lịch chạy hàng ngày thông qua node "Schedule Trigger".

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo tức thời.
- Lưu log hoạt động của workflow để theo dõi hiệu suất.
- Gửi báo cáo định kỳ hàng tuần hoặc hàng tháng bằng cách chỉnh sửa node "Schedule Trigger".

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian đáng kể trong việc theo dõi thị trường chứng khoán. Bằng cách tự động hóa toàn bộ quy trình từ thu thập dữ liệu đến gửi báo cáo, các sếp có thể tập trung vào các nhiệm vụ quan trọng hơn. Hãy áp dụng ngay để nâng cao hiệu suất làm việc!