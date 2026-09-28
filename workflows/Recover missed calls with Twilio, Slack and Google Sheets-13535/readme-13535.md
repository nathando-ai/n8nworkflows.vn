---
title: "📞 Tự Động Hồi Phục Cuộc Gọi Trượt Với Twilio, Slack & Google Sheets - Không Cần Code!"
description: "Workflow tự động hóa hoàn toàn để thu hồi tất cả cuộc gọi trượt, gửi tin nhắn tự động qua Twilio, ghi chép chi tiết vào Google Sheets và thông báo ngay cho đội ngũ trên Slack. Giảm thiểu mất lead và cải thiện trải nghiệm khách hàng chỉ trong vài phút cài đặt."
slug: "tieu-dong-hoi-phuc-cuoc-goi-truoi-twilio-slack-google-sheets"
tags: [n8n, automation, no-code, lead-nurturing, twilio, slack, google-sheets, CRM, business-automation]
keywords: [tự động hóa cuộc gọi trượt, n8n workflow, thu hồi lead từ cuộc gọi, Twilio tự động hóa, Slack thông báo tự động, Google Sheets logging]
---

# 🚀 **Tự Động Hồi Phục Cuộc Gọi Trượt: Không Bỏ Qua Lead Nào!**

### **Nỗi Đau Của Các Sếp**
Bạn đã từng **bỏ lỡ cuộc gọi quan trọng** từ khách hàng tiềm năng chỉ vì không có ai nhận? Hay **không biết cách thu hồi** những cuộc gọi trượt để tiếp tục tương tác? Cuộc gọi trượt không chỉ là mất lead, mà còn là **mất cơ hội bán hàng** và **giảm trải nghiệm khách hàng**.

Với **n8n**, bạn có thể **tự động hóa hoàn toàn** quá trình hồi phục cuộc gọi trượt bằng cách:
✅ **Nhận cuộc gọi trượt từ Twilio** và phân loại chúng (bị treo, bận, không trả lời).
✅ **Kiểm tra xem cuộc gọi xảy ra trong giờ làm việc** để gửi tin nhắn phù hợp.
✅ **Ghi chép chi tiết cuộc gọi vào Google Sheets** để theo dõi và báo cáo.
✅ **Gửi tin nhắn tự động qua Twilio** để gọi lại khách hàng trong thời gian nhanh nhất.
✅ **Thông báo ngay cho đội ngũ trên Slack** để có thể xử lý kịp thời.

