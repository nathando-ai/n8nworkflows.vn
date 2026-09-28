---
title: "🚀 Tự động giám sát hiệu suất website với PageSpeed Insights & Google Sheets trên n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động kiểm tra tốc độ website qua PageSpeed Insights API, lưu lịch sử vào Google Sheets và gửi cảnh báo khi điểm số sụt giảm."
slug: "tu-dong-giam-sat-hieu-suat-website-pagespeed-insights-google-sheets"
tags: [n8n, automation, no-code, google-sheets, seo, devops]
keywords: [n8n workflow, pagespeed insights, giam sat website, google sheets automation, kiem tra toc do website]
---

# 🚀 Tự động giám sát hiệu suất website với PageSpeed Insights & Google Sheets

Các agency marketing, đội ngũ SEO hay quản trị viên hệ thống thường xuyên đối mặt với áp lực phải theo dõi sát sao tốc độ tải trang của hàng loạt website khách hàng. Việc kiểm tra thủ công từng trang trên Google PageSpeed Insights mỗi ngày vừa tốn thời gian, vừa dễ bỏ lỡ các biến động về điểm số hay lỗi Core Web Vitals (LCP, FID, CLS).

Workflow n8n này chính là giải pháp tự động hóa 100% không cần code (No-Code), giúp các sếp tự động hóa toàn bộ quy trình: quét hiệu suất định kỳ theo lịch trình, lưu trữ lịch sử dữ liệu vào Google Sheets, đồng thời gửi email cảnh báo ngay lập tức nếu điểm số rớt xuống dưới mức ngưỡng cho phép.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Theo dõi tự động 24/7:** Hệ thống tự quét danh sách website theo lịch (hàng ngày/hàng tuần) mà không cần can thiệp thủ công.
- **Cảnh báo thông minh:** Tự động gửi email qua **Send a message (Gmail)** ngay khi website sụt giảm hiệu suất dưới ngưỡng cài đặt.
- **Lưu trữ lịch sử trực quan:** Tự động ghi lại toàn bộ chỉ số (LCP, CLS, Điểm hiệu suất...) vào **Save Audit Results (Google Sheets)** để phân tích xu hướng theo thời gian.
- **Hỗ trợ On-Demand:** Tích hợp **Webhook** cho phép kiểm tra nhanh một URL bất cứ lúc nào qua API request.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Google PageSpeed Insights API Key:** Miễn phí từ Google Cloud Console.
- **Google Sheets Credentials:** Tài khoản Google kết nối với n8n để đọc/ghi dữ liệu.
- **Gmail Account / Credentials:** Để gửi thông báo cảnh báo qua email.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ trang chủ n8n (ID: `8328`) và import trực tiếp vào giao diện n8n Editor của các sếp, hoặc sao chép và dán trực tiếp vào canvas.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động mượt mà, các sếp cần cấu hình các node cốt lõi sau:

- **Google Sheets Nodes (`Load Sites from Google Sheet`, `Save Audit Results`, `Update Audit Date`):**
  - Cấu hình kết nối tài khoản Google qua **Google Sheets OAuth2 API**.
  - Chuẩn bị file Google Sheet gồm 2 Sheet chính:
    - Sheet nhập liệu (`sites`): Gồm các cột `URL`, `Site_Name`, `Category`, `Alert_Threshold`, `Last_Processed_Date`, `Device`.
    - Sheet kết quả (`audit_results`): Gồm `Date`, `URL`, `Site_Name`, `Device`, `Performance_Score`, `LCP`, `FID`, `CLS`, `Recommendations`, `Full_Report_URL`.
- **API Request Nodes (`Run PageSpeed Test`, `Run On-Demand Test`):**
  - Đảm bảo đã chèn Google PageSpeed Insights API Key vào phần Header hoặc Query Parameters của HTTP Request để tránh bị giới hạn lượt gọi (Rate Limit).
- **Check Alert Threshold (Node `if`):**
  - Thiết lập điều kiện so sánh giữa điểm số trả về từ PageSpeed với mức `Alert_Threshold` trong Google Sheet. Nếu thấp hơn ngưỡng, workflow sẽ chuyển hướng sang nhánh gửi cảnh báo.
- **Send a message (Node `gmail`):**
  - Kết nối tài khoản Gmail cá nhân hoặc Workspace để gửi email cảnh báo chi tiết kèm theo điểm số và đề xuất tối ưu.
- **Webhook Nodes (`Webhook`, `Return Audit Response`):**
  - Dùng khi cần test nhanh một URL đơn lẻ thông qua phương thức `POST` với định dạng JSON mẫu:
    ```json
    {
      "url": "https://example.com",
      "site_name": "Example Site",
      "alert_threshold": 75
    }
    ```

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (**Execute Workflow**) với dữ liệu mẫu để kiểm tra xem dữ liệu có đẩy về Google Sheet và email có gửi đi thành công hay không.
- Bật công tắc **Active** ở góc trên bên phải để workflow tự động chạy ngầm theo lịch từ **Schedule Trigger**.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Thay vì chỉ dùng Gmail, các sếp có thể kết nối thêm node **Slack** hoặc **Telegram Bot** để nhận cảnh báo ngay lập tức trên điện thoại.
- **Lưu log lỗi:** Thêm các nhánh xử lý lỗi (Error Trigger) để nắm bắt ngay nếu trang web của khách hàng bị sập (Down time) hoặc API trả về lỗi timeout.
- **Báo cáo trực quan:** Kết nối Google Sheet kết quả với **Google Looker Studio (Data Studio)** để vẽ biểu đồ theo dõi xu hướng hiệu suất website cho khách hàng xem trực tuyến.

### 📌 Kết luận
Workflow giám sát hiệu suất website với PageSpeed Insights và Google Sheets này là một "vũ khí" cực kỳ lợi hại cho các SEOer và Digital Agency giúp tiết kiệm hàng giờ kiểm tra thủ công mỗi tuần. Hãy cài đặt ngay lên hệ thống n8n của các sếp để tối ưu hóa quy trình vận hành!