---
title: "🚀 Tự động hóa nội dung: Chuyển đổi bài viết thành nội dung mạng xã hội với Gemini, Olostep và Google Docs"
description: "Hướng dẫn chi tiết cách tự động hóa việc chuyển đổi bài viết thành nội dung mạng xã hội chuyên nghiệp trên LinkedIn, Twitter, Reddit và FAQ với n8n"
slug: "tu-dong-hoa-noi-dung-bai-viet-thanh-noi-dung-mang-xa-hoi"
tags: [n8n, automation, no-code, content-marketing, social-media]
keywords: [n8n workflow, tự động hóa nội dung, content marketing, social media, Google Gemini]
---

# 🚀 Tự động hóa nội dung: Chuyển đổi bài viết thành nội dung mạng xã hội với Gemini, Olostep và Google Docs

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp thường phải tốn nhiều thời gian để chuyển đổi nội dung dài thành các bài đăng ngắn trên các mạng xã hội khác nhau. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình này chỉ trong vài phút, tiết kiệm thời gian quý giá và đảm bảo nội dung luôn được tối ưu cho từng nền tảng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa toàn bộ quy trình từ 30 phút xuống còn 5 phút
- Tối ưu nội dung: Nội dung được tối ưu riêng biệt cho từng nền tảng
- Tăng tương tác: Nội dung được thiết kế theo các nguyên tắc tăng tương tác trên từng nền tảng
- Tự động hóa hoàn toàn: Không cần can thiệp thủ công sau khi thiết lập
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Gemini (PaLM) API Key
- Tài khoản Olostep API Key
- Tài khoản Google Drive (OAuth2)
- Email để nhận kết quả cuối cùng
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấn vào "Import from URL" và dán link sau: [https://n8n.io/workflows/15458](https://n8n.io/workflows/15458)
3. Hoặc tải file JSON về và import từ máy tính

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "On form submission"**:
   - Kích hoạt workflow bằng cách nhấn "Activate"
   - Lưu ý URL form sẽ được tạo ra sau khi kích hoạt

2. **Node "Core Extractor" đến "FAQ"**:
   - Tất cả các node này đều sử dụng Google Gemini
   - Đảm bảo bạn đã thiết lập credentials cho "googlePalmApi"
   - Có thể điều chỉnh prompt trong mỗi node để phù hợp với phong cách nội dung của bạn

3. **Node "Scrape Article"**:
   - Thiết lập credentials cho "olostepScrapeApi"
   - Đảm bảo tài khoản Olostep có đủ credit để sử dụng

4. **Node "Transfer HTML to Doc" đến "Upload html file"**:
   - Tất cả các node này đều sử dụng Google Drive
   - Thiết lập credentials cho "googleDriveOAuth2Api"
   - Đảm bảo tài khoản Google Drive có đủ dung lượng lưu trữ

5. **Node "Share link & email"**:
   - Chỉnh sửa địa chỉ email nhận kết quả cuối cùng
   - Có thể thêm nhiều địa chỉ email bằng cách sử dụng dấu phẩy

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu bằng cách submit một URL bài viết bất kỳ
2. Kiểm tra kết quả trên Google Drive và email của bạn
3. Sau khi xác nhận hoạt động ổn định, bật Active workflow

### ✍️ Mẹo & gợi ý nâng cao
1. **Tùy chỉnh phong cách nội dung**: Chỉnh sửa prompt trong các node Gemini để phù hợp với phong cách nội dung của bạn
2. **Thêm nền tảng mới**: Sao chép một node Gemini hiện có và điều chỉnh prompt để tạo nội dung cho nền tảng mới
3. **Tích hợp với Slack/Discord**: Thay thế node Google Drive bằng node Slack hoặc Discord để nhận kết quả trực tiếp trên các kênh chat
4. **Lưu trữ lịch sử**: Thêm node để lưu trữ các phiên bản nội dung đã tạo trong Google Drive hoặc Notion

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian quý giá trong việc tạo nội dung mạng xã hội chuyên nghiệp. Với khả năng tự động hóa hoàn toàn và tối ưu nội dung cho từng nền tảng, các sếp có thể tập trung vào những nhiệm vụ quan trọng hơn trong công việc hàng ngày. Hãy thử ngay và trải nghiệm cách làm việc thông minh hơn với n8n!