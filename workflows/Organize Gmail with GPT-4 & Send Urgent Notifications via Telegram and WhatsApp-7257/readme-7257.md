---
title: "🚀 Tự Động Hóa Gmail Với GPT-4 + Thông Báo Cấp Thiết Qua Telegram & WhatsApp (Không Cần Code)"
description: "Workflow này tự động phân loại, nhãn hóa email từ Gmail bằng trí tuệ nhân tạo (GPT-4, DeepSeek, Gemini) và gửi thông báo cấp thiết đến Telegram/WhatsApp khi cần. Giúp các sếp tiết kiệm 10+ giờ/ngày quản lý email và không bỏ lỡ tin nhắn quan trọng."
slug: "tieu-dong-hoa-gmail-voi-gpt4-notification-telegram-whatsapp"
tags: [n8n, automation, gmail, ai, gpt-4, telegram, whatsapp, no-code, ticket-management]
keywords: [tự động hóa gmail, gpt-4 trong n8n, thông báo telegram whatsapp, phân loại email bằng ai, workflow n8n gmail, quản lý email tự động]
---

# 🚀 **Tự Động Hóa Gmail Với GPT-4 + Thông Báo Cấp Thiết Qua Telegram & WhatsApp**

### **Giải pháp cho nỗi đau "Bị chìm trong email"**
Các sếp đã từng phải:
- **Lọc hàng trăm email** mỗi ngày để tìm tin nhắn quan trọng giữa spam và tin nhắn cá nhân?
- **Bỏ lỡ tin nhắn cấp thiết** vì không kịp thời theo dõi?
- **Phải nhãn hóa thủ công** email theo chủ đề (DevOps, Marketing, HR...) mất nhiều thời gian?

Workflow này **sử dụng trí tuệ nhân tạo (GPT-4, DeepSeek, Gemini)** để tự động:
✅ **Phân loại email** theo chủ đề (ví dụ: "Dev Tools" nếu sender là GitHub).
✅ **Nhãn hóa tự động** trên Gmail (không cần làm thủ công).
✅ **Xác định mức độ ưu tiên** (urgent/normal) và gửi **thông báo cấp thiết** đến Telegram/WhatsApp.
✅ **Tóm tắt email** bằng AI để các sếp chỉ cần đọc 2 câu chính.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** với tài nguyên mạnh để xử lý AI hiệu quả.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đủ cho workflow này chạy ổn định)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/ngày** quản lý email (phân loại, nhãn hóa, lọc tin nhắn quan trọng).
- **Không bỏ lỡ tin nhắn cấp thiết** nhờ thông báo tự động trên Telegram/WhatsApp.
- **Email được tổ chức logic** theo chủ đề (DevOps, Marketing, HR...) mà không cần làm thủ công.
- **Tóm tắt email bằng AI** giúp các sếp đọc nhanh chỉ trong 2 câu.
- **Hoạt động liên tục 24/7** (không cần can thiệp người dùng).
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Gmail** (cần **API Gmail được kích hoạt** và **OAuth 2.0** cấu hình).
2. **API Key cho các mô hình AI**:
   - **OpenAI API Key** (để sử dụng GPT-4.1-nano).
   - **OpenRouter API Key** (để sử dụng DeepSeek).
   - **Google Cloud API Key** (để sử dụng Gemini).
3. **Thông tin Telegram**:
   - **Token API** của bot Telegram.
   - **ID Chat** (hoặc username) để gửi thông báo.
4. **Số điện thoại WhatsApp** (đã đăng ký với API WhatsApp Business).
5. **Docker** (nếu tự host n8n trên VPS).

