---
title: "🚀 Tự động hóa nội dung: Tóm tắt RSS + Tạo ảnh AI + Đăng lên WordPress & MXH"
description: "Workflow n8n tự động hóa 100% không cần code giúp tóm tắt tin tức từ RSS, tạo ảnh AI và đăng lên WordPress cùng các mạng xã hội. Tiết kiệm 90% thời gian quản lý nội dung."
slug: "tu-dong-hoa-tom-tat-rss-tao-anh-ai-dang-wordpress-mxh"
tags: [n8n, automation, no-code, wordpress, social-media]
keywords: [n8n workflow, tự động hóa nội dung, AI tạo ảnh, đăng tự động MXH, tóm tắt tin tức]
---

# 🚀 Tự động hóa nội dung: Tóm tắt RSS + Tạo ảnh AI + Đăng lên WordPress & MXH

[Các sếp] có biết rằng việc quản lý nội dung trên nhiều kênh truyền thông khác nhau đang tốn đến 90% thời gian làm việc của các chuyên viên nội dung? Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình từ việc lấy tin tức từ RSS, tóm tắt nội dung, tạo ảnh AI đến đăng lên WordPress và các mạng xã hội lớn như Facebook, LinkedIn, Instagram...

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa toàn bộ quy trình từ 30-60 phút xuống còn vài giây
- **Nội dung chuyên nghiệp**: Tóm tắt thông minh từ OpenAI + ảnh AI sinh ra từ mô tả
- **Đa kênh truyền thông**: Đăng tự động lên WordPress, Facebook, LinkedIn, Instagram, Telegram
- **Tự động hóa liên tục**: Workflow chạy 24/7 mà không cần can thiệp thủ công
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản WordPress với quyền quản trị
- API keys cho các dịch vụ:
  - OpenAI (để tóm tắt và tạo ảnh)
  - Facebook Graph API (đăng lên Facebook)
  - LinkedIn API (đăng lên LinkedIn)
  - Telegram Bot Token (đăng lên Telegram)
  - Discord Webhook URL (đăng lên Discord)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/15381)
2. Click "Copy JSON" để sao chép cấu hình
3. Trong n8n Editor, click "Import from Clipboard" và dán JSON đã sao chép

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **RSS Feed Trigger**:
   - Thay đổi URL trong node "RSS Feed Trigger" thành nguồn tin RSS mong muốn
   - Cấu hình số lượng bài viết cần lấy trong "Options"

2. **OpenAI Nodes**:
   - Tạo credentials cho OpenAI trong n8n
   - Cấu hình model và parameters trong các node:
     - "Converts product descriptions (HTML) into short" (sử dụng model gpt-3.5-turbo)
     - "Generate an image" (sử dụng model dall-e-3)

3. **WordPress Node**:
   - Tạo credentials cho WordPress trong n8n
   - Cấu hình các tham số trong node "Create WordPress Post":
     - Post Title: `{{$node["HTML (Extract title)"].json.title}}`
     - Post Content: `{{$node["LLM Chain (Summarization)"].json.text}}`
     - Post Status: "publish"

4. **Social Media Nodes**:
   - Tạo credentials cho từng mạng xã hội trong n8n
   - Cấu hình các tham số trong các node tương ứng:
     - Facebook: Cấu hình page ID và access token
     - LinkedIn: Cấu hình profile ID và access token
     - Telegram: Cấu hình channel ID và bot token
     - Discord: Cấu hình webhook URL

#### 3. Kích hoạt ⚡️
1. Click "Execute Workflow" để test với dữ liệu mẫu
2. Kiểm tra kết quả trên các kênh đã cấu hình
3. Nếu mọi thứ ổn, click "Activate" để chạy workflow tự động

### ✍️ Mẹo & gợi ý nâng cao
1. **Tùy chỉnh tóm tắt**: Điều chỉnh prompt trong node "LLM Chain (Summarization)" để phù hợp với phong cách nội dung của các sếp
2. **Lọc nội dung**: Thêm node "If" để lọc các bài viết không phù hợp trước khi xử lý
3. **Lịch đăng bài**: Thêm node "Schedule" để đặt lịch đăng bài cho các mạng xã hội
4. **Báo cáo tiến độ**: Thêm node "Email" để nhận báo cáo hàng ngày về các bài viết đã đăng

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quy trình quản lý nội dung từ việc lấy tin tức đến đăng lên nhiều kênh truyền thông. Với việc tích hợp AI, các sếp có thể tạo ra nội dung chuyên nghiệp mà không cần phải viết tay. Hãy thử ngay và tiết kiệm thời gian quý giá của các sếp!