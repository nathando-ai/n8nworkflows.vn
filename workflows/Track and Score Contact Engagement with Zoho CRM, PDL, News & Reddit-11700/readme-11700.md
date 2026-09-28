---
title: "🚀 Theo dõi và Đánh giá Tương tác Liên hệ với Zoho CRM, PDL, Tin tức & Reddit"
description: "Tự động hóa quy trình theo dõi tương tác khách hàng trên nhiều nền tảng với n8n - Tiết kiệm thời gian và tăng hiệu quả bán hàng"
slug: "theo-doi-tuong-tac-khach-hang-zoho-crm-pdl-tin-tuc-reddit"
tags: [n8n, automation, no-code, crm, ai]
keywords: [n8n workflow, tự động hóa, zoho crm, pdl, tin tức, reddit]
---

# 🚀 Theo dõi và Đánh giá Tương tác Liên hệ với Zoho CRM, PDL, Tin tức & Reddit

[Các sếp] có biết không? Với quy trình thủ công truyền thống, việc theo dõi tương tác khách hàng trên nhiều nền tảng như LinkedIn, Twitter, Facebook, Google News và Reddit thường tốn thời gian và dễ bỏ sót thông tin quan trọng. Workflow này sẽ giúp các sếp tự động hóa hoàn toàn quy trình này, mang lại những lợi ích bất ngờ.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động thu thập dữ liệu từ nhiều nguồn trong vài giây
- **Chính xác cao**: Không bỏ sót bất kỳ thông tin quan trọng nào
- **Cá nhân hóa**: Đánh giá tương tác khách hàng một cách chi tiết và cụ thể
- **Hoạt động liên tục**: Theo dõi 24/7 mà không cần can thiệp thủ công
- **Tăng hiệu quả bán hàng**: Phát hiện cơ hội kinh doanh tiềm năng nhanh chóng
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Zoho CRM với quyền truy cập API
- API Key từ People Data Labs (PDL)
- API Key từ Google News API
- Các trường tùy chỉnh đã được tạo trong Zoho CRM: Social_Profiles, Engagement_Score, Mentions_Counts, Social_Status
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [trang workflow gốc](https://n8n.io/workflows/11700)
2. Click vào nút "Import" ở góc trên bên phải
3. Copy toàn bộ JSON và dán vào n8n Editor của các sếp

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Zoho CRM New Contact Webhook**:
   - Đặt path là `zoho-crm-new-contact`
   - Phương thức HTTP là POST
   - Cấu hình webhook trong Zoho CRM để kích hoạt khi có liên hệ mới

2. **Zoho CRM Credentials**:
   - Tạo mới credential Zoho OAuth2
   - Điền các thông tin xác thực từ Zoho CRM

3. **PDL Enrichment**:
   - Thêm API Key từ People Data Labs
   - Đảm bảo tài khoản PDL có đủ credit để thực hiện các truy vấn

4. **GNews Mentions**:
   - Thêm API Key từ Google News API
   - Đảm bảo tài khoản có đủ credit

5. **Reddit Mentions**:
   - Không cần cấu hình API Key riêng, nhưng cần đảm bảo tài khoản có thể truy cập công khai các bài đăng trên Reddit

6. **Zoho CRM Create Deal**:
   - Đảm bảo các trường dữ liệu trong Zoho CRM đã được cấu hình đúng
   - Kiểm tra các trường bắt buộc khi tạo deal mới

7. **Add Contact and Account Details In Created Deal**:
   - Kiểm tra các trường dữ liệu cần cập nhật trong deal
   - Đảm bảo các trường này đã được định nghĩa trong Zoho CRM

8. **Create Note**:
   - Kiểm tra nội dung ghi chú sẽ được tạo
   - Đảm bảo các trường dữ liệu cần ghi chú đã được định nghĩa

9. **Zoho CRM Update Contact**:
   - Kiểm tra các trường dữ liệu sẽ được cập nhật
   - Đảm bảo các trường này đã được định nghĩa trong Zoho CRM

#### 3. Kích hoạt ⚡️
1. Kiểm tra toàn bộ cấu hình bằng cách chạy thử với một liên hệ mẫu
2. Kích hoạt workflow bằng cách bật nút Active
3. Kiểm tra các liên hệ mới trong Zoho CRM để đảm bảo workflow hoạt động đúng

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Slack/Telegram**: Thêm node để gửi thông báo khi phát hiện tương tác khách hàng quan trọng
2. **Lưu log hoạt động**: Thêm node để lưu log các hoạt động quan trọng của workflow
3. **Gửi báo cáo định kỳ**: Tạo workflow phụ để tổng hợp và gửi báo cáo tương tác khách hàng hàng tuần
4. **Tích hợp với các công cụ khác**: Kết nối với các công cụ khác như HubSpot, Salesforce để mở rộng phạm vi theo dõi

### 📌 Kết luận
Workflow này sẽ giúp các sếp tiết kiệm thời gian đáng kể trong việc theo dõi tương tác khách hàng, đồng thời mang lại những thông tin quan trọng để đưa ra quyết định kinh doanh chính xác hơn. Hãy áp dụng ngay để nâng cao hiệu quả bán hàng và phát triển khách hàng tiềm năng!