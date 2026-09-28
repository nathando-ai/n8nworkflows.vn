---
title: "📈 Tự động hóa Phân tích Thị trường Chứng khoán với AI Perplexity, GPT-4 và Google Sheets"
description: "Hướng dẫn tự động hóa phân tích thị trường chứng khoán hàng ngày với n8n, kết hợp AI Perplexity và GPT-4 để cung cấp thông tin chuyên sâu về danh mục đầu tư của bạn."
slug: "tu-dong-hoa-phan-tich-thi-truong-chung-khoan-voi-ai-perplexity-gpt-4-google-sheets"
tags: [n8n, automation, no-code, ai, financial-analysis]
keywords: [n8n workflow, tự động hóa tài chính, phân tích thị trường, AI chứng khoán, Google Sheets]
---

# 📈 Tự động hóa Phân tích Thị trường Chứng khoán với AI Perplexity, GPT-4 và Google Sheets

[Các sếp] có thể đã từng phải mất hàng giờ mỗi ngày để theo dõi thị trường chứng khoán, kiểm tra danh mục đầu tư và tìm kiếm thông tin liên quan. Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình này trong vòng vài phút!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Nhận báo cáo thị trường hàng ngày chỉ với 1 click
- **Chính xác**: Dữ liệu được cập nhật tự động từ các nguồn đáng tin cậy
- **Cá nhân hóa**: Phân tích được điều chỉnh theo danh mục đầu tư của từng cá nhân
- **Hoạt động liên tục**: Nhận thông tin mới nhất ngay cả khi các sếp không trực tuyến
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với Google Sheets đã kích hoạt API
- API Key từ OpenAI (cho GPT-4)
- API Key từ Perplexity
- Bot Telegram và Chat ID (hoặc có thể thay thế bằng Slack, Email...)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/5783](https://n8n.io/workflows/5783)
2. Click vào nút "Import" ở góc trên bên phải
3. Đăng nhập vào tài khoản n8n của bạn (nếu chưa có, hãy tạo mới)
4. Chọn "Import from URL" và dán link workflow vào

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Schedule Trigger"**:
   - Thiết lập thời gian chạy hàng ngày (mặc định 10 AM)
   - Có thể thay đổi theo múi giờ của các sếp

2. **Node "OpenAI Chat Model"**:
   - Tạo credentials mới với tên "openAiApi"
   - Nhập API Key từ OpenAI
   - Đảm bảo chọn model "gpt-4.1"

3. **Node "Portfolio Holdings"**:
   - Tạo credentials mới với tên "googleSheetsOAuth2Api"
   - Kết nối với tài khoản Google của các sếp
   - Cấu hình Sheet ID và tên Sheet chứa danh mục đầu tư

4. **Node "Perplexity"**:
   - Tạo credentials mới với tên "perplexityApi"
   - Nhập API Key từ Perplexity
   - Đảm bảo chọn model "sonar-pro"

5. **Node "Telegram"**:
   - Tạo credentials mới với tên "telegramApi"
   - Nhập Bot Token và Chat ID
   - Có thể thay thế bằng Slack, Email hoặc bất kỳ công cụ nào khác được hỗ trợ bởi n8n

#### 3. Kích hoạt ⚡️
1. Click vào nút "Execute Node" để kiểm tra kết nối và dữ liệu đầu ra
2. Sau khi tất cả các node đều hoạt động bình thường, click vào nút "Activate" để kích hoạt workflow

### ✍️ Mẹo & gợi ý nâng cao
1. **Tùy chỉnh báo cáo**: Thay đổi prompt trong node "Stock Market News & Analytics Agent" để nhận thông tin theo nhu cầu cụ thể
2. **Nhiều danh mục đầu tư**: Tạo nhiều node "Portfolio Holdings" cho các danh mục khác nhau và kết hợp chúng trong node "Stock Market News & Analytics Agent"
3. **Báo cáo định kỳ**: Thay đổi node "Schedule Trigger" để nhận báo cáo hàng tuần hoặc hàng tháng
4. **Kết hợp với các công cụ khác**: Thêm node để lưu báo cáo vào Google Drive, Notion hoặc bất kỳ nền tảng nào khác

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quá trình phân tích thị trường chứng khoán hàng ngày, từ thu thập dữ liệu đến tạo báo cáo chuyên nghiệp. Với sự kết hợp của AI Perplexity và GPT-4, các sếp sẽ nhận được thông tin chính xác và cá nhân hóa về danh mục đầu tư của mình. Hãy áp dụng ngay để tiết kiệm thời gian và nâng cao hiệu quả đầu tư!