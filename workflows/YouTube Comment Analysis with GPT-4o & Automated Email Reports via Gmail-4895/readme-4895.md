---
title: "🚀 Phân tích bình luận YouTube tự động với GPT-4o và báo cáo email qua Gmail"
description: "Tự động hóa phân tích bình luận YouTube bằng AI và gửi báo cáo email hàng ngày với n8n - tiết kiệm thời gian và tăng hiệu quả marketing"
slug: "phan-tich-binh-luan-youtube-tu-dong-voi-gpt-4o-va-bao-cao-email"
tags: [n8n, automation, no-code, AI, marketing]
keywords: [n8n workflow, tự động hóa, phân tích bình luận, báo cáo email, marketing]
---

# 🚀 Phân tích bình luận YouTube tự động với GPT-4o và báo cáo email qua Gmail

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp thường phải đối mặt với hàng trăm bình luận trên video YouTube mỗi ngày, nhưng phân tích thủ công tốn thời gian và dễ bỏ sót. Workflow này sẽ giúp tự động hóa toàn bộ quy trình: lấy bình luận, phân tích bằng AI và gửi báo cáo email hàng ngày - tất cả chỉ với một workflow n8n đơn giản.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 80% thời gian phân tích bình luận
- Phân tích sâu sắc với AI GPT-4o
- Báo cáo email tự động hàng ngày
- Theo dõi hiệu suất video liên tục
- Tăng cường tương tác với khán giả
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Cloud với API YouTube Data v3
- Tài khoản Azure OpenAI với GPT-4o
- Tài khoản Gmail để gửi báo cáo
- Google Sheet để lưu trữ dữ liệu video
- API Key từ Google Cloud Console
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/4895)
2. Click "Copy to clipboard" để sao chép JSON workflow
3. Trong n8n Editor, click "Import from Clipboard" và dán JSON

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

**Node "Pick Video Ids from Google sheet"**:
- Cấu hình Google Sheets Trigger:
  - Chọn Google Sheets credentials đã tạo
  - Nhập ID của Google Sheet chứa danh sách video
  - Chỉ định phạm vi dữ liệu (ví dụ: Sheet1!A2:A)

**Node "Get Youtube Video Details"**:
- Cấu hình YouTube node:
  - Chọn YouTube credentials đã tạo
  - Chọn operation "Get Video Details"
  - Thêm tham số videoId từ output của node trước

**Node "Get Youtube Video Comments"**:
- Cấu hình HTTP Request node:
  - Method: GET
  - URL: `https://www.googleapis.com/youtube/v3/commentThreads`
  - Query Parameters:
    - part: snippet
    - videoId: `{{$node["Get Youtube Video Details"].json.videoId}}`
    - key: `{{$credentials.youtubeOAuth2Api.apiKey}}`
    - maxResults: 100

**Node "AI Agent"**:
- Cấu hình Agent node:
  - Chọn Azure OpenAI credentials đã tạo
  - Model: gpt-4o
  - System Prompt:
    ```text
    You are a YouTube comment analyzer. Analyze the following comments and provide:
    1. Overall sentiment (positive/negative/neutral)
    2. Top 3 most common topics
    3. Any actionable insights
    4. Suggested responses to negative comments
    ```

**Node "Gmail Account Configuration"**:
- Cấu hình Gmail node:
  - Chọn Gmail credentials đã tạo
  - Chọn operation "Send Email"
  - Điền thông tin email:
    - To: `{{$node["Get Youtube Video Details"].json.channelTitle}}`
    - Subject: `YouTube Video Analysis Report - {{$node["Get Youtube Video Details"].json.title}}`
    - Body: `{{$node["Prepare HTML for Email"].json.htmlContent}}`

#### 3. Kích hoạt ⚡️
1. Test run với một video mẫu
2. Kiểm tra email báo cáo
3. Bật Active workflow

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack để nhận thông báo tức thời
- Thêm node để lưu log phân tích vào Google Sheets
- Tự động gửi báo cáo hàng tuần thay vì hàng ngày
- Phát triển workflow để tự động trả lời bình luận tích cực/tiêu cực
- Kết nối với Google Analytics để phân tích tương tác toàn diện

### 📌 Kết luận
Workflow này sẽ giúp các sếp tiết kiệm hàng giờ mỗi ngày trong việc phân tích bình luận YouTube. Bằng cách kết hợp sức mạnh của AI và tự động hóa, các sếp có thể đưa ra quyết định nhanh hơn và tăng cường tương tác với khán giả. Hãy thử ngay và xem kết quả thay đổi!