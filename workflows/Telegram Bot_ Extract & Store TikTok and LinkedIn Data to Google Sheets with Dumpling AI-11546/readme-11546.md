---
title: "🚀 Tự động hóa trích xuất dữ liệu TikTok & LinkedIn qua Telegram với Dumpling AI"
description: "Hướng dẫn tự động hóa trích xuất dữ liệu từ TikTok và LinkedIn qua Telegram, lưu vào Google Sheets và nhận thông báo qua email - hoàn toàn không cần code"
slug: "tu-dong-hoa-trich-xuat-du-lieu-tiktok-linkedin-qua-telegram"
tags: [n8n, automation, no-code, telegram, google-sheets]
keywords: [n8n workflow, tự động hóa, trích xuất dữ liệu, tiktok, linkedin]
---

# 🚀 Tự động hóa trích xuất dữ liệu TikTok & LinkedIn qua Telegram với Dumpling AI

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa toàn bộ quy trình trích xuất dữ liệu từ 2 nền tảng lớn nhất
- Chính xác: Sử dụng công nghệ AI Dumpling để trích xuất dữ liệu chính xác nhất
- Cá nhân hóa: Xử lý cả tin nhắn văn bản và giọng nói qua Telegram
- Hoạt động liên tục: Nhận thông báo email khi quá trình hoàn thành
- Tích hợp hoàn hảo: Lưu dữ liệu vào Google Sheets với cấu trúc rõ ràng
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Telegram và bot (tạo qua @BotFather)
- API key OpenAI (cho Whisper và GPT-4.1)
- Credentials Dumpling AI
- Google Sheets với 2 tab: TikTok và LinkedIn
- Tài khoản Gmail để nhận thông báo
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/11546](https://n8n.io/workflows/11546)
2. Click "Import" và chọn "Import from URL"
3. Dán link workflow vào ô nhập liệu
4. Click "Import" để hoàn tất

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Receive Telegram Message"**:
   - Chọn credentials Telegram đã tạo
   - Đảm bảo bot của bạn đã được thêm vào nhóm/channel cần theo dõi

2. **Node "OpenAI Chat Model"**:
   - Chọn credentials OpenAI
   - Đảm bảo tài khoản OpenAI có đủ credit
   - Model mặc định: gpt-4.1-mini

3. **Node "tiktok_profile_scraper" và "linkedin_profile_scraper"**:
   - Chọn credentials Dumpling AI
   - Đảm bảo credentials này đã được cấu hình đúng với API của Dumpling

4. **Node "tiktok_database_saver" và "linkedin_database_saver"**:
   - Chọn credentials Google Sheets
   - Cập nhật Sheet ID của bạn
   - Đảm bảo Google Sheets có cấu trúc đúng với các cột yêu cầu

5. **Node "Send Completion Email"**:
   - Chọn credentials Gmail
   - Cập nhật địa chỉ email nhận thông báo

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu:
   - Gửi tin nhắn "Scrape @charlidamelio" đến bot Telegram của bạn
   - Kiểm tra dữ liệu được lưu vào Google Sheets
   - Xác nhận email thông báo được gửi

2. Bật Active workflow:
   - Chọn workflow trong danh sách
   - Click "Activate" để bắt đầu chạy tự động

### ✍️ Mẹo & gợi ý nâng cao
1. **Tích hợp Slack/Teams**: Thêm node để gửi thông báo đến các kênh chat khác
2. **Lưu log hoạt động**: Thêm node để lưu log các yêu cầu trích xuất
3. **Xử lý lỗi tự động**: Thêm node để xử lý và thông báo khi có lỗi xảy ra
4. **Lập lịch trích xuất**: Thêm node để lập lịch trích xuất dữ liệu định kỳ

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quá trình trích xuất dữ liệu từ TikTok và LinkedIn, tiết kiệm thời gian và tăng độ chính xác. Với khả năng xử lý cả tin nhắn văn bản và giọng nói, cùng hệ thống thông báo tự động, đây là công cụ hoàn hảo cho các chuyên viên nghiên cứu thị trường. Hãy thử ngay và nâng cao hiệu quả công việc của bạn!