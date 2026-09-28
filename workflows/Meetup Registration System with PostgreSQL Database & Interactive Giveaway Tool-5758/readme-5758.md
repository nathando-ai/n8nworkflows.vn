---
title: "🚀 Xây dựng Hệ thống Đăng ký Meetup & Mini-game Quay số trúng thưởng tự động với n8n & PostgreSQL"
description: "Tự động hóa toàn bộ quy trình đăng ký sự kiện Meetup, lưu trữ dữ liệu vào PostgreSQL và tích hợp ứng dụng quay số trúng thưởng (Giveaway) trực tiếp qua n8n."
slug: "he-thong-dang-ky-meetup-va-quay-so-tu-dong-n8n"
tags: [n8n, automation, postgresql, no-code, event-management, webhook]
keywords: [n8n workflow, tự động hóa meetup, quản lý sự kiện n8n, quay số trúng thưởng tự động, postgresql n8n]
---

# 🚀 Tự động hóa Hệ thống Đăng ký Meetup & Quay số trúng thưởng (Giveaway) với n8n

Việc quản lý đăng ký sự kiện Meetup, workshop hay hội thảo thủ công thường khiến ban tổ chức đau đầu: dữ liệu rải rác, nhập liệu dễ sai sót, và việc chuẩn bị danh sách quay số trúng thưởng (giveaway) vừa mất thời gian lại lo ngại vấn đề bảo mật thông tin cá nhân của người tham gia.

Giải pháp? Workflow n8n này sẽ tự động hóa toàn bộ quy trình từ khâu thu thập thông tin qua Form, lưu trữ an toàn vào database PostgreSQL, cho đến việc cung cấp một ứng dụng Mini-game quay số trực tiếp cực kỳ chuyên nghiệp ngay trên trình duyệt mà không cần code phức tạp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100% khâu đăng ký:** Người tham gia điền form, dữ liệu tự động lưu gọn gàng vào PostgreSQL mà không cần đụng tay.
- **Bảo mật thông tin cá nhân:** Tự động ẩn bớt số điện thoại (masking) và mã hóa dữ liệu trước khi hiển thị lên màn hình quay số.
- **Minh họa trực quan tại sự kiện:** Tích hợp sẵn giao diện Webhook hiển thị danh sách và chọn người trúng thưởng ngẫu nhiên trực tiếp trên màn hình lớn.
- **Vận hành trơn tru:** Chống trùng lặp dữ liệu nhờ tính năng Upsert thông minh của database.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Self-hosted hoặc Cloud).
- **Cơ sở dữ liệu PostgreSQL:** Đã có sẵn một database để lưu thông tin người tham gia (bảng chứa các trường như `nama_lengkap`, `email`, `whatsapp`, `discord_username`).
- **Credentials:** Thông tin kết nối PostgreSQL (`postgres` credentials trong n8n).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này từ kho lưu trữ n8n (ID: 5758) hoặc copy/paste trực tiếp JSON vào trình soạn thảo n8n của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 2 luồng chính được kết nối chặt chẽ với nhau:

*   **Luồng 1: Đăng ký thông tin (Registration Flow)**
    - **Participant Form (`formTrigger`):** Node kích hoạt khi có người điền form. Các sếp có thể tùy chỉnh các trường như họ tên, email, số điện thoại, tài khoản Discord...
    - **Mapping Form to Database (`set`):** Node chuẩn hóa dữ liệu đầu vào trước khi lưu trữ.
    - **Save Participant to Database (`postgres`):** Cấu hình đúng credentials PostgreSQL và chọn bảng lưu trữ. Node này sử dụng thao tác *upsert* để tự động cập nhật nếu thông tin đã tồn tại, tránh trùng lặp.
    - **Thank you screen (`form`):** Hiển thị lời cảm ơn sau khi đăng ký thành công.

*   **Luồng 2: Ứng dụng Giveaway (Giveaway App)**
    - **Giveaway App (`webhook`):** Endpoint công khai (`/giveaway`) phục vụ giao diện trình duyệt.
    - **Get all participants (`postgres`):** Truy vấn toàn bộ danh sách người tham gia từ database.
    - **Format participant list (`code`):** Node JavaScript xử lý ẩn bớt thông tin nhạy cảm (ví dụ che số WhatsApp) và mã hóa ID bằng Base64 để đảm bảo tính riêng tư.
    - **Respond to Giveaway App (`respondToWebhook`):** Trả về giao diện Single Page Application (HTML/JS) trực quan để ban tổ chức bấm nút quay số ngẫu nhiên trực tiếp tại sự kiện.

#### 3. Kích hoạt ⚡️
- Chạy thử (Test run) luồng form đăng ký và kiểm tra dữ liệu trong PostgreSQL.
- Test truy cập URL webhook của Giveaway App để đảm bảo giao diện quay số hiển thị mượt mà.
- Bật công tắc **Active** để đưa hệ thống vào vận hành thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Telegram/Slack:** Thêm node gửi thông báo về nhóm chat nội bộ mỗi khi có người đăng ký thành công sự kiện.
- **Gửi Email Xác Nhận:** Kết nối thêm node gửi email (Gmail/SMTP) tự động gửi vé tham dự hoặc mã QR check-in cho người đăng ký ngay sau khi submit form.
- **Lưu lịch sử trúng thưởng:** Mở rộng database để ghi nhận lịch sử những ai đã trúng giải trong mini-game, tránh việc một người trúng nhiều lần.

### 📌 Kết luận
Với hệ thống tự động hóa này, các sếp vừa tiết kiệm được hàng giờ đồng hồ quản lý thủ công, vừa mang lại trải nghiệm chuyên nghiệp, công bằng và đầy hứng khởi cho người tham gia sự kiện. Lên đồ và áp dụng ngay thôi nào!