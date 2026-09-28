---
title: "🚀 Giáo viên AI dạy ngôn ngữ qua Telegram, Google Sheets và GPT-4o"
description: "Tự động hóa việc học từ vựng và luyện tập trò chuyện bằng AI Agent kết nối Telegram, Google Sheet và mô hình GPT-4o."
slug: "ai-powered-language-teacher-telegram-google-sheet-gpt4o"
tags: [n8n, automation, no-code, AI, telegram, google-sheets, openai]
keywords: [n8n workflow, tự động hóa, học ngôn ngữ, AI agent, telegram bot]
---

# 🚀 Giáo viên AI dạy ngôn ngữ qua Telegram, Google Sheets và GPT-4o

Bạn từng cảm thấy học từ vựng bằng sách giấy hoặc ứng dụng flashcard là quá đơn điệu, thiếu tương tác và không thể thích ứng với phong cách học của từng người? Việc tạo ra các bài tập cá nhân hóa, theo dõi tiến độ và cung cấp phản hồi即时 thường tốn nhiều thời gian và dễ bị lỗi khi làm thủ công. Workflow **AI Powered Language Teacher** giải quyết triệt để những nỗi đau này bằng cách biến Telegram thành một gia sư AI 24/7: mỗi tin nhắn từ học viên sẽ kích hoạt một luồng tự động lấy từ vựng từ Google Sheet, tạo ra câu hỏi phù hợp qua GPT‑4o, và trả lời ngay trong cuộc trò chuyện – toàn bộ过程 không cần viết một dòng code nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Học viên nhận được bài tập và phản hồi ngay lập tức mà không cần chờ giáo viên kiểm tra.
- **Cá nhân hóa cao**: Mỗi người dùng có riêng một cuộc trò chuyện dựa trên `chat id`, AI Agent nhớ ngữ cảnh và điều chỉnh độ khó theo tiến độ.
- **Chính xác và nhất quán**: Từ vựng được lấy trực tiếp từ Google Sheet, tránh lỗi nhập liệu hand‑made.
- **Hoạt động liên tục**: Bot Telegram sẵn sàng trả lời 24/7, giúp học tập không bị gián đoạn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Telegram Bot**: Tạo bot qua @BotFather và lấy **Bot Token** để cấu hình nút *Telegram Trigger* và *Telegram* (gửi trả lời).
- **Google Sheet**: Một file chứa danh sách từ vựng (cột tiếng Việt – cột tiếng Anh hoặc bất kỳ cặp ngôn ngữ nào). Cần bật **Google Sheets API** và lấy **OAuth2 credentials** (hoặc API Key) để nút *Retrieve Vocabulary* truy cập.
- **OpenAI API Key**: Để sử dụng mô hình **gpt-4o-mini** (hoặc gpt-4o) qua node *OpenAI Chat Model* trong AI Agent.
- **Tài khoản n8n** (self‑hosted hoặc cloud) có quyền cài đặt các node trên.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Trong n8n Editor, nhấn **Import** → **From File** hoặc dán trực tiếp JSON của workflow vào khung **Import from Clipboard**.
2. Nhấn **Import** để workflow xuất hiện trên canvas.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Cấu hình bắt buộc |
|------|-------------------|
| **Telegram Trigger** | - Chọn **Credentials** → tạo mới hoặc chọn credential Telegram Bot đã có.<br>- Để mặc định **Updates Type** = `Message` (hoặc `All Updates` nếu muốn bắt mọi loại tin). |
| **Retrieve Vocabulary (Google Sheets)** | - Thêm **Google Sheets Credentials** (OAuth2) hoặc dùng **API Key** nếu sheet công khai.<br>- Trong trường **Spreadsheet ID**, dán ID của file Google Sheet (phần giữa URL).<br>- Chọn **Sheet Name** chứa danh sách từ vựng (ví dụ: `Vocab`).<br>- Đảm bảo cột A = từ nguồn (tiếng Việt), cột B = từ đích (tiếng Anh) – hoặc điều chỉnh mapping trong node nếu cần. |
| **OpenAI Chat Model** ( внутри AI Agent ) | - Thêm **OpenAI Credentials** với API Key.<br>- Chọn **Model** = `gpt-4o-mini` (hoặc gpt-4o nếu muốn chất lượng cao hơn).<br>- Trong **System Prompt** của AI Agent, viết rõ mục tiêu học ngôn ngữ, ví dụ: <br>`Bạn là gia sư tiếng Anh. Hãy sử dụng danh sách từ vựng sau: {{ $json["vocabulary_en"] }} và {{ $json["vocabulary_vi"] }} để tạo ra câu hỏi trắc nghiệm hoặc điền lỗi cho học viên. Ghi nhớ cuộc trò chuyện dựa trên chat id.` |
| **Simple Memory** (Memory Buffer Window) | - Đặt **Window Size** = số lượng tin nhắn gần nhất muốn ghi nhớ (ví dụ: 5) để AI Agent duy trì ngữ cảnh ngắn hạn. |
| **Aggregate Vocabulary Lists** | - Không cần thay đổi; node này chỉ gộp hai mảng từ vựng (tiếng Việt và tiếng Anh) thành hai chuỗi riêng để truyền vào AI Agent. |
| **Answer to the User (Telegram)** | - Chọn cùng **Telegram Credentials** như nút Trigger.<br>- Trong trường **Chat ID**, để expression `{{ $json["chatId"] }}` (node Telegram Trigger đã cung cấp).<br>- Nội dung tin nhắn sẽ lấy từ output của AI Agent (`{{ $json["output"] }}`). |

#### 3. Kích hoạt ⚡️
- Nhấn **Workflow → Execute Workflow** để chạy một lần test với tin nhắn mẫu (ví dụ: “Hello”). Kiểm tra xem bot có trả lời đúng không.
- Nếu tudo ổn, bật toggle **Active** ở góc trên‑phía bên phải workflow để nó bắt đầu lắng nghe tin nhắn thực từ Telegram.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo tiến độ**: Thêm một node *Telegram* sau mỗi 5 câu trả lời để gửi báo cáo ngắn gọn về số từ đã học, tỷ lệ đúng.
- **Lưu log vào Google Sheets**: Kết nối node *Google Sheets* (append) để ghi lại mỗi cuộc trò chuyện (chat id, timestamp, câu hỏi, câu trả lời) để phân tích sau này.
- **Nhắc nhở học tập**: Sử dụng node *Cron* để triggers mỗi sáng gửi tin nhắn “Hôm nay bạn muốn ôn tập từ vựng nào?” qua Telegram.
- **Đa ngôn ngữ**: Sao chép workflow, thay đổi Google Sheet và System Prompt để hỗ trợ nhiều ngôn ngữ khác (thái, Nhật,…) mà không cần viết lại từ đầu.
- **Phản hồi giọng nói**: Kết hợp với dịch vụ Text‑to‑Speech (Google Cloud TTS hoặc ElevenLabs) để bot gửi tin nhắn voix cùng với văn bản.

### 📌 Kết luận
Workflow **AI Powered Language Teacher** biến Telegram thành một gia sư AI thông minh, tự động lấy từ vựng từ Google Sheet, tạo ra bài tập cá nhân hóa bằng GPT‑4o và trả lời ngay trong cuộc trò chuyện. Với chỉ một vài bước cấu hình credential và điều chỉnh prompt, các sếp có thể triển khai ngay một hệ thống học ngôn ngữ hoạt động 24/7, giảm tải công việc thủ công và nâng cao trải nghiệm học tập cho học viên. Hãy import, thử nghiệm và kích hoạt hôm nay để thấy sự khác biệt ngay lập tức!