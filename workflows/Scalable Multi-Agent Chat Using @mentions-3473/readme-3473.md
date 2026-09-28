---
title: "🤖 **Tự Động Hóa Chat AI Nhiều Agent Với @Mention - Giải Pháp Tối Ưu Cho Dịch Vụ Chăm Sóc Khách Hàng & Trợ Lý 24/7**"
description: "Workflow này cho phép các sếp khởi tạo cuộc hội thoại song song với nhiều AI Agent khác nhau, mỗi Agent có thể được cấu hình riêng biệt với tên, hệ thống hướng dẫn và mô hình LLM khác nhau. Tiết kiệm thời gian lên tới 80% so với cách làm thủ công, đồng thời cải thiện trải nghiệm khách hàng với phản hồi cá nhân hóa."
slug: "tieu-dong-hoa-chat-ai-nhieu-agent-mention"
tags: [n8n, automation, ai-chatbot, langchain, openrouter, no-code]
keywords: [n8n workflow chatbot, tự động hóa AI agent, @mention trong chatbot, LangChain với n8n, OpenRouter API, chatbot nhiều nhân vật]
---

# 🚀 **Tự Động Hóa Chat AI Nhiều Agent Với @Mention: Giải Pháp Tối Ưu Cho Dịch Vụ Trực Tuyến**

## **Nỗi Đau Của Các Sếp: Chatbot Thiếu Cá Nhân Hóa & Tốn Thời Gian**
Hiện nay, khi sử dụng chatbot AI đơn giản, các sếp thường gặp phải những vấn đề sau:
- **Phản hồi chung chung**: Chatbot chỉ trả lời theo một mô hình duy nhất, không thể phân biệt giữa khách hàng cần hỗ trợ kỹ thuật, tư vấn sản phẩm hay phản hồi cảm xúc.
- **Tốn thời gian cấu hình**: Mỗi khi muốn thêm một "nhân vật" AI mới (ví dụ: nhân viên kỹ thuật, chuyên gia marketing, hoặc trợ lý cá nhân), các sếp phải viết code hoặc cấu hình nhiều workflow riêng biệt.
- **Không hỗ trợ hội thoại đa Agent**: Khách hàng thường muốn "nói chuyện" với nhiều nhân viên cùng lúc (ví dụ: "Tôi muốn nói với kỹ thuật viên @TechSupport và nhân viên bán hàng @Sales"), nhưng hầu hết chatbot chỉ cho phép một Agent duy nhất.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tạo nhiều Agent AI riêng biệt** với tên, mô hình LLM và hệ thống hướng dẫn khác nhau.
✅ **Hỗ trợ @mention** để khách hàng có thể "gọi" Agent cụ thể (ví dụ: `@TechSupport` hoặc `@Sales`).
✅ **Hội thoại liên tục** nhờ bộ nhớ chia sẻ (memory buffer), giúp Agent "nhớ" lịch sử cuộc trò chuyện.
✅ **Tự động hóa 100%** không cần code, chỉ cần cấu hình trong n8n.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động 24/7 với hiệu suất tối ưu, các sếp nên **self-host n8n** trên VPS mạnh mẽ. Dưới đây là 2 lựa chọn tốt nhất với mã giảm giá đặc biệt:

👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
   - Dung lượng 4GB RAM, CPU 2 nhân, băng thông cao.
   - Hỗ trợ cài đặt n8n một cách dễ dàng.

👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)**
   - Máy chủ Xeon 4 nhân, RAM 4GB, ổ SSD 100GB.
   - Phù hợp cho workflow AI nặng như này.

