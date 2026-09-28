---
title: "🎥 Tự động hóa Transcript & Tóm tắt Video YouTube sang Telegram với GPT-4o"
description: "Hướng dẫn chi tiết cách tự động hóa quá trình chuyển đổi video YouTube thành transcript và tóm tắt bằng AI, sau đó gửi kết quả lên Telegram - hoàn toàn không cần code."
slug: "tu-dong-hoa-transcript-tom-tat-video-youtube-sang-telegram-voi-gpt-4o"
tags: [n8n, automation, no-code, AI, marketing]
keywords: [n8n workflow, tự động hóa, transcript video, tóm tắt nội dung, Telegram, GPT-4o]
---

# 🎥 Tự động hóa Transcript & Tóm tắt Video YouTube sang Telegram với GPT-4o

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian xử lý transcript và tóm tắt video YouTube
- Tự động hóa toàn bộ quy trình từ nhập URL đến gửi kết quả
- Sử dụng công nghệ AI tiên tiến (GPT-4o) để phân tích và tóm tắt nội dung
- Nhận kết quả tóm tắt dưới dạng bullet points dễ đọc
- Hoạt động liên tục 24/7 mà không cần can thiệp thủ công
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Telegram và bot Telegram
- API Key từ Supadata (để transcribe video)
- API Key từ OpenAI (để sử dụng GPT-4o)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấn vào "Import from URL" và nhập link: [https://n8n.io/workflows/4964](https://n8n.io/workflows/4964)
3. Hoặc copy/paste JSON từ file workflow vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Input URL" (telegramTrigger)**:
   - Cấu hình credentials cho Telegram API
   - Đảm bảo bot Telegram của bạn đã được kích hoạt và có quyền truy cập vào kênh/group cần sử dụng

2. **Node "Make Transcribe" (supadata)**:
   - Cấu hình credentials cho Supadata API
   - Đảm bảo bạn đã đăng ký và có API Key từ Supadata
   - Có thể cần điều chỉnh tham số "operation" nếu cần

3. **Node "OpenAI" (lmChatOpenAi)**:
   - Cấu hình credentials cho OpenAI API
   - Đảm bảo bạn đã đăng ký và có API Key từ OpenAI
   - Chọn model "gpt-4o-mini" trong danh sách model

4. **Node "Send Summary" (telegram)**:
   - Cấu hình credentials cho Telegram API
   - Đảm bảo bot Telegram của bạn đã được cấu hình đúng để gửi tin nhắn

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu bằng cách gửi URL video YouTube đến bot Telegram của bạn
2. Kiểm tra kết quả transcript và tóm tắt được gửi về Telegram
3. Bật Active workflow để chạy liên tục

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node để lưu log các video đã xử lý
- Kết hợp với Slack để nhận thông báo khi có video mới được xử lý
- Tạo báo cáo định kỳ về các video đã xử lý và tóm tắt nội dung
- Sử dụng workflow này để tự động hóa việc tạo nội dung từ video cho các kênh truyền thông xã hội

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện để tự động hóa quá trình chuyển đổi video YouTube thành transcript và tóm tắt nội dung bằng AI. Với việc tích hợp Telegram, bạn có thể dễ dàng nhận kết quả và chia sẻ với đội ngũ của mình. Hãy thử ngay và tiết kiệm thời gian cho các công việc quan trọng hơn!