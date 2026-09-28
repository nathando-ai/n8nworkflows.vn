---
title: "🌦️ **Tự Động Hóa Dự Báo Thời Tiết Thực Tế với GPT-4o-mini & MCP Weather Tool – Không Cần Code!**"
description: "Workflow tự động hóa lấy dữ liệu thời tiết từ MCP Weather Tool, phân tích và trả lời câu hỏi thời tiết bằng GPT-4o-mini, giúp các sếp tiết kiệm thời gian và cung cấp thông tin chính xác 24/7."
slug: "tu-dong-hoa-du-bao-thoi-tiet-gpt-4o-mini-mcp"
tags: [n8n, automation, AI, no-code, weather-api, OpenAI, LangChain]
keywords: [n8n workflow thời tiết, tự động hóa dự báo thời tiết, GPT-4o-mini API, MCP Weather Tool, tự động hóa không code]
---

# 🚀 **Tự Động Hóa Dự Báo Thời Tiết Thực Tế với GPT-4o-mini & MCP Weather Tool**

### **Giải pháp nào giúp các sếp:**
- **Tiết kiệm thời gian** khi phải tra cứu thời tiết thủ công hàng ngày?
- **Cung cấp thông tin thời tiết chính xác** từ nhiều nguồn khác nhau?
- **Tự động trả lời câu hỏi thời tiết** cho nhân viên hoặc khách hàng bằng AI?

