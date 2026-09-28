---
title: "🤖 Tự Động Hóa Quá Trình Tuyển Dụng Trên WhatsApp Với AI OpenAI - Giảm 80% Thời Gian Phỏng Vấn"
description: "Workflow này tự động hóa toàn bộ quy trình tuyển dụng từ nhận ứng viên, đánh giá AI, lịch phỏng vấn đến thông báo kết quả - hoàn toàn không cần code. Giúp HR tiết kiệm 80% thời gian so với cách làm thủ công."
slug: "tuyen-dung-whatsapp-ai-openai"
tags: [n8n, automation, recruitment, ai-chatbot, openai, whatsapp-business-api]
keywords: [tự động hóa tuyển dụng WhatsApp, AI tuyển dụng, n8n workflow tuyển dụng, tự động hóa phỏng vấn, OpenAI tuyển dụng, CRM tuyển dụng]
---

# 🚀 **Tự Động Hóa Tuyển Dụng Trên WhatsApp Với AI OpenAI - Giảm 80% Thời Gian Phỏng Vấn**

### **Giải pháp hoàn hảo cho HR, tuyển dụng và các doanh nghiệp cần tuyển dụng hiệu quả mà không cần code**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động 24/7 mà không gián đoạn, các sếp nên **self-host n8n trên VPS** để đảm bảo tính bảo mật và ổn định cao nhất.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## **🎯 Kết quả các sếp nhận được**
Workflow này **tự động hóa toàn bộ quy trình tuyển dụng** từ nhận ứng viên đến thông báo kết quả, giúp các sếp:
- **Tiết kiệm 80% thời gian** so với cách làm thủ công (không cần đánh giá từng hồ sơ một).
- **Chọn ứng viên phù hợp** nhờ AI OpenAI đánh giá dựa trên tiêu chí tuyển dụng tự động hóa.
- **Lịch phỏng vấn tự động** theo sẵn thời gian của ứng viên và sếp.
- **Cập nhật trạng thái tuyển dụng** tự động qua WhatsApp (đã phỏng vấn, đã tuyển, từ chối).
- **Lưu toàn bộ lịch sử** vào Google Sheets (CRM) để theo dõi dễ dàng.

---

## **🔧 Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✅ **Twilio WhatsApp Business API** (hoặc **Meta WhatsApp Cloud API**) để nhận và gửi tin nhắn.
✅ **OpenAI API Key** (để sử dụng GPT-4.1-mini trong quá trình đánh giá và thông báo).
✅ **Google Calendar API** (để lịch phỏng vấn tự động).
✅ **Google Sheets** (để lưu trữ CRM tuyển dụng).
✅ **SendGrid hoặc Gmail** (để gửi email backup nếu cần).

---

## **🚀 Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/15620](https://n8n.io/workflows/15620) và import vào **n8n Editor**.
- **Cách 2:** Copy toàn bộ JSON từ link trên và dán vào **Import Workflow** trong n8n.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **27 node**, nhưng các sếp chỉ cần chú ý đến các phần sau:

#### **🔹 Node Webhook - WhatsApp Inbound**
- **Cấu hình:**
  - **Path:** `whatsapp-recruitment-inbound`
  - **HTTP Method:** `POST`
  - **Credentials:** Cấu hình **Twilio WhatsApp API** hoặc **Meta WhatsApp Cloud API** để nhận tin nhắn ứng viên.

#### **🔹 Node AI - Screen Candidate (OpenAI Agent)**
- **Cấu hình:**
  - **Model:** `gpt-4.1-mini` (đã được thiết lập sẵn).
  - **Credentials:** Điền **OpenAI API Key** vào `openAiApi`.
  - **Prompt:** Các sếp có thể **tùy chỉnh tiêu chí tuyển dụng** trong node này (ví dụ: kinh nghiệm, kỹ năng, mức lương mong muốn).

#### **🔹 Node Python - Generate Interview Slots**
- **Cấu hình:**
  - **Logic:** Node này tự động tạo các slot phỏng vấn dựa trên sẵn thời gian của ứng viên và sếp.
  - **Lưu ý:** Các sếp cần **cập nhật sẵn availability** (thời gian sẵn sàng phỏng vấn) trong node này.

#### **🔹 Node Send WhatsApp - Interview Slots**
- **Cấu hình:**
  - **Credentials:** Điền **Twilio WhatsApp API Key** vào `httpBasicAuth`.
  - **Tham số:** Đảm bảo **phone number** của ứng viên được truyền đúng.

#### **🔹 Node Book Calendar Event (Google Calendar)**
- **Cấu hình:**
  - **Credentials:** Đăng ký **Google Calendar API** và cấp quyền cho n8n.
  - **Event Details:** Tự động tạo sự kiện phỏng vấn với tiêu đề, thời gian và mô tả.

#### **🔹 Node Update CRM - Google Sheet**
- **Cấu hình:**
  - **Credentials:** Đăng ký **Google Sheets API** và chọn **Sheet Name** để lưu trữ CRM.
  - **Dữ liệu:** Workflow sẽ tự động cập nhật trạng thái ứng viên (đã phỏng vấn, đã tuyển, từ chối).

#### **🔹 Node AI - Generate Hiring Update**
- **Cấu hình:**
  - **Model:** `gpt-4.1-mini` (đã được thiết lập sẵn).
  - **Credentials:** Điền **OpenAI API Key** vào `openAiApi`.
  - **Prompt:** AI sẽ tự động tạo tin nhắn thông báo kết quả phỏng vấn.

---

### **3. Kích hoạt ⚡️**
- **Test Run:** Chạy thử với **dữ liệu mẫu** (ví dụ: tin nhắn WhatsApp giả lập).
- **Bật Active:** Sau khi kiểm tra, **bật workflow** để hoạt động 24/7.

---

## **✍️ Mẹo & gợi ý nâng cao**
1. **Tùy chỉnh tiêu chí tuyển dụng:**
   - Mở node **AI - Screen Candidate** và chỉnh sửa **prompt** để phù hợp với yêu cầu tuyển dụng cụ thể của công ty.

2. **Thêm Slack/Telegram báo cáo:**
   - Sử dụng **node HTTP Request** để gửi thông báo kết quả phỏng vấn lên Slack/Telegram.

3. **Lưu log toàn bộ quá trình:**
   - Thêm **node Set** để lưu trữ log vào Google Sheets hoặc Firebase.

4. **Tự động gửi email xác nhận:**
   - Kết hợp với **SendGrid** hoặc **Gmail** để gửi email xác nhận phỏng vấn.

---

## **📌 Kết luận**
Workflow này **giải phóng HR khỏi công việc nhọc nhằn** trong tuyển dụng, giúp **tự động hóa từ nhận ứng viên đến thông báo kết quả** một cách chính xác và hiệu quả. **Không cần code, không cần kỹ thuật**, chỉ cần **cấu hình và chạy** là xong!

**🚀 Hãy áp dụng ngay và tiết kiệm 80% thời gian tuyển dụng!** 🚀

---
**🔹 Cần hỗ trợ thêm?**
- **Join nhóm Telegram n8n Việt Nam** để trao đổi: [n8n Vietnam](https://t.me/n8nvietnam)
- **Đăng ký VPS n8n** để tự host: [TinoHost](https://tino.vn/vps-n8n?affid=388) (Mã giảm giá: **VPSN8N**)