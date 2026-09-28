---
title: "🚀 **Tự Động Hóa Theo Dõi SLA Zendesk + Escalation Tickets Với Slack & Google Sheets (N8n)**
**Giải pháp 24/7 theo dõi SLA, cảnh báo Slack & ghi log tự động - Không cần code!**"
description: "Workflow này tự động theo dõi tất cả ticket Zendesk đang mở, tính toán thời gian SLA còn lại, cảnh báo Slack khi SLA sắp hết hạn (75%+) và tự động nâng cấp độ ưu tiên (90%+), đồng thời ghi log vào Google Sheets để kiểm tra và báo cáo. Giúp đội ngũ hỗ trợ tránh vi phạm SLA và cải thiện hiệu suất phản hồi."
slug: "tieu-dong-ho-sla-zendesk-escalation-tickets"
tags: [n8n, automation, Zendesk, Slack, Google Sheets, SLA monitoring, ticket escalation, no-code, self-hosted]
keywords: [n8n workflow Zendesk, tự động hóa theo dõi SLA, cảnh báo Slack khi SLA hết hạn, ghi log ticket vào Google Sheets, tự động nâng cấp độ ưu tiên ticket, giải pháp hỗ trợ khách hàng 24/7]
---

# 🚀 **Tự Động Hóa Theo Dõi SLA Zendesk + Escalation Tickets Với Slack & Google Sheets**

### **Giải pháp nào giúp các sếp:**
- **Tránh vi phạm SLA** với cảnh báo tự động khi ticket sắp hết hạn (75%+).
- **Tự động nâng cấp độ ưu tiên** cho ticket nguy cơ vi phạm (90%+).
- **Ghi log tất cả hoạt động** vào Google Sheets để kiểm tra và báo cáo.
- **Tiết kiệm thời gian** với việc theo dõi tự động thay vì kiểm tra thủ công.
- **Cảnh báo Slack** ngay khi có ticket cần sự chú ý.

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tự động hóa theo dõi SLA 24/7** – Không cần người kiểm tra thủ công.
✅ **Cảnh báo Slack kịp thời** – Đội ngũ hỗ trợ biết ngay khi ticket sắp hết hạn.
✅ **Tự động nâng cấp độ ưu tiên** – Ticket nguy cơ vi phạm được ưu tiên cao.
✅ **Ghi log chi tiết** – Dữ liệu SLA được lưu vào Google Sheets cho báo cáo.
✅ **Giảm thiểu vi phạm SLA** – Hệ thống cảnh báo trước khi deadline đến.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow này hoạt động, các sếp cần chuẩn bị:
- **Tài khoản Zendesk** (API Key và credentials `zendeskApi`).
- **Tài khoản Slack** (API Key và credentials `slackApi`).
- **Tài khoản Google Sheets** (OAuth2 API Key và credentials `googleSheetsOAuth2Api`).
- **Google Sheet** đã tạo sẵn với tên Sheet là **"Stripe Data"** (Sheet1) và các cột: `ticket_id`, `percent_elapsed`, `time_remaining_minutes`, `timestamp`.
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/9829](https://n8n.io/workflows/9829) và import vào n8n Editor.
- **Cách 2:** Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/9829) và paste vào **Import Workflow** trong n8n Editor.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này có **13 node** quan trọng, các sếp cần cấu hình như sau:

#### **🔹 Node 1: Trigger Every Hour (Cron)**
- **Cấu hình:** `0 * * * *` (Chạy mỗi giờ).
- **Lưu ý:** Đảm bảo n8n đang chạy 24/7 (self-hosted).

#### **🔹 Node 2: Fetch Open Tickets from Zendesk**
- **Credentials:** Chọn `zendeskApi` (đã cấu hình trước).
- **Operation:** `getAll` (Lấy tất cả ticket).
- **Lưu ý:** Đảm bảo API Key có quyền truy cập vào tất cả ticket.

#### **🔹 Node 3: Filter: Open Tickets Only (If)**
- **Cấu hình:** Lọc chỉ ticket có `status = 'open'`.
- **Lưu ý:** Nếu không có ticket mở, workflow sẽ chuyển sang **Notify: No Open Tickets**.

#### **🔹 Node 4: Notify: No Open Tickets (Slack)**
- **Credentials:** Chọn `slackApi`.
- **Channel:** `general-information` (hoặc channel tùy chỉnh).
- **Lưu ý:** Thông báo này giúp đội ngũ biết tất cả ticket đã được giải quyết.

