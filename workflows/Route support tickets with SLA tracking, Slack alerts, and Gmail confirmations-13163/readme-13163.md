---
title: "🚀 Tự Động Hóa Hệ Thống Hỗ Trợ Khách Hàng Với Theo Dõi SLA, Cảnh Báo Slack & Xác Nhận Email (N8N)"
description: "Workflow này tự động nhận, phân loại, theo dõi SLA và gửi cảnh báo cho đội ngũ hỗ trợ, đồng thời gửi xác nhận email tự động cho khách hàng - giải pháp hoàn hảo cho doanh nghiệp cần giảm thiểu thời gian phản hồi và cải thiện trải nghiệm khách hàng."
slug: "tieu-dong-hoa-he-thong-ho-tro-khach-hang-sla-slack-gmail"
tags: [n8n, automation, ticket-management, slack, gmail, sla-tracking, no-code]
keywords: [n8n workflow hỗ trợ khách hàng, tự động hóa ticket, theo dõi SLA, cảnh báo Slack, xác nhận email tự động, giải pháp hỗ trợ khách hàng]
---

# 🚀 **Tự Động Hóa Hệ Thống Hỗ Trợ Khách Hàng Với Theo Dõi SLA, Cảnh Báo Slack & Xác Nhận Email**

### **Giải pháp hoàn hảo cho doanh nghiệp cần phản hồi nhanh chóng và giảm thiểu thời gian chờ đợi khách hàng**

Hiện nay, hầu hết doanh nghiệp phải mất nhiều thời gian để quản lý hệ thống ticket hỗ trợ khách hàng thủ công: phân loại yêu cầu, theo dõi thời gian phản hồi (SLA), gửi cảnh báo cho đội ngũ và xác nhận với khách hàng. Kết quả là **trải nghiệm khách hàng bị gián đoạn**, **tỷ lệ giải quyết ticket chậm** và **tốn nhiều nguồn lực** của bộ phận IT/CS.

