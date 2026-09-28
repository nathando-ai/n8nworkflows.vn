---
title: "🚀 Tự động hóa tạo video quảng cáo từ ảnh sản phẩm với Gemini AI, Kling & LATE"
description: "Hướng dẫn chi tiết cách tự động hóa quy trình tạo video quảng cáo từ ảnh sản phẩm bằng công nghệ AI Gemini, Kling và LATE. Tiết kiệm thời gian và nâng cao hiệu quả marketing."
slug: "tu-dong-hoa-tao-video-quang-cao-tu-anh-san-pham-voi-gemini-kling-late"
tags: [n8n, automation, no-code, content creation, social media, ai, multimodal ai]
keywords: [n8n workflow, tự động hóa, tạo video, ảnh sản phẩm, Gemini AI, Kling, LATE, marketing]
---

# 🚀 Tự động hóa tạo video quảng cáo từ ảnh sản phẩm với Gemini AI, Kling & LATE

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian tạo video từ 80% đến 90%
- Tạo ra nội dung chuyên nghiệp với hiệu ứng chuyển động và âm thanh tự động
- Tăng tương tác trên các nền tảng mạng xã hội
- Tự động đăng lên nhiều nền tảng (Instagram, TikTok, YouTube Shorts)
- Duy trì tính nhất quán trong thương hiệu
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Telegram để tương tác với workflow
- API Key từ Google Gemini
- API Key từ ImgBB
- API Key từ LATE (cho việc đăng lên mạng xã hội)
- Tài khoản trên các nền tảng mạng xã hội (Instagram, TikTok, YouTube)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/8318](https://n8n.io/workflows/8318)
2. Click vào nút "Download Workflow"
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON đã tải về
4. Hoặc copy toàn bộ JSON và paste vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Telegram Trigger**:
   - Tạo bot Telegram mới qua @BotFather
   - Lấy token và thêm vào credentials trong n8n
   - Cấu hình chat ID để nhận thông báo

2. **Google Gemini API**:
   - Tạo tài khoản Google Cloud
   - Bật API Google Gemini
   - Tạo API key và thêm vào credentials trong n8n

3. **ImgBB API**:
   - Đăng ký tài khoản tại [imgbb.com](https://imgbb.com/)
   - Lấy API key từ trang tài khoản
   - Thay thế "PASTE_YOUR_IMGBB_API_KEY_HERE" trong node "Set: YOUR API KEY (ImgBB)"

4. **LATE API**:
   - Đăng ký tài khoản tại [late.dev](https://getlate.dev)
   - Lấy API key từ dashboard
   - Thêm vào credentials trong n8n

5. **Kling API**:
   - Đăng ký tài khoản tại [fal.ai](https://fal.ai)
   - Lấy API key từ trang tài khoản
   - Thêm vào credentials trong n8n

6. **Cấu hình các node chính**:
   - **Ask Approval (Images)**: Cấu hình chat ID và thông báo yêu cầu phê duyệt
   - **Creative Director (Orchestrator) agent**: Cấu hình prompt và tham số cho AI
   - **Gen Image A/B**: Cấu hình tham số tạo ảnh từ Gemini
   - **kling Queue A/B**: Cấu hình tham số tạo video từ Kling
   - **Share to Instagram/TikTok/YouTube**: Cấu hình tài khoản và thông tin đăng

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu:
   - Gửi một ảnh sản phẩm qua Telegram bot
   - Kiểm tra từng bước xử lý trong workflow
2. Bật Active workflow sau khi đã kiểm tra và cấu hình đầy đủ

### ✍️ Mẹo & gợi ý nâng cao
1. **Tùy chỉnh nội dung**:
   - Chỉnh sửa prompt trong node "Creative Director" để phù hợp với thương hiệu
   - Thay đổi tham số tạo ảnh trong node "Gen Image A/B"
   - Điều chỉnh hiệu ứng chuyển động trong node "kling Queue A/B"

2. **Tối ưu hiệu suất**:
   - Sử dụng các node "Wait" để quản lý thời gian xử lý
   - Thêm node "Aggregate" để gom nhóm kết quả
   - Sử dụng node "Merge" để kết hợp dữ liệu từ nhiều nguồn

3. **Mở rộng chức năng**:
   - Thêm node "Telegram" để nhận phản hồi từ người dùng
   - Kết nối với các nền tảng khác như Facebook, Twitter
   - Thêm node "Email" để gửi báo cáo sau khi hoàn thành

4. **Quản lý tài nguyên**:
   - Theo dõi sử dụng API trong các node "httpRequest"
   - Thiết lập giới hạn xử lý trong node "Aggregate"
   - Sử dụng node "StickyNote" để ghi chú các bước quan trọng

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc tự động hóa tạo video quảng cáo từ ảnh sản phẩm. Với sự kết hợp của công nghệ AI Gemini, Kling và LATE, các sếp có thể tạo ra nội dung chuyên nghiệp một cách nhanh chóng và hiệu quả. Hãy thử nghiệm và tùy chỉnh workflow này để phù hợp với nhu cầu cụ thể của doanh nghiệp.