---
title: "🤖 **Tự Động Hóa Scoring Leads + Gửi Proposal qua WhatsApp với Gemini AI, HighLevel & Apify – Không Cần Code!**"
description: "Workflow tự động hóa 100% miễn phí giúp các sếp phân loại leads thông minh bằng AI Gemini, tạo cơ hội bán hàng trên HighLevel, và gửi proposal tự động qua WhatsApp – tiết kiệm thời gian lên đến 80% cho bộ phận marketing & sales."
slug: "tieu-dong-hoa-scoring-leads-whatsapp-gemini-highlevel"
tags: [n8n, automation, lead-generation, ai-chatbot, highlevel, whatsapp-business-api, gemini-ai, no-code]
keywords: [n8n workflow leads, tự động hóa scoring leads, gemini ai n8n, gửi proposal whatsapp tự động, highlevel automation, apify n8n]
---

# 🚀 **Tự Động Hóa Scoring Leads + Gửi Proposal qua WhatsApp với Gemini AI, HighLevel & Apify**

Hiện nay, các sếp marketing và sales phải mất **giờ đồng hồ** để:
- **Lọc và phân loại leads** thủ công (rất dễ bị bỏ sót hoặc sai lầm).
- **Tạo cơ hội bán hàng (opportunities)** trên HighLevel một cách rườm rà.
- **Gửi proposal qua WhatsApp** một cách không đồng bộ, mất thời gian phản hồi.
- **Trả lời khách hàng** qua WhatsApp một cách không cá nhân hóa.

