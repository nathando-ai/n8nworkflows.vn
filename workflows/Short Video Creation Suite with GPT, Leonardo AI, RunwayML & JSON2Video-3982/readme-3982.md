---
title: "🎥 Tự động tạo video ngắn với AI: GPT + Leonardo AI + RunwayML + JSON2Video"
description: "Hướng dẫn tự động hóa quy trình tạo video ngắn hoàn chỉnh từ văn bản bằng n8n, kết hợp GPT, Leonardo AI, RunwayML và JSON2Video. Tiết kiệm 90% thời gian sản xuất nội dung."
slug: "tu-dong-tao-video-ngan-voi-ai-gpt-leonardo-runway-json2video"
tags: [n8n, automation, no-code, ai, video-marketing]
keywords: [n8n workflow, tự động hóa video, ai tạo video, json2video, leonardo ai]
---

# 🎥 Tự động tạo video ngắn với AI: GPT + Leonardo AI + RunwayML + JSON2Video

[Các sếp] có bao giờ cảm thấy mệt mỏi khi phải tạo video ngắn cho marketing? Từ viết kịch bản, thiết kế hình ảnh, tạo video, thêm phụ đề cho đến xuất bản - quá nhiều công đoạn thủ công và thời gian. Workflow này sẽ giúp các sếp tự động hóa hoàn toàn quy trình này chỉ với một dòng văn bản đầu vào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian**: Từ 1-2 ngày tạo video thủ công xuống còn vài phút.
- **Nội dung chuyên nghiệp**: Kết hợp AI tạo hình ảnh, video và phụ đề chất lượng cao.
- **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công sau khi cấu hình.
- **Tùy chỉnh linh hoạt**: Có thể thay đổi kịch bản, hình ảnh và giọng nói theo nhu cầu.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản OpenAI API (cho GPT)
- Tài khoản Leonardo AI (tạo hình ảnh)
- Tài khoản RunwayML (tạo video từ hình ảnh)
- Tài khoản JSON2Video (render video cuối cùng)
- Tài khoản Baserow (lưu trữ dữ liệu trung gian)
- (Tùy chọn) Tài khoản HeyGen (tạo video với nhân vật ảo)
- (Tùy chọn) Tài khoản CaptionsAI (tạo phụ đề)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/3982](https://n8n.io/workflows/3982)
2. Chọn "Import" và sao chép JSON vào n8n Editor
3. Hoặc tải file JSON về và import từ menu "Workflows"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Webhook Node**:
   - Cấu hình webhook để nhận dữ liệu đầu vào (ví dụ: từ một form hoặc API khác)
   - Thiết lập các trường dữ liệu cần thiết: `script`, `scriptType`, `backgroundType`, `voiceType`

2. **OpenAI API Credentials**:
   - Tạo credential mới cho OpenAI trong n8n
   - Điền API Key từ tài khoản OpenAI của bạn

3. **Leonardo AI API**:
   - Tạo credential mới cho Leonardo AI
   - Điền API Key từ tài khoản Leonardo AI

4. **RunwayML API**:
   - Tạo credential mới cho RunwayML
   - Điền API Key từ tài khoản RunwayML

5. **JSON2Video API**:
   - Tạo credential mới cho JSON2Video
   - Điền API Key từ tài khoản JSON2Video

6. **Baserow Configuration**:
   - Tạo một bảng mới trong Baserow với các trường sau:
     - `script` (text)
     - `scriptType` (text)
     - `backgroundType` (text)
     - `voiceType` (text)
     - `status` (text)
     - `videoUrl` (text)
   - Cấu hình các node Baserow trong workflow với thông tin kết nối này

7. **Wait Nodes**:
   - Điều chỉnh thời gian chờ (thường là 5-10 giây) giữa các bước để đảm bảo các dịch vụ AI hoàn thành xử lý

#### 3. Kích hoạt ⚡️
1. Test run workflow với dữ liệu mẫu
2. Kiểm tra từng bước để đảm bảo:
   - GPT tạo kịch bản thành công
   - Leonardo AI tạo hình ảnh
   - RunwayML tạo video từ hình ảnh
   - JSON2Video render video cuối cùng
3. Bật Active workflow sau khi kiểm tra thành công

### ✍️ Mẹo & gợi ý nâng cao
1. **Tích hợp Slack/Telegram**: Thêm node gửi thông báo khi video hoàn thành
2. **Lưu log hoạt động**: Thêm node ghi log vào Google Sheets hoặc Notion
3. **Tạo báo cáo định kỳ**: Thêm node tổng hợp số lượng video tạo được trong ngày
4. **Tự động xuất bản**: Kết nối với các dịch vụ xuất bản video như YouTube, TikTok hoặc Facebook

### 📌 Kết luận
Workflow này đã biến quy trình tạo video ngắn từ một công việc mất thời gian thành một quy trình tự động hoàn toàn. Các sếp chỉ cần cung cấp văn bản đầu vào và workflow sẽ tự động tạo ra video hoàn chỉnh với hình ảnh, âm thanh và phụ đề chất lượng cao. Hãy thử ngay và tiết kiệm thời gian quý giá của các sếp!