---
title: "🚀 Xây dựng AI Agent tìm kiếm công thức nấu ăn tự động với n8n và API Ninjas"
description: "Hướng dẫn cấu hình AI Agent trên n8n để tự động trả lời tin nhắn, gọi API Ninjas lấy công thức nấu ăn chi tiết và trò chuyện thông minh với người dùng."
slug: "ai-agent-tim-kiem-cong-thuc-nau-an-n8n-api-ninjas"
tags: [n8n, automation, no-code, ai-agent, openai, api-ninjas]
keywords: [n8n workflow, ai agent n8n, api ninjas recipe, tự động hóa chat, openai chat n8n]
---

# 🚀 Xây dựng AI Agent tìm kiếm công thức nấu ăn tự động với n8n và API Ninjas

Việc tìm kiếm công thức nấu ăn hoặc gợi ý món ăn thủ công thường làm mất nhiều thời gian lướt web tìm kiếm giữa hàng tá trang blog hướng dẫn dài dòng. Nếu các sếp muốn xây dựng một trợ lý ảo (AI Agent) chuyên nghiệp có thể ngay lập tức cung cấp nguyên liệu và các bước nấu ăn chuẩn xác chỉ qua một câu lệnh chat, workflow n8n này chính là giải pháp tự động hóa 100% không cần code mà các sếp đang tìm kiếm!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Trợ lý AI thông minh:** Tự động nhận diện yêu cầu tìm món ăn và gọi công cụ (Tool Calling) chính xác.
- **Tiết kiệm thời gian:** Không cần tra cứu thủ công, nhận ngay danh sách nguyên liệu và hướng dẫn từng bước (step-by-step) chỉ trong 3 giây.
- **Giao diện trò chuyện trực quan:** Tích hợp sẵn Chat Trigger để test và tương tác trực tiếp ngay trong n8n.
- **Duy trì ngữ cảnh (Memory):** Ghi nhớ lịch sử trò chuyện ngắn giúp cuộc trò chuyện tự nhiên và mượt mà hơn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (phiên bản hỗ trợ LangChain / AI Nodes).
- **OpenAI API Key:** Tài khoản và API Key để cấu hình cho LLM.
- **API Ninjas Account:** Đăng ký tài khoản miễn phí tại [API Ninjas](https://api-ninjas.com/) để lấy API Key chuyên dụng cho Recipe API.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này và paste trực tiếp vào n8n Editor của mình, hoặc import file JSON tải từ nguồn gốc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 5 nodes chính hoạt động nhịp nhàng, các sếp cần cấu hình kỹ các điểm sau:
- **LLM - OpenAI Chat**: Chọn model OpenAI mong muốn (ví dụ: `gpt-5-mini` hoặc `gpt-4o-mini`) và thêm **OpenAI API Key** của các sếp vào phần credentials.
- **Recipe Tool - Fetch from API Ninjas**: Cấu hình **HTTP Header Auth** bằng cách điền API Key từ trang API Ninjas vào để công cụ có quyền truy xuất dữ liệu món ăn.
- **AI Agent - Route to Tools**: Giữ nguyên system hint mặc định để AI hiểu khi nào cần gọi công cụ lấy công thức nấu ăn.
- **Memory - Recent Messages (Window)** & **Chat Trigger**: Giữ nguyên cấu hình để Agent có thể duy trì bộ nhớ đệm ngắn hạn cho cuộc trò chuyện.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Chat** để mở khung chat thử nghiệm ngay trên n8n.
- Gõ câu lệnh mẫu: *"Find me a pasta recipe"* (Tìm giúp tôi một công thức mỳ ý). Agent sẽ tự động gọi API Ninjas và trả về danh sách nguyên liệu cùng các bước thực hiện gọn gàng.
- Bật công tắc **Active** để đưa AI Agent vào trạng thái hoạt động chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh chat:** Thay thế node Chat Trigger bằng **Telegram Trigger** hoặc **Slack Trigger** để biến AI Agent này thành trợ lý nấu ăn thực thụ trên ứng dụng nhắn tin hàng ngày.
- **Lưu lịch sử tìm kiếm:** Thêm node **Google Sheets** hoặc **Supabase** phía sau Agent để lưu lại danh sách các món ăn mà người dùng đã tra cứu.
- **Tùy biến ngôn ngữ:** Cập nhật system prompt của AI Agent để yêu cầu trả kết quả hoàn toàn bằng tiếng Việt, phù hợp với thói quen người dùng Việt Nam.

### 📌 Kết luận
Với workflow này, các sếp đã sở hữu ngay một trợ lý AI nấu ăn thông minh, tự động hóa hoàn toàn quy trình tra cứu công thức từ bên thứ ba. Hãy triển khai ngay hôm nay để tối ưu hóa trải nghiệm tự động hóa của mình!