---
title: "🚀 **Tự Động Hóa Email Marketing Với Lượt Theo Dõi & Gửi Lại Tự Động - Giảm 80% Thời Gian Quản Lý Khách Hàng**"
description: "Workflow này tự động gửi email marketing hàng ngày, theo dõi phản hồi và gửi lại tự động theo các giai đoạn (Initial, Follow-Up 1, Follow-Up 2) - hoàn toàn không cần code. Giúp các sếp tiết kiệm thời gian, tăng tỷ lệ tương tác và quản lý khách hàng hiệu quả hơn."
slug: "tieu-dong-hoa-email-marketing-theo-do-tu-dong"
tags: [n8n, automation, email marketing, google-sheets, gmail, no-code]
keywords: [tự động hóa email marketing, gửi email tự động theo giai đoạn, theo dõi phản hồi email, n8n workflow, tự động hóa bán hàng]
---

# 🚀 **Tự Động Hóa Email Marketing Với Lượt Theo Dõi & Gửi Lại Tự Động**

## **💡 Giải Pháp Cho Nỗi Đau Của Các Sếp**
Bạn có bao giờ phải:
- **Gõ tay** gửi email cho hàng trăm khách hàng hàng ngày?
- **Quên theo dõi** phản hồi của khách hàng sau khi gửi email?
- **Phải làm thủ công** để gửi lại email theo giai đoạn (Initial → Follow-Up 1 → Follow-Up 2)?
- **Không biết** liệu email đã được mở hay không?

Workflow này **giải quyết tất cả** bằng cách tự động hóa **tất cả quy trình email marketing**, từ gửi email hàng ngày đến theo dõi phản hồi và cập nhật trạng thái khách hàng trên Google Sheets. **Không cần code, chỉ cần cấu hình và chạy 24/7!**

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
✅ **Tiết kiệm 80% thời gian** quản lý email so với làm thủ công.
✅ **Tăng tỷ lệ tương tác** với khách hàng nhờ gửi lại tự động theo giai đoạn.
✅ **Theo dõi phản hồi chính xác** và cập nhật trạng thái trên Google Sheets.
✅ **Hoạt động liên tục** (24/7) mà không cần can thiệp.
✅ **Cá nhân hóa email** dựa trên dữ liệu khách hàng từ Google Sheets.
:::

---