Workflow này **không cần code**, kết hợp **MCP Weather Tool** (API thời tiết chuyên nghiệp) và **GPT-4o-mini** (mô hình AI tiên tiến của OpenAI) để **tự động hóa việc lấy dữ liệu và phân tích thời tiết** theo yêu cầu của người dùng.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **ổn định 24/7**, các sếp nên **self-host n8n** trên VPS riêng để tránh giới hạn của phiên bản cloud.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** – giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đủ sức mạnh cho AI)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian** – Không phải tra cứu thời tiết thủ công trên nhiều trang web.
✅ **Dữ liệu chính xác** – Sử dụng API MCP Weather Tool (nguồn dữ liệu thời tiết chuyên nghiệp).
✅ **Trả lời tự động** – GPT-4o-mini phân tích và trả lời câu hỏi thời tiết một cách **tự động và cá nhân hóa**.
✅ **Hoạt động 24/7** – Workflow chạy liên tục, không phụ thuộc vào nhân viên.
✅ **Mở rộng dễ dàng** – Có thể kết nối với Slack/Telegram để thông báo thời tiết tự động.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản OpenAI** và **API Key** (để sử dụng GPT-4o-mini).
2. **API Key của MCP Weather Tool** (nếu chưa có, đăng ký tại [MCP Weather](https://www.mcpweather.com/)).
3. **Tài khoản n8n** (self-hosted hoặc cloud).

---
### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/5026) hoặc copy toàn bộ JSON từ đây.
- Mở **n8n Editor** → Nhấn **"Import"** → Chọn file JSON hoặc **paste** JSON vào ô nhập liệu.
- Nhấn **"Import"** để hoàn tất.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **6 node chính**, các sếp cần **cấu hình kỹ** các phần sau:

##### **🔹 Node 1: "When clicking ‘Execute workflow’" (manualTrigger)**
- **Chức năng**: Khởi động workflow khi người dùng nhấn nút **"Execute"**.
- **Lưu ý**: Nếu muốn **tự động hóa hoàn toàn**, các sếp có thể thay thế bằng **Webhook** (ví dụ: từ Slack/Telegram).

##### **🔹 Node 2: "🧪 Enter weather request" (set)**
- **Chức năng**: Nhập **yêu cầu thời tiết** (ví dụ: *"Thời tiết Hà Nội ngày mai"*, *"Nhiệt độ TP.HCM tuần này"*).
- **Lưu ý**:
  - Các sếp có thể **tự động hóa** bằng cách lấy dữ liệu từ **Slack/Telegram** (sử dụng node `httpRequestTool`).
  - Nếu muốn **test nhanh**, nhập thủ công vào ô này.

##### **🔹 Node 3: "MCP - WeatherTrax" (httpRequestTool)**
- **Chức năng**: Gửi yêu cầu API đến **MCP Weather Tool** để lấy dữ liệu thời tiết.
- **Cấu hình cần thiết**:
  - **URL**: `https://api.mcpweather.com/v1/weather`
  - **Headers**:
    ```json
    {
      "Authorization": "Bearer YOUR_MCP_API_KEY",
      "Content-Type": "application/json"
    }
    ```
  - **Body (JSON)**:
    ```json
    {
      "location": "{{ $node["🧪 Enter weather request"].json["location"] }}",
      "date": "{{ $node["🧪 Enter weather request"].json["date"] }}"
    }
    ```
  - **Lưu ý**:
    - Thay thế `YOUR_MCP_API_KEY` bằng **API Key** của MCP Weather Tool.
    - Nếu không có API Key, đăng ký tại [MCP Weather](https://www.mcpweather.com/).

##### **🔹 Node 4: "OpenAI Chat Model" (lmChatOpenAi)**
- **Chức năng**: Sử dụng **GPT-4o-mini** để phân tích và trả lời câu hỏi thời tiết.
- **Cấu hình cần thiết**:
  - **Model**: `gpt-4o-mini` (đã được thiết lập sẵn).
  - **API Key**: Chọn **credentials** `openAiApi` (đã cấu hình trước khi import).
  - **Prompt mẫu** (có thể tùy chỉnh):
    ```
    Bạn là một trợ lý thời tiết thông minh. Hãy phân tích dữ liệu thời tiết từ MCP Weather Tool và trả lời câu hỏi của người dùng một cách chi tiết.
    Dữ liệu đầu vào:
    {{ $node["MCP - WeatherTrax"].json }}
    Câu hỏi: {{ $node["🧪 Enter weather request"].json["question"] }}
    ```
  - **Lưu ý**:
    - Đảm bảo **API Key OpenAI** được nhập đúng trong **Credentials** của n8n.
    - Nếu không có tài khoản OpenAI, đăng ký tại [OpenAI](https://openai.com/).

##### **🔹 Node 5: "AI Agent" (agent)**
- **Chức năng**: Kết nối **OpenAI Chat Model** và **MCP Weather Tool** để xử lý logic tự động.
- **Lưu ý**: Node này **không cần cấu hình thêm**, chỉ cần đảm bảo **2 node trên** hoạt động.

##### **🔹 Node 6: "🧪 View Results Here" (code)**
- **Chức năng**: Hiển thị **kết quả cuối cùng** (câu trả lời thời tiết từ GPT-4o-mini).
- **Lưu ý**:
  - Các sếp có thể **xem kết quả** trong tab **"Execution"** của n8n.
  - Để **hiển thị trên Slack/Telegram**, thêm node `httpRequestTool` để gửi kết quả về chatbot.

---

#### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhập yêu cầu thời tiết (ví dụ: *"Thời tiết Hà Nội ngày mai"*).
   - Chạy workflow và **kiểm tra kết quả** trong node `View Results Here`.
2. **Bật Active**:
   - Nhấn **"Active"** để workflow **chạy tự động** khi được kích hoạt.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết nối với Slack/Telegram**:
   - Sử dụng node `httpRequestTool` để **gửi thông báo thời tiết tự động** khi có yêu cầu từ chatbot.
   - Ví dụ: Khi người dùng gửi tin nhắn *"Thời tiết TP.HCM"*, workflow sẽ trả lời ngay lập tức.

2. **Lưu log dữ liệu**:
   - Thêm node `set` hoặc `httpRequestTool` để **lưu lịch sử tra cứu thời tiết** vào Google Sheets/Notion.

3. **Tùy chỉnh prompt**:
   - Để **câu trả lời chính xác hơn**, các sếp có thể **tùy chỉnh prompt** trong node `OpenAI Chat Model`:
     ```json
     {
       "role": "assistant",
       "content": "Bạn là một trợ lý thời tiết chuyên nghiệp. Hãy trả lời ngắn gọn và chính xác dựa trên dữ liệu từ MCP Weather Tool."
     }
     ```

4. **Sử dụng Webhook thay cho Manual Trigger**:
   - Thay vì nhấn **"Execute"**, các sếp có thể **kích hoạt workflow tự động** khi nhận được yêu cầu từ:
     - **Slack** (sử dụng node `slackWebhook`).
     - **Telegram** (sử dụng node `httpRequestTool`).
     - **Google Calendar** (sự kiện định kỳ).

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp bằng cách **tự động hóa tra cứu và phân tích thời tiết** với sự hỗ trợ của **AI GPT-4o-mini** và **API MCP Weather Tool**. Không cần **viết code**, chỉ cần **cấu hình vài bước**, các sếp đã có một **trợ lý thời tiết 24/7** hoạt động hiệu quả.

**🚀 Hãy áp dụng ngay và tự động hóa việc tra cứu thời tiết cho doanh nghiệp của mình!**

---
**💡 Cần hỗ trợ thêm?**
- **Hỏi đáp trên cộng đồng n8n**: [n8n Community](https://community.n8n.io/)
- **Đăng ký VPS để self-host**: [TinoHost](https://tino.vn/vps-n8n?affid=388) (mã giảm giá **VPSN8N**)