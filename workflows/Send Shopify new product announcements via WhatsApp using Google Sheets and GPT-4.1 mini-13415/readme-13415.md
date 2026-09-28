---
title: "🚀 Tự động thông báo sản phẩm mới Shopify qua WhatsApp với Google Sheets và GPT-4.1 mini"
description: "Hướng dẫn tự động hóa thông báo sản phẩm mới Shopify qua WhatsApp bằng Google Sheets và AI, tiết kiệm thời gian và tăng tương tác khách hàng"
slug: "tu-dong-thong-bao-san-pham-moi-shopify-qua-whatsapp"
tags: [n8n, automation, no-code, Shopify, WhatsApp, Google Sheets, AI]
keywords: [n8n workflow, tự động hóa, Shopify, WhatsApp, Google Sheets, AI, marketing]
---

# 🚀 Tự động thông báo sản phẩm mới Shopify qua WhatsApp với Google Sheets và GPT-4.1 mini

[Các sếp] có biết không? Khi phải thông báo sản phẩm mới cho hàng nghìn khách hàng qua WhatsApp thủ công, bạn sẽ mất bao nhiêu thời gian và công sức? Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình từ khi sản phẩm được tạo đến khi thông báo được gửi đi, chỉ với vài bước cấu hình đơn giản.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa toàn bộ quy trình thông báo sản phẩm mới
- **Tăng tương tác**: Gửi thông báo cá nhân hóa với hình ảnh và mô tả chi tiết
- **Chính xác**: Kiểm tra số điện thoại hợp lệ trước khi gửi
- **Hoạt động liên tục**: Workflow chạy tự động 24/7 mà không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Shopify với quyền truy cập API
- Tài khoản Google với Google Sheets API đã được kích hoạt
- Tài khoản OpenAI với API key cho GPT-4.1 mini
- Tài khoản Rapiwa với API key để gửi tin nhắn WhatsApp
- Danh sách số điện thoại khách hàng trong Google Sheets
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [trang workflow gốc](https://n8n.io/workflows/13415)
2. Click vào nút "Copy to clipboard" để sao chép JSON workflow
3. Trong n8n Editor, click vào "Import from Clipboard" và dán JSON đã sao chép

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Shopify Trigger**:
   - Cấu hình credentials cho Shopify
   - Chọn event "Product Created" để kích hoạt workflow khi có sản phẩm mới

2. **Google Sheets**:
   - Cấu hình credentials cho Google Sheets
   - Điền ID của Google Sheet chứa danh sách số điện thoại khách hàng
   - Đảm bảo cột dữ liệu trong Google Sheet phù hợp với workflow

3. **OpenAI Chat Model**:
   - Cấu hình credentials cho OpenAI
   - Chọn model "gpt-4.1-mini" (hoặc model tương đương nếu không có)
   - Điền prompt phù hợp cho việc tạo mô tả sản phẩm

4. **Rapiwa**:
   - Cấu hình credentials cho Rapiwa
   - Đảm bảo số điện thoại của bạn đã được xác minh trong Rapiwa
   - Kiểm tra số dư tài khoản Rapiwa trước khi gửi tin nhắn

#### 3. Kích hoạt ⚡️
1. Test run workflow với dữ liệu mẫu để đảm bảo mọi thứ hoạt động đúng
2. Sau khi kiểm tra thành công, bật Active workflow để chạy tự động

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Telegram**: Thêm node để nhận thông báo khi có lỗi hoặc khi workflow hoàn thành
- **Lưu log**: Thêm node để lưu log các tin nhắn đã gửi để theo dõi hiệu suất
- **Gửi báo cáo định kỳ**: Tạo workflow phụ để gửi báo cáo tổng hợp hàng ngày/ hàng tuần về hiệu suất gửi tin nhắn
- **Tối ưu hình ảnh**: Thêm node để tự động nén hình ảnh sản phẩm trước khi gửi để tiết kiệm dung lượng dữ liệu

### 📌 Kết luận
Với workflow này, các sếp có thể tự động hóa hoàn toàn quy trình thông báo sản phẩm mới Shopify qua WhatsApp, tiết kiệm thời gian và tăng tương tác với khách hàng. Hãy thử ngay và trải nghiệm sức mạnh của tự động hóa!