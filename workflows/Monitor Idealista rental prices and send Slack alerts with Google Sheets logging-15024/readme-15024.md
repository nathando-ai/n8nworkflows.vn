---
title: "🚀 Tự động giám sát giá thuê nhà Idealista và cảnh báo qua Slack bằng n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động quét dữ liệu thuê nhà từ Idealista mỗi 6 giờ, lọc tin đăng mới, cảnh báo qua Slack và lưu trữ lịch sử vào Google Sheets."
slug: "tu-dong-giam-sat-gia-thue-nha-idealista-slack-google-sheets"
tags: [n8n, automation, no-code, idealista, slack, google-sheets, market-research]
keywords: [n8n workflow, tu dong hoa idealista, giam sat gia thue, slack alert, google sheets automation]
---

# 🚀 Tự động giám sát giá thuê nhà Idealista và cảnh báo qua Slack

Việc theo dõi thủ công các trang web bất động sản lớn như Idealista để tìm kiếm cơ hội thuê nhà hoặc nghiên cứu thị trường cực kỳ tốn thời gian và dễ bỏ lỡ các tin đăng tốt. Thay vì tốn hàng giờ F5 trang web mỗi ngày, các sếp có thể tự động hóa toàn bộ quy trình này 24/7 với n8n mà không cần viết code phức tạp.

Workflow này sẽ giúp tự động quét dữ liệu thuê nhà, lọc ra các tin mới xuất sắc nhất, bắn thông báo tức thì lên Slack và lưu trữ dữ liệu vào Google Sheets để làm lịch sử đối soát.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian:** Không cần thủ công kiểm tra lại các tin đăng cũ hay tìm kiếm định kỳ.
- **Bắt nhịp cơ hội nhanh chóng:** Nhận cảnh báo trực tiếp qua Slack ngay khi có căn hộ mới lên sàn.
- **Lưu trữ dữ liệu thông minh:** Tự động ghi nhận danh sách vào Google Sheets, giúp tránh lặp tin (deduplication) và thuận tiện cho việc nghiên cứu thị trường.
- **Hoạt động tự động 24/7:** Chạy ngầm định trung bình mỗi 6 giờ hoặc theo lịch trình tùy chỉnh của các sếp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Idealista Scraper Node:** Cấu hình truy cập dữ liệu từ Idealista.
- **Slack Account & Bot:** Đã tạo Slack App/Bot để gửi tin nhắn đến kênh (channel) mong muốn.
- **Google Sheets:** Chuẩn bị sẵn một Google Sheet để lưu lịch sử tin đăng.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow hoặc sao chép toàn bộ mã nguồn JSON, sau đó dán trực tiếp vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 6 nodes chính hoạt động nhịp nhàng. Các sếp cần chú ý cấu hình kỹ các node sau:

- **Every 6 Hours1 (`scheduleTrigger`):** Node kích hoạt lịch trình định kỳ. Các sếp có thể thay đổi tần suất quét (ví dụ: mỗi 2 giờ, 1 lần/ngày) tùy theo nhu cầu thực tế.
- **Fetch Idealista Rentals (`idealistaScraper`):** Kết nối và cấu hình tiêu chí tìm kiếm bất động sản mục tiêu (Khu vực, mức giá, số phòng ngủ, loại hình...).
- **Filter New Listings (`code`):** Node chứa đoạn code JavaScript giúp so sánh kết quả vừa quét với lịch sử lưu trữ nhằm đảm bảo chỉ lọc ra các tin thực sự mới (chống trùng lặp).
- **Prepare Slack Message (`set`):** Chuẩn hóa nội dung tin nhắn, định dạng các thông tin như giá, diện tích, link chi tiết để hiển thị đẹp mắt trên Slack.
- **Post Slack Notification (`slack`):** Kết nối tài khoản Slack Credentials của các sếp và chọn đích đến là kênh (Channel) hoặc user nhận thông báo.
- **Append Listings in Sheets (`googleSheets`):** Chọn tài khoản Google Sheets Credentials, trỏ đến file Sheet và Sheet Name dùng để theo dõi lịch sử tin đăng, đảm bảo thao tác `append` hoạt động chính xác.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để chạy thử với dữ liệu mẫu, kiểm tra kỹ xem tin nhắn có bắn về Slack và dữ liệu có được đẩy vào Google Sheets hay không.
- Nếu mọi thứ mượt mà, hãy gạt công tắc sang **Active** để hệ thống tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm AI (OpenAI/Claude):** Thêm một node AI sau bước quét tin để tự động phân tích đánh giá mức giá (rẻ, đắt, hợp lý) so với khu vực trước khi gửi lên Slack.
- **Đa kênh thông báo:** Ngoài Slack, các sếp có thể cấu hình thêm node Telegram hoặc Email để nhận cảnh báo linh hoạt hơn.
- **Báo cáo định kỳ:** Tạo thêm một nhánh chạy vào cuối tuần để tổng hợp số lượng căn hộ mới lên sàn trong tuần qua gửi vào email cá nhân.

### 📌 Kết luận
Với workflow n8n tự động hóa này, việc giám sát thị trường bất động sản hay tìm kiếm nhà cho thuê Idealista trở nên nhẹ nhàng và chuyên nghiệp hơn bao giờ hết. Hãy setup ngay hôm nay để không bỏ lỡ bất kỳ cơ hội nào các sếp nhé!