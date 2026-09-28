---
title: "🚀 Tự động tạo và kiểm thử mã SQL thông minh với GPT-OpenRouter AI và PostgreSQL Sandbox"
description: "Hướng dẫn xây dựng trợ lý AI trên n8n để viết câu lệnh SQL, tự động sửa lỗi và kiểm thử trực tiếp trên PostgreSQL Sandbox."
slug: "tu-dong-tao-va-kiem-thu-sql-voi-ai-postgresql"
tags: [n8n, automation, ai, postgresql, openrouter, openai, sql-generator]
keywords: [n8n workflow, tao sql bang ai, openrouter ai, postgresql sandbox, tu dong hoa n8n, lap trình sql ai]
---

# 🚀 Tự động tạo và kiểm thử mã SQL thông minh với GPT-OpenRouter AI và PostgreSQL Sandbox

Các sếp làm việc với cơ sở dữ liệu chắc hẳn đã quá quen thuộc với việc viết nhầm câu lệnh SQL, cú pháp bị lỗi khi query dữ liệu phức tạp hoặc mất hàng giờ để debug. Việc viết và kiểm thử SQL thủ công vừa tốn thời gian, vừa tiềm ẩn rủi ro thao tác nhầm trên database thật.

Workflow n8n này sinh ra để giải quyết triệt để vấn đề đó! Đây là một hệ thống trợ lý AI toàn diện giúp nhận yêu cầu bằng ngôn ngữ tự nhiên, tự động sinh mã SQL, kiểm thử trực tiếp trên môi trường **PostgreSQL Sandbox**, tự động bắt lỗi, tự fix và trả về kết quả hoàn chỉnh dưới dạng bảng HTML trực quan. Tất cả diễn ra tự động 100% không cần con người can thiệp thủ công.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Chuyển đổi yêu cầu văn bản thông thường thành câu lệnh SQL chuẩn xác.
- **Tự sửa lỗi thông minh (Auto Error Fixing)**: Nếu câu lệnh SQL chạy bị lỗi trên PostgreSQL Sandbox, AI sẽ tự động phân tích mã lỗi, sửa lại và chạy thử lại cho đến khi thành công (có giới hạn số lần để tránh lặp vô tận).
- **Kiểm thử an toàn**: Thực thi câu lệnh trong môi trường sandbox biệt lập, không sợ ảnh hưởng dữ liệu production.
- **Giao diện trò chuyện tương tác**: Tích hợp chat trigger mượt mà, lưu trữ lịch sử hội thoại đầy đủ.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị sẵn:
- **n8n Instance** (Phiên bản Self-hosted hoặc Cloud).
- **PostgreSQL Database** làm Sandbox để thực thi và test câu lệnh SQL.
- **OpenAI API Key** (hoặc tài khoản **OpenRouter** để dùng các mô hình LLM linh hoạt như GPT-4, Claude, v.v.).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Copy mã JSON của workflow này hoặc tải file JSON gốc từ n8n.
- Mở n8n Editor, chọn **Add workflow** -> **Import from File/Clipboard** và dán nội dung vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các thông số quan trọng sau trong workflow:
- **PostgreSQL Nodes** (`Execute_AI_result`, `get_all_tables`, `SelectAllData`): Chọn đúng thông tin credentials kết nối tới cơ sở dữ liệu PostgreSQL Sandbox của các sếp.
- **OpenAI / OpenRouter Nodes** (`OpenRouter Chat Model`, `OpenAIMainBrain`, `getAssistantsList`, `createOpenAiAssistant`): Điền API Key tương ứng của OpenAI hoặc OpenRouter để AI có đủ "trí tuệ" sinh mã SQL.
- **Node `localVariables`**: Nơi cấu hình các biến cục bộ quan trọng như:
  - `sessionId`: Định danh phiên làm việc (uuidv4).
  - `aiProvider`: Nhà cung cấp AI (OpenAI hoặc OpenRouter).
  - `model`: Tên model LLM sử dụng.
  - `autoErrorFixing`: Bật/tắt tính năng tự động sửa lỗi (`true`/`false`).
- **Node `IsMaxAutoErrorReached` & `AutoErrorFixing`**: Thiết lập giới hạn số lần AI được phép tự sửa lỗi liên tiếp để tránh việc chạy vòng lặp vô hạn khi gặp lỗi cú pháp phức tạp.

#### 3. Kích hoạt ⚡️
- Sử dụng tính năng **Chat Trigger** để test trực tiếp các câu lệnh bằng ngôn ngữ tự nhiên (ví dụ: *"Hãy cho tôi biết top 5 khách hàng mua hàng nhiều nhất tháng này"*).
- Kiểm tra xem AI đã sinh SQL và query dữ liệu thành công chưa.
- Sau khi kiểm thử mượt mà, bấm **Active** để đưa workflow vào vận hành chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối thông báo**: Thêm node Telegram hoặc Slack ở cuối workflow để thông báo cho đội ngũ kỹ thuật khi có truy vấn SQL nặng hoặc lỗi hệ thống không thể tự sửa.
- **Lưu lịch sử truy vấn**: Lưu lại các câu lệnh SQL đã sinh thành công vào một bảng PostgreSQL riêng để làm kho tri thức (Query Knowledge Base) cho các lần hỏi sau.
- **Bảo mật Sandbox**: Luôn đảm bảo tài khoản PostgreSQL kết nối trong workflow chỉ có quyền đọc (`SELECT`) hoặc chỉ có quyền trên database mẫu để tránh bị thực thi các câu lệnh nguy hiểm (`DROP`, `DELETE`).

### 📌 Kết luận
Workflow tích hợp AI và PostgreSQL Sandbox này là một công cụ cực kỳ mạnh mẽ giúp tiết kiệm thời gian viết mã, giảm thiểu sai sót và tối ưu hóa quy trình làm việc với dữ liệu cho các lập trình viên lẫn Data Analyst. Hãy cài đặt ngay hôm nay để trải nghiệm sức mạnh của tự động hóa!