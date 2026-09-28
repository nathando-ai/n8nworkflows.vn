---
title: "🚀 Tự động thu thập dữ liệu TikTok từ từ khóa bằng n8n + Bright Data"
description: "Hướng dẫn tự động hóa thu thập dữ liệu TikTok từ từ khóa bằng n8n, Bright Data và Google Sheets - tiết kiệm 80% thời gian làm thủ công"
slug: "tu-dong-thu-thap-du-lieu-tiktok-tu-khoa-bang-n8n"
tags: [n8n, automation, no-code, Bright Data, Google Sheets]
keywords: [n8n workflow, tự động hóa, thu thập dữ liệu TikTok, Bright Data, Google Sheets]
---

# 🚀 Tự động thu thập dữ liệu TikTok từ từ khóa bằng n8n + Bright Data

[Các sếp đang gặp khó khăn khi phải thu thập dữ liệu TikTok từ từ khóa một cách thủ công? Workflow này sẽ giúp các sếp tự động hóa toàn bộ quy trình từ tìm kiếm đến lưu trữ dữ liệu chỉ trong vài phút!]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 80% thời gian thu thập dữ liệu thủ công
- Tự động hóa toàn bộ quy trình từ tìm kiếm đến lưu trữ
- Lấy dữ liệu chi tiết về bài đăng TikTok bao gồm metrics và thông tin profile
- Hoạt động liên tục 24/7 mà không cần can thiệp
- Dữ liệu được lưu trữ tự động vào Google Sheets
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Bright Data với API key
- Tài khoản Google với quyền truy cập Google Sheets
- Dataset ID từ Bright Data (để thực hiện scraping TikTok)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấn vào "Import from URL" và dán link sau: `https://n8n.io/workflows/5153`
3. Hoặc tải file JSON từ [đây](https://n8n.io/workflows/5153) và import thủ công

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Form Trigger Node**:
   - Cấu hình form để nhận input từ người dùng (từ khóa tìm kiếm TikTok)
   - Đảm bảo form có trường nhập liệu cho từ khóa

2. **HTTP Request (Trigger Scraping on Bright Data)**:
   - Thêm credentials cho Bright Data
   - Cập nhật Dataset ID trong request body
   - Đảm bảo API key của Bright Data được nhập chính xác

3. **Snapshot Progress Check**:
   - Kiểm tra endpoint và headers của Bright Data
   - Đảm bảo snapshot_id được truyền đúng từ node trước đó

4. **Google Sheets Node**:
   - Thêm credentials cho Google Sheets
   - Cấu hình Spreadsheet ID và tên sheet cần lưu dữ liệu
   - Đảm bảo cấu trúc dữ liệu đầu ra từ Bright Data khớp với cột trong Google Sheets

#### 3. Kích hoạt ⚡️
1. Test run với từ khóa mẫu (ví dụ: "marketing")
2. Kiểm tra dữ liệu được lưu vào Google Sheets
3. Bật Active workflow để chạy tự động

### ✍️ Mẹo & gợi ý nâng cao
1. Thêm node gửi thông báo Slack/Telegram khi quá trình hoàn thành
2. Tạo bản sao dữ liệu định kỳ vào Google Drive
3. Kết hợp với workflow phân tích dữ liệu để tạo báo cáo tự động
4. Thiết lập lịch chạy định kỳ cho các từ khóa quan trọng

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm hàng giờ mỗi ngày trong việc thu thập dữ liệu TikTok từ từ khóa. Với việc tự động hóa toàn bộ quy trình, các sếp có thể tập trung vào phân tích dữ liệu và đưa ra quyết định chiến lược hiệu quả hơn. Hãy thử ngay và trải nghiệm sự khác biệt!