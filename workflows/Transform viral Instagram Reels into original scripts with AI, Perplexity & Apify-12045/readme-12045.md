---
title: "🎥 Tự động hóa chuyển đổi Reels viral thành kịch bản gốc với AI, Perplexity & Apify"
description: "Hướng dẫn chi tiết cách tự động hóa quá trình chuyển đổi nội dung Reels viral thành kịch bản gốc sử dụng công nghệ AI, Perplexity và Apify trong n8n"
slug: "tu-dong-hoa-chuyen-doi-reels-viral-thanh-kich-ban-goc"
tags: [n8n, automation, no-code, content-creation, ai]
keywords: [n8n workflow, tự động hóa nội dung, AI tạo kịch bản, Perplexity, Apify]
---

# 🎥 Tự động hóa chuyển đổi Reels viral thành kịch bản gốc với AI, Perplexity & Apify

[Các sếp nội dung] đang gặp khó khăn khi phải tìm kiếm ý tưởng mới cho video, phân tích nội dung viral và viết kịch bản từ đầu? Workflow này sẽ giúp các sếp tự động hóa toàn bộ quá trình từ việc thu thập nội dung đến tạo ra kịch bản gốc hoàn chỉnh, chỉ trong vài bước đơn giản!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa toàn bộ quá trình từ 3-5 ngày xuống còn vài giờ.
- **Nội dung độc đáo**: Chuyển đổi từ nội dung viral thành kịch bản gốc, tránh vi phạm bản quyền.
- **Dễ dàng mở rộng**: Có thể kết hợp với các công cụ khác như Slack, Telegram để thông báo kết quả.
- **Hoạt động liên tục**: Chạy tự động theo lịch hoặc theo yêu cầu, không cần can thiệp thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản **Apify** để chạy scraper Instagram.
- Bảng tính **Google Sheet** với các cột: URL, Title, Description, Script.
- API key **Perplexity** để thực hiện bước nghiên cứu.
- API key **OpenAI** (hoặc tương tự) để thực hiện các bước xử lý ngôn ngữ tự nhiên.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc](https://n8n.io/workflows/12045)
2. Sao chép nội dung JSON
3. Trong n8n Editor, nhấn **Import from Clipboard** và dán nội dung JSON

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Limit Node**: Giới hạn số lượng Reels xử lý mỗi lần chạy (mặc định là 1 để kiểm tra).
- **Schedule Trigger**: Thiết lập lịch chạy tự động (ví dụ: hàng ngày lúc 9h sáng).
- **Run Apify Scraper**:
  - Cấu hình credentials Apify.
  - Thiết lập các tham số như số lượng Reels cần lấy, từ khóa tìm kiếm.
- **Check Existing Entries**:
  - Cấu hình credentials Google Sheets.
  - Chỉ định ID bảng tính và tên sheet chứa dữ liệu.
- **Download Reel Video**: Đảm bảo có quyền truy cập vào các URL video.
- **Transcribe Reel Audio**:
  - Cấu hình credentials OpenAI.
  - Chọn model phù hợp (ví dụ: whisper-1).
- **Filter + Generate Script Ideas**:
  - Tùy chỉnh prompt để phù hợp với phong cách nội dung của các sếp.
  - Điều chỉnh tham số nhiệt độ (temperature) để cân bằng giữa sáng tạo và nhất quán.
- **Research with Perplexity**:
  - Cấu hình API key Perplexity.
  - Thiết lập các tham số như độ dài nghiên cứu, ngôn ngữ.
- **Generate Final Script**:
  - Tùy chỉnh prompt để tạo ra kịch bản phù hợp với mục tiêu nội dung.
  - Điều chỉnh các tham số như độ dài, phong cách viết.
- **Update Sheet with Script**:
  - Cấu hình credentials Google Sheets.
  - Chỉ định cột để lưu kết quả kịch bản.

#### 3. Kích hoạt ⚡️
1. Nhấn **Execute Node** để kiểm tra từng bước.
2. Sau khi tất cả các node hoạt động đúng, nhấn **Activate Workflow**.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Telegram**: Thêm node gửi thông báo khi workflow hoàn thành.
- **Lưu log**: Thêm node lưu log hoạt động vào Google Sheets hoặc cơ sở dữ liệu.
- **Gửi báo cáo định kỳ**: Tạo báo cáo tổng hợp các kịch bản đã tạo trong tuần.
- **Tối ưu hóa chi phí**: Sử dụng các model OpenAI rẻ hơn cho các bước không quan trọng.

### 📌 Kết luận
Workflow này không chỉ giúp các sếp tiết kiệm thời gian mà còn mang lại nội dung độc đáo, phù hợp với xu hướng hiện tại. Hãy thử ngay và biến những Reels viral thành nguồn cảm hứng sáng tạo cho nội dung của các sếp!