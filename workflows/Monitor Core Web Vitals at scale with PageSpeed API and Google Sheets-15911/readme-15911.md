---
title: "🚀 Tự động giám sát Core Web Vitals hàng loạt với PageSpeed API và Google Sheets"
description: "Hướng dẫn xây dựng workflow n8n tự động quét Core Web Vitals và điểm số Lighthouse cho toàn bộ website thông qua XML Sitemap hoặc file CSV, sau đó lưu kết quả vào Google Sheets."
slug: "tu-dong-giam-sat-core-web-vitals-voi-pagespeed-api-va-google-sheets"
tags: [n8n, automation, technical-seo, google-sheets, pagespeed-api, core-web-vitals]
keywords: [n8n workflow, giám sát core web vitals, pagespeed api automation, seo technical automation, google sheets lighthouse report]
---

# 🚀 Tự động giám sát Core Web Vitals hàng loạt với PageSpeed API và Google Sheets

Các sếp làm SEO, quản lý website hay e-commerce chắc chắn đã từng đau đầu khi phải kiểm tra tốc độ tải trang (Core Web Vitals và điểm số Lighthouse) thủ công cho từng URL trên website. Việc này không chỉ tốn hàng giờ đồng hồ mà còn rất khó để theo dõi sự biến động hiệu suất định kỳ. 

Workflow n8n tuyệt vời này sẽ giải quyết triệt để nỗi đau đó bằng cách tự động hóa 100%: lấy danh sách URL từ XML Sitemap hoặc file CSV, gọi Google PageSpeed Insights API, phân tích toàn bộ chỉ số hiệu suất, và lưu trực tiếp kết quả chi tiết vào Google Sheets kèm theo email tổng kết!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Quét hàng trăm, hàng ngàn URL chỉ với một cú click hoặc theo lịch định kỳ (Schedule).
- **Báo cáo chuẩn SEO:** Xuất kết quả trực quan vào Google Sheets với đầy đủ các chỉ số Lab (Lighthouse) và Field data (CrUX) như LCP, INP, CLS, FCP, TTFB... kèm kết quả Pass/Fail.
- **Linh hoạt đầu vào:** Hỗ trợ lấy URL tự động từ XML Sitemap hoặc upload file CSV thủ công khi cần test nhanh.
- **Thông báo thông minh:** Gửi email tổng kết kèm link Google Sheets ngay khi hoàn tất quá trình audit.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Google PageSpeed API Key:** Lấy miễn phí từ Google Cloud Console.
- **Google Sheets Credentials:** Tài khoản Google kết nối qua OAuth2 để n8n tự động tạo và ghi dữ liệu.
- **Gmail Credentials:** Tài khoản Gmail để gửi email thông báo kết quả.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này và import trực tiếp vào n8n Editor của các sếp, hoặc sử dụng tính năng copy/paste JSON.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình các node quan trọng sau:
- **Node `Config`:** 
  - Điền PageSpeed API key vào trường `api_key`.
  - Nhập đường dẫn sitemap của website vào trường `xml_sitemap_url` (nếu chạy tự động qua sitemap).
- **Node `Pick default spreadsheet to save the report` & các node Google Sheets:** Chọn tài khoản Google Sheets OAuth2 và cấu hình nơi lưu trữ báo cáo (workflow sẽ tự động tạo sheet, tiêu đề cột và điền dữ liệu).
- **Node `Send audit summary email`:** Điền địa chỉ email nhận báo cáo của các sếp vào phần cài đặt gửi thư qua Gmail.
- **Node `Wait between each batch` (Tùy chọn):** Điều chỉnh thời gian chờ giữa các URL (mặc định 1 giây) để tránh làm quá tải server website của bạn khi quét số lượng lớn.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công bằng cách click vào **`When clicking ‘Execute workflow’`** hoặc upload file qua **`Upload CSV`** để kiểm tra dữ liệu trả về.
- Bật công tắc **Active** để workflow tự động chạy theo lịch trình đã cài đặt ở node **`Schedule Audit`**.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Slack/Telegram:** Thêm node gửi tin nhắn thông báo vào nhóm chat của team kỹ thuật/SEO ngay khi audit hoàn tất.
- **Cảnh báo lỗi:** Thiết lập điều kiện lọc nếu có quá nhiều URL bị lỗi `Pass/Fail` ở các chỉ số quan trọng như LCP hay INP để nhận cảnh báo sớm.
- **Lưu trữ lịch sử:** Định kỳ so sánh dữ liệu giữa các lần chạy để theo dõi xu hướng tối ưu hóa tốc độ website theo thời gian.

### 📌 Kết luận
Workflow này là một "vũ khí tối thượng" giúp các chuyên gia SEO và đội ngũ vận hành website tiết kiệm hàng chục giờ làm việc thủ công mỗi tháng. Hãy "lên đồ" ngay cho hệ thống n8n của các sếp để tự động hóa toàn bộ quy trình kiểm toán hiệu suất website!