**Workflow này giải quyết tất cả!** Sử dụng **AI Gemini** để phân loại leads, **HighLevel** để quản lý cơ hội bán hàng, và **WhatsApp Business API** để gửi proposal tự động – **không cần viết một dòng code nào!**

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[**LỢI ÍCH CỐT LÕI**]
✅ **Tiết kiệm 80% thời gian** cho bộ phận marketing & sales.
✅ **Phân loại leads chính xác** bằng AI Gemini (không còn sai lầm thủ công).
✅ **Tạo cơ hội bán hàng tự động** trên HighLevel (upsert contact + update opportunity).
✅ **Gửi proposal qua WhatsApp** ngay khi lead được phân loại.
✅ **Trả lời khách hàng tự động** qua WhatsApp với AI hỗ trợ (sử dụng Redis để nhớ lịch sử chat).
✅ **Cá nhân hóa tương tác** với khách hàng dựa trên phân tích AI.
✅ **Hoạt động 24/7** – không cần người thủ công.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[**CHUẨN BỊ**]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản HighLevel** (để quản lý contact và opportunity).
2. **API Key HighLevel OAuth2** (cài đặt trong [HighLevel Developer Portal](https://developers.highlevel.com/)).
3. **WhatsApp Business API** (đăng ký tại [Meta Developer](https://developers.facebook.com/)).
4. **API Key Google Gemini** (cài đặt tại [Google AI Studio](https://aistudio.google.com/)).
5. **Redis Server** (để lưu lịch sử chat cho AI Customer Service).
6. **Tài khoản Apify** (nếu muốn sử dụng actor AI bổ sung).
7. **Tài khoản Telegram** (để nhận thông báo nếu cần).
8. **URL Webhook** (để nhận dữ liệu leads từ form, CRM, hoặc API khác).
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/16173](https://n8n.io/workflows/16173) và import vào **n8n Editor**.
- **Copy JSON** từ link trên và paste vào **Import Workflow** trong n8n.

:::note[**Lưu ý quan trọng**]
- **Không copy/paste trực tiếp từ trang web** (sẽ bị lỗi syntax). Mở file JSON và copy toàn bộ nội dung.
- **Nên cài n8n trên VPS** để workflow hoạt động 24/7 (không bị ngắt kết nối).
:::

---
### **2. Các bước cấu hình BẮT BUỘC phải chỉnh 📌**

#### **A. Cấu hình Webhook (Nhận leads từ bên ngoài)**
1. **Node: "When New Lead Received" (webhook)**
   - **Path:** `newlead` (không đổi).
   - **HTTP Method:** `POST`.
   - **URL Webhook:** Sử dụng URL của n8n (ví dụ: `https://tên-domain-n8n.com/webhook/newlead`).
   - **Lưu ý:** Cấu hình URL này trong **form, CRM, hoặc API** bạn sử dụng để gửi leads.

#### **B. Cấu hình Google Gemini AI**
1. **Node: "Gemini Chat Model" (lmChatGoogleGemini)**
   - **Credentials:** Chọn `googlePalmApi` (đã tạo trước).
   - **Prompt:** Các sếp có thể **tùy chỉnh** prompt để phù hợp với ngành nghề (ví dụ: "Phân loại lead này là loại nào: A (hot), B (lạnh), hoặc C (không phù hợp)?").
   - **API Key:** Điền vào **Credentials** của n8n (tạo từ Google AI Studio).

2. **Node: "Customer Service Agent" (agent)**
   - **Credentials:** Chọn `googlePalmApi` (cùng API Key với trên).
   - **Prompt:** Cấu hình để AI trả lời khách hàng một cách tự động (ví dụ: "Trả lời tin nhắn này của khách hàng với tone chuyên nghiệp và đề xuất giải pháp").

#### **C. Cấu hình HighLevel (Quản lý contact & opportunity)**
1. **Credentials HighLevel OAuth2**
   - Tạo trong **n8n Credentials** với:
     - **Client ID & Secret** từ HighLevel Developer Portal.
     - **Scope:** `contacts, opportunities, messages`.

2. **Node: "Create Opportunity" / "Update Opportunity"**
   - **Resource:** `opportunity`.
   - **Operation:** `create` (hoặc `update`).
   - **Tham số cần điền:**
     - `name` (tên cơ hội).
     - `contactId` (ID contact liên quan).
     - `stage` (bước tiến trình, ví dụ: "Prospecting", "Proposal Sent").
     - `value` (giá trị dự kiến).
     - `description` (mô tả cơ hội).

#### **D. Cấu hình WhatsApp Business API**
1. **Credentials WhatsApp API**
   - Tạo trong **n8n Credentials** với:
     - **Phone Number ID** từ Meta Developer.
     - **Access Token** (nếu cần).

2. **Node: "Send WhatsApp Template A/B"**
   - **Template Name:** Chọn template đã tạo trên WhatsApp Business Manager.
   - **Parameters:** Điền biến động (`{{firstName}}`, `{{proposal}}`, etc.) từ dữ liệu lead.

#### **E. Cấu hình Redis (Lưu lịch sử chat AI)**
1. **Node: "Get Redis Chat History" (memoryRedisChat)**
   - **Credentials:** Chọn `redis`.
   - **Host/Port:** Địa chỉ Redis (ví dụ: `redis://your-redis-server:6379`).
   - **Password:** Nếu có.

#### **F. Cấu hình Telegram (Thông báo nếu cần)**
1. **Node: "Send Telegram Message" (telegramTool)**
   - **Credentials:** Chọn `telegramApi`.
   - **Chat ID:** ID chat của bạn (tìm bằng `@userinfobot` trên Telegram).
   - **Message:** Thông báo tự động khi có lead mới hoặc phản hồi từ khách hàng.

#### **G. Cấu hình Apify (Nếu sử dụng)**
1. **Node: "Fetch Google AI Lead Overview" (apify)**
   - **Credentials:** Chọn `apifyApi`.
   - **Actor:** Chọn actor AI bạn muốn sử dụng (ví dụ: "Google Search" hoặc "Lead Analysis").
   - **Input Data:** Điền dữ liệu lead từ trước.

---
### **3. Kích hoạt ⚡️ Workflow**
1. **Test Run** với dữ liệu mẫu:
   - Gửi một **POST request** đến Webhook với dữ liệu lead mẫu (ví dụ:
     ```json
     {
       "name": "Nguyễn Văn A",
       "email": "a@example.com",
       "phone": "+84123456789",
       "message": "Tôi muốn mua dịch vụ SEO cho doanh nghiệp."
     }
     ```
   - Kiểm tra các **node** hoạt động như thế nào (AI phân loại, HighLevel update, WhatsApp gửi proposal).

2. **Bật Active** workflow sau khi kiểm tra thành công.

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::info[**CÁCH TIẾP CẬN THÊM**]
1. **Kết hợp với Slack/Telegram**
   - Thêm node `slackTool` để thông báo lead mới vào channel Slack.
   - Ví dụ: `"Lead mới được phân loại: {{leadType}} - {{contactName}}"` → Slack.

2. **Lưu log hoạt động**
   - Sử dụng node `stickyNote` để ghi lại lịch sử hoạt động của workflow (ví dụ: "Lead ABC đã gửi proposal lúc 10:00").

3. **Gửi báo cáo định kỳ**
   - Tạo một **cron job** trong n8n để gửi báo cáo số liệu leads hàng ngày qua Email hoặc WhatsApp.

4. **Tùy chỉnh AI prompt**
   - Đối với **Lead Processor Agent**, các sếp có thể thêm:
     ```plaintext
     "Nếu lead này có từ khóa 'urgent', hãy ưu tiên gửi proposal ngay và cập nhật stage thành 'Proposal Sent' trong HighLevel."
     ```

5. **Sử dụng Apify để tra cứu thêm thông tin**
   - Ví dụ: Dùng actor Apify để tra cứu **tên công ty** của lead từ Google và thêm vào HighLevel.
:::

---
## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn:
✔ **Tự động hóa toàn bộ quy trình từ nhận leads đến gửi proposal**.
✔ **Tiết kiệm thời gian** cho bộ phận marketing & sales.
✔ **Cải thiện tỷ lệ chuyển đổi** với AI phân loại leads chính xác.
✔ **Cá nhân hóa tương tác** với khách hàng qua WhatsApp.

**Hành động ngay!**
1. **Cài n8n trên VPS** (để workflow hoạt động 24/7).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).

2. **Import workflow** và **cấu hình theo hướng dẫn**.
3. **Test với dữ liệu mẫu** và **bật Active**.

**Không cần code, không cần chuyên gia IT – chỉ cần n8n!** 🚀

---
**Cần hỗ trợ?** Liên hệ tác giả:
👉 [Calendly của Abhi Vaar](https://cal.com/abhi.vaar/n8n) (để đặt lịch tư vấn chi tiết).