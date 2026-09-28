---
title: "🔍 Trợ lý tìm kiếm thông minh với trích dẫn bằng SearchAPI và OpenRouter LLM"
description: "Tự động hóa tìm kiếm thông tin trên web với trích dẫn nguồn, tiết kiệm thời gian và nâng cao hiệu quả công việc bằng công cụ AI mạnh mẽ"
slug: "tro-ly-tim-kiem-thong-minh-voi-trich-dan"
tags: [n8n, automation, no-code, AI, search]
keywords: [n8n workflow, tự động hóa tìm kiếm, AI tìm kiếm, SearchAPI, OpenRouter LLM]
---

# 🔍 Trợ lý tìm kiếm thông minh với trích dẫn bằng SearchAPI và OpenRouter LLM

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp thường phải tìm kiếm thông tin trên nhiều nguồn khác nhau, so sánh kết quả và xác thực nguồn tin. Quá trình này tốn thời gian và dễ gây sai sót. Workflow này sẽ giúp các sếp tự động hóa quy trình tìm kiếm thông tin, lấy trích dẫn nguồn và đưa ra kết quả chính xác chỉ với một câu hỏi.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian tìm kiếm thông tin lên đến 80%
- Đảm bảo tính chính xác và đáng tin cậy của thông tin
- Tự động lấy trích dẫn nguồn từ các trang web uy tín
- Tích hợp dễ dàng với các công cụ khác trong hệ thống
- Hoạt động liên tục 24/7 mà không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản SearchAPI.io (đăng ký tại [searchapi.io](https://www.searchapi.io/))
- Tài khoản OpenRouter (đăng ký tại [openrouter.ai](https://openrouter.ai/))
- API Key từ cả hai dịch vụ trên
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấn vào nút "Import from URL" trên thanh công cụ
3. Dán link sau vào ô nhập liệu: `https://n8n.io/workflows/3829`
4. Nhấn "Import" để tải workflow vào hệ thống

Hoặc bạn cũng có thể:
1. Truy cập vào link workflow: [Web Search Assistant with Citations](https://n8n.io/workflows/3829)
2. Nhấn vào nút "Copy JSON" để sao chép cấu hình
3. Trong n8n Editor, nhấn vào nút "Import from Clipboard"
4. Dán nội dung đã sao chép và nhấn "Import"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **When chat message received (chatTrigger)**
   - Node này sẽ kích hoạt workflow khi nhận được tin nhắn chat
   - Không cần cấu hình gì thêm

2. **Simple Memory (memoryBufferWindow)**
   - Node này lưu trữ lịch sử cuộc trò chuyện
   - Có thể điều chỉnh tham số "k" để xác định số lượng tin nhắn lưu trữ
   - Giá trị mặc định là 5, các sếp có thể tăng lên nếu muốn lưu trữ nhiều tin nhắn hơn

3. **OpenRouter Chat Model (lmChatOpenRouter)**
   - Node này kết nối với OpenRouter để xử lý ngôn ngữ tự nhiên
   - Cần cấu hình credentials cho OpenRouter
   - Tham số "model" đã được đặt sẵn là "deepseek/deepseek-chat:free"
   - Các sếp có thể thay đổi model nếu muốn sử dụng các model khác từ OpenRouter

4. **SearchAPI (CUSTOM.searchApiTool)**
   - Node này sử dụng SearchAPI để tìm kiếm thông tin trên web
   - Cần cấu hình credentials cho SearchAPI
   - Các sếp có thể thay đổi engine tìm kiếm bằng cách chỉnh sửa tham số trong node

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong các node quan trọng, nhấn vào nút "Activate" để kích hoạt workflow
2. Để test workflow, các sếp có thể gửi một tin nhắn chat đến node "When chat message received"
3. Quan sát kết quả trả về từ các node khác trong workflow

### ✍️ Mẹo & gợi ý nâng cao
- Các sếp có thể kết hợp workflow này với Slack hoặc Telegram để nhận thông báo kết quả tìm kiếm
- Có thể thêm node để lưu log các kết quả tìm kiếm vào Google Sheets hoặc cơ sở dữ liệu
- Để nâng cao tính chính xác, các sếp có thể thêm node để lọc và sắp xếp kết quả tìm kiếm
- Workflow có thể được mở rộng để tích hợp với các công cụ khác như Notion, Trello, hoặc các hệ thống CRM

### 📌 Kết luận
Workflow này cung cấp một giải pháp toàn diện để tự động hóa quá trình tìm kiếm thông tin trên web với trích dẫn nguồn. Với khả năng tích hợp mạnh mẽ và tính linh hoạt cao, nó sẽ giúp các sếp tiết kiệm thời gian và nâng cao hiệu quả công việc một cách đáng kể. Hãy thử ngay và trải nghiệm sức mạnh của tự động hóa!