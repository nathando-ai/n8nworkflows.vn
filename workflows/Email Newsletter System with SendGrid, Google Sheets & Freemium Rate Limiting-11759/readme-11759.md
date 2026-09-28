---
title: "🚀 Xây dựng hệ thống Email Newsletter tự động với SendGrid, Google Sheets và giới hạn Freemium Rate Limiting"
description: "Hướng dẫn thiết lập workflow n8n tự động hóa gửi email newsletter, quản lý người dùng qua Google Sheets, tích hợp giới hạn 5 email miễn phí mỗi ngày và thông báo Telegram."
slug: "he-thong-email-newsletter-sendgrid-google-sheets-rate-limiting"
tags: [n8n, automation, sendgrid, google-sheets, telegram, email-marketing]
keywords: [n8n workflow, tự động hóa email, sendgrid n8n, google sheets n8n, rate limiting email]
---

# 🚀 Xây dựng hệ thống Email Newsletter tự động với SendGrid, Google Sheets và Rate Limiting

Các sếp đang vận hành một dịch vụ newsletter hoặc công cụ tạo email nhưng đau đầu vì bị người dùng spam, hoặc muốn cung cấp gói dùng thử (Freemium) giới hạn số lượng email gửi mỗi ngày? Việc quản lý thủ công ai được dùng mấy lượt, ai là tài khoản Pro vừa tốn thời gian lại dễ sai sót. 

Đừng lo, bài viết này sẽ hướng dẫn các sếp triển khai một hệ thống tự động hóa 100% bằng n8n, giúp xử lý yêu cầu từ trang web, phân loại người dùng (Pro/Demo), kiểm tra giới hạn 5 email miễn phí mỗi ngày, cập nhật cơ sở dữ liệu trên Google Sheets, gửi email qua SendGrid và thậm chí bắn thông báo về Telegram cho các sếp. Tất cả diễn ra trong tích tắc mà không cần viết một dòng code phức tạp nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Nhận request từ trang web, xử lý và phản hồi ngay lập tức cho người dùng.
- **Bảo vệ tài nguyên (Rate Limiting):** Tự động chặn và thông báo khi người dùng dùng thử (Demo) vượt quá giới hạn 5 email/ngày.
- **Quản lý dữ liệu thông minh:** Tự động lưu thông tin người dùng mới và cập nhật số lượng gửi vào Google Sheets.
- **Giám sát thời gian thực:** Nhận thông báo tức thì qua Telegram mỗi khi có hoạt động mới diễn ra trên hệ thống.
:::

### 📦 Tài nguyên chuẩn bị từ tác giả Gilbert Onyebuchi
Trước khi bắt đầu, các sếp nhớ chuẩn bị sẵn 2 tài nguyên quan trọng sau từ tác giả:
- 📄 [Tải Webform Email Newsletter](https://drive.google.com/file/d/1ZipYXImNi8JbwnekzphqHoFKf5Qbhu6g/view?usp=sharing)
- 📊 [Tải Google Sheet Template](https://docs.google.com/spreadsheets/d/1JvsOzkCaJzJN8-x1hldFA-H6iPc0A9MH-mVYBCEWtJw/edit?usp=sharing)

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ TRƯỚC KHI "LÊN ĐỒ"]
- **Tài khoản n8n** (Cloud hoặc Self-hosted VPS).
- **Google Sheets API Credentials** (OAuth2) để đọc/ghi dữ liệu người dùng.
- **Tài khoản SendGrid** và API Key để gửi email (Pro & Demo).
- **Telegram Bot Token và Chat ID** để nhận thông báo.
:::

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Các sếp copy mã JSON của workflow này (hoặc tải file JSON từ n8n template #11759).
- Trong giao diện n8n Editor, bấm vào góc trên bên phải chọn **Import from File** hoặc dán trực tiếp JSON vào workspace.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 15 nodes được thiết kế chặt chẽ. Các sếp cần cấu hình kỹ các điểm sau:

- **Webhook1**: Node nhận dữ liệu từ trang web gửi tới. Hãy copy URL của webhook này và dán vào mã nguồn của Webform đã tải ở phần chuẩn bị.
- **Google Sheets Read**, **Create New User1**, **Update User Count1**: Kết nối với tài khoản Google Sheets của các sếp (sử dụng Google Sheets OAuth2 API). Trỏ đến file Google Sheet Template đã chuẩn bị, cấu hình đúng Sheet Name và các cột dữ liệu tương ứng.
- **Send Email (Pro)** & **Send Email (Demo)1**: Chọn credentials của SendGrid. Cấu hình địa chỉ người gửi (Sender Email) và nội dung template email phù hợp cho từng đối tượng.
- **Telegram Notification1**: Cấu hình credentials của Telegram Bot để hệ thống tự động bắn tin nhắn báo cáo về máy các sếp.
- **Check Mode1**, **Check User Exists1**, **Can Send?1**, **Check Limit Logic**, **Check User Exists2**: Các node logic và code (JavaScript) sẽ tự động chạy toán tử kiểm tra hạn mức 5 email/ngày cho tài khoản Demo. Các sếp không cần sửa code bên trong trừ khi muốn thay đổi hạn mức (mặc định là số `5`).

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và thử gửi một request giả lập từ webform để kiểm tra luồng dữ liệu.
- Sau khi test thành công, gạt công tắc sang **Active** để hệ thống chính thức hoạt động 24/7.

---

### ✍️ Mẹo & gợi ý nâng cao
Để hệ thống xịn sò hơn nữa, các sếp có thể mở rộng workflow này với các ý tưởng sau:
1. **Mở rộng kênh thông báo:** Thay vì chỉ gửi Telegram, có thể kết hợp thêm node Slack hoặc Discord để đội ngũ chăm sóc khách hàng cùng nắm tình hình.
2. **Lưu log lỗi:** Thêm nhánh Error Trigger để bắt lỗi nếu SendGrid lỗi hoặc Google Sheets mất kết nối, tự động gửi cảnh báo về Telegram.
3. **Nâng cấp gói cước tự động:** Kết hợp thêm cổng thanh toán (Stripe / PayPal) để khi khách hàng thanh toán Pro, webhook tự động cập nhật trạng thái `Pro` vào Google Sheets mà không cần thao tác tay.

---

### 📌 Kết luận
Hệ thống Email Newsletter tích hợp Rate Limiting này là giải pháp hoàn hảo cho các solopreneur và đội ngũ marketing muốn vận hành một công cụ freemium chuyên nghiệp, tiết kiệm chi phí nhưng cực kỳ hiệu quả. Hãy cài đặt ngay lên VPS của các sếp để tối ưu hóa quy trình ngay hôm nay!