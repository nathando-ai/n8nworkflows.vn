---
title: "🚀 Tự động hóa sản xuất kịch bản Video đa nền tảng (YouTube, Reels, TikTok) bằng n8n, GPT-4o-mini, Google Sheets và Gmail"
description: "Biến một ý tưởng thành 3 kịch bản video hoàn chỉnh cho YouTube, Instagram Reels và TikTok chỉ với một form điền. Tự động lưu Google Sheets và gửi email."
slug: "tu-dong-hoa-kich-ban-video-youtube-reels-tiktok-n8n"
tags: [n8n, automation, content-creation, openai, google-sheets, gmail, ai-agent]
keywords: [n8n workflow, tạo kịch bản video tự động, gpt-4o-mini youtube script, n8n ai agent, tự động hóa marketing]
---

# 🚀 Tự động hóa sản xuất kịch bản Video đa nền tảng với AI

Các sếp làm sáng tạo nội dung (Content Creator), quản lý mạng xã hội (Social Media Manager) hay agency marketing chắc chắn luôn cảm thấy "ngợp" mỗi khi phải ngồi viết lại một chủ đề thành các định dạng kịch bản khác nhau cho YouTube (dài), Instagram Reels (vừa có visual cues) và TikTok (ngắn gọn, giật gân). Việc này vừa tốn hàng giờ đồng hồ, vừa dễ bị cạn kiệt ý tưởng diễn đạt.

Workflow n8n này chính là "vũ khí bí mật" giúp các sếp giải quyết triệt để bài toán trên! Chỉ với **một lần nhập chủ đề duy nhất qua form**, hệ thống sẽ sử dụng sức mạnh của **GPT-4o-mini** để đồng thời sản xuất 3 kịch bản chuẩn chỉnh cho 3 nền tảng, tự động lưu vào **Google Sheets** để làm kho lưu trữ, và gom tất cả gửi thẳng vào **Gmail** của các sếp chỉ trong một nốt nhạc.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 không lo mất kết nối, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Biến 1 ý tưởng thành 3 kịch bản chuyên nghiệp (YouTube 700-900 từ, Reels 100-130 từ kèm chú thích hình ảnh, TikTok 50-70 từ có câu hỏi tương tác).
- **Đồng bộ hóa dữ liệu thông minh:** Tự động ghi nhận toàn bộ kịch bản vào Google Sheets để quản lý chiến dịch dài hạn.
- **Trải nghiệm liền mạch:** Nhận ngay trọn bộ 3 kịch bản gọn gàng trong một email duy nhất ngay sau khi AI hoàn thành.
- **Cá nhân hóa cao:** Dựa trên tệp khán giả, ngách (niche) và giọng văn (tone of voice) do các sếp thiết lập.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ TRƯỚC KHI "LÊN ĐỒ"]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **OpenAI API Key** (Sử dụng model `gpt-4o-mini` tối ưu chi phí và tốc độ).
- **Google Sheets & Gmail** (Tài khoản Google có kết nối OAuth2 trong n8n).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy file JSON của workflow này và paste trực tiếp vào giao diện n8n Editor của mình, hoặc sử dụng tính năng Import từ tệp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình chính xác các node sau để workflow chạy mượt mà:

- **1. Form — Multi-Platform Video Topic**: Nơi người dùng (hoặc các sếp) điền chủ đề video, tệp khách hàng, ngách, tone giọng và tên người gửi.
- **2. Set — Config Values**: **(CỰC KỲ QUAN TRỌNG)** Các sếp nhớ thay thế các giá trị mẫu bằng thông tin thực tế của mình:
  - `PASTE_YOUR_GOOGLE_SHEET_ID_HERE` -> ID bảng Google Sheet của các sếp.
  - `PASTE_YOUR_EMAIL_HERE` -> Email nhận kịch bản.
  - `PASTE_YOUR_NAME_HERE` -> Tên của các sếp.
- **4. OpenAI — GPT-4o-mini Model**: Kết nối OpenAI Credential của các sếp và đảm bảo model đang chọn là `gpt-4o-mini`.
- **7. Google Sheets — Log Video Scripts**: Kết nối Google Sheets OAuth2 credential. Đảm bảo các sếp đã tạo sẵn một Sheet có tab tên là **`Video Scripts`** với các cột: `Date`, `Topic`, `Platform`, `Script Length`, `Hook`, `Script`, `CTA`, `Tags`, `Submitted By`.
- **10. Gmail — Send Scripts Email**: Kết nối Gmail OAuth2 credential để hệ thống tự động bắn email tổng hợp kịch bản.

#### 3. Kích hoạt ⚡️
- Chạy thử (Test step/Test execution) bằng cách gửi một dữ liệu mẫu qua Form Trigger.
- Kiểm tra kết quả trên Google Sheets và hộp thư Gmail xem đã nhận đủ 3 kịch bản chưa.
- Nếu mọi thứ mượt mà, hãy gạt công tắc sang **Active** để đưa workflow vào vận hành chính thức 24/7!

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Chatbot:** Thay vì dùng Form Trigger, các sếp có thể đổi thành Telegram Trigger hoặc Slack Trigger để nhập chủ đề nhanh chóng ngay trên điện thoại.
- **Lưu trữ tự động vào Notion:** Có thể bổ sung node Notion sau bước AI Agent để lưu kịch bản vào cơ sở dữ liệu Notion thay vì Google Sheets nếu team các sếp đang dùng Notion làm Workspace chính.
- **Tạo ảnh Thumbnail tự động:** Kết hợp thêm một node gọi OpenAI DALL-E 3 hoặc Midjourney API để sinh ảnh đại diện cho YouTube ngay trong cùng một luồng.

### 📌 Kết luận
Với workflow n8n này, việc lên ý tưởng và sản xuất kịch bản video đa nền tảng chưa bao giờ dễ dàng và chuyên nghiệp đến thế. Hãy cài đặt ngay hôm nay để giải phóng thời gian sáng tạo của các sếp!