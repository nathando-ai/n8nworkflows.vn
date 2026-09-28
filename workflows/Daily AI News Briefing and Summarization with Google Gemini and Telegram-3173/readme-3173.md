---
title: "📰 Tự Động Hóa Tin Tức AI Hàng Ngày: Tổng Hợp & Gửi Telegram"
description: "Workflow n8n tự động thu thập tin tức từ GNews và NewsAPI, sử dụng Google Gemini AI để tóm tắt thông minh và gửi báo cáo hàng ngày qua Telegram."
slug: "tu-dong-hoa-tin-tuc-ai-telegram"
tags: [n8n, automation, no-code, ai, telegram, google-gemini]
keywords: [n8n workflow, tự động hóa tin tức, ai summarization, telegram bot, google gemini api]
---

# 📰 Tự Động Hóa Tin Tức AI Hàng Ngày: Tổng Hợp & Gửi Telegram

Trong thời đại thông tin bùng nổ, việc theo dõi tin tức hàng ngày có thể trở thành một gánh nặng. Các sếp thường phải dành hàng giờ mỗi sáng để lướt qua hàng chục trang web, đọc các bài báo dài dòng và cố gắng lọc ra những thông tin thực sự quan trọng. Không chỉ tốn thời gian, việc này còn dễ bỏ sót những xu hướng công nghệ hoặc thị trường quan trọng.

