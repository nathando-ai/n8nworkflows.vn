---
title: "🚀 Tự động hóa sản xuất video AI từ tin tức và đăng lên Instagram, TikTok với HeyGen và n8n"
description: "Xây dựng hệ thống sản xuất video AI hoàn toàn tự động từ việc quét tin tức, viết kịch bản AI, tạo video người ảo HeyGen cho đến đăng tải lên Instagram và TikTok."
slug: "tu-dong-hoa-tao-video-ai-tu-tin-tuc-heygen-tiktok-instagram"
tags: [n8n, automation, heygen, ai-video, tiktok, instagram, content-creation]
keywords: [n8n workflow, tạo video AI tự động, HeyGen automation, đăng video TikTok tự động, Perplexity AI n8n, OpenAI kịch bản video]
---

# 🚀 Tự động hóa sản xuất video AI từ tin tức và đăng lên Instagram, TikTok với HeyGen và n8n

Việc sản xuất nội dung video ngắn (Shorts, Reels, TikTok) hàng ngày ngốn của các nhà sáng tạo nội dung và doanh nghiệp vô số thời gian: từ khâu nghiên cứu tin tức nóng, viết kịch bản, dựng hình người ảo (AI Avatar) cho đến thao tác đăng tải thủ công lên hàng loạt nền tảng mạng xã hội. Nếu thuê nhân sự, chi phí vận hành không hề nhỏ mà tiến độ lại dễ bị gián đoạn.

Workflow n8n này chính là giải pháp "All-in-one" giúp các sếp tự động hóa 100% quy trình trên. Hệ thống sẽ tự động quét tin tức mới nhất, nhờ AI viết kịch bản, tạo video người ảo chuyên nghiệp qua HeyGen, lưu trữ dữ liệu vào Google Sheets và cuối cùng tự động xuất bản lên cả Instagram lẫn TikTok mà không cần chạm tay vào bất kỳ công đoạn thủ công nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Từ khâu tìm kiếm thông tin, tạo video AI đến phân phối nội dung lên mạng xã hội không cần con người can thiệp.
- **Cá nhân hóa & Chuyên nghiệp:** Sử dụng công nghệ AI Avatar của HeyGen kết hợp giọng đọc tự nhiên giúp video thu hút lượng tương tác cực cao.
- **Tiết kiệm chi phí nhân sự:** Thay thế cả một đội ngũ nghiên cứu nội dung, dựng phim và quản trị mạng xã hội chỉ với một workflow n8n.
- **Hoạt động 24/7 không nghỉ:** Lên lịch chạy tự động hàng ngày để kênh của các sếp luôn tràn ngập nội dung mới bắt kịp xu hướng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động trơn tru, các sếp cần chuẩn bị sẵn các tài khoản và API Keys sau:
- **n8n Instance** (Self-hosted hoặc Cloud).
- **Perplexity AI API Key** (Dùng cho node Perplexity Search để quét tin tức).
- **OpenAI API Key** (Dùng cho các node Write Video Script và Write Video Caption).
- **HeyGen API Key & Account** (Để tạo video người ảo Avatar).
- **Google Sheets** (Để lưu trữ log, kịch bản và đường dẫn video).
- **Tài khoản mạng xã hội / Công cụ trung gian** (Instagram Graph API, TikTok API hoặc nền tảng hỗ trợ đăng bài như Blotato).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow từ nguồn cung cấp.
- Trong giao diện n8n, chọn **Add workflow** -> Nhấn vào dấu `...` ở góc trên bên phải -> Chọn **Import from File** và tải file JSON lên, hoặc copy/paste trực tiếp mã nguồn.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các thông số quan trọng sau trong các node:
- **Schedule Trigger:** Cài đặt khung giờ chạy workflow hàng ngày hoặc theo tuần tùy thuộc vào chiến lược nội dung của kênh.
- **Perplexity Search & Write Video Script / Write Video Caption:** Điền OpenAI Credentials và Perplexity Credentials. Tinh chỉnh lại câu lệnh `prompt` trong các node OpenAI để kịch bản phù hợp với phong cách thương hiệu của doanh nghiệp.
- **Create Avatar Video (Optimized) & HeyGen Webhook:** Kết nối tài khoản HeyGen, chỉ định Avatar ID và Voice ID mà các sếp muốn sử dụng. Node Webhook sẽ nhận tín hiệu callback từ HeyGen khi video render xong.
- **Store to Google Sheets & Get Caption from Sheets:** Kết nối tài khoản Google Sheets, trỏ tới file Google Sheet chuẩn bị sẵn để lưu trữ kịch bản, đường dẫn video và trạng thái xử lý.
- **INSTAGRAM & TIKTOK / Blotato Nodes:** Cấu hình credentials API hoặc webhook đăng bài để hệ thống tự động đẩy video lên các nền tảng mạng xã hội khi nhận được video hoàn chỉnh từ HeyGen Webhook.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** chạy thử thủ công với một bản ghi mẫu để kiểm tra xem dữ liệu có chảy mượt mà từ đầu đến cuối không.
- Sau khi test thành công, gạt công tắc **Active** ở góc trên cùng bên phải để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm bước duyệt nội dung (Human-in-the-loop):** Trước khi gửi lệnh tạo video qua HeyGen hoặc đăng lên mạng xã hội, các sếp có thể tích hợp thêm node Telegram hoặc Slack để gửi thông báo kèm kịch bản, yêu cầu sếp bấm nút "Phê duyệt" hoặc "Chỉnh sửa".
- **Lưu trữ đa nền tảng:** Lưu trữ bản backup video gốc vào Google Drive hoặc Dropbox để dễ dàng tái sử dụng cho các chiến dịch quảng cáo trả phí (Paid Ads).
- **Tự động tạo Thumbnail:** Thêm một node xử lý hình ảnh hoặc dùng AI (như DALL-E / Midjourney API) để tạo ảnh thumbnail bắt mắt đính kèm khi đăng bài lên TikTok/Instagram.

### 📌 Kết luận
Workflow tự động hóa tạo video AI từ tin tức với HeyGen và n8n là vũ khí tối tân giúp các sếp thống trị các nền tảng video ngắn mà không tốn nhiều nguồn lực. Hãy thiết lập ngay hôm nay để bứt phá lượng tiếp cận và doanh thu từ mạng xã hội!