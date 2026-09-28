---
title: "🚀 Tự động đồng bộ danh sách đăng ký nhận tin từ Squarespace sang Mailchimp qua Google Sheets"
description: "Hướng dẫn chi tiết cách tự động hóa quá trình đồng bộ danh sách đăng ký nhận tin từ Squarespace sang Mailchimp thông qua Google Sheets, giúp tiết kiệm thời gian và tránh lỗi thủ công."
slug: "tu-dong-dong-bo-danh-sach-dang-ky-nhan-tin-squarespace-sang-mailchimp-qua-google-sheets"
tags: [n8n, automation, no-code, Squarespace, Mailchimp, Google Sheets]
keywords: [n8n workflow, tự động hóa, Squarespace, Mailchimp, Google Sheets]
---

# 🚀 Tự động đồng bộ danh sách đăng ký nhận tin từ Squarespace sang Mailchimp qua Google Sheets

[Các sếp đang gặp khó khăn khi phải thủ công nhập danh sách đăng ký nhận tin từ Squarespace vào Mailchimp. Quá trình này tốn thời gian, dễ gây lỗi và không thể tự động hóa. Workflow này sẽ giúp các sếp tự động hóa toàn bộ quá trình này một cách dễ dàng và chính xác.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Không cần phải thủ công nhập dữ liệu từ Squarespace sang Mailchimp.
- Chính xác: Dữ liệu được đồng bộ tự động, giảm thiểu lỗi nhập liệu.
- Cá nhân hóa: Có thể tùy chỉnh các trường dữ liệu theo nhu cầu của các sếp.
- Hoạt động liên tục: Workflow có thể chạy theo lịch hoặc theo yêu cầu, đảm bảo dữ liệu luôn được cập nhật.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với Google Sheets đã được chia sẻ cho n8n.
- Tài khoản Mailchimp với API key và ID của danh sách (Audience) cần đồng bộ.
- Google Sheets mẫu đã được chuẩn bị theo [hướng dẫn](https://docs.google.com/spreadsheets/d/1wi2Ucb4b35e0-fuf-96sMnyzTft0ADz3MwdE_cG_WnQ/edit?usp=sharing).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor.
2. Nhấn vào nút "Import from URL" và nhập URL: `https://n8n.io/workflows/3251`.
3. Hoặc, tải file JSON từ [đây](https://n8n.io/workflows/3251) và import vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Squarespace newsletter submissions"**:
   - Chọn credentials là `googleSheetsOAuth2Api`.
   - Nhập ID của Google Sheet chứa danh sách đăng ký nhận tin từ Squarespace.
   - Đảm bảo các cột trong Google Sheet phù hợp với định dạng: `Submitted On`, `Email Address`, `Name`.

2. **Node "Add new member to Mailchimp"**:
   - Chọn credentials là `mailchimpApi`.
   - Nhập ID của danh sách (Audience) trong Mailchimp cần đồng bộ.
   - Cấu hình các trường dữ liệu phù hợp với các cột trong Google Sheet.

#### 3. Kích hoạt ⚡️
- Nhấn vào nút "Test workflow" để kiểm tra dữ liệu mẫu.
- Sau khi kiểm tra thành công, nhấn vào nút "Activate workflow" để kích hoạt workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Chạy theo lịch**: Cấu hình node "Schedule Trigger" để workflow chạy tự động theo lịch định kỳ.
- **Gửi thông báo**: Kết nối với Slack hoặc Telegram để nhận thông báo khi workflow chạy thành công hoặc thất bại.
- **Lưu log**: Thêm node để lưu log các hoạt động của workflow để theo dõi và kiểm tra sau này.
- **Tùy chỉnh dữ liệu**: Sử dụng node "Function" để tùy chỉnh dữ liệu trước khi gửi sang Mailchimp.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quá trình đồng bộ danh sách đăng ký nhận tin từ Squarespace sang Mailchimp một cách dễ dàng và chính xác. Hãy áp dụng ngay để tiết kiệm thời gian và giảm thiểu lỗi thủ công!