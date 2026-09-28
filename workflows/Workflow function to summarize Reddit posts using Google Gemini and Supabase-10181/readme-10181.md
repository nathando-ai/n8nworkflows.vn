---
title: "🚀 Tự động tổng hợp bài viết Reddit bằng Google Gemini và Supabase - Workflow n8n"
description: "Hướng dẫn tự động hóa tổng hợp bài viết Reddit bằng AI Gemini và lưu trữ kết quả vào cơ sở dữ liệu Supabase. Tiết kiệm thời gian và nâng cao hiệu quả nghiên cứu thị trường."
slug: "tu-dong-tong-hop-bai-viet-reddit-bang-gemini-supabase"
tags: [n8n, automation, no-code, AI, research]
keywords: [n8n workflow, tự động hóa, tổng hợp bài viết, Reddit, Google Gemini, Supabase]
---

# 🚀 Tự động tổng hợp bài viết Reddit bằng Google Gemini và Supabase

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp có thể đã từng phải mất hàng giờ đồng hồ để đọc và tổng hợp các bài viết trên Reddit về thị trường, sản phẩm hoặc ngành nghề của mình. Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình này chỉ trong vài phút, giúp tiết kiệm thời gian quý giá và tập trung vào những việc quan trọng hơn.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian đọc và tổng hợp thủ công lên đến 90%.
- Tự động lọc và tập trung vào các bài viết từ các subreddit quan trọng.
- Tổng hợp thông tin từ cả bài viết và bình luận bằng công nghệ AI tiên tiến.
- Lưu trữ kết quả vào cơ sở dữ liệu Supabase để phân tích sau này.
- Hoạt động liên tục 24/7 mà không cần can thiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Cloud với API key cho Google Gemini.
- Tài khoản Reddit với quyền truy cập API.
- Cơ sở dữ liệu Supabase đã được thiết lập.
- Tài khoản n8n đã được cài đặt và cấu hình.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể import workflow này bằng cách:
1. Truy cập vào n8n Editor.
2. Nhấn vào nút "Import from URL" và dán link sau: [https://n8n.io/workflows/10181](https://n8n.io/workflows/10181)
3. Hoặc tải file JSON về và import thủ công.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

- **Google Gemini Chat Model**: Cần cấu hình credentials cho Google Palm API.
- **extract relevant attribut from comments**: Node này sẽ trích xuất các thuộc tính quan trọng từ bình luận.
- **aggregate post and comment into a single text**: Node này sẽ tổng hợp nội dung bài viết và bình luận thành một văn bản duy nhất.
- **Structured Output Parser**: Node này sẽ phân tích và cấu trúc đầu ra từ mô hình AI.
- **Wait (rate limiting)**: Node này sẽ tạo độ trễ để tránh bị giới hạn tốc độ từ API.
- **manual trigger when testing**: Node này cho phép kích hoạt thủ công khi kiểm tra.
- **check once a day if new post are available**: Node này sẽ kiểm tra hàng ngày xem có bài viết mới không.
- **Get post data from supabase**: Node này sẽ lấy dữ liệu bài viết từ Supabase.
- **and extract their reddit id**: Node này sẽ trích xuất ID của các bài viết từ Reddit.
- **get saved post from reddit profile**: Node này sẽ lấy các bài viết đã lưu từ hồ sơ Reddit.
- **extract relevant attribut and filter posts based on subreddit**: Node này sẽ trích xuất các thuộc tính quan trọng và lọc các bài viết dựa trên subreddit.
- **further filtering existing posts wrt existing posts in database**: Node này sẽ lọc thêm các bài viết hiện có dựa trên cơ sở dữ liệu.
- **LLM1**: Node này sẽ xử lý các tác vụ liên quan đến mô hình ngôn ngữ lớn (LLM).
- **get all comments for the current post**: Node này sẽ lấy tất cả các bình luận cho bài viết hiện tại.
- **LLM2**: Node này sẽ xử lý các tác vụ liên quan đến mô hình ngôn ngữ lớn (LLM).
- **prepare data to be inserted in supabase**: Node này sẽ chuẩn bị dữ liệu để chèn vào Supabase.
- **insert new reddit post**: Node này sẽ chèn các bài viết Reddit mới vào Supabase.
- **Loop Over Every Posts**: Node này sẽ lặp qua từng bài viết.
- **If the condition is satisfied**: Node này sẽ kiểm tra xem điều kiện có được thỏa mãn không.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Các sếp có thể tùy chỉnh danh sách các subreddit để theo dõi.
- Có thể thay đổi tần suất kiểm tra (hàng ngày, hàng tuần, hàng tháng).
- Có thể mở rộng để gửi báo cáo tự động qua email hoặc Slack.
- Có thể tích hợp với các công cụ phân tích dữ liệu khác để tạo báo cáo chi tiết hơn.

### 📌 Kết luận
Workflow này là giải pháp hoàn hảo cho các sếp muốn tự động hóa quá trình tổng hợp và phân tích thông tin từ Reddit. Với công nghệ AI tiên tiến và cơ sở dữ liệu mạnh mẽ, các sếp có thể tiết kiệm thời gian và tập trung vào những việc quan trọng hơn. Hãy áp dụng ngay để nâng cao hiệu quả nghiên cứu thị trường của mình!