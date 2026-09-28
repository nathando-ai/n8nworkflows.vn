---
title: "🎙️ Tự Động Hóa Phân Tích Tin Nhắn Giọng Nói Telegram: Chuyển Văn Bản & Gửi Báo Cáo Gmail"
description: "Workflow n8n giúp chuyển đổi tin nhắn giọng nói Telegram thành văn bản bằng AssemblyAI, phân tích cảm xúc và tóm tắt bằng GPT-4.1, sau đó gửi báo cáo chi tiết qua Gmail."
slug: "phan-tich-tin-nhan-giong-noi-telegram-gmail"
tags: [n8n, automation, no-code, assemblyai, openai, telegram, gmail]
keywords: [n8n workflow, tự động hóa, chuyển giọng nói thành văn bản, phân tích cảm xúc, telegram bot]
---

# 🎙️ Tự Động Hóa Phân Tích Tin Nhắn Giọng Nói Telegram: Chuyển Văn Bản & Gửi Báo Cáo Gmail

Trong môi trường kinh doanh hiện đại, đặc biệt là với các startup và doanh nghiệp nhỏ (SMB), việc ghi âm cuộc họp hoặc trao đổi công việc qua tin nhắn giọng nói (voice notes) trên Telegram đang trở nên cực kỳ phổ biến. Tuy nhiên, nỗi đau lớn nhất là: **Làm sao để khai thác giá trị từ những đoạn audio đó?**

