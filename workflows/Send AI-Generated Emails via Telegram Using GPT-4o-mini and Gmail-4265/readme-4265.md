---
title: "🤖 Tự Động Gửi Email AI-Generated Từ Telegram Sử Dụng GPT-4o-mini & Gmail (Không Cần Code)"
description: "Workflow tự động hóa hoàn toàn giúp các sếp nhận tin nhắn Telegram, sử dụng GPT-4o-mini tạo nội dung email chuyên nghiệp, sau đó tự động gửi qua Gmail - tiết kiệm 90% thời gian so với làm thủ công."
slug: "tieu-dong-gui-email-ai-telegram-gmail"
tags: [n8n, automation, ai, gpt-4o-mini, telegram, gmail, no-code, email-marketing]
keywords: [n8n workflow telegram email, tự động hóa email bằng ai, gpt-4o-mini gửi email tự động, tự động hóa doanh nghiệp không code, giải pháp email marketing tự động]
---

# 🚀 **Tự Động Gửi Email AI-Generated Từ Telegram Sử Dụng GPT-4o-mini & Gmail**

### **Giải pháp hoàn hảo cho các sếp muốn:**
- **Tiết kiệm 90% thời gian** viết email hàng ngày
- **Tự động hóa tương tác khách hàng** qua Telegram
- **Tạo email cá nhân hóa** với GPT-4o-mini (mô hình AI mới nhất của OpenAI)
- **Hoạt động 24/7** mà không cần can thiệp thủ công

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần viết email thủ công, AI tự động tạo nội dung chuyên nghiệp.
- **Tương tác khách hàng nhanh chóng**: Trả lời tin nhắn Telegram ngay lập tức với email tự động.
- **Cá nhân hóa cao**: AI phân tích tin nhắn và tạo email phù hợp với từng trường hợp.
- **Hoạt động liên tục**: Workflow chạy tự động 24/7, không cần can thiệp.
- **Giảm sai sót**: AI giảm thiểu lỗi ngữ pháp và nội dung không phù hợp.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Telegram Bot**:
   - Tạo bot Telegram với quyền gửi tin nhắn (đăng ký tại [@BotFather](https://t.me/BotFather)).
   - Lấy **API Token** của bot và **Chat ID** của nhóm/đối tượng muốn gửi email.

2. **Tài khoản Gmail**:
   - Tài khoản Gmail có quyền gửi email (không phải là tài khoản Google Workspace nếu không cần thiết).
   - **App Password** (nếu sử dụng 2FA) hoặc **OAuth 2.0 Credentials** (khuyến nghị).

3. **API Key OpenAI**:
   - Đăng ký tại [OpenAI Platform](https://platform.openai.com/) và lấy **API Key** cho mô hình `gpt-4o-mini`.

4. **n8n Self-hosted**:
   - Workflow này yêu cầu **n8n tự cài đặt** (không chạy được trên n8n.cloud miễn phí).
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/4265](https://n8n.io/workflows/4265) hoặc copy toàn bộ JSON từ trang này.
- Mở **n8n Editor** và chọn **Import Workflow** → Dán JSON hoặc tải file `.json`.
- **Kích hoạt chế độ "Active"** sau khi import.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
##### **A. Cấu hình Telegram Trigger**
- **Node**: `Telegram Trigger`
- **Cấu hình**:
  - **Bot Token**: Điền **API Token** từ bot Telegram.
  - **Chat ID**: Điền **Chat ID** của nhóm/đối tượng muốn kích hoạt workflow.
  - **Trigger Phrase** (tuỳ chọn): Nếu muốn chỉ kích hoạt khi nhận tin nhắn chứa từ khóa cụ thể (ví dụ: "gửi email").

##### **B. Cấu hình AI Agent (GPT-4o-mini)**
- **Node**: `AI Agent`
- **Cấu hình**:
  - **Tool**: Chọn `Gmail` và `Telegram` (đã cấu hình sẵn trong workflow).
  - **Memory Buffer**: Chọn `Simple Memory` (để AI nhớ lịch sử tương tác).
  - **Model**: Đã mặc định là `gpt-4o-mini` (không cần chỉnh).

##### **C. Cấu hình OpenAI Chat Model**
- **Node**: `OpenAI Chat Model`
- **Cấu hình**:
  - **API Key**: Điền **API Key OpenAI** (từ OpenAI Platform).
  - **Model**: Đã mặc định là `gpt-4o-mini` (không cần chỉnh).
  - **Temperature**: Giữ mặc định (0.7) để AI tạo nội dung tự nhiên.

##### **D. Cấu hình Gmail**
- **Node**: `Gmail`
- **Cấu hình**:
  - **Authentication**: Chọn **OAuth 2.0** (khuyến nghị) hoặc **App Password** (nếu không dùng OAuth).
  - **Refresh Token**: Nếu dùng OAuth, lưu lại token sau khi đăng nhập.
  - **From Address**: Điền email Gmail muốn gửi (ví dụ: `tiengoc@domain.com`).
  - **Subject Template**: Điền mẫu tiêu đề email (ví dụ: `{{$json["subject"]}}`).
  - **Body Template**: Điền mẫu nội dung email (AI sẽ tự động điền nội dung từ tin nhắn Telegram).

##### **E. Cấu hình Telegram Send Message**
- **Node**: `Telegram`
- **Cấu hình**:
  - **Bot Token**: Điền **API Token** của bot Telegram (giống như ở Telegram Trigger).
  - **Chat ID**: Điền **Chat ID** của nhóm/đối tượng muốn nhận phản hồi từ AI.
  - **Message**: Để mặc định (AI sẽ tự động gửi tin nhắn phản hồi).

##### **F. Cấu hình Simple Memory**
- **Node**: `Simple Memory`
- **Cấu hình**:
  - **Window Size**: Giữ mặc định (3) để AI nhớ 3 tin nhắn gần nhất.
  - **Key**: Để mặc định (`memory`).

---

#### **3. Kích hoạt ⚡️**
1. **Test Run** với tin nhắn mẫu:
   - Gửi tin nhắn Telegram đến bot với nội dung như:
     ```
     Gửi email cho khách hàng ABC về đơn hàng #12345.
     ```
   - AI sẽ tự động:
     - Tạo email với tiêu đề và nội dung phù hợp.
     - Gửi email qua Gmail.
     - Trả lời tin nhắn Telegram với kết quả.

2. **Bật Active Workflow**:
   - Chuyển trạng thái workflow từ **Inactive** sang **Active**.

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Tích hợp Slack/Telegram Group**:
   - Thay vì chỉ gửi tin nhắn Telegram, có thể kết nối với Slack để thông báo kết quả gửi email.

2. **Lưu log hoạt động**:
   - Sử dụng **Sticky Note** để lưu lịch sử email đã gửi (giúp theo dõi và phân tích hiệu quả).

3. **Gửi báo cáo định kỳ**:
   - Tạo workflow phụ để gửi báo cáo tổng hợp số lượng email đã gửi hàng tháng qua Gmail.

4. **Cá nhân hóa email hơn**:
   - Sử dụng **custom prompt** trong OpenAI để AI tạo email phù hợp với từng ngành nghề (ví dụ: email bán hàng, hỗ trợ khách hàng, thông báo sự kiện).

5. **Kết hợp với Google Sheets**:
   - Lưu danh sách khách hàng và lịch sử tương tác vào Google Sheets để phân tích dữ liệu.
:::

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa quá trình gửi email từ Telegram với sự trợ giúp của AI. Bằng cách chỉ cần gửi tin nhắn, AI sẽ tự động:
✅ Tạo email chuyên nghiệp với GPT-4o-mini.
✅ Gửi email qua Gmail.
✅ Trả lời tin nhắn Telegram với kết quả.

**Hãy áp dụng ngay để tiết kiệm thời gian và nâng cao hiệu quả làm việc!** 🚀

---
:::note[LƯU Ý CUỐI CUNG]
- Nếu gặp lỗi **CORS** hoặc **API Rate Limit**, kiểm tra lại **API Key OpenAI** và **OAuth 2.0 Credentials** của Gmail.
- Để workflow chạy ổn định, **n8n cần được self-hosted** (không chạy được trên n8n.cloud miễn phí).
- Nếu cần hỗ trợ, tham khảo [n8n Community](https://community.n8n.io/) hoặc liên hệ với tác giả Marconi.
:::