**Workflow này giải quyết tất cả vấn đề trên bằng cách:**
✅ **Tự động nhận ticket** từ webhook (hoặc email, form web)
✅ **Phân loại ticket** theo mức độ ưu tiên (Critical, High, Medium, Low)
✅ **Theo dõi SLA** (thời gian phản hồi tối đa) và cảnh báo tự động
✅ **Gửi xác nhận email** cho khách hàng khi ticket được xử lý
✅ **Cảnh báo Slack** cho đội ngũ hỗ trợ khi có ticket mới hoặc quá hạn SLA
✅ **Tránh trùng lặp ticket** bằng kiểm tra API

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần phải theo dõi ticket thủ công, tự động phân loại và gửi cảnh báo.
- **Cải thiện trải nghiệm khách hàng**: Xác nhận email tự động và phản hồi nhanh chóng.
- **Theo dõi SLA hiệu quả**: Cảnh báo Slack khi ticket quá hạn, đảm bảo không có ticket bị bỏ quên.
- **Giảm trùng lặp ticket**: Kiểm tra trước khi tạo ticket mới.
- **Tự động hóa hoàn toàn**: Không cần code, chỉ cần cấu hình.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Slack**:
   - API Token (Slack App Token) từ [Slack API](https://api.slack.com/apps).
   - Channel Slack để gửi cảnh báo (ví dụ: `#support-tickets`).
2. **Tài khoản Gmail**:
   - Email chính thức của doanh nghiệp (ví dụ: `support@doanhnghiep.com`).
   - App Password (nếu sử dụng 2FA) từ [My Account Google](https://myaccount.google.com/security).
3. **Webhook URL**:
   - URL để nhận ticket từ khách hàng (có thể từ form web, email, hoặc API).
4. **API Key (nếu cần)**:
   - Nếu sử dụng API bên thứ ba để kiểm tra trùng lặp ticket (ví dụ: API của CRM như HubSpot, Zoho, hoặc cơ sở dữ liệu nội bộ).
5. **N8n Self-hosted**:
   - Workflow này yêu cầu n8n được cài đặt trên máy chủ riêng (không thể chạy trên n8n.cloud miễn phí).
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/13163](https://n8n.io/workflows/13163) hoặc copy toàn bộ JSON từ trang này.
- Mở **n8n Editor** (trên máy chủ self-hosted của bạn).
- Nhấn **Import** và dán JSON vào hoặc tải file JSON đã tải xuống.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **22 node** và có nhiều bước quan trọng cần cấu hình cẩn thận. Dưới đây là hướng dẫn chi tiết:

##### **A. Cấu hình Webhook (Node "New Ticket")**
- **URL Webhook**: Đặt URL này trong form web, email, hoặc API của bạn để nhận ticket.
- **Method**: Chọn `POST`.
- **Headers**: Thêm `Content-Type: application/json`.
- **Payload Example**:
  ```json
  {
    "subject": "Ticket về vấn đề thanh toán",
    "description": "Tôi không thể thanh toán được trên trang web",
    "email": "khachhang@example.com",
    "priority": "high"
  }
  ```
  *(Lưu ý: Cấu trúc này phải khớp với logic trong node "Normalize Data")*

##### **B. Cấu hình Slack (Node "Notify Team" và "Error Alert")**
1. **Tạo Slack App**:
   - Truy cập [Slack API](https://api.slack.com/apps) → Tạo một app mới.
   - Chọn **OAuth & Permissions** → Thêm scope:
     - `chat:write` (để gửi tin nhắn)
     - `channels:read` (để đọc channel)
   - Sau khi tạo, copy **Bot Token** (trong **Basic Information**).
2. **Cấu hình trong n8n**:
   - Trong node **Slack**, chọn **Credentials** → Tạo mới.
   - Nhập **Token**: `xoxb-your-bot-token`.
   - **Channel**: Nhập `#support-tickets` (hoặc channel của bạn).

##### **C. Cấu hình Gmail (Node "Send Confirmation")**
1. **Tạo App Password**:
   - Bật **2FA** cho tài khoản Gmail.
   - Truy cập [My Account Google](https://myaccount.google.com/security) → **App Password** → Tạo mật khẩu ứng dụng.
2. **Cấu hình trong n8n**:
   - Trong node **Gmail**, chọn **Credentials** → Tạo mới.
   - **Email**: `support@doanhnghiep.com`.
   - **Password**: App Password vừa tạo.
   - **Subject**: `Xác nhận ticket #{{$node["New Ticket"].json["id"]}} đã được nhận`.
   - **Body**:
     ```html
     <p>Chúng tôi đã nhận được ticket của bạn về <strong>{{$node["New Ticket"].json["subject"]}}</strong>.</p>
     <p>Số ticket: <strong>{{$node["New Ticket"].json["id"]}}</strong></p>
     <p>Trạng thái: <strong>{{$node["Create Ticket"].json["status"]}}</strong></p>
     ```

##### **D. Cấu hình API Kiểm Tra Trùng Lặp (Node "Check Duplicate")**
- Nếu bạn sử dụng **CRM hoặc cơ sở dữ liệu nội bộ**, cần cấu hình node **HTTP Request**:
  - **Method**: `POST` hoặc `GET`.
  - **URL**: API endpoint của CRM (ví dụ: `https://api.hubspot.com/crm/v3/objects/tickets`).
  - **Headers**:
    ```json
    {
      "Authorization": "Bearer YOUR_API_KEY",
      "Content-Type": "application/json"
    }
    ```
  - **Body**:
    ```json
    {
      "properties": {
        "email": "{{$node["New Ticket"].json["email"]}}",
        "subject": "{{$node["New Ticket"].json["subject"]}}"
      }
    }
    ```
  - **Response Handling**: Nếu API trả về ticket trùng lặp, workflow sẽ **bỏ qua** và trả về lỗi 400.

##### **E. Cấu hình SLA (Node "Assign SLA")**
- Trong node **Code**, sửa logic để đặt thời gian SLA phù hợp với doanh nghiệp:
  ```javascript
  // Ví dụ: Critical = 1 giờ, High = 4 giờ, Medium = 24 giờ, Low = 72 giờ
  const sla = {
    critical: 1 * 60 * 60 * 1000, // 1 giờ (ms)
    high: 4 * 60 * 60 * 1000,    // 4 giờ
    medium: 24 * 60 * 60 * 1000, // 24 giờ
    low: 72 * 60 * 60 * 1000     // 72 giờ
  };
  return { sla: sla[$node["Categorize Ticket"].json.priority] };
  ```

##### **F. Cấu hình Phân Loại Ticket (Node "Categorize Ticket")**
- Trong node **Code**, sửa logic phân loại ticket theo nội dung:
  ```javascript
  const keywords = {
    critical: ["nguy hiểm", "khẩn cấp", "hỏng hóc", "dữ liệu mất"],
    high: ["chậm", "không phản hồi", "thanh toán thất bại"],
    medium: ["cập nhật", "thông tin", "hướng dẫn"],
    low: ["thắc mắc", "yêu cầu", "gợi ý"]
  };

  let priority = "low";
  for (const [key, value] of Object.entries(keywords)) {
    if (value.some(word => $node["New Ticket"].json.description.toLowerCase().includes(word))) {
      priority = key;
      break;
    }
  }
  return { priority };
  ```

##### **G. Cấu hình Cảnh Báo Slack Khi Quá Hạn SLA**
- Trong node **Switch** (`Route by Priority`), thêm logic cảnh báo Slack khi ticket quá hạn:
  ```javascript
  // Trong node "Notify Team", thêm logic sau:
  if ($node["Create Ticket"].json.sla_expired) {
    return {
      text: `⚠️ TICKET QUÁ HẠN SLA!\n\n- ID: {{$node["Create Ticket"].json.id}}\n- Chủ đề: {{$node["Create Ticket"].json.subject}}\n- Email: {{$node["Create Ticket"].json.email}}\n- SLA: {{$node["Create Ticket"].json.priority}} (quá hạn {{($node["Create Ticket"].json.sla_expired_time - Date.now()) / 1000 / 60}} phút)`,
      channel: "#support-alerts"
    };
  }
  ```

---

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Gửi một ticket mẫu qua webhook (hoặc sử dụng Postman).
   - Kiểm tra:
     - Ticket có được tạo không?
     - Slack có nhận được cảnh báo không?
     - Email xác nhận có được gửi không?
     - SLA có được tính toán đúng không?
2. **Bật Active**:
   - Sau khi test thành công, chuyển workflow sang **Active**.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với CRM**:
   - Thay vì tạo ticket trong n8n, hãy **gửi ticket trực tiếp đến CRM** (HubSpot, Zoho, Salesforce) bằng node **HTTP Request**.
   - Cấu hình **webhook trả về** từ CRM để n8n biết ticket đã được xử lý.

2. **Lưu Log Tickets**:
   - Sử dụng node **StickyNote** hoặc **Database** (n8n-nodes-base.database) để lưu lịch sử ticket.
   - Ví dụ: Lưu vào Google Sheets hoặc cơ sở dữ liệu MySQL.

3. **Gửi Báo Cáo Định Kỳ**:
   - Sử dụng **n8n Scheduler** để chạy workflow hàng ngày/tuần để gửi báo cáo tổng hợp:
     - Số ticket mới.
     - Ticket quá hạn SLA.
     - Ticket đã giải quyết.

4. **Tích Hợp với AI Tóm Tắt**:
   - Sử dụng node **LLM** (n8n-nodes-base.llm) để tự động tóm tắt nội dung ticket và gợi ý giải pháp.
   - Ví dụ:
     ```javascript
     // Trong node "Normalize Data", thêm logic gọi API LLM:
     const response = await fetch("https://api.openai.com/v1/chat/completions", {
       method: "POST",
       headers: { "Authorization": `Bearer ${OPEN_AI_KEY}` },
       body: JSON.stringify({
         messages: [{ role: "user", content: `$node["New Ticket"].json.description` }],
         model: "gpt-3.5-turbo"
       })
     });
     const data = await response.json();
     return { summary: data.choices[0].message.content };
     ```

5. **Tự Động Phân Chia Ticket**:
   - Sử dụng node **Switch** để phân chia ticket cho thành viên cụ thể trong Slack/Teams:
     ```javascript
     // Ví dụ: Phân ticket Critical cho @support-critical
     const assignee = priority === "critical" ? "@support-critical" : "@support-general";
     return { assignee };
     ```

---

### 📌 **Kết luận**
Workflow này **giải phóng đội ngũ hỗ trợ khỏi công việc thủ công**, giúp họ tập trung vào việc giải quyết vấn đề thay vì quản lý ticket. Với **Slack alerts, SLA tracking và email confirmations tự động**, doanh nghiệp sẽ **cải thiện đáng kể trải nghiệm khách hàng** và **tăng hiệu suất hỗ trợ**.

**Hành động ngay:**
1. **Cài đặt n8n self-hosted** trên VPS (dùng mã giảm giá **VPSN8N**).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Test và bật Active** để tự động hóa hệ thống hỗ trợ của bạn!

**Cần hỗ trợ thêm?** Đừng ngần ngại comment bên dưới hoặc liên hệ với tác giả [Manu](https://n8n.io/workflows/13163) để có hướng dẫn chi tiết hơn!

---