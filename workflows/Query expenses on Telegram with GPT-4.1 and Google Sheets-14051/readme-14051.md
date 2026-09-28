---
title: "🤖 **Tự Động Hóa Trả Lời Hỏi Đáp Chi Phí qua Telegram với GPT-4.1 & Google Sheets**"
description: "Workflow tự động hóa hoàn toàn giúp các sếp trả lời các câu hỏi về chi phí thông qua Telegram bằng trí tuệ nhân tạo, đồng thời tự động phân loại và giải quyết các mâu thuẫn về danh mục và người dùng. Tiết kiệm thời gian lên đến 80% so với cách làm thủ công."
slug: "tieu-dong-hoa-tra-loi-hoi-dap-chiphi-telegram-gpt4-google-sheets"
tags: [n8n, automation, no-code, ai-chatbot, google-sheets, telegram-bot, expense-tracking]
keywords: [n8n workflow tự động hóa, chatbot Telegram trả lời chi phí, GPT-4.1 tự động phân loại danh mục, tự động hóa quản lý chi tiêu, giải pháp không code cho doanh nghiệp]
---

# 🚀 **Tự Động Hóa Trả Lời Hỏi Đáp Chi Phí qua Telegram với GPT-4.1 & Google Sheets**

## **Giới Thiệu**
Các sếp đã bao giờ phải mất **30-60 phút** mỗi ngày để tra cứu, tổng hợp và trả lời các câu hỏi về chi phí cho đồng nghiệp hay khách hàng? Hay phải mở Google Sheets, lọc dữ liệu thủ công, rồi gửi kết quả qua Telegram? **Workflow này giải quyết tất cả những vấn đề đó!**

