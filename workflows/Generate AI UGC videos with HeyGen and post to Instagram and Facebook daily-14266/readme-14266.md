---
title: "🚀 Tự động hóa sản xuất video UGC bằng AI (HeyGen + OpenAI) và đăng tải lên Facebook, Instagram mỗi ngày"
description: "Xây dựng hệ thống tự động hóa hoàn toàn quy trình tạo video người ảo (UGC) bằng AI thông qua HeyGen và OpenAI, sau đó tự động xuất bản lên Instagram và Facebook hàng ngày."
slug: "tu-dong-hoa-video-ugc-heygen-instagram-facebook"
tags: [n8n, automation, heygen, openai, instagram, facebook, content-creation, ai-ugc]
keywords: [n8n workflow, tạo video ai, heygen automation, đăng video tự động instagram facebook, openai gpt script, ugc video ai]
---

# 🚀 Tự động hóa sản xuất video UGC bằng AI (HeyGen + OpenAI) và đăng tải lên Facebook, Instagram mỗi ngày

Các sếp có đang cảm thấy quá tải khi mỗi ngày phải nghĩ kịch bản, quay dựng video UGC (User Generated Content) thủ công, rồi lại mất hàng giờ để đăng lên các nền tảng mạng xã hội không? Quy trình này ngốn rất nhiều thời gian và chi phí nhân sự.

Giải pháp ở đây chính là workflow n8n tự động hóa 100% từ A-Z: Hệ thống sẽ tự động bốc ý tưởng từ Google Sheets, nhờ OpenAI viết kịch bản chuẩn SEO/viral, điều khiển HeyGen tạo video người ảo (talking-head), và cuối cùng là tự động đăng tải lên Facebook, Instagram mỗi ngày mà không cần một chạm tay thủ công nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không cần quay dựng thủ công, hàng loạt video UGC được sản xuất tự động mỗi ngày.
- **Vòng lặp thông minh:** Nội dung được lấy từ Google Sheets và xoay vòng tự động theo năm, không lo bị lặp lại.
- **Đa nền tảng:** Tự động hóa việc xuất bản đồng thời lên cả Instagram và Facebook (qua API trung gian).
- **Kiểm soát chặt chẽ:** Mọi trạng thái thành công hay thất bại đều được log lại chi tiết trong Google Sheets để dễ dàng kiểm tra.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance** (Self-hosted hoặc Cloud).
- **Tài khoản OpenAI API Key** (Dùng cho node `Generate Script`).
- **Tài khoản HeyGen API** (Dùng để tạo video người ảo).
- **Tài khoản Google Sheets** (Chứa kho nội dung "Workbook Content" và bảng "Production Logs").
- **Tài khoản đăng bài mạng xã hội** (Tích hợp qua API upload-post.com cho Facebook và Instagram).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn JSON của workflow (từ nguồn n8n.io/workflows/14266) và dán trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống vận hành trơn tru, các sếp cần cấu hình chính xác các node sau:
- **Schedule: Daily 9am**: Thiết lập khung giờ chạy tự động hàng ngày theo múi giờ mong muốn (ví dụ: 9:00 sáng).
- **Google Sheets (Get Workbook Content & Production Logs)**: Kết nối tài khoản Google Drive/Sheets, trỏ tới file Google Sheet quản lý nội dung của các sếp. Đảm bảo cấu trúc cột khớp với yêu cầu của workflow (có cột `Status = "Idea"`).
- **Generate Script (OpenAI)**: Điền thông tin OpenAI Credentials, cấu hình Model (khuyên dùng `gpt-4.1-mini` hoặc tương đương) với system prompt đóng vai "The Shepherd" để tạo kịch bản 30 giây (75-90 từ).
- **HTTP: HeyGen Generate Video**: Cấu hình Header chứa API Key của HeyGen để kích hoạt tiến trình render video.
- **Wait: HeyGen Processing & HTTP: Poll HeyGen Status**: Node `Wait` sẽ chờ 50 giây trước mỗi lần gọi lại (poll) trạng thái video từ HeyGen (tối đa 20 lần tương đương ~16 phút render).
- **facebook & instagram**: Cấu hình node HTTP request để đẩy video lên mạng xã hội. *Lưu ý:* Node `facebook` mặc định có thể đang ở trạng thái disable, các sếp nhớ enable lên khi đã sẵn sàng chạy thật.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để chạy thử thủ công và kiểm tra dữ liệu trả về ở từng node Code/Google Sheets.
- Nếu mọi thứ xanh mướt (success), các sếp hãy bật công tắc **Active** ở góc trên cùng bên phải để workflow chạy tự động hàng ngày.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Telegram/Slack Bot:** Thêm một node Telegram ở cuối luồng để bắn thông báo kèm link video vừa tạo về điện thoại cho các sếp duyệt trước hoặc nắm tình hình.
- **Mở rộng nền tảng:** Có thể bổ sung thêm các node HTTP để đẩy video lên TikTok, YouTube Shorts hoặc LinkedIn cùng lúc.
- **Quản lý lỗi thông minh:** Tận dụng node `Google Sheets: Log Failure` kết hợp bắn alert nếu HeyGen render lỗi quá thời gian timeout.

### 📌 Kết luận
Workflow "Generate AI UGC videos with HeyGen" là một cỗ máy marketing tự động cực kỳ mạnh mẽ, giúp doanh nghiệp tối ưu hóa chi phí sản xuất content video ngắn. Hãy triển khai ngay hôm nay để bứt phá lượt tiếp cận trên mạng xã hội!