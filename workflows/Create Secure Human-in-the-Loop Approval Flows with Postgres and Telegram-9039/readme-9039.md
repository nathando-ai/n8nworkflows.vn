---
title: "🔒 Tự Động Hóa Quá Trình Phê Chuẩn Người Dùng (Human-in-the-Loop) Với PostgreSQL & Telegram - N8n"
description: "Giải pháp tự động hóa hoàn toàn không code cho doanh nghiệp cần phê duyệt thủ công an toàn, theo dõi được lịch sử và tự động hóa thông báo qua Telegram. Giảm thiểu thời gian chờ đợi 90% và tối ưu hóa quy trình phê chuẩn."
slug: "tieu-dong-hoa-qua-trinh-phe-chuan-nguoi-dung-postgres-telegram"
tags: [n8n, automation, no-code, postgres, telegram, human-in-the-loop, approval-flows, security, workflows]
keywords: [tự động hóa phê duyệt, n8n workflow, postgres telegram integration, human-in-the-loop approval, tự động hóa doanh nghiệp, phê duyệt an toàn, tự động hóa không code]
---

# 🚀 **Tự Động Hóa Quá Trình Phê Chuẩn Người Dùng (Human-in-the-Loop) Với PostgreSQL & Telegram**

## **📌 Giới Thiệu**
Bạn đã bao giờ phải chờ đợi phê duyệt từ quản lý trong nhiều ngày, chỉ vì một email hoặc tin nhắn bị bỏ qua? Hoặc phải lo lắng về việc dữ liệu phê duyệt không được theo dõi kịp thời? **Workflow này giải quyết tất cả những vấn đề đó!**

Với **Human-in-the-Loop Approval Flow**, các sếp có thể:
- **Phê duyệt tự động** thông qua liên kết an toàn (HMAC-signed) được gửi qua Telegram.
- **Theo dõi lịch sử phê duyệt** một cách chi tiết trong cơ sở dữ liệu PostgreSQL.
- **Cảnh báo tự động** khi có hành động không hợp lệ hoặc liên kết hết hạn.
- **Tiết kiệm thời gian** lên đến **90%** so với cách làm thủ công.

Workflow này **không cần viết code**, chỉ cần cấu hình và chạy 24/7 trên VPS của bạn.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tự động hóa phê duyệt** mà không cần can thiệp thủ công.
✅ **An toàn tuyệt đối** với HMAC-signed links và thời gian hết hạn (TTL).
✅ **Theo dõi lịch sử phê duyệt** chi tiết trong PostgreSQL.
✅ **Thông báo tự động** qua Telegram khi có sự kiện quan trọng (phê duyệt, từ chối, hết hạn).
✅ **Giảm thiểu lỗi người dùng** với cảnh báo cho hành động không hợp lệ.
✅ **Hoạt động liên tục 24/7** trên VPS riêng, không phụ thuộc vào email hay tin nhắn.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **n8n Self-hosted** (cài đặt trên VPS).
2. **Cơ sở dữ liệu PostgreSQL** với các bảng:
   - `tickets` (để lưu thông tin ticket).
   - `ticket_audit` (để theo dõi lịch sử phê duyệt).
   - `workflow_errors` (để ghi lỗi nếu có).
3. **Bot Telegram** với token API.
4. **Khóa bí mật (`SECRET_KEY`)** để ký số hóa liên kết phê duyệt.
5. **ID Chat của quản lý** (để nhận thông báo).

---
## **🚀 Cách Import & Lưu ý khi "Lên đồ"**

