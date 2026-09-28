---
title: "🚀 Tạo AI Agent đầu tiên – Kết hợp Google Gemini, SerpAPI & Bộ nhớ ngắn hạn trong n8n"
description: "Hướng dẫn chi tiết cách xây dựng một AI Agent tự động trả lời câu hỏi, tìm kiếm web, tính toán và ghi nhớ cuộc trò chuyện mà không cần viết code."
slug: "tao-ai-agent-dau-tien-google-gemini-serpapi-memory"
tags: [n8n, automation, no-code, AI Agent, Google Gemini, SerpAPI, Calculator, Think, Memory]
keywords: [n8n workflow, tự động hóa, AI Agent, Google Gemini, SerpAPI, chatbot, bộ nhớ ngắn hạn]
---

# 🚀 Tạo AI Agent đầu tiên – Kết hợp Google Gemini, SerpAPI & Bộ nhớ ngắn hạn trong n8n

Bạn từng cảm thấy mệt mỏi khi phải trả lời lại các câu hỏi lặp đi lặp lại, tra cứu thông tin trên Google hay thực hiện các phép tính đơn giản trong quá trình làm việc? Với workflow **AI Agent** này, bạn sẽ có một trợ lý ảo thông minh có thể:

- Trả lời câu hỏi tự nhiên bằng mô hình **Google Gemini** (miễn phí).  
- Tìm kiếm thông tin thời gian thực qua **SerpAPI** để luôn cung cấp dữ liệu mới nhất.  
- Thực hiện phép tính bằng công cụ **Calculator** nội built.  
- Suy nghĩ step‑by‑step bằng công cụ **Think** trước khi đưa ra câu trả lời.  
- Ghi nhớ 5 lượt trò chuyện gần nhất nhờ **Memory Buffer Window**, giúp cuộc trò chuyện liên mạch và bối cảnh nhất quán.

