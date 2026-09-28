---
title: "🚀 Tự động hóa sản xuất & đăng tải video AI Avatar tin tức với HeyGen và Blotato"
description: "Xây dựng phòng thu tin tức tự động 100%: Quét tin tức AI, viết kịch bản bằng AI Agent, tạo video avatar dọc qua HeyGen và tự động phát hành lên đa nền tảng mạng xã hội qua Blotato."
slug: "tu-dong-hoa-tao-video-ai-avatar-heygen-blotato"
tags: [n8n, automation, no-code, heygen, blotato, ai-video, content-creation]
keywords: [n8n workflow, tạo video ai tự động, heygen api, blotato publishing, ai agent n8n, tự động hóa kênh tiktok youtube shorts]
---

# 🚀 Tự động hóa sản xuất & đăng tải video AI Avatar tin tức với HeyGen và Blotato

Các sếp có đang tốn hàng giờ mỗi ngày để cập nhật tin tức công nghệ, viết kịch bản, quay dựng video dọc (Reels/Shorts/TikTok) và thủ công đăng tải lên từng nền tảng? Công việc lặp đi lặp lại này ngốn rất nhiều thời gian mà hiệu quả đôi khi không ổn định.

Hãy tưởng tượng sở hữu một **"phòng thu tin tức tự động trong một chiếc hộp" (Newsroom in a Box)**: Tự động quét tin hot, chọn lọc câu chuyện viral nhất, nhờ AI viết kịch bản 30 giây, tạo video người đại diện ảo (AI Avatar) chuyên nghiệp và tự động đẩy lên TikTok, Instagram, YouTube Shorts mà các sếp không cần chạm tay vào bất kỳ công đoạn thủ công nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Loại bỏ hoàn toàn khâu viết kịch bản thủ công, dựng video và đăng bài.
- **Sản xuất nội dung 24/7:** Workflow chạy tự động theo lịch hẹn, giúp kênh luôn duy trì độ phủ sóng và tương tác đều đặn.
- **Đa nền tảng (Omnichannel):** Đồng bộ hóa việc xuất bản video lên TikTok, YouTube Shorts, Instagram Reels, Facebook... thông qua Blotato.
- **Chất lượng chuyên nghiệp:** Sử dụng AI tiên tiến nhất (`o3-mini`, `AI Agent`) và công nghệ tạo video avatar chân thực từ HeyGen.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n v1.105.4+** (Bản Cloud hoặc Self-hosted).
- Tài khoản **OpenAI** (hoặc LM Chat OpenAI) với API Key hoạt động tốt.
- Tài khoản **HeyGen** kèm API Key, `avatar_id` và `voice_id` của các sếp.
- Tài khoản **Blotato** kèm API Key và ID các kênh mạng xã hội đích.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của template này và import trực tiếp vào n8n Editor của các sếp, hoặc sử dụng tính năng copy/paste JSON trực tiếp vào giao diện làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình chính xác các thông số cốt lõi sau:

- **Schedule Trigger1:** Cài đặt lại khung giờ chạy tự động hàng ngày (mặc định đang để 10:00 sáng).
- **AI Agent1 & Write Script1 (`o3-mini`):** Kiểm tra cấu hình kết nối OpenAI. Các sếp có thể tinh chỉnh prompt trong AI Agent để chuyển chủ đề từ tin tức AI/LLM sang bất kỳ lĩnh vực nào các sếp muốn (Crypto, Marketing, Tech...).
- **Setup Heygen1 (Node Set):** Điền chính xác các thông số:
  - `heygen_api_key`
  - `avatar_id` và `voice_id` của riêng các sếp.
  - `background_video_url` (tuỳ chọn video nền cho video dọc 9:16).
- **Prepare for Publish1 (Node Set):** Nhập `blotato_api_key` và các ID định danh nền tảng đích (TikTok, YouTube, Instagram...).
- **Các node `[TikTOK] Publish via Blotato...`:** Các node đăng bài này đang được **tắt (disabled) mặc định**. Các sếp hãy bật (enable) những nền tảng nào mình thực sự muốn tự động đăng.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (Test workflow) để kiểm tra luồng dữ liệu từ việc quét RSS đến khâu tạo video qua HeyGen.
- Sau khi mọi thứ mượt mà, gạt công tắc sang **Active** để hệ thống tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp cảnh báo Telegram/Slack:** Thêm một node Telegram ngay sau bước hoàn thành video để gửi thông báo kèm bản xem trước (preview) về điện thoại của các sếp trước khi bấm đăng.
- **Quản lý lịch sử qua Google Sheets:** Lưu lại tiêu đề, kịch bản, và link video đã tạo vào Google Sheets để tiện theo dõi kho nội dung.
- **Đa ngôn ngữ:** Dễ dàng thay đổi ngôn ngữ trong prompt của AI Agent nếu các sếp muốn làm kênh tin tức bằng tiếng Anh, tiếng Trung hoặc các thứ tiếng khác.

### 📌 Kết luận
Với workflow tự động hóa này, việc duy trì một kênh video tin tức triệu view không còn là gánh nặng nhân sự. Hãy thiết lập ngay hôm nay và để AI làm thay phần việc nặng nhọc nhất cho doanh nghiệp của các sếp!