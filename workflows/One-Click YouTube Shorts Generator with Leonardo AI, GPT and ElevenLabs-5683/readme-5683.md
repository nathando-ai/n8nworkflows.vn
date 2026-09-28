---
title: "🚀 Tạo Video YouTube Shorts Một Click với Leonardo AI, GPT & ElevenLabs"
description: "Giải pháp tự động hóa 100% tạo video Shorts từ prompt văn bản, bao gồm nội dung, hình ảnh, âm thanh và biên tập, giúp các sếp tiết kiệm thời gian và tăng chất lượng nội dung."
slug: "tac-dong-youtube-shorts-mot-click"
tags: [n8n, automation, no-code, youtube, ai, video, content-creation]
keywords: [n8n workflow, tự động hóa, youtube shorts, ai video, leonardo ai, elevenlabs, openai]
---

# 🚀 Tạo Video YouTube Shorts Một Click với Leonardo AI, GPT & ElevenLabs

Bạn đang gặp khó khăn khi phải viết kịch bản, tạo hình ảnh, chuyển đổi văn bản thành giọng nói và biên tập video thủ công? Workflow này sẽ giúp bạn **tự động hóa toàn bộ quy trình** chỉ với một lần nhấn nút, từ ý tưởng đến video hoàn chỉnh, hoàn toàn không cần code.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ vài giờ lên tới vài phút.
- **Chính xác**: Nội dung, hình ảnh và âm thanh được đồng bộ hoàn hảo.
- **Cá nhân hóa**: Thay đổi prompt, voice ID, hoặc style chỉ bằng một vài dòng cấu hình.
- **Hoạt động liên tục**: Workflow có thể chạy bất cứ lúc nào, 24/7.
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
- **OpenAI API key** – dùng cho node `Ideator` và `image-prompter`.
- **ElevenLabs API key** – dùng cho node `Script Generator` (text‑to‑speech).
- **Leonardo AI API key** – dùng cho node `request image` (tạo hình ảnh).
- **Creatomate API key** – dùng cho node `Create editor JSON` và `Editor`.
- **Cloudinary credentials** – dùng cho node `Upload Cloudinary`.
- **Environment variable** `CLOUDINARY_CLOUD_NAME` – tên cloud của bạn trên Cloudinary.
- **HTTP Header Auth** – dùng cho các node `httpRequest` cần header `Authorization: Bearer <token>`.
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
1. Tải file JSON của workflow từ [link gốc](https://n8n.io/workflows/5683) hoặc copy toàn bộ JSON.
2. Mở n8n Editor → **Import** → **Import from JSON** → dán JSON hoặc upload file.
3. Nhấn **Import** và workflow sẽ xuất hiện trong danh sách.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Tên node | Mô tả | Cấu hình cần chỉnh |
|------|----------|-------|---------------------|
| `When clicking ‘Execute workflow’` | `manualTrigger` | Bắt đầu workflow | Không cần chỉnh |
| `Ideator 🧠` | `openAi` | Tạo kịch bản, tiêu đề, mô tả | Chọn **OpenAI API** credentials |
| `Script` | `set` | Định dạng dữ liệu đầu ra | Đặt biến `script` từ node `Ideator` |
| `Script Generator` | `httpRequest` | Gửi script tới ElevenLabs | Chọn **httpHeaderAuth** credentials, đặt URL `https://api.elevenlabs.io/v1/text-to-speech/...` |
| `image-prompter` | `openAi` | Tạo prompt hình ảnh | Chọn **OpenAI API** credentials |
| `request image` | `httpRequest` | Gửi prompt tới Leonardo AI | Chọn **httpHeaderAuth** credentials, URL `https://api.leonardo.ai/v1/generate` |
| `Upload Cloudinary` | `httpRequest` | Upload hình ảnh lên Cloudinary | Đặt `CLOUDINARY_CLOUD_NAME` và API credentials |
| `Aggregate` | `aggregate` | Gộp dữ liệu hình ảnh | Định dạng `{{ $json["imageUrl"] }}` |
| `Merge` | `merge` | Kết hợp dữ liệu video | Định dạng `{{ $json["videoUrl"] }}` |
| `Create editor JSON` | `httpRequest` | Tạo JSON cấu trúc video | Chọn **httpHeaderAuth** credentials |
| `SET JSON VARIABLE` | `set` | Đặt biến JSON | Đặt `editorJson` |
| `Editor` | `httpRequest` | Gửi JSON tới Creatomate | Chọn **httpHeaderAuth** credentials |
| `Rendering wait` | `wait` | Đợi Creatomate render | Đặt thời gian (ví dụ 30s) |
| `Get final video` | `httpRequest` | Lấy video cuối | Chọn **httpHeaderAuth** credentials |
| `request image1` / `request image2` | `httpRequest` | Tạo thêm hình ảnh phụ | Chọn **httpHeaderAuth** credentials |
| `Request Video` | `httpRequest` | Tạo video từ hình ảnh | Chọn **httpHeaderAuth** credentials |
| `Edit Fields` | `set` | Sửa thông tin video | Đặt tiêu đề, mô tả |
| `Wait1` / `Wait2` / `Wait3` / `Wait4` | `wait` | Đợi các bước xử lý | Đặt thời gian phù hợp (tùy workflow) |
| `Merge` (lần cuối) | `merge` | Kết hợp toàn bộ video | Định dạng `{{ $json["finalVideoUrl"] }}` |

> **Lưu ý**: Mỗi node `httpRequest` cần có **URL** và **Body** chính xác. Bạn có thể tham khảo tài liệu API của ElevenLabs, Leonardo AI, Creatomate và Cloudinary để điền đúng tham số.

### 3. Kích hoạt ⚡️
1. **Test run**: Nhấn nút **Execute** trong n8n Editor, nhập prompt ví dụ “Tôi muốn một video về cách trồng rau trong nhà”.
2. Kiểm tra log từng node, đảm bảo không có lỗi.
3. Khi mọi thứ ổn, bật **Active** cho workflow.
4. Mỗi lần nhấn **Execute workflow** sẽ tạo một video Shorts mới.

## ✍️ Mẹo & gợi ý nâng cao
- **Thêm Slack/Telegram**: Dùng node `slack` hoặc `telegram` để gửi link video ngay khi hoàn thành.
- **Lưu log**: Dùng node `writeBinaryFile` để lưu video vào thư mục local hoặc S3.
- **Báo cáo định kỳ**: Kết hợp với `cron` node để tự động tạo video hàng ngày về một chủ đề cụ thể.
- **Tùy chỉnh voice**: Thay đổi `voice_id` trong node `Script Generator` để chọn giọng nói khác nhau.
- **Tối ưu độ dài**: Sử dụng node `splitOut` để chia script thành các đoạn ngắn hơn, giúp video ngắn gọn và thu hút.

## 📌 Kết luận
Workflow “One-Click YouTube Shorts Generator” là công cụ mạnh mẽ giúp các sếp **tự động hóa toàn bộ quy trình tạo nội dung video** – từ ý tưởng, kịch bản, hình ảnh, âm thanh đến biên tập và xuất bản. Bạn chỉ cần một prompt ngắn gọn, workflow sẽ làm hết công việc nặng nề, giúp bạn tập trung vào chiến lược nội dung và phát triển kênh. Hãy thử ngay và trải nghiệm sự tiện lợi, tiết kiệm thời gian và chi phí!

---