Lắng nghe lại từng đoạn audio để tìm thông tin quan trọng, tóm tắt ý chính hay xác định hành động cần làm (action items) là một quá trình tốn thời gian và dễ bỏ sót chi tiết. Workflow này giải quyết hoàn toàn vấn đề đó. Nó tự động bắt tin nhắn giọng nói từ Telegram, sử dụng **AssemblyAI** để chuyển giọng nói thành văn bản chính xác, sau đó dùng sức mạnh của **GPT-4.1** để phân tích sâu: tóm tắt, đánh giá cảm xúc, trích xuất ý chính và các hành động cần thực hiện. Cuối cùng, một báo cáo chuyên nghiệp được gửi thẳng vào hộp thư Gmail của bạn.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, đặc biệt khi xử lý file audio (có thể mất vài giây đến vài phút), các sếp nên cài n8n trên VPS riêng (Self-hosted) để tránh giới hạn thời gian thực thi của các bản dùng thử.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian đáng kể:** Không cần nghe lại audio, mọi thông tin quan trọng được tóm tắt trong vài giây.
- **Phân tích chuyên sâu:** Không chỉ là văn bản thô, bạn nhận được phân tích cảm xúc (Sentiment), các ý chính (Key Points), và danh sách việc cần làm (Action Items).
- **Lưu trữ có cấu trúc:** Báo cáo được gửi qua Gmail, dễ dàng tìm kiếm, lưu trữ và chia sẻ cho đội ngũ.
- **Tự động hóa 100%:** Workflow hoạt động liên tục, xử lý mọi tin nhắn giọng nói mới đến mà không cần can thiệp thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị các tài khoản và API keys sau:
1. **Telegram Bot Token:** Tạo bot qua @BotFather và lấy API Token.
2. **AssemblyAI API Key:** Đăng ký tại [AssemblyAI](https://www.assemblyai.com/) để sử dụng dịch vụ chuyển giọng nói thành văn bản (Speech-to-Text).
3. **OpenAI API Key:** Đăng ký tại [OpenAI Platform](https://platform.openai.com/) để sử dụng mô hình GPT-4.1 (hoặc GPT-4o) cho phân tích.
4. **Gmail OAuth2:** Tài khoản Gmail để kết nối và gửi email.
5. **n8n Instance:** Một instance n8n đang chạy (Cloud hoặc Self-hosted).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n của bạn.
2. Chọn **Import from URL** hoặc **Import from File** (nếu bạn đã tải file JSON về).
3. Dán link gốc: `https://n8n.io/workflows/8605` hoặc chọn file JSON đã tải.
4. Workflow sẽ xuất hiện trong editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Đây là phần quan trọng nhất. Các sếp cần kiểm tra và cấu hình lại các node sau:

**1. Node `Voice Message` (Telegram Trigger)**
- Chọn **Credentials** cho Telegram API.
- Đảm bảo Bot Token đã được thêm vào n8n Credentials.
- *Lưu ý:* Bot cần được thêm vào nhóm hoặc chat nơi bạn sẽ gửi tin nhắn giọng nói.

**2. Node `Upload Audio to Assembly AI` (HTTP Request)**
- Trong phần **Body** (JSON), tìm trường `api_key`.
- Thay thế placeholder `<<YOUR_ASSEMBLYAI_API_KEY>>` bằng API Key thật của bạn.
- *Mẹo:* Nếu muốn tăng độ chính xác, bạn có thể thêm các tham số khác như `language_code` (ví dụ: 'vi' cho tiếng Việt, 'en' cho tiếng Anh) vào body JSON nếu AssemblyAI hỗ trợ trong cấu hình này.

**3. Node `Get Transcript` & `Request Transcript from AssemblyAI2` (HTTP Request)**
- Các node này dùng để lấy kết quả từ AssemblyAI.
- Kiểm tra URL và headers. Đảm bảo API Key được truyền đúng (thường là trong header `authorization` hoặc body, tùy thuộc vào cách AssemblyAI yêu cầu).
- *Lưu ý:* Workflow có node `Wait` để chờ AssemblyAI xử lý xong. Nếu audio dài, bạn có thể cần tăng thời gian chờ ở node `Wait`.

**4. Node `Transcript Analysis (AI)` (OpenAI)**
- Chọn **Credentials** cho OpenAI API.
- Kiểm tra **Model**: Đảm bảo model được chọn là `gpt-4.1` hoặc `gpt-4o` (hoặc model nào bạn có quyền truy cập).
- **System Prompt:** Đọc kỹ prompt trong node này. Nó hướng dẫn AI cách tóm tắt, phân tích cảm xúc và trích xuất action items. Các sếp có thể tùy chỉnh prompt này để phù hợp với ngành nghề của mình (ví dụ: tập trung vào kỹ thuật, marketing, hay tài chính).
- **Input:** Đảm bảo input nhận đúng transcript từ bước trước.

**5. Node `Send Analysis Email` (Gmail)**
- Chọn **Credentials** cho Gmail OAuth2.
- Thay thế placeholder `<<YOUR_EMAIL ID>>` trong trường **To** bằng địa chỉ email thật của bạn.
- Kiểm tra **Subject** và **HTML Body** để đảm bảo định dạng email đẹp và dễ đọc.

**6. Node `Route: Text vs Audio` (Switch)**
- Node này phân loại tin nhắn là text hay audio.
- Đảm bảo logic switch đúng với cấu trúc dữ liệu trả về từ Telegram Trigger.

#### 3. Kích hoạt ⚡️
1. **Test Run:**
   - Nhấn **Execute Workflow**.
   - Gửi một tin nhắn giọng nói ngắn (ví dụ: "Chào bạn, đây là một cuộc họp về dự án X. Chúng ta cần hoàn thành báo cáo trước thứ Sáu.") đến Bot Telegram.
   - Theo dõi execution trong n8n. Đảm bảo các node chạy lần lượt: Trigger -> Upload -> Wait -> Get Transcript -> AI Analysis -> Send Email.
   - Kiểm tra hộp thư Gmail xem email có đến đúng không và nội dung có chính xác không.
2. **Bật Active:**
   - Sau khi test thành công, nhấn nút **Active** (góc trên bên phải) để workflow bắt đầu chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tùy chỉnh Prompt AI:** Thay đổi System Prompt trong node `Transcript Analysis (AI)` để yêu cầu AI tập trung vào các khía cạnh cụ thể. Ví dụ: "Hãy trích xuất các con số quan trọng" hoặc "Đánh giá mức độ khẩn cấp của từng action item".
- **Gửi báo cáo qua Slack/Telegram:** Thay vì chỉ gửi Gmail, bạn có thể thêm node `Slack` hoặc `Telegram` để gửi báo cáo trực tiếp vào kênh chat làm việc, giúp team phản hồi nhanh hơn.
- **Lưu trữ vào Google Sheets/Notion:** Thêm node `Google Sheets` hoặc `Notion` để lưu transcript và các action items vào bảng tính hoặc database, tạo thành một kho tri thức (knowledge base) cho công ty.
- **Phân loại theo dự án:** Sử dụng AI để phân loại tin nhắn theo dự án hoặc khách hàng, sau đó gửi báo cáo vào các thư mục Gmail khác nhau hoặc các kênh Slack khác nhau.

### 📌 Kết luận
Workflow này là một công cụ mạnh mẽ giúp các sếp biến những tin nhắn giọng nói "chết" thành dữ liệu có giá trị, dễ truy cập và hành động. Với sự kết hợp của AssemblyAI và GPT-4.1, bạn không chỉ tiết kiệm thời gian mà còn nâng cao hiệu quả làm việc và ra quyết định. Hãy import, cấu hình và bắt đầu tự động hóa quy trình làm việc của bạn ngay hôm nay!