**Kết quả?** **Không mất lead nào**, **tăng tỷ lệ chuyển đổi** và **cải thiện trải nghiệm khách hàng** chỉ với một workflow đơn giản!

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài **n8n trên VPS riêng (Self-hosted)** để tránh giới hạn của phiên bản cloud.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Thu hồi 100% cuộc gọi trượt** → Không bỏ qua lead nào.
- **Tiết kiệm thời gian** → Không cần phải theo dõi thủ công.
- **Tin nhắn cá nhân hóa** → Gửi lời nhắc gọi lại nhanh chóng hoặc trong giờ làm việc.
- **Đội ngũ được thông báo ngay** → Có thể xử lý kịp thời.
- **Dữ liệu theo dõi chi tiết** → Ghi chép vào Google Sheets để báo cáo và phân tích.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản Twilio** (để nhận cuộc gọi và gửi tin nhắn).
✔ **Google Sheets** (để ghi chép chi tiết cuộc gọi).
✔ **Slack Workspace** (để thông báo cho đội ngũ).
✔ **API Keys & Credentials**:
   - **Twilio Account SID & Auth Token** (từ [Twilio Console](https://console.twilio.com/)).
   - **Google Sheets OAuth 2.0 API Key** (tạo từ [Google Cloud Console](https://console.cloud.google.com/)).
   - **Slack API Token** (tạo từ [Slack API](https://api.slack.com/apps)).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n Workflow](https://n8n.io/workflows/13535) hoặc copy toàn bộ JSON từ trang này.
- Mở **n8n Editor** → Nhấn **Import** → Chọn file JSON hoặc dán JSON vào ô nhập.
- **Xác nhận import** và workflow sẽ hiển thị trên canvas.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **9 node chính**, các sếp cần chú ý cấu hình sau:

##### **🔹 Node 1: Receive Missed Call Webhook (webhook)**
- **Cấu hình Webhook**:
  - **Path**: `missed-calls` (không thay đổi).
  - **HTTP Method**: `POST`.
  - **URL Webhook**: Đặt URL này trong **Twilio Console** (trong phần **Voice > Active Numbers > Webhooks**).
  - **Twilio phải gửi dữ liệu JSON** về workflow khi có cuộc gọi trượt.

##### **🔹 Node 2: Check Call Failed/Busy/No-Answer (if)**
- **Cấu hình điều kiện**:
  - Kiểm tra trường `status` trong dữ liệu Twilio:
    - **Bỏ qua** nếu `status = "answered"` (cuộc gọi đã được trả lời).
    - **Tiếp tục** nếu `status = "failed"`, `"busy"` hoặc `"no-answer"`.

##### **🔹 Node 3: Check Business Hours (code)**
- **Mở node Code** và chỉnh sửa logic để phù hợp với **giờ làm việc** của doanh nghiệp.
  - Ví dụ:
    ```javascript
    // Kiểm tra giờ hiện tại (UTC) và so sánh với giờ làm việc
    const now = new Date();
    const hour = now.getHours();
    const isBusinessHours = hour >= 8 && hour < 18; // Giờ làm việc từ 8h đến 18h
    return { isBusinessHours };
    ```
  - **Chú ý**: Đảm bảo **timezone** trong code phù hợp với khu vực của bạn.

##### **🔹 Node 4: Log Missed Call to Google Sheets (googleSheets)**
- **Chọn Credentials**: `googleSheetsOAuth2Api`.
- **Chọn Sheet & Tab**:
  - Tạo một **Google Sheet mới** với **tab "Missed Calls"**.
  - Cấu hình **Header Row** để n8n biết cách ghi dữ liệu.
- **Operation**: `append` (thêm mới dữ liệu).

##### **🔹 Node 5: Is It Business Hours? (if)**
- **Sử dụng kết quả từ Node Code** để quyết định gửi tin nhắn nào:
  - **Nếu trong giờ làm việc** → Gửi tin nhắn **"Call Back in 5 Minutes"**.
  - **Nếu ngoài giờ làm việc** → Gửi tin nhắn **"Will Contact in Business Hours"**.

##### **🔹 Node 6 & 7: SMS - Call Back in 5 Minutes / SMS - Will Contact in Business Hours (twilio)**
- **Chọn Credentials**: `twilioAccount`.
- **Cấu hình tin nhắn**:
  - **Body SMS**:
    - **Nếu trong giờ làm việc**:
      ```
      Xin chào! Chúng tôi đã nhận được cuộc gọi của bạn. Chúng tôi sẽ gọi lại trong 5 phút. Xin vui lòng đợi!
      ```
    - **Nếu ngoài giờ làm việc**:
      ```
      Xin chào! Chúng tôi đã nhận được cuộc gọi của bạn. Chúng tôi sẽ liên lạc lại trong giờ làm việc (8h-18h).
      ```
  - **From Number**: Chọn số Twilio đã đăng ký.

##### **🔹 Node 8: Notify Team on Slack (slack)**
- **Chọn Credentials**: `slackApi`.
- **Chọn Channel**: Chọn kênh Slack để thông báo.
- **Cấu hình Message**:
  ```json
  {
    "blocks": [
      {
        "type": "section",
        "text": {
          "type": "mrkdwn",
          "text": "*Missed Call Alert!* 🚨"
        }
      },
      {
        "type": "divider"
      },
      {
        "type": "section",
        "fields": [
          {
            "type": "mrkdwn",
            "text": "*Caller:*"
          },
          {
            "type": "mrkdwn",
            "text": `$$.json["From"]`
          }
        ]
      },
      {
        "type": "section",
        "fields": [
          {
            "type": "mrkdwn",
            "text": "*Status:*"
          },
          {
            "type": "mrkdwn",
            "text": `$$.json["status"]`
          }
        ]
      },
      {
        "type": "actions",
        "elements": [
          {
            "type": "button",
            "text": {
              "type": "plain_text",
              "text": "Follow Up"
            },
            "url": `https://your-crm.com/callers/$$.json["From"]`
          }
        ]
      }
    ]
  }
  ```
  - **Thay `your-crm.com`** bằng liên kết CRM hoặc trang liên hệ của bạn.

---

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Gửi một cuộc gọi trượt **mẫu** từ Twilio để kiểm tra workflow.
  - Kiểm tra:
    - **Google Sheets** có ghi dữ liệu không?
    - **Slack** có thông báo không?
    - **Twilio** có gửi tin nhắn không?
- **Bật Active**:
  - Sau khi kiểm tra thành công, **bật workflow** để hoạt động liên tục.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Thêm Logs & Báo Cáo Hàng Ngày**:
   - Sử dụng **node `dateTime`** để tính toán số cuộc gọi trượt trong ngày.
   - Gửi **báo cáo tự động** qua Slack hoặc Email hàng ngày.

2. **Kết Nối Với CRM (HubSpot, Salesforce, Zoho)**:
   - Sau khi ghi chép vào Google Sheets, **sử dụng node `webhook`** để gửi dữ liệu lên CRM tự động.

3. **Tự Động Gọi Lại Sau 5 Phút**:
   - Sử dụng **Twilio Call Node** để gọi lại khách hàng sau 5 phút (nếu trong giờ làm việc).

4. **Phân Loại Lead Theo Đơn Vị**:
   - Thêm **node `code`** để phân loại lead theo ngành nghề (ví dụ: "Doanh nghiệp", "Cá nhân") và gửi tin nhắn phù hợp.

5. **Thông Báo Trên Telegram**:
   - Sử dụng **node `telegram`** để gửi thông báo cùng với Slack.

---

### 📌 **Kết Luận**
Workflow này **giải quyết triệt để** vấn đề mất lead từ cuộc gọi trượt, giúp doanh nghiệp **tăng tỷ lệ chuyển đổi** và **cải thiện trải nghiệm khách hàng** một cách **tự động hóa hoàn toàn**.

**Hành động ngay!**
1. **Cài đặt n8n trên VPS** (để workflow chạy 24/7).
2. **Import workflow** và cấu hình các node theo hướng dẫn.
3. **Test & Bật Active** để bắt đầu thu hồi lead ngay!

**Bạn đã sẵn sàng không bỏ qua lead nào nữa?** 🚀

---
**🔗 [Tải workflow nguyên bản từ n8n](https://n8n.io/workflows/13535)**
**📌 [Cài đặt n8n Self-hosted](https://docs.n8n.io/hosting/self-hosting-on-a-vps/)**