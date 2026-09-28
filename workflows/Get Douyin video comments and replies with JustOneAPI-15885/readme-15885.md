---
title: "🚀 Tự động lấy bình luận và phản hồi video Douyin bằng JustOneAPI với n8n"
description: "Hướng dẫn chi tiết cách tự động thu thập bình luận và các phản hồi (replies) từ video Douyin sử dụng JustOneAPI và n8n workflow."
slug: "tu-dong-lay-binh-luan-video-douyin-justoneapi-n8n"
tags: [n8n, automation, no-code, douyin, justoneapi, market-research]
keywords: [n8n workflow, douyin comments, justoneapi, tự động hóa, cào bình luận douyin, nghiên cứu thị trường]
---

# 🚀 Tự động lấy bình luận và phản hồi video Douyin bằng JustOneAPI

Các nhà sáng tạo nội dung, marketer và nhà nghiên cứu thị trường thường gặp rất nhiều khó khăn khi muốn phân tích phản hồi của khán giả trên Douyin (TikTok Trung Quốc). Việc copy thủ công từng bình luận hay các chuỗi hội thoại trả lời (replies) cực kỳ tốn thời gian, dễ bỏ sót thông tin quan trọng.

Giải pháp ở đây là gì? Workflow n8n này sẽ tự động hóa toàn bộ quy trình: gọi API qua **JustOneAPI**, lọc các bình luận có chứa phản hồi, bóc tách dữ liệu sạch sẽ và xuất ra kết quả chỉ trong vài giây mà không cần viết code phức tạp.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Bỏ qua thao tác thủ công, nhanh chóng trích xuất toàn bộ bình luận và phản hồi từ một video Douyin bất kỳ.
- **Xử lý thông minh:** Tự động kiểm tra xem bình luận có phản hồi hay không để điều hướng luồng dữ liệu (có hoặc không có reply) một cách mượt mà.
- **Dữ liệu cấu trúc sẵn:** Chuyển đổi dữ liệu thô từ API thành các tập dữ liệu gọn gàng, sẵn sàng để đưa vào Google Sheets, Database hoặc các công cụ phân tích AI.
- **Phục vụ nghiên cứu thị trường:** Dễ dàng thấu hiểuInsight khách hàng, nắm bắt xu hướng phản hồi trên Douyin để tối ưu chiến lược nội dung.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một hệ thống **n8n** đang hoạt động (Cloud hoặc Self-hosted).
- Tài khoản và API Key từ **JustOneAPI** (dùng để gọi dữ liệu Douyin).
- ID của video Douyin cần phân tích bình luận.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy toàn bộ mã nguồn JSON của workflow.
- Mở giao diện n8n của các sếp, chọn **Workflows** -> **Import from File / Clipboard** và dán đoạn JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import thành công, các sếp cần chú ý cấu hình chính xác các node sau:

- **Node `Prepare API and Comment Data` (`set`):** 
  - Điền ID video Douyin (`video_id`) cần lấy bình luận vào phần tham số đầu vào.
  - Cấu hình các tham số gọi API theo tài liệu của JustOneAPI.
- **Các Node `Fetch Video Comments via API` & `Fetch Comment Replies via API` (`httpRequest`):**
  - Thiết lập phương thức kết nối (GET/POST) và endpoint URL của JustOneAPI.
  - Thêm API Key của các sếp vào phần Header xác thực (Authentication/Headers) của HTTP Request.
- **Node `Select Comment with Replies` (`code`):**
  - Node này sử dụng đoạn mã JavaScript để tìm ra bình luận đầu tiên có chứa phản hồi. Các sếp có thể tùy chỉnh logic đoạn code này nếu muốn lọc theo các tiêu chí khác (ví dụ: bình luận có nhiều lượt thích nhất, hoặc lọc theo từ khóa).

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** để chạy thử nghiệm thủ công và kiểm tra dữ liệu trả về ở các node `Output Raw Comments Data` hoặc `Output Final Reply Data`.
- Khi đã chắc chắn mọi thứ hoạt động trơn tru, hãy gạt công tắc sang **Active** để sẵn sàng sử dụng bất cứ lúc nào.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối Google Sheets / Airtable:** Thêm một node Google Sheets vào cuối luồng để tự động lưu trữ toàn bộ bình luận và phản hồi vào bảng tính phục vụ việc báo cáo.
- **Tích hợp AI phân tích cảm xúc (Sentiment Analysis):** Đưa dữ liệu bình luận thu được vào OpenAI/Claude node để tự động phân tích xem khán giả đang khen hay chê, từ đó đưa ra đánh giá thị trường tự động.
- **Nhận thông báo qua Telegram/Slack:** Cấu hình để gửi các chuỗi hội thoại thú vị hoặc cảnh báo bình luận tiêu cực trực tiếp về nhóm chat làm việc ngay khi quét xong.

### 📌 Kết luận
Workflow "Get Douyin video comments and replies with JustOneAPI" là một công cụ cực kỳ mạnh mẽ giúp các marketer và nhà sáng tạo tiết kiệm hàng giờ đồng hồ nghiên cứu thủ công. Hãy import ngay vào n8n của các sếp và bắt đầu khai thác mỏ vàng dữ liệu từ Douyin nhé!