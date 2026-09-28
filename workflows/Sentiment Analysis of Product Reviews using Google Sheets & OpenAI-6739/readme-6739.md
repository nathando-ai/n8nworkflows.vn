---
title: "🚀 Phân tích cảm xúc đánh giá sản phẩm bằng Google Sheets & OpenAI - Workflow n8n tự động hóa"
description: "Tự động phân tích cảm xúc đánh giá sản phẩm từ Google Sheets bằng OpenAI, cập nhật kết quả trực tiếp vào bảng tính - Giải pháp tối ưu hóa thời gian và chính xác cho quản lý sản phẩm"
slug: "phan-tich-cam-xuc-danh-gia-san-pham-google-sheets-openai"
tags: [n8n, automation, no-code, google-sheets, openai, ai, sentiment-analysis]
keywords: [n8n workflow, tự động hóa, phân tích cảm xúc, đánh giá sản phẩm, google sheets, openai]
---

# 🚀 Phân tích cảm xúc đánh giá sản phẩm bằng Google Sheets & OpenAI - Workflow n8n tự động hóa

[Các sếp đang gặp khó khăn khi phải phân tích hàng trăm đánh giá sản phẩm thủ công? Workflow này sẽ giúp các sếp tự động hóa toàn bộ quy trình từ Google Sheets đến OpenAI, tiết kiệm thời gian và nâng cao hiệu quả quản lý sản phẩm.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động phân tích cảm xúc đánh giá sản phẩm ngay khi có đánh giá mới
- Cập nhật kết quả trực tiếp vào Google Sheets, dễ theo dõi và quản lý
- Tiết kiệm thời gian đáng kể so với phân tích thủ công
- Nâng cao hiệu quả quản lý sản phẩm với dữ liệu chính xác và cập nhật liên tục
- Hỗ trợ ra quyết định kinh doanh dựa trên phân tích dữ liệu khách hàng
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với Google Sheets đã kích hoạt API
- Tài khoản OpenAI với API key
- Bảng tính Google Sheets chứa cột đánh giá sản phẩm
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor
2. Nhấn vào "Import from URL" và dán link: https://n8n.io/workflows/6739
3. Hoặc tải file JSON về và import từ local

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Google Sheets Trigger**:
   - Chọn credentials: `googleSheetsTriggerOAuth2Api`
   - Cấu hình Spreadsheet ID và Sheet Name chứa đánh giá sản phẩm

2. **OpenAI Chat Model**:
   - Chọn credentials: `openAiApi`
   - Đảm bảo đã chọn model `gpt-4o-mini` (hoặc model khác phù hợp)

3. **Updated Sentiment of Product Review**:
   - Chọn credentials: `googleSheetsOAuth2Api`
   - Cấu hình Spreadsheet ID và Sheet Name để lưu kết quả phân tích

#### 3. Kích hoạt ⚡️
- Test run với dữ liệu mẫu để kiểm tra kết quả
- Bật Active workflow sau khi đã cấu hình đầy đủ

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để thông báo khi có đánh giá tiêu cực
- Lưu log phân tích để theo dõi xu hướng cảm xúc theo thời gian
- Tự động gửi báo cáo hàng tuần về xu hướng đánh giá sản phẩm
- Kết hợp với các công cụ khác như Google Analytics để có cái nhìn toàn diện về khách hàng

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quy trình phân tích cảm xúc đánh giá sản phẩm, từ thu thập dữ liệu đến cập nhật kết quả. Với việc tích hợp Google Sheets và OpenAI, các sếp có thể dễ dàng theo dõi và quản lý đánh giá sản phẩm một cách hiệu quả. Hãy áp dụng ngay để nâng cao hiệu quả kinh doanh của doanh nghiệp!