### **🔧 Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ**]
Trước khi chạy workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Gmail** (để gửi email) với **API Gmail được kích hoạt** ([Cách kích hoạt API Gmail](https://developers.google.com/gmail/api/quickstart/python)).
✔ **Tài khoản Google Sheets** với **Google API được kết nối** ([Cách kết nối Google API](https://developers.google.com/sheets/api/quickstart/python)).
✔ **Tài khoản IMAP** (để đọc email phản hồi) - có thể là cùng tài khoản Gmail hoặc khác.
✔ **Google Sheet** có cấu trúc dữ liệu như sau (cột bắt buộc: **Name, Email, Stage**):
   | Name       | Email               | Stage       |
   |------------|---------------------|-------------|
   | Khách Hàng 1 | customer1@example.com | Initial    |
   | Khách Hàng 2 | customer2@example.com | Follow-Up 1 |
   | ...        | ...                 | ...         |
✔ **Mã API Key** từ [n8n.io](https://n8n.io/) (nếu tự host).
:::

---

## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/7175](https://n8n.io/workflows/7175) (chọn **Export as JSON**).
2. **Mở n8n Editor** (trên [n8n.io](https://n8n.io/) hoặc self-hosted).
3. Nhấn **Import** → Chọn file JSON vừa tải → **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Copy toàn bộ mã JSON** từ [n8n.io/workflows/7175](https://n8n.io/workflows/7175) (chọn **Export as JSON**).
2. Trong n8n Editor, nhấn **Import** → Chọn **Paste JSON** → Dán và **Import**.

---
### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **10 node**, nhưng **các node quan trọng nhất** cần cấu hình kỹ lưỡng:

#### **🔹 Node 1: Daily Trigger (9 AM)**
- **Cấu hình Cron**: `0 3 9 * * ?` (gửi email hàng ngày lúc 9 AM UTC).
- **Lưu ý**:
  - Nếu sử dụng **VPS Việt Nam**, hãy điều chỉnh giờ theo **UTC+7** (ví dụ: `0 2 9 * * ?`).
  - **Không cần thay đổi** nếu đang dùng n8n.io (môi trường cloud).

#### **🔹 Node 2: Fetch Contact Data (Google Sheets)**
- **Chọn Credentials**: `googleApi` (đã cấu hình trước khi import).
- **Cấu hình Sheet**:
  - **Sheet Name**: Tên tệp Google Sheets của bạn.
  - **Range**: `Sheet1!A1:D1000` (đảm bảo bao gồm tất cả dữ liệu khách hàng).
  - **Headers**: Bật `Use headers` và chọn cột **Name, Email, Stage**.

#### **🔹 Node 3: Iterate Contacts (SplitInBatches)**
- **Cấu hình Batch Size**:
  - Mặc định là **100**, nhưng có thể giảm xuống **50** nếu gặp lỗi rate limit của Gmail.
  - **Không cần thay đổi** nếu không gặp vấn đề.

#### **🔹 Node 4: Determine Follow-Up Stage (If)**
- **Cấu hình điều kiện**:
  - **Stage = Initial** → Gửi **Follow-Up Email 1**.
  - **Stage = Follow-Up 1** → Gửi **Follow-Up Email 2**.
  - **Khác** → Bỏ qua (không gửi email).

#### **🔹 Node 5 & 6: Send Follow-Up Email 1 & 2 (Gmail)**
- **Chọn Credentials**: `googleApi` (tài khoản Gmail sẽ gửi email).
- **Cấu hình Email**:
  - **From**: Điền email của bạn (ví dụ: `no-reply@domain.com`).
  - **Subject**: Tùy chỉnh (ví dụ: `🔥 Follow-Up: Dịch vụ của chúng tôi`).
  - **HTML Content**: Sử dụng **các biến động** từ Google Sheets (ví dụ: `{{ $json["Name"] }}`).
  - **Lưu ý**:
    - **Không gửi email trống** → Kiểm tra lại **Google Sheets** có dữ liệu đầy đủ không.
    - **Rate limit Gmail**: Nếu gặp lỗi `Too many requests`, giảm **Batch Size** ở Node 3.

#### **🔹 Node 7: Update Sheet with Follow-Up Status (Google Sheets)**
- **Cấu hình Update**:
  - **Range**: `Sheet1!D1:D1000` (cột Status).
  - **Value**: `{{ $json["Stage"] }}` (cập nhật trạng thái sau khi gửi email).

#### **🔹 Node 8: Check Email Responses (IMAP)**
- **Chọn Credentials**: `imap` (tài khoản IMAP để đọc email phản hồi).
- **Cấu hình**:
  - **Host**: `imap.gmail.com` (nếu dùng Gmail).
  - **Port**: `993`.
  - **Username/Password**: Tài khoản IMAP của bạn.
  - **Folder**: `INBOX` (hoặc folder chứa email phản hồi).
  - **Search Query**: `FROM:{{ $json["Email"] }}` (tìm email từ khách hàng đó).

#### **🔹 Node 9: Update Sheet with Response (Google Sheets)**
- **Cấu hình Update**:
  - **Range**: `Sheet1!E1:E1000` (cột Response).
  - **Value**: `{{ $json["Subject"] }} + " - " + {{ $json["Body"] }}` (lưu nội dung phản hồi).

---
### **3. Kích Hoạt ⚡️**
1. **Test Run** với **1-2 email mẫu**:
   - Chọn **Run Workflow** → Chọn **1-2 contact** từ Google Sheets → Kiểm tra email đã gửi và phản hồi có được cập nhật không.
2. **Bật Active**:
   - Sau khi test thành công, nhấn **Active** để workflow chạy tự động hàng ngày.

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**
:::info[**MỞ RỘNG THÊM TÍNH NĂNG**]
🔹 **Gửi email qua Slack/Telegram khi có phản hồi**:
   - Thêm **Node Slack/Telegram** sau **Node 9** để thông báo phản hồi tức thời.

🔹 **Lưu log hoạt động vào Google Sheets**:
   - Thêm **Node StickyNote** để ghi lại lỗi hoặc thông tin debug.

🔹 **Gửi báo cáo định kỳ**:
   - Sử dụng **Node ScheduleTrigger** để gửi báo cáo tổng hợp (ví dụ: hàng tuần) về tỷ lệ mở email, phản hồi...

🔹 **Cá nhân hóa email hơn**:
   - Thêm **Node LLM** (n8n-nodes-ai.llm) để tự động viết nội dung email dựa trên dữ liệu khách hàng.

🔹 **Kết hợp với CRM khác**:
   - Thay thế Google Sheets bằng **HubSpot, Salesforce** hoặc **Airtable** để quản lý khách hàng chuyên nghiệp hơn.
:::

---

## **📌 Kết Luận**
Workflow này **giải phóng thời gian** của các sếp để tập trung vào việc **tăng doanh số** thay vì làm thủ công. **Chỉ cần cấu hình 1 lần**, workflow sẽ tự động:
✔ Gửi email hàng ngày.
✔ Theo dõi phản hồi.
✔ Cập nhật trạng thái khách hàng.
✔ Gửi lại tự động theo giai đoạn.

**🚀 Hãy áp dụng ngay và bắt đầu tự động hóa email marketing của mình!**
Nếu gặp vấn đề, **hãy comment bên dưới** hoặc liên hệ [Oneclick AI Squad](https://oneclickai.com/) để hỗ trợ.

---
:::note[**LƯU Ý CUỐI CÙNG**]
- **N8n Self-hosted** chạy ổn định hơn trên **VPS** (không bị gián đoạn).
- **🎁 Mã giảm giá VPS TinoHost**: **VPSN8N** (giảm tới 39%).
  👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)
- **💡 Nếu muốn tối ưu hơn**, có thể kết hợp với **n8n AI Nodes** để tự động viết email.
:::