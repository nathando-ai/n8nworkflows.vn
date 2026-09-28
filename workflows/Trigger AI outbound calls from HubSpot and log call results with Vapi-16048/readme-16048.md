---
title: "📞 Tự động hóa cuộc gọi AI với HubSpot và Vapi - Workflow n8n hoàn chỉnh"
description: "Hướng dẫn chi tiết cách tự động hóa cuộc gọi AI outbound từ HubSpot và ghi lại kết quả gọi với Vapi. Tiết kiệm thời gian và nâng cao hiệu quả chăm sóc khách hàng."
slug: "tu-dong-hoa-cuoc-goi-ai-hubspot-vapi-n8n"
tags: [n8n, automation, no-code, hubspot, vapi, ai, outbound-calling]
keywords: [n8n workflow, tự động hóa cuộc gọi, hubspot api, vapi ai, chăm sóc khách hàng, tự động hóa marketing]
---

# 📞 Tự động hóa cuộc gọi AI với HubSpot và Vapi - Workflow n8n hoàn chỉnh

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp đang gặp khó khăn khi phải thực hiện các cuộc gọi outbound thủ công với hàng nghìn khách hàng tiềm năng trên HubSpot. Quá trình này tốn thời gian, dễ bị lỗi và không thể cá nhân hóa cho từng khách hàng. Ngoài ra, việc theo dõi kết quả cuộc gọi và lưu trữ thông tin lại là một công việc tốn kém thời gian và công sức.

Với workflow này, các sếp có thể tự động hóa hoàn toàn quy trình gọi điện AI từ HubSpot và ghi lại kết quả cuộc gọi với Vapi. Workflow này sẽ giúp tiết kiệm thời gian, nâng cao hiệu quả chăm sóc khách hàng và tự động hóa quy trình kinh doanh.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian và công sức cho đội ngũ chăm sóc khách hàng.
- Tăng hiệu quả chăm sóc khách hàng với cuộc gọi AI cá nhân hóa.
- Tự động hóa quy trình kinh doanh và nâng cao hiệu suất làm việc.
- Theo dõi kết quả cuộc gọi và lưu trữ thông tin một cách dễ dàng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản HubSpot với quyền truy cập API.
- Tài khoản Vapi với Assistant và Phone Number đã cấu hình.
- Bearer token cho Vapi API.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Để import workflow này vào n8n, các sếp có thể làm theo các bước sau:

1. Truy cập vào n8n Editor.
2. Nhấn vào nút "Import" ở góc trên bên phải.
3. Chọn file JSON của workflow hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

- **HubSpot Trigger**: Cấu hình credentials cho HubSpot Developer API và chọn đúng event type (mặc định là tất cả các sự kiện liên quan đến contact).
- **Get a contact**: Cấu hình credentials cho HubSpot OAuth2 API và chọn operation là "get".
- **Parse Response**: Node này sẽ tự động chuẩn hóa và định dạng lại dữ liệu từ HubSpot.
- **Check Phone Format**: Node này sẽ kiểm tra định dạng số điện thoại và chỉ cho phép cuộc gọi được thực hiện nếu số điện thoại hợp lệ.
- **Make a Call**: Cấu hình credentials cho Vapi API và cập nhật `assistantId` và `phoneNumberId` với giá trị của Vapi Assistant và Phone Number của các sếp.
- **Wait for 2 minutes**: Node này sẽ đợi 2 phút trước khi bắt đầu quá trình polling.
- **Get Vapi Call Details**: Cấu hình credentials cho Vapi API để lấy thông tin chi tiết về cuộc gọi.
- **Pick One**: Node này sẽ đảm bảo chỉ có một cuộc gọi được xử lý tại một thời điểm.
- **Check Status**: Node này sẽ kiểm tra trạng thái của cuộc gọi và chỉ tiếp tục nếu cuộc gọi đã kết thúc.
- **Log Call**: Cấu hình credentials cho HubSpot OAuth2 API để ghi lại kết quả cuộc gọi vào HubSpot.
- **Polling**: Node này sẽ đợi 10 giây trước khi tiếp tục quá trình polling.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Các sếp có thể kết hợp workflow này với Slack hoặc Telegram để nhận thông báo khi có cuộc gọi mới được thực hiện.
- Lưu log cuộc gọi vào Google Sheets hoặc cơ sở dữ liệu để phân tích và báo cáo.
- Gửi báo cáo định kỳ về kết quả cuộc gọi và hiệu suất chăm sóc khách hàng.

### 📌 Kết luận
Workflow này sẽ giúp các sếp tự động hóa hoàn toàn quy trình gọi điện AI từ HubSpot và ghi lại kết quả cuộc gọi với Vapi. Với workflow này, các sếp có thể tiết kiệm thời gian, nâng cao hiệu quả chăm sóc khách hàng và tự động hóa quy trình kinh doanh. Hãy áp dụng ngay workflow này để nâng cao hiệu suất làm việc và đạt được kết quả tốt nhất.