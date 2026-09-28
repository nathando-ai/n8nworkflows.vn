---
title: "🚀 Tự động trích xuất và làm sạch Transcript video YouTube bằng n8n & YouTube Data API"
description: "Hướng dẫn chi tiết cách sử dụng workflow n8n để trích xuất, lọc ngôn ngữ, tải file VTT và làm sạch transcript video YouTube tự động cho AI xử lý."
slug: "trich-xuat-clean-transcript-youtube-n8n"
tags: [n8n, automation, youtube-api, ai-summarization, document-extraction]
keywords: [n8n workflow, trích xuất transcript youtube, youtube data api, làm sạch sub youtube, automation n8n]
---

# 🚀 Tự động trích xuất và làm sạch Transcript video YouTube bằng n8n

Các sếp có bao giờ cảm thấy mệt mỏi khi phải thủ công nghe lại video, copy sub hoặc xử lý các tệp phụ đề (VTT, SRT) lộn xộn chứa đầy thời gian, chú thích âm thanh `[Music]` hay các dòng lặp lại để đưa vào AI tóm tắt chưa? 

Việc này vừa tốn thời gian, vừa làm giảm chất lượng đầu vào khi đưa dữ liệu vào các mô hình LLM. Đừng lo, bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ mạnh mẽ do **Joel Cantero** thiết kế, giúp tự động hóa 100% quy trình gọi YouTube Data API, tải phụ đề, chọn ngôn ngữ thông minh, loại bỏ các ký tự rác và trả về một bản transcript hoàn toàn sạch sẽ, sẵn sàng phục vụ cho các chiến dịch AI Content của doanh nghiệp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Nhận `videoId` và trả về văn bản transcript sạch chỉ trong vài giây.
- **Lọc ngôn ngữ thông minh**: Tự động khớp với ngôn ngữ ưu tiên của các sếp (ví dụ: `es`, `en`, `vi`...), có cơ chế fallback thông minh về ngôn ngữ mặc định nếu không tìm thấy.
- **Làm sạch chuyên sâu**: Tự động xóa sạch timestamps (`00:01:23`), tiêu đề WEBVTT, hiệu ứng âm thanh (`[Music]`, `[Música]`), từ trùng lặp và khoảng trắng thừa.
- **Sẵn sàng cho AI**: Dữ liệu đầu ra đi kèm metadata (`wordCount`, `charCount`, `status`) chuẩn mực, cực kỳ tối ưu để nối tiếp (downstream) với các AI Summarization, Sentiment Analysis hoặc Content Generation nodes.
:::

### Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance**: Đã cài đặt n8n (Self-hosted hoặc Cloud).
- **YouTube OAuth2 Credentials**: Cần có tài khoản Google Cloud Console, tạo OAuth2 Client ID/Secret và cấp quyền cho scope `youtube.captions.read` và `youtube.force-ssl`.
- **Lưu ý quan trọng từ tác giả**: API này chỉ hoạt động với các video thuộc **chính kênh YouTube của các sếp** (Authenticated Channel). Không thể lấy phụ đề từ video công khai của kênh khác do giới hạn của YouTube Data API v3.
:::

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể sử dụng file JSON workflow của n8n (Link gốc: [n8n Workflow #11795](https://n8n.io/workflows/11795)), copy toàn bộ mã JSON và paste trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 10 nodes hoạt động nhịp nhàng với nhau. Các sếp cần chú ý cấu hình kỹ các điểm sau:

- **Node "When Executed by Another Workflow" (`executeWorkflowTrigger`)**: Đóng vai trò làm Sub-workflow nhận dữ liệu truyền vào. Các sếp có thể thay thế bằng Webhook hoặc Form Trigger nếu muốn chạy độc lập.
  - *Ví dụ JSON payload đầu vào:*
  ```json
  {
    "youtubeVideoId": "nxub8Bmia68",
    "preferredLanguage": "es"
  }
  ```
- **Nodes "List Captions" & "Download VTT" (`httpRequest`)**: 
  - ⚠️ **BẮT BUỘC**: Phải kết nối tài khoản **YouTube OAuth2 API** của các sếp tại đây.
  - Đảm bảo tài khoản Google đã được cấp quyền `youtube.captions.read`.
- **Node "Caption Language Selector" (`code`)**: Chạy đoạn mã JavaScript thông minh để lọc ngôn ngữ:
  1. Khớp chính xác với `preferredLanguage` được truyền vào (ví dụ: `es`, `en`).
  2. Fallback về caption đầu tiên có sẵn nếu không tìm thấy ngôn ngữ ưu tiên.
- **Node "Caption File Conversion" (`extractFromFile`)**: Xử lý tệp nhị phân VTT tải về và trích xuất thành văn bản thuần túy (plain text).
- **Node "Clean Transcript" (`code`)**: Thực hiện các thuật toán Regex để loại bỏ timestamps, các thẻ WEBVTT rác, hiệu ứng âm thanh `[Music]` và chuẩn hóa khoảng trắng.
- **Node "No Captions Fallback" & "Stop and Error" (`stopAndError`)**: Xử lý trường hợp video không có sub, trả về thông báo lỗi cấu trúc rõ ràng thay vì làm sập workflow âm thầm.

#### 3. Kích hoạt ⚡️
- Thực hiện **Test Step** từng node với `videoId` từ kênh của các sếp để kiểm tra kết quả trả về.
- Sau khi test thành công, bật **Active** để đưa workflow vào vận hành chính thức.

---

### ✍️ Mẹo & gợi ý nâng cao
Để khai thác tối đa sức mạnh của workflow này, các sếp có thể mở rộng thêm:
1. **Tích hợp AI Summarizer**: Nối tiếp node `Clean Transcript` với OpenAI / Anthropic Node để tự động tóm tắt video thành các bài blog, bullet points hoặc trích xuất từ khóa.
2. **Lưu trữ tự động**: Đẩy toàn bộ `text` và `metadata` vào Google Sheets hoặc Notion Database để xây dựng thư viện nội dung số cho kênh YouTube.
3. **Thông báo qua Slack/Telegram**: Gửi báo cáo hoàn thành hoặc cảnh báo lỗi qua webhook chat ngay khi quá trình trích xuất hoàn tất.

---

### 📌 Kết luận
Workflow trích xuất và làm sạch transcript YouTube này là một "vũ khí bí mật" giúp các content creator, marketer và các nhà phát triển tự động hóa toàn bộ khâu chuẩn bị dữ liệu đầu vào cho AI. Hãy cài đặt ngay hôm nay để tiết kiệm hàng giờ đồng hồ thao tác thủ công! Chúc các sếp automation vui vẻ! 🎉