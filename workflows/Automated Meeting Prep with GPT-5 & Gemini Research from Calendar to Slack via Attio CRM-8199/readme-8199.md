---
title: "🤖 **Tự Động Hoàn Hảo Hẹn Phỏng Vấn với GPT-5 & Gemini: Từ Lịch Trình Đến Slack Qua Attio CRM**"
description: "Workflow tự động hóa chuẩn bị hẹn phỏng vấn AI tiên tiến, tích hợp Google Calendar, Gmail, Attio CRM và Slack để tự động nghiên cứu đối tác, tổng hợp thông tin và gửi báo cáo chuẩn bị chi tiết vào Slack hàng ngày. Giúp các sếp tiết kiệm 10+ giờ/tuần và chuẩn bị chuyên nghiệp cho mỗi cuộc họp."
slug: "tieu-dong-hoan-hao-phen-van-gpt-5-gemini-attio-slack"
tags: [n8n, automation, ai-summarization, crm-integration, slack-automation, google-calendar, gmail-api]
keywords: [tự động hóa hẹn phỏng vấn, n8n workflow, gemini 2.5 flash, gpt-5, attio crm, slack bot, google calendar api, ai research tool]
---

# 🚀 **Tự Động Hoàn Hảo Hẹn Phỏng Vấn với AI: Từ Lịch Trình Đến Slack Qua Attio CRM**

## **💡 Giới Thiệu: Tiết Kiệm 10+ Giờ/Tuần Cho Các Cuộc Hẹp Quý Giá**
Hàng ngày, các sếp phải mất **giờ đồng hồ** để:
- **Tìm kiếm thông tin** về đối tác từ email, lịch sử cuộc họp, và CRM.
- **Tổng hợp bối cảnh** về công ty, dự án, và mục tiêu của cuộc họp.
- **Chuẩn bị điểm nhấn** để cuộc họp diễn ra hiệu quả.
- **Gửi báo cáo** cho đồng nghiệp hoặc ghi chú sau cuộc họp.

