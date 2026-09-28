---
title: "🚀 Tự Động Hóa Cuộc Hỏi Dàn (Anketa) WhatsApp Sang PostgreSQL - Giảm 90% Công Việc Nhập Liệu"
description: "Workflow này tự động thu thập và lưu trữ tất cả câu trả lời từ cuộc hỏi dàn WhatsApp vào cơ sở dữ liệu PostgreSQL, giúp các sếp tiết kiệm thời gian và giảm thiểu lỗi nhập liệu. Hỗ trợ quản lý trạng thái bot và cá nhân hóa trải nghiệm người dùng."
slug: "tu-dong-hoa-cuoc-hoi-dan-whatsapp-sang-postgres"
tags: [n8n, automation, no-code, whatsapp-business-api, postgresql, marketing-automation]
keywords: [n8n workflow whatsapp, tự động hóa anketa, lưu trữ câu trả lời whatsapp, postgresql automation, giảm công việc nhập liệu]
---

# 🚀 **Tự Động Hóa Cuộc Hỏi Dàn (Anketa) WhatsApp Sang PostgreSQL**

### **Giải pháp hoàn hảo cho các sếp muốn:**
- **Tiết kiệm 90% thời gian** nhập liệu từ WhatsApp vào Excel/Google Sheets.
- **Lưu trữ dữ liệu an toàn** trong PostgreSQL với khả năng truy xuất nhanh.
- **Cá nhân hóa trải nghiệm** cho khách hàng qua bot WhatsApp.
- **Hoạt động 24/7** mà không cần can thiệp thủ công.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động ổn định và không bị gián đoạn, các sếp nên **self-host n8n** trên một VPS ổn định. Dưới đây là một số gợi ý:
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (Đảm bảo tốc độ và độ tin cậy cao)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tự động thu thập** tất cả câu trả lời từ cuộc hỏi dàn WhatsApp.
✅ **Lưu trữ dữ liệu** vào PostgreSQL với cấu trúc rõ ràng (không cần nhập liệu thủ công).
✅ **Quản lý trạng thái bot** (đã bắt đầu, đang trả lời, hoàn thành anketa).
✅ **Cá nhân hóa** trải nghiệm người dùng với các câu hỏi động.
✅ **Hoạt động liên tục** 24/7, không phụ thuộc vào nhân viên.
✅ **Giảm thiểu lỗi** do nhập liệu sai hoặc mất dữ liệu.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
🔹 **Tài khoản WhatsApp Business API** (cần **Phone Number ID** và **Access Token**).
🔹 **Cơ sở dữ liệu PostgreSQL** (cần **host, port, username, password, database name**).
🔹 **Bảng dữ liệu trong PostgreSQL** với các cột:
   - `bot_id` (ID của bot)
   - `question_id` (ID của câu hỏi)
   - `answer` (câu trả lời của người dùng)
   - `status` (trạng thái: `START`, `ANKETA`, `FINISHED`)
🔹 **API Key của n8n** (nếu self-host).

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Tải file JSON từ [n8n.io/workflows/3653](https://n8n.io/workflows/3653).
2. Vào **n8n Editor** → **Import Workflow** → Chọn file JSON.
3. Hoặc copy toàn bộ JSON và paste vào **Import Workflow** → **Paste JSON**.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **22 node** và cần cấu hình kỹ lưỡng các phần sau:

#### **🔹 Cấu hình WhatsApp Trigger**
- **Node:** `WhatsApp Trigger` (n8n-nodes-base.whatsAppTrigger)
  - **Credentials:** Chọn tài khoản WhatsApp Business API đã đăng ký.
  - **Phone Number ID:** Điền vào `Phone Number ID` từ WhatsApp Business API.
  - **Access Token:** Điền vào `Access Token` từ WhatsApp Business API.

#### **🔹 Cấu hình PostgreSQL**
- **Node:** `Get Bot Status`, `Update Bot Status on ANKETA`, `Update Bot Status on START`, `Get First Question`, `Get Available Questions`, `Add prev Answer`, `Add Answer`, `Upsert Bot Status on START`
  - **Host:** Điền địa chỉ IP/host của PostgreSQL.
  - **Port:** Thường là `5432`.
  - **Database:** Tên cơ sở dữ liệu.
  - **Username & Password:** Tài khoản truy cập PostgreSQL.
  - **Query:** Các câu lệnh SQL cần chỉnh sửa để phù hợp với bảng dữ liệu của các sếp.

#### **🔹 Cấu hình StickyNote (Lưu ý)**
- **Node:** `Initialization`, `Define Flow`, `Is Questions available?`, `Is Question found?`
  - Các node này dùng để **lưu trạng thái** của bot (ví dụ: đã bắt đầu anketa, đang trả lời câu hỏi nào).
  - Các sếp **không cần chỉnh sửa** nếu muốn sử dụng mặc định.

#### **🔹 Cấu hình WhatsApp Messages**
- **Node:** `Starts`, `Main Menu`, `First Question`, `Question`, `Finish Anketa`
  - **Text:** Chỉnh sửa nội dung tin nhắn để phù hợp với anketa của các sếp.
  - **Reply Keywords:** Điền các từ khóa để bot phản hồi (ví dụ: `start`, `next`, `finish`).

#### **🔹 Cấu hình Switch & If**
- **Node:** `Commands`, `Define Flow`, `Is Questions available?`, `Is Question found?`
  - Các node này **quản lý logic** của bot (ví dụ: nếu người dùng chọn `start`, bot sẽ chuyển đến câu hỏi đầu tiên).
  - **Không cần chỉnh sửa** nếu muốn sử dụng logic mặc định.

### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Gửi tin nhắn `start` đến số WhatsApp của bot.
   - Kiểm tra bot có phản hồi đúng không?
   - Kiểm tra PostgreSQL có lưu trữ câu trả lời không?
2. **Bật Active Workflow** sau khi test thành công.

---

## ✍️ **Mẹo & gợi ý nâng cao**
### **🔹 Kết hợp với Slack/Telegram để báo cáo**
- Thêm **node Slack/Telegram** sau `Add Answer` để gửi thông báo khi có câu trả lời mới.
- Ví dụ: `Gửi tin nhắn Slack: "Có câu trả lời mới từ anketa: [Answer]"`.
### **🔹 Lưu log hoạt động**
- Thêm **node StickyNote** hoặc **node File** để lưu log tất cả hoạt động của bot.
- Có thể sử dụng **node Email** để gửi báo cáo định kỳ cho team.
### **🔹 Tự động gửi báo cáo định kỳ**
- Sử dụng **node Set** + **node Cron** để chạy query lấy tổng hợp dữ liệu và gửi qua Email/Slack.
### **🔹 Cá nhân hóa anketa**
- Thêm **node LLM (n8n-nodes-base.llm)** để phân tích câu trả lời và gửi câu hỏi động.

---

## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa cuộc hỏi dàn WhatsApp mà không cần code. Với PostgreSQL làm cơ sở dữ liệu, dữ liệu sẽ được **lưu trữ an toàn và dễ truy xuất**, đồng thời **giảm thiểu công việc nhập liệu thủ công**.

**Hãy áp dụng ngay và tiết kiệm thời gian cho team của mình!** 🚀

---
**💡 Cần hỗ trợ thêm?**
- **Đăng ký VPS n8n** để self-host: [TinoHost](https://tino.vn/vps-n8n?affid=388)
- **Hỏi đáp nhanh** trên [Community n8n](https://community.n8n.io/)