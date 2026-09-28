---
title: "🚀 Tự động đồng bộ leads từ Google Sheets sang HubSpot - Workflow n8n"
description: "Hướng dẫn chi tiết cách tự động đồng bộ leads từ Google Sheets sang HubSpot bằng workflow n8n. Tiết kiệm thời gian và tránh lỗi nhập liệu thủ công."
slug: "tu-dong-dong-bo-leads-google-sheets-hubspot-n8n"
tags: [n8n, automation, no-code, lead-generation, hubspot, google-sheets]
keywords: [n8n workflow, tự động hóa leads, đồng bộ dữ liệu, hubspot api, google sheets api]
---

# 🚀 Tự động đồng bộ leads từ Google Sheets sang HubSpot - Workflow n8n

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp thường gặp khó khăn khi phải nhập liệu leads từ Google Sheets sang HubSpot thủ công. Quá trình này tốn thời gian, dễ gây lỗi và không nhất quán. Workflow này sẽ giúp các sếp tự động hóa toàn bộ quy trình này chỉ trong vài bước đơn giản.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian nhập liệu thủ công
- Giảm thiểu lỗi nhập liệu
- Đồng bộ dữ liệu liên tục và tự động
- Dữ liệu luôn đồng bộ nhất quán giữa Google Sheets và HubSpot
- Tự động tránh trùng lặp leads dựa trên email
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với quyền truy cập vào Google Sheets chứa dữ liệu leads
- Tài khoản HubSpot với quyền truy cập vào danh sách contacts
- Access Token từ HubSpot (hướng dẫn chi tiết bên dưới)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor
2. Click vào "Import from URL" và nhập link: https://n8n.io/workflows/13460
3. Hoặc copy JSON từ link trên và paste vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

**Node 1: Manual Trigger - Start Workflow**
- Không cần cấu hình gì thêm, chỉ cần kích hoạt workflow

**Node 2: Get Contact Leads from Google Sheet**
1. Chọn credentials Google Sheets (nếu chưa có, tạo mới)
2. Cấu hình các tham số:
   - Spreadsheet ID: ID của Google Sheet chứa dữ liệu leads
   - Sheet Name: Tên sheet chứa dữ liệu leads
   - Range: Phạm vi dữ liệu cần lấy (ví dụ: A2:E)
3. Đảm bảo cột dữ liệu trong Google Sheets phải chứa các trường thông tin cơ bản như: Email, Company Name, Name, Phone Number

**Node 3: Create or Update HubSpot Contact**
1. Chọn credentials HubSpot (nếu chưa có, tạo mới theo hướng dẫn bên dưới)
2. Cấu hình các tham số:
   - Property Mappings: Đảm bảo ánh xạ đúng giữa các trường dữ liệu từ Google Sheets và các trường trong HubSpot
   - Match By: Chọn "Email" để tránh trùng lặp leads

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu trước khi kích hoạt workflow
2. Sau khi test thành công, bật Active workflow

### ✍️ Mẹo & gợi ý nâng cao
- Thiết lập workflow chạy tự động theo lịch sử (ví dụ: mỗi ngày lúc 9h sáng)
- Kết hợp với Slack/Telegram để nhận thông báo khi workflow chạy thành công
- Lưu log hoạt động của workflow để theo dõi hiệu suất
- Tự động gửi báo cáo định kỳ về số lượng leads đã đồng bộ

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian và giảm thiểu lỗi khi đồng bộ leads giữa Google Sheets và HubSpot. Bằng cách tự động hóa quy trình này, các sếp có thể tập trung vào các nhiệm vụ quan trọng hơn trong công việc hàng ngày. Hãy thử ngay và trải nghiệm sự tiện lợi mà tự động hóa mang lại!