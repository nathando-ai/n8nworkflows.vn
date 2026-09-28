---
title: "🔄 **Tự Động Hóa Gmail ↔ iMessage: Đối Tác Khách Hàng Trực Tuyến 24/7 Với Blooio & Close CRM**"
description: "Workflow tự động hóa chuyển đổi email thành tin nhắn iMessage và ngược lại, đồng thời ghi log toàn bộ cuộc trò chuyện vào Close CRM - tiết kiệm 100+ giờ/năm cho bộ phận bán hàng và hỗ trợ khách hàng."
slug: "tieu-dong-hoa-gmail-iMessage-blooio-close"
tags: [n8n, automation, lead-nurturing, blooio, close-crm, gmail-integration]
keywords: [tự động hóa email iMessage, blooio n8n, close crm automation, chatbot doanh nghiệp, tự động hóa bán hàng]
---

# 🚀 **Tự Động Hóa Gmail ↔ iMessage: Đối Tác Khách Hàng Trực Tuyến 24/7**

### **Nỗi Đau Của Các Sếp**
Các sếp đang mất **100+ giờ/năm** để:
- **Trả lời khách hàng qua email và tin nhắn iMessage** song song, dẫn đến trễ trả lời và mất cơ hội bán hàng.
- **Không theo dõi toàn bộ cuộc trò chuyện** của khách hàng trên nhiều kênh (email + iMessage), gây mất mát dữ liệu quan trọng.
- **Phải nhớ ghi log cuộc trò chuyện** vào CRM (Close, HubSpot, Salesforce...) thủ công, tốn thời gian và dễ sai sót.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Chuyển email thành tin nhắn iMessage** (và ngược lại) một cách **liên tục 24/7**.
✅ **Ghi log toàn bộ cuộc trò chuyện** vào Close CRM (hoặc CRM khác) để theo dõi lịch sử.
✅ **Tiết kiệm 50% thời gian** cho bộ phận bán hàng và hỗ trợ khách hàng.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để tránh giới hạn của phiên bản miễn phí.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100+ giờ/năm** cho bộ phận bán hàng và hỗ trợ khách hàng.
- **Khách hàng được hỗ trợ 24/7** qua email **và** tin nhắn iMessage, tăng trải nghiệm và tỷ lệ chuyển đổi.
- **Dữ liệu khách hàng toàn diện** được ghi log vào CRM, giúp phân tích hành vi và tối ưu chiến lược bán hàng.
- **Tự động hóa hoàn toàn** - không cần code, chỉ cần cấu hình.
- **Hoạt động song song** với các hệ thống khác (Slack, Telegram, CRM khác) bằng cách mở rộng workflow.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản Gmail** (để kết nối với n8n và nhận/send email).
✔ **Tài khoản Blooio** ([bloo.io](https://bloo.io/)) để chuyển đổi email ↔ iMessage.
✔ **Tài khoản Close CRM** ([close.com](https://close.com/)) để ghi log cuộc trò chuyện.
✔ **API Keys** của các dịch vụ trên (cách lấy ở phần **Cách import & Lưu ý khi "lên đồ"**).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow này:
- **Tải file JSON** từ [n8n.io/workflows/15786](https://n8n.io/workflows/15786) và import vào **n8n Editor**.
- **Copy/paste JSON** từ link trên vào **n8n Editor** (tab **Import/Export**).

:::note[Lưu ý]
- **Không sử dụng phiên bản n8n miễn phí** (Community Edition) vì có giới hạn node và không hỗ trợ webhook.
- **Kích hoạt "Active"** sau khi cấu hình xong để workflow bắt đầu hoạt động.
:::

---

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **11 node** quan trọng, các sếp cần cấu hình kỹ như sau:

##### **🔹 Node 1: "When Email Received" (gmailTrigger)**
- **Chọn credential Gmail** đã kết nối trước đó.
- **Chọn inbox** cần theo dõi (ví dụ: `bridge-inbox@domain.com`).
- **Lưu ý**: Nếu inbox chưa tồn tại, tạo mới và **không sử dụng inbox chính** của cá nhân.

##### **🔹 Node 2: "If Phone in Subject" (if)**
- **Cấu hình điều kiện**: Kiểm tra xem **subject của email có chứa số điện thoại** (ví dụ: `^\+[0-9]{10,15}$`).
- **Lưu ý**: Nếu không tìm thấy số điện thoại, email sẽ bị bỏ qua.

##### **🔹 Node 3: "Prepare iMessage Data" (set)**
- **Lọc và sạch dữ liệu**: Xóa các ký tự đặc biệt, giữ lại nội dung chính của email.
- **Lưu ý**: Cần **định dạng lại JSON** để Blooio nhận được dữ liệu đúng format.

##### **🔹 Node 4: "Send iMessage via Blooio" (blooioMessaging)**
- **Chọn credential Blooio** đã kết nối.
- **Điền số điện thoại** từ node trước vào field `phone`.
- **Điền nội dung email** vào field `message`.
- **Lưu ý**:
  - **Kiểm tra webhook URL** của Blooio đã được đăng ký trong **Node 5** ("When iMessage Received").
  - **Test send** trước khi bật workflow.

##### **🔹 Node 5: "When iMessage Received" (webhook)**
- **Đăng ký webhook** trong tài khoản Blooio:
  - Path: `imessage-email-inbound`
  - HTTP Method: `POST`
  - **Lưu ý**: Nếu là môi trường sản xuất, **bật HMAC verification** để tăng an toàn.

##### **🔹 Node 6: "If Inbound Message Event" (if)**
- **Lọc chỉ các tin nhắn mới** (không phải tin nhắn đã gửi trước đó).
- **Lưu ý**: Nếu không cấu hình đúng, workflow có thể bị lặp lại.

##### **🔹 Node 7: "Build Email From iMessage" (set)**
- **Chuyển đổi tin nhắn iMessage** thành format email (Reply-To, Subject, Body).
- **Lưu ý**: **Đặt Reply-To** là email của inbox bridge để khách hàng trả lời được tự động chuyển về email.

##### **🔹 Node 8: "Send Email to Inbox" (gmail)**
- **Chọn credential Gmail** đã kết nối.
- **Chọn inbox** để gửi email (cùng inbox trong Node 1).
- **Lưu ý**: **Test send** trước khi bật workflow để đảm bảo email được gửi đúng.

##### **🔹 Node 9 & 10: "Find Lead in Close by Phone" & "If Lead Found" (httpRequest + if)**
- **Chọn credential Close API** (cách lấy ở [Close Developer Docs](https://developers.close.com/)).
- **Điền API Key** vào header `Authorization: Bearer {API_KEY}`.
- **Lưu ý**:
  - **API Endpoint**: `https://api.close.com/v1/leads` (tìm kiếm lead bằng số điện thoại).
  - **Nếu lead không tìm thấy**, workflow sẽ **bỏ qua** và không ghi log.

##### **🔹 Node 11: "Log iMessage to Close" (httpRequest)**
- **Gửi request POST** để ghi log cuộc trò chuyện vào Close CRM.
- **API Endpoint**: `https://api.close.com/v1/leads/{lead_id}/activities` (đổi `{lead_id}` thành ID lead từ Node 9).
- **Lưu ý**:
  - **Format JSON** phải đúng với yêu cầu của Close API.
  - **Test API** trước khi bật workflow để đảm bảo dữ liệu ghi log chính xác.

---

#### **3. Kích Hoạt ⚡️**
1. **Test run** với **dữ liệu mẫu**:
   - Gửi email có số điện thoại trong subject và nội dung test.
   - Kiểm tra tin nhắn iMessage được gửi và trả lời có được chuyển về email không.
   - Kiểm tra log trong Close CRM có xuất hiện không.
2. **Bật "Active"** workflow khi tất cả test thành công.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[CÁCH MỞ RỘNG WORKFLOW]
1. **Kết nối với Slack/Telegram**:
   - Sử dụng node **Slack** hoặc **Telegram Bot** để gửi thông báo khi có tin nhắn mới.
   - Ví dụ: Khi khách hàng trả lời iMessage, workflow tự động gửi tin nhắn đến nhóm Slack của bộ phận bán hàng.

2. **Lưu log vào Google Sheets/Notion**:
   - Thay thế node **httpRequest** của Close bằng node **Google Sheets** hoặc **Notion API** để lưu dữ liệu cuộc trò chuyện.

3. **Gửi báo cáo định kỳ**:
   - Sử dụng node **Set** + **Google Calendar** để tự động gửi báo cáo tổng hợp cuộc trò chuyện hàng tuần cho quản lý.

4. **Bật AI Chatbot (LLM)**:
   - Sử dụng node **LLM (n8n-nodes-base.llm)** để tự động trả lời tin nhắn iMessage nếu khách hàng hỏi về sản phẩm/dịch vụ.

5. **Cài đặt HMAC cho webhook**:
   - Trong Node 5 ("When iMessage Received"), bật **HMAC verification** để tăng an toàn cho webhook.

6. **Tích hợp với Zapier/Make**:
   - Nếu không muốn tự host n8n, có thể sử dụng **Zapier** hoặc **Make (Integromat)** để tự động hóa phần này, nhưng hiệu suất sẽ kém hơn.
:::

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào **bán hàng và chiến lược**, trong khi hệ thống tự động:
✔ **Chuyển đổi email ↔ iMessage** một cách liên tục.
✔ **Ghi log cuộc trò chuyện** vào Close CRM.
✔ **Tự động trả lời khách hàng** qua cả hai kênh.

**Hành động ngay hôm nay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test với dữ liệu mẫu** trước khi bật Active.
3. **Mở rộng** bằng cách kết nối thêm Slack, Telegram hoặc AI Chatbot.

**🚀 [Tải workflow ngay từ n8n.io](https://n8n.io/workflows/15786) và tự động hóa đối tác khách hàng của bạn!**

---
**📌 Cần hỗ trợ?** Đăng ký tư vấn miễn phí tại [SMB Excel](https://www.smbexcel.com) để tối ưu workflow cho doanh nghiệp của bạn!