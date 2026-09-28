---
title: "📰 Tự Động Hóa Tin Tức & Phân Phối Đa Kênh với AI Agent (Telegram, Gmail, WhatsApp)"
description: "Workflow n8n sử dụng AI Agent (Gemini + SerpAPI) để tự động tìm kiếm tin tức, tổng hợp nội dung và gửi broadcast qua Telegram, Gmail và WhatsApp theo lịch hoặc theo yêu cầu."
slug: "tu-dong-hoa-tin-tuc-ai-agent-telegram-gmail-whatsapp"
tags: [n8n, automation, ai-agent, serpapi, telegram, whatsapp]
keywords: [n8n workflow, tự động hóa tin tức, ai agent n8n, serpapi integration, broadcast telegram whatsapp]
---

# 📰 Tự Động Hóa Tin Tức & Phân Phối Đa Kênh với AI Agent (Telegram, Gmail, WhatsApp)

Việc theo dõi và tổng hợp tin tức hàng ngày thường tốn rất nhiều thời gian. Bạn phải mở hàng chục tab trình duyệt, đọc lướt qua các trang báo, sao chép nội dung và sau đó đăng lên các kênh khác nhau như Telegram, gửi email cho khách hàng hoặc nhắn tin qua WhatsApp. Quy trình thủ công này không chỉ chậm mà còn dễ bỏ sót thông tin quan trọng và thiếu tính nhất quán trong giọng văn.

Workflow này giải quyết triệt để vấn đề đó bằng cách sử dụng **AI Agent** mạnh mẽ. Thay vì chỉ gọi API đơn thuần, workflow này trang bị cho AI khả năng "tư duy" (Think), "tìm kiếm" (SerpAPI) và "đọc tài liệu" (Google Docs). AI sẽ tự động tìm kiếm chủ đề bạn quan tâm, tổng hợp lại thành bài viết chuyên nghiệp và phân phối đồng thời qua **Telegram**, **Gmail** và **WhatsApp** (qua Rapiwa) mà không cần bạn can thiệp.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, đặc biệt khi có lịch trình (Schedule) và xử lý AI, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian nghiên cứu:** AI tự động tìm kiếm và tổng hợp tin tức từ nguồn thực tế (SerpAPI) thay vì "bịa" thông tin.
- **Phân phối đa kênh tức thì:** Một lần chạy, tin tức được gửi đồng bộ đến Telegram Channel, Email và WhatsApp.
- **Nội dung chất lượng cao:** Sử dụng Google Gemini kết hợp công cụ Think để đảm bảo logic và độ chính xác của bài viết.
- **Linh hoạt kích hoạt:** Có thể chạy tự động theo lịch (Schedule) hoặc kích hoạt thủ công qua Form khi cần.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị các credentials sau:
1. **Google Gemini API Key:** Dùng cho node `Google Gemini Chat Model`.
2. **SerpAPI Key:** Dùng cho node `SerpAPI` để tìm kiếm tin tức trên web.
3. **Telegram Bot Token & Chat ID:** Dùng cho node `Post on Channel` và `Send a text message`.
4. **Gmail Credentials:** Dùng cho node `Send a message` (OAuth2 hoặc App Password).
5. **Rapiwa API Key & Phone Number:** Dùng cho node `Rapiwa` để gửi tin nhắn WhatsApp (nếu có sử dụng).
6. **Google Docs Credentials (Tùy chọn):** Nếu muốn AI tham chiếu thêm tài liệu nội bộ, cần cấp quyền truy cập Google Docs.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n Editor.
2. Chọn **Import from URL** hoặc **Import from File** và dán link/JSON của workflow.
3. Sau khi import, các sếp sẽ thấy một workflow phức tạp với nhiều nhánh: nhánh Schedule, nhánh Form Trigger, và các node AI Agent.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Đây là phần quan trọng nhất. Workflow sử dụng **AI Agent** nên cấu hình prompt và tools rất quan trọng.

**A. Cấu hình AI Agent (Trái tim của workflow)**
- **Node `AI Agent`**:
    - **Model**: Chọn `Google Gemini Chat Model`. Đảm bảo đã điền đúng API Key.
    - **Tools**: Node này sẽ kết nối với các tools bên dưới. Hãy đảm bảo các tools sau được gắn vào:
        - `Think`: Giúp AI suy luận trước khi trả lời.
        - `SerpAPI`: Công cụ tìm kiếm web. **Lưu ý**: Trong node `SerpAPI`, các sếp cần điền `API Key` và cấu hình `Query` (thường là biến động từ prompt).
        - `Get a document in Google Docs`: (Tùy chọn) Nếu dùng, hãy chọn đúng Document ID.
        - `HTTP Request`: (Tùy chọn) Nếu cần gọi API khác.
    - **System Prompt**: Đây là nơi các sếp định hình "nhân cách" của AI. Ví dụ: *"Bạn là một biên tập viên tin tức chuyên nghiệp. Nhiệm vụ của bạn là tìm kiếm tin tức mới nhất về [Chủ đề], tóm tắt ngắn gọn, chính xác và viết lại theo giọng văn thân thiện, phù hợp đăng lên mạng xã hội."*

