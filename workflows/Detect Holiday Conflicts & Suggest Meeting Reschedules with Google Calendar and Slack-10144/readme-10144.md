---
title: "🚀 Tự động phát hiện xung đột lịch họp ngày lễ & Gợi ý lịch đổi qua Google Calendar & Slack"
description: "Tự động quét lịch họp tuần tới trên Google Calendar, so sánh với ngày lễ quốc tế và gửi báo cáo thông minh kèm lịch gợi ý lên Slack cho team phân tán."
slug: "tu-dong-phat-hien-xung-dot-lich-hop-ngay-le-slack-google-calendar"
tags: [n8n, automation, no-code, google-calendar, slack, productivity]
keywords: [n8n workflow, tự động hóa lịch họp, phát hiện ngày lễ, google calendar slack, n8n template tieng viet]
---

# 🚀 Tự động phát hiện xung đột lịch họp ngày lễ & Gợi ý lịch đổi qua Google Calendar & Slack

Các sếp làm việc trong các team phân tán (remote/global teams) chắc chắn đã từng gặp cảnh "dở khóc dở cười" khi đặt lịch họp vào đúng ngày nghỉ lễ của đồng nghiệp ở quốc gia khác. Việc kiểm tra thủ công lịch nghỉ lễ của từng nước rồi rà soát lại calendar tốn rất nhiều thời gian và dễ bị sót.

Workflow n8n này sẽ giải quyết triệt để vấn đề đó: Tự động hóa 100% việc quét lịch họp tuần tới, đối chiếu với ngày lễ công khai toàn cầu, tìm ra các điểm xung đột và tự động đề xuất ngày dời lịch hợp lý, sau đó gửi báo cáo gọn gàng trực tiếp lên Slack. Không cần code phức tạp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian:** Không cần thủ công kiểm tra lịch nghỉ lễ của từng quốc gia trước khi book lịch họp.
- **Tránh nhầm lẫn:** Phát hiện chính xác 100% các cuộc họp bị trùng vào ngày nghỉ lễ trong tuần tới.
- **Thông minh & Tiện lợi:** Tự động tính toán và gợi ý ngày làm việc tiếp theo gần nhất không vướng ngày lễ hay cuối tuần.
- **Cảnh báo tập trung:** Gửi một thông báo tổng hợp (digest) duy nhất qua Slack giúp team nắm bắt nhanh chóng.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** (Self-hosted hoặc Cloud).
- **Google Calendar:** Tài khoản có quyền đọc sự kiện (Read access).
- **Slack App:** Đã cấu hình quyền `chat:write` và quyền truy cập kênh Slack.
- **API Ngày lễ:** Workflow sử dụng Nager.Date API công khai (không cần API Key).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này và import trực tiếp vào n8n Editor của các sếp, hoặc copy toàn bộ JSON và paste trực tiếp vào màn hình workflow trống.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình các thành phần quan trọng sau:

- **Node `Workflow Configuration` (Set):** Đây là trung tâm cấu hình của workflow. Các sếp cần chỉnh sửa các biến:
  - `countryCodes`: Danh sách các mã quốc gia cần kiểm tra ngày lễ (ví dụ: `["US", "JP", "VN"]`).
  - `calendarId`: ID của Google Calendar cần kiểm tra (thường là `primary` hoặc email tài khoản Google).
  - `slackChannel`: Kênh Slack nhận thông báo (ví dụ: `#general` hoặc `#meetings`).
  - `currentYear`, `nextWeekStart`, `nextWeekEnd`: Khoảng thời gian quét lịch.
- **Node `Get Next Week Calendar Events` (Google Calendar):** Kết nối lại tài khoản Google của các sếp để cấp quyền đọc lịch.
- **Node `Post Slack Digest` (Slack):** Kết nối lại tài khoản Slack OAuth của các sếp để bot có quyền gửi tin nhắn.
- **Node `Daily Check` (Schedule Trigger):** Mặc định chạy vào 09:00 sáng mỗi ngày làm việc. Các sếp có thể đổi thành chạy hàng tuần (Thứ Hai) nếu muốn.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** để test thủ công xem dữ liệu trả về từ API ngày lễ và Google Calendar có chính xác không.
- Sau khi test thành công, bật nút **Active** ở góc trên cùng bên phải để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm kênh thông báo:** Ngoài Slack, các sếp có thể duplicate node Slack và đổi thành node Telegram Bot để gửi cảnh báo trực tiếp về điện thoại cá nhân.
- **Lưu log vào Google Sheets:** Thêm một node Google Sheets ở cuối nhánh phát hiện xung đột để lưu lại lịch sử thay đổi/phát hiện ngày lễ phục vụ kiểm toán nội bộ.
- **Mở rộng phạm vi:** Tùy chỉnh node `Generate Reschedule Suggestions` bằng đoạn code JS sẵn có để tinh chỉnh logic tìm ngày thay thế phù hợp với múi giờ của doanh nghiệp.

### 📌 Kết luận
Workflow này là một "trợ lý ảo" hoàn hảo cho các team làm việc xuyên quốc gia, giúp loại bỏ hoàn toàn các buổi họp "hụt" do bất đồng lịch nghỉ lễ. Hãy cài đặt ngay hôm nay để tối ưu hóa năng suất cho toàn bộ tổ chức các sếp nhé!