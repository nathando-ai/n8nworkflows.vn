---
title: "🚀 Tự Động Hóa Khôi Phục Giao Dịch Trệ Chệ HubSpot Với AI OpenAI, Gmail, Slack & Google Sheets"
description: "Workflow tự động hóa 24/7 phát hiện và khôi phục giao dịch trệ chệ trong HubSpot bằng AI, gửi email cá nhân hóa, cảnh báo Slack và theo dõi toàn bộ hoạt động. Giúp doanh nghiệp không bỏ lỡ bất kỳ cơ hội nào và tối ưu hóa quy trình bán hàng."
slug: "tieu-dong-hoa-khoi-phuc-giao-dich-trce-hubspot-ai"
tags: [n8n, automation, no-code, HubSpot, AI, Gmail, Slack, GoogleSheets, sales-funnel]
keywords: [tự động hóa HubSpot, AI khôi phục giao dịch, email cá nhân hóa, Slack alert, Google Sheets tracking, workflow n8n]
---

# 🚀 **Tự Động Hóa Khôi Phục Giao Dịch Trệ Chệ HubSpot Với AI – Không Bỏ Qua Bất Kỳ Cơ Hội Nào!**

### **Nỗi Đau Của Các Sếp?**
Bạn đã từng **bỏ lỡ giao dịch** vì không theo dõi kịp thời? Hay **tốn thời gian** để viết email cá nhân hóa cho từng khách hàng trệ chệ? Với workflow này, **AI sẽ tự động phát hiện và khôi phục giao dịch** trong HubSpot, gửi email cá nhân hóa, cảnh báo Slack và theo dõi toàn bộ hoạt động – **không cần viết một dòng code nào!**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Khôi phục giao dịch trệ chệ tự động** (không bỏ lỡ bất kỳ cơ hội nào)
✅ **Email cá nhân hóa** dựa trên lịch sử và giai đoạn giao dịch (AI OpenAI)
✅ **Cảnh báo Slack** cho đội bán hàng ngay khi có hành động
✅ **Theo dõi toàn bộ hoạt động** trên Google Sheets (dễ dàng phân tích)
✅ **Báo cáo tổng hợp hàng ngày** trên Slack (không bị lạm email)
✅ **Xử lý lỗi tự động** (Slack alert khi có vấn đề)
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản HubSpot** (API Key hoặc OAuth)
✔ **Tài khoản Gmail** (để gửi email tự động)
✔ **Tài khoản Slack** (để cảnh báo đội bán hàng và lỗi)
✔ **Google Sheet** (để lưu log hoạt động, cấu trúc như sau):
   | Date       | Deal Name   | Contact Email | Stage  | Days Stalled | Email Sent | Slack Notified | Status |
   |------------|------------|----------------|-------|--------------|------------|-----------------|---------|
