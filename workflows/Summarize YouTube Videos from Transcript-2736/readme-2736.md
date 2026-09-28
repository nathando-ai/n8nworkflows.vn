---
title: "🎬 Tự động tóm tắt video YouTube bằng AI - Workflow n8n"
description: "Giải pháp tự động hóa hoàn toàn không cần code giúp tóm tắt nội dung video YouTube dài thành bản tóm tắt ngắn gọn, chính xác bằng công nghệ AI LangChain và OpenAI"
slug: "tu-dong-tom-tat-video-youtube-bang-ai"
tags: [n8n, automation, no-code, youtube, ai]
keywords: [n8n workflow, tự động hóa, tóm tắt video, youtube, openai]
---

# 🎬 Tự động tóm tắt video YouTube bằng AI - Workflow n8n

[Các sếp] có bao giờ phải ngồi xem video YouTube dài hàng giờ để tìm thông tin quan trọng? Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình tóm tắt video chỉ trong vài phút, tiết kiệm hàng giờ công sức mỗi ngày.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động xử lý hàng chục video mỗi ngày mà không cần can thiệp
- **Nội dung chính xác**: Sử dụng công nghệ AI LangChain và OpenAI để phân tích và tóm tắt nội dung
- **Tùy chỉnh dễ dàng**: Có thể thay đổi độ dài tóm tắt và phong cách viết theo nhu cầu
- **Tích hợp linh hoạt**: Kết nối với nhiều hệ thống khác như Slack, Email, Google Sheets...
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản OpenAI với API key (để sử dụng mô hình ngôn ngữ)
- URL video YouTube cần tóm tắt
- (Tùy chọn) Tài khoản Slack/Email để nhận kết quả tóm tắt
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập trang [workflow gốc trên n8n.io](https://n8n.io/workflows/2736)
2. Click vào nút "Download" để tải file JSON
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "YouTube video URL" (formTrigger)**:
   - Thay đổi input từ form thành webhook nếu muốn tích hợp với hệ thống khác
   - Hoặc giữ nguyên để nhập URL trực tiếp trong n8n Editor

2. **Node "Summarization Engine" (lmChatOpenAi)**:
   - Cấu hình credentials OpenAI API
   - Tùy chỉnh các tham số như:
     - Model: Chọn mô hình OpenAI phù hợp (gpt-3.5-turbo, gpt-4...)
     - Temperature: Điều chỉnh độ sáng tạo của tóm tắt (0.7 là giá trị mặc định)
     - Max Tokens: Giới hạn độ dài của tóm tắt

3. **Node "Summarization of a YouTube script" (chainSummarization)**:
   - Tùy chỉnh prompt để điều chỉnh phong cách tóm tắt
   - Có thể thêm các yêu cầu cụ thể như: "Tóm tắt theo 3 điểm chính", "Sử dụng ngôn ngữ chuyên nghiệp..."

#### 3. Kích hoạt ⚡️
1. Test run với URL video mẫu
2. Kiểm tra kết quả tóm tắt trong node cuối cùng
3. Bật Active workflow để sử dụng trong thực tế

### ✍️ Mẹo & gợi ý nâng cao
1. **Tích hợp với Slack/Email**:
   - Thêm node gửi email hoặc thông báo Slack ngay sau node tóm tắt
   - Tự động gửi tóm tắt đến nhóm làm việc

2. **Lưu trữ kết quả**:
   - Kết nối với Google Sheets để lưu trữ lịch sử tóm tắt
   - Hoặc lưu vào cơ sở dữ liệu để phân tích sau này

3. **Tự động hóa định kỳ**:
   - Thêm node Schedule Trigger để tự động tóm tắt video mới mỗi ngày
   - Hoặc kết nối với RSS feed của kênh YouTube để theo dõi video mới

4. **Phân tích cảm xúc**:
   - Thêm node phân tích cảm xúc từ nội dung tóm tắt
   - Giúp đánh giá xu hướng của video

### 📌 Kết luận
Workflow này không chỉ giúp các sếp tiết kiệm thời gian mà còn nâng cao hiệu quả làm việc bằng cách cung cấp thông tin quan trọng một cách nhanh chóng và chính xác. Hãy thử ngay và biến những giờ ngồi xem video dài thành những phút làm việc hiệu quả hơn!