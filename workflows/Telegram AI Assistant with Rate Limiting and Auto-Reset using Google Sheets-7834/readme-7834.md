---
title: "🤖 Tự động hóa Trợ lý AI Telegram với Giới hạn Tin nhắn và Tự động Reset bằng Google Sheets"
description: "Hướng dẫn chi tiết cách tự động hóa trợ lý AI Telegram với hệ thống giới hạn tin nhắn và tự động reset bằng Google Sheets, giúp quản lý chi phí và tránh lạm dụng."
slug: "tu-dong-hoa-tro-ly-ai-telegram-voi-gioi-han-tin-nhan-va-tu-dong-reset-bang-google-sheets"
tags: [n8n, automation, no-code, telegram, google-sheets, ai-chatbot, langchain]
keywords: [n8n workflow, tự động hóa, trợ lý AI, Telegram, Google Sheets, giới hạn tin nhắn, tự động reset]
---

# 🤖 Tự động hóa Trợ lý AI Telegram với Giới hạn Tin nhắn và Tự động Reset bằng Google Sheets

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Quản lý chi phí hiệu quả**: Giới hạn số lượng tin nhắn mỗi người dùng có thể gửi, giúp kiểm soát chi phí sử dụng AI.
- **Tránh lạm dụng**: Ngăn chặn người dùng gửi tin nhắn quá nhiều, bảo vệ tài nguyên hệ thống.
- **Dễ dàng theo dõi**: Theo dõi số lượng tin nhắn của từng người dùng thông qua Google Sheets.
- **Tự động reset**: Hệ thống tự động reset số lượng tin nhắn sau mỗi khoảng thời gian, cho phép người dùng tiếp tục tương tác.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Telegram và bot token.
- Tài khoản Google và Google Sheets API đã được kích hoạt.
- Azure OpenAI API key (hoặc các API khác nếu sử dụng mô hình AI khác).
- Biết cách tạo và cấu hình các credentials trong n8n.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor.
2. Nhấn vào nút "Import from URL" và dán link: [https://n8n.io/workflows/7834](https://n8n.io/workflows/7834).
3. Hoặc tải file JSON từ link trên và import vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

- **Telegram Trigger**: Cấu hình credentials cho Telegram API và chọn bot của bạn.
- **Google Sheets**: Cấu hình credentials cho Google Sheets API và tạo một bảng tính mới với các cột "ID" và "Message Counter".
- **Azure OpenAI**: Cấu hình credentials cho Azure OpenAI API và chọn mô hình AI phù hợp (ví dụ: gpt-4.1-2).
- **Switch Node**: Chỉnh sửa điều kiện để thay đổi giới hạn số lượng tin nhắn cho mỗi người dùng (mặc định là 3).
- **Schedule Trigger**: Cấu hình lịch reset số lượng tin nhắn (ví dụ: mỗi giờ, mỗi ngày, mỗi tuần).

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng.
- Bật Active workflow để bắt đầu tự động hóa.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Telegram**: Gửi thông báo khi người dùng đạt đến giới hạn tin nhắn.
- **Lưu log**: Thêm node để lưu log các tương tác của người dùng.
- **Gửi báo cáo định kỳ**: Tạo một workflow phụ để gửi báo cáo số lượng tin nhắn mỗi ngày.
- **Tích hợp với các dịch vụ khác**: Kết nối với các dịch vụ khác như Google Drive, Notion để lưu trữ dữ liệu.

### 📌 Kết luận
Workflow này cung cấp một giải pháp toàn diện để quản lý và kiểm soát việc sử dụng trợ lý AI trên Telegram. Với hệ thống giới hạn tin nhắn và tự động reset, các sếp có thể dễ dàng quản lý chi phí và tránh lạm dụng. Hãy thử ngay và tối ưu hóa quy trình của bạn!