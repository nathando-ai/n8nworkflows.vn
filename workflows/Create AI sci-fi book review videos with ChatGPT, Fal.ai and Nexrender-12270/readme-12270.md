---
title: "🚀 Tạo video đánh giá sách khoa học viễn tưởng bằng AI với ChatGPT, Fal.ai và Nexrender"
description: "Tự động tạo video đánh giá sách sci‑fi 100% bằng AI, giảm công sức thủ công và nâng cao chất lượng nội dung."
slug: "tao-video-danh-gia-sach-khoa-hoc-vien-tuong-bai-voi-ai"
tags: [n8n, automation, no-code, AI, video, book-review]
keywords: [n8n workflow, tự động hóa, video AI, book review, sci‑fi, Fal.ai, Nexrender, ChatGPT]
---

# 🚀 Tạo video đánh giá sách khoa học viễn tưởng bằng AI với ChatGPT, Fal.ai và Nexrender

Bạn đang làm việc trong lĩnh vực xuất bản, marketing sách hoặc chỉ đơn giản là một người yêu sách muốn chia sẻ nhận xét một cách sinh động? Việc tạo video review thủ công tốn thời gian, chi phí và đòi hỏi kỹ năng thiết kế. Workflow này giúp bạn **tự động** tạo video đánh giá sách sci‑fi chỉ với vài click, không cần viết code.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ vài giờ tạo video thủ công xuống chỉ vài phút.
- **Chính xác và nhất quán**: Nội dung được sinh ra bởi ChatGPT, hình ảnh và video được tạo bởi Fal.ai, đảm bảo chất lượng đồng nhất.
- **Tự động hoá 100%**: Khi webhook nhận dữ liệu, toàn bộ quy trình từ viết script, tạo video tới xuất bản được thực hiện tự động.
- **Khả năng mở rộng**: Dễ dàng tích hợp thêm Slack, Telegram, email để gửi video ngay khi hoàn thành.
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
- **Webhook URL**: Được tạo khi bạn import workflow.
- **ChatGPT API key**: Đăng ký tại https://platform.openai.com/account/api-keys.
- **Fal.ai API key**: Đăng ký tại https://fal.ai/.
- **Nexrender**: Cài đặt Nexrender trên máy chủ hoặc sử dụng dịch vụ Render API (https://nexrender.io/).
- **Storage** (tùy chọn): S3, Google Drive hoặc Dropbox để lưu trữ video cuối cùng.
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
1. Truy cập link gốc: <https://n8n.io/workflows/12270> và tải file JSON.
2. Mở n8n Editor → **Import** → **Upload file** → chọn file JSON vừa tải.
3. Workflow sẽ xuất hiện với tên “Create AI sci‑fi book review videos with ChatGPT, Fal.ai and Nexrender”.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Mô tả | Cài đặt cần thiết |
|------|-------|-------------------|
| **Webhook** | Nhận dữ liệu sách (title, author, summary). | Đặt URL, cấu hình phương thức POST. |
| **ChatGPT** | Sinh script review dựa trên dữ liệu nhận vào. | Chọn model (gpt‑4o), nhập API key, cấu hình prompt. |
| **Fal.ai** | Tạo video từ script và hình ảnh. | Chọn template, nhập API key, cấu hình độ dài video. |
| **Nexrender** | Render video cuối cùng và lưu trữ. | Định cấu hình job, đường dẫn output, credentials lưu trữ. |
| **HTTP Request** (tùy chọn) | Gửi video tới nền tảng chia sẻ (YouTube, Vimeo). | API key, endpoint. |

> **Tip**: Kiểm tra kỹ các trường `{{ $json["field"] }}` trong các node để đảm bảo dữ liệu được truyền đúng.

### 3. Kích hoạt ⚡️
1. **Test run**: Nhấn “Execute Node” trên Webhook node với dữ liệu mẫu (JSON gồm `title`, `author`, `summary`).
2. Xem log để xác nhận mọi node hoạt động đúng.
3. Khi mọi thứ ổn, bật **Active** cho workflow.

## ✍️ Mẹo & gợi ý nâng cao
- **Slack/Telegram**: Thêm node Slack hoặc Telegram để gửi link video ngay khi hoàn thành.
- **Lưu log**: Sử dụng node “Write Binary File” để lưu log JSON vào S3, giúp theo dõi lịch sử tạo video.
- **Báo cáo định kỳ**: Kết hợp node “Cron” để tự động gửi video review hàng tuần tới kênh email marketing.
- **Tùy chỉnh prompt**: Thêm biến `genre` vào prompt ChatGPT để tạo video review phong cách khác nhau (horror, mystery, etc.).

## 📌 Kết luận
Workflow “Create AI sci‑fi book review videos with ChatGPT, Fal.ai and Nexrender” là công cụ mạnh mẽ giúp các sếp tiết kiệm thời gian, giảm chi phí và nâng cao chất lượng nội dung video. Hãy **đăng ký VPS**, **cài đặt n8n**, **import workflow** và **đặt credentials** ngay hôm nay để bắt đầu tự động hoá quy trình tạo video đánh giá sách sci‑fi 100% AI!