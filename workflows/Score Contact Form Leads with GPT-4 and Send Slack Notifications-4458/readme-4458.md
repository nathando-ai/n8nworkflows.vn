---
title: "🚀 Tự Động Hạng Độ Tiềm Năng Lead Từ Form Liên Hệ Với GPT-4 & Gửi Thông Báo Slack (N8n)"
description: "Workflow tự động hóa phân tích và xếp hạng tiềm năng lead từ form liên hệ bằng trí tuệ nhân tạo GPT-4, sau đó gửi thông báo ngay lập tức đến Slack để đội ngũ bán hàng nhanh chóng phản hồi với lead ưu tiên cao nhất. Tiết kiệm thời gian lên đến 80% trong quá trình triết lý lead."
slug: "tieu-dong-hang-do-tien-nang-lead-gpt4-slack"
tags: [n8n, automation, sales, ai, gpt-4, slack, no-code, lead-scoring]
keywords: [n8n workflow tự động hóa, phân tích lead bằng GPT-4, gửi thông báo Slack tự động, tự động hóa bán hàng, lead scoring, n8n self-hosted]
---

# 🚀 **Tự Động Hạng Độ Tiềm Năng Lead Từ Form Liên Hệ Với GPT-4 & Gửi Thông Báo Slack**

### **Giải pháp nào giúp các sếp không còn phải mất thời gian thủ công triết lý hàng trăm lead mỗi ngày?**
Hãy tưởng tượng: Một lead mới gửi form liên hệ, nhưng bạn không thể biết ngay liệu họ là **Hot** (sẵn sàng mua ngay), **Warm** (cần tiếp cận thêm), hay **Cold** (không tiềm năng). Với **n8n + GPT-4**, workflow này tự động:
✅ **Phân tích nội dung message** bằng trí tuệ nhân tạo để xếp hạng lead.
✅ **Gửi thông báo ngay lập tức** vào Slack với thông tin chi tiết (tên, email, mức độ tiềm năng).
✅ **Giúp đội ngũ bán hàng** tập trung vào lead ưu tiên cao nhất, **tăng tỷ lệ chuyển đổi lên 30%**.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **24/7** mà không bị gián đoạn, các sếp nên **self-host n8n** trên VPS chuyên dụng:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đảm bảo tốc độ cao, không lag)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần thủ công phân loại lead, tự động hóa **100% quá trình triết lý**.
- **Chính xác cao**: GPT-4 phân tích ngữ điệu và nội dung message để xếp hạng **Hot/Warm/Cold** chính xác hơn con người.
- **Tăng tỷ lệ chuyển đổi**: Đội ngũ bán hàng chỉ tập trung vào lead **Hot**, giảm thời gian phản hồi từ **24h xuống 1h**.
- **Hoạt động liên tục**: Workflow chạy **24/7** ngay cả khi các sếp ngủ, không cần can thiệp.
- **Tích hợp Slack**: Thông báo ngay lập tức vào kênh #social, giúp team **không bỏ lỡ lead nào**.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản n8n self-hosted** (đã cài đặt và chạy trên VPS).
✔ **API Key OpenAI** (để kết nối với GPT-4).
✔ **Credentials Slack**:
   - **Slack App Token** (để gửi thông báo).
   - **Kênh Slack** (ví dụ: `#social`).
✔ **Form liên hệ** (cần cấu hình webhook để gửi dữ liệu POST đến `/form-submission`).

