---
title: "🤖 **Tự Động Hồi Đáp DM Instagram với Liên Kết Affiliate Theo Từ Khóa - Không Cần Code!**"
description: "Workflow n8n tự động phát hiện tin nhắn Instagram chứa từ khóa sản phẩm, trả lời tự động với liên kết affiliate cá nhân hóa, tiết kiệm thời gian và tăng doanh số. Hoạt động 24/7, không cần can thiệp thủ công."
slug: "tieu-dong-hoi-dap-dm-instagram-affiliate"
tags: [n8n, automation, instagram, affiliate marketing, meta-graph-api, no-code]
keywords: [n8n workflow instagram, tự động hóa dm instagram, affiliate instagram, meta graph api, tự động trả lời tin nhắn instagram]
---

# 🚀 **Tự Động Hồi Đáp DM Instagram với Liên Kết Affiliate Theo Từ Khóa**

### **Giải pháp hoàn hảo cho các sếp bán hàng online**
Bạn đã bao giờ phải mất **30 phút/ngày** để trả lời tin nhắn Instagram từ khách hàng tìm kiếm sản phẩm? Hay phải lo lắng **quên trả lời** khi đang bận với công việc khác? Workflow này sẽ **tự động hóa 100%** quá trình trả lời DM với **liên kết affiliate cá nhân hóa**, giúp bạn:
- **Tiết kiệm 5+ giờ/tuần** để tập trung vào chiến lược marketing.
- **Tăng tỷ lệ chuyển đổi** với tin nhắn tự động nhưng **cá nhân hóa**.
- **Không bỏ lỡ khách hàng** nhờ hoạt động liên tục 24/7.
- **Tăng doanh thu** từ affiliate với liên kết chính xác.

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công, hoạt động tự động mỗi 15 phút.
✅ **Cá nhân hóa liên kết affiliate**: Trả lời với liên kết sản phẩm phù hợp với từ khóa khách hàng tìm kiếm.
✅ **Tránh trùng lặp**: Không gửi lại tin nhắn đã trả lời trước đó.
✅ **Dễ dàng mở rộng**: Thêm/loại bỏ từ khóa sản phẩm chỉ cần chỉnh file `products.json`.
✅ **Báo cáo tự động**: Theo dõi lịch sử tin nhắn đã trả lời trong `replied_dms.json`.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Instagram Business/Creator** (đã kích hoạt tính năng DM).
2. **Meta Page Access Token**:
   - Đăng ký ứng dụng trên [Meta Developer Portal](https://developers.facebook.com/) với **permissions**:
     - `instagram_manage_messages`
     - `pages_messaging`
   - Lấy **Long-lived Access Token** (thời hạn 60 ngày, có thể renew).
3. **ID số của tài khoản Instagram** (tham khảo [hướng dẫn Meta](https://developers.facebook.com/docs/instagram-api/reference/user/)).
4. **File `products.json`** (định dạng JSON) ở đường dẫn `/home/node/.n8n-files/` với cấu trúc:
   ```json
   {
     "keyword1": "https://lienket-affiliate-1.com",
     "keyword2": "https://lienket-affiliate-2.com"
   }
   ```
   Ví dụ:
   ```json
   {
     "sản phẩm A": "https://affiliate.example.com/productA",
     "máy tính xách tay": "https://affiliate.example.com/laptop",
     "sách học tiếng Anh": "https://affiliate.example.com/english-book"
   }
   ```
5. **File `replied_dms.json`** (để lưu lịch sử tin nhắn đã trả lời):
   ```json
   {
     "replied_message_ids": []
   }
   ```
   (File này sẽ tự động tạo khi workflow chạy lần đầu và trả lời thành công).
6. **n8n Self-hosted** (không dùng phiên bản cloud để đảm bảo ổn định 24/7).
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. **Tải workflow** từ [n8n.io/workflows/15130](https://n8n.io/workflows/15130).
2. **Nhấp vào "Import"** trong n8n Editor.
3. **Chọn file JSON** hoặc **copy toàn bộ JSON** vào ô "Paste JSON" và nhấn "Import".

:::note[LƯU Ý]
- **Không sử dụng phiên bản n8n cloud** vì không hỗ trợ schedule trigger và file hệ thống.
- **Cài n8n trên VPS** để workflow hoạt động liên tục.
:::

---

### **2. Các bước cấu hình BẮT BUỘC phải chỉnh 📌**
#### **A. Cấu hình Token & ID Tài Khoản (Node: Configure Global Settings)**
1. Mở node **"Configure Global Settings"**.
2. **Thay thế `[YOUR-META-ACCESS-TOKEN]`** bằng **Long-lived Access Token** của bạn.
3. **Thay thế `[YOUR-INSTAGRAM-ACCOUNT-ID]`** bằng **ID số tài khoản Instagram** (lấy từ Meta Developer Portal).
   - **Cách lấy ID Instagram**:
     - Mở [Graph API Explorer](https://developers.facebook.com/tools/explorer/).
     - Đăng nhập với tài khoản Meta của bạn.
     - Gõ query:
       ```graphql
       GET /{page-id}/instagram_business_account
       ```
     - Thay `{page-id}` bằng ID của Page của bạn (lấy từ URL: `https://www.facebook.com/{page-id}`).
     - Kết quả trả về sẽ có trường `id` là **ID Instagram Business**.

#### **B. Cấu hình File `products.json` và `replied_dms.json`**
1. **Tạo thư mục `.n8n-files`** ở đường dẫn `/home/node/` (nếu chưa có):
   ```bash
   mkdir -p /home/node/.n8n-files
   ```
2. **Tạo file `products.json`** với nội dung như ví dụ trên.
3. **Tạo file `replied_dms.json`** với cấu trúc:
   ```json
   {
     "replied_message_ids": []
   }
   ```
   - File này sẽ tự động cập nhật khi workflow trả lời thành công.

#### **C. Cấu hình Schedule Trigger**
1. Mở node **"Schedule Trigger"**.
2. **Thay đổi interval** từ `*/15 * * * *` (mỗi 15 phút) thành giá trị phù hợp (ví dụ: `*/30 * * * *` để chạy mỗi 30 phút).
   - **Lưu ý**: Interval nhỏ hơn 15 phút có thể bị Meta chặn vì quá tải API.

#### **D. Cấu hình Node "Filter New DMs" (Thay đổi template trả lời)**
1. Mở node **"Filter New DMs"** (node type: `code`).
2. **Tìm và chỉnh sửa phần `replyMessage`** trong code JavaScript để thay đổi nội dung trả lời.
   - Ví dụ mặc định:
     ```javascript
     replyMessage = `Xin chào! Tôi thấy bạn quan tâm đến ${keyword}. Đây là liên kết affiliate: ${url}. Chúc bạn mua sắm tốt!`;
     ```
   - **Thay đổi thành template cá nhân hóa** của bạn.

#### **E. Kiểm tra Node "Check If Should Reply"**
1. Mở node **"Check If Should Reply"** (node type: `if`).
2. **Đảm bảo điều kiện `json["text"].toLowerCase().includes(keyword)`** hoạt động đúng với từ khóa trong `products.json`.

---

### **3. Kích hoạt ⚡️ Workflow**
1. **Nhấn "Run"** để test với dữ liệu mẫu.
2. **Kiểm tra log** để xác nhận:
   - Workflow đã lấy được tin nhắn từ Instagram.
   - Đã trả lời thành công với liên kết affiliate.
   - File `replied_dms.json` đã cập nhật.
3. **Bật "Active"** để workflow chạy tự động theo schedule.

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Kết nối với Slack/Telegram**:
   - Thêm node **Slack/Telegram Webhook** sau node **"Send DM Reply"** để báo cáo tin nhắn đã trả lời.
   - Cấu hình trong node **HTTP Request** với endpoint của Slack/Telegram.

2. **Lưu log chi tiết**:
   - Thêm node **Google Sheets** hoặc **Airtable** để ghi lại lịch sử tin nhắn, từ khóa, và liên kết affiliate đã gửi.
   - Cấu hình trong node **"Read DM History"** và **"Save DM History"**.

3. **Phân loại tin nhắn**:
   - Sử dụng node **Code** trong **"Filter New DMs"** để phân loại tin nhắn (ví dụ: tin nhắn từ khách hàng mới vs. khách hàng cũ) và trả lời khác nhau.

4. **Báo cáo định kỳ**:
   - Thêm node **Schedule Trigger** mới để chạy mỗi ngày và gửi báo cáo tổng hợp qua email (sử dụng node **Email**).

5. **Cập nhật liên kết affiliate**:
   - Tạo một **node HTTP Request** để tự động pull danh sách sản phẩm mới từ API của nhà cung cấp affiliate (ví dụ: Amazon Associates, CJ Affiliate).
   - Cập nhật `products.json` tự động bằng node **ReadWriteFile (write)**.

6. **Ngôn ngữ đa dạng**:
   - Sử dụng node **Code** để tự động chuyển đổi tin nhắn thành nhiều ngôn ngữ (ví dụ: tiếng Việt, tiếng Anh) dựa trên ngôn ngữ của khách hàng.
   - Sử dụng API như **DeepL** hoặc **Google Translate**.
:::

---
## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** để tự động hóa quá trình trả lời DM Instagram với liên kết affiliate, giúp các sếp **tiết kiệm thời gian**, **tăng doanh thu**, và **cá nhân hóa trải nghiệm khách hàng**. Bằng cách chỉ cần **cấu hình một lần**, workflow sẽ hoạt động **liên tục 24/7** mà không cần can thiệp thủ công.

**Hãy áp dụng ngay và bắt đầu tự động hóa DM Instagram của bạn!** 🚀

---
:::tip[CHÚC MỪNG]
Các sếp đã có một công cụ **tự động hóa cao cấp** để tăng hiệu suất bán hàng. Nếu có vấn đề, hãy liên hệ với cộng đồng n8n hoặc [TinoHost](https://tino.vn) để hỗ trợ cài đặt VPS!
:::

---
:::info[HƯỚNG DẪN CẢI ĐẶT VPS CHO N8N]
👉 **Đăng ký VPS TinoHost** (giảm giá **39%** với mã **VPSN8N**):
🔗 [https://tino.vn/vps-n8n?affid=388](https://tino.vn/vps-n8n?affid=388)

👉 **Đăng ký VPS Xeon 4GB chỉ 50k/tháng** (đảm bảo ổn định):
🔗 [https://my.bnix.one/aff.php?aff=172](https://my.bnix.one/aff.php?aff=172)
:::