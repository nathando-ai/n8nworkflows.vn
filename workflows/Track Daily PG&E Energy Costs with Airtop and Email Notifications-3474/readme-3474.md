---
title: "💡 Theo dõi chi phí năng lượng hàng ngày của PG&E với Airtop và thông báo qua Email"
description: "Tự động hóa việc theo dõi chi phí năng lượng hàng ngày từ PG&E và nhận thông báo qua email với workflow n8n này. Giảm thiểu công việc thủ công và nhận dữ liệu cập nhật một cách chính xác và kịp thời."
slug: "theo-doi-chi-phi-nang-luong-pge-airtop-email"
tags: [n8n, automation, no-code, ai, energy, pg&e]
keywords: [n8n workflow, tự động hóa, theo dõi năng lượng, pg&e, airtop]
---

# 💡 Theo dõi chi phí năng lượng hàng ngày của PG&E với Airtop và thông báo qua Email

[Các sếp đang làm việc thủ công để theo dõi chi phí năng lượng hàng ngày từ PG&E? Hãy để workflow n8n này tự động hóa quy trình này cho các sếp. Với workflow này, các sếp sẽ nhận được thông báo email hàng ngày với chi tiết về chi phí năng lượng, bao gồm cả điện và khí tự nhiên, một cách chính xác và kịp thời.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần phải truy cập trang web PG&E hàng ngày để kiểm tra chi phí.
- **Chính xác**: Dữ liệu được trích xuất một cách tự động và chính xác từ trang web.
- **Cá nhân hóa**: Thông báo email được định dạng rõ ràng và dễ đọc.
- **Hoạt động liên tục**: Workflow chạy tự động hàng ngày, đảm bảo các sếp luôn nhận được thông tin cập nhật.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản PG&E hợp lệ.
- Tài khoản Gmail để nhận thông báo.
- Airtop API key để sử dụng các tính năng tương tác và trích xuất dữ liệu.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor.
2. Nhấn vào nút "Import from URL" và nhập URL: [https://n8n.io/workflows/3474](https://n8n.io/workflows/3474).
3. Hoặc copy/paste nội dung JSON từ file workflow vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Schedule Trigger**:
   - Cấu hình thời gian chạy workflow hàng ngày (ví dụ: 8:00 AM).

2. **Type username**:
   - Nhập tên người dùng của tài khoản PG&E vào trường `text`.

3. **Type password**:
   - Nhập mật khẩu của tài khoản PG&E vào trường `text`.

4. **Variables**:
   - Cấu hình các biến cần thiết cho workflow (ví dụ: URL trang web PG&E).

5. **Extract Costs**:
   - Đảm bảo rằng prompt trích xuất dữ liệu được cấu hình đúng để trích xuất chi phí năng lượng hàng ngày.

6. **Send email**:
   - Cấu hình tài khoản Gmail để gửi thông báo.
   - Điền địa chỉ email người nhận vào trường `to`.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng.
- Bật Active workflow để chạy tự động hàng ngày.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Telegram**: Thêm node để gửi thông báo qua Slack hoặc Telegram thay vì email.
- **Lưu log**: Thêm node để lưu log các hoạt động của workflow để theo dõi và kiểm tra.
- **Gửi báo cáo định kỳ**: Cấu hình workflow để gửi báo cáo chi phí năng lượng hàng tháng hoặc hàng quý.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa việc theo dõi chi phí năng lượng hàng ngày từ PG&E và nhận thông báo qua email một cách chính xác và kịp thời. Hãy áp dụng ngay để tiết kiệm thời gian và giảm thiểu công việc thủ công!