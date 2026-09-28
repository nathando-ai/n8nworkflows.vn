---
title: "🚀 Tự động theo dõi cảm xúc khu vực từ mạng xã hội với Bright Data & OpenAI"
description: "Hướng dẫn tự động hóa quy trình thu thập và phân tích cảm xúc từ bài đăng thời tiết trên Yelp bằng n8n, Bright Data và OpenAI"
slug: "tu-dong-theo-doi-cam-xuc-khu-vuc-tu-mang-xa-hoi"
tags: [n8n, automation, no-code, Bright Data, OpenAI, Market Research, AI Summarization]
keywords: [n8n workflow, tự động hóa, phân tích cảm xúc, Bright Data, OpenAI, Yelp, Trello]
---

# 🚀 Tự động theo dõi cảm xúc khu vực từ mạng xã hội với Bright Data & OpenAI

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian thu thập dữ liệu từ Yelp
- Phân tích cảm xúc tự động từ bài đăng thời tiết
- Tạo thẻ Trello tự động cho chiến dịch marketing
- Dữ liệu được cấu trúc sẵn sàng cho phân tích tiếp theo
- Tự động hóa hoàn toàn quy trình từ thu thập đến báo cáo
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản OpenAI API (để sử dụng các model GPT)
- Tài khoản Bright Data (để sử dụng MCP Client)
- Tài khoản Trello (để tạo thẻ chiến dịch)
- URL của trang Yelp chứa bài đăng thời tiết (ví dụ: https://www.yelp.com/)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/5973](https://n8n.io/workflows/5973)
2. Nhấn nút "Import" trên trang workflow
3. Hoặc copy JSON workflow và dán vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "🔘 Trigger: Execute Workflow"**:
   - Không cần cấu hình gì, chỉ cần nhấn "Execute" khi muốn chạy workflow

2. **Node "🌐 Set Yelp URL (Weather Posts - Los Angeles)"**:
   - Thay đổi URL trong node này thành URL thực tế của trang Yelp bạn muốn thu thập dữ liệu

3. **Node "💬 AI Model" và "OpenAI Chat Model"**:
   - Cấu hình credentials OpenAI API
   - Đảm bảo chọn model phù hợp (gpt-4.1-mini hoặc các model khác)

4. **Node "🌐 MCP Client: Scrape Weather Posts Data"**:
   - Cấu hình credentials Bright Data MCP Client
   - Đảm bảo đã cài đặt và cấu hình Bright Data MCP Client trong n8n

5. **Node "🤖 AI Agent: Scrape Yelp Weather Posts and tailor campaigns"**:
   - Không cần cấu hình gì, node này sẽ tự động xử lý dữ liệu từ các node trước

6. **Node "📋 Create Trello Card for Weather Campaign"**:
   - Cấu hình credentials Trello
   - Chọn board và list phù hợp trong Trello để lưu thẻ chiến dịch

#### 3. Kích hoạt ⚡️
1. Test run workflow với dữ liệu mẫu
2. Kiểm tra kết quả trên Trello để đảm bảo thẻ được tạo đúng
3. Bật Active workflow sau khi đã kiểm tra và cấu hình đầy đủ

### ✍️ Mẹo & gợi ý nâng cao
1. **Lập lịch chạy workflow**: Sử dụng node "Schedule Trigger" để tự động chạy workflow theo lịch định kỳ
2. **Kết hợp với Slack/Teams**: Thêm node gửi thông báo đến Slack/Teams khi workflow hoàn thành
3. **Lưu log hoạt động**: Thêm node lưu log hoạt động vào Google Sheets hoặc cơ sở dữ liệu
4. **Phân tích dữ liệu nâng cao**: Kết nối với các công cụ phân tích dữ liệu như Tableau hoặc Power BI

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quy trình thu thập và phân tích cảm xúc từ bài đăng thời tiết trên Yelp. Bằng cách sử dụng Bright Data để thu thập dữ liệu và OpenAI để phân tích cảm xúc, workflow này cung cấp thông tin quan trọng để tối ưu hóa chiến dịch marketing của bạn. Hãy áp dụng ngay để tiết kiệm thời gian và nâng cao hiệu quả kinh doanh!