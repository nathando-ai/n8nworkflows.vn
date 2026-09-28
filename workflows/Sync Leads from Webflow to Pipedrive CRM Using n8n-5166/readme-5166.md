---
title: "🚀 Tự động đồng bộ dữ liệu khách hàng từ Webflow sang Pipedrive CRM bằng n8n"
description: "Hướng dẫn chi tiết cách tự động hóa quy trình đồng bộ dữ liệu khách hàng từ form Webflow sang Pipedrive CRM bằng n8n, tiết kiệm thời gian và tránh trùng lặp dữ liệu"
slug: "tu-dong-dong-bo-du-lieu-khach-hang-tu-webflow-sang-pipedrive-crm-bang-n8n"
tags: [n8n, automation, no-code, webflow, pipedrive]
keywords: [n8n workflow, tự động hóa, webflow, pipedrive, crm]
---

# 🚀 Tự động đồng bộ dữ liệu khách hàng từ Webflow sang Pipedrive CRM bằng n8n

[Các sếp đang gặp khó khăn khi phải nhập thủ công dữ liệu khách hàng từ form Webflow vào Pipedrive CRM. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình này chỉ trong vài bước đơn giản.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian nhập liệu thủ công
- Giảm thiểu dữ liệu trùng lặp
- Tự động hóa toàn bộ quy trình từ form Webflow đến Pipedrive
- Dữ liệu khách hàng luôn được cập nhật mới nhất
- Tích hợp liền mạch giữa các công cụ marketing và sales
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Webflow với form cần đồng bộ
- Tài khoản Pipedrive CRM
- API key của Pipedrive
- Quyền truy cập vào n8n Editor
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor
2. Click vào "Import from URL" và nhập link: https://n8n.io/workflows/5166
3. Hoặc copy JSON từ link trên và paste vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Webflow Trigger Node**:
   - Chọn credentials "webflowOAuth2Api"
   - Cấu hình webhook để nhận dữ liệu từ form Webflow

2. **Pipedrive Nodes**:
   - Tất cả các node Pipedrive đều cần credentials "pipedriveApi"
   - Đảm bảo API key của Pipedrive có quyền truy cập đầy đủ

3. **Code Node (Website)**:
   - Node này dùng để trích xuất domain từ email
   - Có thể tùy chỉnh regex nếu cần xử lý các định dạng email đặc biệt

#### 3. Kích hoạt ⚡️
1. Test run với dữ liệu mẫu từ form Webflow
2. Kiểm tra kết quả trên Pipedrive CRM
3. Bật Active workflow sau khi đã kiểm tra kỹ

### ✍️ Mẹo & gợi ý nâng cao
1. Kết nối với Slack để nhận thông báo khi có lead mới
2. Thêm node gửi email tự động cho khách hàng mới
3. Tích hợp với Google Sheets để lưu trữ dữ liệu phụ
4. Thêm bước xử lý dữ liệu để tự động gán nhãn cho lead theo tiêu chí nhất định

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quy trình từ khi khách hàng điền form Webflow đến khi dữ liệu được cập nhật vào Pipedrive CRM. Với việc giảm thiểu công việc thủ công, các sếp có thể tập trung vào các nhiệm vụ quan trọng hơn. Hãy thử ngay và trải nghiệm sự tiện lợi mà tự động hóa mang lại!