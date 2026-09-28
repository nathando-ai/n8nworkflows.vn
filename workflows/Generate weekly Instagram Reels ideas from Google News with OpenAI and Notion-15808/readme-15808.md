---
title: "🚀 Tự động tạo 7 ý tưởng Instagram Reels hàng tuần từ Google News với OpenAI và Notion"
description: "Hướng dẫn xây dựng workflow n8n tự động cập nhật xu hướng từ Google News, dùng OpenAI tạo kịch bản Reels chi tiết và lưu trực tiếp vào Notion."
slug: "tu-dong-tao-y-tuong-instagram-reels-google-news-openai-notion"
tags: [n8n, automation, no-code, openai, notion, content-creation, ai]
keywords: [n8n workflow, tạo ý tưởng reels tự động, google news rss, openai gpt-4o-mini, notion content calendar]
---

# 🚀 Tự động tạo 7 ý tưởng Instagram Reels hàng tuần từ Google News với OpenAI và Notion

Các sếp làm sáng tạo nội dung, đặc biệt là trong các ngách như D2C skincare, mỹ phẩm hay lifestyle chắc chắn luôn đau đầu mỗi tuần khi phải nghĩ xem tuần này sẽ quay video gì, bắt trend gì trên Instagram Reels. Việc ngồi đọc tin tức, lọc xu hướng rồi nghĩ hook, viết caption thủ công vừa tốn thời gian lại dễ cạn kiệt ý tưởng.

Giải pháp đây rồi! Workflow n8n này sẽ tự động hóa 100% quy trình từ việc "đánh hơi" xu hướng mới nhất trên Google News, đưa vào AI phân tích để đóng gói thành 7 ý tưởng Reels cực xịn, kèm theo hook, caption, hashtag, format quay và tự động đẩy toàn bộ lịch nội dung vào Notion của các sếp. Không cần code, chỉ cần setup một lần là chạy mãi mãi!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian lên kế hoạch**: Không còn cảnh vắt óc nghĩ chủ đề mỗi thứ Hai đầu tuần.
- **Bắt trend thần tốc**: Tận dụng nguồn dữ liệu cực kỳ tươi mới từ Google News RSS trong 7 ngày gần nhất.
- **Nội dung chuyên sâu & chuyên nghiệp**: AI đóng vai trò chiến lược gia nội dung (Content Strategist) với cấu trúc kịch bản hoàn chỉnh (Ngày đăng, Chủ đề, Hook, Caption, Hashtag, Định dạng, Lý do hiệu quả).
- **Đồng bộ mượt mà**: Toàn bộ lịch content tự động được lưu trữ gọn gàng trong Notion Content Calendar.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance**: Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **OpenAI API Key**: Để kết nối với mô hình GPT-4o-mini.
- **Notion Integration & Database**: Tài khoản Notion và một trang Database được thiết lập sẵn để lưu lịch content.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này và paste trực tiếp vào giao diện n8n Editor, hoặc import file JSON tải về từ nguồn gốc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động trơn tru theo ý muốn, các sếp cần cấu hình chính xác các node sau:

- **Weekly Content Schedule**: Mặc định node này được cài đặt chạy vào **Thứ Hai hàng tuần lúc 8:00 sáng**. Các sếp có thể đổi lại khung giờ yêu thích nếu muốn.
- **Get Trends (RSS Feed Read)**: Node này đọc nguồn RSS của Google News dựa trên từ khóa tìm kiếm (ví dụ: *skincare trends*, *skincare routine*). Các sếp có thể thay đổi URL RSS thành bất kỳ ngách nào mà thương hiệu của mình đang theo đuổi (F&B, Tech, Finance...).
- **Top 7 Trends (Limit)**: Giữ nguyên giới hạn lấy 7 bài viết nổi bật nhất để tránh làm quá tải token của AI.
- **OpenAI Chat Model & Generate 7 Instagram Reel Ideas**: 
  - Chọn Credentials là `OpenAI API`.
  - Chọn model `gpt-4o-mini` (hoặc các model mạnh hơn tùy nhu cầu).
  - Kiểm tra lại system prompt trong Chain LLM để AI đóng vai đúng chân dung thương hiệu (D2C skincare brand - GlowCare) và trả về cấu trúc dữ liệu mong muốn.
- **Save ideas to Content Calendar (Notion)**:
  - Chọn Credentials là `Notion API`.
  - Liên kết với Database Notion của các sếp tại thông số `resource` (Database Page). Đảm bảo các trường thuộc tính (properties) trong Notion khớp với dữ liệu mà AI trả về.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Test workflow** để chạy thử nghiệm xem dữ liệu có chảy từ Google News qua OpenAI và đổ vào Notion thành công hay không.
- Nếu mọi thứ xanh mướt, hãy gạt công tắc **Active** ở góc trên cùng bên phải để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo**: Thêm node Telegram hoặc Slack ở bước cuối cùng để bắn một tin nhắn thông báo: *"Ê sếp ơi, lịch Reels tuần này đã sẵn sàng trong Notion rồi nè!"*.
- **Mở rộng nguồn dữ liệu**: Ngoài Google News RSS, các sếp có thể kết hợp thêm xu hướng từ Reddit, Twitter/X hoặc YouTube RSS để AI có góc nhìn đa chiều hơn.
- **Tự động tạo ảnh minh họa**: Kết hợp thêm node DALL-E hoặc Midjourney API để tạo luôn hình ảnh/moodboard cho từng ý tưởng Reels.

### 📌 Kết luận
Tự động hóa không chỉ giúp tiết kiệm thời gian mà còn nâng tầm chất lượng vận hành marketing cho doanh nghiệp. Hãy áp dụng ngay workflow này để tối ưu hóa quy trình sáng tạo nội dung của các sếp ngay hôm nay!