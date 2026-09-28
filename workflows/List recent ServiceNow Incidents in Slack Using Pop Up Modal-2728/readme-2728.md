---
title: "🚀 Xem nhanh sự cố ServiceNow trực tiếp trong Slack bằng Popup Modal"
description: "Tự động hóa tra cứu sự cố ServiceNow từ giao diện Slack Modal, lọc theo độ ưu tiên và trạng thái, sau đó trả kết quả về kênh hoặc tin nhắn riêng."
slug: "xem-nhanh-su-co-servicenow-trong-slack-bang-modal"
tags: [n8n, automation, no-code, slack, servicenow, it-support]
keywords: [n8n workflow, tự động hóa slack servicenow, tra cứu sự cố it, slack modal n8n]
---

# 🚀 Tự động hóa tra cứu sự cố ServiceNow qua Slack Modal

Các sếp làm IT Support hoặc quản trị hệ thống chắc hẳn luôn gặp phiền toái mỗi khi cần kiểm tra nhanh trạng thái các sự cố (incidents) trên ServiceNow: cứ phải rời khỏi Slack, mở trình duyệt, đăng nhập vào ServiceNow, tìm kiếm thủ công mất rất nhiều thời gian. 

Bài toán này sẽ được giải quyết triệt để với workflow n8n cực kỳ thông minh do Angel Menendez thiết kế. Workflow này cho phép các sếp mở một cửa sổ **Popup Modal trực tiếp ngay trong Slack**, nhập các tiêu chí lọc (độ ưu tiên, trạng thái) và ngay lập tức nhận về danh sách 5 sự cố mới nhất dưới định dạng Block Kit cực kỳ chuyên nghiệp – gửi thẳng vào kênh Slack chung hoặc tin nhắn cá nhân (DM) mà không cần rời khỏi ứng dụng chat!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian**: Tra cứu sự cố ServiceNow ngay trong Slack chỉ với vài cú click chuột.
- **Tương tác mượt mà**: Sử dụng Slack Modal và Block Kit để hiển thị thông tin trực quan, đẹp mắt.
- **Linh hoạt đầu ra**: Tự động nhận diện chọn kênh hay gửi tin nhắn riêng (DM) tùy theo lựa chọn của người dùng.
- **Hoạt động tự động 24/7**: Xử lý hàng đợi sự cố liên tục, không bỏ sót thông tin quan trọng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Slack App / Workspace** có quyền cấu hình Webhook, Slash Commands và API truy cập Slack (`slackApi` credentials).
- **ServiceNow Instance** với tài khoản quản trị hoặc API có quyền đọc thông tin Incident (`serviceNowBasicApi` credentials).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy toàn bộ mã nguồn JSON từ trang quản lý n8n.
- Mở n8n Editor, chọn **Add workflow** -> **Import from JSON** và dán đoạn mã vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống liên lạc thông suốt giữa Slack và ServiceNow, các sếp cần chú ý cấu hình các node sau:
- **Node Webhook**: Lấy URL webhook endpoint được cung cấp bởi n8n sau khi active workflow và cấu hình vào Slack App Event Subscriptions / Slash Command.
- **Node ServiceNow**: Cấu hình credentials (`serviceNowBasicApi`) với thông tin domain, username và password của hệ thống ServiceNow doanh nghiệp.
- **Node ServiceNow Modal**, **Slack Nodes** (`Channel - Send Matching Incidents`, `DM - Send Matching Incidents`, v.v.): Chọn đúng credentials (`slackApi`) được cấp quyền tương tác với Slack Workspace.

#### 3. Kích hoạt ⚡️
- Thực hiện test thử bằng cách gọi lệnh Slack Modal hoặc gửi sự kiện mẫu qua Webhook node để kiểm tra luồng dữ liệu.
- Bật công tắc **Active** ở góc trên cùng bên phải để đưa workflow vào vận hành chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm thông báo khẩn**: Kết hợp thêm node Telegram hoặc MS Teams để bắn cảnh báo khi có sự cố Priority 1 (P1) mới xuất hiện.
- **Lưu log vào Google Sheets**: Thêm bước lưu lại lịch sử tra cứu của nhân viên để dễ dàng thống kê và kiểm toán nội bộ.
- **Tùy chỉnh giới hạn**: Thay đổi thông số ở node `Retain First 5 Incidents` nếu các sếp muốn hiển thị nhiều hơn (hoặc ít hơn) 5 sự cố gần nhất.

### 📌 Kết luận
Workflow này là một "vũ khí" tuyệt vời giúp tối ưu hóa quy trình vận hành CNTT (ITSM), mang lại trải nghiệm làm việc liền mạch cho đội ngũ kỹ thuật ngay trên không gian chat quen thuộc. Áp dụng ngay để tăng tốc độ phản hồi sự cố cho doanh nghiệp các sếp nhé!