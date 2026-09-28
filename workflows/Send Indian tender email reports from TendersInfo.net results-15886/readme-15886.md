---
title: "🚀 Tự động hóa tìm kiếm và báo cáo thầu Ấn Độ từ TendersInfo.net với n8n"
description: "Hướng dẫn cấu hình workflow n8n giúp tự động cào dữ liệu thầu từ TendersInfo.net, lọc gói thầu GEM/MSE và tạo báo cáo HTML chuyên nghiệp."
slug: "tu-dong-hoa-tim-kiem-va-bao-cao-thau-an-do-n8n"
tags: [n8n, automation, no-code, web-scraping, api-integration, market-research]
keywords: [n8n workflow, tendersinfo, tu dong hoa thau, api integration, n8n viet nam]
keywords: [n8n workflow, tự động hóa, tendersinfo, báo cáo thầu, api integration]
---

# 🚀 Tự động hóa tìm kiếm và báo cáo thầu Ấn Độ từ TendersInfo.net

Việc theo dõi các cơ hội đấu thầu tại thị trường Ấn Độ (đặc biệt là trên nền tảng TendersInfo.net và cổng GEM) theo cách thủ công thường ngốn rất nhiều thời gian của các doanh nghiệp. Các nhà quản lý phải liên tục tra cứu từ khóa, lọc các tiêu chí khắt khe về MSME hay GEM, sau đó tổng hợp thủ công thành các báo cáo để gửi cho đội ngũ kinh doanh. Điều này không chỉ chậm trễ mà còn dễ bỏ lỡ các gói thầu quan trọng.

Giải pháp ở đây chính là **workflow n8n tự động hóa 100%** do chuyên gia Rahul Joshi thiết kế. Quy trình này sẽ giúp các sếp nhận các báo cáo thầu trực quan dưới dạng bảng HTML chuyên nghiệp ngay lập tức thông qua Webhook.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không cần tra cứu thủ công hàng ngày trên TendersInfo.net.
- **Lọc chuẩn xác:** Tự động chọn lọc các gói thầu GEM và MSE (Micro & Small Enterprises) đủ điều kiện.
- **Báo cáo chuyên nghiệp:** Dữ liệu được tổng hợp thành bảng HTML trực quan, nhóm theo công ty, sẵn sàng gửi email hoặc hiển thị ngay.
- **Hoạt động 24/7:** Kích hoạt linh hoạt qua Webhook bất cứ lúc nào cần dữ liệu.
:::

### Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một hệ thống n8n (Self-hosted hoặc Cloud).
- Tài khoản trên **TendersInfo.net** để lấy thông tin xác thực (`ANTI_FORGERY_TOKEN` và `SESSION_ID`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ n8n.io (ID: 15886) hoặc copy mã JSON và dán trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 7 nodes chính, các sếp cần chú ý cấu hình kỹ các điểm sau để hệ thống chạy mượt mà:

- **Webhook Trigger1**: Node này nhận các yêu cầu POST chứa từ khóa tìm kiếm (`keywords`), tùy chọn MSME (`msme`), và email người nhận (`email`). Hãy copy đường dẫn Production Webhook URL để tích hợp với hệ thống bên ngoài.
- **Fetch Tender Data from API1 (`httpRequest`)**: Đây là node cốt lõi gọi dữ liệu từ TendersInfo.net. Các sếp **bắt buộc phải thay thế** phần `Cookie` header trong node này bằng thông tin `ANTI_FORGERY_TOKEN` và `SESSION_ID` hợp lệ lấy từ tài khoản TendersInfo.net của mình. *Lưu ý bảo mật thông tin phiên làm việc này, tuyệt đối không chia sẻ công khai.*
- **Parse Tender Response1 (`code`)**: Node xử lý code JavaScript giúp bóc tách dữ liệu JSON thô từ API thành các bản ghi riêng biệt, có cấu trúc rõ ràng.
- **Filter GEM Tenders Only1 (`filter`)**: Node lọc dữ liệu giúp giữ lại các gói thầu đủ điều kiện GEM và MSE.
- **Select Email Fields1 (`set`)** & **Build HTML Table (`code`)**: Các node định dạng dữ liệu, ánh xạ các trường thông tin (đường dẫn, ngày tháng, chi tiết công ty) và biên tập thành bảng HTML hoàn chỉnh.
- **Respond to Webhook1 (`respondToWebhook`)**: Trả kết quả báo cáo HTML về cho yêu cầu ban đầu.

#### 3. Kích hoạt ⚡️
- **Test run:** Gửi một request POST mẫu tới Webhook với định dạng JSON:
  ```json
  {
    "keywords": "software",
    "msme": "eligible",
    "email": "user@example.com"
  }
  ```
- Kiểm tra kết quả trả về để đảm bảo API hoạt động ổn định.
- Bật **Active workflow** để đưa hệ thống vào vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Email/Slack:** Thay vì chỉ trả về qua Webhook, các sếp có thể nối thêm node **Gmail** hoặc **Slack** ngay sau bước tạo bảng HTML để gửi báo cáo trực tiếp đến hòm thư hoặc kênh thông báo của team.
- **Lưu trữ dữ liệu:** Thêm node **Google Sheets** hoặc **Airtable** để lưu lại lịch sử các gói thầu đã tìm kiếm, phục vụ cho việc phân tích xu hướng thị trường sau này.
- **Lịch chạy tự động (Cron):** Thay thế Webhook bằng node **Schedule Trigger** để hệ thống tự động quét thầu vào mỗi buổi sáng mà không cần gọi thủ công.

### 📌 Kết luận
Với workflow n8n tự động hóa tìm kiếm thầu từ TendersInfo.net này, các sếp hoàn toàn có thể giải phóng đội ngũ khỏi những tác vụ tra cứu thủ công nặng nhọc. Hãy áp dụng ngay hôm nay để nắm bắt nhanh chóng các cơ hội kinh doanh giá trị tại thị trường Ấn Độ!