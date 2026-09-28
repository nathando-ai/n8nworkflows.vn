---
title: "🚀 Theo dõi nhắc đến thương hiệu hàng ngày từ Hacker News đến Slack với phân tích cảm xúc GPT-4o-mini"
description: "Tự động hóa theo dõi nhắc đến thương hiệu hàng ngày từ Hacker News đến Slack với phân tích cảm xúc AI, tiết kiệm thời gian và nâng cao hiệu quả giám sát thương hiệu"
slug: "theo-doi-nhac-den-thuong-hieu-hacker-news-slack-gpt4o-mini"
tags: [n8n, automation, no-code, slack, ai, market-research, ai-summarization]
keywords: [n8n workflow, tự động hóa, giám sát thương hiệu, phân tích cảm xúc, Hacker News, Slack]
---

# 🚀 Theo dõi nhắc đến thương hiệu hàng ngày từ Hacker News đến Slack với phân tích cảm xúc GPT-4o-mini

[Các sếp] có bao giờ phải mất hàng giờ mỗi ngày để theo dõi nhắc đến thương hiệu trên các diễn đàn công nghệ như Hacker News? Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình theo dõi, phân tích và báo cáo nhắc đến thương hiệu chỉ trong vài phút mỗi ngày.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa quy trình theo dõi nhắc đến thương hiệu hàng ngày
- **Phân tích cảm xúc**: Sử dụng AI GPT-4o-mini để phân tích cảm xúc, chủ đề và mức độ quan trọng của mỗi nhắc đến
- **Báo cáo tự động**: Nhận báo cáo hàng ngày trên Slack với thông tin tổng hợp về nhắc đến thương hiệu
- **Giám sát liên tục**: Theo dõi nhắc đến thương hiệu 24/7 mà không cần can thiệp thủ công
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Slack với quyền gửi tin nhắn đến kênh
- API Key từ OpenAI để sử dụng GPT-4o-mini
- Thương hiệu và từ khóa cần theo dõi
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/11080](https://n8n.io/workflows/11080)
2. Click vào nút "Import" để tải xuống file JSON
3. Trong n8n Editor, chọn "Import from File" và chọn file JSON vừa tải xuống

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Every Day at 09:00"**:
   - Đảm bảo thời gian chạy phù hợp với nhu cầu của các sếp

2. **Node "Brand Config"**:
   - Cập nhật tên thương hiệu và từ khóa cần theo dõi trong trường "brandName" và "keywords"

3. **Node "Send Daily Report to Slack" và "Send No Mentions to Slack"**:
   - Thêm credentials Slack và chọn kênh để gửi báo cáo
   - Đảm bảo bot Slack có quyền gửi tin nhắn đến kênh đã chọn

4. **Node "OpenAI Chat Model - GPT-4o-mini"**:
   - Thêm credentials OpenAI
   - Đảm bảo tài khoản OpenAI có đủ credit để sử dụng GPT-4o-mini

5. **Node "Slack: Send Error Alert"**:
   - Thêm credentials Slack OAuth2
   - Chọn kênh để nhận thông báo lỗi

#### 3. Kích hoạt ⚡️
1. Chạy thử với dữ liệu mẫu để kiểm tra định dạng và nội dung báo cáo
2. Bật chế độ Active workflow để bắt đầu theo dõi nhắc đến thương hiệu hàng ngày

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với các công cụ khác như Google Sheets để lưu trữ lịch sử nhắc đến thương hiệu
- Thêm bước gửi báo cáo qua email để các thành viên không sử dụng Slack cũng có thể theo dõi
- Tùy chỉnh prompt trong node "AI Agent - Classify Mention Sentiments" để phù hợp với nhu cầu phân tích cụ thể
- Thiết lập báo cáo định kỳ hàng tuần hoặc hàng tháng để đánh giá xu hướng nhắc đến thương hiệu

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quy trình theo dõi nhắc đến thương hiệu từ Hacker News đến Slack với phân tích cảm xúc AI. Với việc triển khai workflow này, các sếp có thể tiết kiệm hàng giờ mỗi ngày và nhận được thông tin tổng hợp về nhắc đến thương hiệu một cách nhanh chóng và chính xác. Hãy áp dụng ngay để nâng cao hiệu quả giám sát thương hiệu của các sếp!