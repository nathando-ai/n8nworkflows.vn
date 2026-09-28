---
title: "🚀 Tự động chào mừng thành viên mới vào nhóm WhatsApp với Evolution API"
description: "Hướng dẫn tự động hóa gửi tin nhắn chào mừng thành viên mới vào nhóm WhatsApp bằng n8n và Evolution API, tiết kiệm thời gian và tạo trải nghiệm thân thiện hơn cho cộng đồng."
slug: "tu-dong-chao-mung-thanh-vien-moi-whatsapp-evolution-api"
tags: [n8n, automation, no-code, whatsapp, social-media]
keywords: [n8n workflow, tự động hóa, whatsapp group, evolution api, tin nhắn chào mừng]
---

# 🚀 Tự động chào mừng thành viên mới vào nhóm WhatsApp với Evolution API

[Các sếp đang gặp khó khăn khi phải chào mừng từng thành viên mới vào nhóm WhatsApp một cách thủ công. Với workflow này, các sếp có thể tự động hóa quy trình này hoàn toàn, tạo trải nghiệm thân thiện hơn cho cộng đồng và tiết kiệm thời gian quý giá.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian chào mừng thành viên mới
- Tạo trải nghiệm thân thiện và chuyên nghiệp cho cộng đồng
- Tự động hóa hoàn toàn quy trình chào mừng
- Tăng tương tác và gắn kết cộng đồng
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Evolution API (self-hosted hoặc cloud)
- WhatsApp Business đã kết nối với Evolution API
- Quyền quản trị viên nhóm WhatsApp
- API Key của Evolution API
- URL webhook của Evolution API
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấn vào nút "Import from URL" và dán link sau: [https://n8n.io/workflows/6462](https://n8n.io/workflows/6462)
3. Hoặc tải file JSON về máy và import từ file

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Webhook - Receive Group Events**:
   - Đảm bảo đường dẫn là "whatsapp-group-welcome"
   - Phương thức HTTP là POST

2. **Set Variables - Configure Here**:
   - Cập nhật các biến sau với thông tin của bạn:
     - `EVOLUTION_API_URL`: URL của Evolution API instance
     - `EVOLUTION_API_KEY`: API Key của Evolution API
     - `TARGET_GROUP_ID`: ID của nhóm WhatsApp cần theo dõi
     - `WELCOME_MESSAGE`: Nội dung tin nhắn chào mừng (có thể chứa biến như `{{name}}` để cá nhân hóa)

3. **Filter - Check if Target Group**:
   - Node này sẽ kiểm tra xem sự kiện xảy ra trong nhóm mục tiêu hay không

4. **If - New Member Joined**:
   - Node này sẽ xác nhận xem có thành viên mới tham gia nhóm hay không

5. **Wait - Natural Delay**:
   - Thiết lập thời gian chờ (ví dụ: 5-10 giây) để tạo cảm giác tự nhiên

6. **Send Welcome Message**:
   - Node này sẽ gửi tin nhắn chào mừng thông qua Evolution API

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong, nhấn vào nút "Activate" để kích hoạt workflow
2. Thử nghiệm bằng cách mời một thành viên mới vào nhóm WhatsApp của bạn

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node để lưu log các tin nhắn đã gửi
- Kết hợp với Slack/Telegram để nhận thông báo khi có thành viên mới
- Cá nhân hóa tin nhắn chào mừng dựa trên vai trò của thành viên
- Thêm chức năng gửi tin nhắn định kỳ cho thành viên mới

### 📌 Kết luận
Với workflow này, các sếp có thể tự động hóa hoàn toàn việc chào mừng thành viên mới vào nhóm WhatsApp, tạo trải nghiệm thân thiện và chuyên nghiệp cho cộng đồng. Hãy áp dụng ngay để tiết kiệm thời gian và tăng tương tác cộng đồng!