Tất cả được xây dựng trên nền tảng **n8n** – không cần viết một dòng code nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Agent tự động xử lý truy vấn, tìm kiếm và tính toán thay bạn.  
- **Chính xác & cập nhật**: Nhờ SerpAPI, thông tin luôn mới nhất; Gemini cung cấp câu trả lời chất lượng cao.  
- **Cá nhân hóa & bối cảnh**: Bộ nhớ ngắn hạn ghi lại 5 lượt trò chuyện gần nhất, giúp Agent “nhớ” cuộc hội thoại.  
- **Hoạt động liên tục**: Sau khi kích hoạt, workflow sẵn sàng phản hồi ngay khi có tin nhắn mới.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản SerpAPI** – lấy API Key tại [serpapi.com](https://serpapi.com/).  
- **Tài khoản Google Gemini** – lấy API Key từ Google AI Studio (miễn phí cho mức sử dụng cơ bản).  
- **n8n instance** (self‑hosted hoặc n8n.cloud) đã được cài đặt và có quyền tạo workflow.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Sao chép toàn bộ JSON workflow từ trang gốc (https://n8n.io/workflows/4941).  
2. Trong n8n Editor, nhấn **Import** → **Upload file** hoặc **Paste JSON** → dán JSON vừa copy → **Import**.  
3. Workflow sẽ xuất hiện với tên **🤖 Build Your First AI Agent – Powered by Google Gemini with Memory**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node (tên trên canvas) | Loại node | Cấu hình bắt buộc |
|------------------------|-----------|-------------------|
| **When chat message received** | `chatTrigger` | - Chọn **Chat Trigger** (nếu chưa có, tạo mới). <br> - Đặt **Path** (ví dụ: `/webhook/chat-agent`) – đây là endpoint mà bạn sẽ gửi tin nhắn tới. |
| **AI Agent** | `agent` | - **Agent Type**: `Conversational Agent`. <br> - **Tools**: Kéo thả các tool sau vào danh sách: `Think`, `SerpAPI`, `Calculator`. <br> - **Language Model**: Chọn **Google Gemini Chat Model** (node dưới). <br> - **Memory**: Chọn **Simple Memory** (node dưới). |
| **Think** | `toolThink` | - Không cần cấu hình thêm; chỉ cần đảm bảo node được kết nối vào AI Agent như một tool. |
| **SerpAPI** | `toolSerpApi` | - **Credentials**: Chọn hoặc tạo credential **serpApi** và dán API Key lấy từ SerpAPI. <br> - **Parameter**: Để mặc định (q) hoặc tùy chỉnh nếu muốn giới hạn kết quả. |
| **Google Gemini Chat Model** | `lmChatGoogleGemini` | - **Credentials**: Chọn hoặc tạo credential **googlePalmApi** và dán API Key từ Google AI Studio. <br> - **Model**: Chọn `gemini-pro` (hoặc model miễn phí mà bạn có quyền truy cập). <br> - **Temperature**: Điều chỉnh (0.7 là giá trị tốt cho sự sáng tạo cân bằng). |
| **Calculator** | `toolCalculator` | - Không cần cấu hình thêm; chỉ cần đảm bảo node được kết nối vào AI Agent như một tool. |
| **Simple Memory** | `memoryBufferWindow` | - **Window Size**: Đặt `5` (ghi nhớ 5 lượt trò chuyện gần nhất). <br> - **Memory Key**: Để mặc định `chatHistory` hoặc đổi tên nếu muốn. |

> **Lưu ý quan trọng**: Sau khi chọn credentials cho mỗi node, nhấn **Save** rồi **Execute Node** để kiểm tra kết nối API thành công trước khi tiếp tục.

#### 3. Kích hoạt ⚡️
1. Nhấn **Execute Workflow** và gửi một tin nhắn test qua URL webhook (ví dụ: sử dụng curl, Postman hoặc trực tiếp trong n8n Chat Trigger nếu được bật).  
2. Kiểm tra phản hồi: Agent nên suy nghĩ (Think), tìm kiếm (SerpAPI nếu cần), tính toán (Calculator nếu có biểu thức toán) và trả lời dựa trên Gemini.  
3. Nếu mọi thứ ổn, chuyển toggle **Active** sang **ON** để workflow bắt đầu lắng nghe tin nhắn real‑time.  

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo Slack/Telegram**: Thêm node **Slack** hoặc **Telegram** sau AI Agent để gửi bản tin nhắn trả lời vào kênh team, giúp mọi người theo dõi tương tác.  
- **Lưu log trò chuyện**: Kết hợp node **Google Sheets** hoặc **Airtable** để lưu mỗi lượt chat (câu hỏi, câu trả lời, thời gian) để phân tích sau này.  
- **Báo cáo định kỳ**: Sử dụng node **Cron** để kích hoạt workflow mỗi sáng, tổng hợp số lượng câu hỏi đã xử lý và gửi email báo cáo qua node **Email Send**.  
- **Mở rộng công cụ**: Thêm tool **HTTP Request** để gọi API nội bộ (CRM, ERP) hoặc **MongoDB** để truy xuất dữ liệu khách hàng cá nhân hóa hơn.  
- **Tuning mô hình**: Thay đổi **Temperature** hoặc **Top P** trên node Gemini để cân bằng giữa sự sáng tạo và độ chính xác tùy theo trường hợp sử dụng (hỗ trợ khách hàng vs. tạo nội dung sáng tạo).  

### 📌 Kết luận
Workflow **AI Agent** này là bước khởi đầu hoàn hảo để các sếp tự động hóa tương tác với khách hàng, nội bộ hoặc даже bản thân – không cần viết code, chỉ cần cấu hình một few credentials và kéo thả các node. Hãy import ngay, thử nghiệm và thấy sự khác biệt trong thời gian phản hồi và chất lượng câu trả lời. Nếu cần hỗ trợ tùy chỉnh hoặc mở rộng thêm功能, hãy liên hệ với **DigiMetaLab** qua email **digimetalab@gmail.com** hoặc Telegram [@digimetalab](https://t.me/digimetalab) để được tư vấn miễn phí.

Chúc các sếp thành công với cuộc hành trình tự động hóa! 🚀