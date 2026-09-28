---
title: "🚀 Tự động kéo dài & ghép video UGC Viral bằng Kling 2.1, đăng tải đa nền tảng MXH"
description: "Hướng dẫn xây dựng quy trình n8n tự động hóa hoàn toàn việc mở rộng video ngắn, ghép nối mượt mà bằng AI Kling 2.1 và đăng lên TikTok, Instagram, YouTube, Facebook."
slug: "tu-dong-keo-dai-ghep-video-ugc-viral-kling-2.1"
tags: [n8n, automation, ai-video, kling-2.1, social-media, content-creation]
keywords: [n8n workflow, tự động hóa video, Kling 2.1, AI video generation, đăng video tự động, Postiz, Fal AI]
---

# 🚀 Tự động kéo dài & ghép video UGC Viral bằng Kling 2.1, đăng tải đa nền tảng MXH

Việc sản xuất và biên tập các video UGC (User Generated Content) dạng ngắn để chạy quảng cáo hoặc làm viral marketing thường ngốn rất nhiều thời gian của anh em Content Creator. Đặc biệt là công đoạn cắt ghép, tạo các phân đoạn nối tiếp sao cho khớp màu sắc, bối cảnh và tự động hóa việc đăng tải lên hàng loạt nền tảng mạng xã hội.

Giải pháp thủ công vừa chậm chạp lại dễ thiếu sót. Workflow n8n này sinh ra để giải quyết triệt để bài toán đó: tự động đọc dữ liệu từ Google Sheets, trích xuất khung hình cuối, dùng AI **Kling 2.1** sinh tiếp đoạn video nối dài, ghép nối hoàn chỉnh, lưu trữ Google Drive và tự động phân phối lên **TikTok, Instagram, Facebook, YouTube, X (Twitter)** thông qua Postiz và Upload-Post.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 (vì AI render video mất thời gian chờ), các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Biến video ngắn thành video dài hơn, mượt mà nhờ AI mà không cần dùng Premiere hay CapCut thủ công.
- **Đa nền tảng (Omnichannel):** Đăng đồng loạt lên TikTok, Instagram, Facebook, YouTube chỉ với một dòng lệnh kích hoạt.
- **Đồng bộ dữ liệu thông minh:** Tự động cập nhật trạng thái, link video hoàn thiện vào Google Sheets để dễ dàng theo dõi.
- **Hoạt động không nghỉ:** Tích hợp sẵn cơ chế `Wait` thông minh để chờ các tiến trình AI render xong mà không sợ lỗi timeout.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Fal.ai:** Lấy API Key để dùng dịch vụ trích xuất khung hình (`Extract last frame`) và ghép video (`Merge Videos`).
- **Tài khoản Runpod (Kling 2.1):** Lấy API Token để gọi mô hình AI tạo clip kéo dài (`Generate clip`).
- **Tài khoản Postiz:** Để quản lý và đăng video lên các nền tảng MXH (TikTok, Instagram, Facebook, X).
- **Tài khoản Upload-Post:** Hỗ trợ đăng tải chuyên biệt lên YouTube.
- **Google Sheets & Google Drive:** Lưu trữ file đầu vào, cập nhật kết quả và lưu video thành phẩm.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này và import trực tiếp vào n8n Editor của các sếp, hoặc sử dụng tính năng copy/paste JSON.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 26 nodes phối hợp nhịp nhàng, các sếp chú ý cấu hình kỹ các điểm sau:
- **Google Sheets nodes (`Get video`, `Update video url`, `Get videos to merge`...):** Kết nối tài khoản Google Sheets OAuth2 và trỏ tới file [Google Sheet mẫu tại đây](https://docs.google.com/spreadsheets/d/14zlCDJFLrJIhcq7HwFGdKAHIwvjmkwP-FSTHmLTj0ow/edit?usp=sharing). Điền đầy đủ các cột `START`, `PROMPT` và `DURATION` (5 hoặc 10 giây cho Kling 2.1).
- **Node `Extract last frame` & `Merge Videos` (Fal.ai):** Cấu hình `Header Auth` với Name là `Authorization`, Value là `Key YOURAPIKEY` (lấy từ Fal.ai).
- **Node `Generate clip` (Runpod - Kling 2.1):** Cấu hình `Bearer Auth` với token từ Runpod.
- **Node `Upload to Social` (Postiz):** Cấu hình `postizApi` credentials và thiết lập `Channel_ID`, `TITLE` cho các kênh MXH.
- **Node `Upload to Youtube` (Upload-Post):** Cấu hình `httpHeaderAuth`, set `_USERNAME` và `TITLE` theo hướng dẫn của Upload-Post.

#### 3. Kích hoạt ⚡️
- Bấm nút `When clicking ‘Execute workflow’` để test chạy thử với 1 dòng dữ liệu mẫu trong Google Sheet.
- Kiểm tra xem video đã được sinh, ghép và đẩy lên Google Drive / MXH thành công chưa.
- Sau khi mọi thứ mượt mà, bật nút **Active** để workflow chạy tự động theo lịch hoặc trigger.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Telegram/Slack Bot:** Thêm một node Telegram ở cuối chuỗi để bắn thông báo kèm link video trực tiếp về máy mỗi khi render xong một video viral.
- **Quản lý lỗi (Error Handling):** Bổ sung thêm nhánh `Error Trigger` để nếu AI Fal.ai hoặc Runpod quá tải/lỗi, hệ thống sẽ tự động ghi log vào Google Sheets ở cột trạng thái "Failed" để tiện kiểm tra lại.
- **Lập lịch tự động (Cron):** Thay vì dùng Manual Trigger, các sếp có thể đổi thành Schedule Trigger để hệ thống tự động quét Google Sheet mỗi ngày vào khung giờ vàng và sản xuất video đều đặn.

### 📌 Kết luận
Quy trình tự động hóa này là một "vũ khí bí mật" cực kỳ mạnh mẽ cho các agency marketing hoặc các nhà sáng tạo nội dung muốn scale-up số lượng video viral lên các nền tảng mà tốn cực kỳ ít sức lao động thủ công. Triển khai ngay thôi các sếp ơi!