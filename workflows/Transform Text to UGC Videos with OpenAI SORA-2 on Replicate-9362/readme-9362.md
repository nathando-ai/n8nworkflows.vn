---
title: "🎬 Tự động hóa tạo video từ văn bản với OpenAI SORA-2 trên n8n"
description: "Hướng dẫn chi tiết cách tự động hóa tạo video từ văn bản sử dụng công nghệ AI tiên tiến của OpenAI SORA-2 trên nền tảng n8n. Giải phóng thời gian sáng tạo nội dung và nâng cao hiệu quả marketing."
slug: "tu-dong-hoa-tao-video-tu-van-ban-openai-sora-2-n8n"
tags: [n8n, automation, no-code, openai, video-generation]
keywords: [n8n workflow, tự động hóa nội dung, tạo video từ văn bản, openai sora-2, marketing tự động]
---

# 🎬 Tự động hóa tạo video từ văn bản với OpenAI SORA-2 trên n8n

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian sáng tạo nội dung lên đến 80%
- Tạo hàng loạt video từ cùng một hình ảnh với các prompt khác nhau
- Tự động hóa quy trình phê duyệt và xuất bản video
- Tiết kiệm chi phí sản xuất video truyền thống
- Tăng tốc độ thử nghiệm và lựa chọn nội dung hiệu quả nhất
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Replicate với API key
- Tài khoản OpenAI với API key
- Hình ảnh seed có kích thước 1280x720
- Nền tảng lưu trữ video (Google Drive, AWS S3, v.v.)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấn vào nút "Import from URL" và dán link: https://n8n.io/workflows/9362
3. Hoặc tải file JSON về và chọn "Import from file"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Manual Trigger** (n8n-nodes-base.manualTrigger):
   - Đây là điểm bắt đầu của workflow
   - Không cần cấu hình gì thêm

2. **Set API Token** (n8n-nodes-base.set):
   - Thêm hai biến môi trường:
     - `REPLICATE_API_TOKEN`: API key từ Replicate
     - `OPENAI_API_KEY`: API key từ OpenAI

3. **Add Seed Image, Prompt and amount of seconds** (n8n-nodes-base.set):
   - Thêm các biến:
     - `seed_image_url`: URL của hình ảnh seed (1280x720)
     - `prompt`: Mô tả chi tiết về cảnh và chuyển động (không chứa ký tự đặc biệt)
     - `seconds`: Thời lượng video (4, 8 hoặc 12)

4. **Create Video** (n8n-nodes-base.httpRequest):
   - Đảm bảo endpoint là: `https://api.replicate.com/v1/models/openai/sora-2/predictions`
   - Method: POST
   - Body:
     ```json
     {
       "input": {
         "prompt": "{{$node["Add Seed Image, Prompt and amount of seconds"].json["prompt"]}}",
         "aspect_ratio": "landscape",
         "seconds": {{$node["Add Seed Image, Prompt and amount of seconds"].json["seconds"]}},
         "seed_image": "{{$node["Add Seed Image, Prompt and amount of seconds"].json["seed_image_url"]}}"
       }
     }
     ```

5. **Check Status** (n8n-nodes-base.httpRequest):
   - Method: GET
   - URL: `https://api.replicate.com/v1/predictions/{{$node["Create Video"].json["id"]}}`

6. **Loop Over Items** (n8n-nodes-base.splitInBatches):
   - Kích hoạt để xử lý hàng loạt video
   - Thiết lập batch size theo nhu cầu

#### 3. Kích hoạt ⚡️
1. Kiểm tra kết nối với các API (Replicate và OpenAI)
2. Chạy thử với dữ liệu mẫu
3. Kích hoạt workflow bằng cách nhấn nút "Activate"

### ✍️ Mẹo & gợi ý nâng cao
1. **Tối ưu hóa prompt**:
   - Sử dụng các từ khóa cụ thể về chuyển động và góc quay
   - Ví dụ: "A close-up shot of a product moving from left to right with smooth camera movement"

2. **Xử lý hàng loạt**:
   - Kết nối node "Batch Process Videos" sau "Set API Token" để tạo nhiều video cùng lúc
   - Có thể sử dụng cùng hình ảnh với các prompt khác nhau hoặc nhiều hình ảnh với các prompt khác nhau

3. **Lưu trữ và xuất bản**:
   - Kết nối với các dịch vụ lưu trữ như Google Drive, AWS S3 để tự động lưu video đã tạo
   - Tích hợp với các nền tảng xuất bản như YouTube, TikTok để tự động xuất bản nội dung

4. **Theo dõi và báo cáo**:
   - Thêm node để ghi log các video đã tạo
   - Tạo báo cáo tự động về hiệu suất và chi phí của các video đã tạo

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc tự động hóa tạo video từ văn bản sử dụng công nghệ AI tiên tiến của OpenAI SORA-2. Với khả năng tạo hàng loạt video từ cùng một hình ảnh với các prompt khác nhau, các sếp có thể tiết kiệm thời gian và tài nguyên đáng kể trong quá trình sáng tạo nội dung. Hãy áp dụng ngay để nâng cao hiệu quả marketing và truyền thông của doanh nghiệp!