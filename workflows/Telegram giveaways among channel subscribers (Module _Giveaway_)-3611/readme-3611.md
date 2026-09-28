---
title: "🎁 Tự động hóa Quay số may mắn Telegram cho thành viên kênh - Workflow n8n"
description: "Hướng dẫn chi tiết cách tự động hóa chương trình quay số may mắn trên Telegram cho thành viên kênh, tiết kiệm thời gian và tăng tương tác"
slug: "tu-dong-hoa-quay-so-may-man-telegram"
tags: [n8n, automation, no-code, telegram, marketing]
keywords: [n8n workflow, tự động hóa, telegram, marketing, giveaway]
---

# 🎁 Tự động hóa Quay số may mắn Telegram cho thành viên kênh - Workflow n8n

[Các sếp đang làm thủ công chương trình quay số may mắn trên Telegram?] Hãy để workflow này giúp các sếp tự động hóa hoàn toàn quy trình từ đăng ký đến chọn người trúng thưởng, tiết kiệm thời gian và tăng tương tác với cộng đồng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa hoàn toàn quy trình quay số may mắn
- Tiết kiệm thời gian quản lý chương trình
- Tăng tương tác với thành viên kênh
- Đảm bảo tính công bằng trong việc chọn người trúng thưởng
- Hoạt động liên tục 24/7 không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Telegram với quyền quản trị kênh
- API Token từ BotFather của Telegram
- Cơ sở dữ liệu PostgreSQL để lưu trữ thông tin
- Các sếp cần chuẩn bị thông tin về các kênh Telegram sẽ tham gia chương trình
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể import workflow này từ file JSON hoặc copy/paste JSON vào n8n Editor. Để import từ file JSON:

1. Truy cập vào n8n Editor
2. Nhấn vào nút "Import from File" trên thanh công cụ
3. Chọn file JSON của workflow
4. Nhấn "Import"

Hoặc copy/paste JSON trực tiếp:

1. Truy cập vào n8n Editor
2. Nhấn vào nút "Import from Clipboard" trên thanh công cụ
3. Dán nội dung JSON của workflow
4. Nhấn "Import"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình các node quan trọng sau:

- **Telegram Trigger**: Cấu hình API Token của bot Telegram
- **Telegram**: Cấu hình API Token của bot Telegram cho tất cả các node Telegram
- **PostgreSQL**: Cấu hình kết nối đến cơ sở dữ liệu PostgreSQL
- **Initialization**: Cấu hình các biến khởi tạo như tên bot, thông điệp chào mừng
- **Welcome message Referal**: Cấu hình thông điệp chào mừng cho người giới thiệu
- **Welcome message Manager**: Cấu hình thông điệp chào mừng cho quản lý chương trình
- **Create Giveaway**: Cấu hình thông điệp và nút bấm cho chương trình quay số
- **Request New Channel**: Cấu hình thông điệp yêu cầu thêm kênh mới
- **SMS for Winner**: Cấu hình thông điệp thông báo cho người trúng thưởng
- **SMS for Manager**: Cấu hình thông điệp thông báo cho quản lý chương trình

#### 3. Kích hoạt ⚡️
Sau khi cấu hình xong, các sếp cần:

1. Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng
2. Bật Active workflow để chạy liên tục
3. Kiểm tra các thông báo trên kênh Telegram để đảm bảo chương trình hoạt động đúng

### ✍️ Mẹo & gợi ý nâng cao
- Các sếp có thể kết hợp với Slack/Telegram để nhận thông báo khi có người tham gia chương trình
- Lưu log các hoạt động để theo dõi hiệu suất chương trình
- Gửi báo cáo định kỳ về số lượng người tham gia và người trúng thưởng
- Tích hợp với các dịch vụ email để gửi thông báo cho người trúng thưởng
- Sử dụng các biến động để tùy chỉnh thông điệp theo từng chương trình

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn chương trình quay số may mắn trên Telegram, tiết kiệm thời gian và tăng tương tác với cộng đồng. Hãy áp dụng ngay để nâng cao trải nghiệm người dùng và tăng doanh thu cho kênh của các sếp!