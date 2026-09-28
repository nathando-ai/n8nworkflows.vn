---
title: "🚀 Tự động hóa Báo cáo Thời tiết hàng ngày với OpenWeather API, Google Sheets và Gmail"
description: "Xây dựng hệ thống tự động lấy dữ liệu thời tiết mỗi ngày qua OpenWeather API, lưu trữ vào Google Sheets và gửi email báo cáo HTML đẹp mắt qua Gmail với n8n."
slug: "tu-dong-hoa-bao-cao-thoi-tiet-hang-ngay-n8n"
tags: [n8n, automation, no-code, openweather, google-sheets, gmail]
keywords: [n8n workflow, tu dong hoa thoi tiet, openweather api, google sheets, gmail automation, personal productivity]
---

# 🚀 Tự động hóa Báo cáo Thời tiết hàng ngày với OpenWeather API, Google Sheets và Gmail

Các sếp có bao giờ cảm thấy mất thời gian mỗi sáng khi phải lên các trang web thời tiết để kiểm tra nhiệt độ, độ ẩm hay sức gió trước khi ra ngoài hoặc lập kế hoạch cho công việc? Hay việc quản lý dữ liệu thời tiết lịch sử để phân tích trở nên thủ công và nhàm chán? 

Đừng lo! Workflow n8n này sẽ giải quyết triệt để vấn đề đó. Hệ thống sẽ tự động hóa toàn bộ quy trình: lấy dữ liệu thời tiết mới nhất từ OpenWeather API, lưu trữ có cấu trúc vào Google Sheets, và gửi một bản báo cáo định dạng HTML trực quan qua Gmail vào mỗi buổi sáng mà không cần các sếp phải nhón tay làm gì.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động 100%:** Kích hoạt đúng giờ mỗi ngày (10:00 AM) mà không cần can thiệp thủ công.
- **Lưu trữ lịch sử thông minh:** Tự động ghi nhận các chỉ số khí hậu (nhiệt độ, độ ẩm, áp suất, sức gió...) vào Google Sheets để dễ dàng theo dõi theo thời gian.
- **Báo cáo chuyên nghiệp:** Nhận email tóm tắt thời tiết định dạng HTML đẹp mắt, rõ ràng ngay trong hộp thư Gmail.
- **Tối ưu năng suất cá nhân:** Giúp các sếp nắm bắt nhanh chóng thông tin thời tiết để lên kế hoạch làm việc, di chuyển hiệu quả.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Tài khoản OpenWeather:** Lấy API Key miễn phí từ [OpenWeather](https://openweathermap.org/).
- **Tài khoản Google:** Chuẩn bị sẵn một Google Sheet để lưu dữ liệu và cấp quyền Google Sheets OAuth2.
- **Tài khoản Gmail:** Cấp quyền Gmail OAuth2 trên n8n để gửi email tự động.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần tải file JSON của workflow này hoặc copy trực tiếp mã JSON từ trang chủ n8n và paste vào n8n Editor của mình là xong.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node sau:

- **Trigger Daily at 10 AM (`scheduleTrigger`):** 
  - Node này mặc định chạy lúc 10:00 AM mỗi ngày. Các sếp có thể thay đổi múi giờ (Timezone) hoặc khung giờ tùy ý cho phù hợp với nhu cầu cá nhân.
- **Fetch Weather from OpenWeather (`httpRequest`):** 
  - Cần cấu hình kết nối `httpQueryAuth` với OpenWeather API Key.
  - Điền tọa độ (Latitude, Longitude) của khu vực các sếp muốn theo dõi thời tiết và chọn đơn vị đo lường (metric units cho độ C).
- **Append Weather to Sheet (`googleSheets`):** 
  - Kết nối tài khoản Google Sheets thông qua `googleSheetsOAuth2Api`.
  - Chọn file Google Sheet và Sheet Name tương ứng. Đảm bảo các cột trong Sheet khớp với các trường dữ liệu mà workflow đẩy lên (Country, Temperature, Humidity, Wind Speed, v.v.).
- **Generate Weather Email HTML (`html` / Set/Function node):** 
  - Node này chịu trách nhiệm dựng template HTML hiển thị thông tin thời tiết. Các sếp có thể tùy chỉnh lại màu sắc, bố cục hoặc thêm bớt các thông số thời tiết cho phù hợp sở thích cá nhân.
- **Send Weather Update Email (`gmail`):** 
  - Kết nối tài khoản Gmail qua `gmailOAuth2`.
  - Cấu hình địa chỉ email người nhận, tiêu đề email (ví dụ: *“Daily Weather Report – {{ $now.toFormat('dd MMM yyyy') }}”*) và lấy kết quả HTML từ node phía trước làm nội dung email.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để test thử nghiệm xem dữ liệu có được ghi vào Google Sheets và email có được gửi đi thành công hay không.
- Sau khi test ngon lành, hãy gạt công tắc sang **Active** để hệ thống tự động chạy ngầm hàng ngày.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Chat App:** Thay vì chỉ gửi Gmail, các sếp có thể mở rộng workflow để bắn thông tin thời tiết trực tiếp lên **Telegram** hoặc **Slack** để tiện đọc trên điện thoại.
- **Theo dõi nhiều địa điểm:** Nhân bản node Fetch Weather và Google Sheets để gom dữ liệu thời tiết từ nhiều thành phố khác nhau (ví dụ: nơi ở, nơi làm việc, địa điểm du lịch sắp tới).
- **Cảnh báo thời tiết cực đoan:** Thêm một nhánh điều kiện (If Node) để nếu nhiệt độ quá cao hoặc có mưa bão, hệ thống sẽ gửi một cảnh báo khẩn cấp ngay lập tức.

### 📌 Kết luận
Workflow **Daily Weather Reports** là một ví dụ tuyệt vời cho thấy tự động hóa no-code có thể cải thiện đời sống và công việc hàng ngày dễ dàng thế nào. Hãy nhanh tay cài đặt ngay để bắt đầu ngày mới với những thông tin thời tiết trong tầm tay các sếp nhé!