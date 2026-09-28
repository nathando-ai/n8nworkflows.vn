---
title: "🎬 Tự động hóa phân tích video đối thủ bằng AI và gửi báo cáo qua Gmail"
description: "Hướng dẫn tự động hóa workflow n8n để theo dõi video đối thủ trên YouTube, tổng kết nội dung bằng AI và gửi báo cáo qua email tự động."
slug: "tu-dong-hoa-phan-tich-video-doi-thu-bang-ai-va-gmail"
tags: [n8n, automation, no-code, ai, market-research]
keywords: [n8n workflow, tự động hóa, phân tích thị trường, ai summarization, gmail]
---

# 🎬 Tự động hóa phân tích video đối thủ bằng AI và gửi báo cáo qua Gmail

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa toàn bộ quy trình từ phân tích đến gửi báo cáo.
- Chính xác: Sử dụng AI để tổng kết nội dung video một cách chi tiết và chính xác.
- Cá nhân hóa: Tùy chỉnh báo cáo theo nhu cầu của từng doanh nghiệp.
- Hoạt động liên tục: Workflow chạy tự động 24/7 mà không cần can thiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Gmail để gửi báo cáo.
- API Key từ WayinVideo để phân tích video.
- Kiến thức cơ bản về n8n và cách cấu hình các node.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn.
2. Nhấn vào nút "Import from URL" và dán link sau: [https://n8n.io/workflows/14408](https://n8n.io/workflows/14408).
3. Hoặc tải file JSON về và import trực tiếp từ máy tính.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

- **Node "🎬 Submit Video for Summary" (httpRequest)**:
  - Thêm credentials cho API WayinVideo.
  - Thay thế `YOUR_WAYINVIDEO_API_KEY` bằng API Key thực tế của bạn.
  - Tùy chỉnh `target_lang` để thay đổi ngôn ngữ của báo cáo (ví dụ: "en", "vi", "fr").

- **Node "📧 Build Competitor Analysis Email" (code)**:
  - Chỉnh sửa template HTML để phù hợp với thương hiệu của bạn.
  - Thêm hoặc bớt các phần như hashtags, highlights theo nhu cầu.

- **Node "📨 Send Analysis via Gmail" (gmail)**:
  - Thêm credentials cho Gmail.
  - Thay thế `YOUR_REPORT_EMAIL@domain.com` bằng địa chỉ email nhận báo cáo.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng.
- Bật Active workflow để bắt đầu tự động hóa.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi báo cáo được gửi.
- Lưu log các báo cáo đã gửi để theo dõi lịch sử phân tích.
- Gửi báo cáo định kỳ hàng tuần hoặc hàng tháng cho các video đối thủ quan trọng.

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian và công sức trong việc phân tích video đối thủ. Bằng cách tự động hóa quy trình, các sếp có thể tập trung vào các chiến lược quan trọng hơn. Hãy áp dụng ngay để nâng cao hiệu suất làm việc!