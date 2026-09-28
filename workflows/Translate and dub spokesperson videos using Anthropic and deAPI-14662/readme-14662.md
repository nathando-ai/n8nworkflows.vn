---
title: "🎤 Tự động hóa dịch & lồng tiếng video người phát ngôn bằng Anthropic và deAPI"
description: "Hướng dẫn tự động hóa dịch và lồng tiếng video người phát ngôn bằng n8n, Anthropic và deAPI - tiết kiệm thời gian 80% cho nội dung đa ngôn ngữ"
slug: "tu-dong-hoa-dich-long-tieng-video-nguoi-phat-ngon"
tags: [n8n, automation, no-code, AI, video, content creation]
keywords: [n8n workflow, tự động hóa nội dung, dịch video, lồng tiếng, AI, deAPI, Anthropic]
---

# 🎤 Tự động hóa dịch & lồng tiếng video người phát ngôn bằng n8n, Anthropic và deAPI

[Các sếp] có bao giờ phải đối mặt với tình trạng phải dịch và lồng tiếng video người phát ngôn cho nhiều ngôn ngữ? Quá trình này thường tốn thời gian, công sức và chi phí đáng kể. Với workflow này, các sếp có thể tự động hóa hoàn toàn quy trình này chỉ trong vài bước đơn giản!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm **80% thời gian** so với làm thủ công
- Tạo nội dung đa ngôn ngữ **chính xác** và **tự nhiên**
- **Tự động hóa hoàn toàn** quy trình dịch và lồng tiếng
- **Tiết kiệm chi phí** nhờ sử dụng AI thay vì dịch viên chuyên nghiệp
- **Tăng tốc độ phát hành** nội dung đa ngôn ngữ lên gấp 10 lần
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản [deAPI](https://deapi.ai) (cho dịch, lồng tiếng và tạo video)
- Tài khoản [Anthropic](https://www.anthropic.com/) (cho dịch thuật AI)
- Video người phát ngôn nguồn (định dạng: MP4, MPEG, MOV, AVI, WMV, OGG)
- Ảnh người phát ngôn địa phương (định dạng: JPG, JPEG, PNG, GIF, BMP, WebP, kích thước tối đa 10MB)
- Instance n8n phải chạy trên **HTTPS**
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n Community Workflows](https://n8n.io/workflows/14662)
2. Click vào nút "Import" ở góc trên bên phải
3. Chọn "Import from URL" và dán link workflow vào
4. Click "OK" để hoàn tất import

Hoặc có thể copy/paste JSON workflow vào n8n Editor bằng cách:
1. Click vào nút "+" ở góc trên bên trái
2. Chọn "Code"
3. Dán nội dung JSON workflow vào và click "OK"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Manual Trigger**: Node này chỉ để kích hoạt workflow thủ công. Không cần cấu hình gì thêm.

2. **Set Fields**:
   - Cấu hình trường `target_language` với ngôn ngữ mục tiêu (ví dụ: Spanish, Japanese, French)

3. **Read Source Video**:
   - Cập nhật đường dẫn file video nguồn trong trường `File Path`
   - Đảm bảo file video có định dạng hợp lệ (MP4, MPEG, MOV, AVI, WMV, OGG)

4. **Read Local Presenter Image**:
   - Cập nhật đường dẫn file ảnh người phát ngôn địa phương trong trường `File Path`
   - Đảm bảo file ảnh có định dạng hợp lệ (JPG, JPEG, PNG, GIF, BMP, WebP) và kích thước không vượt quá 10MB

5. **deAPI Transcribe Video**:
   - Đảm bảo đã tạo và cấu hình credentials cho deAPI
   - Node này sử dụng model Whisper Large V3 để dịch video

6. **AI Agent**:
   - Không cần cấu hình gì thêm, node này sẽ tự động dịch nội dung

7. **Anthropic Chat Model**:
   - Đảm bảo đã tạo và cấu hình credentials cho Anthropic
   - Chọn model "Claude Opus 4.6" trong trường `model`

8. **deAPI Generate Speech**:
   - Đảm bảo đã tạo và cấu hình credentials cho deAPI
   - Node này sử dụng model Qwen3 để tạo giọng nói

9. **Merge Audio + Image**:
   - Không cần cấu hình gì thêm, node này sẽ tự động hợp nhất âm thanh và hình ảnh

10. **deAPI Generate From Audio**:
    - Đảm bảo đã tạo và cấu hình credentials cho deAPI
    - Node này sử dụng model LTX-2.3 22B để tạo video từ âm thanh
    - Prompt mặc định: "A person speaking naturally to the camera, subtle head movements and facial expressions, professional lighting, medium close-up shot, steady camera"

#### 3. Kích hoạt ⚡️
1. Click vào nút "Test Workflow" để chạy thử workflow
2. Kiểm tra kết quả đầu ra để đảm bảo workflow hoạt động đúng
3. Sau khi kiểm tra thành công, click vào nút "Active" để kích hoạt workflow

### ✍️ Mẹo & gợi ý nâng cao
1. **Tùy chỉnh giọng nói**: Thay đổi model trong node "deAPI Generate Speech" để phù hợp với giọng nói mong muốn
2. **Tối ưu video**: Điều chỉnh prompt trong node "deAPI Generate From Audio" để tạo ra video chất lượng cao hơn
3. **Tích hợp Slack/Telegram**: Thêm node gửi thông báo khi workflow hoàn thành
4. **Lưu log**: Thêm node lưu log để theo dõi quá trình xử lý

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quy trình dịch và lồng tiếng video người phát ngôn, tiết kiệm thời gian và chi phí đáng kể. Với chỉ vài bước cấu hình đơn giản, các sếp có thể tạo ra nội dung đa ngôn ngữ chất lượng cao mà không cần phải làm thủ công. Hãy thử ngay và trải nghiệm sự tiện lợi của tự động hóa nội dung với n8n!