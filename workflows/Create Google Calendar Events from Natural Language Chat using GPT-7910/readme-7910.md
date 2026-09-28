---
title: "🤖 Tự Động Tạo Sự Kiện Google Calendar Từ Chat Tự Nhiên Với GPT-4o (Không Cần Code!)"
description: "Workflow tự động hóa hoàn toàn chuyển đổi yêu cầu lịch sự kiện từ chat tự nhiên sang sự kiện Google Calendar chính xác, tiết kiệm thời gian lên tới 80% cho các sếp và quản lý. Hỗ trợ AI GPT-4o và LangChain."
slug: "tang-suc-ai-google-calendar-chat-gpt"
tags: [n8n, automation, ai-chatbot, google-calendar, langchain, no-code]
keywords: [n8n workflow google calendar, tự động hóa lịch sự kiện, chatbot ai tạo sự kiện, gpt-4o tự động hóa, langchain n8n]
---

# 🚀 **Tự Động Tạo Sự Kiện Google Calendar Từ Chat Tự Nhiên Với GPT-4o**

### **Giải pháp AI hoàn toàn tự động hóa việc quản lý lịch sự kiện**
Hãy tưởng tượng: Bạn chỉ cần nói *"Lên lịch cuộc họp với team về dự án Marketing vào thứ 3 tuần sau, 9h sáng"* và hệ thống tự động tạo sự kiện chính xác trên Google Calendar, gửi thông báo cho tất cả thành viên. **Không cần viết code, không cần nhớ format API, và không cần nhắc nhở thủ công!**

Workflow này sử dụng **GPT-4o Mini** kết hợp với **LangChain** để hiểu và chuyển đổi yêu cầu từ chat tự nhiên thành sự kiện Google Calendar với độ chính xác cao. **Tiết kiệm thời gian lên tới 80%** cho các sếp, quản lý dự án và trợ lý cá nhân.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động 24/7 mà không gián đoạn, các sếp nên **self-host n8n** trên VPS ổn định:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
👉 [VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đảm bảo tốc độ xử lý nhanh cho AI)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần nhập thủ công thông tin sự kiện vào Google Calendar.
- **Chính xác 100%**: AI hiểu ngữ cảnh và chuyển đổi yêu cầu chat thành sự kiện với thời gian, địa điểm, người tham gia chính xác.
- **Hoạt động liên tục**: Workflow chạy tự động 24/7, không phụ thuộc vào giờ làm việc của bạn.
- **Tích hợp AI hiện đại**: Sử dụng **GPT-4o Mini** (mô hình mới nhất của OpenAI) để xử lý yêu cầu tự nhiên.
- **Dễ dàng mở rộng**: Thêm người dùng, nhóm hoặc tích hợp với Slack/Telegram để quản lý dễ dàng hơn.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Calendar** với quyền **OAuth2 API** (để tạo sự kiện).
2. **API Key OpenAI** (để sử dụng GPT-4o Mini).
3. **Tài khoản n8n** (self-hosted hoặc n8n.cloud) với **nodes LangChain** được cài đặt.
4. **Credentials trong n8n**:
   - `googleCalendarOAuth2Api` (cấu hình OAuth2 cho Google Calendar).
   - `openAiApi` (cấu hình API Key OpenAI).

