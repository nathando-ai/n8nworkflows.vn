---
title: "🚀 Tự động tạo câu lệnh SQL từ cấu trúc Database bằng AI Agent trong n8n"
description: "Hướng dẫn xây dựng hệ thống chatbot AI kết nối MySQL, tự động đọc Schema và sinh câu lệnh SQL chính xác để truy vấn dữ liệu nhanh chóng mà không cần viết code thủ công."
slug: "tao-sql-query-tu-schema-database-bang-ai-trong-n8n"
tags: [n8n, automation, ai-agent, mysql, openai, langchain]
keywords: [n8n workflow, tạo sql bằng ai, ai agent mysql, text to sql n8n, chat với database mysql]
---

# 🚀 Tự động tạo câu lệnh SQL từ cấu trúc Database bằng AI Agent trong n8n

Các sếp làm kỹ sư dữ liệu, DevOps hay phát triển phần mềm chắc chắn đã quen thuộc với việc viết câu lệnh SQL thủ công mỗi khi có yêu cầu truy vấn dữ liệu từ đội ngũ kinh doanh hay vận hành. Việc này vừa tốn thời gian, vừa dễ gây nhầm lẫn nếu cấu trúc bảng (schema) phức tạp.

Giải pháp là đây! Workflow n8n này sẽ giúp các sếp xây dựng một **AI Chatbot thông minh** có khả năng "đọc hiểu" cấu trúc database MySQL, trò chuyện trực tiếp với người dùng, tự động sinh ra câu lệnh SQL chính xác, thực thi và trả về kết quả ngay lập tức ngay trong khung chat. Tất cả tự động hóa 100%!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tốc độ vượt trội:** Chatbot đọc schema từ file cache cục bộ thay vì query trực tiếp database từ xa mỗi lần hỏi, giúp phản hồi cực nhanh.
- **Bảo mật dữ liệu:** AI Agent chỉ nhìn thấy cấu trúc bảng (schema) chứ không tiếp cận trực tiếp dữ liệu thô, đảm bảo an toàn thông tin.
- **Linh hoạt thông minh:** Tự nhận diện khi nào cần sinh câu lệnh SQL (ví dụ: *"Lấy danh sách khách hàng Đức"*) và khi nào chỉ cần trả lời thông thường (ví dụ: *"Database có những bảng nào?"*).
- **Trải nghiệm mượt mà:** Kết hợp Chat Trigger, tự động kiểm tra câu lệnh, chạy truy vấn MySQL và định dạng kết quả trả về giao diện chat rõ ràng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (phiên bản hỗ trợ LangChain Nodes).
- **OpenAI API Key:** Sử dụng mô hình `gpt-4o` cho AI Agent.
- **MySQL Database:** Một database MySQL (có thể dùng bản miễn phí như db4free.net hoặc test với mẫu dữ liệu Chinook).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow này từ nguồn gốc hoặc copy trực tiếp.
- Trong giao diện n8n Editor, chọn **Add workflow** -> **Import from File** (hoặc dán trực tiếp JSON vào màn hình làm việc).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống vận hành trơn tru, các sếp cần cấu hình chính xác các node sau:

- **OpenAI Chat Model:** Chọn hoặc thêm mới thông tin `credentials` cho OpenAI, đảm bảo model được cấu hình là `gpt-4o`.
- **List all tables in a database**, **Extract database schema**, và **Run SQL query**: Các node này đều cần kết nối với database MySQL của các sếp. Hãy cấu hình `credentials` cho MySQL (Host, Database, User, Password).
- **Chạy khởi tạo lần đầu (Run this part only once):** 
  - Theo ghi chú trên canvas, các sếp cần chạy phần lấy danh sách bảng, trích xuất schema, chuyển đổi sang JSON và lưu vào file cục bộ (`./chinook_mysql.json`) **ít nhất một lần** trước khi dùng chat.
- **AI Agent & System Prompt:** Node này sử dụng LangChain Agent kết hợp với `Window Buffer Memory` để ghi nhớ lịch sử hội thoại, giúp người dùng tra cứu ngữ cảnh liên tục.

#### 3. Kích hoạt ⚡️
- Nhấn **Test workflow** và thử gửi một câu hỏi qua **Chat Trigger** (ví dụ: *"Liệt kê tất cả các bảng"* hoặc *"Cho tôi danh sách khách hàng đến từ Đức"*).
- Kiểm tra kết quả trả về ở khung chat và các node xử lý phía sau.
- Nếu mọi thứ chạy mượt mà, gạt công tắc sang **Active** để đưa vào sử dụng chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh liên lạc:** Thay vì dùng Chat Trigger mặc định của n8n, các sếp có thể đổi thành **Telegram Trigger** hoặc **Slack Trigger** để đội ngũ sales/ops có thể tra cứu dữ liệu trực tiếp qua chatwork của công ty.
- **Lưu lịch sử truy vấn:** Thêm một node Google Sheets hoặc Airtable phía sau để log lại các câu hỏi và câu lệnh SQL mà AI tạo ra, giúp đội ngũ kỹ thuật tối ưu hóa index và performance của database sau này.
- **Bổ sung bảo mật:** Thêm bước kiểm tra (IF node) để ngăn chặn các câu lệnh SQL độc hại (như DROP, DELETE, TRUNCATE) nhằm bảo vệ database tuyệt đối.

### 📌 Kết luận
Workflow tích hợp AI này là trợ thủ đắc lực giúp thu hẹp khoảng cách giữa dữ liệu kỹ thuật phức tạp và nhu cầu khai thác thông tin hàng ngày của doanh nghiệp. Hãy thiết lập ngay hôm nay để tối ưu hóa hiệu suất làm việc cho đội ngũ của các sếp!