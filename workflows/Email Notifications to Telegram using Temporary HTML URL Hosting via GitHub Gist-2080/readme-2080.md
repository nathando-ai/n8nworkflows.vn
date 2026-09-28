---
title: "🚀 Tự động hóa thông báo Email qua Telegram kèm Link xem HTML tạm thời trên GitHub Gist"
description: "Hướng dẫn xây dựng workflow n8n chuyển đổi email đến qua IMAP thành trang web HTML tạm thời trên GitHub Gist và gửi thông báo trực quan tới Telegram."
slug: "tu-dong-hoa-thong-bao-email-qua-telegram-kem-link-html-github-gist"
tags: [n8n, automation, no-code, telegram, github-gist, email-trigger]
keywords: [n8n workflow, tu dong hoa email, telegram notification, github gist api, imap email trigger]
---

# 🚀 Tự động hóa thông báo Email qua Telegram kèm Link xem HTML tạm thời trên GitHub Gist

Các sếp có bao giờ cảm thấy mệt mỏi khi phải liên tục mở hòm thư để kiểm tra các email quan trọng, hay việc đọc nội dung email HTML dài dằng dặc trên điện thoại qua các thông báo văn bản thô trở nên vô cùng khó nhìn? Đừng lo lắng! Với workflow n8n này, mọi email mới đến sẽ được tự động xử lý, biến hóa thành một trang web HTML xem trực tuyến thông qua **GitHub Gist**, sau đó gửi một chiếc thông báo gọn gàng kèm đường link trực tiếp đến **Telegram** của các sếp. Giải pháp tự động hóa 100% không cần code từ *Nskha* sẽ giúp các sếp quản lý email mọi lúc mọi nơi cực kỳ chuyên nghiệp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian tuyệt đối:** Không cần mở ứng dụng Email liên tục, nhận tin ngay lập tức trên Telegram.
- **Trải nghiệm đọc hoàn hảo:** Chuyển đổi nội dung email HTML phức tạp thành một trang web tạm thời sạch sẽ, dễ đọc trên mọi thiết bị.
- **Tự động dọn dẹp thông minh:** Hỗ trợ tính năng chờ và tự động xóa hoặc quản lý tin nhắn thông báo cũ, giữ cho Telegram luôn ngăn nắp.
- **Hoạt động 24/7 bền bỉ:** Tự động bắt sự kiện email đến qua giao thức IMAP bất cứ lúc nào.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Một server n8n đang hoạt động ổn định.
- **Tài khoản Email (IMAP):** Thông tin kết nối IMAP (Host, Port, Username, App Password) của Gmail, Outlook hoặc các nhà cung cấp khác.
- **Tài khoản Telegram & Bot:** Tạo một Telegram Bot qua `@BotFather` và lấy **Bot Token**, cùng với **Chat ID** của các sếp hoặc nhóm chat.
- **Tài khoản GitHub:** Tạo một Personal Access Token (PAT) có quyền tạo Gist để workflow có thể xuất file HTML tự động.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần tải file JSON của workflow này, sau đó vào n8n Editor chọn **Add workflow** -> **Import from File** (hoặc copy toàn bộ JSON và dán trực tiếp vào màn hình làm việc của n8n).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống vận hành trơn tru, các sếp nhớ cấu hình kỹ các node trọng điểm sau:

- **Node `Email Trigger (IMAP)`:** Điền chính xác thông tin cấu hình IMAP của hòm thư doanh nghiệp hoặc cá nhân. Chọn đúng credential để n8n có thể "lắng nghe" email mới đến thời gian thực.
- **Node `Github Gist` (và `Github Gist ‌`):** 
  - Cấu hình credentials sử dụng `Predefined Credential Type` => `GitHub API` (hoặc Header Auth với Personal Access Token).
  - Đảm bảo endpoint API cấu hình đúng định dạng để tạo public/secret Gist chứa nội dung HTML của email.
- **Node `Telegram` & `Telegram ‌`:** 
  - Thêm Telegram Bot Token vào credentials.
  - Tại node gửi tin nhắn, điền chính xác `Chat ID` của các sếp.
  - Node `Telegram ‌` (với operation `deleteMessage`) giúp dọn dẹp hoặc tương tác nâng cao với tin nhắn nếu cần thiết.
- **Node `Wait`:** Điều chỉnh thời gian chờ phù hợp trước khi thực hiện các bước xử lý tiếp theo (nếu áp dụng logic xóa hoặc cập nhật tin nhắn).

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để thử nghiệm gửi một email mẫu và kiểm tra xem Gist có được tạo và Telegram có nhận được thông báo hay không.
- Nếu mọi thứ chạy mượt mà, gạt công tắc sang **Active** để workflow tự động chiến đấu 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng lưu trữ domain riêng:** Các sếp có thể kết hợp host mã nguồn giao diện hiển thị trên GitHub Pages theo hướng dẫn từ tác giả để tạo một trang web xem email mang thương hiệu riêng.
- **Tích hợp thêm kênh chat:** Ngoài Telegram, các sếp có thể duplicate nhánh gửi để đẩy thêm thông báo về Slack hoặc Discord.
- **Lưu log vào Google Sheets:** Thêm một node Google Sheets ở đầu hoặc cuối luồng để lưu trữ lịch sử các email quan trọng đã được xử lý tự động.

### 📌 Kết luận
Workflow chuyển đổi email thành HTML page trên GitHub Gist và bắn thông báo Telegram này là một "vũ khí" cực kỳ lợi hại giúp tối ưu hóa quy trình làm việc, không bỏ lỡ bất kỳ thông tin quan trọng nào. Hãy cài đặt ngay lên hệ thống n8n của các sếp và tận hưởng thành quả tự động hóa nhé!