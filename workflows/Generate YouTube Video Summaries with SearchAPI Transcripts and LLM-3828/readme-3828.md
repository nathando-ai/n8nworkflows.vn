---
title: "🚀 Tự động tóm tắt video YouTube thông minh với SearchAPI và LLM trong n8n"
description: "Hướng dẫn cài đặt workflow n8n giúp trích xuất transcript YouTube qua SearchAPI và tự động tóm tắt nội dung cực nhanh bằng AI (OpenRouter)."
slug: "tu-dong-tom-tat-video-youtube-voi-searchapi-va-llm-trong-n8n"
tags: [n8n, automation, youtube, ai, openrouter, searchapi, summarization]
keywords: [n8n workflow, tóm tắt video youtube, searchapi transcript, openrouter ai, tự động hóa marketing, n8n ai chain]
---

# 🚀 Tự động tóm tắt video YouTube thông minh với SearchAPI và LLM

Các sếp có bao giờ mất hàng giờ chỉ để xem hết một video YouTube dài dằng dặc để tìm một ý chính? Hay đội ngũ nội dung của các sếp phải cày cuốc xem video đối thủ để lấy research? Việc xem thủ công này cực kỳ tốn thời gian, lãng phí nguồn lực và khó scale.

Đừng lo, bài toán này sẽ được giải quyết triệt để với workflow n8n tự động hóa 100%. Bằng cách kết hợp **SearchAPI** (lấy transcript YouTube) và **OpenRouter LLM** (tóm tắt thông minh), hệ thống sẽ tự động biến các video dài thành các bản tóm tắt súc tích, chuẩn xác chỉ trong tích tắc mà không cần viết một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không cần xem video dài, nhận ngay bản tóm tắt chi tiết các ý chính.
- **Tự động hóa hoàn toàn:** Chỉ cần truyền `video_id`, hệ thống tự động xử lý từ A-Z.
- **Ứng dụng AI thông minh:** Sử dụng mô hình ngôn ngữ lớn (LLM) qua OpenRouter để cấu trúc lại nội dung mạch lạc, dễ đọc.
- **Linh hoạt mở rộng:** Dễ dàng kết nối thêm vào Google Sheets, Notion, Telegram hoặc Slack để lưu trữ và chia sẻ tự động.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API Key sau:
- **n8n Instance:** Đã cài đặt sẵn (phiên bản hỗ trợ AI nodes).
- **SearchAPI Account:** Lấy API key tại [searchapi.io](https://www.searchapi.io/) để trích xuất transcript YouTube.
- **OpenRouter Account:** Lấy API key tại [openrouter.ai](https://openrouter.ai/) để sử dụng các mô hình LLM (Workflow đang cấu hình mặc định model `qwen/qwen3-0.6b-04-28:free`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy trực tiếp mã nguồn JSON.
- Trong giao diện n8n Editor, nhấn vào menu **Workflows** > **Import from File / Paste JSON** và dán đoạn mã vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 7 nodes chính được thiết kế để xử lý văn bản dài và gọi AI tóm tắt. Các sếp cần chú ý cấu hình kỹ các node sau:

- **When clicking ‘Test workflow’ (`manualTrigger`):** Node khởi chạy thủ công. Các sếp có thể thay thế bằng *Webhook*, *Schedule Trigger* hoặc kết nối từ các node khác (như nhận link video từ Google Sheets, Typeform). Hãy đảm bảo truyền đúng tham số `video_id`.
- **SearchAPI (`CUSTOM.searchApi`):** 
  - Chọn hoặc tạo mới `searchApi` credentials bằng API Key đã đăng ký.
  - Cấu hình truyền tham số `video_id` vào node này để lấy toàn bộ dữ liệu phụ đề (transcript) của video YouTube.
- **OpenRouter Chat Model (`lmChatOpenRouter`):**
  - Cấu hình `openRouterApi` credentials bằng API Key của OpenRouter.
  - Model mặc định được cài sẵn là `qwen/qwen3-0.6b-04-28:free` (hoặc các sếp có thể đổi sang các model khác mạnh hơn như Claude 3.5 Sonnet, GPT-4o nếu muốn).
- **Các node xử lý văn bản (`Split Out`, `Recursive Character Text Splitter`, `Summarize`, `Summarization Chain`):**
  - Các node này hoạt động đồng bộ để cắt nhỏ đoạn transcript dài (tránh vượt quá giới hạn token của LLM), sau đó gom nhóm và đưa vào chuỗi tóm tắt (`Summarization Chain`). Hầu như các sếp không cần chỉnh sửa sâu ở các node này trừ khi muốn tuỳ chỉnh prompt tóm tắt của AI.

#### 3. Kích hoạt ⚡️
- Nhấn **Test workflow** để chạy thử với một `video_id` mẫu (ví dụ: một video YouTube bất kỳ).
- Kiểm tra kết quả trả về ở node `Summarization Chain`.
- Nếu mọi thứ mượt mà, gạt công tắc sang **Active** để chính thức đưa workflow vào vận hành tự động!

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa workflow này cho công việc thực tế, các sếp có thể mở rộng thêm:
1. **Lưu trữ tự động:** Thêm node **Google Sheets** hoặc **Notion** ở cuối workflow để lưu tiêu đề video, link và bản tóm tắt vào một cơ sở dữ liệu chung.
2. **Thông báo qua chat:** Thêm node **Telegram** hoặc **Slack** để bot tự động gửi bản tóm tắt vào nhóm chat ngay khi có video mới.
3. **Nhận link tự động:** Thay thế Trigger thủ công bằng **Webhook** kết nối với một form thu thập link YouTube từ khách hàng hoặc team nội bộ.

### 📌 Kết luận
Việc tóm tắt video YouTube chưa bao giờ dễ dàng đến thế với sức mạnh của n8n và AI. Hãy áp dụng ngay workflow này để tối ưu hóa thời gian nghiên cứu và sản xuất nội dung của các sếp ngay hôm nay! Chúc các sếp automation thành công! 🚀