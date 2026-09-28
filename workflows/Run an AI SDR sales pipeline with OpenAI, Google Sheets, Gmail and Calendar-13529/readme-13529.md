---
title: "🤖 **Tự Động Hóa Pipeline SDR AI: Từ Lead Đến Khách Hàng - Không Cần Code!**"
description: "Workflow n8n hoàn chỉnh tự động chuyển đổi leads thành khách hàng bằng AI (OpenAI), Google Sheets, Gmail và Calendar. Giúp các sếp tiết kiệm 10+ giờ/ngày theo dõi và gửi email tự động hóa 100%."
slug: "tieu-dong-hoa-pipeline-sdr-ai-voi-openai-google-sheets"
tags: [n8n, automation, sales, ai-chatbot, lead-nurturing, openai, google-sheets, gmail, google-calendar]
keywords: [tự động hóa sdrc, pipeline sdrc, workflow n8n ai, tự động hóa bán hàng, chatbot sdrc, openai cho doanh nghiệp, tự động hóa email bán hàng]
---

# 🚀 **Tự Động Hóa Pipeline SDR AI: Từ Lead Đến Khách Hàng - Không Cần Code!**

## **💡 Bạn đang gặp vấn đề gì?**
- **Tốn quá nhiều thời gian** để theo dõi leads từ Google Sheets, gửi email cá nhân hóa và cập nhật CRM?
- **Không biết cách tự động hóa** quá trình SDR (Sales Development Representative) mà không cần viết code?
- **Sợ quên gửi follow-up** hoặc gửi email không phù hợp với từng khách hàng?
- **Muốn một hệ thống tự động** chuyển đổi leads thành khách hàng mà không cần can thiệp thủ công?

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Nhập leads** từ Google Sheets vào CRM
✅ **Gửi 3 email follow-up cá nhân hóa** (bằng AI OpenAI) trong 48h
✅ **Dừng tự động** khi khách hàng đặt lịch hẹn
✅ **Gửi email reschedule** cho những người không đến cuộc gọi
✅ **Cập nhật CRM tự động** khi có sự kiện mới trên Google Calendar

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/ngày** theo dõi và gửi email thủ công.
- **Tăng tỷ lệ chuyển đổi** với email cá nhân hóa bằng AI.
- **Không quên gửi follow-up** nhờ hệ thống tự động.
- **Cập nhật CRM liên tục** khi có sự kiện mới.
- **Giảm công việc lặp lại** với 4 agent tự động (CRM, Follow-Up, Concierge, No-Show).
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Google Sheets** (để lưu lead list và CRM)
✔ **Tài khoản Gmail** (để gửi email tự động)
✔ **Tài khoản Google Calendar** (để theo dõi lịch hẹn)
✔ **API Key OpenAI** (để personalize email bằng AI)
✔ **VPS n8n** (để chạy workflow 24/7)
:::

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/13529](https://n8n.io/workflows/13529) hoặc copy JSON từ trang này.
- **Mở n8n Editor** → Nhấn **Import** → Dán JSON và nhấn **Import**.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **4 agent tự động** (CRM, Follow-Up, Concierge, No-Show). Dưới đây là các bước cấu hình quan trọng:

#### **📌 Agent 1: CRM Agent (Nhập leads từ Google Sheets)**
- **Node "Email List"**: Chỉ định **Google Sheet chứa leads** (cột cần có: `Name`, `Email`, `Company`, `Role`, `Industry`).
- **Node "Update CRM"**: Chỉ định **Google Sheet CRM** (cột cần có: `Status`, `Follow-Up Count`, `Last Email Sent`, `Call Scheduled`).

#### **📌 Agent 2: Follow-Up Agent (Gửi email tự động)**
- **Node "OpenAI Follow Up"**: Điền **API Key OpenAI** và cấu hình **prompt** để AI tạo email cá nhân hóa.
  ```json
  {
    "model": "gpt-4.1-nano",
    "messages": [
      {"role": "system", "content": "You are a professional sales assistant. Personalize this email for {Name} at {Company}."},
      {"role": "user", "content": "Email template: {Template}"}
    ]
  }
  ```
- **Node "Send First/Second/Third Follow Up"**: Chỉ định **Gmail OAuth2** và **địa chỉ email gửi** (ví dụ: `sales@doanhnghiep.com`).

#### **📌 Agent 3: Concierge Agent (Cập nhật khi có lịch hẹn)**
- **Node "Google Calendar Trigger"**: Chỉ định **Google Calendar** và **thời gian kích hoạt** (ví dụ: khi có sự kiện mới).
- **Node "Update CRM (Call Scheduled)"**: Cập nhật **trạng thái "Call Scheduled"** cho lead đó.

#### **📌 Agent 4: No-Show Agent (Gửi email reschedule)**
- **Node "Check for 'No Shows'"**: Lọc leads có **trạng thái "No Show"**.
- **Node "Send No-Show Follow-Up"**: Gửi email mời reschedule và cập nhật CRM.

---

### **3. Kích hoạt ⚡️**
- **Test run** với 1-2 lead mẫu để kiểm tra email và cập nhật CRM.
- **Bật Active workflow** và **đặt lịch chạy định kỳ** (ví dụ: CRM Agent chạy hàng ngày, Follow-Up Agent chạy mỗi 2 ngày).

---

## ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁC Ý TƯỞNG MỞ RỘNG]
- **Kết hợp với Slack/Telegram**: Gửi thông báo khi có lead mới hoặc email được gửi thành công.
- **Lưu log hoạt động**: Sử dụng **Google Sheets** hoặc **n8n Database** để theo dõi lịch sử.
- **Tăng cường AI**: Sử dụng **LangChain** để cải thiện logic personalization.
- **Gửi báo cáo định kỳ**: Tạo một **Google Sheet báo cáo** tổng hợp kết quả mỗi tháng.
:::

---

## 📌 **Kết luận**
Workflow này là **hệ thống SDR AI hoàn chỉnh**, giúp các sếp tự động hóa toàn bộ quá trình từ lead đến khách hàng. **Không cần code, không cần theo dõi thủ công** – chỉ cần cài đặt và chạy!

**🚀 Hãy áp dụng ngay và tiết kiệm thời gian cho đội ngũ bán hàng của mình!**

---
**💬 Cần hỗ trợ?** Hỏi ở [n8n Forum](https://community.n8n.io/) hoặc liên hệ tác giả [Vincent Nguyen](http://linkedin.com/in/vincentthenguyen/).