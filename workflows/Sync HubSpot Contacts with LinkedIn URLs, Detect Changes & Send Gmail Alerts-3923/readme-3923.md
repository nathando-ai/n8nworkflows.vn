---
title: "🚀 Tự động hóa HubSpot & LinkedIn: Phát hiện thay đổi và cảnh báo qua Gmail"
description: "Workflow n8n tự động đồng bộ danh sách khách hàng HubSpot với LinkedIn, phát hiện thay đổi và gửi cảnh báo qua email - tiết kiệm thời gian và nâng cao hiệu quả chăm sóc khách hàng"
slug: "tu-dong-hoa-hubspot-linkedin-voi-gmail"
tags: [n8n, automation, no-code, sales, it-ops]
keywords: [n8n workflow, tự động hóa, hubspot, linkedin, gmail]
---

# 🚀 Tự động hóa HubSpot & LinkedIn: Phát hiện thay đổi và cảnh báo qua Gmail

[Các sếp] có biết rằng việc theo dõi thay đổi trên LinkedIn của khách hàng HubSpot đang tốn nhiều thời gian và dễ bỏ sót thông tin quan trọng? Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình: từ lấy dữ liệu khách hàng đến phát hiện thay đổi và gửi cảnh báo qua email - hoàn toàn không cần viết code!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa toàn bộ quy trình theo dõi thay đổi
- **Chính xác cao**: Phát hiện thay đổi ngay khi có sự kiện mới
- **Cá nhân hóa**: Cảnh báo riêng cho từng khách hàng
- **Hoạt động liên tục**: Theo dõi 24/7 mà không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản HubSpot với quyền truy cập API
- Tài khoản Gmail với quyền truy cập API
- Google Sheet mẫu đã được sao chép từ [đây](https://docs.google.com/spreadsheets/d/1y17jIU6JnNPcmazWf2GsmRpdjBBMnkN41tRJnAO5KrQ/edit?usp=sharing)
- API Key từ RapidAPI (để tìm kiếm thông tin trên LinkedIn)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/3923](https://n8n.io/workflows/3923)
2. Chọn "Import" và sao chép nội dung JSON vào n8n Editor
3. Hoặc tải file JSON về và import trực tiếp trong n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Set data here"**:
   - Điền email của các sếp trong HubSpot
   - Cập nhật ID Google Sheet đã sao chép

2. **Node "Get list of owners" và "Get list of clients for owner"**:
   - Tạo credentials HubSpot OAuth2 API theo hướng dẫn [tại đây](https://docs.n8n.io/integrations/builtin/credentials/hubspot/?utm_source=n8n_app&utm_medium=credential_settings&utm_campaign=create_new_credentials_modal#required-scopes-for-hubspot-trigger-node)

3. **Node "Gmail"**:
   - Tạo credentials Gmail OAuth2 API

4. **Node "Search for user by link"**:
   - Thêm RapidAPI Key vào credentials HTTP Header Auth

5. **Node "Create entry with email" và các node Google Sheets khác**:
   - Đảm bảo Google Sheet có cấu trúc phù hợp với dữ liệu đầu vào
   - Cấu hình đúng Sheet ID và tên sheet

6. **Node "Change this for testing"**:
   - Thêm bộ lọc để kiểm tra với số lượng khách hàng nhỏ trước khi chạy toàn bộ

#### 3. Kích hoạt ⚡️
1. Chạy test với nút "Test workflow" để kiểm tra dữ liệu mẫu
2. Sau khi kiểm tra thành công, bật "Active" workflow để chạy tự động

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Teams để nhận cảnh báo ngay lập tức
- Thêm chức năng theo dõi bình luận mới trên LinkedIn
- Tích hợp với HubSpot Activities để theo dõi các hoạt động quan trọng
- Thiết lập gửi báo cáo định kỳ về các thay đổi quan trọng

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm hàng giờ mỗi ngày trong việc theo dõi khách hàng HubSpot trên LinkedIn. Bằng cách tự động hóa toàn bộ quy trình và gửi cảnh báo tức thời, các sếp có thể tập trung vào những nhiệm vụ quan trọng hơn. Hãy áp dụng ngay để nâng cao hiệu quả chăm sóc khách hàng của doanh nghiệp!

Nếu cần hỗ trợ hoặc tùy chỉnh workflow, các sếp có thể liên hệ:
📧 [thomas@pollup.net](mailto:thomas@pollup.net)