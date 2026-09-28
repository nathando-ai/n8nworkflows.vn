---
title: "🚀 Tự động theo dõi xu hướng đối thủ Instagram với Claude 3.5 & Cảnh báo đa kênh"
description: "Hướng dẫn xây dựng workflow n8n tự động quét bài viết đối thủ trên Instagram, dùng Claude AI phân tích xu hướng và gửi cảnh báo qua Email, WhatsApp."
slug: "tu-dong-theo-doi-xu-huong-doi-thu-instagram-claude-ai"
tags: [n8n, automation, no-code, instagram, claude-ai, market-research]
keywords: [n8n workflow, theo dõi đối thủ instagram, claude ai, automation marketing, phân tích xu hướng]
---

# 🚀 Tự động theo dõi xu hướng đối thủ Instagram với Claude 3.5 & Cảnh báo đa kênh

Các sếp có đang tốn hàng giờ mỗi tuần để mò mẫm vào trang cá nhân của đối thủ, đếm lượt like, đọc comment để xem họ đang làm nội dung gì hot? Việc làm thủ công này không chỉ mất thời gian mà còn dễ bỏ sót các xu hướng thị trường quan trọng.

Đừng lo, bài viết này sẽ hướng dẫn các sếp thiết lập một siêu phẩm workflow n8n mang tên **"Monitor Instagram Competitor Trends with Claude 3.5 & Multi-Channel Alerts"** (được phát triển bởi *Oneclick AI Squad*). Workflow này sẽ tự động hóa 100% quy trình thu thập dữ liệu, nhờ AI phân tích chiến lược và gửi báo cáo thẳng đến điện thoại hoặc email của các sếp mỗi ngày!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không cần thủ công vào check từng đối thủ nữa, mọi thứ diễn ra tự động.
- **Phân tích thông minh bằng AI:** Claude 3.5 sẽ lọc ra các điểm nhấn chiến lược (strategic insights) cực kỳ sắc bén từ dữ liệu bài viết.
- **Cảnh báo đa kênh tức thì:** Nhận báo cáo chi tiết qua Email và tin nhắn ngắn gọn qua WhatsApp (Twilio).
- **Lưu trữ dữ liệu tự động:** Mọi số liệu và insight đều được ghi chép lại cẩn thận vào Google Sheets để tiện xem lại lịch sử.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động mượt mà, các sếp cần chuẩn bị sẵn các tài nguyên sau:
1. **n8n Instance** (Self-hosted hoặc Cloud).
2. **Google Sheets**: 1 file chứa danh sách tài khoản đối thủ và 1 sheet để lưu log cảnh báo.
3. **Instagram Graph API / HTTP Request**: Token để lấy bài viết gần nhất của đối thủ.
4. **Claude AI API Key (Anthropic)**: Để AI phân tích số liệu và viết báo cáo.
5. **SMTP Credentials**: Để gửi email báo cáo chi tiết.
6. **Twilio Account**: Để bắn tin nhắn WhatsApp cảnh báo nhanh.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể copy mã JSON của workflow này và dán trực tiếp vào n8n Editor của mình, hoặc import file JSON tải từ trang chủ n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình chính xác các node trọng điểm sau:

- **Schedule Trigger**: Mặc định lịch chạy là 10 giờ sáng mỗi ngày (hoặc kích hoạt qua webhook `/competitor-alert`). Các sếp có thể đổi giờ tùy ý.
- **Get Competitor List (Google Sheets)**: Kết nối tài khoản Google API, trỏ tới file Google Sheets chứa danh sách các tài khoản Instagram đối thủ cần theo dõi.
- **Loop Over Competitors (Split In Batches)**: Node này giúp xử lý từng đối thủ một để tránh vượt quá giới hạn API (rate limits).
- **Get Competitor Posts (HTTP Request)**: Cấu hình gọi Instagram Graph API để lấy 10 bài viết gần nhất của từng đối thủ.
- **Calculate Performance Metrics (Code)**: Node JavaScript có sẵn nhiệm vụ tính toán độ tương tác trung bình (avg engagement) và xu hướng từ dữ liệu bài viết.
- **Generate AI Insights (Claude AI) (HTTP Request)**: Nhập API Key của Anthropic, tùy chỉnh prompt để Claude phân tích dữ liệu và trả về 3 gạch đầu dòng insight chiến lược quan trọng nhất.
- **Send Email Alert & Send WhatsApp Alert**: Điền thông tin cấu hình SMTP của email và tài khoản Twilio WhatsApp để hệ thống gửi thông báo.
- **Log Alert (Google Sheets)**: Trỏ tới sheet lưu log để ghi nhận lại toàn bộ số liệu và insight sau mỗi lần chạy.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** để chạy thử với dữ liệu mẫu xem hệ thống có báo lỗi ở đâu không.
- Nếu mọi thứ xanh mướt (success), hãy gạt công tắc sang **Active** để workflow tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa hơn nữa hệ thống này, các sếp có thể tham khảo các ý tưởng mở rộng:
- **Tích hợp Telegram / Slack**: Thay vì chỉ dùng WhatsApp hay Email, hãy bắn thông báo trực tiếp vào group chat công ty để team content cùng nắm bắt.
- **Cảnh báo ngưỡng đột phá**: Thêm điều kiện (If node) – nếu bài viết của đối thủ có lượng tương tác vượt gấp 3 lần bình thường, lập tức bắn tin nhắn khẩn cấp.
- **Mở rộng nguồn dữ liệu**: Kết hợp thêm TikTok hoặc Facebook Page để có cái nhìn toàn diện về bức tranh Social Media của ngành hàng.

### 📌 Kết luận
Workflow **Monitor Instagram Competitor Trends with Claude 3.5 & Multi-Channel Alerts** là trợ thủ đắc lực giúp các marketer và chủ doanh nghiệp luôn đi trước một bước so với đối thủ. Hãy thiết lập ngay hôm nay để tối ưu hóa năng suất và làm chủ cuộc chơi truyền thông xã hội nhé các sếp!