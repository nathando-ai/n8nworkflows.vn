---
title: "🚀 Tự động hóa Enrichment Contact LinkedIn với Surfe, Google Sheets & HubSpot"
description: "Workflow n8n giúp tự động hóa quá trình lấy thông tin chi tiết từ LinkedIn, xử lý dữ liệu và cập nhật vào HubSpot - tiết kiệm thời gian và nâng cao hiệu quả chăm sóc khách hàng."
slug: "tu-dong-hoa-enrichment-contact-linkedin-voi-surfe-google-sheets-hubspot"
tags: [n8n, automation, no-code, lead-generation, crm]
keywords: [n8n workflow, tự động hóa, lead generation, HubSpot, Google Sheets, LinkedIn]
---

# 🚀 Tự động hóa Enrichment Contact LinkedIn với Surfe, Google Sheets & HubSpot

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp khi phải thu thập và xử lý thông tin liên hệ từ LinkedIn một cách thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa quá trình lấy thông tin từ LinkedIn, xử lý dữ liệu và cập nhật vào HubSpot.
- Dữ liệu chính xác: Sử dụng API của Surfe để lấy thông tin chi tiết và đáng tin cậy.
- Tự động hóa hoàn toàn: Không cần can thiệp thủ công, workflow chạy liên tục 24/7.
- Tích hợp đa nền tảng: Kết nối liền mạch với Google Sheets, HubSpot và Gmail.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Workspace (để sử dụng Google Sheets và Google Drive Trigger).
- Tài khoản HubSpot (để tạo/update contact).
- Tài khoản Gmail (để gửi email thông báo).
- API Key của Surfe (để sử dụng Surfe Bulk Enrichments API).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor.
2. Click vào "Import from URL" và nhập link: [https://n8n.io/workflows/5776](https://n8n.io/workflows/5776).
3. Hoặc copy/paste JSON từ file workflow vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Google Sheets**:
   - Cấu hình credentials cho Google Sheets.
   - Chỉnh sửa ID của Google Sheet và tên của sheet cần xử lý.

2. **Google Drive Trigger**:
   - Cấu hình credentials cho Google Drive.
   - Chỉnh sửa ID của file Google Drive cần theo dõi.

3. **Filter: phone AND email**:
   - Kiểm tra và điều chỉnh điều kiện lọc nếu cần.

4. **Extract list of peoples from Surfe API response**:
   - Kiểm tra và chỉnh sửa code để trích xuất dữ liệu từ API response của Surfe.

5. **Surfe Bulk Enrichments API**:
   - Cấu hình API Key của Surfe.
   - Kiểm tra và chỉnh sửa URL và body của request nếu cần.

6. **HubSpot: Create or Update**:
   - Cấu hình credentials cho HubSpot.
   - Kiểm tra và chỉnh sửa các trường dữ liệu cần cập nhật.

7. **Gmail**:
   - Cấu hình credentials cho Gmail.
   - Chỉnh sửa địa chỉ email nhận thông báo.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi workflow hoàn thành.
- Lưu log hoạt động vào Google Sheets để theo dõi lịch sử.
- Gửi báo cáo định kỳ về số lượng contact đã được xử lý.

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian và nâng cao hiệu quả chăm sóc khách hàng bằng cách tự động hóa quá trình lấy thông tin chi tiết từ LinkedIn, xử lý dữ liệu và cập nhật vào HubSpot. Hãy áp dụng ngay để tối ưu hóa quy trình làm việc của bạn!