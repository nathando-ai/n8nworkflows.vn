---
title: "🚀 Tự Động Nhận Thông Báo Cập Nhật Sự Kiện Calendly Mới Nhất - Không Cần Code!"
description: "Giải pháp tự động hóa hoàn hảo để các sếp không bỏ lỡ bất kỳ sự kiện mới trên Calendly, ngay cả khi đang ngủ. Nhận thông báo tức thời qua email, Slack hay ứng dụng di động."
slug: "tu-dong-nhan-thong-bao-cap-nhat-su-kien-calendly"
tags: [n8n, automation, calendly, no-code, business-automation]
keywords: [tự động hóa calendly, nhận thông báo sự kiện calendly, workflow n8n, tự động hóa không code, tự động hóa sự kiện online]
---

# 🚀 **Tự Động Nhận Thông Báo Cập Nhật Sự Kiện Calendly - Không Cần Code!**

### **Giải pháp cho các sếp không muốn bỏ lỡ bất kỳ một sự kiện quan trọng nào!**
Các sếp đã từng gặp phải tình huống này chưa? Bạn đã đặt lịch hẹn trên **Calendly**, nhưng vì quá bận rộn hoặc quên kiểm tra thường xuyên, mà **bỏ lỡ thông báo mới nhất** về sự kiện? Hay thậm chí, bạn phải **lặp lại công việc thủ công** để theo dõi các thay đổi như hủy, hoãn, hoặc cập nhật chi tiết sự kiện?

**Workflow này sẽ giúp các sếp:**
✅ **Tự động nhận thông báo tức thời** khi có sự kiện mới hoặc thay đổi trên Calendly.
✅ **Không cần code** – chỉ cần cài đặt và chạy 24/7.
✅ **Tiết kiệm thời gian** bằng cách loại bỏ việc kiểm tra thủ công.
✅ **Hoạt động liên tục**, ngay cả khi các sếp đang ngủ hoặc bận công việc khác.

---
### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Không bỏ lỡ bất kỳ sự kiện nào** – Nhận thông báo ngay khi có thay đổi (tạo mới, hủy, cập nhật).
- **Tiết kiệm thời gian** – Không cần phải truy cập Calendly liên tục để kiểm tra.
- **Tự động hóa hoàn toàn** – Workflow chạy 24/7, không cần can thiệp thủ công.
- **Dễ dàng mở rộng** – Có thể kết nối với Slack, Email, hoặc Telegram để nhận thông báo ngay trên ứng dụng di động.
:::

---
### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow này hoạt động, các sếp cần:
1. **Tài khoản Calendly** (đã đăng ký và sử dụng).
2. **API Key của Calendly** (cần tạo trong tài khoản Calendly).
   - **Cách tạo API Key:**
     - Đăng nhập vào [Calendly Dashboard](https://calendly.com/).
     - Tiến đến **Settings (Cài đặt)** → **Integrations (Kết nối)** → **API Keys**.
     - Tạo một **API Key mới** và sao lưu nó (không thể lấy lại nếu mất).
3. **Tài khoản n8n** (cài đặt trên máy chủ riêng hoặc sử dụng n8n Cloud).
   - **👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)** để tự host n8n ổn định 24/7.
   - **👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (nếu cần cấu hình cao).

---
### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Workflow này chỉ có **1 node** duy nhất: **Calendly Trigger**, giúp theo dõi tất cả sự kiện mới hoặc thay đổi trên Calendly.

