---
title: "🤖 **Tự Động Hóa Chat Trực Tuyến Với Tài Liệu PDF Bằng Telegram + AI RAG (Không Cần Code!)**"
description: "Workflow này giúp các sếp tự động hóa việc tra cứu thông tin từ nhiều tài liệu PDF thông qua Telegram, sử dụng công nghệ AI RAG vectorless của PageIndex. Thay vì tốn thời gian tìm kiếm thủ công, chỉ cần gửi PDF một lần và chat với AI để nhận câu trả lời chính xác, có nguồn gốc từ trang nào trong tài liệu. Hoạt động 24/7, tiết kiệm thời gian và tăng hiệu suất làm việc."
slug: "tieu-dong-hoa-chat-voi-pdf-bang-telegram-ai-rag"
tags: [n8n, automation, ai-rag, telegram-bot, pageindex, no-code, pdf-automation]
keywords: [n8n workflow pdf telegram, tự động hóa tra cứu pdf, ai rag vectorless, chatbot pdf telegram, tự động hóa văn phòng, công cụ tra cứu thông tin]
---

# 🚀 **Tự Động Hóa Chat Trực Tuyến Với Tài Liệu PDF Bằng Telegram + AI RAG (Không Cần Code)**

## 📌 **Nỗi Đau Của Các Sếp**
Các sếp thường phải mất thời gian quý báu để:
- **Tìm kiếm thủ công** thông tin trong hàng chục tài liệu PDF.
- **Đọc lại nhiều trang** để xác nhận thông tin chính xác.
- **Quên mất nguồn gốc** của thông tin (trang nào, tài liệu nào).
- **Không thể tra cứu nhanh** khi cần giải đáp thắc mắc trong cuộc họp.

