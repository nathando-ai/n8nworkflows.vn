---
title: "🤖 Chatbot CRM Bán Hàng AI Tự Động Hóa với GPT-4o-mini, Google Sheets & Nhớ Lịch Sử (Self-hosted)"
description: "Workflow tự động hóa CRM bán hàng AI giúp các sếp tự động trả lời câu hỏi khách hàng, tra cứu dữ liệu Outreach & Opportunity từ Google Sheets, và nhớ lịch sử chat qua nhiều lượt tương tác - hoàn toàn không cần code. Giúp tiết kiệm thời gian, tăng trải nghiệm khách hàng và tối ưu hóa quy trình bán hàng."
slug: "chatbot-crm-ai-gpt-4o-mini-google-sheets"
tags: [n8n, automation, ai-chatbot, crm, google-sheets, self-hosted, gpt-4o-mini]
keywords: [n8n workflow crm, chatbot bán hàng tự động, tự động hóa google sheets, nhớ lịch sử chat, gpt-4o-mini n8n, CRM AI không code]
---

# 🚀 **Chatbot CRM Bán Hàng AI Tự Động Hóa với GPT-4o-mini, Google Sheets & Nhớ Lịch Sử**

Hãy tưởng tượng một chatbot không chỉ trả lời câu hỏi khách hàng mà còn **tự động tra cứu dữ liệu Outreach, Opportunity từ Google Sheets**, **nhớ lại lịch sử chat** qua nhiều lượt tương tác, và **tự động ghi log** mọi cuộc trò chuyện để các sếp có thể theo dõi và cải thiện dịch vụ. **Không cần viết một dòng code nào!**

Workflow này là giải pháp **AI + CRM tự động hóa 100%** dành cho các doanh nghiệp bán hàng, giúp các sếp:
- **Tiết kiệm thời gian** bằng cách tự động trả lời câu hỏi thường gặp (lead status, proposal, outreach progress).
- **Tăng trải nghiệm khách hàng** với phản hồi nhanh chóng và chính xác.
- **Tối ưu hóa quy trình bán hàng** bằng cách tra cứu dữ liệu từ Google Sheets một cách tự động.
- **Nhớ lại lịch sử chat** để các cuộc trò chuyện trở nên tự nhiên và liên tục, không cần khách hàng phải lặp lại thông tin.

---
### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tự động trả lời 24/7** – Khách hàng được hỗ trợ ngay lập tức, không cần chờ nhân viên.
✅ **Tra cứu dữ liệu CRM nhanh chóng** – Chatbot tự động lấy thông tin từ Google Sheets (Outreach, Opportunity) mà không cần nhập thủ công.
✅ **Nhớ lại lịch sử chat** – Khách hàng không cần lặp lại thông tin trong nhiều lượt tương tác (ví dụ: "Tôi đã nói với bạn về lead ABC trước đó").
✅ **Ghi log tất cả cuộc trò chuyện** – Dữ liệu chat được lưu vào Google Sheets để theo dõi, phân tích và cải thiện dịch vụ.
✅ **Chính xác và an toàn** – Không cần lo lắng về việc chatbot "đoán" sai dữ liệu, nó **luôn tra cứu từ nguồn thực tế**.
:::

---
### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow này hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản n8n Self-hosted** (để chạy 24/7):
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)

