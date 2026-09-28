---
title: "🔍 Theo dõi giá và tính năng của đối thủ bằng BrowserAct và Google Sheets"
description: "Tự động hóa theo dõi giá và tính năng của đối thủ hàng tuần với BrowserAct và Google Sheets, giúp bạn nhận được báo cáo thay đổi chi tiết và cập nhật cơ sở dữ liệu tự động."
slug: "theo-doi-gia-tinh-nang-doi-thu-browseract-google-sheets"
tags: [n8n, automation, no-code, browseract, google-sheets]
keywords: [n8n workflow, tự động hóa, theo dõi đối thủ, browseract, google sheets]
---

# 🔍 Theo dõi giá và tính năng của đối thủ bằng BrowserAct và Google Sheets

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp có bao giờ phải theo dõi giá và tính năng của đối thủ hàng tuần không? Việc này thường tốn thời gian và công sức, và kết quả có thể không chính xác nếu làm thủ công. Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình theo dõi, từ thu thập dữ liệu đến phân tích và báo cáo, giúp tiết kiệm thời gian và tăng độ chính xác.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa toàn bộ quá trình theo dõi hàng tuần.
- Chính xác: Dữ liệu được thu thập và phân tích tự động, giảm thiểu sai sót.
- Cá nhân hóa: Báo cáo thay đổi chi tiết cho từng đối thủ.
- Hoạt động liên tục: Workflow chạy tự động mà không cần can thiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản BrowserAct với API key và template **AI Competitor Spy: Pricing & Feature Tracker**.
- Tài khoản Google Sheets với bảng dữ liệu có các cột: `Competitor Name`, `URL`, `Last_Scrape_Content`, và `Last_Scrape_Date`.
- Tài khoản Slack để nhận thông báo khi workflow hoàn thành.
- Tài khoản OpenRouter để sử dụng mô hình AI phân tích dữ liệu.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:
- **Weekly Trigger**: Cấu hình lịch chạy hàng tuần.
- **Fetch links & history**: Cấu hình Google Sheets credentials và chỉ định bảng dữ liệu chứa danh sách đối thủ.
- **Extract page content**: Cấu hình BrowserAct credentials và đảm bảo template **AI Competitor Spy: Pricing & Feature Tracker** đã được kích hoạt.
- **Analyze target pages**: Cấu hình OpenRouter credentials và mô hình AI để phân tích dữ liệu.
- **Update Database**: Cấu hình Google Sheets credentials và chỉ định bảng dữ liệu để lưu trữ kết quả.
- **Notify on completion**: Cấu hình Slack credentials để nhận thông báo khi workflow hoàn thành.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack hoặc Telegram để nhận thông báo ngay lập tức khi có thay đổi quan trọng.
- Lưu log hoạt động của workflow để theo dõi lịch sử thay đổi.
- Gửi báo cáo định kỳ qua email để các thành viên trong nhóm có thể theo dõi tiến độ.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quá trình theo dõi giá và tính năng của đối thủ, từ thu thập dữ liệu đến phân tích và báo cáo. Với việc chạy tự động hàng tuần, các sếp có thể tập trung vào các nhiệm vụ quan trọng khác trong công việc. Hãy áp dụng ngay để tiết kiệm thời gian và tăng độ chính xác trong việc theo dõi đối thủ.