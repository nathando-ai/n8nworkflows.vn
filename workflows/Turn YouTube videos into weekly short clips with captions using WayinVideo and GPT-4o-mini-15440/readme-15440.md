---
title: "🎥 Tự động hóa nội dung: Chuyển đổi video YouTube thành clip ngắn hàng tuần với phụ đề bằng n8n"
description: "Hướng dẫn tự động hóa quy trình chuyển đổi video YouTube thành clip ngắn hàng tuần với phụ đề bằng n8n, WayinVideo và GPT-4o-mini. Tiết kiệm thời gian và nâng cao hiệu quả nội dung."
slug: "tu-dong-hoa-chuyen-doi-video-youtube-thanh-clip-ngan-hang-tuan"
tags: [n8n, automation, no-code, content-creation, ai]
keywords: [n8n workflow, tự động hóa nội dung, video YouTube, clip ngắn, phụ đề tự động]
---

# 🎥 Tự động hóa nội dung: Chuyển đổi video YouTube thành clip ngắn hàng tuần với phụ đề bằng n8n

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các nhà sáng tạo nội dung khi phải xử lý thủ công hàng trăm video YouTube. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian xử lý hàng tuần: Tự động hóa quy trình từ 30-60 phút xuống còn vài giây.
- Tăng hiệu quả nội dung: Tạo ra 3 clip ngắn chất lượng cao từ mỗi video gốc.
- Cá nhân hóa nội dung: Phụ đề và hashtag được tối ưu riêng cho từng nền tảng.
- Hoạt động liên tục: Chạy tự động mỗi thứ Hai lúc 9h sáng mà không cần can thiệp.
- Tăng tương tác: Clip ngắn với phụ đề hấp dẫn giúp tăng tỷ lệ tương tác lên 30-50%.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Workspace (Google Sheets, Google Drive)
- API Key từ WayinVideo
- API Key từ OpenAI (cho GPT-4o-mini)
- Google Sheets với 2 tab:
  1. Video List: Chứa danh sách video cần xử lý (cột: Video URL, Video Title, Niche/Category, Status)
  2. Content Calendar: Lưu kết quả xử lý (cột: Video URL, Video Title, Niche, Video Summary, Clip Number, Clip Title, Clip Score, Clip Timestamp, WayinVideo Export Link, Google Drive Link, TikTok Caption, Facebook Caption, LinkedIn Caption, Hashtags, Processed On, Status)
- Thư mục Google Drive để lưu clip đã xử lý
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/15440](https://n8n.io/workflows/15440)
2. Nhấn nút "Import" trên trang workflow
3. Trong n8n Editor, chọn "Import from URL" và dán URL workflow
4. Hoàn tất import

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node 3, 5, 9, 11 (WayinVideo APIs)**:
   - Thay thế `YOUR_WAYINVIDEO_API_KEY` bằng API Key thực của bạn
   - Đảm bảo tài khoản WayinVideo có đủ credit

2. **Node 16 (OpenAI - GPT-4o-mini Model)**:
   - Kết nối với OpenAI credential của bạn
   - Đảm bảo tài khoản OpenAI có đủ credit

3. **Node 2 và 21 (Google Sheets - Video List)**:
   - Kết nối với Google Sheets OAuth2
   - Thay thế `YOUR_VIDEO_LIST_SHEET_ID` bằng ID của Google Sheet chứa tab Video List

4. **Node 20 (Google Sheets - Content Calendar)**:
   - Kết nối với Google Sheets OAuth2
   - Thay thế `YOUR_CONTENT_CALENDAR_SHEET_ID` bằng ID của Google Sheet chứa tab Content Calendar

5. **Node 19 (Google Drive - Upload Clip)**:
   - Kết nối với Google Drive OAuth2
   - Thay thế `YOUR_GOOGLE_DRIVE_FOLDER_ID` bằng ID thư mục lưu clip

6. **Cấu hình Google Sheets**:
   - Tạo tab Video List với các cột: Video URL, Video Title, Niche/Category, Status
   - Tạo tab Content Calendar với các cột: Video URL, Video Title, Niche, Video Summary, Clip Number, Clip Title, Clip Score, Clip Timestamp, WayinVideo Export Link, Google Drive Link, TikTok Caption, Facebook Caption, LinkedIn Caption, Hashtags, Processed On, Status

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu:
   - Thêm 1-2 video vào tab Video List với Status = "Pending"
   - Chạy workflow bằng tay (nhấn "Execute Workflow")
   - Kiểm tra kết quả trên tab Content Calendar và Google Drive

2. Bật Active workflow:
   - Sau khi test thành công, nhấn "Activate" để workflow chạy tự động mỗi thứ Hai lúc 9h sáng

### ✍️ Mẹo & gợi ý nâng cao
1. **Tối ưu chi phí**:
   - Thay đổi thời gian chạy từ mỗi thứ Hai sang mỗi ngày để xử lý lượng video lớn hơn
   - Giảm số lượng clip từ 3 xuống 2 để tiết kiệm credit WayinVideo

2. **Tích hợp thêm nền tảng**:
   - Thêm node để tự động đăng clip lên TikTok, Facebook và LinkedIn
   - Sử dụng node Slack/Telegram để thông báo khi workflow hoàn thành

3. **Phân tích hiệu quả**:
   - Thêm node để theo dõi số lượt xem và tương tác của các clip đã đăng
   - Tạo báo cáo hàng tuần về hiệu quả của các clip đã tạo

4. **Quản lý nội dung**:
   - Thêm node để tự động dịch phụ đề sang các ngôn ngữ khác
   - Tạo hệ thống đánh giá tự động cho nội dung được tạo

### 📌 Kết luận
Workflow này giúp các nhà sáng tạo nội dung tự động hóa quy trình chuyển đổi video YouTube thành clip ngắn hàng tuần với phụ đề chất lượng cao. Bằng cách tích hợp n8n, WayinVideo và GPT-4o-mini, các sếp có thể tiết kiệm thời gian đáng kể và nâng cao hiệu quả nội dung một cách đáng kể. Hãy áp dụng ngay để bắt đầu tự động hóa nội dung của bạn!