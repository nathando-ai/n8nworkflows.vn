---
title: "🤖 **Tự Động Hóa Agent Tìm Kiếm Web Thông Minh với Tavily + AI Chatbot (N8n)**"
description: "Workflow tự động hóa AI giúp các sếp tìm kiếm thông tin web nhanh chóng, chính xác và cá nhân hóa thông qua Tavily Search + Gemini 3, hoạt động 24/7 mà không cần code."
slug: "tieu-dong-hoa-agent-tim-kiem-web-thong-minh-tavily-gemini"
tags: [n8n, automation, ai-chatbot, market-research, tavily-search]
keywords: [n8n workflow tìm kiếm web, tự động hóa agent AI, Tavily Search + Gemini, chatbot doanh nghiệp, tự động hóa không code]
---

# 🚀 **Agent Tìm Kiếm Web Thông Minh với Tavily + AI Chatbot (N8n)**

### **Giải pháp tự động hóa tìm kiếm thông tin web siêu tốc cho các sếp**
Hãy tưởng tượng một AI agent có thể **tìm kiếm, tổng hợp và trả lời câu hỏi liên quan đến web** chỉ trong vài giây, thay vì các sếp phải mất thời gian ghé thăm nhiều trang web, copy-paste hoặc tra cứu thủ công. **Workflow này** kết hợp **Tavily Search** (một công cụ tìm kiếm web mạnh mẽ) với **Gemini 3** (mô hình AI tiên tiến của Google) để tạo ra một **agent thông minh** hoạt động trong **Chat Hub** của n8n, giúp các sếp:
✅ **Tìm kiếm thông tin web nhanh chóng** (thay vì tra cứu Google thủ công).
✅ **Tự động tổng hợp và trả lời câu hỏi** một cách chính xác.
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.
✅ **Cá nhân hóa** theo nhu cầu của doanh nghiệp (thêm công cụ, hệ thống prompt tùy chỉnh).

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này **chạy ổn định 24/7**, các sếp nên **self-host n8n** trên VPS để đảm bảo tính riêng tư và hiệu suất tối ưu.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đảm bảo tốc độ nhanh cho AI)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần tra cứu thủ công trên Google hoặc các trang web.
- **Trả lời chính xác**: AI tổng hợp thông tin từ nhiều nguồn web khác nhau.
- **Hoạt động liên tục**: Agent sẵn sàng trả lời bất kỳ lúc nào, kể cả ban đêm.
- **Cá nhân hóa**: Thêm các công cụ hoặc hệ thống prompt tùy chỉnh để phù hợp với nhu cầu của doanh nghiệp.
- **Tích hợp với Chat Hub**: Trả lời ngay trong giao diện **n8n Chat Hub** (địa chỉ: `{your-n8n-url}/home/chat`).
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Tavily API** (để tìm kiếm web):
   - Đăng ký tại: [https://tavily.com/](https://tavily.com/)
   - Lấy **API Key** và thêm vào **Credentials** của n8n (tên: `tavilyApi`).
✔ **Tài khoản OpenRouter API** (để sử dụng mô hình Gemini 3):
   - Đăng ký tại: [https://openrouter.ai/](https://openrouter.ai/)
   - Lấy **API Key** và thêm vào **Credentials** của n8n (tên: `openRouterApi`).
✔ **Cài đặt n8n với các nodes cần thiết**:
   - `@n8n/n8n-nodes-langchain` (để sử dụng AI agent và chat).
   - `@tavily/n8n-nodes-tavily` (để tìm kiếm web).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ **file JSON** hoặc **copy/paste JSON** vào **n8n Editor**:
1. **Tải file JSON** từ [liên kết gốc](https://n8n.io/workflows/13271).
2. Trong **n8n Editor**, nhấn **Import** và chọn file JSON.
   **Hoặc**:
   - Copy toàn bộ JSON từ file và dán vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này bao gồm **5 node chính**, các sếp cần **cấu hình kỹ lưỡng** như sau:

##### **A. Node "When chat message received in Chat Hub" (chatTrigger)**
- **Chức năng**: Khởi động workflow khi có tin nhắn trong **Chat Hub**.
- **Lưu ý**:
  - Đảm bảo **Chat Hub** đã được kích hoạt trong n8n (địa chỉ: `{your-n8n-url}/home/chat`).
  - Không cần cấu hình thêm (n8n tự động detect tin nhắn).

##### **B. Node "Search" (tavilyTool)**
- **Chức năng**: Tìm kiếm web bằng Tavily API.
- **Cấu hình bắt buộc**:
  - **Credentials**: Chọn `tavilyApi` (đã thêm API Key trước đó).
  - **Key Parameters**:
    - `model`: `default` (sử dụng mô hình mặc định của Tavily).
    - `query`: **Auto-filled** từ tin nhắn người dùng (không cần chỉnh).
  - **Lưu ý**:
    - Nếu muốn **tùy chỉnh mô hình tìm kiếm**, tham khảo [Tavily Docs](https://docs.tavily.com/).
    - Đảm bảo **API Key** còn hạn và có đủ credit.

##### **C. Node "Chat Model" (lmChatOpenRouter)**
- **Chức năng**: Sử dụng **Gemini 3** để trả lời dựa trên kết quả tìm kiếm.
- **Cấu hình bắt buộc**:
  - **Credentials**: Chọn `openRouterApi` (đã thêm API Key OpenRouter).
  - **Key Parameters**:
    - `model`: `google/gemini-3-flash-preview` (mô hình Gemini 3).
    - `messages`: **Auto-filled** từ kết quả của Tavily + tin nhắn người dùng.
  - **Lưu ý**:
    - Nếu muốn **thay đổi mô hình**, các sếp có thể chọn mô hình khác từ [OpenRouter AI Benchmark](https://n8n.io/ai-benchmark).
    - Đảm bảo **API Key OpenRouter** còn hạn và có đủ credit.

##### **D. Node "Simple Memory" (memoryBufferWindow)**
- **Chức năng**: Giữ lịch sử chat để AI có thể tham khảo trong các cuộc trò chuyện sau.
- **Cấu hình mặc định**:
  - **Window Size**: `10` (lưu 10 tin nhắn gần nhất).
  - **Lưu ý**:
    - Nếu muốn **tùy chỉnh**, các sếp có thể thay đổi `windowSize` để lưu nhiều hoặc ít tin nhắn hơn.

##### **E. Node "AI Agent" (agent)**
- **Chức năng**: Quản lý toàn bộ logic của agent (tìm kiếm + trả lời).
- **Cấu hình mặc định**:
  - **System Prompt**: Có sẵn (các sếp có thể **tùy chỉnh** để phù hợp với nhu cầu).
  - **Lưu ý**:
    - Nếu muốn **thêm công cụ khác**, các sếp có thể mở rộng trong **System Prompt** hoặc thêm node mới.
    - Ví dụ: Thêm **Slack Notification** để báo cáo kết quả.

#### **3. Kích hoạt ⚡️**
1. **Test Run** với một tin nhắn mẫu:
   - Gửi tin nhắn vào **Chat Hub** (ví dụ: *"Tìm kiếm thông tin về thị trường AI Việt Nam năm 2024"*).
   - Kiểm tra kết quả trả lời của AI.
2. **Bật Active workflow**:
   - Nhấn **Active** trên tab workflow.

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::note[CÁCH THÊM CÔNG CỤ KHÁC]
Các sếp có thể **mở rộng agent** bằng cách:
- **Thêm Slack/Telegram Notification**: Gửi kết quả tìm kiếm vào kênh Slack/Telegram.
- **Lưu log vào Google Sheets**: Để theo dõi lịch sử tìm kiếm.
- **Tùy chỉnh System Prompt**: Ví dụ:
  ```json
  "system": "Bạn là một trợ lý tìm kiếm thông minh. Trả lời ngắn gọn và chính xác dựa trên kết quả từ Tavily. Nếu không tìm thấy thông tin, hãy nói 'Không tìm thấy kết quả'."
  ```
- **Kết hợp với Zapier/Make**: Nếu cần tự động hóa thêm các tác vụ bên ngoài.
:::

:::tip[CÁCH TÙY CHỈNH MÔ HÌNH AI]
Nếu muốn **thay đổi mô hình AI** (không phải Gemini 3), các sếp có thể:
1. Đổi `model` trong **Chat Model** (node `lmChatOpenRouter`).
2. Ví dụ:
   ```json
   "model": "mistral/mistral-7b"
   ```
3. **Kiểm tra mô hình mới** trên [OpenRouter AI Benchmark](https://n8n.io/ai-benchmark).
:::

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn **tự động hóa tìm kiếm web thông minh** mà không cần viết code. Với **Tavily Search + Gemini 3**, agent sẽ **tìm kiếm, tổng hợp và trả lời** một cách nhanh chóng và chính xác, giúp tiết kiệm thời gian và nâng cao hiệu suất làm việc.

**🚀 Hãy áp dụng ngay và trải nghiệm sự thay đổi!**
- **Import workflow** và **cấu hình API Key**.
- **Test với các câu hỏi** và theo dõi kết quả.
- **Mở rộng** bằng cách thêm các công cụ hoặc tùy chỉnh prompt.

Nếu có bất kỳ câu hỏi nào, các sếp có thể **trả lời trong Chat Hub** hoặc liên hệ với cộng đồng n8n tại [n8n Community](https://community.n8n.io/). **Chúc các sếp thành công!** 💪