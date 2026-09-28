---
title: "☀️ Tích hợp dự báo thời tiết 7 ngày từ National Weather Service vào Slack tự động với n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động lấy dữ liệu thời tiết 7 ngày tới từ National Weather Service (NWS) và gửi thông báo trực tiếp vào Slack chỉ với vài cú click."
slug: "du-bao-thoi-tiet-national-weather-service-slack-n8n"
tags: [n8n, automation, slack, weather-forecast, webhook, api-integration]
keywords: [n8n workflow, n8n weather slack, national weather service api, tich hop slack thoi tiet, tu dong hoa n8n]
---

# ☀️ Tự động hóa gửi dự báo thời tiết 7 ngày từ NWS lên Slack qua n8n

Các sếp có bao giờ cảm thấy việc cập nhật thời tiết thủ công mỗi ngày cho team hoặc cho các dự án ngoài trời, vận chuyển tốn quá nhiều thời gian không? Thay vì phải tra cứu từng khu vực trên web, workflow n8n này sẽ giúp các sếp tự động hóa 100% quy trình: nhận yêu cầu qua Webhook, tra cứu tọa độ từ OpenStreetMap, gọi dữ liệu dự báo thời tiết 7 ngày từ **National Weather Service (NWS)** và đẩy thẳng kết quả trực quan vào kênh Slack của doanh nghiệp.

Được thiết kế bởi chuyên gia n8n Ambassador Alex Kim, giải pháp này cực kỳ gọn nhẹ, tối ưu và sẵn sàng để các sếp "lên đồ" ứng dụng ngay lập tức!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian tuyệt đối:** Không cần tra cứu thủ công, thông tin thời tiết 7 ngày được tổng hợp và gửi đi tự động.
- **Cập nhật chính xác:** Sử dụng dữ liệu thời tiết chuẩn xác từ National Weather Service (NWS) kết hợp định vị tọa độ OpenStreetMap.
- **Cộng đồng kết nối liền mạch:** Gửi thông tin trực tiếp vào Slack giúp toàn bộ team dễ dàng nắm bắt tình hình thời tiết để lên kế hoạch công việc.
- **Hoạt động 24/7:** Vận hành trơn tru trên hệ thống n8n tự động hoàn toàn không cần can thiệp thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n đang hoạt động (Cloud hoặc Self-hosted).
- Tài khoản Slack và quyền kết nối Slack App (Slack OAuth2 API) để gửi tin nhắn.
- Không cần API Key phức tạp cho NWS hay OpenStreetMap vì sử dụng các endpoint công khai tiêu chuẩn.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow từ nguồn cấp hoặc copy đoạn JSON tương ứng.
- Trong giao diện n8n Editor, chọn **Add workflow** -> Nhấp vào biểu tượng ba chấm ở góc trên bên phải -> Chọn **Import from File** hoặc **Import from Clipboard** và dán mã JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 5 nodes chính, các sếp cần chú ý cấu hình kỹ các điểm sau:

- **Webhook:**
  - Node này nhận yêu cầu kích hoạt (HTTP Method: `POST`, Path: `slack1`). Các sếp có thể thay đổi đường dẫn path tùy theo nhu cầu gọi từ hệ thống bên ngoài hoặc cấu hình Slash Command từ Slack.
- **OpenStreetMap (HTTP Request):**
  - Chịu trách nhiệm chuyển đổi tên địa điểm/khu vực thành tọa độ (Latitude/Longitude) để NWS có thể đọc được. Kiểm tra lại URL request và các tham số truyền vào đảm bảo khớp với địa điểm các sếp muốn tra cứu.
- **NWS & NWS1 (HTTP Request):**
  - Các nodes gọi API đến National Weather Service. Node đầu tiên dùng để lấy điểm lưới (grid points) dựa trên tọa độ, và node thứ hai lấy bản tin dự báo 7 ngày chi tiết (`forecast`). Các sếp chỉ cần giữ nguyên cấu trúc URL chuẩn của NWS.
- **Slack:**
  - Cần thiết lập **Credentials** (`slackOAuth2Api`). 
  - Chọn tài khoản Slack đã kết nối, chỉ định Channel (kênh) nhận tin nhắn và tùy chỉnh template nội dung hiển thị (lấy dữ liệu trả về từ các nodes NWS phía trước) để bản tin thời tiết gửi lên sinh động, dễ đọc nhất.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và bắn một request mẫu qua Webhook để test thử xem dữ liệu trả về và tin nhắn trên Slack đã chuẩn chỉnh chưa.
- Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để workflow chính thức đi vào hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm Lệnh Slash trong Slack:** Thay vì Webhook thông thường, các sếp có thể cấu hình Slack Slash Command (ví dụ: `/weather [địa_điểm]`) để gọi trực tiếp n8n workflow.
- **Gửi báo cáo định kỳ tự động:** Thay thế node Webhook bằng node **Schedule Trigger** để hệ thống tự động gửi dự báo thời tiết mỗi sáng lúc 7:00 AM vào kênh Slack chung của công ty.
- **Cảnh báo thời tiết xấu:** Thêm một node **If** để lọc dữ liệu dự báo, nếu phát hiện mưa bão hoặc nhiệt độ khắc nghiệt, tự động gắn thẻ (tag) tên các quản lý hoặc gửi thông báo khẩn cấp.

### 📌 Kết luận
Workflow tích hợp dự báo thời tiết 7 ngày từ National Weather Service lên Slack là một mảnh ghép tuyệt vời giúp tối ưu hóa giao tiếp và lập kế hoạch công việc dựa trên điều kiện thực tế. Hãy áp dụng ngay vào hệ thống n8n của các sếp để tối ưu hóa vận hành ngay hôm nay!