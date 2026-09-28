---
title: "📰 Tự Động Hóa Bản Tin AI: GPT-5.1 + NewsAPI + Tavily Gửi Telegram"
description: "Workflow n8n tự động thu thập tin tức, dùng AI chọn lọc và tóm tắt chuyên sâu, sau đó gửi bản tin Markdown định kỳ qua Telegram. Không cần code, tiết kiệm hàng giờ mỗi tuần."
slug: "tu-dong-hoa-ban-tin-ai-telegram"
tags: [n8n, automation, no-code, ai-newsletter, telegram-bot, gpt-5]
keywords: [n8n workflow, tự động hóa tin tức, ai summarization, telegram bot, newsapi integration]
---

# 📰 Tự Động Hóa Bản Tin AI: GPT-5.1 + NewsAPI + Tavily Gửi Telegram

Việc theo dõi tin tức hàng ngày có thể trở thành một gánh nặng thực sự. Các sếp thường phải lướt qua hàng chục trang báo, mạng xã hội và blog để tìm ra những thông tin thực sự quan trọng cho ngành của mình. Làm thủ công không chỉ tốn thời gian mà còn dễ bỏ sót những chi tiết quan trọng hoặc bị nhiễu bởi thông tin không liên quan.

Workflow này giải quyết triệt để vấn đề đó bằng cách tự động hóa toàn bộ quy trình: từ việc quét tin tức mới nhất qua **NewsAPI**, sử dụng sức mạnh của **GPT-5.1** để chọn lọc 5 bài viết chất lượng nhất, dùng **Tavily** để kiểm chứng và làm giàu thêm dữ liệu, và cuối cùng là gửi một bản tin Markdown gọn gàng, chuyên nghiệp trực tiếp vào **Telegram** của các sếp.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian tối đa**: Không cần đọc lướt hàng trăm tin, AI đã lọc sẵn 5 tin "ăn tiền" nhất.
- **Độ chính xác cao**: Kết hợp GPT-5.1 (lý luận) và Tavily (kiểm chứng sự thật) giúp bản tin có độ tin cậy cao, tránh tin giả.
- **Cá nhân hóa tuyệt đối**: Tự do chỉnh sửa chủ đề (topics) và ngôn ngữ (language) để phù hợp với lĩnh vực kinh doanh cụ thể.
- **Hoạt động liên tục**: Chạy tự động theo lịch (ví dụ: 9h sáng Chủ nhật), đảm bảo các sếp luôn cập nhật thông tin đầu tuần mà không cần thao tác gì.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị các credentials sau trong n8n:
1. **OpenAI API Key**: Để sử dụng model GPT-5.1 cho việc chọn lọc và viết nội dung.
2. **NewsAPI Key**: Để truy cập nguồn tin tức (thường dùng query auth).
3. **Tavily API Key**: Để sử dụng công cụ tìm kiếm web chuyên dụng cho AI (fact-checking).
4. **Telegram Bot Token & Chat ID**: Để gửi tin nhắn. Các sếp cần tạo bot qua @BotFather và lấy Chat ID của mình.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ link gốc hoặc copy toàn bộ code JSON và dán vào n8n Editor.
1. Mở n8n, chọn **New Workflow**.
2. Nhấn vào nút **Import from URL** hoặc **Import from File** (nếu có file JSON).
3. Hoặc đơn giản là copy JSON và dán vào màn hình trống, n8n sẽ tự động render các node.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình lại các node quan trọng sau để workflow chạy đúng ý đồ:

*   **Node: `Set topics and language`**
    *   Đây là node cấu hình đầu vào quan trọng nhất.
    *   **Topics**: Điền các chủ đề quan tâm, phân tách bằng dấu phẩy. Ví dụ: `AI, Crypto, Marketing, Vietnam Economy`.
    *   **Language**: Chọn ngôn ngữ đầu ra. Mặc định có thể là `English`, các sếp có thể đổi sang `Vietnamese` nếu muốn bản tin tiếng Việt (lưu ý GPT-5.1 hỗ trợ đa ngôn ngữ rất tốt).

