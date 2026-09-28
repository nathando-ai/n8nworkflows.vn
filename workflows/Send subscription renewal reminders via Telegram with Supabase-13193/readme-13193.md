---
title: "🚀 Tự động nhắc nhở gia hạn dịch vụ qua Telegram với Supabase - Workflow n8n hoàn chỉnh"
description: "Hướng dẫn chi tiết cách tự động gửi thông báo nhắc nhở gia hạn dịch vụ qua Telegram khi đến hạn, sử dụng Supabase để quản lý dữ liệu và n8n để tự động hóa quy trình."
slug: "tu-dong-nhac-nho-gia-han-dich-vu-qua-telegram-voi-supabase"
tags: [n8n, automation, no-code, Telegram, Supabase]
keywords: [n8n workflow, tự động hóa, nhắc nhở gia hạn, Telegram, Supabase]
---

# 🚀 Tự động nhắc nhở gia hạn dịch vụ qua Telegram với Supabase - Workflow n8n hoàn chỉnh

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động gửi thông báo nhắc nhở gia hạn dịch vụ qua Telegram khi đến hạn.
- Quản lý dữ liệu gia hạn dịch vụ hiệu quả với Supabase.
- Tiết kiệm thời gian và công sức cho nhân viên.
- Đảm bảo không bỏ sót bất kỳ khách hàng nào cần gia hạn.
- Nhận phản hồi và xử lý lỗi một cách tự động.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Supabase với URL và Service Role Key.
- Tài khoản Telegram và Token của bot Telegram.
- API Key bí mật để xác thực webhook.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn.
2. Nhấn vào nút "Import from URL" và dán link sau: [https://n8n.io/workflows/13193](https://n8n.io/workflows/13193).
3. Hoặc tải file JSON về và import từ máy tính.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Webhook Trigger**:
   - Đảm bảo đường dẫn là `subscription-renewal` và phương thức là `POST`.

2. **Extract API Key**:
   - Không cần cấu hình gì thêm.

3. **Authorized?**:
   - Thay thế `{{YOUR_SECRET_KEY}}` bằng API Key bí mật của bạn.
   - Đảm bảo truyền API Key qua header `x-api-key` khi gọi webhook.

4. **Fetch Subscriptions**:
   - Cấu hình credentials Supabase với URL và Service Role Key của bạn.
   - Đảm bảo bảng `subscriptions` có các cột: `customer_id`, `customer_name`, `telegram_chat_id`, `expiry_date`.

5. **Calculate Days**:
   - Không cần cấu hình gì thêm.

6. **Expiring Soon?**:
   - Không cần cấu hình gì thêm.

7. **Create Telegram Message**:
   - Không cần cấu hình gì thêm.

8. **Send Telegram Reminder**:
   - Cấu hình credentials Telegram với Token của bot Telegram.
   - Đảm bảo `telegram_chat_id` trong bảng `subscriptions` là hợp lệ.

9. **Telegram Sent?**:
   - Không cần cấu hình gì thêm.

10. **Prepare Reminder Log**:
    - Không cần cấu hình gì thêm.

11. **Insert Reminder Log**:
    - Đảm bảo bảng `renewal_reminders` đã được tạo trong Supabase.

12. **Compose Success Response**:
    - Không cần cấu hình gì thêm.

13. **Respond to Webhook**:
    - Không cần cấu hình gì thêm.

14. **Compose Error Response**:
    - Không cần cấu hình gì thêm.

15. **Insert Error Log**:
    - Đảm bảo bảng `workflow_errors` đã được tạo trong Supabase.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack để nhận thông báo lỗi và thành công.
- Lưu log chi tiết vào Google Sheets hoặc CSV.
- Gửi báo cáo định kỳ về số lượng thông báo đã gửi và tỷ lệ thành công.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa việc gửi thông báo nhắc nhở gia hạn dịch vụ qua Telegram, tiết kiệm thời gian và công sức cho nhân viên. Đảm bảo không bỏ sót bất kỳ khách hàng nào cần gia hạn và nhận phản hồi một cách tự động. Hãy áp dụng ngay để tối ưu hóa quy trình quản lý dịch vụ của bạn!