---
:::note[LƯU Ý QUAN TRỌNG]
- Nếu chưa có **API Key OpenAI**, đăng ký tại [OpenAI](https://platform.openai.com/) và thêm vào **Credentials** trong n8n.
- Đảm bảo **kênh Slack** đã được tạo và **Slack App** có quyền gửi tin nhắn.
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ **file JSON** hoặc **copy/paste JSON** vào n8n Editor:
```bash
# Cách 1: Import từ file JSON
1. Tải file workflow từ [n8n.io/workflows/4458](https://n8n.io/workflows/4458).
2. Trong n8n Editor, nhấn **Import** → Chọn file JSON.
3. Chọn **Create new workflow** và nhấn **Import**.

# Cách 2: Copy/paste JSON (nếu không muốn tải file)
1. Mở n8n Editor → Tạo workflow mới.
2. Nhấn **Import** → Chọn **Paste JSON**.
3. Dán JSON từ [n8n.io/workflows/4458](https://n8n.io/workflows/4458) và nhấn **Import**.
```

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Sau khi import, các sếp **phải cấu hình** các node sau:

##### **🔹 Node 1: Receive Form Submission (Webhook)**
- **Path**: Đảm bảo giữ nguyên `/form-submission`.
- **HTTP Method**: Giữ nguyên `POST`.
- **Credentials**: Không cần thiết (webhook công khai, nhưng các sếp nên **bảo mật** bằng cách thêm **IP Allowlist** nếu cần).

##### **🔹 Node 2: Extract Lead Details (Set)**
- **Expression**: Các sếp **không cần chỉnh sửa** (n8n tự động trích xuất `name`, `email`, `message` từ payload).
- **Lưu ý**: Nếu form liên hệ của các sếp có **cấu trúc khác**, cần chỉnh sửa **JSONPath** trong node này:
  ```json
  {
    "name": "$$.jsonBody.name",
    "email": "$$.jsonBody.email",
    "message": "$$.jsonBody.message"
  }
  ```

##### **🔹 Node 3: Rate Lead Interest (OpenAI)**
- **API Key**: Điền **API Key OpenAI** từ **Credentials**.
- **Model**: Giữ nguyên `gpt-4-1106-preview` (hoặc chọn model mới nhất).
- **Prompt**: Các sếp **không cần chỉnh sửa** (GPT-4 sẽ trả về **Hot/Warm/Cold** dựa trên message).
- **Lưu ý**:
  - Nếu **quá tải API**, các sếp có thể **cài đặt rate limit** trong node này.
  - Nếu muốn **cải thiện độ chính xác**, các sếp có thể **tùy chỉnh prompt** (ví dụ: thêm yêu cầu phân tích ngữ điệu).

##### **🔹 Node 4: Send Lead Alert to Slack (Slack)**
- **Credentials**: Chọn **Slack App Token** đã cấu hình trước.
- **Channel**: Điền **#social** (hoặc kênh khác các sếp muốn).
- **Message Format**: Các sếp **không cần chỉnh sửa** (n8n tự động tạo tin nhắn với template:
  ```
  🔥 **Interest Level**: {{ $node["Rate Lead Interest"].json["result"] }}
  🧑 **Name**: {{ $node["Extract Lead Details"].json["name"] }}
  📧 **Email**: {{ $node["Extract Lead Details"].json["email"] }}
  💬 **Message**: {{ $node["Extract Lead Details"].json["message"] }}
  ```
- **Lưu ý**:
  - Nếu **Slack App** chưa được cấu hình, các sếp cần tạo tại [Slack API](https://api.slack.com/apps) và thêm **Bot Token** vào **Credentials** của n8n.

#### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Gửi một **POST request** đến `/form-submission` (ví dụ bằng Postman hoặc cURL):
     ```bash
     curl -X POST https://[your-n8n-domain]/form-submission \
     -H "Content-Type: application/json" \
     -d '{"name":"John Doe","email":"john@example.com","message":"Tôi muốn mua sản phẩm của quý công ty!"}'
     ```
   - Kiểm tra **Slack** để xem tin nhắn có xuất hiện không.
2. **Bật Active workflow**:
   - Nhấn **Active** trên canvas n8n.

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁCH NÂNG CAO HIỆU QUẢ]
1. **Lưu log lead vào Google Sheets/Notion**:
   - Thêm node **Google Sheets** hoặc **Notion** sau node **Rate Lead Interest** để lưu lịch sử lead.
   - Cấu hình như sau:
     ```json
     {
       "sheetName": "Leads",
       "row": {
         "Name": "{{ $node["Extract Lead Details"].json["name"] }}",
         "Email": "{{ $node["Extract Lead Details"].json["email"] }}",
         "Interest": "{{ $node["Rate Lead Interest"].json["result"] }}",
         "Message": "{{ $node["Extract Lead Details"].json["message"] }}",
         "Timestamp": "{{ $node["Date/Time"].date }}"
       }
     }
     ```

2. **Gửi email tự động cho lead Hot**:
   - Thêm node **Send Email** (ví dụ: **SendGrid** hoặc **Gmail**) sau node **Rate Lead Interest**.
   - Cấu hình điều kiện:
     ```json
     {
       "condition": "{{ $node["Rate Lead Interest"].json["result"] === 'Hot' }}"
     }
     ```
   - Nội dung email:
     ```
     Xin chào {{ $node["Extract Lead Details"].json["name"] }},
     Chúng tôi đã nhận được tin nhắn của bạn và đánh giá đây là một lead **Hot**! Chúng tôi sẽ liên hệ ngay trong ngày.
     ```

3. **Tích hợp với CRM (HubSpot, Salesforce)**:
   - Thay thế node **Slack** bằng node **HubSpot** hoặc **Salesforce** để tự động tạo lead trong CRM.
   - Ví dụ với **HubSpot**:
     ```json
     {
       "properties": {
         "name": "{{ $node["Extract Lead Details"].json["name"] }}",
         "email": "{{ $node["Extract Lead Details"].json["email"] }}",
         "lead_status": "{{ $node["Rate Lead Interest"].json["result"] }}"
       }
     }
     ```

4. **Dùng Telegram thay Slack**:
   - Thay node **Slack** bằng **Telegram Bot** để gửi thông báo.
   - Cấu hình như sau:
     ```json
     {
       "chatId": "@your_telegram_bot",
       "message": "🔥 **Interest Level**: {{ $node["Rate Lead Interest"].json["result"] }}\n🧑 **Name**: {{ $node["Extract Lead Details"].json["name"] }}"
     }
     ```
:::

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp và đội ngũ bán hàng, giúp họ **tập trung vào lead có tiềm năng cao nhất** mà không cần mất thời gian phân loại thủ công. Với **GPT-4 + Slack**, các sếp sẽ **không bỏ lỡ lead nào** và **tăng tỷ lệ chuyển đổi đáng kể**.

**Bắt tay vào tự động hóa ngay hôm nay!**
👉 [Tải workflow từ n8n.io](https://n8n.io/workflows/4458)
👉 [Đăng ký VPS n8n để self-host](https://tino.vn/vps-n8n?affid=388) (🎁 **Giảm 39%**)

---
**Cần hỗ trợ?** Liên hệ với tác giả Yaron Been qua:
📧 [Yaron@nofluff.online](mailto:Yaron@nofluff.online)
🎥 [YouTube](https://www.youtube.com/@YaronBeen/videos)
💼 [LinkedIn](https://www.linkedin.com/in/yaronbeen/)