*   **Node: `Schedule Trigger`**
    *   Mặc định chạy vào **Chủ nhật lúc 09:00**.
    *   Các sếp có thể chỉnh lại thời gian và tần suất (ví dụ: hàng ngày, hàng tuần) tùy theo nhu cầu cập nhật thông tin.

*   **Node: `Call NewsAPI`**
    *   Chọn credentials **httpQueryAuth** đã tạo trước đó.
    *   Kiểm tra tham số `query` đảm bảo nó tham chiếu đúng đến biến `topics` từ node `Set topics and language`.
    *   Kiểm tra khoảng thời gian tìm kiếm (mặc định là 7 ngày qua).

*   **Node: `AI Topic Selector` & `GPT-5.1`**
    *   Chọn credentials **openAiApi**.
    *   Đảm bảo model được chọn là `gpt-5.1` (hoặc model mới nhất tương đương).
    *   Node `AI Topic Selector` sẽ dùng AI để đọc danh sách tin từ NewsAPI và chọn ra 5 bài viết không trùng lặp, liên quan nhất.

*   **Node: `Newsletter AI Agent`**
    *   Đây là node trung tâm điều phối. Nó kết nối với:
        *   `GPT-5.1` (để viết tóm tắt).
        *   `Tavily` (tool tìm kiếm để làm giàu thông tin).
        *   `Parser` (để đảm bảo đầu ra đúng định dạng JSON).
    *   Các sếp cần đảm bảo credentials **tavilyApi** được gắn vào node `Tavily` bên trong agent.

*   **Node: `Send a text message`**
    *   Chọn credentials **telegramApi**.
    *   Điền đúng **Chat ID** của các sếp hoặc nhóm Telegram.
    *   Nội dung tin nhắn sẽ được định dạng sẵn bằng Markdown, các sếp có thể chỉnh sửa template hiển thị nếu muốn thêm logo hoặc chữ ký.

#### 3. Kích hoạt ⚡️
1. Nhấn **Execute Workflow** để chạy thử với dữ liệu mẫu.
2. Kiểm tra xem tin nhắn có được gửi đúng vào Telegram không, nội dung có đúng chủ đề và ngôn ngữ không.
3. Nếu ổn, nhấn nút **Active** ở góc trên bên phải để workflow chạy tự động theo lịch.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa ngôn ngữ**: Thử đặt `language` là `Vietnamese` để nhận bản tin tiếng Việt. GPT-5.1 dịch và tóm tắt tiếng Việt rất mượt mà.
- **Gửi đa kênh**: Thay vì chỉ gửi Telegram, các sếp có thể thêm node `Email` hoặc `Slack` sau node `Aggregate` để gửi bản tin đồng thời vào email hoặc kênh làm việc.
- **Lưu trữ lịch sử**: Thêm node `Google Sheets` hoặc `Airtable` sau `Aggregate` để lưu lại toàn bộ nội dung bản tin đã gửi. Điều này giúp các sếp có thể tra cứu lại tin tức cũ.
- **Tùy chỉnh độ dài**: Trong prompt của `Newsletter AI Agent`, các sếp có thể yêu cầu tóm tắt ngắn gọn hơn (ví dụ: 2 câu) hoặc chi tiết hơn (ví dụ: 5 bullet points) tùy sở thích đọc.

### 📌 Kết luận
Workflow này là một ví dụ điển hình cho sức mạnh của việc kết hợp các API tin tức, công cụ tìm kiếm AI và LLM tiên tiến trong n8n. Thay vì để tin tức trôi qua, các sếp giờ đây có một "trợ lý cá nhân" thông minh, luôn sẵn sàng tổng hợp và gửi đến những thông tin giá trị nhất một cách tự động. Hãy import và tùy chỉnh ngay hôm nay để bắt đầu tiết kiệm thời gian và nâng cao hiệu suất làm việc!