**Lưu ý:** Nên chọn gói VPS có **OpenRouter API Key** và **LangChain** được hỗ trợ.
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian lên tới 80%** so với cách làm thủ công (không cần viết code hoặc cấu hình nhiều workflow).
- **Cá nhân hóa trải nghiệm khách hàng**: Khách hàng có thể "nói chuyện" với nhiều nhân viên cùng lúc (ví dụ: `@TechSupport` và `@Sales`).
- **Hội thoại liên tục**: AI "nhớ" lịch sử trò chuyện qua nhiều lượt nhắn tin nhờ bộ nhớ chia sẻ.
- **Dễ dàng mở rộng**: Thêm hoặc thay đổi Agent chỉ bằng cách chỉnh sửa JSON trong các node `Define Agent Settings`.
- **Hỗ trợ nhiều mô hình LLM**: Sử dụng OpenRouter để chọn mô hình AI phù hợp (ví dụ: Mistral, Llama 2, GPT-4).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản OpenRouter API**:
   - Đăng ký tại [OpenRouter](https://openrouter.ai/) và lấy **API Key**.
   - Trong n8n, thêm **credentials** mới với tên `openRouterApi` và gán API Key vào đó.
   - *Lưu ý:* OpenRouter hỗ trợ nhiều mô hình AI như Mistral, Llama 2, GPT-4. Các sếp có thể chọn mô hình phù hợp.

2. **Node LangChain**:
   - Workflow này sử dụng các node LangChain của n8n. Nên cài đặt package `@n8n/n8n-nodes-langchain` bằng lệnh:
     ```bash
     npx n8n install @n8n/n8n-nodes-langchain
     ```

3. **Không cần API Key nào khác**:
   - Workflow chỉ sử dụng OpenRouter và các node mặc định của n8n.

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải file JSON** từ [đây](https://n8n.io/workflows/3473) (hoặc copy toàn bộ JSON từ link trên).
- Trong n8n, nhấn **Import Workflow** và dán JSON vào.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Sau khi import, các sếp cần chỉnh sửa **3 node quan trọng** để workflow hoạt động:

##### **A. Cấu Hình Settings (Node `Define Global Settings` và `Define Agent Settings`)**
- Mở node **`Define Global Settings`** (node thứ 10) và chỉnh sửa JSON như sau:
  ```json
  {
    "user": {
      "name": "Tên của bạn (ví dụ: 'Nguyễn Văn A')",
      "role": "Người dùng"
    },
    "system": {
      "content": "Bạn là một trợ lý AI chuyên nghiệp. Hãy trả lời khách hàng một cách thân thiện và chuyên nghiệp."
    }
  }
  ```
- Mở node **`Define Agent Settings`** (node thứ 11) và cấu hình các Agent như ví dụ dưới đây:
  ```json
  {
    "agents": [
      {
        "name": "TechSupport",
        "system": "Bạn là nhân viên kỹ thuật hỗ trợ khách hàng. Hãy giải quyết vấn đề kỹ thuật một cách chi tiết.",
        "model": "mistral-tiny" // Chọn mô hình từ OpenRouter
      },
      {
        "name": "Sales",
        "system": "Bạn là nhân viên bán hàng. Hãy tư vấn sản phẩm và khuyến mãi một cách chuyên nghiệp.",
        "model": "llama-2-7b-chat"
      }
    ]
  }
  ```
  - **Lưu ý:** Các sếp có thể thêm/bớt Agent tùy ý. Mỗi Agent cần có:
    - `name`: Tên gọi (sẽ được sử dụng trong @mention).
    - `system`: Hệ thống hướng dẫn cho Agent.
    - `model`: Mô hình LLM từ OpenRouter (ví dụ: `mistral-tiny`, `llama-2-7b-chat`).

##### **B. Kết Nối OpenRouter (Node `OpenRouter Chat Model`)**
- Node này đã tự động lấy `model` từ node `Extract mentions`.
- **Chỉ cần đảm bảo credentials `openRouterApi` đã được cấu hình** (cách làm ở phần **Yêu cầu cần thiết**).

##### **C. Cấu Hình Node `chatTrigger`**
- Node này là điểm bắt đầu workflow. Các sếp có thể:
  - **Sử dụng Webhook** để nhận tin nhắn từ Slack, Telegram, hoặc ứng dụng web.
  - **Test với dữ liệu mẫu** trước khi deploy:
    ```json
    {
      "message": "Xin chào! Tôi muốn nói với @TechSupport về vấn đề lỗi trên sản phẩm."
    }
    ```

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Nhấn **Run Workflow** và gửi tin nhắn mẫu như:
    ```
    Xin chào! Tôi muốn nói với @TechSupport về lỗi trên sản phẩm và @Sales về khuyến mãi.
    ```
  - Kết quả mong đợi:
    - Agent `@TechSupport` sẽ trả lời về lỗi kỹ thuật.
    - Agent `@Sales` sẽ trả lời về khuyến mãi.
    - Các Agent sẽ trả lời theo thứ tự ngẫu nhiên (nếu không có @mention).

- **Bật Active**:
  - Sau khi test thành công, chuyển workflow sang **Active**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết Nối Với Slack/Telegram**:
   - Sử dụng node **Slack** hoặc **Telegram Bot** để nhận tin nhắn từ các kênh này.
   - Cấu hình **webhook** trong node `chatTrigger` để nhận dữ liệu từ Slack/Telegram.

2. **Lưu Log Cuộc Trò Chuyện**:
   - Thêm node **Google Sheets** hoặc **Airtable** sau node `Combine and format responses` để lưu lịch sử hội thoại.
   - Ví dụ:
     ```json
     {
       "sheetName": "Chatbot_Logs",
       "headers": ["Time", "User", "Agent", "Message"]
     }
     ```

3. **Gửi Báo Cáo Định Kỳ**:
   - Sử dụng node **Email** hoặc **Slack Notification** để báo cáo tổng hợp kết quả chatbot hàng ngày.
   - Ví dụ: "Hôm nay có 50 tin nhắn, trong đó 30% liên quan đến @TechSupport".

4. **Tối Ưu Hiệu Suất**:
   - Nếu workflow chậm, các sếp có thể:
     - Chọn mô hình LLM nhỏ hơn (ví dụ: `mistral-tiny` thay vì `gpt-4`).
     - Giảm số lượng Agent hoạt động cùng lúc.

---

### 📌 **Kết Luận: Áp Dụng Ngay Để Cải Thiện Trải Nghiệm Khách Hàng**
Workflow **Scalable Multi-Agent Chat Using @mentions** là giải pháp **tự động hóa cao** cho các sếp muốn:
✔ **Tạo chatbot AI cá nhân hóa** với nhiều nhân vật khác nhau.
✔ **Giảm thời gian cấu hình** từ nhiều giờ xuống còn vài phút.
✔ **Hỗ trợ khách hàng 24/7** với phản hồi nhanh chóng và chuyên nghiệp.

**Hành động ngay:**
1. **Cài đặt n8n trên VPS** (sử dụng mã giảm giá trên).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Test với tin nhắn mẫu** và deploy!

**Nếu có vấn đề**, các sếp có thể tham khảo [cộng đồng n8n](https://community.n8n.io/) hoặc liên hệ với tác giả Jon Doran qua [GitHub](https://github.com/jondoran).

---
**Chúc các sếp thành công với chatbot AI thông minh nhất của mình!** 🚀