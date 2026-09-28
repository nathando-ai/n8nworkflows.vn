---
title: "🚀 Tự động hóa sản xuất Audio AI biểu cảm cao với ElevenLabs v3, Claude Sonnet, Google Drive và FTP"
description: "Xây dựng đường ống (pipeline) tự động chuyển văn bản thành giọng nói giàu cảm xúc bằng ElevenLabs v3, được tối ưu hóa thẻ cảm xúc bởi Claude Sonnet AI và tự động lưu trữ lên Google Drive cùng FTP."
slug: "tu-dong-hoa-elevenlabs-v3-tts-google-drive-ftp"
tags: [n8n, automation, elevenlabs, ai-agent, google-drive, ftp, text-to-speech]
keywords: [n8n workflow, elevenlabs v3, claude sonnet, tts automation, google drive upload, ftp upload]
---

# 🚀 Tự động hóa sản xuất Audio AI biểu cảm cao với ElevenLabs v3, Google Drive và FTP

Các sếp có bao giờ cảm thấy việc sản xuất file âm thanh (audio/voiceover) cho video, podcast hay khóa học tốn quá nhiều thời gian thủ công? Từ việc tinh chỉnh kịch bản, thêm các thẻ cảm xúc sao cho giọng đọc tự nhiên, cho đến việc xuất file MP3 rồi upload lần lượt lên Google Drive hay máy chủ FTP để đội ngũ sử dụng. 

Giờ đây, với workflow n8n cực kỳ mạnh mẽ được phát triển bởi Davide, toàn bộ quy trình này sẽ được tự động hóa 100% nhờ sự kết hợp giữa **Claude Sonnet AI**, **ElevenLabs v3**, **Google Drive** và **FTP Server**. Các sếp chỉ việc nhập văn bản, AI sẽ lo phần còn lại!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Biến văn bản thô thành file MP3 biểu cảm cao mà không cần thao tác thủ công phức tạp.
- **AI thông minh chèn thẻ cảm xúc**: Sử dụng Claude Sonnet 4.5 và Context7 MCP để tự động phân tích văn bản và thêm các thẻ ngữ điệu, cảm xúc chuẩn xác theo tài liệu ElevenLabs v3.
- **Đa kênh kích hoạt**: Hỗ trợ nhận văn bản qua Trigger thủ công, Webhook POST API hoặc qua khung chat trực tiếp.
- **Đồng bộ lưu trữ tức thì**: File MP3 sau khi render xong sẽ tự động được đẩy đồng thời lên Google Drive và máy chủ FTP (ví dụ: BunnyCDN) để sẵn sàng sử dụng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow vận hành trơn tru, các sếp cần chuẩn bị sẵn các tài khoản và API sau:
- **n8n Instance**: Đã cài đặt n8n (hỗ trợ các node LangChain và ElevenLabs Community node).
- **Anthropic API Key**: Dành cho model Claude Sonnet 4.5 trong AI Agent.
- **ElevenLabs API Key**: Tài khoản ElevenLabs (hỗ trợ v3 alpha) kèm theo Voice ID muốn sử dụng.
- **Context7 API Key**: Đăng ký miễn phí tại [Context7 Dashboard](https://context7.com/sign-in?redirect_url=%2Fdashboard) để validate các thẻ audio.
- **Google Drive Credentials**: Tài khoản Google OAuth2 để cấp quyền upload file vào thư mục chỉ định.
- **FTP Credentials**: Thông tin kết nối FTP server hoặc BunnyCDN storage của các sếp.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow này và paste trực tiếp vào giao diện n8n Editor của mình, hoặc import file JSON trực tiếp thông qua menu quản lý workflow.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import thành công, các sếp cần cấu hình các thành phần quan trọng sau:
- **Node `Anthropic Chat Model`**: Chọn kết nối `anthropicApi` và cấu hình model là `Claude Sonnet 4.5` (`claude-sonnet-4-5-20250929`).
- **Node `Context7` (mcpClientTool)**: Thiết lập Header xác thực với API Key nhận được từ Context7:
  ```json
  {
    "headers": {
      "CONTEXT7_API_KEY": "YOUR_API_KEY"
    }
  }
  ```
- **Node `Convert text to speech`**: Cài đặt ElevenLabs Community node, điền `elevenLabsApi` credentials, nhập Voice ID mong muốn và tinh chỉnh các thông số giọng nói (stability, similarity boost, style, speed...).
- **Node `Set text`**: Nơi các sếp nhập nội dung văn bản mẫu khi test chạy thủ công bằng nút `When clicking ‘Execute workflow’`.
- **Node `Upload to FTP`**: Điều chỉnh lại đường dẫn `path` trong node theo cấu trúc thư mục của các sếp (ví dụ: `=/YOUR_PATH/{{ $binary.data.fileName }}`).
- **Node `Upload file to Drive`**: Chọn tài khoản `googleDriveOAuth2Api` và cấu hình Folder ID đích để lưu trữ file MP3 trên Google Drive.
- **Webhook Node**: Nếu tích hợp hệ thống bên thứ ba gọi vào, hãy kiểm tra lại đường dẫn `path` (mặc định: `b2e00463-dec7-4dbd-9ce6-f323ef6876d0`) và phương thức `POST`.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** tại node `When clicking ‘Execute workflow’` hoặc gửi một tin nhắn test qua `When chat message received` để kiểm tra toàn bộ đường ống.
- Sau khi kiểm tra file đã xuất thành công về Google Drive và FTP, các sếp gạt công tắc sang **Active** để đưa workflow vào vận hành chính thức.

---

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Telegram/Slack Bot**: Thêm node thông báo Telegram hoặc Slack ngay sau bước upload thành công để đội ngũ nhận được link file MP3 ngay lập tức.
- **Lưu trữ Log vào Google Sheets**: Thêm một bước ghi lại lịch sử nội dung văn bản, thời gian tạo và link file Drive vào Google Sheets để dễ quản lý.
- **Xử lý hàng loạt (Batch Processing)**: Kết hợp thêm node Split In Batches nếu các sếp cần chuyển đổi cả một kịch bản sách nói (audiobook) dài hàng ngàn từ thành nhiều phân đoạn audio nhỏ.

---

### 📌 Kết luận
Workflow này là một "vũ khí" cực kỳ lợi hại cho các nhà sáng tạo nội dung, Marketer và các doanh nghiệp muốn tự động hóa hoàn toàn quy trình sản xuất âm thanh chất lượng cao. Hãy áp dụng ngay vào hệ thống n8n của các sếp để tối ưu hóa năng suất làm việc!