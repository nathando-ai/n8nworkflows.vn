---
title: "🚀 Tự động hóa biến tài liệu PDF thành Podcast 2 MC với OpenAI, Smallest AI và Gmail"
description: "Biến mọi tài liệu PDF thành podcast đối thoại 2 người chuyên nghiệp phong cách NotebookLM bằng n8n, tích hợp GPT-5, Smallest AI Lightning và gửi trực tiếp qua Gmail."
slug: "chuyen-pdf-thanh-podcast-2-mc-n8n-openai-smallest-ai"
tags: [n8n, automation, ai, openai, smallest-ai, podcast, gpt-5]
keywords: [n8n workflow, pdf to podcast, smallest ai, openai gpt-5, tu dong hoa podcast, text to speech, gmail automation]
---

# 🚀 Biến tài liệu PDF thành Podcast 2 MC cực đỉnh với AI

Các sếp có tài liệu PDF dài dằng dặc, báo cáo nghiên cứu hay sách trắng mà không có thời gian đọc? Thay vì đọc chay, hãy để workflow n8n này tự động "biến phép thuật" chuyển hóa chúng thành một **podcast đối thoại sống động giữa 2 MC** (giống phong cách NotebookLM của Google) và gửi thẳng vào hộp thư Gmail của các sếp! 

Đặc biệt, workflow này hỗ trợ hơn 19 ngôn ngữ (bao gồm cả tiếng Việt, tiếng Anh và nhiều ngôn ngữ khác) với công nghệ tổng hợp giọng nói siêu tốc từ Smallest AI, kết hợp xử lý âm thanh thuần bằng JavaScript mà không cần cài đặt FFmpeg phức tạp.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow xử lý các file PDF lớn và chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian tối đa:** Tự động hóa hoàn toàn từ khâu nhận file PDF, tạo kịch bản, chuyển đổi giọng nói đến gửi email.
- **Trải nghiệm nghe tự nhiên:** Podcast có sự tham gia của 2 MC đối thoại qua lại, phân tích tài liệu một cách sinh động thay vì đọc văn bản khô khan.
- **Đa ngôn ngữ & Giọng đọc phong phú:** Hỗ trợ hơn 19 ngôn ngữ với chất lượng âm thanh siêu tốc (~100ms TTFB).
- **Hoạt động linh hoạt:** Sử dụng mã JavaScript thuần để ghép nối file WAV, chạy mượt mà ngay cả trên n8n Cloud mà không cần cấu hình phức tạp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Smallest AI API Key**: Lấy tại [Smallest AI Dashboard](https://app.smallest.ai/dashboard/api-keys) (có gói miễn phí).
- **OpenAI API Key**: Hỗ trợ GPT-5 hoặc GPT-4o-mini để viết kịch bản.
- **Tài khoản Gmail**: Cấu hình OAuth2 để gửi email tự động.
- **Community Node**: Cần cài đặt `n8n-nodes-smallestai` trong n8n trước khi import workflow.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Cài đặt Community Node `n8n-nodes-smallestai` bằng cách vào **Settings → Community Nodes → Install** trên giao diện n8n.
- Copy mã JSON của workflow hoặc import file JSON trực tiếp vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 13 nodes hoạt động nhịp nhàng. Các sếp cần chú ý cấu hình các điểm sau:
- **When Form Submitted (`formTrigger`)**: Nơi người dùng tải file PDF lên qua form giao diện.
- **Generate Podcast Script (GPT-5) (`openAi`)**: Nhập OpenAI API Key, chọn model (GPT-5 hoặc GPT-4o-mini) và đảm bảo cấu hình schema JSON để sinh ra kịch bản đối thoại 2 người chuẩn xác.
- **Synthesize Host A Audio & Synthesize Host B Audio (`n8n-nodes-smallestai.smallestai`)**: 
  - Kết nối Smallest AI API Key.
  - Tùy chỉnh `voiceId` (Mặc định: `avery` cho Host A và `devansh` cho Host B). Có thể tham khảo thêm kho giọng đọc tại [Smallest AI Voices](https://docs.smallest.ai/waves/v-4-0-0/api-reference/api-reference/voices/get-waves-voices).
  - **LƯU Ý QUAN TRỌNG:** Giữ nguyên thông số `sample_rate` đồng nhất ở cả 2 node giọng nói để tránh file WAV sau khi ghép bị nhiễu/lỗi âm thanh.
- **Concatenate WAV Audio (`code`)**: Node sử dụng code JavaScript thuần để nối các đoạn audio theo thứ tự cuộc trò chuyện mà không cần FFmpeg.
- **Email Podcast to User (`gmail`)**: 
  - Kết nối tài khoản Gmail qua OAuth2.
  - **Cập nhật trường `To`**: Thay đổi địa chỉ email nhận kết quả thành email thực tế của các sếp.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và thử tải lên một file PDF mẫu thông qua Form Trigger để test quá trình chạy.
- Kiểm tra hộp thư Gmail xem đã nhận được file podcast định dạng `.wav` chưa.
- Sau khi test thành công, bật công tắc **Active** để đưa workflow vào vận hành chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Đổi chủ đề / Phong cách kịch bản:** Sửa đổi system prompt trong node OpenAI để đổi phong cách từ đối thoại thông thường sang dạng tranh luận (debate), phỏng vấn chuyên sâu, hoặc kể chuyện cho trẻ em.
- **Đa dạng kênh trả kết quả:** Thay vì chỉ gửi qua Gmail, các sếp có thể mở rộng nhánh để gửi file audio tự động lên **Telegram Bot**, **Slack Channel**, hoặc lưu trực tiếp vào **Google Drive**.
- **Tạo bản ghi lưu trữ:** Thêm một node Google Sheets để ghi lại lịch sử các tài liệu PDF đã được chuyển đổi thành công kèm thời gian và tên file.

### 📌 Kết luận
Workflow "PDF to Podcast" là giải pháp tự động hóa đỉnh cao giúp các sếp tận dụng sức mạnh của AI đa phương thức để tối ưu hóa việc tiếp thu kiến thức từ tài liệu. Hãy cài đặt ngay hôm nay để biến mọi tài liệu thành những phút giây nghe podcast thú vị!