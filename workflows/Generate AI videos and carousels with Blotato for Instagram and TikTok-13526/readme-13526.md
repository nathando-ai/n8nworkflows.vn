---
title: "🚀 Tự động tạo Video AI và Carousel đăng Instagram, TikTok với Blotato và n8n"
description: "Xây dựng hệ thống Social Media Autopilot toàn diện: Biến link bài viết thành video AI, carousel hấp dẫn và tự động xuất bản lên Instagram, TikTok qua Telegram."
slug: "tu-dong-hoa-tao-video-ai-carousel-blotato-instagram-tiktok"
tags: [n8n, automation, blotato, ai-video, instagram, tiktok, telegram]
keywords: [n8n workflow, tự động hóa marketing, tạo video ai, blotato n8n, đăng bài instagram tự động, tiktok autopilot]
---

# 🚀 Tự động tạo Video AI và Carousel đăng Instagram, TikTok với Blotato và n8n

Việc sáng tạo nội dung đa nền tảng (Cross-platform content creation) cho Instagram và TikTok ngốn của các nhà sáng tạo và doanh nghiệp hàng tấn thời gian: từ việc tóm tắt bài viết, viết kịch bản, thiết kế hình ảnh/carousel, dựng video đến việc lên lịch đăng bài thủ công. 

Workflow n8n này (được thiết kế bởi chuyên gia Dr. Firas) giải quyết triệt để nỗi đau đó bằng cách tự động hóa 100% quy trình: Chỉ cần gửi một đường link và yêu cầu qua Telegram, hệ thống AI sẽ tự động xử lý, tạo video/carousel chuyên nghiệp và xuất bản thẳng lên kênh social của các sếp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không còn cảnh tự tay cắt ghép video hay thiết kế từng chiếc tweet-card carousel thủ công.
- **Vận hành qua chat:** Điều khiển mọi thứ trực tiếp từ ứng dụng Telegram quen thuộc ngay trên điện thoại.
- **Đa dạng hóa nội dung:** Tự động tạo carousel chuyên sâu cho Instagram và video AI bắt mắt cho TikTok từ bất kỳ nguồn URL nào.
- **Tự động hóa hoàn toàn (End-to-End):** Từ bước thu thập nguồn, xử lý AI, tạo media, kiểm tra trạng thái hoàn thành cho đến khi đăng tải và gửi thông báo báo cáo.
:::

### 📦 Các thành phần trong Workflow (12 Nodes)
Workflow tích hợp các công cụ mạnh mẽ thuộc hệ sinh thái LangChain và Blotato:
- **Telegram Trigger & Telegram Tool (`telegramTrigger`, `telegramTool`):** Nhận lệnh từ người dùng và gửi thông báo kết quả.
- **Social Media Autopilot Agent (`agent`):** AI Agent trung tâm điều phối quy trình xử lý nội dung.
- **OpenAI ChatGPT (`lmChatOpenAi` - `gpt-4o-mini`):** Phân tích và tạo prompt tối ưu.
- **Simple Memory (`memoryBufferWindow`):** Lưu trữ ngữ cảnh hội thoại ngắn hạn.
- **Blotato Tools (`@blotato/n8n-nodes-blotato.blotatoTool`):** Bộ công cụ xử lý chuyên sâu gồm:
  - `Create source` & `Get source`: Trích xuất nội dung từ URL nguồn.
  - `Create visual - tweet card carousel` & `Create visual - AI image video`: Khởi tạo thiết kế video/carousel.
  - `Get visual`: Kiểm tra tiến độ render media.
  - `Post to Instagram` & `Post to TikTok`: Xuất bản trực tiếp lên mạng xã hội.

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một **n8n instance** đang hoạt động.
- Tài khoản **[Blotato](https://blotato.com/?ref=firas)** có quyền truy cập API.
- Các tài khoản Instagram và/hoặc TikTok đã được kết nối sẵn bên trong **[Blotato](https://blotato.com/?ref=firas)**.
- Một **Telegram Bot** (tạo qua BotFather) để làm cổng giao tiếp nhận lệnh và thông báo.
- Tài khoản **OpenAI API Key** để vận hành AI Agent.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này và import trực tiếp vào giao diện n8n Editor của các sếp, hoặc sử dụng tính năng copy/paste JSON.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Telegram Trigger & Telegram Tool:** Điền thôngดูก Telegram Bot Token hợp lệ để kết nối với con bot của các sếp.
- **OpenAI ChatGPT Node:** Cấu hình OpenAI API credentials và chọn model `gpt-4o-mini` (hoặc model tương đương).
- **Blotato Nodes (`Create visual`, `Post to Instagram`, `Post to TikTok`...):** Thêm Blotato API Credentials. Tại các node đăng bài, tiến hành chọn đúng tài khoản Instagram/TikTok đã liên kết trong hệ thống Blotato của các sếp.

#### 3. Kích hoạt ⚡️
- Thực hiện một lượt chạy thử (Test run) bằng cách nhắn tin qua Telegram Bot với một đường link bài viết kèm yêu cầu cụ thể để kiểm tra luồng dữ liệu.
- Sau khi test thành công, bật công tắc **Active** để đưa workflow vào chế độ tự động hóa 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Thay vì chỉ gửi thông báo về Telegram cá nhân, các sếp có thể tích hợp thêm node Slack hoặc Discord để đội ngũ cùng theo dõi tiến độ sản xuất nội dung.
- **Lưu trữ dữ liệu:** Kết nối thêm một Google Sheets node để lưu lại lịch sử các URL đã tạo video và trạng thái bài đăng nhằm dễ dàng kiểm toán (audit).
- **Lên lịch tự động:** Thay vì kích hoạt thủ công qua Telegram Trigger, các sếp có thể đổi thành Schedule Trigger để hệ thống tự động quét các bài viết mới từ RSS Feed hàng ngày và tự tạo video đăng tải.

### 📌 Kết luận
Với sự kết hợp hoàn hảo giữa n8n, AI Agent và Blotato, việc quản lý nội dung đa nền tảng chưa bao giờ dễ dàng đến thế. Hãy cài đặt ngay workflow này để tối ưu hóa hiệu suất truyền thông xã hội cho doanh nghiệp của các sếp ngay hôm nay!