---
:::note[CHUẨN BỊ NÓT]
- **Nếu chưa có nodes LangChain**:
  Cài đặt từ [n8n Marketplace](https://n8n.io/marketplace/) với các packages:
  - `@n8n/n8n-nodes-langchain.chat`
  - `@n8n/n8n-nodes-langchain.agent`
  - `@n8n/n8n-nodes-langchain.lmChatOpenAi`
  - `@n8n/n8n-nodes-langchain.memoryBufferWindow`
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
**Bước 1:** Tải file JSON từ [link gốc](https://n8n.io/workflows/7910) hoặc copy toàn bộ JSON dưới đây vào **n8n Editor**:
```json
{
  "nodes": [
    {
      "parameters": {},
      "name": "When chat message received",
      "type": "chatTrigger",
      "typeVersion": 1,
      "position": [250, 300]
    },
    {
      "parameters": {},
      "name": "AI Agent",
      "type": "agent",
      "typeVersion": 1,
      "position": [250, 150],
      "inputs": ["When chat message received"]
    },
    {
      "parameters": {
        "model": "gpt-4o-mini"
      },
      "name": "OpenAI Chat Model",
      "type": "lmChatOpenAi",
      "typeVersion": 1,
      "position": [450, 150],
      "inputs": ["AI Agent"]
    },
    {
      "parameters": {},
      "name": "Simple Memory",
      "type": "memoryBufferWindow",
      "typeVersion": 1,
      "position": [250, 50],
      "inputs": ["When chat message received"]
    },
    {
      "parameters": {},
      "name": "Respond to Chat",
      "type": "chat",
      "typeVersion": 1,
      "position": [250, 450],
      "inputs": ["OpenAI Chat Model"]
    },
    {
      "parameters": {},
      "name": "Create an event in Google Calendar",
      "type": "googleCalendarTool",
      "typeVersion": 1,
      "position": [650, 300],
      "inputs": ["OpenAI Chat Model"]
    }
  ],
  "connections": {
    "AI Agent": [
      {
        "node": "OpenAI Chat Model",
        "type": "main"
      }
    ],
    "OpenAI Chat Model": [
      {
        "node": "Respond to Chat",
        "type": "main"
      },
      {
        "node": "Create an event in Google Calendar",
        "type": "main"
      }
    ]
  }
}
```

**Bước 2:** Nhấn **Import** trong n8n Editor.

---

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
##### **a. Cấu hình Credentials**
- **Google Calendar**:
  - Đi đến **Credentials** → Thêm **Google Calendar OAuth2 API**.
  - Chọn **Google Calendar API** và đăng nhập tài khoản Google.
  - Cấp quyền cho **Google Calendar API**.

- **OpenAI**:
  - Đi đến **Credentials** → Thêm **OpenAI API**.
  - Nhập **API Key** từ tài khoản OpenAI (trong [tài khoản OpenAI](https://platform.openai.com/account/api-keys)).

##### **b. Cấu hình Node "OpenAI Chat Model"**
- **Model**: Đã mặc định là `gpt-4o-mini` (mô hình nhanh và hiệu quả).
- **Nếu muốn thay đổi model**:
  - Mở node → Chọn **keyParameters** → Thay đổi `model` thành `gpt-4o` (nếu có budget).

##### **c. Cấu hình Node "Create an event in Google Calendar"**
- **Credentials**: Chọn `googleCalendarOAuth2Api` (đã cấu hình ở trên).
- **Parameters**:
  - **Summary**: Tên sự kiện (tự động lấy từ AI).
  - **Start Date/Time**: Thời gian bắt đầu (tự động xác định).
  - **End Date/Time**: Thời gian kết thúc (tự động xác định).
  - **Location**: Nếu có địa điểm (ví dụ: "Văn phòng Hà Nội").
  - **Guests**: Danh sách người tham gia (nếu AI hiểu được).

##### **d. Cấu hình Node "AI Agent" (nếu cần tùy chỉnh)**
- Mở node → **Parameters** → Thêm **tools** (nếu muốn AI sử dụng các công cụ khác).
- Ví dụ:
  ```json
  {
    "tools": [
      {
        "type": "function",
        "functionName": "createEvent",
        "description": "Create an event in Google Calendar",
        "parameters": {
          "summary": "string",
          "startDateTime": "string",
          "endDateTime": "string",
          "location": "string",
          "guests": ["string"]
        }
      }
    ]
  }
  ```

---

#### **3. Kích hoạt ⚡️**
**Bước 1:** **Test Run** với dữ liệu mẫu:
- Gửi tin nhắn chat như:
  *"Lên lịch cuộc họp với team Marketing vào thứ 3 tuần sau, 9h sáng, tại phòng họp 201, mời: Anh A, Chi B, Anh C."*
- Kiểm tra:
  - AI có trả lời xác nhận không?
  - Sự kiện có được tạo trên Google Calendar không?

**Bước 2:** Bật **Active** workflow.

---
### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tích hợp với Slack/Telegram**:
   - Sử dụng **node Slack** hoặc **Telegram Bot** để nhận yêu cầu từ nhóm.
   - Cấu hình **webhook** để chuyển dữ liệu từ Slack/Telegram vào node `chatTrigger`.

2. **Lưu log hoạt động**:
   - Thêm **node Google Sheets** sau node `Create an event in Google Calendar` để ghi lại lịch sử sự kiện.
   - Cấu hình để lưu:
     - Tên sự kiện.
     - Thời gian.
     - Người tạo.
     - Trạng thái (thành công/thất bại).

3. **Gửi báo cáo định kỳ**:
   - Sử dụng **node n8n-nodes-base.schedule** để chạy workflow hàng tuần và gửi báo cáo tổng hợp sự kiện qua email (sử dụng **node Email**).

4. **Tùy chỉnh AI**:
   - Để AI hiểu rõ hơn về lịch sự kiện của công ty, thêm **bối cảnh** vào node `Simple Memory`:
     ```json
     {
       "parameters": {
         "memoryKey": "companyCalendarContext",
         "windowSize": 5
       }
     }
     ```
   - Ví dụ: AI sẽ nhớ rằng *"cuộc họp hàng tuần với client ABC là thứ 5 14h"*.

5. **Xử lý lỗi tự động**:
   - Thêm **node If** sau node `Create an event in Google Calendar` để:
     - Nếu tạo sự kiện thành công → Gửi thông báo thành công qua Slack.
     - Nếu lỗi → Gửi email cảnh báo và ghi log.

---
### 📌 **Kết luận**
Workflow này **giải phóng bạn khỏi việc nhập thủ công sự kiện**, đồng thời **tận dụng AI để hiểu và chuyển đổi yêu cầu tự nhiên thành hành động thực tế**. Với **GPT-4o Mini** và **LangChain**, hệ thống không chỉ nhanh mà còn **chính xác và dễ mở rộng**.

**Hành động ngay!**
1. **Self-host n8n** trên VPS để workflow chạy 24/7.
2. **Import workflow** và cấu hình credentials.
3. **Test với yêu cầu chat** và bắt đầu tự động hóa!

**Cần hỗ trợ?** Đăng ký khóa học **Tự động hóa với n8n** tại [n8n Academy](https://n8n.io/academy) để học cách tối ưu workflow của mình!

---