2. **API Key OpenAI** (để sử dụng GPT-4o-mini):
   - Tạo tại [OpenAI API](https://platform.openai.com/account/api-keys) và thêm vào **Credentials** trong n8n với tên `openAiApi`.

3. **Google Sheets OAuth 2.0 API**:
   - Tạo **Service Account** trong Google Cloud Console và cấp quyền truy cập vào các sheet cần thiết (Outreach, Opportunities, chat_memory).
   - Thêm vào **Credentials** trong n8n với tên `googleSheetsOAuth2Api`.

4. **Google Sheets đã chuẩn bị**:
   - **3 sheet chính**:
     - `outreach automation`: Dữ liệu về lead, email, tiến độ outreach.
     - `ghl database`: Dữ liệu Opportunity, pipeline, deal value.
     - `chat_memory`: Sheet để lưu lịch sử chat (cần tạo cột: `timestamp`, `sessionId`, `userMessage`, `assistantResponse`).

---
### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### 1. **Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/10840](https://n8n.io/workflows/10840) hoặc copy toàn bộ JSON từ trang này.
- Trong **n8n Editor**, nhấn **Import** và dán JSON vào.
- **Hoặc** tải file JSON từ [đây](https://github.com/rahuljoshi/n8n-workflows/blob/main/sales-crm-chatbot.json) (nếu có).

#### 2. **Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này có **10 node chính**, nhưng các bước sau đây là **quan trọng nhất** cần điều chỉnh:

##### **A. Cấu hình OpenAI (GPT-4o-mini)**
- Node: **"OpenAI Chat Model"**
  - **Không cần chỉnh gì** nếu đã thêm `openAiApi` vào Credentials.
  - **Model mặc định** là `gpt-4o-mini` (rẻ và hiệu quả).

##### **B. Cấu hình Google Sheets**
- **Node: "outreachSheet"**
  - **Sheet Name**: Điền tên sheet `outreach automation`.
  - **Range**: Điền `Sheet1!A1:Z` (hoặc phạm vi dữ liệu thực tế).
  - **Credentials**: Chọn `googleSheetsOAuth2Api`.

- **Node: "opportunitySheet"**
  - **Sheet Name**: Điền tên sheet `ghl database`.
  - **Range**: Điền `Sheet1!A1:Z`.
  - **Credentials**: Chọn `googleSheetsOAuth2Api`.

- **Node: "Write Chat Memory to Google Sheets"**
  - **Sheet Name**: Điền tên sheet `chat_memory`.
  - **Range**: Điền `Sheet1!A1:Z` (hoặc phạm vi cột cần ghi).
  - **Credentials**: Chọn `googleSheetsOAuth2Api`.
  - **Headers**: Đảm bảo cột trong sheet phù hợp với `timestamp`, `sessionId`, `userMessage`, `assistantResponse`.

##### **C. Cấu hình AI Sales CRM Router**
- Node: **"AI Sales CRM Router"**
  - Đây là **cốt lõi logic** của chatbot.
  - **Không cần chỉnh thủ công**, nhưng các sếp nên kiểm tra:
    - **Tool calls** được gọi tự động (ví dụ: `outreachSheet`, `opportunitySheet`).
    - **JSON tool calls** phải đúng định dạng:
      ```json
      {
        "tool": "<toolName>",
        "input": {
          "searchColumn": "<column>",
          "searchValue": "<value>"
        }
      }
      ```

##### **D. Cấu hình Conversation Memory Buffer**
- Node: **"Conversation Memory Buffer"**
  - **Window Size**: Đặt **7 turns** (lưu 7 lượt chat gần nhất).
  - **Credentials**: Không cần thêm, mặc định là `memoryBufferWindow`.

##### **E. Validate AI Output Payload**
- Node: **"Validate AI Output Payload"**
  - **Không cần chỉnh**, nó tự động kiểm tra nếu `output` có giá trị hay không.
  - Nếu **không có output**, nó sẽ log vào sheet `chat_memory` với cột `error`.

##### **F. Log Invalid Chat Records**
- Node: **"Log Invalid Chat Records to Google Sheets"**
  - **Sheet Name**: Điền `chat_memory` (cùng sheet với `Write Chat Memory`).
  - **Range**: Đảm bảo có cột `error` để ghi lỗi.

##### **G. Send Chat Response**
- Node: **"Send Chat Response"**
  - **Không cần chỉnh**, nó tự động trả lời người dùng qua giao diện chat của n8n.

---
#### 3. **Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Gửi một tin nhắn test vào chat (ví dụ: *"Tôi muốn biết tiến độ lead ABC"*).
   - Kiểm tra:
     - Chatbot có trả lời chính xác không?
     - Dữ liệu có được tra cứu từ Google Sheets không?
     - Lịch sử chat có được lưu vào `chat_memory` không?

2. **Bật Active workflow**:
   - Nhấn **Active** ở góc trên bên phải.

---
### ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁCH LÀM NÂNG CAO]
1. **Kết hợp với Slack/Telegram**:
   - Thay vì dùng giao diện chat của n8n, các sếp có thể **kết nối với Slack/Telegram** bằng node `n8n-nodes-base.slack` hoặc `n8n-nodes-base.telegram` để chatbot hoạt động trên nhiều kênh.

2. **Tự động gửi báo cáo hàng tuần**:
   - Sử dụng **node `n8n-nodes-base.schedule`** để chạy workflow định kỳ (ví dụ: mỗi Chủ Nhật) và gửi báo cáo tổng hợp từ `chat_memory` qua email (node `n8n-nodes-base.email`).

3. **Cải thiện logic AI**:
   - Thêm **prompt engineering** vào node `lmChatOpenAi` để chatbot trả lời chính xác hơn (ví dụ: *"Bạn là một trợ lý bán hàng chuyên nghiệp, hãy tra cứu dữ liệu từ Google Sheets trước khi trả lời"*).

4. **Lọc dữ liệu trong Google Sheets**:
   - Sử dụng **Google Apps Script** để tự động sắp xếp dữ liệu trong `outreach automation` và `ghl database` trước khi chatbot tra cứu.

5. **Dùng nhiều model AI**:
   - Thay vì chỉ dùng `gpt-4o-mini`, các sếp có thể **chuyển đổi model** trong node `lmChatOpenAi` để tiết kiệm chi phí (ví dụ: `gpt-3.5-turbo` cho các câu hỏi đơn giản).
:::

---
### 📌 **Kết luận**
Workflow **Chatbot CRM Bán Hàng AI với GPT-4o-mini** là giải pháp **tự động hóa hoàn chỉnh** giúp các sếp:
✔ **Tiết kiệm thời gian** bằng cách tự động trả lời khách hàng.
✔ **Tăng hiệu quả bán hàng** với dữ liệu tra cứu từ Google Sheets.
✔ **Nhớ lại lịch sử chat** để trải nghiệm khách hàng trở nên tự nhiên.
✔ **Ghi log tất cả cuộc trò chuyện** để phân tích và cải thiện.

**Hãy áp dụng ngay workflow này trên VPS của mình và bắt đầu tự động hóa CRM bán hàng của doanh nghiệp!**
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%) để chạy workflow 24/7 mà không lo downtime.

---
**Chia sẻ và phản hồi:**
Nếu các sếp có bất kỳ câu hỏi hoặc cần hỗ trợ thêm, hãy để lại comment dưới đây hoặc liên hệ qua [n8n Community](https://community.n8n.io/). Chúc các sếp thành công với tự động hóa CRM! 🚀