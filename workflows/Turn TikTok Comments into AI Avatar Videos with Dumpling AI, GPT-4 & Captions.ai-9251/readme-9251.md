---
title: "🎬 Tự động hóa tạo video AI từ bình luận TikTok với Dumpling AI, GPT-4 & Captions.ai"
description: "Hướng dẫn tự động hóa quy trình tạo video AI từ bình luận TikTok bằng n8n, kết hợp Dumpling AI, GPT-4 và Captions.ai để tạo nội dung tự động hóa 100% không cần code"
slug: "tu-dong-hoa-tao-video-ai-tu-binh-luan-tiktok"
tags: [n8n, automation, no-code, content creation, multimodal AI]
keywords: [n8n workflow, tự động hóa nội dung, video AI, TikTok, Dumpling AI, GPT-4, Captions.ai]
---

# 🎬 Tự động hóa tạo video AI từ bình luận TikTok với Dumpling AI, GPT-4 & Captions.ai

[Các sếp] có biết không? Với lượng bình luận khổng lồ trên TikTok mỗi ngày, việc tạo nội dung video từ bình luận thủ công không chỉ tốn thời gian mà còn dễ bỏ sót những bình luận quan trọng. Workflow này sẽ giúp các sếp tự động hóa toàn bộ quy trình từ lấy bình luận, tạo transcript, viết kịch bản cho đến tạo video AI hoàn chỉnh - tất cả chỉ với một lần cài đặt trên n8n.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa toàn bộ quy trình từ 30 phút xuống còn 5 phút mỗi video
- **Nội dung cá nhân hóa**: Tạo video từ bình luận thực tế của người xem, tăng tương tác
- **Chất lượng cao**: Kết hợp AI tiên tiến (GPT-4, Dumpling AI, Captions.ai) tạo ra video chuyên nghiệp
- **Hoạt động liên tục**: Workflow chạy tự động theo lịch, không cần can thiệp thủ công
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n đã cài đặt và cấu hình
- API keys cho các dịch vụ:
  - OpenAI (cho GPT-4)
  - Dumpling AI (cho transcript)
  - Captions.ai (tạo video AI)
  - Submagic (tối ưu video)
  - Airtable (lưu trữ kết quả)
- Dữ liệu mẫu trong DataTable chứa URL video TikTok và bình luận
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/9251)
2. Click "Download" để tải file JSON
3. Trong n8n Editor, click "Import from File" và chọn file JSON vừa tải

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Trigger on Schedule**:
   - Cấu hình lịch chạy phù hợp (ví dụ: mỗi ngày lúc 9h sáng)

2. **Get TikTok Video & Comments from DataTable**:
   - Đảm bảo DataTable đã có dữ liệu mẫu với cấu trúc:
     ```json
     {
       "video_url": "https://www.tiktok.com/@username/video/123456789",
       "top_comment": "This is an amazing video!"
     }
     ```

3. **Get Transcript from Dumpling AI**:
   - Cấu hình credentials cho Dumpling AI
   - Đảm bảo API key có quyền truy cập vào dịch vụ

4. **Generate TikTok Script with GPT-4**:
   - Cấu hình credentials cho OpenAI
   - Tùy chỉnh prompt trong node này nếu cần thay đổi phong cách viết

5. **Clean Up Script Formatting**:
   - Kiểm tra và điều chỉnh đoạn code JavaScript trong node này nếu cần xử lý thêm các trường hợp đặc biệt

6. **Captions: Generate Avatar Video**:
   - Cấu hình credentials cho Captions.ai
   - Chọn avatar và giọng nói phù hợp trong node này

7. **Save Final Video Details to Airtable**:
   - Cấu hình credentials cho Airtable
   - Đảm bảo bảng Airtable đã có các trường: `Video URL`, `Caption Video ID`

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu để kiểm tra toàn bộ workflow
2. Sau khi kiểm tra thành công, bật Active workflow
3. Đảm bảo các dịch vụ API đều hoạt động bình thường

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Slack/Telegram**: Thêm node để thông báo khi video hoàn thành
2. **Lưu log hoạt động**: Thêm node để lưu log các bước xử lý
3. **Gửi báo cáo định kỳ**: Tạo báo cáo tổng hợp các video đã tạo trong tuần
4. **Tối ưu hóa chi phí**: Thêm node để kiểm tra và cảnh báo khi sử dụng quá nhiều credits API

### 📌 Kết luận
Workflow này không chỉ giúp các sếp tiết kiệm thời gian mà còn tạo ra nội dung video chất lượng cao, cá nhân hóa từ bình luận thực tế của người xem. Với việc tự động hóa toàn bộ quy trình, các sếp có thể tập trung vào những nhiệm vụ quan trọng hơn trong việc phát triển nội dung. Hãy thử ngay và biến những bình luận thành những video AI hấp dẫn nhé!