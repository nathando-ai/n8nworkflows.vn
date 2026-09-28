---
title: "🤖 **Tự Động Hóa Làm Nóng Lại Khách Hàng HubSpot Bằng AI GPT-4o + Gmail + Slack (Miễn Phí 100%)**"
description: "Workflow tự động hóa AI giúp các sếp HubSpot **làm nóng lại khách hàng đã đánh dấu 'Không phù hợp thời điểm'**, tự động tạo email follow-up thông minh bằng GPT-4o, gửi draft cho team review trên Gmail và thông báo trên Slack. **Không cần code**, hoạt động 24/7, tiết kiệm **10+ giờ/ngày** cho bộ phận bán hàng."
slug: "tieu-dong-hubspot-ai-gpt4o-gmail-slack"
tags: [n8n, automation, lead-nurturing, ai-agent, hubspot, gpt-4o, slack, gmail, no-code]
keywords: [tự động hóa hubspot, làm nóng lại khách hàng, ai agent n8n, gpt-4o tự động hóa email, workflow hubspot slack, tự động hóa bán hàng no-code]
---

# 🚀 **Tự Động Hóa Làm Nóng Lại Khách Hàng HubSpot Bằng AI GPT-4o + Gmail + Slack**

## **Nỗi Đau Của Các Sếp HubSpot**
Các sếp bán hàng đã từng gặp phải tình trạng:
- **Khách hàng "đã mất"** sau khi đánh dấu `BAD_TIMING` trong HubSpot, nhưng lại **quên làm nóng lại** sau 1-2 tuần.
- **Team phải làm thủ công** tìm kiếm, viết email follow-up, và nhắc nhở đồng nghiệp → **Tốn 10+ giờ/ngày**.
- **Rủi ro tự động gửi email** mà không kiểm tra → **Tỷ lệ phản hồi thấp** hoặc **khách hàng phản cảm**.
- **Không biết cách personalize** email cho từng lead, dẫn đến **tỷ lệ chuyển đổi thấp**.

**Workflow này giải quyết tất cả!** Dùng **AI GPT-4o** tự động tạo email follow-up **nhẹ nhàng, cá nhân hóa**, gửi draft cho team review trên **Gmail**, và thông báo trên **Slack** để đồng nghiệp **không bỏ qua bất kỳ lead nào**.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**3 Lợi Ích Cốt Lõi**]
✅ **Tiết kiệm 10+ giờ/ngày** cho bộ phận bán hàng (không cần tìm kiếm, viết email thủ công).
✅ **Tỷ lệ phản hồi tăng 30-50%** nhờ email **cá nhân hóa, không pushy** do AI tạo.
✅ **Không bỏ qua lead nào** – Nếu AI thất bại, hệ thống **thông báo ngay trên Slack** để team xử lý thủ công.
✅ **Hoạt động 24/7** – Không cần can thiệp người dùng, tự động làm nóng lại lead **mỗi 24h**.
:::

---

