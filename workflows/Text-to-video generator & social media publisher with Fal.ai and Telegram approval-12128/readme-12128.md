---
title: "🎥 Tự động tạo video từ văn bản và đăng lên mạng xã hội với Fal.ai và Telegram"
description: "Hướng dẫn tự động hóa tạo video từ văn bản, kiểm duyệt qua Telegram và đăng lên nhiều nền tảng với n8n. Tiết kiệm thời gian và nâng cao hiệu quả nội dung."
slug: "tu-dong-tao-video-tu-van-ban-va-dang-len-mang-xa-hoi"
tags: [n8n, automation, no-code, ai, social-media]
keywords: [n8n workflow, tự động hóa nội dung, tạo video từ văn bản, đăng lên mạng xã hội, Fal.ai]
---

# 🎥 Tự động tạo video từ văn bản và đăng lên mạng xã hội với Fal.ai và Telegram

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian tạo nội dung: Tự động hóa toàn bộ quy trình từ ý tưởng đến xuất bản
- Tăng hiệu quả nội dung: Video chất lượng cao được tạo ra nhanh chóng
- Quản lý hiệu quả: Kiểm duyệt và xuất bản nội dung qua Telegram
- Tối ưu đa nền tảng: Đăng đồng thời lên nhiều mạng xã hội khác nhau
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Telegram và bot token
- API key từ Fal.ai
- Tài khoản Google Sheets
- Tài khoản Blotato (cho đăng lên mạng xã hội)
- API key từ OpenRouter (cho các node LLM)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/12128](https://n8n.io/workflows/12128)
2. Nhấn nút "Download" để tải file JSON workflow
3. Trong n8n Editor, nhấn vào "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node Telegram Message**:
   - Tạo bot Telegram mới và lấy token
   - Thêm bot vào nhóm hoặc kênh Telegram
   - Cấu hình credentials trong n8n

2. **Node Draft Video Prompt**:
   - Đảm bảo đã cấu hình credentials OpenRouterApi
   - Chọn model "z-ai/glm-4.5-air:free" hoặc "openai/gpt-5.2"

3. **Node Generate Video (Fal.ai)**:
   - Đăng ký tài khoản Fal.ai và lấy API key
   - Cấu hình credentials trong n8n
   - Đảm bảo tài khoản có đủ credit để tạo video

4. **Node Log to Google Sheets**:
   - Tạo Google Sheet mới và lấy Sheet ID
   - Cấu hình credentials Google Sheets trong n8n
   - Chọn Sheet ID và tên bảng

5. **Các node Blotato**:
   - Đăng ký tài khoản Blotato và lấy Account ID
   - Cấu hình credentials cho từng mạng xã hội (Instagram, Facebook, LinkedIn, TikTok, YouTube)
   - Đảm bảo tài khoản có quyền đăng bài

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu:
   - Gửi tin nhắn "A calm forest scene" đến bot Telegram
   - Kiểm tra quá trình tạo video và kiểm duyệt
2. Bật Active workflow

### ✍️ Mẹo & gợi ý nâng cao
1. **Tối ưu hóa nội dung**:
   - Thêm node để phân tích hiệu suất bài đăng sau khi xuất bản
   - Tích hợp với các công cụ phân tích như Google Analytics

2. **Quản lý nội dung**:
   - Thêm node để lưu trữ các phiên bản video đã tạo
   - Tích hợp với các công cụ quản lý nội dung như Contentful

3. **Tự động hóa nâng cao**:
   - Thêm node để tự động tạo nội dung từ các nguồn dữ liệu khác
   - Tích hợp với các công cụ CRM như HubSpot

4. **Báo cáo định kỳ**:
   - Thêm node để gửi báo cáo hàng tuần về hiệu suất nội dung
   - Tích hợp với các công cụ báo cáo như Tableau

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quy trình tạo video từ văn bản, kiểm duyệt qua Telegram và đăng lên nhiều nền tảng mạng xã hội. Với việc tích hợp các công cụ AI tiên tiến như Fal.ai và OpenRouter, các sếp có thể tạo ra nội dung chất lượng cao một cách nhanh chóng và hiệu quả. Hãy áp dụng ngay để nâng cao hiệu quả nội dung và tiết kiệm thời gian cho doanh nghiệp!