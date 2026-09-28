---
title: "🚀 Tự động gửi nhắc nhở phỏng vấn qua Slack DM trước 10 phút từ Google Calendar với n8n"
description: "Giải pháp tự động hóa giúp đội ngũ HR không bao giờ bỏ lỡ lịch phỏng vấn. Workflow tự động quét Google Calendar và gửi tin nhắn Slack trực tiếp (DM) cho ứng viên/phỏng vấn viên trước 10 phút."
slug: "tu-dong-nhac-nho-phong-van-google-calendar-slack"
tags: [n8n, automation, no-code, hr, google-calendar, slack]
keywords: [n8n workflow, tự động hóa phỏng vấn, nhắc nhở lịch họp slack, google calendar integration, hr automation]
---

# 🚀 Tự động gửi nhắc nhở phỏng vấn qua Slack DM trước 10 phút

Các sếp làm HR hay tuyển dụng chắc chắn đã từng ít nhất vài lần gặp cảnh ứng viên quên lịch phỏng vấn, hoặc phỏng vấn viên mải họp quên mất giờ vào phòng meeting. Nhắn tin nhắc nhở thủ công từng người vừa mất thời gian, vừa dễ sót việc khi lịch tuyển dụng dày đặc.

Đừng lo, giải pháp ở đây rồi! Bài viết này sẽ hướng dẫn các sếp thiết lập một workflow n8n cực kỳ thông minh từ **WeblineIndia**. Workflow này sẽ tự động quét lịch trên **Google Calendar**, kiểm tra và gửi tin nhắn nhắc nhở qua **Slack (Direct Message)** đúng **10 phút trước giờ G** mà không cần con người nhúng tay vào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tăng tỷ lệ tham gia:** Giảm thiểu tối đa tình trạng "bùng" lịch phỏng vấn nhờ thông báo đúng thời điểm (trước 10 phút).
- **Tiết kiệm 100% thời gian thủ công:** Không cần nhân sự HR phải đi canh giờ và nhắn tin nhắc lịch bằng tay.
- **Cá nhân hóa chuyên nghiệp:** Gửi tin nhắn trực tiếp (DM) qua Slack đến đúng tài khoản của người liên quan.
- **Cơ chế chống spam thông minh:** Hệ thống ghi nhớ lịch sử (Ledger) để đảm bảo một sự kiện chỉ gửi nhắc nhở đúng 1 lần duy nhất, có kênh Fallback phòng hờ khi không tìm thấy user trên Slack.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã hoạt động (Self-hosted hoặc Cloud).
- **Google Calendar Account:** Tài khoản chứa lịch phỏng vấn của công ty.
- **Slack Workspace:** Đã được cấp quyền tích hợp (OAuth2) để n8n có thể gửi tin nhắn DM và đăng bài lên kênh chung.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy đoạn mã JSON của workflow (hoặc tải file từ nguồn n8n.io/workflows/6683), sau đó vào giao diện n8n chọn **Add workflow** -> Dán (Paste) trực tiếp vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp cần cấu hình chính xác các node trọng điểm sau:

- **Cron Trigger:** Mặc định node này sẽ chạy định kỳ (thường là mỗi phút hoặc vài phút một lần) để quét lịch. Hãy kiểm tra lại tần suất cho phù hợp với quy mô công ty.
- **Set: Config:** Nơi cấu hình các tham số chung cho toàn bộ workflow (ví dụ: ID lịch Google Calendar cần quét, cấu hình tên kênh Fallback...).
- **Get many events (Google Calendar):** 
  - Chọn Credentials tài khoản Google Calendar của các sếp.
  - Cấu hình thông số `operation` là `getAll` để lấy danh sách các sự kiện sắp diễn ra.
- **Prepare Pings & Check Ledger (Function):** Các đoạn mã JavaScript tùy chỉnh giúp lọc ra sự kiện nào chuẩn bị diễn ra trong 10 phút tới và đối chiếu xem sự kiện đó đã được gửi tin nhắn nhắc nhở hay chưa (tránh gửi trùng lặp).
- **If Not Already Sent & User Found? (If):** Các cổng điều kiện kiểm tra trạng thái lịch sử gửi và xác định xem có tìm thấy User tương ứng trên Slack hay không.
- **Send DM & Post to Fallback Channel (Slack):**
  - Kết nối Slack Credentials.
  - **Send DM:** Gửi tin nhắn trực tiếp đến tài khoản Slack của ứng viên/phỏng vấn viên.
  - **Post to Fallback Channel:** Trường hợp hệ thống không tìm thấy User trên Slack (ví dụ: dùng email sai, chưa join workspace), tin nhắn sẽ được đẩy vào một kênh Slack chung để đội ngũ HR chủ động xử lý.
- **Record Ping Sent (Function):** Ghi nhận lại trạng thái sự kiện đã gửi nhắc nhở vào ledger để các chu kỳ quét sau bỏ qua.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để test thử với dữ liệu lịch hiện tại xem hệ thống có bắt đúng sự kiện chuẩn bị diễn ra trong 10 phút hay không.
- Sau khi test thành công không lỗi lầm, gạt công tắc sang **Active** để hệ thống tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Thay vì chỉ dùng Slack, các sếp có thể nối thêm nhánh gửi tin nhắn qua **Telegram Bot** hoặc **Zalo ZNS** nếu ứng viên không dùng Slack thường xuyên.
- **Lưu log vào Google Sheets:** Thêm một node Google Sheets ở bước *Record Ping Sent* để lưu lại lịch sử ai đã nhận được nhắc nhở lúc mấy giờ, phục vụ cho việc báo cáo hiệu suất tuyển dụng.
- **Tùy chỉnh nội dung:** Viết lại nội dung template trong tin nhắn Slack thật thân thiện, có kèm theo link Google Meet hoặc Zoom để người tham gia chỉ cần bấm vào là vào phòng họp luôn.

### 📌 Kết luận
Tự động hóa quy trình tuyển dụng với workflow nhắc nhở phỏng vấn tích hợp Google Calendar và Slack này sẽ giúp bộ phận HR chuyên nghiệp hơn gấp nhiều lần, loại bỏ hoàn toàn tình trạng quên lịch ngớ ngẩn. Hãy cài đặt ngay hôm nay để tối ưu hóa hiệu suất làm việc cho đội ngũ của các sếp nhé!