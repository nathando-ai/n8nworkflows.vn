```yaml
---
title: "🚀 Tự động hóa tổng kết video YouTube bằng AI và xuất ra Google Docs"
description: "Workflow n8n giúp tự động hóa quá trình tổng kết video YouTube bằng AI, trích xuất bài học quan trọng và xuất ra Google Docs. Tiết kiệm thời gian và nâng cao hiệu suất làm việc."
slug: "tu-dong-hoa-tong-ket-video-youtube-bang-ai-va-xuat-ra-google-docs"
tags: [n8n, automation, no-code, AI, Google Docs]
keywords: [n8n workflow, tự động hóa, tổng kết video, AI, Google Docs]
---
```

# 🚀 Tự động hóa tổng kết video YouTube bằng AI và xuất ra Google Docs

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động tổng kết video YouTube mà không cần phải xem từng phút giây.
- Tăng hiệu suất: Xuất ra Google Docs với định dạng chuyên nghiệp, sẵn sàng sử dụng.
- Cá nhân hóa: Đáp ứng nhu cầu cụ thể của từng người dùng thông qua AI.
- Hoạt động liên tục: Tự động hóa quy trình mà không cần can thiệp thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Drive với quyền truy cập vào Google Docs.
- API Key từ OpenRouter để sử dụng mô hình Gemini 2.0 flash.
- API Key từ Supadata.ai để truy cập nội dung video YouTube.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:
- **When chat message received**: Node này sẽ kích hoạt workflow khi nhận được tin nhắn chat. Các sếp cần cấu hình để nhận tin nhắn từ nguồn chat của mình (ví dụ: Slack, Telegram, Discord).
- **supadata API - YouTube endpoint**: Node này sẽ gửi yêu cầu đến API của Supadata.ai để lấy nội dung transcript của video YouTube. Các sếp cần cấu hình API Key của Supadata.ai.
- **Gemini 2.0 flash**: Node này sử dụng mô hình Gemini 2.0 flash của OpenRouter để tổng kết nội dung transcript. Các sếp cần cấu hình API Key của OpenRouter.
- **Create new Google Doc with summary**: Node này sẽ tạo một Google Doc mới với nội dung tổng kết. Các sếp cần cấu hình tài khoản Google Drive và quyền truy cập vào Google Docs.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi workflow hoàn thành.
- Lưu log các hoạt động để theo dõi hiệu suất của workflow.
- Gửi báo cáo định kỳ về các video đã tổng kết để đánh giá hiệu quả của workflow.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa quá trình tổng kết video YouTube bằng AI, trích xuất bài học quan trọng và xuất ra Google Docs. Tiết kiệm thời gian và nâng cao hiệu suất làm việc. Các sếp hãy áp dụng ngay để trải nghiệm sự tiện lợi và hiệu quả của tự động hóa!