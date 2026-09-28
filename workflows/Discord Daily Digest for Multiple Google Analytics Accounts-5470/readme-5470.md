---
title: "🚀 Tự động gửi báo cáo Google Analytics hằng ngày lên Discord cho nhiều tài khoản"
description: "Hướng dẫn cấu hình workflow n8n giúp tự động tổng hợp dữ liệu Google Analytics của nhiều Property và gửi báo cáo thông minh lên Discord hằng ngày, kèm tính năng cập nhật số liệu chuẩn xác."
slug: "discord-daily-digest-google-analytics-multiple-accounts"
tags: [n8n, automation, no-code, google-analytics, discord, marketing, market-research]
keywords: [n8n workflow, tự động hóa google analytics, discord digest, báo cáo marketing tự động, n8n viet nam]
---

# 🚀 Tự động gửi báo cáo Google Analytics hằng ngày lên Discord cho nhiều tài khoản

Chào các sếp! Quản lý một hay nhiều website đồng nghĩa với việc các sếp phải liên tục kiểm tra số liệu truy cập trên Google Analytics (GA4). Việc mở từng dashboard mỗi ngày để xem traffic vừa tốn thời gian, vừa dễ bỏ quên các biến động quan trọng. 

Bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ xịn sò được thiết kế bởi **Jay Emp0**. Workflow này sẽ tự động hóa toàn bộ quy trình: lấy dữ liệu từ **nhiều Google Analytics Property khác nhau**, xử lý thông minh qua các node logic, sau đó gửi báo cáo tóm tắt (Daily Digest) trực tiếp lên các **kênh Discord** tương ứng. Điểm ăn tiền nhất là workflow còn hỗ trợ tự động cập nhật lại các chỉ số trong quá khứ (vì dữ liệu GA thường mất vài ngày để hoàn thiện), giúp các sếp luôn có con số chính xác nhất!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Không cần mò vào GA4 hằng ngày, số liệu tự động đẩy thẳng vào Discord theo lịch hẹn.
- **Đa tài khoản (Multi-account):** Gom số liệu của nhiều website/property khác nhau và phân tách gửi về các kênh Discord riêng biệt.
- **Số liệu luôn chính xác:** Cơ chế cập nhật thông minh giúp tinh chỉnh lại các giá trị traffic cũ khi GA4 đã chốt số liệu (thường sau 7 ngày).
- **Teamwork hiệu quả:** Team Marketing, Sales hoặc Founder cùng nắm bắt được nhịp độ tăng trưởng trực quan ngay trên Discord chung của công ty.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt sẵn sàng (Cloud hoặc Self-hosted).
- **Google Analytics Account:** Tài khoản có quyền truy cập vào các GA4 Property cần lấy số liệu (Chuẩn bị sẵn Google Analytics Property ID).
- **Discord Bot / Server:** Quyền tạo Webhook hoặc Bot trên Discord, cùng với Discord Channel ID nơi nhận thông báo.
- **HTTP Header Auth:** Token cho Discord Bot để gọi API cập nhật tin nhắn.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow từ nguồn cung cấp (hoặc file JSON tải về), vào n8n editor, chọn **Add workflow** -> **Import from File / Paste JSON** là xong.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 22 nodes với hệ thống xử lý phức tạp, các sếp cần lưu ý cấu hình kỹ các điểm sau:

- **Node `Google Analytics`:** 
  - Kết nối tài khoản qua **Google Analytics OAuth2**.
  - Điền Property ID của các website cần theo dõi. (Xem ID bằng cách vào GA4 dashboard, nhìn góc trên bên phải của property).
- **Node `Schedule Trigger` (và các Schedule Trigger 1, 2, 3):**
  - Cấu hình lịch chạy (ví dụ: mỗi ngày lúc 8:00 sáng, hoặc sau thời điểm UTC midnight khi GA4 làm mới dữ liệu).
- **Nodes xử lý dữ liệu (`Code`, `gaData`, `Sort`, `Switch`):**
  - Các node này làm nhiệm vụ lọc, sắp xếp và gom nhóm dữ liệu theo ngày (`Date`). Sếp chỉ cần kiểm tra lại logic mapping nếu muốn đổi định dạng hiển thị.
- **Node `Discord` & `HTTP Request` (Cập nhật tin nhắn):**
  - Cấu hình **Discord OAuth2 API** cho node Discord chính để lấy danh sách/gửi tin nhắn mới.
  - Đối với node `HTTP Request` (dùng để update tin nhắn cũ trên Discord): Do tính năng sửa tin nhắn qua node mặc định chưa hoàn thiện, workflow sử dụng trực tiếp Discord API. Sếp cần chuẩn bị **Bot Token Authorization Header** theo [tài liệu Discord Developer](https://discord.com/developers/docs/reference#authentication).
- **Lấy Discord Channel ID:**
  - Gửi một tin nhắn bất kỳ lên kênh Discord muốn nhận báo cáo, sau đó copy link tin nhắn dạng: `https://discord.com/channels/server_id/channel_id/message_id`. Lấy đoạn số ở giữa chính là `channel_id`.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test workflow**) bằng tay cho một Property trước để kiểm tra dữ liệu trả về trên Discord.
- Nếu mọi thứ hiển thị mượt mà, gạt công tắc sang **Active** để hệ thống tự động chạy ngầm mỗi ngày.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh nhận tin:** Ngoài Discord, các sếp có thể clone nhánh dữ liệu để gửi đồng thời bản tóm tắt qua Telegram Bot hoặc Slack.
- **Lưu trữ lịch sử:** Thêm một node Google Sheets ở cuối chuỗi xử lý để lưu lại lịch sử báo cáo hằng ngày phục vụ việc vẽ biểu đồ tăng trưởng dài hạn.
- **Cảnh báo thông minh (Alerts):** Kết hợp thêm node `If` hoặc `Switch` để nếu traffic tăng/giảm đột ngột trên X%, tự động ping tag `@here` hoặc `@everyone` nhắc nhở team.

### 📌 Kết luận
Việc theo dõi số liệu marketing chưa bao giờ khỏe đến thế. Với workflow n8n kết hợp Google Analytics và Discord này, các sếp vừa tiết kiệm được hàng giờ đồng hồ mỗi tuần, vừa giúp đội ngũ bám sát dữ liệu sát sao hơn. Triển khai ngay và tận hưởng thành quả thôi nào các sếp!