✔ **API Key OpenAI** (để AI sinh email cá nhân hóa)
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/16077](https://n8n.io/workflows/16077) hoặc copy JSON từ canvas.
- Mở **n8n Editor**, nhấn **"Import"** và dán JSON.
- **Hoặc** tải file `.json` từ [đây](https://example.com/link-to-json) (nếu có).

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow có **17 node**, các sếp cần chú ý cấu hình sau:

##### **🔹 Node "Get All Open Deals" (HubSpot)**
- Chọn **credentials HubSpot** đã thiết lập trước.
- **Operation:** `getAll` (resource: `deal`).
- **Filter:** Lọc giao dịch **mở (open)** và **không hoạt động trong 7+ ngày**.

##### **🔹 Node "Filter Stalled Deals" (Code)**
- **Logic:** Lọc giao dịch có `lastActivityDate` < `7 ngày trước`.
- **Output:** Danh sách giao dịch trệ chệ.

##### **🔹 Node "Has Associated Contact?" (If)**
- **Nếu không có liên hệ:** Gửi đến **"Log Skipped — No Contact"** (Google Sheets).
- **Nếu có liên hệ:** Tiếp tục xử lý.

##### **🔹 Node "Has Valid Email?" (If)**
- **Nếu email không hợp lệ:** Gửi đến **"Log Skipped — No Email"** (Google Sheets).
- **Nếu email hợp lệ:** Tiến hành sinh email AI.

##### **🔹 Node "Generate Re-Engagement Email" (OpenAI)**
- **Prompt AI:** Sử dụng **Lịch sử giao dịch, tên khách hàng, công ty, giai đoạn và giá trị giao dịch** để sinh email cá nhân hóa.
- **Ví dụ Prompt:**
  ```
  Tôi là AI hỗ trợ bán hàng. Viết một email cá nhân hóa để khôi phục giao dịch trệ chệ với khách hàng [Tên Khách Hàng] từ [Công Ty]. Giao dịch đang ở giai đoạn [Stage] với giá trị [Value]. Đảm bảo email thân thiện, ngắn gọn và có call-to-action rõ ràng.
  ```

##### **🔹 Node "Send Re-Engagement Email" (Gmail)**
- Chọn **credentials Gmail** đã thiết lập.
- **Subject:** "Khôi phục giao dịch [Deal Name]"
- **Body:** Nội dung email từ OpenAI.

##### **🔹 Node "Slack Alert to Sales Team"**
- **Channel:** Chọn kênh Slack dành cho đội bán hàng.
- **Message Format:**
  ```
  🚨 **Giao dịch trệ chệ được khôi phục!**
  - **Tên Giao Dịch:** [Deal Name]
  - **Khách Hàng:** [Contact Name] ([Email])
  - **Giai Đoạn:** [Stage]
  - **Email đã gửi:** ✅
  ```

##### **🔹 Node "Error Alert to Slack"**
- **Channel:** Chọn kênh **lỗi** (ví dụ: `#n8n-errors`).
- **Message:** Chi tiết lỗi (ví dụ: "Lỗi Gmail khi gửi email cho [Email]").

##### **🔹 Node "Build Daily Digest" (Code)**
- **Logic:** Tóm tắt tất cả giao dịch đã xử lý trong ngày (bao gồm:
  - Số giao dịch khôi phục
  - Số giao dịch bị bỏ qua
  - Số lỗi
- **Gửi Slack:** Kênh tổng hợp (ví dụ: `#daily-summary`).

---

#### **3. Kích Hoạt ⚡️**
- **Test Run:** Chạy thử với **1-2 giao dịch mẫu** để kiểm tra email và Slack.
- **Bật Active:** Sau khi kiểm tra thành công, **bật workflow** và chọn **lịch trình hàng ngày** (ví dụ: 7h sáng).

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với CRM khác:**
   - Thay HubSpot bằng **Pipedrive** hoặc **Salesforce** bằng cách thay đổi node `hubspot` thành `pipedrive` hoặc `salesforce`.

2. **Tự động cập nhật Google Sheets:**
   - Thêm **node `googleSheets.update`** để cập nhật trạng thái giao dịch thay vì chỉ append.

3. **Gửi báo cáo định kỳ cho CEO:**
   - Sử dụng **node `email`** để gửi báo cáo hàng tuần cho quản lý.

4. **Tăng cường AI với LangChain:**
   - Nếu muốn **tối ưu hóa email hơn**, thay node `openAi` bằng **LangChain** để sử dụng **chất lượng AI cao hơn**.

5. **Lưu log chi tiết hơn:**
   - Thêm **node `stickyNote`** để ghi chú thêm thông tin vào giao dịch HubSpot.

---

### 📌 **Kết Luận**
Workflow này **giải quyết vấn đề trệ chệ giao dịch** một cách **tự động, cá nhân hóa và hiệu quả**. Các sếp không cần lo lắng về việc **bỏ lỡ khách hàng** hoặc **tốn thời gian viết email** – **AI và tự động hóa sẽ làm tất cả!**

👉 **Hãy import ngay và bắt đầu khôi phục giao dịch trong vòng 10 phút!**
🔗 [Tải workflow từ n8n.io](https://n8n.io/workflows/16077)

---
**Chia sẻ ý kiến hoặc cần hỗ trợ cấu hình?** Để lại comment bên dưới! 🚀