#### **🔹 Node 5: Calculate SLA Time Remaining (Function)**
- **Cấu hình:** Node này tự động tính toán:
  - `slaTotal` (thời gian SLA còn lại).
  - `timeRemainingMinutes` (thời gian còn lại tính bằng phút).
  - `percentElapsed` (tỷ lệ SLA đã qua, từ 0-100%).
- **Lưu ý:** Đảm bảo node này hoạt động chính xác với dữ liệu timestamp từ Zendesk.

#### **🔹 Node 6: Prepare Escalation Payload (Set)**
- **Cấu hình:** Điền thông tin nâng cấp độ ưu tiên:
  - `priority: 'High'`
  - `note: 'Auto-prioritised due to SLA nearing breach'`
- **Lưu ý:** Thông tin này sẽ được gửi đến Zendesk khi ticket sắp hết hạn.

#### **🔹 Node 7 & 8: Update Zendesk (Warning & Escalation)**
- **Credentials:** Chọn `zendeskApi`.
- **Operation:** `update` (cập nhật ticket).
- **Lưu ý:**
  - **Node 7 (75%+):** Nâng cấp độ ưu tiên và thêm ghi chú cảnh báo.
  - **Node 8 (90%+):** Nâng cấp độ ưu tiên cao và cảnh báo vi phạm SLA.

#### **🔹 Node 9 & 10: Alert Slack (Warning & Escalation)**
- **Credentials:** Chọn `slackApi`.
- **Channel:** `general-information` (hoặc tùy chỉnh).
- **Lưu ý:**
  - **Node 9 (75%+):** Cảnh báo Slack khi ticket còn 25% SLA.
  - **Node 10 (90%+):** Cảnh báo Slack khi ticket còn 10% SLA.

#### **🔹 Node 11: Log to Google Sheets**
- **Credentials:** Chọn `googleSheetsOAuth2Api`.
- **Operation:** `append` (thêm dữ liệu mới).
- **Lưu ý:**
  - Đảm bảo Sheet có tên **Stripe Data (Sheet1)** và các cột: `ticket_id`, `percent_elapsed`, `time_remaining_minutes`, `timestamp`.
  - Dữ liệu sẽ được ghi vào hàng mới mỗi khi có ticket cần cảnh báo.

#### **🔹 Node 12 & 13: If ≥ 75% (Warn) & If ≥ 90% (Escalate)**
- **Cấu hình:** Lọc dựa trên `percentElapsed`:
  - **≥ 75%:** Chuyển sang cảnh báo Slack và ghi log.
  - **≥ 90%:** Chuyển sang nâng cấp độ ưu tiên cao và cảnh báo Slack.

---
### **3. Kích hoạt ⚡️**
1. **Test Run:** Chạy thử với dữ liệu mẫu để kiểm tra logic.
2. **Active Workflow:** Bật chế độ **Active** để workflow chạy tự động mỗi giờ.

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁC Ý TƯỞNG MỞ RỘNG]
- **Kết hợp với Telegram:** Thay vì Slack, có thể gửi cảnh báo qua Telegram.
- **Gửi báo cáo định kỳ:** Sử dụng **n8n-nodes-base.email** để gửi báo cáo SLA hàng tuần.
- **Tích hợp với Jira:** Nếu sử dụng Jira, có thể tự động tạo ticket mới khi SLA vi phạm.
- **Ghi log vào Database:** Thay vì Google Sheets, có thể lưu vào **PostgreSQL** hoặc **MongoDB**.
- **Cảnh báo qua Email:** Sử dụng **n8n-nodes-base.email** để gửi cảnh báo cho quản lý.
:::

---
## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** để tự động hóa theo dõi SLA Zendesk, cảnh báo Slack và ghi log vào Google Sheets. **Không cần code**, chỉ cần cấu hình đúng credentials là workflow sẽ hoạt động 24/7, giúp đội ngũ hỗ trợ tránh vi phạm SLA và cải thiện hiệu suất phản hồi.

👉 **Bắt đầu tự động hóa ngay hôm nay!**
🔗 [Tải workflow từ n8n.io](https://n8n.io/workflows/9829)

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**Hãy áp dụng ngay và làm việc hiệu quả hơn!** 🚀