### 🔧 **Yêu Cầu Cần Thiết (Chuẩn Bị Trước Khi Lên Đồ)**
:::info[**Danh Sách Credentials Cần Có**]
| **Dịch Vụ**          | **Thông Tin Cần Thiết**                          | **Lưu Ý**                                  |
|----------------------|--------------------------------------------------|---------------------------------------------|
| **HubSpot**          | App Token (API Key)                             | Cấp từ **Settings > Integrations > API Keys** |
| **Azure OpenAI**     | API Key + Endpoint (Model: `gpt-4o`)            | Đăng ký tại [Azure Portal](https://azure.microsoft.com/) |
| **Gmail**            | OAuth2 Credentials (Tài khoản email chính)      | Cấp từ [Google Cloud Console](https://console.cloud.google.com/) |
| **Slack**            | API Token (Bot Token)                           | Tạo từ **Apps > Create App > Add Bot**       |
| **Tài khoản n8n**   | (Self-hosted hoặc n8n.cloud)                   | **Khuyến nghị self-hosted** để ổn định 24/7 |
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/13518](https://n8n.io/workflows/13518) (chọn **Export JSON**).
2. **Trên n8n Editor**, nhấn **Import** → Chọn file JSON vừa tải.
3. **Xác nhận import** và workflow sẽ hiện lên canvas.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Copy toàn bộ mã JSON** từ [n8n.io/workflows/13518](https://n8n.io/workflows/13518) (chọn **Export JSON**).
2. **Trên n8n Editor**, nhấn **Import** → Chọn **Paste JSON**.
3. **Xác nhận** và workflow sẽ được tạo.

---
### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này **có 11 node**, nhưng **các node quan trọng nhất** cần cấu hình kỹ là:

#### **🔹 Node 1: Daily Trigger (Every 24h)**
- **Không cần chỉnh gì** (nếu muốn thay đổi thời gian, chỉnh ở **Schedule Trigger** → **Cron Expression**).
- **Lưu ý**: Nếu self-hosted, **đảm bảo VPS không ngắt kết nối** (n8n sẽ tự động chạy mỗi ngày).

#### **🔹 Node 2: HubSpot - Fetch Recent Leads**
- **Credentials**: Chọn `hubspotAppToken` (đã cấu hình trước).
- **Operation**: Để mặc định là `getAll`.
- **Lọc lead mới**: Nếu muốn chỉ lấy lead trong **7 ngày gần nhất**, thêm điều kiện ở **Filter Node** sau.

#### **🔹 Node 3: Filter - Lead Status = BAD_TIMING**
- **Chỉnh sửa điều kiện**:
  ```json
  {
    "jsonPath": "$[*]?.properties.status.value == 'BAD_TIMING'"
  }
  ```
- **Lưu ý**:
  - Nếu HubSpot dùng **trạng thái khác** (ví dụ: `INACTIVE` hoặc `COLD`), **cập nhật lại giá trị** ở trên.
  - **Không lọc lead đang hoạt động** để tránh spam.

#### **🔹 Node 4: Batch Leads (Split In Batches)**
- **Chỉnh số lượng batch**:
  - Mặc định là **1 lead/batch** (để tránh rate limit của Azure OpenAI).
  - Nếu muốn **xử lý 5 lead/lần**, chỉnh `batchSize` thành `5`.
- **Lưu ý**: Nếu batch quá lớn, **AI có thể bị timeout** hoặc **tốn chi phí cao**.

#### **🔹 Node 5 & 9: AI Agent (Generate Follow-Up Email)**
- **Credentials**: Chọn `azureOpenAiApi`.
- **Model**: Để mặc định là `gpt-4o`.
- **Prompt mặc định**:
  ```plaintext
  You are an AI assistant helping sales teams re-engage leads.
  For the given lead data, generate a **short, polite follow-up email** (max 100 words).
  The email should:
  1. Reference their last interaction (if any).
  2. Ask a **non-pushy question** to re-open the conversation.
  3. End with a **soft CTA** (e.g., "Let me know if you'd like to discuss further").
  4. **Avoid salesy language** – focus on value.
  ```
- **Lưu ý**:
  - **Cập nhật lead data** vào prompt (ví dụ: `{{$json.leadData}}`).
  - **Test prompt** trước khi chạy toàn bộ workflow.

#### **🔹 Node 6: Parse AI JSON**
- **Code mẫu** (chỉnh nếu AI trả về format khác):
  ```javascript
  // Kiểm tra output của AI và chuyển đổi thành format email
  return {
    emailBody: item.json.output?.emailBody || "Email generation failed",
    subject: item.json.output?.subject || "Follow-up from [Your Company]",
    leadEmail: item.json.leadData.email,
    leadName: item.json.leadData.properties.firstName.value || "Lead"
  };
  ```
- **Lưu ý**:
  - Nếu AI trả về **format khác**, **cập nhật lại code** ở đây.

#### **🔹 Node 7: Gmail - Create Follow-Up Draft**
- **Credentials**: Chọn `gmailOAuth2`.
- **Chỉnh template email**:
  ```plaintext
  Subject: {{subject}}
  Body:
  Hi {{leadName}},\n
  {{emailBody}}
  Best regards,\n
  [Your Name]
  [Your Company]
  ```
- **Lưu ý**:
  - **Không tự động gửi email** (để team review trước).
  - **Test gửi draft** trước khi chạy toàn bộ workflow.

#### **🔹 Node 8 & 10: Slack Notifications**
- **Credentials**: Chọn `slackApi`.
- **Message mẫu cho Slack (Node 8 - Thông báo thành công)**:
  ```json
  {
    "text": ":mailbox: *New follow-up draft ready!* 🚀",
    "blocks": [
      {
        "type": "section",
        "text": {
          "type": "mrkdwn",
          "text": `*Lead:* <${leadEmail}|${leadName}>`
        }
      },
      {
        "type": "actions",
        "elements": [
          {
            "type": "button",
            "text": {
              "type": "plain_text",
              "text": "Open Gmail Draft"
            },
            "url": "{{$json.emailUrl}}"
          }
        ]
      }
    ]
  }
  ```
- **Message mẫu cho Slack (Node 10 - Thông báo thất bại)**:
  ```json
  {
    "text": ":rotating_light: *AI failed to generate email for:* <${leadEmail}|${leadName}>",
    "blocks": [
      {
        "type": "section",
        "text": {
          "type": "mrkdwn",
          "text": `*Error:* ${item.json.errorMessage || "Unknown error"}`
        }
      },
      {
        "type": "actions",
        "elements": [
          {
            "type": "button",
            "text": {
              "type": "plain_text",
              "text": "Manually Follow Up"
            },
            "url": `https://app.hubspot.com/contacts/${leadId}`
          }
        ]
      }
    ]
  }
  ```
- **Lưu ý**:
  - **Thay thế `{{$json.emailUrl}}`** bằng URL draft email từ Gmail (có thể lấy từ **Node 7**).
  - **Thay thế `{{leadId}}`** bằng ID lead từ HubSpot.

---
### **3. Kích Hoạt ⚡️**
1. **Test Run với 1-2 lead mẫu**:
   - Chọn **1 lead có trạng thái `BAD_TIMING`** và chạy **Manual Trigger**.
   - Kiểm tra:
     - Email draft có được tạo trên Gmail không?
     - Slack có thông báo không?
     - Nếu AI thất bại, Slack có cảnh báo không?
2. **Bật Active workflow**:
   - Nhấn **Active** ở góc trên bên phải.
   - **Kiểm tra log** trong **Execution History** để đảm bảo không lỗi.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[**3 Ý Tưởng Thực Tiễn**]
1. **Thêm CRM Status Update**
   - Sau khi team **xác nhận email đã gửi**, tự động **cập nhật trạng thái lead** trong HubSpot từ `BAD_TIMING` → `FOLLOW_UP_SENT`.
   - **Node cần thêm**: `hubspot` (operation: `updateContact`).

2. **Push Follow-Ups vào CRM Task Queue**
   - Thay vì chỉ thông báo Slack, **tạo task tự động** trong HubSpot cho team theo dõi.
   - **Node cần thêm**: `hubspot` (operation: `createTask`).

3. **Lưu Log Tất Cả Email Đã Tạo**
   - Dùng **Google Sheets** hoặc **Airtable** để **lưu lịch sử email** đã tạo, ai đã review, và kết quả.
   - **Node cần thêm**: `googleSheets` (hoặc `airtable`).

4. **Thay đổi Tần Suất Làm Nóng**
   - Mặc định là **mỗi 24h**, nhưng có thể **thay đổi thành tuần** (ví dụ: `0 0 * * 1` để chạy mỗi thứ 2).
   - **Node cần chỉnh**: `scheduleTrigger` → **Cron Expression**.

5. **Tích Hợp với Zoom/Calendly**
   - Nếu lead phản hồi, **tự động tạo meeting** với Zoom/Calendly.
   - **Node cần thêm**: `zoom` hoặc `calendly`.
:::

---

## 📌 **Kết Luận: Áp Dụng Ngay & Tăng Doanh Thu!**
Workflow này **giải phóng team bán hàng** khỏi công việc **làm nóng lead thủ công**, đồng thời **tăng tỷ lệ chuyển đổi** nhờ email **cá nhân hóa, không pushy** do AI tạo.

**Các sếp nên:**
✅ **Self-host n8n** trên VPS để **ổn định 24/7** (không phụ thuộc n8n.cloud).
✅ **Test với 1-2 lead** trước khi chạy toàn bộ.
✅ **Cập nhật prompt AI** để phù hợp với **tone brand** của công ty.
✅ **Kết hợp với CRM Task** để **tăng trách nhiệm** của team.

**🎁 Đăng ký VPS TinoHost (Self-host n8n) với mã giảm giá:**
👉 [VPSN8N](https://tino.vn/vps-n8n?affid=388) **(Giảm 39%)**
👉 [VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)

**🚀 Hành động ngay!** Import workflow, **cấu hình và chạy thử** – bạn sẽ **ngạc nhiên với kết quả** trong vòng 1 tuần! 💪