**B. Cấu hình Kích hoạt (Trigger)**
Workflow có 2 cách kích hoạt:
1. **Tự động theo lịch**:
   - **Node `Schedule`**: Chỉnh thời gian chạy (ví dụ: 8:00 sáng mỗi ngày).
   - **Node `Edit Fields`**: Đặt biến `topic` hoặc `query` mà AI sẽ tìm kiếm. Ví dụ: `"Tin tức công nghệ mới nhất hôm nay"`.
2. **Thủ công qua Form**:
   - **Node `On form submission`**: Tạo form để người dùng nhập chủ đề tin tức muốn tìm.
   - **Node `Edit Fields1`**: Map dữ liệu từ form vào biến cho AI Agent.

**C. Cấu hình Phân phối (Output)**
1. **Telegram**:
   - **Node `Post on Channel`**: Điền `Chat ID` của Channel (thường bắt đầu bằng `-100...`).
   - **Node `Send a text message`**: Điền `Chat ID` của cá nhân hoặc nhóm riêng tư.
   - Đảm bảo Bot đã được thêm vào Channel/Group với quyền Admin.
2. **Gmail**:
   - **Node `Send a message`**: Điền `To` (email nhận), `Subject` và `Message`. Có thể dùng biến `{{ $json.output }}` từ AI Agent để lấy nội dung tin tức.
3. **WhatsApp (Rapiwa)**:
   - **Node `Rapiwa`**: Điền `Phone Number` (số điện thoại nhận tin) và `Message`.
   - Đảm bảo số điện thoại của bạn đã được đăng ký và kích hoạt trên Rapiwa.

**D. Logic Điều khiển**
- **Node `If`**: Kiểm tra xem dữ liệu trả về từ AI có hợp lệ không (ví dụ: không rỗng). Nếu không hợp lệ, nó sẽ đi vào nhánh `Do nothing` hoặc báo lỗi.
- **Node `Wait`**: Chờ một khoảng thời gian ngắn (ví dụ: 5-10 giây) trước khi gửi tin nhắn để tránh bị rate limit từ các API (đặc biệt là Telegram/WhatsApp).

#### 3. Kích hoạt ⚡️
1. **Test Run**:
   - Chạy thử nhánh `Schedule` hoặc `Form Trigger`.
   - Kiểm tra output của node `AI Agent` để xem nội dung tin tức có chính xác và đúng giọng văn không.
   - Kiểm tra từng node gửi tin (Telegram, Gmail, Rapiwa) để đảm bảo tin nhắn đã được gửi thành công.
2. **Bật Active**:
   - Sau khi test ổn định, bật nút **Active** ở góc trên bên phải.
   - Workflow sẽ tự động chạy theo lịch hoặc chờ form submission.

### ✍️ Mẹo & gợi ý nâng cao
- **Cá nhân hóa theo ngành nghề**: Thay đổi System Prompt để AI tập trung vào một ngách cụ thể (ví dụ: "Tin tức bất động sản Hà Nội", "Cập nhật tỷ giá ngoại tệ").
- **Thêm hình ảnh**: Kết hợp thêm node `HTTP Request` để tải ảnh minh họa từ Unsplash hoặc Pexels dựa trên từ khóa, sau đó gửi kèm ảnh trong Telegram/WhatsApp.
- **Lưu trữ lịch sử**: Thêm node `Google Sheets` hoặc `Airtable` để lưu lại toàn bộ tin tức đã gửi, giúp các sếp có cơ sở dữ liệu tin tức theo thời gian.
- **Tương tác hai chiều**: Kết hợp thêm node `Telegram` để nhận phản hồi từ người dùng và dùng AI Agent để trả lời tự động, biến kênh tin tức thành kênh chatbot hỗ trợ.

### 📌 Kết luận
Workflow này là một ví dụ điển hình cho sức mạnh của **AI Agent** trong n8n. Thay vì chỉ tự động hóa các tác vụ lặp đi lặp lại, các sếp đang trao cho AI khả năng "tư duy", "nghiên cứu" và "sáng tạo". Kết hợp với khả năng phân phối đa kênh (Telegram, Email, WhatsApp), đây là công cụ cực kỳ mạnh mẽ để xây dựng thương hiệu cá nhân hoặc doanh nghiệp, giúp các sếp luôn là người cập nhật thông tin nhanh nhất và chuyên nghiệp nhất. Hãy import và tùy chỉnh ngay để trải nghiệm sự khác biệt!