**Cách import:**
- Truy cập [n8n Editor](https://n8n.io/editor).
- Nhấp vào **"Import"** → **"From JSON"** và dán mã JSON từ [link gốc](https://n8n.io/workflows/540).
- Hoặc tải file JSON từ [đây](https://n8n.io/workflows/540/download) và import trực tiếp.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
:::warning[CẤU HÌNH QUAN TRỌNG]
- **Node: Calendly Trigger**
  - **Credentials:** Chọn **"calendlyApi"** (nếu chưa tạo, thêm mới trong **Credentials Manager** của n8n).
  - **API Key:** Điền **API Key** của Calendly (đã tạo ở phần **Yêu cầu cần thiết**).
  - **Event Types (Loại Sự Kiện):** Chọn tất cả hoặc chỉ những loại sự kiện cần theo dõi (ví dụ: `created`, `updated`, `cancelled`).
  - **Webhook URL (Nếu muốn kết nối thêm):** Nếu muốn nhận thông báo qua Webhook (ví dụ gửi đến Slack, Email), cần cấu hình thêm sau này.

:::note[LƯU Ý]
- Workflow này **chỉ theo dõi sự kiện mới hoặc thay đổi**, nhưng **không tự động gửi thông báo** (ví dụ qua Email/Slack). Các sếp cần **mở rộng workflow** bằng các node như:
  - **n8n-nodes-base.email** (gửi Email tự động).
  - **n8n-nodes-base.slack** (gửi thông báo Slack).
  - **n8n-nodes-base.telegram** (gửi thông báo Telegram).
  - **n8n-nodes-base.httpRequest** (gửi thông báo đến API cá nhân).

---

#### **3. Kích hoạt ⚡️**
1. **Test Run (Kiểm tra thử):**
   - Nhấp vào nút **"Run"** để kiểm tra workflow với dữ liệu mẫu.
   - Nếu không có sự kiện mới, có thể **simulate** bằng cách tạo một sự kiện mới trên Calendly và kiểm tra lại.
2. **Bật Active:**
   - Sau khi kiểm tra thành công, nhấp vào **"Active"** để workflow chạy liên tục.

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁCH MỞ RỘNG WORKFLOW]
1. **Gửi thông báo qua Email:**
   - Thêm **node Email** sau **Calendly Trigger** để tự động gửi Email khi có sự kiện mới.
   - Cấu hình:
     - **From:** `noreply@tênđômin.com`
     - **To:** Email của các sếp.
     - **Subject:** `🚨 Thông báo sự kiện Calendly mới: {{ $node["Calendly Trigger"].json["event"]["title"] }}`
     - **Body:** `Sự kiện mới được tạo/hoàn thành/hủy: {{ $node["Calendly Trigger"].json["event"]["description"] }}`

2. **Gửi thông báo Slack/Telegram:**
   - Thêm **node Slack** hoặc **Telegram Bot** để nhận thông báo tức thời trên ứng dụng.
   - Ví dụ với Slack:
     - Tạo **Webhook URL** trong Slack (Settings → Apps → Custom Integrations → Incoming Webhooks).
     - Thêm **node HTTP Request** sau **Calendly Trigger** với:
       - **Method:** `POST`
       - **URL:** `https://hooks.slack.com/services/XXXX/YYYY/ZZZZ`
       - **Body:** `{"text": "🚨 Sự kiện Calendly mới: {{ $node["Calendly Trigger"].json["event"]["title"] }}"}`

3. **Lưu log vào Google Sheets/Notion:**
   - Thêm **node Google Sheets** hoặc **Notion** để ghi lại tất cả sự kiện.
   - Cấu hình:
     - **Sheet Name:** `Calendly Events Log`
     - **Columns:** `Title, Description, Status, Date`

4. **Tự động cập nhật Google Calendar:**
   - Nếu muốn đồng bộ hóa sự kiện Calendly vào **Google Calendar**, thêm **node Google Calendar** và cấu hình:
     - **Calendar ID:** ID của Calendar trong Google.
     - **Event Details:** Lấy từ dữ liệu của **Calendly Trigger**.

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** để các sếp **không bao giờ bỏ lỡ một sự kiện Calendly nào**, ngay cả khi đang bận rộn. Với **tự động hóa 100% không code**, các sếp chỉ cần **cài đặt một lần** và **quên đi việc kiểm tra thủ công**.

**🚀 Hãy áp dụng ngay và tự động hóa công việc của mình!**
Nếu có bất kỳ câu hỏi nào, hãy để lại comment bên dưới. Chúc các sếp thành công! 💪

---
**🔗 [Xem workflow gốc tại n8n](https://n8n.io/workflows/540)** | **📌 [Tải file JSON](https://n8n.io/workflows/540/download)**