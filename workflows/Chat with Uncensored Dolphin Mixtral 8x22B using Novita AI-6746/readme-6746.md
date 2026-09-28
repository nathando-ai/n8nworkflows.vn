---
title: "🦈 Tự Động Hóa Chat AI Miễn Censure với Dolphin Mixtral 8x22B - Không Cần Code!"
description: "Tự động hóa chatbot AI thông minh với Dolphin Mixtral 8x22B trên Novita AI, giúp các sếp tiết kiệm thời gian và nâng cao hiệu suất tương tác khách hàng 24/7. Workflow hoàn toàn tự động, không cần viết code."
slug: "tieu-dong-hoa-chatbot-dolphin-mixtral-8x22b"
tags: [n8n, automation, ai-chatbot, novita-ai, dolphin-mixtral]
keywords: [n8n workflow chatbot, tự động hóa chat AI, Dolphin Mixtral 8x22B, Novita API, chatbot không code]
---

# 🦈 **Tự Động Hóa Chatbot AI Dolphin Mixtral 8x22B - Không Cần Code!**

### **Giải pháp AI cho doanh nghiệp không còn phụ thuộc vào cloud đắt đỏ**
Các sếp đang gặp khó khăn khi phải phụ thuộc vào các dịch vụ cloud AI đắt tiền như Mistral Enterprise hoặc các giải pháp AI từ Google/Microsoft? Hay đang muốn xây dựng một chatbot AI riêng tư, miễn censor, nhưng không biết bắt đầu từ đâu? **Workflow này sẽ giúp các sếp tự động hóa chatbot AI với Dolphin Mixtral 8x22B trên Novita AI – một giải pháp riêng tư, tiết kiệm chi phí và hoạt động 24/7 mà không cần viết một dòng code nào!**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động ổn định và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng để đảm bảo tính riêng tư và hiệu suất tối ưu.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm chi phí**: Không cần trả phí cao cho các dịch vụ cloud AI như Mistral Enterprise.
- **Tính riêng tư cao**: Dữ liệu và tương tác được xử lý trên Novita AI (không bị censor).
- **Hoạt động liên tục**: Workflow tự động hóa 24/7, không cần can thiệp thủ công.
- **Tương tác thông minh**: Sử dụng mô hình Dolphin Mixtral 8x22B – một trong những mô hình AI tiên tiến nhất hiện nay.
- **Dễ dàng mở rộng**: Có thể kết nối với Slack, Telegram hoặc lưu lịch sử chat vào Google Sheets.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
- **Tài khoản Novita AI**: [Đăng ký tại đây](https://novita.ai/?ref=mze5m2e&utm_source=affiliate) (sử dụng mã giới thiệu `mze5m2e` để được hỗ trợ).
- **API Key của Novita**: Sau khi đăng ký, lấy API Key từ **Dashboard Novita** (đường dẫn: `https://novita.ai/dashboard/api-keys`).
- **Tài khoản n8n**: Nếu chưa có, các sếp có thể [đăng ký miễn phí tại đây](https://n8n.io/).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Truy cập [n8n Editor](https://n8n.io/editor).
2. Nhấp vào **"Import"** và chọn file JSON (hoặc copy/paste JSON từ [link gốc](https://n8n.io/workflows/6746)).
3. Chọn **"Create Workflow"** để bắt đầu.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này bao gồm **4 node chính**, các sếp cần cấu hình như sau:

##### **Node 1: When chat message received (chatTrigger)**
- **Loại node**: `@n8n/n8n-nodes-langchain.chatTrigger`
- **Cấu hình**:
  - **Trigger Type**: Chọn **"Webhook"** (để nhận tin nhắn từ các ứng dụng bên ngoài như Slack, Telegram, hoặc form web).
  - **Endpoint**: Các sếp có thể giữ mặc định hoặc thay đổi theo yêu cầu.

##### **Node 2: Generate Chat Completion (httpRequest)**
- **Loại node**: `n8n-nodes-base.httpRequest`
- **Cấu hình**:
  - **Method**: `POST`
  - **URL**: `https://api.novita.ai/v1/chat/completions`
  - **Headers**:
    - `Authorization`: `Bearer <API_KEY_NOVITA>` (thay `<API_KEY_NOVITA>` bằng API Key của các sếp).
    - `Content-Type`: `application/json`
  - **Body (JSON)**:
    ```json
    {
      "model": "dolphin-mixtral-8x22b",
      "messages": [
        {
          "role": "user",
          "content": "{{ $json["message"] }}"
        }
      ],
      "temperature": 0.7,
      "max_tokens": 1024
    }
    ```
    - **Lưu ý**:
      - Thay `{{ $json["message"] }}` bằng biến nhận từ node **Set fields** (node 4).
      - Các sếp có thể điều chỉnh `temperature` và `max_tokens` theo nhu cầu.

##### **Node 3: Return output (set)**
- **Loại node**: `n8n-nodes-base.set`
- **Cấu hình**:
  - **Set JSON Path**: `$.response`
  - **Value**: `{{ $json }}` (trả về kết quả từ API Novita).

##### **Node 4: Set fields (set)**
- **Loại node**: `n8n-nodes-base.set`
- **Cấu hình**:
  - **Set JSON Path**: `$.message`
  - **Value**: `{{ $input }}` (đảm bảo dữ liệu từ Webhook được truyền vào node **Generate Chat Completion**).

#### **3. Kích hoạt ⚡️**
1. **Test run dữ liệu mẫu**:
   - Gửi một tin nhắn mẫu (ví dụ: `"Hello, how are you?"`) qua Webhook để kiểm tra.
   - Kiểm tra kết quả trả về từ node **Return output**.
2. **Bật Active workflow**:
   - Nhấp vào nút **"Active"** ở góc trên bên phải của canvas.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết nối với Slack/Telegram**:
   - Sử dụng node **Slack Webhook** hoặc **Telegram Bot** để nhận tin nhắn từ các kênh này và truyền vào workflow.
2. **Lưu lịch sử chat vào Google Sheets**:
   - Thêm node **Google Sheets** sau node **Return output** để lưu tất cả các cuộc trò chuyện.
3. **Tự động gửi báo cáo định kỳ**:
   - Sử dụng node **Set** kết hợp với **HTTP Request** để gửi báo cáo tổng hợp về hiệu suất chatbot qua email.
4. **Cải thiện mô hình bằng Fine-tuning**:
   - Nếu các sếp có nhu cầu, có thể fine-tuning mô hình Dolphin Mixtral trên Novita để phù hợp với ngành nghề cụ thể.

---

### 📌 **Kết luận**
Workflow này giúp các sếp **tự động hóa chatbot AI với Dolphin Mixtral 8x22B trên Novita AI**, tiết kiệm chi phí và nâng cao hiệu suất tương tác khách hàng. **Không cần viết code, không phụ thuộc vào cloud đắt đỏ** – chỉ cần một VPS và một chút cấu hình!

**Hãy thử ngay và biến chatbot của mình thành một công cụ thông minh, riêng tư và hiệu quả!** 🚀

---
**🔗 [Xem workflow gốc tại n8n.io](https://n8n.io/workflows/6746)**
**📌 [Đăng ký Novita AI với mã giới thiệu](https://novita.ai/?ref=mze5m2e&utm_source=affiliate)**