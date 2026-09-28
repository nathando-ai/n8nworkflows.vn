---
title: "🚀 Tự động cảnh báo task bị kẹt trên Monday.com qua Slack với n8n"
description: "Hướng dẫn xây dựng workflow n8n giúp tự động quét các task bị kẹt (Stuck) trên Monday.com và gửi cảnh báo ngay lập tức qua Slack, giúp tối ưu quản lý dự án."
slug: "tu-dong-canh-bao-task-bi-ket-monday-com-qua-slack"
tags: [n8n, automation, monday, slack, project-management, no-code]
keywords: [n8n workflow, monday.com slack integration, tự động hóa monday, cảnh báo task stuck, quản lý dự án n8n]
keywords: [n8n workflow, tự động hóa, monday.com, slack, quản lý dự án]
---

# 🚀 Tự động cảnh báo task bị kẹt trên Monday.com qua Slack với n8n

Các sếp có đang gặp tình trạng dự án trên Monday.com bị chậm tiến độ chỉ vì các task cứ "treo" ở trạng thái **Stuck** mà không ai hay biết? Việc phải đi kiểm tra thủ công từng board rồi nhắn tin giục nhân sự tốn rất nhiều thời gian và năng lượng.

Đừng lo, trong bài viết này, tôi sẽ hướng dẫn các sếp thiết lập một workflow n8n cực kỳ thông minh (do chuyên gia Robert Breen phát triển) giúp tự động quét các task bị kẹt trên Monday.com và bắn tin nhắn cảnh báo thẳng vào Slack một cách nhanh chóng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Không cần mất công kiểm tra thủ công từng board hay nhóm công việc nữa.
- **Phản ứng nhanh chóng:** Phát hiện ngay các task bị kẹt (Stuck) và nhắc nhở đúng người, đúng thời điểm.
- **Tăng năng suất đội ngũ:** Giúp các sếp và team chủ động xử lý điểm nghẽn, tránh tình trạng "quên việc" làm chậm tiến độ dự án.
- **Hoạt động liên tục:** Có thể dễ dàng chuyển đổi Trigger sang dạng Schedule (lịch trình) để chạy tự động hàng ngày.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một tài khoản **n8n** (Cloud hoặc Self-hosted).
- Tài khoản **Monday.com** với quyền lấy Personal API Token.
- Workspace **Slack** có quyền tạo App và kết nối Bot Token.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ n8n.io (ID: 7737) hoặc sử dụng tính năng copy/paste JSON trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 5 nodes chính hoạt động nhịp nhàng với nhau. Các sếp cần cấu hình kỹ các điểm sau:

- **Node `Get many items1` (Monday.com):** 
  - Tạo Credentials mới loại **Monday.com API**: Vào Monday.com → Admin → API để lấy *Personal API Token* và dán vào n8n.
  - Chọn Board ID và Group ID chứa danh sách task cần theo dõi.
- **Node `Set Columns` (Set):** Dùng để chuẩn hóa dữ liệu các cột, giúp lọc trạng thái chính xác hơn.
- **Node `Filter for Stuck Items` (Filter):** Thiết lập điều kiện lọc chỉ lấy các task có trạng thái (`Status`) bằng giá trị `"Stuck"`.
- **Node `Alert Team` (Slack):**
  - Tạo một Slack App tại [api.slack.com/apps](https://api.slack.com/apps).
  - Thêm các OAuth Scopes: `chat:write`, `channels:read`, `groups:read`, `users:read`.
  - Cài đặt App vào Workspace và lấy **Bot User OAuth Token**.
  - Trong n8n, tạo Credentials **Slack OAuth2 API** và chọn kênh (`channel`) hoặc người nhận (`user`) để nhận thông báo cảnh báo.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** (hoặc dùng `When clicking ‘Execute workflow’` trigger) để test thử dữ liệu mẫu xem tin nhắn có bắn về Slack thành công hay không.
- Nếu mọi thứ mượt mà, hãy bật nút **Active** để workflow chính thức hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Đổi Trigger tự động:** Thay vì dùng Manual Trigger, các sếp có thể gắn thêm node **Schedule Trigger** để hệ thống tự động quét task bị kẹt vào mỗi sáng lúc 9:00 AM hàng ngày.
- **Gửi tin nhắn trực tiếp cho Owner:** Dùng thông tin người phụ trách (Assignee) từ Monday.com để map thẳng vào Slack User ID, giúp ping đúng người chịu trách nhiệm.
- **Lưu Log:** Kết nối thêm một node Google Sheets hoặc Airtable để lưu lại lịch sử các lần cảnh báo task bị kẹt phục vụ việc họp đánh giá hiệu suất.

### 📌 Kết luận
Một giải pháp gọn nhẹ nhưng mang lại hiệu quả cực kỳ lớn trong việc quản lý dự án và tối ưu vận hành đội ngũ. Hãy áp dụng ngay vào hệ thống n8n của các sếp để giải quyết dứt điểm tình trạng task bị "ngâm" nhé!