---
title: "🏠 Tự động tạo website đặt phòng trực tiếp từ Airbnb và đăng lên Netlify"
description: "Hướng dẫn tự động hóa quy trình tạo website đặt phòng trực tiếp từ bất kỳ listing Airbnb nào và đăng lên Netlify miễn phí với n8n"
slug: "tu-dong-tao-website-dat-phong-tu-airbnb-va-dang-len-netlify"
tags: [n8n, automation, no-code, Airbnb, Netlify]
keywords: [n8n workflow, tự động hóa, Airbnb, Netlify, website đặt phòng]
---

# 🏠 Tự động tạo website đặt phòng trực tiếp từ Airbnb và đăng lên Netlify

[Các sếp đang gặp khó khăn khi phải tạo website đặt phòng trực tiếp từ Airbnb một cách thủ công. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình từ việc lấy dữ liệu listing đến việc tạo website và đăng lên Netlify miễn phí.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian đáng kể trong việc tạo website đặt phòng trực tiếp
- Website được tạo tự động với thiết kế đẹp mắt và chuyên nghiệp
- Dữ liệu listing được cập nhật tự động từ Airbnb
- Website được đăng lên Netlify miễn phí với URL riêng
- Quá trình tự động hóa hoạt động liên tục 24/7
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Airbnb Scraper API (lấy token tại [shortrentals.ai](https://scraper.shortrentals.ai))
- Tài khoản Netlify API (tạo personal access token tại [Netlify](https://app.netlify.com/user/applications#personal-access-tokens))
- ID của listing Airbnb (có thể tìm thấy trong URL của listing)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow](https://n8n.io/workflows/11672)
2. Click vào nút "Import" để tải file JSON về máy
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Set Listing ID"**:
   - Chỉnh sửa giá trị của biến `listingId` với ID của listing Airbnb bạn muốn tạo website
   - Ví dụ: Nếu URL listing là `airbnb.com/rooms/1234567890`, thì giá trị `listingId` sẽ là `1234567890`

2. **Node "Airbnb Scraper"**:
   - Đảm bảo đã tạo và cấu hình credentials cho Airbnb Scraper API
   - Chọn operation là "scrapeListing"

3. **Node "Create Netlify Site"**:
   - Đảm bảo đã tạo và cấu hình credentials cho Netlify API
   - Chỉnh sửa URL endpoint nếu cần (mặc định là `https://api.netlify.com/api/v1/sites`)

4. **Node "Deploy ZIP"**:
   - Đảm bảo đã tạo và cấu hình credentials cho Netlify API
   - Chỉnh sửa URL endpoint nếu cần (mặc định là `https://api.netlify.com/api/v1/sites/{siteId}/deploys`)

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong, click vào nút "Execute Node" để test workflow với dữ liệu mẫu
2. Kiểm tra kết quả đầu ra để đảm bảo website đã được tạo và đăng lên Netlify thành công
3. Nếu mọi thứ ổn, click vào nút "Activate" để kích hoạt workflow

### ✍️ Mẹo & gợi ý nâng cao
- Để cập nhật website sau này, bạn có thể lưu lại site ID từ kết quả đầu ra và sử dụng nó trong node "Deploy ZIP"
- Bạn có thể kết hợp workflow này với các dịch vụ khác như Slack hoặc Telegram để nhận thông báo khi website được tạo thành công
- Để tối ưu hóa, bạn có thể thêm node để gửi báo cáo định kỳ về hiệu suất của website
- Bạn có thể tùy chỉnh thiết kế của website bằng cách chỉnh sửa mã HTML trong node "Generate HTML Site"

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quy trình tạo website đặt phòng trực tiếp từ Airbnb và đăng lên Netlify miễn phí. Với việc tự động hóa quy trình này, các sếp có thể tiết kiệm thời gian đáng kể và tập trung vào các nhiệm vụ quan trọng hơn. Hãy áp dụng ngay workflow này để nâng cao hiệu quả kinh doanh của bạn!