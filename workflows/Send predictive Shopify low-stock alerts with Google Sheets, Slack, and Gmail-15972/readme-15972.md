---
title: "🚀 Tự động cảnh báo hàng tồn kho Shopify thông minh với Google Sheets, Slack và Gmail"
description: "Hướng dẫn tự động hóa cảnh báo hàng tồn kho Shopify với n8n - Tiết kiệm thời gian, tối ưu kho hàng và tăng doanh thu"
slug: "tu-dong-canh-bao-hang-ton-kho-shopify-voi-n8n"
tags: [n8n, automation, no-code, shopify, google-sheets, slack, gmail]
keywords: [n8n workflow, tự động hóa, shopify, cảnh báo hàng tồn kho, google sheets, slack, gmail]
---

# 🚀 Tự động cảnh báo hàng tồn kho Shopify thông minh với Google Sheets, Slack và Gmail

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Khi quản lý hàng tồn kho Shopify thủ công, các sếp thường gặp phải những vấn đề như:
- Không kịp thời cảnh báo hàng tồn kho
- Không thể dự đoán nhu cầu hàng hóa chính xác
- Thiếu hệ thống theo dõi lịch sử cảnh báo
- Không có kênh thông báo nhanh chóng và đồng bộ

Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình theo dõi và cảnh báo hàng tồn kho Shopify một cách thông minh, tiết kiệm thời gian và tối ưu hóa kho hàng hiệu quả.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian quản lý hàng tồn kho
- Dự đoán nhu cầu hàng hóa chính xác hơn
- Theo dõi lịch sử cảnh báo hiệu quả
- Nhận thông báo nhanh chóng qua Slack và Email
- Tăng doanh thu bằng cách tối ưu hóa kho hàng
- Giảm thiểu rủi ro hết hàng đột ngột
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Shopify với quyền truy cập API
- Tài khoản Google với quyền truy cập Google Sheets
- Tài khoản Slack với quyền gửi tin nhắn
- Tài khoản Gmail với quyền gửi email
- Google Sheet đã được tạo sẵn để lưu trữ lịch sử cảnh báo
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **When Daily at 7am** (scheduleTrigger):
   - Cấu hình thời gian chạy workflow hàng ngày (mặc định 7am)

2. **Set Inventory Settings** (set):
   - Cấu hình các tham số quan trọng:
     - daysToCalculateVelocity: Số ngày tính toán tốc độ bán hàng (mặc định 30 ngày)
     - recipientMail: Email nhận cảnh báo
     - googleSheetUrl: URL của Google Sheet lưu trữ lịch sử cảnh báo
     - slackEscalationChannel: Kênh Slack nhận cảnh báo

3. **Fetch Shopify Orders** (shopify):
   - Cấu hình credentials Shopify
   - Đảm bảo có quyền truy cập vào API Shopify

4. **Fetch Shopify Inventory** (shopify):
   - Cấu hình credentials Shopify
   - Đảm bảo có quyền truy cập vào API Shopify
   - Chọn đúng store, sản phẩm và vị trí kho hàng

5. **Read Inventory Logs from Sheets** (googleSheets):
   - Cấu hình credentials Google Sheets
   - Điền URL của Google Sheet lưu trữ lịch sử cảnh báo
   - Chọn đúng sheet và phạm vi dữ liệu

6. **Calculate Inventory Velocity** (code):
   - Node này sử dụng code để tính toán tốc độ bán hàng và dự đoán hàng tồn kho
   - Không cần cấu hình, chỉ cần đảm bảo node trước đó đã lấy được dữ liệu Shopify

7. **Append Alert to Sheets** (googleSheets):
   - Cấu hình credentials Google Sheets
   - Điền URL của Google Sheet lưu trữ lịch sử cảnh báo
   - Chọn đúng sheet và phạm vi dữ liệu

8. **Post Inventory Alert to Slack** (slack):
   - Cấu hình credentials Slack
   - Chọn đúng kênh Slack nhận cảnh báo

9. **Build Email Content** (code):
   - Node này sử dụng code để xây dựng nội dung email cảnh báo
   - Không cần cấu hình, chỉ cần đảm bảo node trước đó đã tính toán được dữ liệu hàng tồn kho

10. **Send Stock Alert Email** (gmail):
    - Cấu hình credentials Gmail
    - Điền địa chỉ email nhận cảnh báo
    - Đảm bảo email gửi và nhận đã được cấu hình đúng

11. **On Global Error** (errorTrigger):
    - Node này bắt lỗi toàn cục của workflow
    - Không cần cấu hình

12. **Post Error to Slack** (slack):
    - Cấu hình credentials Slack
    - Chọn đúng kênh Slack nhận thông báo lỗi

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Telegram để nhận cảnh báo hàng tồn kho
- Lưu log chi tiết hơn vào Google Sheets (thêm thông tin về sản phẩm, giá cả, thời gian cảnh báo)
- Gửi báo cáo hàng tuần/hàng tháng về tình trạng hàng tồn kho
- Tích hợp với các hệ thống quản lý kho hàng khác (WooCommerce, BigCommerce)
- Thiết lập cảnh báo cho nhiều cửa hàng Shopify khác nhau

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quy trình theo dõi và cảnh báo hàng tồn kho Shopify một cách thông minh, tiết kiệm thời gian và tối ưu hóa kho hàng hiệu quả. Bằng cách áp dụng workflow này, các sếp có thể giảm thiểu rủi ro hết hàng đột ngột, tăng doanh thu và cải thiện trải nghiệm khách hàng.