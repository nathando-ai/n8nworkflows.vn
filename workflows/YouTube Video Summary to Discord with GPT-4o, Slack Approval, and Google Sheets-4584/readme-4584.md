---
title: "🚀 Tự động hóa YouTube: Tóm tắt video, duyệt Slack và đăng lên Discord với GPT-4o"
description: "Giải pháp tự động hóa hoàn chỉnh giúp theo dõi video YouTube mới, tóm tắt nội dung bằng AI, lưu vào Google Sheets và đăng lên Discord sau khi được duyệt qua Slack"
slug: "tu-dong-hoa-youtube-tom-tat-video-slack-discord-gpt-4o"
tags: [n8n, automation, no-code, youtube, discord, slack, google-sheets, ai]
keywords: [n8n workflow, tự động hóa youtube, tóm tắt video, discord, slack, google sheets, gpt-4o]
---

# 🚀 Tự động hóa YouTube: Tóm tắt video, duyệt Slack và đăng lên Discord với GPT-4o

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 80% thời gian thủ công khi xử lý video YouTube
- Tự động tóm tắt nội dung dài bằng AI GPT-4o
- Đảm bảo chất lượng nội dung qua hệ thống duyệt Slack
- Đồng bộ thông tin đến nhiều nền tảng (Google Sheets, Discord)
- Hoạt động liên tục 24/7 mà không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản YouTube (để lấy RSS feed)
- API Key của YouTube Data API
- Tài khoản Google với quyền truy cập Google Sheets
- Tài khoản Slack với quyền gửi tin nhắn
- Tài khoản Discord với quyền đăng tin
- API Key của OpenAI (cho GPT-4o)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/4584)
2. Click vào nút "Import" ở góc trên bên phải
3. Copy toàn bộ JSON workflow và dán vào n8n Editor của bạn

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "YouTube RSS Trigger"**:
   - Cập nhật URL RSS feed của kênh YouTube bạn muốn theo dõi
   - Ví dụ: `https://www.youtube.com/feeds/videos.xml?channel_id=UC...`

2. **Node "Extract Channel ID"**:
   - Kiểm tra và điều chỉnh đoạn code JavaScript nếu cần
   - Đảm bảo nó có thể trích xuất đúng Channel ID từ URL video

3. **Node "Fetch Video Details"**:
   - Thêm API Key của YouTube Data API vào credentials
   - Kiểm tra các tham số đầu ra cần thiết (videoTitle, videoDescription, videoPublishedAt, videoURL)

4. **Node "OpenAI GPT Summary Model"**:
   - Cập nhật API Key của OpenAI
   - Đảm bảo chọn đúng model (gpt-4o-mini)
   - Điều chỉnh prompt nếu cần cho phù hợp với nội dung video

5. **Node "Store results to Google Sheet"**:
   - Thiết lập Google Sheets OAuth2 credentials
   - Chỉ định đúng Spreadsheet ID và tên Sheet
   - Kiểm tra các trường dữ liệu cần lưu (Title, Video URL, Summary, Video Published Date)

6. **Node "Send Summary for Approval"**:
   - Cấu hình Slack credentials
   - Chỉ định đúng channel ID để gửi tin nhắn
   - Tùy chỉnh nội dung tin nhắn nếu cần

7. **Node "Post Approved Summary"**:
   - Cấu hình Discord credentials
   - Chỉ định đúng channel ID để đăng tin
   - Tùy chỉnh định dạng tin nhắn nếu cần

#### 3. Kích hoạt ⚡️
1. Test run workflow với một video mẫu
2. Kiểm tra tất cả các node hoạt động đúng
3. Bật Active workflow để bắt đầu theo dõi liên tục

### ✍️ Mẹo & gợi ý nâng cao
1. **Tùy chỉnh tóm tắt**: Điều chỉnh prompt trong node "OpenAI GPT Summary Model" để phù hợp với phong cách nội dung của bạn
2. **Thông báo lỗi**: Thêm node gửi email hoặc Slack thông báo khi workflow gặp lỗi
3. **Lịch sử phiên bản**: Thêm trường "Version" trong Google Sheets để theo dõi các phiên bản tóm tắt
4. **Báo cáo định kỳ**: Tạo workflow phụ để gửi báo cáo tổng hợp hàng tuần qua email

### 📌 Kết luận
Workflow này mang lại giải pháp toàn diện cho việc tự động hóa quản lý nội dung từ YouTube, giúp các sếp tiết kiệm thời gian và đảm bảo chất lượng nội dung. Với hệ thống duyệt Slack và đăng tin tự động, bạn có thể duy trì một luồng thông tin chuyên nghiệp mà không cần can thiệp thủ công. Hãy thử ngay và nâng cao hiệu suất làm việc của đội ngũ!