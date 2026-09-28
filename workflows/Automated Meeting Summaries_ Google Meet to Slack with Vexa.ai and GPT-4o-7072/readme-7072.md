---
title: "🤖 Tự Động Tóm Tắt Cuộc Họp Google Meet Sang Slack Với AI (Vexa.ai + GPT-4o) - Không Cần Code"
description: "Workflow tự động hóa hoàn chỉnh giúp các sếp tự động tóm tắt nội dung cuộc họp Google Meet qua Vexa.ai, sau đó gửi tóm tắt sang Slack với GPT-4o - tiết kiệm thời gian lên đến 90% cho các cuộc họp hàng ngày. Chỉ cần cài đặt 1 lần, workflow hoạt động 24/7."
slug: "tieu-dong-tom-tat-cuoc-hop-google-meet-sang-slack-ai"
tags: [n8n, automation, no-code, ai-summarization, google-meet, slack, vexa-ai, openai]
keywords: [tự động hóa cuộc họp, tóm tắt cuộc họp AI, google meet slack, n8n workflow, tự động hóa no-code, GPT-4o tóm tắt]
---

# 🚀 **Tự Động Tóm Tắt Cuộc Họp Google Meet Sang Slack Với AI (Vexa.ai + GPT-4o)**

### **Giải pháp cho các sếp bị "chìm" trong cuộc họp hàng ngày**
Các sếp đã từng gặp phải tình trạng sau cuộc họp:
- **Không ghi chép đầy đủ** → Quên nội dung quan trọng.
- **Tóm tắt thủ công** → Tốn thời gian 30-60 phút/ngày.
- **Thiếu sự chính xác** → Tóm tắt sai lệch, mất thời gian sửa chữa.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Chuyển đổi cuộc họp Google Meet** thành văn bản chính xác (Vexa.ai).
✅ **Tóm tắt bằng AI GPT-4o** với ngữ cảnh và logic hoàn chỉnh.
✅ **Gửi tóm tắt sang Slack** ngay lập tức, giúp các sếp **tiết kiệm 90% thời gian** và **không bỏ lỡ bất kỳ chi tiết nào**.

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm thời gian**: Không cần tóm tắt thủ công sau mỗi cuộc họp.
- **Chính xác 100%**: Dữ liệu từ Vexa.ai + AI GPT-4o đảm bảo không bỏ sót chi tiết.
- **Hoạt động 24/7**: Workflow chạy tự động ngay khi cuộc họp bắt đầu.
- **Cá nhân hóa**: Tóm tắt được gửi trực tiếp vào kênh Slack của bạn.
- **Giá thành hợp lý**: ~$0.01-$0.05/cuộc họp (OpenAI), tiết kiệm so với thuê nhân viên.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[**CHUẨN BỊ**]
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản Google Calendar** (API miễn phí).
✔ **Tài khoản Vexa.ai** (API key) để ghi lại cuộc họp.
✔ **Tài khoản OpenAI** (GPT-4o) để tóm tắt.
✔ **Slack Workspace** (quyền admin để tạo bot).
✔ **Thời gian cài đặt**: ~15-20 phút (lần đầu tiên).
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. **Tải file JSON** từ [link gốc](https://n8n.io/workflows/7072).
2. Trong **n8n Dashboard**, chọn **"Import"** → Chọn file JSON.
3. **Hoặc** copy toàn bộ JSON vào **"Import Workflow"** và nhấn **"Import"**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **9 node chính**, các sếp cần chú ý cấu hình các node sau:

##### **🔹 Node "Google Calendar Trigger" (n8n-nodes-base.googleCalendarTrigger)**
- **Cấu hình**:
  - Chọn **Google Calendar OAuth2 API** (đã thiết lập trước).
  - **Event Trigger**: Chọn **"eventStarted"** (cuộc họp bắt đầu).
  - **Calendar**: Chọn lịch Google Meet bạn thường dùng.
  - **⚠️ Lưu ý**: **Chỉ hoạt động với liên kết Google Meet** trong sự kiện calendar.

##### **🔹 Node "Add bot to meet" (n8n-nodes-base.httpRequest)**
- **Mục đích**: Thêm bot Vexa.ai vào cuộc họp tự động.
- **Cấu hình**:
  - **URL**: `https://api.vexa.ai/bots/{botId}/meetings/{meetingId}/join`
  - **Headers**:
    - `X-API-Key`: API Key của Vexa.ai (đã thêm trong **HTTP Header Auth**).
    - `Content-Type`: `application/json`
  - **Body**:
    ```json
    {
      "meetingId": "{{ $node["Google Calendar Trigger"].json["meetingLink"] }}"
    }
    ```
  - **⚠️ Lưu ý**: **Meeting ID** được tự động trích xuất từ liên kết Google Meet.

##### **🔹 Node "Get Vexa Transcript" (n8n-nodes-base.httpRequest)**
- **Mục đích**: Lấy bản ghi âm cuộc họp từ Vexa.ai.
- **Cấu hình**:
  - **URL**: `https://api.vexa.ai/bots/{botId}/meetings/{meetingId}/transcript`
  - **Headers**:
    - `X-API-Key`: API Key của Vexa.ai.
  - **⚠️ Lưu ý**: **Chờ 30-60 giây** sau khi cuộc họp bắt đầu để bot Vexa.ai tham gia.

##### **🔹 Node "OpenAI Chat Model" (n8n-nodes-base.lmChatOpenAi)**
- **Mục đích**: Tóm tắt văn bản bằng GPT-4o.
- **Cấu hình**:
  - **Model**: Chọn **"chatgpt-4o-latest"** (đã cấu hình sẵn).
  - **Prompt**: Sử dụng **default prompt** của workflow (có thể tùy chỉnh):
    ```
    Tóm tắt cuộc họp này thành một bản tóm tắt ngắn gọn (3-5 câu) với:
    - Điểm chính được thảo luận.
    - Các quyết định hoặc hành động cần thực hiện.
    - Thời gian và người phụ trách.
    ```
  - **⚠️ Lưu ý**: **Đảm bảo tài khoản OpenAI có đủ credit** (~$0.01-$0.05/cuộc họp).

##### **🔹 Node "Send a message" (n8n-nodes-base.slack)**
- **Mục đích**: Gửi tóm tắt sang Slack.
- **Cấu hình**:
  - **Channel**: Chọn kênh Slack muốn gửi (ví dụ: `#meeting-summaries`).
  - **Message Format**:
    ```json
    {
      "text": "📝 **Tóm tắt cuộc họp**: {{ $node["OpenAI Chat Model"].json }}"
    }
    ```
  - **⚠️ Lưu ý**: **Bot Slack phải có quyền `chat:write`** để gửi tin nhắn.

##### **🔹 Node "If" (n8n-nodes-base.if)**
- **Mục đích**: Kiểm tra nếu cuộc họp có bản ghi âm (transcript) từ Vexa.ai.
- **Cấu hình**:
  - **Condition**: `{{ $json["transcript"] }} != null`
  - **⚠️ Lưu ý**: Nếu không có transcript, workflow sẽ **bỏ qua** và không gửi tóm tắt.

##### **🔹 Node "Wait" (n8n-nodes-base.wait)**
- **Mục đích**: Chờ 30 giây để bot Vexa.ai tham gia cuộc họp.
- **Cấu hình**:
  - **Time**: `30000` (30 giây).

---

#### **3. Kích hoạt ⚡️**
1. **Test run** với một cuộc họp mẫu:
   - Chọn **"Run Workflow"** và nhập **meeting link** từ Google Calendar.
   - Kiểm tra **Slack** để xem tóm tắt được gửi không.
2. **Bật Active workflow**:
   - Sau khi test thành công, chuyển **status** từ **"Inactive"** sang **"Active"**.

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::info[**CÁCH LÀM NÀY ĐỂ TIẾT KIỆM THÊM THỜI GIAN**]
1. **Lưu log cuộc họp**:
   - Thêm node **Google Sheets** để lưu toàn bộ transcript và tóm tắt vào một bảng Excel.
   - **Cách làm**:
     - Sử dụng node **Google Sheets** (n8n-nodes-base.googleSheets).
     - Cấu hình **Sheet Name** và **Range** để ghi dữ liệu.

2. **Gửi báo cáo định kỳ**:
   - Sử dụng **node `n8n-nodes-base.email`** để gửi báo cáo tuần/month cho team.
   - **Cách làm**:
     - Thêm node **Email** sau node **OpenAI Chat Model**.
     - Cấu hình **From**, **To**, và **Subject**:
       ```
       "Báo cáo tóm tắt cuộc họp tuần này"
       ```

3. **Tùy chỉnh prompt AI**:
   - Nếu muốn tóm tắt theo **cách riêng**, chỉnh sửa **prompt** trong node **OpenAI Chat Model**:
     ```json
     {
       "prompt": "Tóm tắt cuộc họp này theo định dạng sau:\n1. Điểm 1: [Nội dung]\n2. Điểm 2: [Nội dung]\n3. Hành động: [Ai làm gì? Thời gian?]"
     }
     ```

4. **Kết hợp với Notion/Google Docs**:
   - Thay vì Slack, các sếp có thể **ghi tóm tắt vào Notion** hoặc **Google Docs** bằng node **Notion API** hoặc **Google Docs**.
   - **Cách làm**:
     - Thêm node **Notion** (n8n-nodes-base.notion) sau node **OpenAI Chat Model**.
     - Cấu hình **Database ID** và **Properties** để lưu tóm tắt.

5. **Xử lý cuộc họp bị lỗi**:
   - Thêm node **Error Handling** (n8n-nodes-base.code) để **lặp lại** nếu Vexa.ai không lấy được transcript.
   - **Mã JavaScript**:
     ```javascript
     // Nếu transcript null, chờ 10 giây và thử lại
     if (!json.transcript) {
       return { json: { retry: true } };
     }
     return json;
     ```
---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn **tự động hóa tóm tắt cuộc họp** mà không cần code. Với **Vexa.ai + GPT-4o**, bạn sẽ:
✔ **Tiết kiệm 90% thời gian** sau cuộc họp.
✔ **Không bỏ sót bất kỳ chi tiết nào**.
✔ **Hoạt động 24/7** mà không cần can thiệp.

**Hành động ngay!**
1. **Cài đặt n8n trên VPS** (Self-hosted) để workflow chạy ổn định.
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Bật Active** và **nghỉ ngơi** khi AI làm việc thay bạn!

---
:::info[**Gợi ý hạ tầng cho n8n**]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

**Bắt đầu tự động hóa cuộc họp của mình ngay hôm nay!** 🚀