---
:::note[LƯU Ý QUAN TRỌNG]
- **Không cần code** – workflow đã sẵn sàng, chỉ cần cấu hình API.
- **Nếu không muốn tự host**, có thể dùng **n8n Cloud** (miễn phí cho workflow nhỏ).
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
**Cách 1: Từ file JSON**
1. Tải workflow từ [n8n.io/workflows/7257](https://n8n.io/workflows/7257) (chọn "Download JSON").
2. Trên n8n Editor, nhấn **"Import"** và chọn file JSON tải xuống.

**Cách 2: Copy/Paste JSON**
1. Copy toàn bộ JSON từ [n8n.io/workflows/7257](https://n8n.io/workflows/7257) (chọn "Copy JSON").
2. Trên n8n Editor, nhấn **"Import"** → **"Paste JSON"**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow có **23 node**, nhưng các node **quan trọng nhất** cần cấu hình như sau:

##### **A. Cấu hình Gmail**
1. **Node "Gmail Trigger1"**:
   - Đi đến **Credentials** → **"Add new"** → Chọn **"Gmail"**.
   - Đăng nhập Gmail và cấp quyền cho n8n.
   - Chọn **"Use OAuth 2.0"** (để lưu token an toàn).

2. **Node "Get Existing Labels1"**:
   - Không cần cấu hình thêm (n8n sẽ tự lấy danh sách nhãn hiện có).

3. **Node "Create Label if Doesn't exist1"**:
   - Điền **tên nhãn mới** (ví dụ: "Dev Tools", "Urgent") vào trường `name`.
   - N8n sẽ tự tạo nhãn nếu chưa có.

##### **B. Cấu hình AI (GPT-4, DeepSeek, Gemini)**
1. **Node "OpenAI Chat Model" (GPT-4.1-nano)**:
   - Đi đến **Credentials** → **"Add new"** → **"OpenAI"**.
   - Điền **API Key** từ OpenAI.
   - Chọn mô hình: `gpt-4.1-nano`.

2. **Node "OpenRouter Chat Model2/3" (DeepSeek)**:
   - Đi đến **Credentials** → **"Add new"** → **"OpenRouter"**.
   - Điền **API Key** từ OpenRouter.
   - Chọn mô hình: `deepseek/deepseek-chat-v3-0324:free`.

3. **Node "Google Gemini Chat Model2/3"**:
   - Đi đến **Credentials** → **"Add new"** → **"Google Cloud"**.
   - Điền **API Key** từ Google Cloud.
   - Chọn mô hình: `gemini-pro`.

##### **C. Cấu hình Telegram & WhatsApp**
1. **Node "Send a text message1" (Telegram)**:
   - Đi đến **Credentials** → **"Add new"** → **"Telegram"**.
   - Điền **Token API** của bot Telegram (mua trên [@BotFather](https://t.me/BotFather)).
   - Điền **ID Chat** (hoặc username) của nhóm/đối thoại muốn nhận thông báo.

2. **Node "Send message1" (WhatsApp)**:
   - Đi đến **Credentials** → **"Add new"** → **"WhatsApp"**.
   - Điền **Số điện thoại** (ví dụ: `+84123456789`) và **API Key** từ nhà cung cấp (ví dụ: Twilio, MessageBird).

##### **D. Cấu hình Prompt cho AI**
Workflow đã **sẵn sàng prompt** để phân loại email và xác định mức độ ưu tiên. Các sếp có thể **tùy chỉnh** trong node **"AI Agent1"** và **"AI Agent3"** bằng cách:
- Nhấn **double-click** vào node.
- Chỉnh sửa **Prompt** trong tab **"Code"**.
- Ví dụ:
  ```json
  "prompt": "Analyze the email content and classify it into one of these categories: Dev Tools, Marketing, HR, Finance, Urgent. If the sender is GitHub, classify as 'Dev Tools'. If the subject contains 'urgent' or 'ASAP', classify as 'Urgent'. Return only the category name."
  ```

#### **3. Kích hoạt ⚡️**
1. **Test Run** với email mẫu:
   - Gửi email mẫu đến Gmail (ví dụ: từ `support@github.com` với tiêu đề "Urgent: Bug in DevOps").
   - Nhấn **"Run Workflow"** trên n8n Editor để kiểm tra.
   - Kiểm tra:
     - Email có được nhãn hóa không?
     - Có thông báo trên Telegram/WhatsApp không?
     - Tóm tắt email có logic không?

2. **Bật Active**:
   - Sau khi test thành công, nhấn **"Active"** trên workflow.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Google Sheets để lưu log**:
   - Thêm node **"Google Sheets"** sau node **"Add label to thread1"** để ghi lại lịch sử nhãn hóa.
   - Cấu hình để lưu **ID email, chủ đề, ngày giờ, người gửi**.

2. **Gửi báo cáo định kỳ**:
   - Sử dụng node **"Wait"** + **"Google Sheets"** để tạo báo cáo hàng ngày về số email được phân loại.

3. **Tùy chỉnh mức độ ưu tiên**:
   - Thay đổi **prompt** trong node **"AI Agent3"** để thêm/loại bỏ điều kiện phân loại (ví dụ: thêm "Legal" nếu email từ `legal@company.com`).

4. **Dùng Slack thay cho Telegram**:
   - Thay node **"Telegram"** bằng **"Slack"** và cấu hình với **API Key Slack**.

5. **Optimize chi phí AI**:
   - Thay **GPT-4.1-nano** bằng **GPT-3.5-turbo** (rẻ hơn) nếu không cần độ chính xác cao.

---

### 📌 **Kết luận**
Workflow này **giải phóng các sếp khỏi công việc nhàn nhạt** như phân loại email, nhãn hóa và theo dõi tin nhắn cấp thiết. Với **trí tuệ nhân tạo (GPT-4, DeepSeek, Gemini)** và **tự động hóa thông báo**, các sếp sẽ:
✔ **Tiết kiệm 10+ giờ/ngày**.
✔ **Không bỏ lỡ tin nhắn quan trọng**.
✔ **Email được tổ chức logic** mà không cần làm thủ công.

**Hành động ngay!**
1. **Import workflow** theo hướng dẫn trên.
2. **Cấu hình API** (Gmail, OpenAI, Telegram, WhatsApp).
3. **Test với email mẫu** và **bật Active**.
4. **Tận hưởng sự tự động hóa hoàn toàn!**

---
**💡 Cần hỗ trợ?**
- Trên [n8n Community](https://community.n8n.io/) hoặc liên hệ tác giả [Iniyavan JC](https://n8n.io/workflows/7257) để tùy chỉnh workflow cho doanh nghiệp của các sếp!