### **1. Import Workflow 📥**
- Tải file JSON của workflow từ [n8n.io/workflows/9039](https://n8n.io/workflows/9039).
- Trong n8n Editor, nhấn **Import Workflow** và chọn file JSON.
- Lưu workflow và kích hoạt nó.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **21 node** với các chức năng chính sau:

#### **🔹 Node Webhook (01 Webhook Trigger: Approval Decision)**
- **Đường dẫn:** `/approval`
- **Chức năng:** Nhận yêu cầu phê duyệt từ liên kết an toàn.
- **Lưu ý:** Không cần cấu hình thêm, chỉ cần đảm bảo webhook hoạt động.

#### **🔹 Node Code (02 FN: Verify Signature + TTL)**
- **Chức năng:** Kiểm tra chữ ký HMAC và thời gian hết hạn (TTL) của liên kết.
- **Yêu cầu:**
  - Thiết lập biến môi trường `SECRET_KEY` trong `.env`:
    ```env
    SECRET_KEY=your-secret-key-here
    ```
  - **Lưu ý:** Nếu không có `SECRET_KEY`, workflow sẽ **không hoạt động** (do yêu cầu an toàn).

#### **🔹 Node PostgreSQL (DB: Update Ticket Status, DB: Get Ticket Owner, DB: Insert Audit Row, DB: Insert Audit Expired, DB: Insert Audit Invalid)**
- **Chức năng:** Cập nhật trạng thái ticket và ghi log phê duyệt.
- **Cấu hình:**
  - Đi đến **Credentials → PostgreSQL** và thêm thông tin kết nối:
    - Host, Port, Database, Username, Password.
  - **SQL Query mẫu:**
    ```sql
    -- Cập nhật trạng thái ticket
    UPDATE tickets SET status = $1 WHERE id = $2;

    -- Lấy chủ sở hữu ticket
    SELECT chat_id FROM tickets WHERE id = $1;

    -- Thêm log phê duyệt
    INSERT INTO ticket_audit (ticket_id, correlation_id, action, new_status, actor_chat_id)
    VALUES ($1, $2, $3, $4, $5);
    ```

#### **🔹 Node Telegram (Notify Resolved, Notify In Progress, Telegram: Update Confirmation, Telegram: Notify Expired, Telegram: Alert Invalid)**
- **Chức năng:** Gửi thông báo qua Telegram khi có sự kiện phê duyệt.
- **Cấu hình:**
  - Đi đến **Credentials → Telegram API** và thêm token bot.
  - **Thay thế `chat_id`** trong các node Telegram bằng ID chat của quản lý (để nhận thông báo).
    - Để lấy ID chat, gửi tin nhắn cho bot Telegram và sử dụng `@userinfobot` để lấy thông tin.

#### **🔹 Node If & Switch (Kiểm tra điều kiện & Chuyển hướng)**
- **Chức năng:** Xác định trạng thái ticket (đã giải quyết, đang tiến hành, hết hạn, không hợp lệ).
- **Lưu ý:**
  - Node **If Resolved** và **If in_progress** sẽ chuyển hướng dựa trên trạng thái ticket.
  - Node **Actions (Switch)** quyết định hành động tiếp theo (cập nhật, cảnh báo, ghi log).

---

### **3. Kích hoạt ⚡️**
1. **Test run dữ liệu mẫu:**
   - Sử dụng liên kết mẫu:
     ```
     http://YOUR_N8N_HOST/approval?cid=<UUID>&status=in_progress&action=approve&exp=1735939200&sig=<hmac-signature>
     ```
   - Thay thế:
     - `cid` → ID ticket từ cơ sở dữ liệu.
     - `status` → `resolved` hoặc `in_progress`.
     - `action` → `approve` hoặc `reject`.
     - `exp` → Thời gian hết hạn (timestamp epoch).
     - `sig` → Chữ ký HMAC-SHA256 của `cid|status|exp`.

2. **Kiểm tra kết quả:**
   - Trạng thái ticket được cập nhật trong PostgreSQL.
   - Log phê duyệt được ghi vào `ticket_audit`.
   - Thông báo được gửi qua Telegram.
   - Nếu liên kết không hợp lệ hoặc hết hạn, sẽ có cảnh báo và ghi vào `workflow_errors`.

---

## **✍️ Mẹo & Gợi ý Nâng Cao**
1. **Tự động gửi liên kết phê duyệt:**
   - Kết hợp với node **Telegram Bot** để tự động gửi liên kết phê duyệt cho quản lý khi có ticket mới.

2. **Lưu log chi tiết hơn:**
   - Thêm trường `ip_address` vào bảng `ticket_audit` để theo dõi địa chỉ IP của người phê duyệt.

3. **Cảnh báo qua Email:**
   - Kết hợp với node **Email** để gửi cảnh báo khi có hành động không hợp lệ.

4. **Thiết lập thời gian hết hạn động:**
   - Sử dụng node **Code** để tính toán thời gian hết hạn dựa trên ngày tạo ticket.

5. **Tích hợp với Slack:**
   - Thay thế Telegram bằng **Slack Webhook** để thông báo trong Slack.

---

## **📌 Kết Luận**
Workflow **Human-in-the-Loop Approval Flow** là giải pháp **tự động hóa hoàn toàn không code** giúp doanh nghiệp:
✔ **Tiết kiệm thời gian** với phê duyệt tự động.
✔ **Tăng độ an toàn** với chữ ký HMAC và thời gian hết hạn.
✔ **Theo dõi được lịch sử** mọi hành động phê duyệt.
✔ **Hoạt động 24/7** trên VPS riêng.

**Hãy áp dụng ngay để cải thiện quy trình phê duyệt của doanh nghiệp!** 🚀

---
**🔗 [Tải workflow JSON](https://n8n.io/workflows/9039) | [Hướng dẫn cài đặt PostgreSQL](https://www.postgresql.org/download/)**