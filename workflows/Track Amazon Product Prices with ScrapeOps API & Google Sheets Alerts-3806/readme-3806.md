---
title: "🚀 Theo dõi giá sản phẩm Amazon tự động với ScrapeOps API & cảnh báo Google Sheets"
description: "Hướng dẫn tự động hóa theo dõi giá sản phẩm Amazon, tính toán thay đổi giá và gửi cảnh báo qua email khi giá vượt ngưỡng đặt sẵn"
slug: "theo-doi-gia-san-pham-amazon-tu-dong"
tags: [n8n, automation, no-code, amazon, scrapeops]
keywords: [n8n workflow, tự động hóa, theo dõi giá, amazon, scrapeops]
---

# 🚀 Theo dõi giá sản phẩm Amazon tự động với ScrapeOps API & cảnh báo Google Sheets

[Các sếp] có bao giờ phải theo dõi giá hàng ngày của hàng chục sản phẩm Amazon để tìm kiếm cơ hội mua sắm tốt nhất? Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình này trong vòng vài phút, không cần viết một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động theo dõi giá hàng ngày mà không cần can thiệp thủ công
- **Chính xác cao**: Dữ liệu được lấy từ API chuyên nghiệp của ScrapeOps, tránh bị chặn
- **Cá nhân hóa**: Đặt ngưỡng cảnh báo riêng cho từng sản phẩm
- **Hoạt động liên tục**: Kiểm tra giá định kỳ theo lịch trình đã đặt
- **Dễ theo dõi**: Tất cả dữ liệu được lưu trữ trong Google Sheets với lịch sử giá chi tiết
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google để truy cập Google Sheets
- Email để nhận cảnh báo (có thể dùng Gmail, Outlook, v.v.)
- API Key từ ScrapeOps (đăng ký tại [https://scrapeops.io/app/register/main](https://scrapeops.io/app/register/main))
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [https://n8n.io/workflows/3806](https://n8n.io/workflows/3806)
2. Nhấn nút "Download" để tải file JSON workflow
3. Trong n8n Editor, nhấn vào "Import from File" và chọn file vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Products to Monitor"**:
   - Thiết lập credentials cho Google Sheets OAuth2 API
   - Đảm bảo spreadsheet có cấu trúc phù hợp (sao chép từ [template](https://docs.google.com/spreadsheets/d/1hRv-TBXrpN6rkIU65WorttNHt-IPWas_An0sF4Of39U))

2. **Node "Scrapeops - Amazon Product"**:
   - Thêm API Key từ ScrapeOps vào trường "api_key"
   - Đảm bảo endpoint là `https://api.scrapeops.io/v1/scrape`

3. **Node "Send Email"**:
   - Thiết lập credentials cho SMTP (Gmail, Outlook, v.v.)
   - Cấu hình địa chỉ email nhận cảnh báo

4. **Node "Schedule Trigger"**:
   - Đặt lịch chạy workflow theo tần suất mong muốn (ví dụ: hàng ngày lúc 9h sáng)

5. **Node "Setup"**:
   - Cập nhật biến `spreadsheet_url` với liên kết đến bản sao của bạn trong Google Sheets

#### 3. Kích hoạt ⚡️
1. Nhấn nút "Execute Node" để kiểm tra dữ liệu mẫu
2. Sau khi kiểm tra thành công, nhấn "Activate" để kích hoạt workflow

### ✍️ Mẹo & gợi ý nâng cao
- Thêm cảnh báo qua Slack/Telegram bằng cách kết nối với các node tương ứng
- Tạo báo cáo tổng hợp giá hàng tháng/quý bằng cách thêm node xử lý dữ liệu
- Kết hợp với workflow khác để tự động đặt hàng khi giá đạt ngưỡng mong muốn
- Thiết lập cảnh báo giá giảm đột ngột (ví dụ: giảm 20% trong vòng 24h)

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm hàng giờ mỗi ngày trong việc theo dõi giá sản phẩm Amazon. Với khả năng tự động hóa toàn diện và cảnh báo tức thời, các sếp có thể tập trung vào những việc quan trọng hơn trong kinh doanh. Hãy thử ngay và bắt đầu tiết kiệm thời gian và tiền bạc!