---
title: "🔍 Kiểm tra Tron Wallet USDT Blacklist qua Telegram - Tự động hóa an toàn giao dịch 100% không code"
description: "Workflow tự động kiểm tra địa chỉ ví USDT trên blockchain Tron có bị blacklist hay không, trả kết quả ngay qua Telegram. Giúp các sếp tránh rủi ro giao dịch với ví bị cấm, tiết kiệm thời gian và bảo mật giao dịch."
slug: kiem-tra-tron-wallet-usdt-blacklist-qua-telegram
tags: [n8n, blockchain, tron, usdt, blacklist, telegram, automation, finance, crypto]
keywords: [n8n workflow tron usdt, kiểm tra ví blacklist tron, tự động hóa kiểm tra ví crypto, telegram bot tron, an toàn giao dịch usdt tron]
---

# 🔍 **Kiểm tra Tron Wallet USDT Blacklist qua Telegram - Tự động hóa an toàn giao dịch**

### **Nỗi đau của các sếp khi giao dịch USDT trên Tron**
Giao dịch USDT trên blockchain Tron là một trong những hoạt động phổ biến nhất trong cộng đồng crypto. Tuy nhiên, việc kiểm tra thủ công xem một ví USDT có bị **blacklist** (cấm giao dịch) hay không là một quá trình tốn thời gian và dễ gây sai sót. Các sếp thường phải:
- **Tìm kiếm thủ công** trên các trang web hoặc API của Tron.
- **Lo lắng về rủi ro** giao dịch với ví bị cấm, dẫn đến mất tiền hoặc bị khóa tài khoản.
- **Không có cảnh báo kịp thời** khi giao dịch với ví blacklist.

**Workflow này giải quyết toàn bộ vấn đề đó!** Với chỉ một tin nhắn qua Telegram, các sếp sẽ nhận được kết quả **tự động** về trạng thái blacklist của ví USDT trên Tron, giúp **tiết kiệm thời gian, tăng an toàn và tối ưu hóa giao dịch**.

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Kiểm tra tức thì** trạng thái blacklist của bất kỳ ví USDT trên Tron nào chỉ bằng một tin nhắn Telegram.
- **Tự động hóa hoàn toàn** - không cần code, không cần phải mở nhiều tab browser.
- **An toàn tuyệt đối** - tránh giao dịch với ví bị cấm, giảm rủi ro mất tiền.
- **Hoạt động 24/7** - workflow chạy liên tục trên VPS, không phụ thuộc vào thời gian làm việc.
- **Dễ dàng mở rộng** - có thể kết hợp với các bot khác như Slack, Discord hoặc gửi báo cáo định kỳ.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Telegram** và **API Key Telegram Bot**:
   - Tạo một bot Telegram mới tại [@BotFather](https://t.me/BotFather) và lấy **API Token**.
   - Thêm bot vào nhóm hoặc chat cá nhân để nhận kết quả.
2. **Không cần API Key đặc biệt** cho Tron Blacklist API (workflow sẽ tự động gọi API từ Tron).
3. **N8n Self-hosted** (không thể chạy trên n8n.cloud vì yêu cầu API Telegram).
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/3797) hoặc copy toàn bộ JSON từ trang này.
- Mở **n8n Editor** và chọn **"Import Workflow"** → Dán JSON hoặc tải file `.json`.
- **Không cần chỉnh sửa** cấu trúc cơ bản của workflow.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này có **6 node chính**, nhưng chỉ cần **cấu hình 2 node quan trọng** sau:

##### **A. Cấu hình Telegram Trigger & Telegram Send Message**
- **Node: "Telegram Trigger"**
  - **Credentials**: Chọn `telegramApi` (đã tạo trước khi import).
  - **Chat ID**: Lấy từ link chat Telegram (ví dụ: `@YourBot?start=123456789` → `123456789`).
  - **Command**: Đặt là `/check` (sẽ yêu cầu các sếp gửi tin nhắn với cú pháp `/check <wallet_address>`).

- **Node: "Telegram Send Message"**
  - **Credentials**: Chọn `telegramApi` (giống node trước).
  - **Chat ID**: Giống node Telegram Trigger.
  - **Message**: Workflow sẽ tự động gửi kết quả (ví dụ: *"Ví TRX... đã bị blacklist!"*).

##### **B. Cấu hình Node "Check Wallet Address Format" (If Node)**
- **Condition**: Kiểm tra xem địa chỉ ví có đúng định dạng **TRX** (ví dụ: `TRX...`) hay không.
- **Nếu sai định dạng**:
  - Node **"Set Error Message (Wallet Address Format)"** sẽ gửi tin nhắn lỗi: *"Địa chỉ ví không hợp lệ!"*.

##### **C. Node "Tron BlackList Stable Token Api Request"**
- **Method**: `GET`
- **URL**: `https://api.trongrid.io/wallet/blacklist/{wallet_address}`
  *(Workflows sẽ tự động thay thế `{wallet_address}` từ input của Telegram.)*
- **Headers**: Không cần thêm (API Tron không yêu cầu headers).

##### **D. Node "Check Api Response" (Code Node)**
- **Logic**: Kiểm tra phản hồi từ API Tron:
  ```javascript
  // Nếu API trả về "blacklisted": true → gửi tin nhắn cảnh báo.
  // Nếu API trả về "blacklisted": false → gửi tin nhắn an toàn.
  ```
- **Lưu ý**: Node này **không cần chỉnh sửa** vì đã được cấu hình sẵn trong workflow gốc.

---

#### **3. Kích hoạt ⚡️**
1. **Test Run** với một ví mẫu (ví dụ: `/check TRX...`).
   - Nếu ví **không bị blacklist**, sẽ nhận tin nhắn: *"Ví TRX... đang hoạt động bình thường!"*.
   - Nếu ví **bị blacklist**, sẽ nhận tin nhắn: *"⚠️ Cảnh báo: Ví TRX... đã bị blacklist!"*.
2. **Bật Active workflow** và **đặt lên VPS** để chạy 24/7.

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::info[CÁCH SỬ DỤNG HIỆU QUẢ]
1. **Kết hợp với Slack/Email**:
   - Thêm node **Slack** hoặc **Email** để gửi báo cáo cho team khi phát hiện ví blacklist.
2. **Lưu log giao dịch**:
   - Sử dụng node **Google Sheets** hoặc **Notion** để ghi lại lịch sử kiểm tra.
3. **Tự động cảnh báo định kỳ**:
   - Sử dụng **n8n Scheduler** để kiểm tra ví của khách hàng hàng ngày.
4. **Tạo bot cá nhân**:
   - Mỗi sếp có thể tạo bot riêng và chia sẻ với team để kiểm tra ví của khách hàng.
:::

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** để các sếp **tự động hóa kiểm tra blacklist USDT trên Tron** một cách nhanh chóng và an toàn. **Không cần code, không cần phải mở nhiều tab**, chỉ cần một tin nhắn Telegram là có kết quả tức thì.

**Hãy áp dụng ngay để:**
✅ **Tiết kiệm thời gian** kiểm tra ví.
✅ **Tránh rủi ro giao dịch** với ví bị cấm.
✅ **Tăng cường an toàn** cho giao dịch USDT trên Tron.

---
:::success[🚀 BẮT ĐẦU NGÀY HÔM NAY]
- **Cài n8n trên VPS** để workflow chạy 24/7.
- **Tạo bot Telegram** và chia sẻ với team.
- **Kiểm tra ví USDT** một cách tự động hóa!
:::