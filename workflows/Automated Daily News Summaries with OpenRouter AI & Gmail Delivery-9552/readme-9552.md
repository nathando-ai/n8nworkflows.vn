---
title: "📰 Tự Động Hóa Tin Tức Hàng Ngày: AI Tổng Hợp & Gửi Gmail"
description: "Workflow n8n tự động tìm kiếm tin tức nóng hổi qua Tavily, sử dụng AI (OpenRouter) để tóm tắt chuyên sâu và gửi email định dạng HTML đẹp mắt đến hộp thư của bạn mỗi ngày."
slug: "tu-dong-hoa-tin-tuc-ai-gui-gmail"
tags: [n8n, automation, ai-news, tavily, openrouter, gmail]
keywords: [n8n workflow, tin tức ai, tự động hóa báo cáo, tavily api, openrouter, gmail automation]
---

# 📰 Tự Động Hóa Tin Tức Hàng Ngày: AI Tổng Hợp & Gửi Gmail

Mỗi sáng, các sếp có bao nhiêu thời gian để lướt qua hàng chục trang web, mạng xã hội và báo điện tử để cập nhật những tin tức quan trọng nhất về công nghệ, kinh doanh hay sự kiện thế giới? Việc này không chỉ tốn thời gian mà còn dễ bỏ sót thông tin then chốt do quá tải dữ liệu.

Workflow **"Automated Daily News Summaries with OpenRouter AI & Gmail Delivery"** chính là giải pháp "thư ký AI" hoàn hảo. Nó tự động chạy theo lịch trình, sử dụng sức mạnh của AI Agent kết hợp với API tìm kiếm thực tế (Tavily) để thu thập tin tức, tóm tắt lại một cách súc tích, có cấu trúc và gửi thẳng vào hộp thư Gmail của bạn dưới dạng email HTML chuyên nghiệp. Không cần code, không cần lo lắng, chỉ cần ngồi vào bàn làm việc và đọc báo cáo đã được "nấu" sẵn.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian đáng kể:** Biến quá trình cập nhật tin tức từ 30-60 phút mỗi ngày xuống còn 5 phút đọc email.
- **Thông tin chính xác & Cập nhật:** Sử dụng Tavily API để lấy tin tức thời gian thực, tránh tin giả hoặc tin cũ.
- **Cá nhân hóa nội dung:** AI Agent có thể được cấu hình để tập trung vào các chủ đề cụ thể (Tech, Business, World Events) theo nhu cầu của sếp.
- **Trình bày chuyên nghiệp:** Email được định dạng HTML đẹp mắt, dễ đọc trên cả máy tính và điện thoại.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị các tài khoản và API keys sau:
1. **Tài khoản n8n:** Đã cài đặt và chạy (Cloud hoặc Self-hosted).
2. **OpenRouter API Key:** Để sử dụng các mô hình AI (LLM) cho việc tóm tắt và phân tích.
3. **Tavily API Key:** Để truy cập API tìm kiếm tin tức chuyên dụng cho AI.
4. **Tài khoản Gmail:** Đã cấp quyền OAuth2 cho n8n để gửi email.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n Editor.
2. Chọn **Import from File** hoặc **Import from URL**.
3. Tải file JSON của workflow (hoặc copy link gốc từ n8n.io/workflows/9552) và dán vào.
4. Workflow sẽ hiện ra với 8 nodes chính.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Đây là phần quan trọng nhất. Các sếp cần click vào từng node và cấu hình như sau:

*   **Node: Schedule Trigger**
    *   Chọn thời gian chạy mong muốn (ví dụ: 07:00 sáng mỗi ngày).
    *   *Mẹo:* Chọn múi giờ phù hợp với địa điểm làm việc của sếp.

