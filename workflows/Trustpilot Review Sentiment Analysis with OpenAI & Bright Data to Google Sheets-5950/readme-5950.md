---
title: "🚀 Tự động hóa phân tích cảm xúc đánh giá Trustpilot với OpenAI & Bright Data lên Google Sheets"
description: "Hướng dẫn tự động hóa 100% không cần code để thu thập, phân tích cảm xúc và lưu trữ đánh giá khách hàng từ Trustpilot lên Google Sheets"
slug: "tu-dong-hoa-phan-tich-cam-xuc-trustpilot-openai-brightdata-google-sheets"
tags: [n8n, automation, no-code, trustpilot, google-sheets]
keywords: [n8n workflow, tự động hóa đánh giá, phân tích cảm xúc, bright data, openai]
---

# 🚀 Tự động hóa phân tích cảm xúc đánh giá Trustpilot với OpenAI & Bright Data lên Google Sheets

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp thường phải đối mặt với tình trạng thu thập đánh giá khách hàng từ các trang đánh giá như Trustpilot một cách thủ công. Quá trình này tốn thời gian, dễ bị lỗi và không thể tự động hóa theo dõi. Workflow này sẽ giúp các sếp tự động hóa toàn bộ quy trình từ thu thập đánh giá đến phân tích cảm xúc và lưu trữ dữ liệu lên Google Sheets.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa toàn bộ quy trình từ 30 phút xuống còn vài giây
- Phân tích cảm xúc chính xác: Sử dụng công nghệ AI của OpenAI để phân tích cảm xúc của đánh giá
- Dữ liệu được lưu trữ sạch sẽ: Mỗi đánh giá được lưu trữ thành một dòng trong Google Sheets
- Theo dõi liên tục: Có thể chạy định kỳ để cập nhật đánh giá mới nhất
- Dễ tích hợp: Dữ liệu có thể được sử dụng cho các báo cáo và dashboard khác
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google để truy cập Google Sheets
- API Key từ OpenAI để sử dụng các tính năng AI
- Tài khoản Bright Data để sử dụng công cụ scraper
- URL của trang đánh giá Trustpilot cần phân tích
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Để import workflow, các sếp có thể làm theo các bước sau:

1. Truy cập vào trang [n8n.io/workflows/5950](https://n8n.io/workflows/5950)
2. Nhấn vào nút "Download" để tải file JSON của workflow
3. Trong n8n Editor, nhấn vào nút "Import from File" và chọn file JSON vừa tải về
4. Hoặc, các sếp có thể copy toàn bộ nội dung JSON từ trang và paste vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Set Trustpilot company URL** (Node: set)
   - Cần cấu hình URL của trang đánh giá Trustpilot cần phân tích

2. **Bright Data MCP Scrapper** (Node: mcpClientTool)
   - Cần cấu hình credentials cho Bright Data MCP
   - Đảm bảo tài khoản Bright Data có đủ credit để sử dụng công cụ scraper

3. **Chat Model** (Node: lmChatOpenAi)
   - Cần cấu hình credentials cho OpenAI API
   - Đảm bảo tài khoản OpenAI có đủ credit để sử dụng các model AI

4. **Save Reviews to Google Sheets** (Node: googleSheets)
   - Cần cấu hình credentials cho Google Sheets OAuth2
   - Chỉ định tên sheet và phạm vi dữ liệu cần lưu trữ

5. **Manual Start** (Node: manualTrigger)
   - Node này dùng để kích hoạt workflow thủ công
   - Các sếp có thể cấu hình để chạy workflow theo lịch trình tự động

#### 3. Kích hoạt ⚡️
Sau khi đã cấu hình các node quan trọng, các sếp cần thực hiện các bước sau:

1. Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng
2. Nhấn vào nút "Activate" để kích hoạt workflow
3. Kiểm tra kết quả trên Google Sheets để đảm bảo dữ liệu được lưu trữ đúng

### ✍️ Mẹo & gợi ý nâng cao
- Các sếp có thể kết hợp workflow này với Slack hoặc Telegram để nhận thông báo khi có đánh giá mới
- Có thể lưu log các lần chạy workflow để theo dõi lịch sử thay đổi
- Có thể cấu hình để gửi báo cáo định kỳ về tình hình đánh giá khách hàng
- Có thể mở rộng để phân tích cảm xúc từ nhiều trang đánh giá khác nhau

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện để tự động hóa quá trình phân tích đánh giá khách hàng từ Trustpilot. Với công nghệ AI của OpenAI và công cụ scraper của Bright Data, các sếp có thể thu thập, phân tích và lưu trữ dữ liệu một cách nhanh chóng và chính xác. Hãy áp dụng ngay để tiết kiệm thời gian và nâng cao chất lượng dịch vụ của doanh nghiệp!