---
title: "⏰ Tự Động Thông Báo Giờ Tiết Kiệm Ánh Sáng Ngày (DST) Cho Đa Múi Giờ Với n8n"
description: "Hướng dẫn cài đặt workflow n8n tự động kiểm tra và thông báo lịch chuyển đổi Giờ tiết kiệm ánh sáng ngày (DST) qua Slack và Email cho các múi giờ khác nhau."
slug: "tu-dong-thong-bao-gio-tiet-kiem-anh-sang-ngay-dst"
tags: [n8n, automation, no-code, slack, timezones, dateTime]
keywords: [n8n workflow, Daylight Saving Time, thong bao mui gio, tu dong hoa n8n, slack automation, doi gio he gio dong]
---

# ⏰ Tự Động Thông Báo Giờ Tiết Kiệm Ánh Sáng Ngày (DST) Cho Đa Múi Giờ Với n8n

Các sếp có đang quản lý đội ngũ nhân sự, hệ thống server hoặc đối tác làm việc rải rác ở nhiều quốc gia khác nhau không? Việc quên mất lịch chuyển đổi **Giờ tiết kiệm ánh sáng ngày (Daylight Saving Time - DST)** (từ giờ mùa đông sang giờ mùa hè và ngược lại) thường dẫn đến việc trễ họp, lệch deadline hoặc lỗi lịch trình vô cùng phiền toái. 

Thay vì phải thủ công tra cứu lịch đổi giờ của từng quốc gia, workflow n8n này sẽ tự động hóa 100% quy trình: quét danh sách múi giờ, tính toán thời điểm chuyển đổi và gửi cảnh báo trực tiếp qua **Slack** hoặc **Email** trước khi sự thay đổi diễn ra.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Không bao giờ lỡ hẹn:** Chủ động nhận thông báo trước khi múi giờ thay đổi, giúp sắp xếp lịch họp quốc tế chính xác.
- **Tự động hóa hoàn toàn:** Hệ thống tự chạy định kỳ nhờ lịch trình (`Schedule Trigger`) mà không cần con người can thiệp.
- **Đa kênh thông báo:** Linh hoạt gửi cảnh báo qua kênh Slack của team hoặc gửi Email trực tiếp.
- **Dễ dàng mở rộng:** Thêm bớt bất kỳ quốc gia hay múi giờ nào chỉ với vài dòng cấu hình code JavaScript.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Slack Workspace:** Cần quyền kết nối hoặc Bot Token để gửi tin nhắn thông báo (qua node `Send Notification On Upcoming Change`).
- **SMTP Server (Tùy chọn):** Nếu muốn nhận thông báo qua email (qua node `Send Email On Upcoming Change`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trong n8n, sau đó copy toàn bộ mã JSON của workflow này và dán trực tiếp vào màn hình n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 9 nodes chính hoạt động nhịp nhàng. Các sếp cần chú ý cấu hình các node quan trọng sau:

- **Schedule Trigger:** Mặc định workflow sẽ chạy tự động theo lịch (ví dụ: chạy hàng ngày). Hãy cấu hình khung giờ chạy phù hợp với múi giờ của các sếp.
- **Timezones List (Node Code):** Mở node này và thêm danh sách các múi giờ mà các sếp muốn theo dõi (ví dụ: `America/New_York`, `Europe/London`, `Asia/Tokyo`,...).
- **Calculate Zone Date and Time & Check If Daylight Saving Time (Nodes Set):** Các node này xử lý logic tính toán thời gian thực tế và trạng thái DST của từng múi giờ được truyền vào từ danh sách.
- **Check If Change Tomorrow (Node If):** Kiểm tra xem ngày mai có phải là thời điểm múi giờ đó thay đổi lịch DST hay không.
- **Calculate Tomorrow's Date (Node DateTime):** Sử dụng thao tác `addToDate` để xác định chính xác mốc thời gian ngày tiếp theo.
- **Send Notification On Upcoming Change (Node Slack):** 
  - Chọn hoặc tạo mới **Credentials** cho Slack (OAuth2).
  - Chọn kênh (Channel) hoặc User nhận tin nhắn thông báo.
- **Send Email On Upcoming Change (Node EmailSend):** 
  - Cấu hình thông tin SMTP (Gmail, SendGrid, Amazon SES,...) nếu muốn nhận cảnh báo qua email.

#### 3. Kích hoạt ⚡️
- Nhấn nút **‘Test workflow’** để chạy thử nghiệm xem hệ thống có quét và trả về đúng dữ liệu múi giờ hay không.
- Sau khi kiểm tra mọi thứ hoạt động trơn tru, hãy gạt công tắc sang **Active** để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
Để workflow trở nên "lợi hại" hơn, các sếp có thể tùy biến:
1. **Tích hợp thêm Telegram:** Thêm node Telegram Bot bên cạnh Slack để bắn thông báo vào nhóm chat chung của công ty.
2. **Lưu lịch sử vào Google Sheets:** Ghi lại mỗi lần có thay đổi DST vào một file Google Sheets để làm nhật ký theo dõi.
3. **Cá nhân hóa nội dung:** Viết lại template thông báo trên Slack với các icon sinh động (⏰, ⚠️, 🌍) để đội ngũ chú ý hơn.

### 📌 Kết luận
Việc quản lý các múi giờ có quy đổi DST thủ công rất dễ gây nhầm lẫn và sai sót. Với workflow n8n này, các sếp đã có ngay một "trợ lý" thông minh tự động túc trực 24/7 để nhắc nhở toàn bộ team. Cài đặt ngay thôi nào!