*   **Node: OpenRouter Chat Model**
    *   Chọn **Credentials** -> Tạo mới hoặc chọn **OpenRouter API** đã có.
    *   Chọn **Model**: Khuyến nghị dùng các model mạnh về reasoning như `anthropic/claude-3-sonnet` hoặc `openai/gpt-4o` để đảm bảo chất lượng tóm tắt.

*   **Node: Tavily News Search**
    *   Trong phần **Headers** hoặc **Body**, tìm trường `api_key`.
    *   Dán **Tavily API Key** của sếp vào đây.
    *   Kiểm tra URL và Method (thường là POST) đã đúng theo tài liệu Tavily chưa.

*   **Node: AI News Agent**
    *   Đây là "bộ não" của workflow.
    *   Kiểm tra **System Prompt**: Đảm bảo prompt yêu cầu AI tìm kiếm các chủ đề cụ thể (Tech, Business, World) và định dạng output theo JSON schema đã định nghĩa.
    *   Đảm bảo node này đã kết nối với **OpenRouter Chat Model**, **Tavily News Search** và **News Output Parser**.

*   **Node: News Output Parser**
    *   Kiểm tra **JSON Schema**: Đảm bảo cấu trúc dữ liệu đầu ra (ví dụ: mảng tin tức với tiêu đề, tóm tắt, link nguồn) khớp với logic xử lý ở node tiếp theo.

*   **Node: Format for Gmail**
    *   Đây là node Code (JavaScript).
    *   Sếp có thể chỉnh sửa HTML/CSS trong code này để thay đổi màu sắc, font chữ, layout email cho phù hợp với thương hiệu cá nhân hoặc công ty.

*   **Node: Send a message**
    *   Chọn **Credentials** -> **Gmail OAuth2**.
    *   **To**: Điền địa chỉ email nhận tin tức của sếp.
    *   **Subject**: Có thể để động (ví dụ: `Tin tức AI & Tech - {{ $now.format('DD/MM/YYYY') }}`).
    *   **Message**: Chọn **HTML** và map dữ liệu từ node `Format for Gmail`.

#### 3. Kích hoạt ⚡️
1. Click **Execute Workflow** để chạy thử với dữ liệu mẫu.
2. Kiểm tra hộp thư Gmail xem email có đến đúng, định dạng có đẹp không, nội dung có chính xác không.
3. Nếu ổn, bật công tắc **Active** ở góc trên bên phải để workflow tự động chạy hàng ngày.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa dạng hóa nguồn tin:** Thay vì chỉ dùng Tavily, sếp có thể thêm các tool HTTP khác để scrape RSS feed từ các trang báo uy tín (VnExpress, BBC, TechCrunch) và đưa vào AI Agent để tổng hợp đa chiều.
- **Gửi qua Telegram/Slack:** Thay vì (hoặc song song với) Gmail, sếp có thể thêm node Telegram hoặc Slack để nhận tin tức ngay trên điện thoại, tiện lợi hơn khi di chuyển.
- **Lưu trữ lịch sử:** Thêm node Google Sheets hoặc Database để lưu lại các tin tức đã gửi. Điều này giúp sếp có thể tra cứu lại tin tức cũ hoặc phân tích xu hướng tin tức theo thời gian.
- **Cá nhân hóa theo ngành:** Chỉnh sửa Prompt trong AI Agent để tập trung vào một ngành cụ thể (ví dụ: "Chỉ tập trung vào tin tức về AI trong y tế" hoặc "Tin tức về thị trường chứng khoán Mỹ").

### 📌 Kết luận
Workflow này là một ví dụ điển hình cho sức mạnh của n8n khi kết hợp với AI và các API bên thứ ba. Thay vì để AI chỉ là công cụ chat, sếp đã biến nó thành một quy trình làm việc tự động, chủ động và có giá trị thực tiễn cao. Hãy import ngay, cấu hình 5 phút và bắt đầu nhận "báo cáo tin tức" cá nhân hóa mỗi sáng. Chúc các sếp làm việc hiệu quả!