Bằng cách kết hợp **GPT-4.1 (OpenAI)**, **Google Sheets** và **Telegram Bot**, các sếp có thể:
✅ **Trả lời tự động** các câu hỏi như *"Tôi đã chi bao nhiêu tiền cho ăn uống tháng trước?"* chỉ bằng một tin nhắn Telegram.
✅ **Phân loại tự động** danh mục chi phí và người dùng, **học hỏi từ từng tương tác** để ngày càng chính xác hơn.
✅ **Tiết kiệm thời gian** lên đến **80%** so với cách làm thủ công.
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo bảo mật và hiệu suất tối ưu.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Trả lời hàng trăm câu hỏi chi phí chỉ trong vài giây.
- **Chính xác cao**: Phân loại danh mục và người dùng tự động, giảm sai sót.
- **Tự học và cải tiến**: Hệ thống **học hỏi từ từng tương tác**, ngày càng thông minh hơn.
- **Hoạt động liên tục**: Không cần can thiệp của con người, hoạt động 24/7.
- **Tích hợp hoàn hảo**: Kết nối với Telegram, Google Sheets và AI GPT-4.1 một cách tự động.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Telegram Bot**:
   - Tạo một bot mới trên [@BotFather](https://t.me/BotFather) và lấy **API Token**.
2. **Tài khoản OpenAI**:
   - Đăng ký [OpenAI](https://platform.openai.com/) và lấy **API Key** cho GPT-4.1-nano.
3. **Google Sheets**:
   - **5 bảng Google Sheets** với cấu trúc cụ thể (chi tiết ở phần sau).
4. **Chat IDs của người dùng**:
   - Mỗi người dùng cần **Chat ID** để xác thực. Các sếp có thể lấy Chat ID bằng cách gửi tin nhắn cho bot `@userinfobot` trên Telegram.

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Tải file JSON từ [n8n.io/workflows/14051](https://n8n.io/workflows/14051).
2. Trong **n8n Editor**, nhấn **Import** và chọn file JSON.
3. Hoặc copy toàn bộ JSON và dán vào **Import Workflow** trong giao diện.

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

Workflow được chia thành **6 Layer** chính. Các sếp cần chú ý cấu hình các node quan trọng sau:

#### **🟩 Layer 1 — Nhận tin nhắn Telegram (Input)**
- **MSG | Telegram Inbound**:
  - Đăng ký **Telegram API** vào node này.
  - Cấu hình **Chat IDs** cho phép trong node **IF | User Authorized?** (thay thế `1000000000`, `1000000001` bằng Chat IDs thực tế của người dùng).
- **TG | Confirm Category/Person Selection**:
  - Đăng ký cùng **Telegram API** như trên.

#### **🟦 Layer 2 — Phân tích ý định (Intent Parsing)**
- **LLM | Parse Intent**:
  - Đăng ký **OpenAI API** vào node này.

#### **🟨 Layer 3a — Giải quyết danh mục (Entity Resolution: Categories)**
- **GS | Read Category Mapping** & **GS | Save Category Mapping**:
  - Thay thế `YOUR_SPREADSHEET_ID` bằng **ID của bảng `categories_mapping`**.
  - Cấu trúc bảng cần có cột: `find` (danh mục người dùng nhập) và `replace` (danh mục chuẩn).
- **GS | Read Allowed Categories**:
  - Thay thế `YOUR_SPREADSHEET_ID` bằng **ID của bảng `expense_categories`**.
  - Cấu trúc bảng cần có cột: `category`, `description`, `examples`.
- **LLM | Classify Category**:
  - Đăng ký **OpenAI API** vào node này.
- **HTTP | Send Category Selection Message**:
  - Thay thế `{{YOUR_BOT_TOKEN}}` bằng **Token Telegram Bot** thực tế.

#### **🟠 Layer 3b — Giải quyết người dùng (Entity Resolution: Persons)**
- **GS | Read Person Mapping** & **GS | Save Person Mapping**:
  - Thay thế `YOUR_SPREADSHEET_ID` bằng **ID của bảng `person_mapping`**.
  - Cấu trúc bảng cần có cột: `find` (tên người dùng nhập) và `replace` (tên chuẩn).
- **GS | Read Allowed Persons**:
  - Thay thế `YOUR_SPREADSHEET_ID` bằng **ID của bảng `list_persons`**.
  - Cấu trúc bảng cần có cột: `person`, `description`.
- **LLM | Classify Person**:
  - Đăng ký **OpenAI API** vào node này.
- **HTTP | Send Person Selection Message**:
  - Thay thế `{{YOUR_BOT_TOKEN}}` bằng **Token Telegram Bot** thực tế.

#### **🟧 Layer 4 — Query Engine (Tải dữ liệu từ Google Sheets)**
- **GS | Load Expenses**:
  - Thay thế `YOUR_SPREADSHEET_ID` bằng **ID của bảng `expenses`**.
  - Cấu trúc bảng cần có cột: `date`, `amount`, `category`, `description`, `common_expense`, `Person`.
- **GS | Load Categories**:
  - Thay thế `YOUR_SPREADSHEET_ID` bằng **ID của bảng `expense_categories`**.
  - Cấu trúc bảng cần có cột: `category`, `description`, `examples`.

#### **🟥 Layer 5 — Tính toán và tổng hợp (Analytics & Aggregation)**
- **JS | Filter & Aggregate**:
  - Node này tự động xử lý dựa trên dữ liệu đã giải quyết từ các layer trước. **Không cần cấu hình thêm**.

#### **🟪 Layer 6 — Trả lời người dùng (Response)**
- **TG | Send Reply**:
  - Đăng ký **Telegram API** vào node này.
- **JS | Format Response Message**:
  - Các sếp có thể chỉnh sửa nội dung trả lời trong node này để phù hợp với ngôn ngữ hoặc định dạng mong muốn.

---

### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Gửi một tin nhắn mẫu (ví dụ: *"Hãy cho tôi biết tôi đã chi bao nhiêu tiền cho ăn uống tháng trước?"*) đến bot Telegram.
   - Kiểm tra workflow có hoạt động như mong đợi không.
2. **Bật Active**:
   - Sau khi kiểm tra xong, nhấn **Active** để workflow hoạt động liên tục.

---

## ✍️ **Mẹo & gợi ý nâng cao**
1. **Tích hợp với Slack/Email**:
   - Sử dụng node **HTTP Request** để gửi kết quả trả lời đến Slack hoặc Email thay vì chỉ Telegram.
2. **Lưu log hoạt động**:
   - Thêm node **Google Sheets** hoặc **Database** để lưu lịch sử các câu hỏi và trả lời.
3. **Báo cáo định kỳ**:
   - Tạo một workflow riêng để gửi báo cáo tổng hợp chi phí hàng tháng tự động qua Telegram.
4. **Cập nhật danh mục và người dùng**:
   - Khi thêm mới danh mục hoặc người dùng vào Google Sheets, hệ thống sẽ tự động học hỏi và áp dụng trong tương lai.

---

## 📌 **Kết luận**
Workflow này không chỉ **tự động hóa** quá trình trả lời các câu hỏi về chi phí mà còn **tự học và cải tiến** qua từng tương tác. Các sếp không cần viết một dòng code nào cả, chỉ cần cấu hình các node và kết nối với Telegram, Google Sheets và OpenAI.

**Hãy áp dụng ngay để tiết kiệm thời gian và nâng cao hiệu suất làm việc!** 🚀

---
**Bạn có bất kỳ câu hỏi nào về cách cấu hình chi tiết? Hãy để lại bình luận dưới đây!** 👇