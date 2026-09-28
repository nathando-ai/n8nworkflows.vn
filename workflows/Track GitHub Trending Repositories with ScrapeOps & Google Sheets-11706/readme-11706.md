---
title: "🚀 Theo dõi Top Repositories GitHub Hàng ngày với ScrapeOps & Google Sheets"
description: "Hướng dẫn tự động hóa theo dõi các repositories nổi bật trên GitHub hàng ngày, hàng tuần và hàng tháng với n8n và ScrapeOps. Lưu kết quả vào Google Sheets một cách tự động và hiệu quả."
slug: "theo-doi-top-repositories-github-hang-ngay"
tags: [n8n, automation, no-code, github, scrapeops, google-sheets]
keywords: [n8n workflow, tự động hóa, github trending, scrapeops, google sheets]
---

# 🚀 Theo dõi Top Repositories GitHub Hàng ngày với ScrapeOps & Google Sheets

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp khi phải theo dõi thủ công các repositories nổi bật trên GitHub hàng ngày. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động cập nhật danh sách repositories nổi bật hàng ngày, hàng tuần và hàng tháng.
- **Chính xác**: Sử dụng ScrapeOps để đảm bảo dữ liệu được lấy một cách đáng tin cậy.
- **Cá nhân hóa**: Lọc theo ngôn ngữ lập trình và thời gian theo dõi (daily/weekly/monthly).
- **Hoạt động liên tục**: Workflow chạy tự động theo lịch trình đã cài đặt.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản ScrapeOps và API key (đăng ký tại [ScrapeOps](https://scrapeops.io/app/register/n8n)).
- Tài khoản Google và Google Sheets với các tab và cột tương ứng (sao chép từ [Google Sheet mẫu](https://docs.google.com/spreadsheets/d/1GhCbbPilZXMVDox0hQ0Ncqf5-g3AdFFy55Ld30gPD-E/edit?usp=sharing)).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/11706](https://n8n.io/workflows/11706) để tải file JSON của workflow.
2. Trong n8n Editor, nhấn vào **Import from File** và chọn file JSON đã tải về.
3. Hoặc, copy toàn bộ JSON từ trang web và paste vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Cron (daily/weekly)**: Cấu hình lịch trình chạy workflow (hàng ngày, hàng tuần).
2. **Build URLs**: Không cần cấu hình, node này tự động tạo URL dựa trên các tham số đầu vào.
3. **Split URLs (loop)**: Không cần cấu hình, node này chia nhỏ danh sách URL để xử lý tuần tự.
4. **ScrapeOps: Fetch HTML**:
   - Chọn credentials **scrapeOpsApi**.
   - Đảm bảo API key của ScrapeOps đã được thêm vào n8n.
5. **Polite Delay**: Thiết lập thời gian chờ giữa các lần scrape để tránh bị chặn bởi GitHub.
6. **Extract Trending Repos**: Không cần cấu hình, node này tự động trích xuất dữ liệu từ HTML.
7. **Normalize + Enrich-from-page**: Không cần cấu hình, node này chuẩn hóa và bổ sung dữ liệu.
8. **Write to Google Sheets (raw tab)**:
   - Chọn credentials **googleSheetsOAuth2Api**.
   - Đảm bảo Google Sheets đã được chia sẻ với tài khoản được sử dụng.
   - Thiết lập **operation** thành **Append or Update Row** và **dedupe_key** để tránh trùng lặp.
9. **Write to Google Sheets (weekly tab)**:
   - Chọn credentials **googleSheetsOAuth2Api**.
   - Thiết lập **operation** thành **Append**.
10. **Set Inputs**:
    - Thiết lập tham số `since` (daily/weekly/monthly).
    - Thêm các ngôn ngữ lập trình vào `languages_csv` (ví dụ: `any,python,go,rust`).
11. **Read raw (for weekly)**: Không cần cấu hình, node này đọc dữ liệu từ tab raw.
12. **Generate Weekly**: Không cần cấu hình, node này tạo báo cáo hàng tuần.

#### 3. Kích hoạt ⚡️
1. **Test run dữ liệu mẫu**: Chạy workflow với dữ liệu mẫu để kiểm tra tính năng.
2. **Bật Active workflow**: Sau khi kiểm tra thành công, bật workflow để chạy tự động theo lịch trình.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Telegram**: Thêm node gửi thông báo qua Slack hoặc Telegram khi có repositories mới nổi bật.
- **Lưu log**: Thêm node lưu log hoạt động của workflow để theo dõi và gỡ lỗi.
- **Gửi báo cáo định kỳ**: Tạo báo cáo tổng hợp và gửi qua email hoặc lưu vào Google Drive.
- **Mở rộng ngôn ngữ lập trình**: Thêm các ngôn ngữ lập trình khác vào danh sách `languages_csv` để theo dõi.

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian và công sức trong việc theo dõi các repositories nổi bật trên GitHub. Với việc tự động hóa toàn bộ quá trình, các sếp có thể tập trung vào các nhiệm vụ quan trọng hơn. Hãy áp dụng ngay để nâng cao hiệu suất làm việc!