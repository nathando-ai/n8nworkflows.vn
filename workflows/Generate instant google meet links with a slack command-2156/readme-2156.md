---
title: "🚀 Tạo Link Google Meet Tức Thì Ngay Trong Slack Bằng n8n"
description: "Tự động hóa việc tạo và gửi link Google Meet trực tiếp từ Slack chỉ bằng một câu lệnh đơn giản, giúp tiết kiệm thời gian họp nhóm."
slug: "tao-link-google-meet-tu-dong-tu-slack"
tags: [n8n, automation, slack, google-calendar, productivity]
keywords: [n8n workflow, tao link google meet, slack command, tu dong hoa n8n]
---

# 🚀 Tạo Link Google Meet Tức Thì Ngay Trong Slack Bằng n8n

Việc phải mở Google Calendar, tạo sự kiện mới chỉ để lấy một link Google Meet rồi copy gửi qua Slack đôi khi làm các sếp mất tập trung và tốn thời gian. Giải pháp thủ công này hoàn toàn có thể được tối ưu hóa.

Với workflow n8n này, các sếp chỉ cần gõ một lệnh đơn giản trên Slack (ví dụ: `/meet`), hệ thống sẽ tự động tạo một sự kiện tạm thời trên Google Calendar, lấy ngay link Google Meet, gửi thẳng vào kênh Slack và dọn dẹp sự kiện thừa ngay lập tức. Tất cả diễn ra chỉ trong tích tắc và hoàn toàn tự động!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tốc độ chớp nhoáng:** Tạo và nhận link Google Meet ngay trong Slack mà không cần chuyển đổi tab hay ứng dụng.
- **Tự động hóa quy trình:** Không còn thao tác thủ công tạo lịch họp rườm rà.
- **Tối ưu trải nghiệm nhóm:** Mọi thành viên trong kênh Slack có thể thấy và tham gia cuộc họp ngay lập tức.
- **Hoạt động 24/7:** Hệ thống tự động dọn dẹp các lịch hẹn tạm thời trên Google Calendar, giữ cho lịch làm việc luôn gọn gàng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản **n8n** (Cloud hoặc Self-hosted).
- Tài khoản **Slack Workspace** có quyền tạo App và Slash Command.
- Tài khoản **Google Account** đã kết nối Google Calendar.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này và import trực tiếp vào n8n Editor của các sếp, hoặc tạo mới một workflow và copy/paste cấu trúc JSON tương ứng.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

Workflow này gồm 4 nodes chính, các sếp cần cấu hình tuần tự như sau:

**Bước A: Cấu hình Slack App & Webhook Node**
1. Truy cập [Slack API Apps](https://api.slack.com/apps), bấm **New App** và chọn Workspace của các sếp.
2. Vào **OAuth & Permissions**, tại phần *Bot Token Scopes*, thêm quyền `chat:write` và `chat:write.public`.
3. Vào phần **Slash Commands**, bấm **Create New Command** với lệnh `/meet`.
4. Copy **Production URL** từ node **Webhook** (`path`: `slack-meet-trigger`, phương thức `POST`) dán vào ô *Request URL* trong Slack.
5. Cài đặt App vào Workspace của các sếp.

**Bước B: Cấu hình Google Calendar (Tạo sự kiện & Lấy link Meet)**
- Tại node **Create event with google meet link**, kết nối tài khoản Google Calendar của các sếp.
- Chọn đúng Calendar (Lịch) muốn sử dụng để sinh link họp. Node này sẽ tự động đính kèm link Google Meet vào sự kiện.

**Bước C: Gửi tin nhắn qua Slack**
- Tại node **Send msg with Google meet link**, kết nối tài khoản Slack.
- Cấu hình nội dung tin nhắn, đảm bảo sử dụng biểu thức (`expression`) chứa `hangoutLink` để hệ thống trích xuất và hiển thị link Google Meet vừa tạo ra.

**Bước D: Dọn dẹp lịch tạm thời**
- Node **Delete temporary calendar event** sử dụng thao tác xóa (`operation: delete`) để tự động xóa sự kiện ảo vừa được tạo ra ở bước trên nhằm tránh làm rác lịch Google Calendar của các sếp.

#### 3. Kích hoạt ⚡️
- Chạy thử (Test run) bằng cách gõ lệnh trên Slack để kiểm tra luồng dữ liệu.
- Sau khi mọi thứ hoạt động trơn tru, bật trạng thái **Active** cho workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm thông báo:** Các sếp có thể mở rộng workflow để gửi thông báo tóm tắt qua tin nhắn riêng (Direct Message) cho người khởi tạo lệnh.
- **Ghi log cuộc họp:** Lưu trữ thông tin thời gian và link meet vào Google Sheets để tiện theo dõi lịch sử họp trong tuần/tháng.
- **Tùy chỉnh tên sự kiện:** Thay đổi tiêu đề sự kiện mặc định trên Google Calendar theo cú pháp: `Quick Meeting - [Tên người dùng Slack]` để dễ phân biệt.

### 📌 Kết luận
Chỉ với vài phút thiết lập, các sếp đã có ngay một "trợ lý ảo" chuyên cấp phát link Google Meet trực tiếp trong Slack cực kỳ chuyên nghiệp. Áp dụng ngay để tối ưu hóa thời gian làm việc nhóm thôi nào!