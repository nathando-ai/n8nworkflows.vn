---
title: "🚀 Tự động thu thập đánh giá Trustpilot bằng Bright Data + Google Sheets"
description: "Hướng dẫn tự động hóa thu thập đánh giá từ Trustpilot bằng Bright Data và đồng bộ dữ liệu vào Google Sheets hoàn toàn không cần code"
slug: "tu-dong-thu-thap-danh-gia-trustpilot-bang-bright-data-google-sheets"
tags: [n8n, automation, no-code, web scraping, google sheets]
keywords: [n8n workflow, tự động hóa, web scraping, đánh giá Trustpilot, Bright Data]
---

# 🚀 Tự động thu thập đánh giá Trustpilot bằng Bright Data + Google Sheets

[Các sếp đang gặp khó khăn khi phải thu thập đánh giá từ Trustpilot thủ công? Workflow này sẽ giúp các sếp tự động hóa toàn bộ quy trình từ thu thập dữ liệu đến lưu trữ trong Google Sheets, hoàn toàn không cần code!]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa toàn bộ quy trình thu thập dữ liệu từ Trustpilot
- **Chính xác cao**: Sử dụng công nghệ web scraping của Bright Data để đảm bảo dữ liệu chính xác
- **Tích hợp liền mạch**: Đồng bộ dữ liệu trực tiếp vào Google Sheets của các sếp
- **Hoạt động liên tục**: Workflow có thể chạy tự động theo lịch hoặc theo yêu cầu
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Bright Data với API key
- Tài khoản Google với quyền truy cập Google Sheets
- URL của trang đánh giá Trustpilot cần thu thập
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/5145](https://n8n.io/workflows/5145)
2. Click vào nút "Import" ở góc trên bên phải
3. Chọn "Import from URL" và dán link trên vào ô nhập liệu
4. Click "OK" để hoàn tất import

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Form Trigger Node**:
   - Cấu hình trường `Trustpilot Website URL` để nhập URL trang đánh giá Trustpilot cần thu thập

2. **POST to Bright Data**:
   - Cấu hình credentials cho Bright Data
   - Đảm bảo dataset ID trong payload phù hợp với yêu cầu thu thập dữ liệu

3. **Google Sheets (Append)**:
   - Cấu hình credentials Google Sheets
   - Đảm bảo tên sheet là `Trustpilot`
   - Kiểm tra các trường dữ liệu được ánh xạ đúng với cấu trúc dữ liệu từ Bright Data

#### 3. Kích hoạt ⚡️
1. Test run workflow với URL mẫu để kiểm tra kết quả
2. Sau khi xác nhận kết quả, bật Active workflow để chạy tự động

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi thu thập dữ liệu hoàn tất
- Thiết lập lịch chạy tự động để thu thập dữ liệu định kỳ
- Tạo báo cáo tự động từ dữ liệu thu thập được trong Google Sheets
- Kết hợp với các công cụ phân tích dữ liệu khác để phân tích đánh giá khách hàng

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quy trình thu thập đánh giá từ Trustpilot, đồng thời lưu trữ dữ liệu vào Google Sheets một cách liền mạch. Với việc không cần code, các sếp có thể tập trung vào phân tích dữ liệu và đưa ra quyết định kinh doanh hiệu quả hơn. Hãy áp dụng ngay để tiết kiệm thời gian và nâng cao hiệu quả công việc!