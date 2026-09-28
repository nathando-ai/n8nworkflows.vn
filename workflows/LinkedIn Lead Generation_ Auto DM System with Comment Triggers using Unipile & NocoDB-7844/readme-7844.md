---
title: "🚀 Tự động hóa LinkedIn Lead Generation: Gửi DM và tài liệu qua Comment cực đỉnh với Unipile & NocoDB"
description: "Hướng dẫn thiết lập workflow n8n tự động quét bình luận trên LinkedIn, kiểm tra kết nối, gửi tin nhắn trực tiếp (DM) kèm quà tặng (Lead Magnet) và lưu trữ thông tin qua NocoDB."
slug: "linkedin-lead-generation-auto-dm-system-unipile-nocodb"
tags: [n8n, automation, no-code, linkedin, unipile, nocodb]
keywords: [n8n workflow, tự động hóa linkedin, lead generation, unipile api, nocodb automation, gửi dm tự động]
---

# 🚀 Tự động hóa LinkedIn Lead Generation: Gửi DM và tài liệu qua Comment cực đỉnh với Unipile & NocoDB

Các sếp có đang tốn hàng giờ mỗi ngày để lọc bình luận trên LinkedIn, kiểm tra xem ai là bạn bè, ai chưa kết nối, rồi thủ công nhắn tin gửi tài liệu (Lead Magnet) cho từng khách hàng tiềm năng không? Công việc lặp đi lặp lại này vừa mất thời gian lại dễ bỏ sót khách hàng nóng.

Đừng lo nữa, bài viết này sẽ hướng dẫn các sếp triển khai một hệ thống tự động hóa 100% bằng n8n, kết hợp với **Unipile** (quản lý LinkedIn API) và **NocoDB** (lưu trữ database). Workflow này sẽ tự động bắt từ khóa trong comment, kiểm tra trạng thái kết nối, gửi lời mời kết nối hoặc nhắn tin gửi tài liệu ngay lập tức một cách cực kỳ tự nhiên!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn phải thủ công copy/paste link tài liệu hay gõ tin nhắn cho từng người comment.
- **Tương tác thông minh:** Tự động nhận diện đã kết nối hay chưa để gửi tin nhắn (DM) trực tiếp hoặc gửi lời mời kết nối kèm reply bình luận tự nhiên.
- **Chống trùng lặp thông minh:** Hệ thống đối chiếu qua NocoDB để đảm bảo không gửi tin nhắn 2 lần cho cùng một người.
- **An toàn cho tài khoản:** Tích hợp thời gian chờ (Wait) ngẫu nhiên giữa các lần gửi, giúp mô phỏng hành vi con người, tránh bị LinkedIn quét.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Tài khoản Unipile:** Dùng để kết nối và thao tác với LinkedIn API (`httpHeaderAuth`).
- **Tài khoản NocoDB:** Tạo sẵn database để lưu log khách hàng (`n0coDbApiToken`).
- **Form Trigger (Tùy chọn):** Nơi các sếp nhập Post ID, từ khóa kích hoạt (trigger word) và link tài liệu (Lead Magnet URL).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy trực tiếp mã JSON từ nguồn.
- Vào giao diện n8n Editor, chọn **Add workflow** -> **Import from File** hoặc dán trực tiếp vào màn hình làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống vận hành trơn tru, các sếp cần chú ý cấu hình các node cốt lõi sau:

- **Node `On form submission` (hoặc Trigger đầu vào):** Cấu hình các biến đầu vào theo ghi chú canvas bao gồm: `Post ID` (ID bài viết LinkedIn), `trigger` (từ khóa trong comment cần bắt), và `lead magnet URL` (đường dẫn tài liệu tặng kèm).
- **Node `Get Comments from Posts`, `Send DM with Lead Magnet`, `Answer to comment`, `Ask For connection`:** Đây là các node gọi API thông qua **Unipile**. Các sếp cần cấu hình **Credentials** loại `HTTP Header Auth` trỏ tới tài khoản Unipile của mình.
- **Các node NocoDB (`Create a row`, `Get all the rows where...`, `Create a row2`):** Kết nối với bảng NocoDB của các sếp bằng `NocoDb API Token`. Đảm bảo các tên bảng và trường dữ liệu (columns) khớp với dữ liệu workflow truyền vào để tracking lịch sử gửi DM và kết nối.
- **Node `Wait`:** Cấu hình thời gian chờ linh hoạt (có độ trễ ngẫu nhiên) nhằm đảm bảo an toàn, tránh việc LinkedIn đánh dấu tài khoản là spam bot.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm một lượt (**Test workflow**) với một bài đăng cụ thể có bình luận mẫu để kiểm tra luồng dữ liệu qua các nhánh `If`, `Filter`, và `Split In Batches`.
- Sau khi test thành công không báo lỗi, hãy bật công tắc **Active** để hệ thống tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Telegram/Slack:** Thêm một node Telegram hoặc Slack ở cuối luồng để gửi thông báo về điện thoại mỗi khi có một Lead mới nhận được tài liệu.
- **Mở rộng AI Response:** Kết hợp thêm OpenAI node để tạo lời nhắn phản hồi comment mang tính cá nhân hóa cao hơn dựa trên nội dung bình luận thực tế của khách hàng.
- **Báo cáo định kỳ:** Tạo thêm cron trigger chạy cuối tuần để tổng hợp số lượng lead đã tiếp cận vào Google Sheets hoặc Email báo cáo.

### 📌 Kết luận
Hệ thống tự động hóa LinkedIn Lead Generation này chính là "vũ khí bí mật" giúp các sếp tối ưu hóa phễu bán hàng B2B mà không tốn nhiều nhân lực. Hãy thiết lập ngay hôm nay và tận hưởng lượng khách hàng tiềm năng đổ về tự động mỗi ngày!