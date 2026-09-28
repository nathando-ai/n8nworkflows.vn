---
title: "🚀 Tự động gửi yêu cầu kết nối LinkedIn với Airtop - Giải pháp tự động hóa 100% không cần code"
description: "Hướng dẫn chi tiết cách tự động gửi yêu cầu kết nối LinkedIn với Airtop, tiết kiệm thời gian và tăng hiệu quả kết nối mạng"
slug: "tu-dong-gui-yeu-cau-ket-noi-linkedin-voi-airtop"
tags: [n8n, automation, no-code, LinkedIn, sales]
keywords: [n8n workflow, tự động hóa, LinkedIn, kết nối mạng, Airtop]
---

# 🚀 Tự động gửi yêu cầu kết nối LinkedIn với Airtop - Giải pháp tự động hóa 100% không cần code

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp có biết không? Việc gửi yêu cầu kết nối LinkedIn thủ công tốn thời gian và dễ bị lỗi. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình này một cách hoàn toàn không cần code, giúp tiết kiệm thời gian quý giá và tăng hiệu quả kết nối mạng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa toàn bộ quy trình gửi yêu cầu kết nối LinkedIn.
- Chính xác: Kiểm tra trạng thái kết nối trước khi gửi yêu cầu.
- Cá nhân hóa: Có thể thêm tin nhắn cá nhân hóa cho mỗi yêu cầu kết nối.
- Hoạt động liên tục: Chạy 24/7 mà không cần can thiệp thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Airtop API Key (miễn phí).
- Airtop Profile đã đăng nhập LinkedIn (yêu cầu xác thực một lần).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:
- **On form submission**: Cấu hình form để nhập các tham số đầu vào (linked_url, airtop_profile, message).
- **When Executed by Another Workflow**: Cấu hình để workflow này có thể được kích hoạt từ workflow khác.
- **Unify Params**: Cấu hình để thống nhất các tham số đầu vào.
- **Create a Session**: Chọn credentials Airtop API.
- **Create a window**: Cấu hình URL LinkedIn profile từ tham số đầu vào.
- **Click on connect**: Cấu hình để nhấp vào nút "Connect".
- **Send connection w/out message**: Cấu hình để gửi yêu cầu kết nối không có tin nhắn.
- **Click add a note**: Cấu hình để nhấp vào nút "Add a note".
- **Type the message**: Cấu hình để nhập tin nhắn từ tham số đầu vào.
- **Send connection w/ message**: Cấu hình để gửi yêu cầu kết nối có tin nhắn.
- **Check connection status**: Cấu hình để kiểm tra trạng thái kết nối.
- **Terminate session**: Cấu hình để kết thúc phiên làm việc.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với workflow tìm kiếm profile LinkedIn để tự động hóa toàn bộ quy trình tìm kiếm và kết nối.
- Lưu log kết quả vào Google Sheets hoặc CRM để theo dõi hiệu quả kết nối.
- Gửi báo cáo định kỳ về số lượng yêu cầu kết nối đã gửi và trạng thái kết nối.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quy trình gửi yêu cầu kết nối LinkedIn một cách chính xác và hiệu quả. Với các sếp có thể áp dụng ngay để tăng hiệu quả kết nối mạng và tiết kiệm thời gian quý giá.