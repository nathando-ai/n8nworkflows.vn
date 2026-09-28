---
title: "🚀 Hệ thống cảnh báo tin tức thông minh với DeepSeek AI và Slack"
description: "Tự động hóa thu thập tin tức từ RSS, phân tích nội dung bằng AI và gửi cảnh báo Slack - giải pháp tiết kiệm thời gian cho các sếp quản lý thông tin"
slug: "he-thong-canh-bao-tin-tuc-thong-minh-voi-deepseek-ai-va-slack"
tags: [n8n, automation, no-code, AI, Slack]
keywords: [n8n workflow, tự động hóa, AI phân tích tin tức, Slack notifications, DeepSeek AI]
---

# 🚀 Hệ thống cảnh báo tin tức thông minh với DeepSeek AI và Slack

[Các sếp đang mệt mỏi với việc phải theo dõi hàng chục nguồn tin tức hàng ngày? Bạn có muốn nhận được những tin tức quan trọng nhất được lọc và tóm tắt một cách tự động? Hãy thử workflow này để tiết kiệm thời gian và tập trung vào những thông tin thực sự quan trọng!]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần phải đọc hàng chục bài báo mỗi ngày
- **Chính xác cao**: AI DeepSeek phân tích và lọc những tin tức quan trọng nhất
- **Cá nhân hóa**: Nhận thông báo chỉ khi có tin tức liên quan đến lĩnh vực của bạn
- **Hoạt động liên tục**: Hệ thống chạy tự động 24/7 mà không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Slack với quyền tạo bot và gửi tin nhắn
- API key của DeepSeek AI (hoặc OpenAI nếu sử dụng mô hình khác)
- Danh sách URL nguồn tin tức RSS (ví dụ: các trang báo chính thống, blog ngành nghề)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/8131](https://n8n.io/workflows/8131)
2. Click vào nút "Import" ở góc trên bên phải
3. Trong n8n Editor, chọn "Import from URL" và dán link trên
4. Hoặc copy toàn bộ JSON workflow và chọn "Import from JSON"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **RSS Feed** node:
   - Thay đổi URL nguồn tin tức trong trường "Feed URL"
   - Có thể thêm nhiều node RSS Feed nếu cần theo dõi nhiều nguồn

2. **DeepSeek Chat Model** node:
   - Thêm credentials "deepSeekApi" với API key của bạn
   - Có thể thay thế bằng mô hình OpenAI nếu cần

3. **send to Slack** node:
   - Thêm credentials "slackApi" với Bot Token của bạn
   - Chỉnh sửa "Channel" để chọn kênh Slack nhận thông báo
   - Tùy chỉnh template tin nhắn trong trường "Message"

4. **analyze with LLM** node:
   - Điều chỉnh prompt trong trường "Prompt" nếu muốn thay đổi cách AI phân tích tin tức
   - Có thể thêm các từ khóa quan trọng trong lĩnh vực của bạn để AI lọc chính xác hơn

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong, click vào nút "Activate" ở góc trên bên phải
2. Để test workflow, bạn có thể kích hoạt thủ công bằng cách click vào nút "Execute Workflow"
3. Kiểm tra kênh Slack để xác nhận hệ thống hoạt động bình thường

### ✍️ Mẹo & gợi ý nâng cao
- **Tùy chỉnh độ quan trọng**: Thêm node "if" sau "analyze with LLM" để lọc những tin tức có độ quan trọng cao hơn
- **Lưu trữ tin tức**: Kết nối với Google Sheets hoặc Notion để lưu trữ lịch sử tin tức đã xử lý
- **Thông báo định kỳ**: Thêm node "Schedule Trigger" để gửi báo cáo tổng hợp hàng ngày
- **Kết hợp với các công cụ khác**: Có thể kết nối với Google Calendar để tạo sự kiện từ những tin tức quan trọng

### 📌 Kết luận
Hệ thống cảnh báo tin tức thông minh này giúp các sếp tiết kiệm thời gian quý giá, tập trung vào những thông tin thực sự quan trọng và nhận được thông báo chỉ khi có tin tức liên quan đến lĩnh vực của mình. Hãy thử ngay và trải nghiệm cách làm việc thông minh hơn với n8n!