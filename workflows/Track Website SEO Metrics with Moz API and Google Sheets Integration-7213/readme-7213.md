---
title: "🚀 Theo dõi chỉ số SEO Website với Moz API và Google Sheets - Tự động hóa hoàn toàn"
description: "Hướng dẫn tự động hóa việc theo dõi chỉ số SEO như Domain Authority (DA), Page Authority (PA) của website bằng Moz API và lưu kết quả vào Google Sheets - không cần code"
slug: "theo-doi-chi-so-seo-website-voi-moz-api-va-google-sheets"
tags: [n8n, automation, no-code, seo, google-sheets]
keywords: [n8n workflow, tự động hóa, seo, domain authority, page authority]
---

# 🚀 Theo dõi chỉ số SEO Website với Moz API và Google Sheets - Tự động hóa hoàn toàn

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa toàn bộ quy trình theo dõi SEO
- Chính xác: Lấy dữ liệu trực tiếp từ Moz API - nguồn tin cậy hàng đầu
- Cá nhân hóa: Lưu kết quả vào Google Sheets theo định dạng tùy chỉnh
- Hoạt động liên tục: Theo dõi chỉ số SEO 24/7 mà không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Cloud với quyền truy cập Google Sheets API
- API Key từ Moz API (có thể lấy từ RapidAPI)
- Google Sheet đã tạo sẵn với các cột: Website, DA, PA, Spam Score, DR, Organic Traffic
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấn vào "Import from URL" và dán link: https://n8n.io/workflows/7213
3. Hoặc tải file JSON từ link trên và import thủ công

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "On form submission"**:
   - Cấu hình form để nhận trường "website" chứa URL cần kiểm tra
   - Bạn có thể tùy chỉnh giao diện form theo nhu cầu

2. **Node "DA PA API Request"**:
   - Thêm credentials cho Moz API (hoặc RapidAPI)
   - Đảm bảo endpoint API là: `https://moz.com/api/url-metrics`
   - Thêm header: `Content-Type: application/json`
   - Thêm body JSON:
     ```json
     {
       "targets": "{{$node["On form submission"].json["website"]}}",
       "access_id": "YOUR_MOZ_ACCESS_ID",
       "secret_key": "YOUR_MOZ_SECRET_KEY"
     }
     ```

3. **Node "Google Sheets"**:
   - Thêm credentials Google API
   - Chọn Spreadsheet ID của Google Sheet bạn đã tạo
   - Đặt tên Sheet (Sheet Name) và phạm vi (Range) để lưu dữ liệu
   - Đảm bảo các cột trong Google Sheet khớp với dữ liệu trả về từ API

#### 3. Kích hoạt ⚡️
- Test run với URL mẫu (ví dụ: https://n8n.io)
- Kiểm tra kết quả trong Google Sheet
- Bật Active workflow để chạy tự động khi có form submission

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node gửi email báo cáo khi chỉ số SEO thay đổi đáng kể
- Kết hợp với Slack để thông báo ngay khi có dữ liệu mới
- Tạo biểu đồ tự động trong Google Sheets từ dữ liệu thu thập
- Thiết lập lịch chạy định kỳ thay vì chỉ chạy khi có form submission

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian đáng kể trong việc theo dõi chỉ số SEO quan trọng. Bằng cách tự động hóa quy trình này, bạn có thể tập trung vào việc phân tích dữ liệu và đưa ra quyết định chiến lược hơn là phải làm thủ công. Hãy thử ngay và nâng cấp chiến lược SEO của bạn với dữ liệu chính xác và cập nhật liên tục!