```yaml
---
title: "🎬 Tự động hóa tạo video từ văn bản với GPT-4 và FLUX.1 Pro"
description: "Hướng dẫn chi tiết cách tự động chuyển đổi ý tưởng văn bản thành video chất lượng cao sử dụng n8n, GPT-4, FLUX.1 Pro và Veo 3"
slug: "tu-dong-hoa-tao-video-tu-van-ban-gpt4-flux1pro"
tags: [n8n, automation, no-code, ai, video-generation]
keywords: [n8n workflow, tự động hóa video, AI tạo video, FLUX.1 Pro, Veo 3]
---

# 🎬 Tự động hóa tạo video từ văn bản với GPT-4 và FLUX.1 Pro

[Các sếp] có bao giờ muốn chuyển đổi ý tưởng văn bản thành video chất lượng cao mà không cần phải làm thủ công từng bước? Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình từ ý tưởng ban đầu đến video hoàn thiện chỉ trong vài giây!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian đáng kể trong quá trình tạo nội dung video
- Tự động hóa toàn bộ quy trình từ ý tưởng đến video hoàn thiện
- Tạo video chất lượng chuyên nghiệp với chỉ 1 ý tưởng văn bản
- Hệ thống ghi log chi tiết giúp quản lý và theo dõi quá trình tạo video
- Tích hợp dễ dàng với các công cụ khác trong hệ sinh thái n8n
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản OpenAI API (cho GPT-4.1 và GPT-4o)
- Tài khoản Dumpling AI (cho FLUX.1 Pro)
- Tài khoản Veo 3
- Tài khoản Google Sheets (để lưu log)
- Kiến thức cơ bản về n8n và cách cấu hình credentials
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấn vào "Import from URL" và dán link: https://n8n.io/workflows/8564
3. Hoặc tải file JSON về và chọn "Import from File"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Capture Image Idea" (formTrigger)**:
   - Cấu hình form để người dùng nhập ý tưởng văn bản
   - Đảm bảo form có trường "imageIdea" để lưu ý tưởng

2. **Node "Generate Image Prompt (GPT-4.1)" (openAi)**:
   - Cấu hình credentials OpenAI API
   - Đảm bảo model được chọn là GPT-4.1
   - Prompt mẫu có thể sử dụng:
     ```
     Expand this text idea into a vivid, cinematic prompt:
     {{ $node["Capture Image Idea"].json["imageIdea"] }}

     Include visual details such as setting, lighting, mood, and characters.
     ```

3. **Node "Generate Image (FLUX.1 Pro) with Dumpling AI" (httpRequest)**:
   - Cấu hình credentials cho Dumpling AI
   - Đảm bảo endpoint API đúng với FLUX.1 Pro
   - Tham số cần thiết:
     ```
     {
       "prompt": "{{ $node["Generate Image Prompt (GPT-4.1)"].json["text"] }}",
       "width": 1920,
       "height": 1080,
       "steps": 25,
       "cfg_scale": 7,
       "sampler": "euler_a"
     }
     ```

4. **Node "Generate Video Prompt (GPT-4o)" (openAi)**:
   - Cấu hình credentials OpenAI API
   - Đảm bảo model được chọn là GPT-4o
   - Prompt mẫu có thể sử dụng:
     ```
     Analyze this image and write a matching scene script for Veo 3:
     [Image URL: {{ $node["Generate Image (FLUX.1 Pro) with Dumpling AI"].json["image_url"] }}]

     Format the script as:
     - 1 action
     - 1 short line of dialogue
     - style notes
     ```

5. **Node "Upload Image to KIE API for Veo 3" (httpRequest)**:
   - Cấu hình credentials cho Veo 3
   - Đảm bảo endpoint API đúng với Veo 3
   - Tham số cần thiết:
     ```
     {
       "image_url": "{{ $node["Generate Image (FLUX.1 Pro) with Dumpling AI"].json["image_url"] }}"
     }
     ```

6. **Node "Log to Google Sheet" (googleSheets)**:
   - Cấu hình credentials Google Sheets
   - Đảm bảo spreadsheet ID và tên sheet đúng
   - Cấu hình các cột dữ liệu cần lưu:
     ```
     [
       { "property": "imageIdea", "value": "{{ $node["Capture Image Idea"].json["imageIdea"] }}" },
       { "property": "imagePrompt", "value": "{{ $node["Generate Image Prompt (GPT-4.1)"].json["text"] }}" },
       { "property": "videoPrompt", "value": "{{ $node["Generate Video Prompt (GPT-4o)"].json["text"] }}" },
       { "property": "videoUrl", "value": "{{ $node["Check Video Status (Veo 3)"].json["video_url"] }}" }
     ]
     ```

#### 3. Kích hoạt ⚡️
1. Test run workflow với dữ liệu mẫu
2. Kiểm tra từng node để đảm bảo dữ liệu được truyền đúng
3. Bật Active workflow sau khi đã kiểm tra kỹ

### ✍️ Mẹo & gợi ý nâng cao
1. **Tích hợp Slack/Telegram**: Thêm node gửi thông báo khi video hoàn thành
2. **Tự động hóa thêm**: Kết nối với các công cụ khác như Canva, Adobe Premiere
3. **Quản lý nội dung**: Tạo workflow con để xử lý các video không đạt tiêu chuẩn
4. **Tối ưu hóa**: Thêm node để tự động chọn các tham số tốt nhất cho FLUX.1 Pro

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quá trình tạo video từ ý tưởng văn bản, từ việc mở rộng ý tưởng đến tạo video hoàn thiện và lưu log. Với các bước cấu hình đơn giản, các sếp có thể bắt đầu tạo video chất lượng chuyên nghiệp chỉ trong vài phút! Hãy thử ngay và tiết kiệm thời gian quý giá của mình!```