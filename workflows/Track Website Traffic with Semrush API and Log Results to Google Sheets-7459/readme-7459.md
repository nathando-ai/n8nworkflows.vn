---
title: "🚀 Theo dõi lưu lượng truy cập website với Semrush API và lưu kết quả vào Google Sheets"
description: "Hướng dẫn tự động hóa việc theo dõi lưu lượng truy cập website thông qua Semrush API và lưu kết quả vào Google Sheets với n8n, tiết kiệm thời gian và nâng cao hiệu quả SEO."
slug: "theo-doi-luu-luong-truy-cap-website-voi-semrush-va-google-sheets"
tags: [n8n, automation, no-code, seo, market-research]
keywords: [n8n workflow, tự động hóa, theo dõi website, Semrush API, Google Sheets]
---

# 🚀 Theo dõi lưu lượng truy cập website với Semrush API và lưu kết quả vào Google Sheets

[Các sếp] có bao giờ phải theo dõi thủ công lưu lượng truy cập của nhiều website không? Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình từ nhập URL đến lưu kết quả vào Google Sheets chỉ trong vài bước đơn giản.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa quy trình theo dõi lưu lượng truy cập hàng ngày
- Chính xác: Dữ liệu được lấy trực tiếp từ Semrush API
- Cá nhân hóa: Có thể theo dõi nhiều website khác nhau
- Hoạt động liên tục: Workflow chạy tự động 24/7 mà không cần can thiệp
- Dễ dàng quản lý: Tất cả dữ liệu được lưu trữ trong Google Sheets
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google để truy cập Google Sheets
- API Key từ Semrush (đăng ký tại [Semrush](https://www.semrush.com/))
- Google Sheets đã tạo sẵn với cấu trúc phù hợp
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/7459](https://n8n.io/workflows/7459)
2. Click vào nút "Import" ở góc trên bên phải
3. Chọn "Import from URL" và dán link trên vào ô nhập liệu
4. Click "OK" để hoàn tất import

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "On form submission"**:
   - Cấu hình form để nhận URL của website cần theo dõi
   - Đảm bảo form có trường nhập liệu cho URL

2. **Node "Check webTraffic"**:
   - Thêm credentials cho Semrush API
   - Cấu hình request URL: `https://api.semrush.com/analytics/v1`
   - Thêm các headers cần thiết:
     ```
     Content-Type: application/json
     X-Api-Key: {{your_semrush_api_key}}
     ```
   - Thêm body request:
     ```json
     {
       "url": "{{$node["On form submission"].json["url"]}}"
     }
     ```

3. **Node "Re format output"**:
   - Sử dụng JavaScript để trích xuất và định dạng dữ liệu từ response của Semrush
   - Ví dụ mã xử lý:
     ```javascript
     const data = $input.all()[0].json;
     return {
       url: data.url,
       traffic: data.traffic,
       rank: data.rank,
       keywords: data.keywords,
       timestamp: new Date().toISOString()
     };
     ```

4. **Node "Google Sheets"**:
   - Thêm credentials cho Google API
   - Chọn Spreadsheet ID của Google Sheets cần lưu dữ liệu
   - Đặt tên Sheet Name (ví dụ: "Website Traffic")
   - Cấu hình các cột dữ liệu tương ứng với dữ liệu đầu ra từ node trước

#### 3. Kích hoạt ⚡️
1. Test workflow với URL mẫu (ví dụ: "https://example.com")
2. Kiểm tra dữ liệu đã được lưu đúng vào Google Sheets
3. Bật Active workflow để chạy tự động khi có form submission

### ✍️ Mẹo & gợi ý nâng cao
1. Thêm node gửi email báo cáo hàng tuần với dữ liệu từ Google Sheets
2. Kết hợp với Slack để thông báo khi lưu lượng truy cập vượt ngưỡng đặt trước
3. Tự động hóa việc theo dõi nhiều website cùng lúc bằng cách sử dụng vòng lặp
4. Thêm chức năng lưu ảnh chụp màn hình website để theo dõi thiết kế và nội dung

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian đáng kể trong việc theo dõi lưu lượng truy cập website. Bằng cách tự động hóa quy trình này, các sếp có thể tập trung vào phân tích dữ liệu và đưa ra quyết định chiến lược hiệu quả hơn. Hãy thử ngay và nâng cao hiệu quả SEO của các website quan trọng!