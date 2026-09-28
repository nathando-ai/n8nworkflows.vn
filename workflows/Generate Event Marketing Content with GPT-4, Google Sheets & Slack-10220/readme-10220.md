---
title: "🚀 Tự Động Hóa Tạo Nội Dung Marketing Event Với GPT-4, Google Sheets & Slack – Không Cần Code!"
description: "Workflow này tự động tạo nội dung email, bài đăng mạng xã hội và copy quảng cáo cho sự kiện từ thông tin cơ bản, tiết kiệm thời gian cho các sếp marketing 90% công việc thủ công. Kết quả: Nội dung cá nhân hóa, chuyên nghiệp, và được gửi tự động đến email và Slack."
slug: "tu-dong-hoa-tao-noi-dung-marketing-event-gpt4-google-sheets-slack"
tags: [n8n, automation, content-creation, marketing-automation, ai-gpt4, google-sheets, slack-integration]
keywords: [n8n workflow marketing, tự động hóa nội dung sự kiện, GPT-4 tạo nội dung, Slack tự động hóa marketing, Google Sheets lưu trữ campaign]
---

# 🚀 **Tự Động Hóa Tạo Nội Dung Marketing Event Với GPT-4, Google Sheets & Slack**

### **🔥 Bỏ T Tay Thủ Công!**
Hãy tưởng tượng: Một sự kiện quan trọng sắp diễn ra, nhưng bạn phải viết **email chào mời**, **bài đăng trên LinkedIn, Instagram, Facebook, Twitter**, và **copy quảng cáo cho Google/Facebook** trong vòng **1 tiếng**? Thời gian quý giá của các sếp marketing bị "chôn vùi" trong công việc thủ công, trong khi nội dung không được tối ưu hóa cho từng platform.

**Workflow này giải quyết tất cả!**
Chỉ cần **gửi thông tin sự kiện** (tên, ngày giờ, địa điểm, đối tượng mục tiêu) qua **Webhook**, n8n sẽ tự động:
✅ **Tạo email cá nhân hóa** với subject, body, CTA và dòng PS khuyến khích.
✅ **Sinh ra 4 bài đăng mạng xã hội** (LinkedIn, Twitter, Instagram, Facebook) với tone phù hợp.
✅ **Tạo copy quảng cáo** cho Google Search, Facebook Ads và LinkedIn Sponsored.
✅ **Gửi toàn bộ nội dung** đến **email** và **Slack** để team review.
✅ **Lưu lịch sử campaign** vào **Google Sheets** để theo dõi hiệu quả.

---
### **🎯 Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian** so với viết thủ công.
- **Nội dung chuyên nghiệp** được tối ưu cho từng platform.
- **Hoạt động 24/7** – không cần can thiệp thủ công.
- **Dữ liệu campaign được lưu trữ** trên Google Sheets, dễ dàng phân tích.
- **Team marketing được thông báo tức thời** qua Slack.
:::

