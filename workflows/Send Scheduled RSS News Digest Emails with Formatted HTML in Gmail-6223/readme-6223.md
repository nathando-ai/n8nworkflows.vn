---
title: "📰 Tự động hóa gửi email tổng hợp tin tức RSS hàng ngày với HTML đẹp mắt"
description: "Hướng dẫn chi tiết cách tự động hóa gửi email tổng hợp tin tức từ RSS hàng ngày với định dạng HTML đẹp mắt sử dụng n8n và Gmail"
slug: "tu-dong-hoa-gui-email-tong-hop-tin-tuc-rss-hang-ngay"
tags: [n8n, automation, no-code, rss, gmail]
keywords: [n8n workflow, tự động hóa tin tức, email tự động hóa, rss feed, gmail api]
---

# 📰 Tự động hóa gửi email tổng hợp tin tức RSS hàng ngày với HTML đẹp mắt

[Các sếp] có biết không? Với lượng tin tức ngày càng tăng, việc phải theo dõi và đọc từng bài viết một cách thủ công thật là tốn thời gian và dễ bị bỏ sót thông tin quan trọng. Với workflow này, các sếp có thể tự động hóa việc thu thập tin tức từ RSS feed, định dạng chúng thành email đẹp mắt và gửi hàng ngày một cách tự động.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần phải theo dõi tin tức hàng ngày một cách thủ công.
- **Thông tin cập nhật kịp thời**: Nhận tổng hợp tin tức quan trọng hàng ngày qua email.
- **Định dạng đẹp mắt**: Tin tức được trình bày với định dạng HTML đẹp mắt, dễ đọc.
- **Tự động hóa hoàn toàn**: Quá trình thu thập, định dạng và gửi email hoàn toàn tự động.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Gmail để gửi email.
- Quyền truy cập vào RSS feed của trang tin tức mong muốn (ví dụ: prothomalo.com).
- Tạo và cấu hình OAuth2 cho Gmail trong n8n.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn.
2. Nhấn vào nút "Import from URL" và nhập URL sau: [https://n8n.io/workflows/6223](https://n8n.io/workflows/6223).
3. Hoặc, tải file JSON từ liên kết trên và import vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Schedule Trigger**:
   - Cấu hình thời gian gửi email hàng ngày (ví dụ: 8:00 AM mỗi ngày).
   - Để cấu hình, nhấn vào node "Schedule Trigger" và chọn "Add Schedule".

2. **HTTP Request**:
   - Thay đổi URL RSS feed nếu cần (ví dụ: từ prothomalo.com sang trang tin khác).
   - Để cấu hình, nhấn vào node "Get RSS from Prothom Alo" và thay đổi URL trong phần "URL".

3. **Send a message (Gmail)**:
   - Cấu hình thông tin email (người gửi, người nhận, tiêu đề).
   - Đảm bảo đã tạo và cấu hình OAuth2 cho Gmail trong n8n.
   - Để cấu hình, nhấn vào node "Send a message" và chọn "Add Credential" nếu chưa có.

#### 3. Kích hoạt ⚡️
1. **Test run dữ liệu mẫu**:
   - Nhấn vào nút "Execute Workflow" để kiểm tra workflow với dữ liệu mẫu.
2. **Bật Active workflow**:
   - Sau khi kiểm tra thành công, nhấn vào nút "Activate" để kích hoạt workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm nhiều nguồn tin tức**: Kết nối với nhiều RSS feed khác nhau để có được tổng hợp tin tức đa dạng hơn.
- **Tùy chỉnh định dạng email**: Sửa đổi mã HTML trong node "Generate HTML News Preview" để phù hợp với phong cách và yêu cầu của các sếp.
- **Gửi báo cáo định kỳ**: Thay đổi tần suất gửi email từ hàng ngày sang hàng tuần hoặc hàng tháng.
- **Kết hợp với Slack/Telegram**: Thêm node để gửi thông báo qua Slack hoặc Telegram khi có tin tức quan trọng.

### 📌 Kết luận
Với workflow này, các sếp có thể tự động hóa việc thu thập và gửi tin tức hàng ngày một cách dễ dàng và chuyên nghiệp. Hãy áp dụng ngay để tiết kiệm thời gian và nhận thông tin cập nhật kịp thời!