Workflow **Daily AI News Briefing** được thiết kế để giải quyết triệt để vấn đề này. Thay vì làm thủ công, các sếp sẽ có một "trợ lý AI" tự động chạy mỗi sáng, thu thập tin tức từ các nguồn uy tín, sử dụng sức mạnh của **Google Gemini** để tóm tắt ngắn gọn, dễ hiểu và gửi thẳng vào **Telegram** của các sếp. Toàn bộ quy trình diễn ra hoàn toàn tự động, không cần viết một dòng code nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian đáng kể:** Không cần đọc hàng chục bài báo, chỉ cần đọc bản tin tóm tắt 30 giây.
- **Thông tin chính xác & tập trung:** AI Gemini lọc bỏ thông tin nhiễu, giữ lại các điểm mấu chốt.
- **Đa nguồn tin tức:** Kết hợp dữ liệu từ cả GNewsAPI và NewsAPI để có cái nhìn toàn diện.
- **Tiện lợi tối đa:** Nhận báo cáo trực tiếp trên điện thoại qua Telegram mọi lúc, mọi nơi.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị các tài khoản và API keys sau:
1. **Tài khoản n8n:** Đã cài đặt và chạy được n8n (Cloud hoặc Self-hosted).
2. **Google Gemini API Key:** Đăng ký tại [Google AI Studio](https://aistudio.google.com/) để lấy API Key cho node `Google Gemini Chat Model`.
3. **GNews API Key:** Đăng ký tại [GNews.io](https://gnews.io/) (có gói miễn phí).
4. **NewsAPI Key:** Đăng ký tại [NewsAPI.org](https://newsapi.org/) (có gói miễn phí cho cá nhân).
5. **Telegram Bot Token:** Tạo bot qua @BotFather trên Telegram để lấy Token.
6. **Telegram Chat ID:** ID của kênh hoặc nhóm mà các sếp muốn nhận tin.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n Editor.
2. Chọn **Import from File** hoặc **Import from URL**.
3. Tải file JSON của workflow này hoặc dán link gốc: `https://n8n.io/workflows/3173`.
4. Sau khi import, các sếp sẽ thấy 10 nodes được kết nối sẵn.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Đây là phần quan trọng nhất. Các sếp cần click vào từng node và điền thông tin theo hướng dẫn sau:

**A. Node `Trigger workflow at 6am everyday` (Schedule Trigger)**
- Mặc định workflow chạy lúc 6:00 sáng. Các sếp có thể chỉnh giờ theo nhu cầu (ví dụ: 7:00 sáng để đọc trước khi đi làm).

**B. Node `News Source: GNewsAPI` (HTTP Request)**
- **URL:** Kiểm tra lại URL API.
- **Headers/Query Parameters:** Điền `API Key` của GNews vào đây.
- **Query Params:** Chỉnh `q` (keyword) nếu muốn tìm tin về chủ đề cụ thể (ví dụ: "AI", "Marketing", "Vietnam"). Mặc định có thể là tin công nghệ chung.

**C. Node `News Source: NewsAPI` (HTTP Request)**
- Tương tự, điền `API Key` NewsAPI vào Query Parameters.
- Đảm bảo `from` và `to` date được cấu hình đúng (thường là ngày hôm qua hoặc hôm nay tùy logic).

**D. Node `Substract Current date by one` (Date & Time)**
- Node này tính toán ngày hôm trước để lấy tin tức mới nhất. Thường không cần chỉnh sửa gì thêm nếu logic mặc định phù hợp.

**E. Node `ExtractAllNews` & `ExtractAllNews1` (Set)**
- Các node này dùng để chuẩn hóa dữ liệu từ 2 nguồn tin khác nhau trước khi gộp lại.
- Kiểm tra xem các trường `title`, `description`, `url` có được map đúng không.

**F. Node `Merge` (Merge)**
- Gộp dữ liệu từ 2 nguồn tin. Đảm bảo chế độ Merge là "Append" hoặc "Combine" tùy thuộc vào cấu trúc dữ liệu đầu vào.

**G. Node `Google Gemini Chat Model` (LM Chat Google Gemini)**
- **Model:** Chọn model phù hợp (ví dụ: `gemini-1.5-flash` hoặc `gemini-1.5-pro` tùy tốc độ và chất lượng cần thiết).
- **API Key:** Dán **Google Gemini API Key** vào đây.

**H. Node `AI Agent` (Agent)**
- **System Prompt:** Đây là "linh hồn" của workflow. Các sếp có thể chỉnh sửa prompt để thay đổi giọng văn tóm tắt.
  - *Ví dụ prompt mặc định:* "Bạn là một chuyên gia tin tức. Hãy tóm tắt các tin tức sau đây thành một bản tin ngắn gọn, dễ đọc, chia thành các mục rõ ràng. Sử dụng emoji để tăng tính trực quan."
- **Tools:** Đảm bảo không có tool nào được gắn nếu chỉ cần tóm tắt văn bản.

**I. Node `Telegram` (Telegram)**
- **Credentials:** Chọn hoặc tạo mới credentials Telegram.
  - **Bot Token:** Dán token từ @BotFather.
- **Chat ID:** Dán ID của kênh/nhóm cá nhân.
- **Message:** Kiểm tra biểu thức (expression) để đảm bảo nội dung từ AI Agent được truyền vào trường `text`.

#### 3. Kích hoạt ⚡️
1. **Test Run:** Click vào nút **Execute Workflow** (hoặc chạy từng node) để kiểm tra xem dữ liệu có được lấy từ API, AI có tóm tắt đúng và Telegram có nhận được tin không.
2. **Active Workflow:** Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để workflow tự động chạy hàng ngày.

### ✍️ Mẹo & gợi ý nâng cao
- **Cá nhân hóa chủ đề:** Thay vì tin tức chung chung, các sếp có thể thay đổi keyword trong node HTTP Request để tập trung vào ngành nghề của mình (ví dụ: "Real Estate", "Crypto", "SaaS").
- **Gửi vào nhóm riêng:** Tạo một kênh Telegram riêng cho "Bản tin AI" để không làm phiền các cuộc trò chuyện cá nhân.
- **Lưu trữ lịch sử:** Thêm một node `Google Sheets` hoặc `Notion` sau node Telegram để lưu lại toàn bộ bản tin hàng ngày, giúp các sếp dễ dàng tra cứu lại tin tức cũ.
- **Đa ngôn ngữ:** Chỉnh sửa System Prompt của AI Agent để yêu cầu tóm tắt bằng tiếng Việt thay vì tiếng Anh, giúp việc đọc hiểu nhanh hơn.

### 📌 Kết luận
Với workflow **Daily AI News Briefing**, các sếp không còn phải lo lắng về việc bỏ lỡ thông tin quan trọng hay tốn thời gian đọc tin tức. Chỉ với vài phút cấu hình ban đầu, các sếp sẽ có một nguồn tin tức được "chưng cất" bởi AI, gửi thẳng vào điện thoại mỗi sáng. Hãy thử ngay hôm nay và trải nghiệm sự khác biệt trong cách tiếp cận thông tin!