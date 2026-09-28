---
title: "🎥 Tự động hóa YouTube: Chuyển đổi Video thành Báo cáo GEO với Whisper & GPT-4o-mini trong Notion"
description: "Hướng dẫn tự động hóa hoàn toàn quy trình chuyển đổi video YouTube thành báo cáo GEO (Goal-Execution-Outcome) bằng công nghệ AI Whisper và GPT-4o-mini, lưu trữ kết quả vào Notion."
slug: "tu-dong-hoa-youtube-whisper-gpt4o-mini-notion"
tags: [n8n, automation, no-code, youtube, notion, ai, summarization]
keywords: [n8n workflow, tự động hóa video, báo cáo GEO, Whisper, GPT-4o-mini, Notion]
---

# 🎥 Tự động hóa YouTube: Chuyển đổi Video thành Báo cáo GEO với Whisper & GPT-4o-mini trong Notion

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm **80% thời gian** xử lý video thủ công
- Tạo báo cáo **GEO chuẩn** (Goal-Execution-Outcome) từ bất kỳ video YouTube nào
- **Tự động hóa hoàn toàn** quy trình từ tải video đến lưu trữ kết quả
- **Tích hợp liền mạch** với Notion - công cụ quản lý kiến thức yêu thích của các sếp
- **Cá nhân hóa** báo cáo theo nhu cầu cụ thể của từng dự án
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản **YouTube** với quyền truy cập API
- API Key từ **OpenAI** (để sử dụng Whisper và GPT-4o-mini)
- Tài khoản **Notion** với Database đã tạo sẵn
- API Key từ **RapidAPI** (để tải audio từ YouTube)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/11083)
2. Click vào nút **"Copy to clipboard"** để sao chép JSON workflow
3. Trong n8n Editor, click vào **"Import from Clipboard"** và dán JSON đã sao chép

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
**Node quan trọng nhất cần cấu hình:**
- **Schedule Trigger**: Thiết lập tần suất chạy workflow (mặc định: hàng giờ)
- **HTTP - Get YouTube Audio**: Thay thế placeholder RapidAPI key bằng key thực tế
- **Notion - Create GEO Summary Page**: Cập nhật Notion Database ID theo workspace của bạn
- **YouTube - Fetch Video Details**: Kết nối với tài khoản YouTube OAuth2 của bạn
- **OpenAI - Transcribe Audio (Whisper)**: Kết nối với OpenAI API key của bạn

**Lưu ý quan trọng:**
- Thay thế video ID cứng (hardcoded) bằng input động hoặc nguồn playlist
- Test với 1 video trước khi kích hoạt schedule để đảm bảo workflow hoạt động đúng
- Xóa tất cả token cá nhân trước khi chia sẻ template

#### 3. Kích hoạt ⚡️
1. Click vào nút **"Execute Workflow"** để test với dữ liệu mẫu
2. Sau khi xác nhận hoạt động đúng, click vào **"Activate"** để bật workflow

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Teams**: Thêm node gửi thông báo khi có video mới được xử lý
- **Lưu log hoạt động**: Thêm node lưu log vào Google Sheets hoặc Notion
- **Tự động gửi báo cáo**: Thiết lập gửi báo cáo định kỳ qua email hoặc Slack
- **Xử lý nhiều video cùng lúc**: Sử dụng node "Split" để xử lý nhiều video trong 1 lần chạy

### 📌 Kết luận
Workflow này là giải pháp hoàn hảo cho các sếp muốn **tự động hóa hoàn toàn** quy trình chuyển đổi video YouTube thành báo cáo GEO chuyên nghiệp, mà không cần phải can thiệp thủ công. Với tích hợp liền mạch với Notion và công nghệ AI tiên tiến, workflow này sẽ giúp các sếp **tiết kiệm thời gian, nâng cao hiệu suất và tạo ra nội dung có giá trị hơn**. Hãy thử ngay và trải nghiệm cách làm việc thông minh hơn!