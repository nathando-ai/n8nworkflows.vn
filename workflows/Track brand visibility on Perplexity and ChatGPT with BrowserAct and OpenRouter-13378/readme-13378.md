---
title: "🚀 Theo dõi sự hiện diện thương hiệu trên Perplexity và ChatGPT với BrowserAct và OpenRouter"
description: "Tự động hóa theo dõi sự hiện diện thương hiệu của bạn trên các công cụ tìm kiếm AI hàng tuần, phân tích kết quả và gửi báo cáo tự động đến Slack."
slug: "theo-doi-su-hien-dien-thuong-hieu-ai"
tags: [n8n, automation, no-code, AI, market-research]
keywords: [n8n workflow, tự động hóa, theo dõi thương hiệu, AI search, Perplexity, ChatGPT]
---

# 🚀 Theo dõi sự hiện diện thương hiệu trên Perplexity và ChatGPT với BrowserAct và OpenRouter

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp khi phải theo dõi thủ công sự hiện diện thương hiệu trên các công cụ tìm kiếm AI. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian theo dõi thủ công hàng tuần
- Phân tích tự động sự hiện diện thương hiệu trên Perplexity và ChatGPT
- Nhận báo cáo định kỳ với đánh giá về sự hiện diện và cảm xúc của thương hiệu
- Hoạt động liên tục 24/7 mà không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản BrowserAct với template **AI Search Visibility Tracker (Perplexity & ChatGPT)**
- API Key từ OpenRouter (đăng ký tại [OpenRouter](https://openrouter.ai/))
- Tài khoản Slack để nhận báo cáo
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/13378)
2. Click vào nút "Copy to Clipboard" để sao chép JSON workflow
3. Trong n8n Editor, click vào "Import from Clipboard" và dán JSON đã sao chép

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Add Brand & Description"**:
   - Cập nhật thông tin thương hiệu của bạn trong trường "Company Name"
   - Thêm mô tả chi tiết về sản phẩm/dịch vụ của bạn trong trường "Value Proposition"

2. **Node "OpenRouter Chat Model" và "OpenRouter Chat Model1"**:
   - Đảm bảo bạn đã tạo credentials "openRouterApi" trong n8n
   - Chọn model GPT-4 hoặc model khác phù hợp với nhu cầu của bạn

3. **Node "Run a Perplexity Search" và "Run ChatGPT Search"**:
   - Đảm bảo bạn đã tạo credentials "browserActApi" trong n8n
   - Kiểm tra template **AI Search Visibility Tracker (Perplexity & ChatGPT)** đã được lưu trong tài khoản BrowserAct của bạn

4. **Node "Send team update"**:
   - Đảm bảo bạn đã tạo credentials "slackApi" trong n8n
   - Chọn channel Slack phù hợp để nhận báo cáo

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong, click vào nút "Activate" để kích hoạt workflow
2. Để test workflow, bạn có thể chạy thử với nút "Execute Workflow"
3. Kiểm tra kết quả trên Slack để đảm bảo workflow hoạt động đúng

### ✍️ Mẹo & gợi ý nâng cao
1. **Tùy chỉnh tần suất báo cáo**: Thay đổi cài đặt trong node "Weekly Trigger" để nhận báo cáo theo tần suất khác (hàng ngày, hàng tháng...)
2. **Mở rộng phân tích**: Thêm các công cụ tìm kiếm AI khác vào workflow để có cái nhìn toàn diện hơn
3. **Tích hợp với các công cụ khác**: Kết nối workflow với Google Sheets để lưu trữ lịch sử báo cáo
4. **Tùy chỉnh báo cáo**: Chỉnh sửa prompt trong node "Analyze both results & generate report" để phù hợp với nhu cầu phân tích cụ thể của bạn

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian và công sức trong việc theo dõi sự hiện diện thương hiệu trên các công cụ tìm kiếm AI. Với khả năng tự động hóa hoàn toàn, các sếp có thể tập trung vào các chiến lược quan trọng hơn thay vì phải theo dõi thủ công hàng tuần. Hãy thử ngay và nâng cao khả năng cạnh tranh của thương hiệu trên thị trường AI!