---
### **🔧 Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **API Key GPT-4** (hoặc mô hình AI tương tự) để gọi API tạo nội dung.
   - *Lưu ý:* Workflow sử dụng **OpenAI API**, các sếp cần đăng ký tại [OpenAI](https://platform.openai.com/) và cung cấp API key.
2. **Google Sheets** với:
   - **Tên Sheet:** `Marketing_Campaigns`
   - **File ID:** `5x4w3v2u1t0s9r8q` (các sếp phải tạo sheet mới và chia sẻ cho n8n với quyền **Editor**).
3. **Tài khoản SMTP** để gửi email (ví dụ: Gmail, SendGrid, Mailgun).
4. **Credentials Slack**:
   - **Token Slack API** (tạo tại [API Slack](https://api.slack.com/apps)).
   - **Channel ID** của nhóm `#marketing-updates` (ví dụ: `C11223MARKETING`).
:::

---
### **🚀 Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow:
- **Tải file JSON** từ [n8n.io/workflows/10220](https://n8n.io/workflows/10220) và import vào **n8n Editor**.
- **Copy/paste JSON** từ link trên vào **Create Workflow** trong n8n.

:::note[LƯU Ý]
- **Không sử dụng phiên bản n8n Community miễn phí** nếu muốn chạy 24/7. **Self-hosted** là lựa chọn ổn định nhất.
- **Đăng ký VPS** với **n8n.io** để tự động hóa không ngừng nghỉ:
  👉 [VPS TinoHost (Mã giảm giá: **VPSN8N** - 39% off)](https://tino.vn/vps-n8n?affid=388)
  👉 [VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này **không hoạt động ngay** sau khi import. Các sếp cần cấu hình **các node quan trọng** sau:

##### **🔹 Webhook Trigger (Gửi thông tin sự kiện)**
- **Path:** `create-event-content` (không thay đổi).
- **HTTP Method:** `POST`.
- **Test:** Gửi request từ **Postman** hoặc **công cụ API testing** với payload:
  ```json
  {
    "event_name": "Hội nghị Marketing 2024",
    "date": "2024-12-15",
    "time": "09:00 AM - 05:00 PM",
    "location": "Sài Gòn Convention Center",
    "target_audience": "Marketing Manager, Brand Manager, Digital Marketer"
  }
  ```

##### **🔹 HTTP Request Nodes (Gọi API GPT-4)**
- **3 node** này (`Generate Email Content`, `Generate Social Posts`, `Generate Ad Copy`) **cần cấu hình API key**:
  - **URL:** `https://api.openai.com/v1/chat/completions` (hoặc mô hình AI khác).
  - **Headers:**
    ```json
    {
      "Authorization": "Bearer YOUR_OPENAI_API_KEY",
      "Content-Type": "application/json"
    }
    ```
  - **Body (Prompt):**
    - **Email:** `"Tạo email chào mời sự kiện [event_name] cho [target_audience]. Nội dung phải bao gồm: subject hấp dẫn, body giới thiệu chi tiết, CTA rõ ràng, và dòng PS khuyến khích đăng ký."`
    - **Social Posts:** `"Tạo 4 bài đăng cho [event_name] phù hợp với [platform] (LinkedIn/Twitter/Instagram/Facebook). Tone chuyên nghiệp, có hashtag và CTA."`
    - **Ad Copy:** `"Tạo copy quảng cáo cho [platform] (Google/Facebook/LinkedIn) với budget [assumed budget, e.g., 500k VND]. Nội dung phải ngắn gọn, hấp dẫn và có CTA mạnh mẽ."`

##### **🔹 Code Nodes (Parse Response)**
- **3 node** này (`Parse Email Response`, `Parse Social Response`, `Parse Ad Response`) **cần JavaScript** để xử lý JSON trả về từ API.
  *Ví dụ code cho `Parse Email Response`:*
  ```javascript
  // Xử lý response từ OpenAI và trả về JSON chuẩn
  const response = JSON.parse($input.all().response);
  return {
    json: {
      subject: response.choices[0].message.content.split("\n")[0],
      body: response.choices[0].message.content.split("\n").slice(1).join("\n"),
      cta: response.choices[0].message.content.split("CTA:")[1].split("\n")[0],
      ps: response.choices[0].message.content.split("PS:")[1]
    }
  };
  ```

##### **🔹 Google Sheets (Lưu lịch sử campaign)**
- **Credentials:** Chọn `googleApi` đã cấu hình trước.
- **Sheet Name:** `Marketing_Campaigns` (không thay đổi).
- **Headers (cột):**
  ```
  Event Name | Date | Email Subject | LinkedIn Post | Twitter Post | Instagram Post | Facebook Post | Google Ad Copy | Facebook Ad Copy | LinkedIn Ad Copy
  ```

##### **🔹 Email Send (Gửi nội dung)**
- **Credentials:** Chọn `smtp` đã cấu hình (ví dụ: Gmail).
- **To:** `events@company.com`
- **CC:** `marketing-team@company.com`
- **Subject:** `"[CAMPAIGN] Nội dung sự kiện: ${{ $json.event_name }}"`
- **Body:** Nội dung email từ node `Parse Email Response`.

##### **🔹 Slack Notification (Thông báo team)**
- **Credentials:** Chọn `slackApi` đã cấu hình.
- **Channel:** `#marketing-updates` (ID: `C11223MARKETING`).
- **Message:** `"🚀 Nội dung sự kiện [{{ $json.event_name }}] đã được tạo!\n\n- Email: {{ $json.subject }}\n- LinkedIn: {{ $json.linkedin_post }}\n- Slack: <{{ $input.all().url }}|Xem chi tiết>"`

---
### **✍️ Mẹo & gợi ý nâng cao**
:::tip[NÂNG CAO HỆ THỐNG]
1. **Kết hợp với Zapier/Integromat** để tự động lấy thông tin sự kiện từ **Google Calendar** hoặc **Eventbrite**.
2. **Lưu log hoạt động** vào **Google Drive** hoặc **Notion** để theo dõi hiệu suất.
3. **Tự động gửi báo cáo tuần** về campaign qua **email** hoặc **Slack**.
4. **Sử dụng mô hình AI khác** (ví dụ: Mistral AI, BARD) nếu OpenAI API quá đắt.
5. **Tối ưu prompt** để nội dung phù hợp với **đối tượng mục tiêu** cụ thể (ví dụ: B2B vs B2C).
:::

---
### **📌 Kết luận**
Workflow này **giải phóng thời gian** cho các sếp marketing để tập trung vào **strategy** thay vì viết nội dung thủ công. **Chỉ cần 1 lần setup**, hệ thống sẽ tự động tạo và phân phối nội dung cho **tất cả channel** trong giây lát.

**👉 Hãy import ngay và thử nghiệm!**
Nếu có vấn đề, các sếp có thể **comment bên dưới** hoặc liên hệ với **Oneclick AI Squad** qua [GitHub](https://github.com/oneclickai).

---
**💡 Chúc các sếp thành công với chiến dịch marketing mới!** 🚀