**Workflow này giải quyết tất cả!** Chỉ cần **gửi PDF một lần** vào Telegram, AI sẽ **tự động tạo chỉ mục** và **trả lời câu hỏi** của bạn với **câu trả lời chính xác + nguồn gốc từ trang nào**, mọi lúc mọi nơi.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng** (Self-hosted) để tránh giới hạn của phiên bản miễn phí.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (Đảm bảo tốc độ nhanh, không lag)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian** lên đến **90%** so với tra cứu thủ công.
✅ **Câu trả lời chính xác** với **nguồn gốc từ trang nào** (không phải giả mạo).
✅ **Hoạt động liên tục** (24/7) mà không cần can thiệp của con người.
✅ **Tích hợp Telegram** – tra cứu dễ dàng từ điện thoại, không cần mở máy tính.
✅ **Không cần code** – chỉ cần copy/paste workflow và cấu hình API.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Telegram** và **Token Bot** (tạo tại [@BotFather](https://t.me/BotFather)).
2. **API Key của PageIndex** (đăng ký tại [dash.pageindex.ai](https://dash.pageindex.ai/)).
3. **File PDF** (các sếp muốn tra cứu) để **nạp lên một lần**.
4. **n8n Editor** (cài đặt tại [n8n.io](https://n8n.io/) hoặc trên VPS).

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/13977](https://n8n.io/workflows/13977) (chọn **Export as JSON**).
2. **Mở n8n Editor** và nhấn **Import** → Chọn file JSON vừa tải.
3. **Chọn "Create new workflow"** và nhấn **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Tải JSON** từ link trên và **copy toàn bộ nội dung**.
2. Trong **n8n Editor**, nhấn **Import** → Chọn **Paste JSON** và dán vào.
3. **Tạo workflow mới** và nhấn **Import**.

---
### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **2 phần chính**:
- **Phần 1: Nạp PDF lên PageIndex** (chỉ cần làm **1 lần**).
- **Phần 2: Chat với AI để tra cứu** (hoạt động liên tục).

#### **📌 Cấu Hình Telegram Bot**
1. **Tạo Bot Telegram**:
   - Mở Telegram → Tìm `@BotFather` → Gửi `/newbot`.
   - Đặt tên bot (ví dụ: `PDFChatBot`) và nhận **Token Bot** (vd: `123456:ABC-DEF1234ghIkl-zyx57W2v1u123ew11`).
   - Lưu **Token Bot** này để sử dụng trong **n8n**.

2. **Thêm Credential Telegram trong n8n**:
   - Trong **n8n Editor**, nhấn **Credentials** (góc trên bên phải) → **Add Credential** → **Telegram**.
   - Điền:
     - **Token**: Paste Token Bot vừa lấy.
     - **Chat ID**: Lấy từ [@userinfobot](https://t.me/userinfobot) (gửi `/get_id` để nhận Chat ID cá nhân).
   - **Lưu credential** với tên **`telegramApi`**.

#### **📌 Cấu Hình PageIndex API Key**
1. **Đăng ký API Key**:
   - Truy cập [dash.pageindex.ai](https://dash.pageindex.ai/) → Đăng ký tài khoản.
   - Tạo **API Key** mới (giữ nó **an toàn**, không chia sẻ).

2. **Thêm Credential trong n8n**:
   - Trong **n8n Editor**, nhấn **Credentials** → **Add Credential** → **HTTP Header**.
   - Đặt tên **`pageindexApi`** và thêm header:
     ```
     Authorization: Bearer <API_KEY_CỦA_BẠN>
     ```
   - **Lưu credential**.

#### **📌 Cấu Hình Node HTTP Request (PageIndex)**
Trong **n8n Editor**, mở **node "Index PDF on PageIndex"** và **"LLM Reasoning over Document Tree"**:
- **URL Base**:
  ```
  https://api.pageindex.ai/v1
  ```
- **Headers**:
  - `Authorization`: Chọn **`pageindexApi`** (credential vừa tạo).
  - `Content-Type`: `application/json`.

#### **📌 Kích Hoạt Workflow**
1. **Test Flow 1 (Nạp PDF)**:
   - Gửi **file PDF** đến bot Telegram (nhắn tin với bot và chọn file PDF).
   - Kiểm tra **node "Index PDF on PageIndex"** có trả về `doc_id` không (vd: `pi-abc123`).

2. **Test Flow 2 (Chat với AI)**:
   - Gửi **câu hỏi** về nội dung PDF đã nạp (vd: *"Trang 5 nói gì về chiến lược?"*).
   - Kiểm tra bot trả lời có **đúng thông tin** và **có nguồn gốc trang** không.

3. **Bật Active**:
   - Nhấn **Active** trên workflow để **hoạt động liên tục**.

---
## ✍️ **Mẹo & Gợi Ý Nâng Cao**
### **1. Tích Hợp Với Slack/Email**
- **Gửi kết quả tra cứu** đến Slack/Email thay vì Telegram:
  - Thay thế **node "Send Answer to User"** bằng **Slack API** hoặc **Email Node** trong n8n.
  - Cấu hình **webhook Slack** hoặc **SMTP** để gửi thông báo.

### **2. Lưu Log Tra Cứu**
- **Ghi lại lịch sử câu hỏi** để theo dõi:
  - Thêm **node "Set"** sau **"Send Answer to User"** để lưu `question`, `answer`, và `doc_id` vào **Google Sheets** hoặc **Database**.
  - Dùng **node "Google Sheets"** để tự động ghi log.

### **3. Tự Động Nạp PDF Từ Google Drive/Dropbox**
- **Kết nối với Google Drive/Dropbox**:
  - Thêm **node "Google Drive"** hoặc **"Dropbox"** để tự động lấy file PDF mới.
  - Kết nối với **node "Download PDF File"** để nạp tự động.

### **4. Cập Nhật Tài Liệu Định Kỳ**
- **Chạy workflow tự động** mỗi tuần/mỗi tháng:
  - Sử dụng **node "Schedule"** trong n8n để **nạp lại PDF** nếu có thay đổi.

---
## 📌 **Kết Luận**
Workflow này **giải phóng thời gian** của các sếp để tập trung vào công việc chiến lược hơn, thay vì mất thời gian tra cứu thông tin trong hàng chục tài liệu PDF. **Chỉ cần nạp PDF một lần**, sau đó **chat với AI** để nhận câu trả lời **chính xác + có nguồn gốc**, mọi lúc mọi nơi.

**Hành động ngay!**
1. **Cài đặt n8n trên VPS** (để workflow hoạt động 24/7).
2. **Import workflow** và cấu hình **Telegram + PageIndex**.
3. **Test với PDF đầu tiên** và **tận hưởng hiệu quả tự động hóa!**

🚀 **Nếu có thắc mắc, hãy comment bên dưới hoặc liên hệ với chúng tôi!** Chúng tôi sẵn sàng hỗ trợ các sếp trong quá trình triển khai.