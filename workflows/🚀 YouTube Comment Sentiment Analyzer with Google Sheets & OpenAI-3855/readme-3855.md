---
title: "🚀 Phân tích cảm xúc bình luận YouTube với Google Sheets & OpenAI - Tự động hóa 100% không cần code"
description: "Hướng dẫn tự động hóa phân tích cảm xúc bình luận YouTube bằng n8n, Google Sheets và OpenAI. Tiết kiệm thời gian, tối ưu hóa nội dung và quản lý dữ liệu hiệu quả."
slug: "phan-tich-cam-xuc-binh-luan-youtube-voi-google-sheets-openai"
tags: [n8n, automation, no-code, youtube, google-sheets, openai, sentiment-analysis]
keywords: [n8n workflow, tự động hóa, phân tích cảm xúc, youtube, google sheets, openai]
---

# 🚀 Phân tích cảm xúc bình luận YouTube với Google Sheets & OpenAI - Tự động hóa 100% không cần code

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp có biết không? Với lượng bình luận khổng lồ trên YouTube mỗi ngày, việc phân tích cảm xúc thủ công là một công việc cực kỳ tốn thời gian và dễ mắc sai sót. Bạn phải đọc từng bình luận, đánh giá cảm xúc và ghi lại kết quả - một quá trình chậm chạp và dễ gây lỗi.

Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình này trong vài phút, tiết kiệm hàng giờ mỗi ngày cho công việc quan trọng hơn.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động phân tích hàng nghìn bình luận trong vài phút.
- **Dữ liệu chính xác**: Sử dụng mô hình AI tiên tiến của OpenAI để phân tích cảm xúc.
- **Quản lý hiệu quả**: Lưu trữ và quản lý dữ liệu bình luận trong Google Sheets.
- **Tối ưu hóa nội dung**: Nhận thông tin chi tiết về cảm xúc của khán giả để cải thiện nội dung.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với quyền truy cập vào Google Sheets.
- API Key từ OpenAI (để phân tích cảm xúc).
- API Key từ YouTube Data API v3 (để lấy bình luận).
- Bảng Google Sheets đã được cấu hình theo hướng dẫn bên dưới.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/3855](https://n8n.io/workflows/3855)
2. Click vào nút "Import" để tải workflow về máy.
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON đã tải về.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Cấu hình Google Sheets**:
   - Tạo một bảng Google Sheets mới với 2 sheet:
     - **Sheet1 (Results with Sentiment)**:
       - Cột A: `commentId` (ID bình luận YouTube)
       - Cột B: `video_url` (URL video)
       - Cột C: `comment` (Nội dung bình luận)
       - Cột D: `authorName` (Tên tác giả)
       - Cột E: `likes` (Số lượt thích)
       - Cột F: `reply` (Số lượt trả lời)
       - Cột G: `sentiment` (Cảm xúc phân tích)
       - Cột H: `published_at` (Thời gian đăng)
     - **Sheet2 (Video URLs)**:
       - Cột A: `video_urls` (Danh sách URL video)
       - Cột B: `last_fetched_time` (Thời gian lấy cuối cùng)
       - Cột C: `next_fetch_time` (Thời gian lấy tiếp theo)

2. **Cấu hình Credentials**:
   - **Google Sheets**:
     - Tạo một Service Account trong Google Cloud Console.
     - Cấp quyền truy cập vào bảng Google Sheets của bạn.
     - Thêm Service Account vào n8n Credentials.
   - **YouTube Data API v3**:
     - Tạo một API Key trong Google Cloud Console.
     - Thêm API Key vào n8n Credentials.
   - **OpenAI API Key**:
     - Tạo một API Key trong tài khoản OpenAI.
     - Thêm API Key vào n8n Credentials.

3. **Cấu hình các node quan trọng**:
   - **Get Video Urls from Google Sheet**:
     - Chọn credentials Google Sheets đã cấu hình.
     - Điền tham số:
       - Sheet Name: `Sheet2`
       - Range: `A2:A` (hoặc phạm vi chứa danh sách URL video của bạn)
   - **Get Comments for video urls**:
     - Chọn credentials YouTube Data API đã cấu hình.
     - Điền tham số:
       - URL: `https://www.googleapis.com/youtube/v3/commentThreads`
       - Query Parameters:
         - `part`: `snippet`
         - `videoId`: `{{$node["Get Video Urls from Google Sheet"].json[0].video_urls}}`
         - `maxResults`: `100`
   - **OpenAI Chat Model**:
     - Chọn credentials OpenAI đã cấu hình.
     - Điền tham số:
       - Model: `gpt-4o-mini` (hoặc mô hình khác phù hợp)
   - **Insert and update comment in google sheet**:
     - Chọn credentials Google Sheets đã cấu hình.
     - Điền tham số:
       - Sheet Name: `Sheet1`
       - Range: `A2:H` (hoặc phạm vi chứa dữ liệu bình luận của bạn)
       - Operation: `appendOrUpdate`
   - **Update last fetched time and next_fetch_time**:
     - Chọn credentials Google Sheets đã cấu hình.
     - Điền tham số:
       - Sheet Name: `Sheet2`
       - Range: `B2:C` (hoặc phạm vi chứa thời gian lấy của bạn)
       - Operation: `appendOrUpdate`

#### 3. Kích hoạt ⚡️
1. Click vào nút "Execute Workflow" để chạy workflow lần đầu tiên.
2. Kiểm tra kết quả trong Google Sheets để đảm bảo dữ liệu được cập nhật đúng cách.
3. Bật Active workflow để chạy tự động theo lịch trình.

### ✍️ Mẹo & gợi ý nâng cao
- **Tự động hóa hoàn toàn**: Thay thế node "Manual Trigger" bằng node "Cron" để chạy workflow tự động theo lịch trình.
- **Gửi báo cáo**: Thêm node "Email" hoặc "Slack" để gửi báo cáo cảm xúc hàng ngày.
- **Phân tích nâng cao**: Sử dụng các node khác của LangChain để phân tích cảm xúc theo nhiều chiều khác nhau.
- **Lưu log**: Thêm node "No Operation" để lưu log hoạt động của workflow.

### 📌 Kết luận
Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình phân tích cảm xúc bình luận YouTube trong vài phút. Tiết kiệm thời gian, đảm bảo dữ liệu chính xác và tối ưu hóa nội dung hiệu quả. Hãy áp dụng ngay để nâng cao trải nghiệm của khán giả và cải thiện nội dung của bạn!