---
title: "🔄 Tự động đồng bộ dữ liệu liên hệ giữa KlickTipp và Salesforce - Workflow n8n hoàn chỉnh"
description: "Hướng dẫn chi tiết cách thiết lập workflow n8n để đồng bộ tự động dữ liệu liên hệ, đồng ý và phân khúc giữa KlickTipp và Salesforce, đảm bảo tuân thủ GDPR và tối ưu hóa quy trình marketing"
slug: "tu-dong-dong-bo-du-lieu-giua-klicktipp-va-salesforce"
tags: [n8n, automation, no-code, crm, marketing-automation]
keywords: [n8n workflow, tự động hóa, đồng bộ dữ liệu, KlickTipp, Salesforce, GDPR]
---

# 🔄 Tự động đồng bộ dữ liệu liên hệ giữa KlickTipp và Salesforce - Workflow n8n hoàn chỉnh

[Các sếp marketing] đang gặp khó khăn khi phải quản lý hai hệ thống CRM khác nhau (KlickTipp và Salesforce) một cách thủ công. Việc đồng bộ dữ liệu liên hệ, trạng thái đồng ý và phân khúc giữa hai nền tảng này tốn thời gian và dễ gây lỗi. Workflow n8n này sẽ giúp các sếp tự động hóa toàn bộ quy trình này một cách hoàn toàn không cần code.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Đồng bộ tự động dữ liệu liên hệ giữa hai nền tảng CRM
- Tiết kiệm thời gian lên tới 80% so với làm thủ công
- Đảm bảo dữ liệu luôn đồng bộ và chính xác
- Tự động xử lý yêu cầu xóa dữ liệu theo quy định GDPR
- Tối ưu hóa quy trình marketing với dữ liệu đồng nhất
- Giảm thiểu rủi ro lỗi do nhập liệu thủ công
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Salesforce với quyền truy cập API
- Tài khoản KlickTipp với quyền quản trị
- API Keys cho cả hai nền tảng
- Trên Salesforce: Tạo trường tùy chỉnh `KlickTipp_ID__c` trên đối tượng Contact
- Trên KlickTipp: Tạo trường tùy chỉnh để lưu Salesforce ID (mapped đến `field227883`)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/13474](https://n8n.io/workflows/13474)
2. Chọn "Download" để tải file JSON workflow
3. Trong n8n Editor, nhấn "Import from File" và chọn file vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Cấu hình Credentials**:
   - Tạo credentials cho KlickTipp API (klickTippApi)
   - Tạo credentials cho Salesforce OAuth2 API (salesforceOAuth2Api)

2. **Cấu hình các node quan trọng**:
   - **Daily Cleanup Trigger**: Đặt lịch chạy hàng ngày (ví dụ: 2:00 AM)
   - **Contact tagged in KlickTipp**: Cập nhật path với webhook URL của bạn từ KlickTipp
   - **Fetch Deleted SF Contacts**: Cập nhật URL với instance Salesforce của bạn (ví dụ: `https://yourinstance.salesforce.com/services/data/v56.0/sobjects/Contact/deleted`)
   - **Assign SF Topic (Customer) và Assign SF Topic (ABC)**: Cập nhật các Topic ID tương ứng với hệ thống của bạn
   - **GDPR Deletion Request Trigger**: Cập nhật path với webhook URL từ KlickTipp

3. **Cấu hình Data Normalization & Mapping**:
   - Điều chỉnh các mapping giữa các trường dữ liệu của hai nền tảng
   - Đặc biệt chú ý đến việc mapping trường ngày sinh (Birthday)

#### 3. Kích hoạt ⚡️
1. Chạy test với dữ liệu mẫu để kiểm tra kết nối và mapping
2. Kích hoạt workflow bằng cách nhấn "Active" trên mỗi node trigger

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Slack/Teams**: Thêm node gửi thông báo khi đồng bộ thất bại
2. **Lưu log hoạt động**: Thêm node lưu log vào Google Sheets hoặc database
3. **Báo cáo định kỳ**: Tạo workflow phụ để gửi báo cáo trạng thái đồng bộ hàng tuần
4. **Xử lý lỗi tự động**: Thêm node xử lý lỗi và gửi email cảnh báo khi có vấn đề

### 📌 Kết luận
Workflow này tạo ra một hệ thống đồng bộ tự động hoàn chỉnh giữa KlickTipp và Salesforce, giúp các sếp tiết kiệm thời gian, giảm thiểu lỗi và đảm bảo tuân thủ GDPR. Hãy triển khai ngay để tối ưu hóa quy trình marketing của bạn!