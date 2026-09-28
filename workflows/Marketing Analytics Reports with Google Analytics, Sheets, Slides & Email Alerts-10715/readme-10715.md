---
title: "🚀 Tự động hóa Báo cáo Marketing Analytics với Google Analytics, Sheets, Slides & Email"
description: "Hướng dẫn xây dựng workflow n8n tự động tổng hợp dữ liệu từ Google Analytics, Ad Platform, CRM, tính toán KPI (MAU, LTV, CAC), tạo Google Slides và gửi báo cáo qua Gmail."
slug: "tu-dong-hoa-bao-cao-marketing-analytics-n8n"
tags: [n8n, automation, google-analytics, google-sheets, google-slides, marketing-reports]
keywords: [n8n workflow, tự động hóa báo cáo marketing, google analytics n8n, tính toán kpi tự động, google slides automation]
---

# 🚀 Tự động hóa Báo cáo Marketing Analytics với Google Analytics, Sheets, Slides & Email

Các sếp có đang cảm thấy mệt mỏi mỗi khi đầu tuần hay cuối tháng lại phải "hì hục" đăng nhập vào hàng loạt công cụ (Google Analytics, Ads, CRM), copy-paste dữ liệu thủ công vào Google Sheets, rồi lại lọ mọ thiết kế slide báo cáo và soạn email gửi sếp lớn? Công việc lặp đi lặp lại này không chỉ ngốn hàng giờ đồng hồ quý giá mà còn cực kỳ dễ xảy ra sai sót số liệu.

Đừng lo, bài viết này sẽ hướng dẫn các sếp triển khai một **workflow n8n tự động hóa 100%** giúp giải quyết toàn bộ quy trình từ thu thập dữ liệu, tính toán KPI nâng cao, lưu trữ lịch sử, tạo slide báo cáo chuyên nghiệp cho đến việc gửi email thông báo và cảnh báo lỗi qua Slack.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không lo gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Tự động gom dữ liệu, tính toán và xuất báo cáo định kỳ hàng tuần/hàng tháng mà không cần đụng tay.
- **Số liệu chính xác, nhất quán:** Tránh hoàn toàn các sai sót do nhập liệu thủ công (human error).
- **Cá nhân hóa báo cáo:** Tự động tạo Google Slides với số liệu mới nhất và gửi trực tiếp qua Gmail cho các stakeholders.
- **Giám sát thông minh:** Hệ thống tự động kiểm tra lỗi và bắn cảnh báo ngay lập tức qua Slack nếu có sự cố xảy ra trong quá trình lấy dữ liệu.
:::

### 📦 Các Nodes sử dụng trong Workflow
Workflow này bao gồm 11 nodes phối hợp nhịp nhàng với nhau:
1. **Weekly/Monthly Schedule** (`scheduleTrigger`): Lên lịch chạy tự động theo tuần hoặc tháng.
2. **Workflow Configuration** (`set`): Lưu trữ các biến cấu hình chung (Property ID, API URLs, Template ID...).
3. **Get Google Analytics Data** (`googleAnalytics`): Lấy dữ liệu người dùng, phiên truy cập, tỷ lệ chuyển đổi.
4. **Get Ad Platform Data** (`httpRequest`): Lấy chi phí quảng cáo (Ad Spend) từ các nền tảng quảng cáo.
5. **Get CRM Data** (`httpRequest`): Lấy dữ liệu khách hàng mới và doanh thu từ CRM.
6. **Calculate KPIs (MAU, LTV, CAC)** (`code`): Xử lý dữ liệu thô bằng JavaScript để tính toán MAU, CAC, LTV, tỷ lệ LTV:CAC.
7. **Write Data to Google Sheets** (`googleSheets`): Lưu trữ dữ liệu lịch sử KPI phục vụ phân tích xu hướng.
8. **Create Google Slides Report** (`googleSlides`): Tạo bản báo cáo trực quan dưới dạng Google Slides.
9. **Check for Errors** (`if`): Kiểm tra trạng thái thực thi của các bước trước đó.
10. **Send Report Email** (`gmail`): Gửi email tóm tắt kèm link Google Slides đến danh sách nhận báo cáo.
11. **Send Error Notification** (`slack`): Gửi cảnh báo về kênh Slack nếu có lỗi phát sinh.

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ TRƯỚC KHI BẮT ĐẦU]
- Tài khoản n8n (Self-hosted hoặc Cloud).
- Tài khoản và API/Credentials cho: **Google Analytics, Google Sheets, Google Slides, Gmail, Slack**.
- API Access cho nền tảng quảng cáo (Facebook/Google Ads) và hệ thống CRM của doanh nghiệp.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow (hoặc copy toàn bộ JSON từ nguồn cấp).
- Trong giao diện n8n Editor, nhấn vào menu **Add workflow** -> Chọn **Import from File** hoặc dán trực tiếp JSON.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các điểm sau:
- **Node `Workflow Configuration` (`set`):** Đây là nơi quản lý tham số cốt lõi. Hãy thay thế các giá trị mẫu bằng thông tin thực tế của doanh nghiệp:
  - `gaPropertyId`: ID thuộc tính Google Analytics của bạn.
  - `adPlatformApiUrl`: Endpoint API của nền tảng chạy Ads.
  - `crmApiUrl`: Endpoint API của CRM.
  - `reportSpreadsheetId`: ID của Google Sheet lưu trữ lịch sử dữ liệu.
  - `slidesTemplateId`: ID của Google Slides Template làm mẫu báo cáo.
  - `reportRecipients`: Danh sách email nhận báo cáo (cách nhau bởi dấu phẩy).
  - `slackChannel`: ID kênh Slack nhận thông báo lỗi.
- **Thiết lập Credentials:** Kết nối tài khoản Google Analytics, Google Sheets, Google Slides, Gmail (`gmailOAuth2`) và Slack (`slackOAuth2Api`) tương ứng với các node trong hệ thống.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (**Test Workflow**) để kiểm tra toàn bộ luồng dữ liệu từ đầu đến cuối.
- Kiểm tra lại Google Sheet, Google Slides và Email xem kết quả trả về đã chính xác chưa.
- Gạt công tắc sang **Active** để hệ thống tự động chạy theo lịch trình đã định.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Ngoài Slack, có thể kết hợp thêm node Telegram hoặc Zalo OA để gửi bản tóm tắt KPI nhanh cho ban giám đốc.
- **Tùy chỉnh chu kỳ:** Dễ dàng thay đổi lịch chạy từ hàng tháng sang hàng tuần hoặc hàng ngày ngay tại node `Weekly/Monthly Schedule`.
- **Nâng cấp biểu đồ Slides:** Tận dụng Javascript trong node `Calculate KPIs` kết hợp với Google Slides API để tự động vẽ biểu đồ tăng trưởng trực quan hơn.

### 📌 Kết luận
Việc tự động hóa báo cáo marketing không chỉ giúp các sếp giải phóng thời gian khỏi những công việc thủ công nhàm chán mà còn mang lại sự chuyên nghiệp, minh bạch và kịp thời trong việc ra quyết định dựa trên dữ liệu. Hãy import workflow này ngay hôm nay và tối ưu hóa quy trình vận hành marketing của doanh nghiệp!