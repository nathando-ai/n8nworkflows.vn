---
title: "🎥 Tự động tóm tắt & dịch video YouTube với n8n, SupaData và OpenAI"
description: "Hướng dẫn chi tiết cách tự động hóa quá trình tóm tắt và dịch nội dung video YouTube bằng công cụ n8n, SupaData và OpenAI - giải pháp tiết kiệm thời gian 100% không cần code"
slug: "tu-dong-tom-tat-dich-video-youtube-n8n-supadata-openai"
tags: [n8n, automation, no-code, youtube, ai]
keywords: [n8n workflow, tự động hóa video, tóm tắt video, dịch video, openai]
---

# 🎥 Tự động tóm tắt & dịch video YouTube với n8n, SupaData và OpenAI

[Các sếp] có bao giờ phải ngồi xem hàng chục video YouTube để lấy thông tin quan trọng? Hay phải dịch từng đoạn văn bản một cách thủ công? Với workflow này, các sếp có thể tự động hóa hoàn toàn quá trình này chỉ trong vài bước đơn giản.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động xử lý hàng chục video trong ngày
- **Chính xác cao**: Sử dụng công nghệ AI của OpenAI
- **Đa ngôn ngữ**: Tóm tắt và dịch sang nhiều ngôn ngữ khác nhau
- **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản OpenAI với API key
- Tài khoản SupaData với API key
- URL video YouTube cần xử lý
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/16122)
2. Click vào nút "Import" ở góc trên bên phải
3. Copy toàn bộ JSON workflow và dán vào n8n Editor của bạn

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "When URL Submitted"**:
   - Cấu hình form để nhận URL video YouTube
   - Đảm bảo form có trường nhập liệu cho URL

2. **Node "Extract Transcript"**:
   - Thêm credentials "supadataApi"
   - Đảm bảo operation được đặt là "getTranscript"

3. **Node "Fetch Video Details"**:
   - Thêm credentials "supadataApi"
   - Đảm bảo operation được đặt là "getVideoDetails"

4. **Node "AI Summarization and Translation"**:
   - Thêm credentials "openAiApi"
   - Điều chỉnh prompt theo nhu cầu dịch và tóm tắt
   - Ví dụ prompt:
     ```
     Summarize the following video content in [language] and provide a translation to [target language]:
     Video title: {{videoTitle}}
     Video description: {{videoDescription}}
     Transcript: {{transcript}}
     ```

#### 3. Kích hoạt ⚡️
1. Test run với URL video mẫu
2. Kiểm tra kết quả tóm tắt và dịch
3. Bật Active workflow sau khi xác nhận hoạt động ổn định

### ✍️ Mẹo & gợi ý nâng cao
1. **Lưu trữ kết quả**: Kết nối với Google Drive hoặc Dropbox để lưu trữ các file kết quả
2. **Thông báo kết quả**: Thêm node gửi email hoặc Slack khi quá trình hoàn thành
3. **Xử lý hàng loạt**: Sử dụng node "Loop Over Items" để xử lý nhiều video cùng lúc
4. **Tùy chỉnh ngôn ngữ**: Điều chỉnh prompt trong node OpenAI để hỗ trợ nhiều ngôn ngữ khác nhau

### 📌 Kết luận
Workflow này mang lại giải pháp toàn diện cho việc tự động hóa tóm tắt và dịch video YouTube. Với công nghệ AI tiên tiến và giao diện đơn giản, các sếp có thể tiết kiệm hàng giờ làm việc mỗi ngày. Hãy thử ngay và trải nghiệm sự tiện lợi mà công nghệ mang lại!