**Workflow này giải quyết tất cả bằng AI!** Nó tự động:
✅ **Lấy dữ liệu** từ Google Calendar, Gmail, và Attio CRM.
✅ **Nghiên cứu sâu** về đối tác bằng GPT-5, Gemini, và Perplexity.
✅ **Tạo báo cáo chuẩn bị** với mục tiêu, điểm nhấn, và gợi ý.
✅ **Gửi báo cáo** vào Slack với định dạng chuyên nghiệp.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tuần** cho việc chuẩn bị cuộc họp.
- **Chuẩn bị chuyên nghiệp** với thông tin từ nhiều nguồn (CRM, email, lịch sử).
- **Cá nhân hóa** báo cáo cho từng đối tác và dự án.
- **Hoạt động tự động** hàng ngày (6h sáng, từ thứ 2 đến thứ 6).
- **Gửi báo cáo Slack** với định dạng Block Kit đẹp mắt.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Google Calendar** (OAuth2 credentials) – Để lấy lịch họp.
2. **Gmail** (OAuth2 credentials) – Để tra cứu email liên quan.
3. **Slack** (Bot token) – Để gửi báo cáo.
4. **Attio CRM** (Bearer Token) – Để quản lý thông tin đối tác.
5. **OpenRouter API Key** – Để sử dụng GPT-5, Gemini, và các mô hình AI khác.
6. **Perplexity API Key** – Để nghiên cứu bổ sung về đối tác.
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/8199](https://n8n.io/workflows/8199) hoặc copy/paste JSON vào **n8n Editor**.
- **Nhấn "Import"** và chọn **Self-hosted** (nếu tự cài đặt).

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow có **33 node** phức tạp, nhưng chỉ cần chú ý đến các phần sau:

#### **🔹 Node "Daily Weekday Trigger" (Định thời gian)**
- **Cron:** `0 6 * * 1-5` (6h sáng, từ thứ 2 đến thứ 6).
- **Không cần chỉnh** nếu muốn chạy theo lịch mặc định.

#### **🔹 Node "Fetch Today's Calendar Events" (Lấy lịch họp)**
- **Chỉnh "calendarEmail"** thành email của Google Calendar cá nhân.
- **Ví dụ:**
  ```json
  "calendarEmail": "your-calendar@group.calendar.google.com"
  ```

#### **🔹 Node "Slack Integration" (Gửi báo cáo Slack)**
- **Chỉnh `channelId`** trong node **"Send Meeting Brief to Slack"** thành ID của channel Slack.
- **Cách lấy ID channel:**
  1. Mở Slack > Channel > Nhấn **...** > **Copy link**.
  2. ID channel là phần sau `/channels/` (ví dụ: `C123ABC456`).

#### **🔹 Node "OpenRouter & AI Models" (Chọn mô hình AI)**
Workflow sử dụng **4 mô hình AI**:
| Node | Mô Hình AI | Ghi Chú |
|------|------------|---------|
| **Primary AI Model** | `google/gemini-2.5-flash` | Mô hình chính cho nghiên cứu. |
| **Secondary AI Model** | `openai/gpt-5` | Mô hình phụ (nếu Gemini không khả dụng). |
| **Fallback AI Model** | `openai/gpt-5-mini` | Mô hình dự phòng (rẻ hơn). |
| **Brief Optimizer** | `openai/gpt-5-mini` | Optimize báo cáo cuối cùng. |

- **Lưu ý:**
  - Nếu **GPT-5 không khả dụng**, thay bằng `openai/gpt-4o` hoặc `openai/gpt-4`.
  - **Gemini 2.5 Flash** phải được kích hoạt trên OpenRouter.

#### **🔹 Node "Attio CRM Integration" (Thông tin đối tác)**
- **Chỉnh `httpBearerAuth`** trong các node liên quan đến Attio:
  - **Attio List Notes Tool**
  - **Attio Search People Tool**
  - **Attio Read Notes Tool**
  - **Create New Person Record**
  - **Create Meeting Prep Note**
- **Ví dụ cấu hình:**
  ```json
  "httpBearerAuth": "Bearer YOUR_ATTIO_API_KEY"
  ```

#### **🔹 Node "Perplexity Research Tool" (Nghiên cứu bổ sung)**
- **Chỉnh `perplexityApi`** trong node này:
  ```json
  "perplexityApi": "Bearer YOUR_PERPLEXITY_API_KEY"
  ```
- **Mô hình:** `sonar-pro` (mô hình mạnh nhất của Perplexity).

---

### **3. Kích Hoạt ⚡️**
1. **Test Run** với một ngày có họp:
   - Chọn **1 cuộc họp mẫu** trong Google Calendar.
   - **Run node "Fetch Today's Calendar Events"** để kiểm tra.
2. **Bật Active** workflow sau khi kiểm tra thành công.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**

### **1. Tích Hợp với Zoom/Teams (Nâng Cao)**
- **Sử dụng node `zoomTool`** (n8n-zoom) để lấy thông tin cuộc họp từ Zoom.
- **Cách làm:**
  - Thêm node `zoomTool` sau "Fetch Today's Calendar Events".
  - Lấy `meetingId` từ Google Calendar và tra cứu chi tiết trên Zoom.

### **2. Lưu Log & Theo Dõi Chi Phí AI**
- **Thêm node `stickyNote`** sau mỗi AI model để ghi log:
  ```json
  {
    "operation": "create",
    "key": "ai_model_logs",
    "value": {
      "model": "{{ $node["Primary AI Model"].json["model"] }}",
      "input": "{{ $json["prompt"] }}",
      "output": "{{ $json["response"] }}",
      "timestamp": "{{ $node["Primary AI Model"].date }}"
    }
  }
  ```
- **Dùng node `googleSheets`** để lưu log vào bảng Excel.

### **3. Gửi Báo Cáo Email Thay Vì Slack**
- **Thay node `slack`** bằng `gmailTool` để gửi email tự động:
  ```json
  {
    "operation": "sendEmail",
    "to": "team@example.com",
    "subject": "Báo cáo chuẩn bị cuộc họp: {{ $json["event"]["summary"] }}",
    "body": "{{ $json["slackMessage"] }}"
  }
  ```

### **4. Tự Động Xóa Cuộc Hợp Không Cần Thiết**
- **Thêm node `if`** sau "Check if Person Exists in CRM":
  - Nếu **không tìm thấy người** trong CRM, **xóa cuộc họp** từ lịch.

---

## 📌 **Kết Luận: Áp Dụng Ngay Để Cuộc Hợp Đơn Giản Hơn!**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào **strategy** thay vì **chuẩn bị cuộc họp**. Với sự hỗ trợ của **GPT-5, Gemini, và Attio CRM**, mỗi cuộc họp đều được chuẩn bị **chuyên nghiệp, cá nhân hóa, và hiệu quả**.

**Bắt đầu ngay!**
1. **Import workflow** từ [n8n.io/workflows/8199](https://n8n.io/workflows/8199).
2. **Chỉnh các node quan trọng** (Google Calendar, Slack, Attio API).
3. **Bật Active** và **chờ AI làm việc** hàng ngày!

---
**💬 Cần hỗ trợ?** Đăng câu hỏi trên [Community n8n](https://community.n8n.io/) hoặc liên hệ với **TinoHost** để hỗ trợ cài đặt VPS!