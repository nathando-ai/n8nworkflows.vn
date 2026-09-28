---
title: "🤖 Tự Động Hóa Email + Telegram + AI: Phân Loại & Trả Lời Tự Động Với Azure OpenAI & Google Sheets"
description: "Workflow tự động hóa hoàn chỉnh giúp phân loại email vào 5 danh mục (an ninh, cá nhân, cập nhật, quảng cáo, không quan trọng) và gửi cảnh báo Telegram tự động. Kết hợp AI Azure OpenAI để tổng hợp nội dung email và trả lời thông minh cho người dùng."
slug: "tieu-dong-hoa-email-telegram-azure-openai-google-sheets"
tags: [n8n, automation, no-code, azure-openai, google-sheets, telegram-bot, ai-summarization, email-management]
keywords: [n8n workflow email, tự động hóa email Telegram, phân loại email bằng AI, Azure OpenAI n8n, Google Sheets tự động, bot Telegram trả lời thông minh]
---

# 🚀 **Tự Động Hóa Email + Telegram: Phân Loại & Trả Lời Tự Động Với AI Azure OpenAI**

### **Giải pháp cho những ai:**
- **Mệt mỏi phải kiểm tra hàng trăm email hàng ngày** và phải phân loại thủ công?
- **Muốn được cảnh báo ngay khi có email quan trọng** (an ninh, cập nhật công việc) mà không cần mở email?
- **Thích sử dụng AI để tổng hợp và trả lời email** thay vì làm thủ công?
- **Cần một hệ thống tự động hóa email + Telegram** mà không cần viết code?

Workflow này sẽ **tự động phân loại email** vào 5 danh mục khác nhau và **gửi cảnh báo Telegram** khi có email quan trọng. Ngoài ra, bạn còn có thể **trả lời email thông minh** bằng AI Azure OpenAI khi cần!

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Không phải mở email thủ công, AI tự phân loại và cảnh báo.
✅ **Trả lời email thông minh**: Sử dụng Azure OpenAI để tổng hợp và trả lời email thay vì bạn.
✅ **Cảnh báo Telegram tự động**: Nhận thông báo ngay khi có email an ninh, cập nhật hoặc cá nhân.
✅ **Dữ liệu email được lưu trữ sạch sẽ**: Tất cả email được phân loại và lưu vào Google Sheets.
✅ **Hoạt động 24/7**: Không cần phải mở máy tính, workflow chạy tự động.
:::

---

## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Bạn cần chuẩn bị các tài khoản và API keys sau để workflow hoạt động:
1. **Tài khoản Gmail** (để lấy email qua IMAP):
   - Bật **2FA (Two-Factor Authentication)** và tạo **App Password** (nếu sử dụng Gmail với 2FA).
   - [Hướng dẫn chi tiết](https://docs.n8n.io/integrations/builtin/credentials/imap/gmail/#enable-2-step-verification).

2. **Tài khoản Google Cloud** (để kết nối Google Sheets):
   - Tạo **Google Cloud Project** và bật **Google Sheets API**.
   - [Hướng dẫn chi tiết](https://docs.n8n.io/integrations/builtin/credentials/google/oauth-single-service/).

3. **Azure OpenAI API Key** (hoặc OpenAI/Gemini nếu muốn thay thế):
   - Tạo **Azure OpenAI Account** và lấy **API Key**.
   - [Hướng dẫn tạo Azure OpenAI](https://learn.microsoft.com/en-us/azure/ai-services/openai/).

4. **Bot Telegram** (để nhận cảnh báo và tương tác):
   - Tạo bot Telegram bằng cách chat với `@BotFather` và lấy **API Token**.
   - [Hướng dẫn chi tiết](https://docs.n8n.io/integrations/builtin/credentials/telegram/).

5. **Google Sheets** (để lưu trữ dữ liệu email):
   - Tạo **bảng Google Sheets** với các sheet sau (đặt tên chính xác như trong workflow):
     - `user_ids` (lưu ID Telegram của người dùng).
     - `emails` (lưu thông tin email).
     - `checked_emails` (lưu email đã được kiểm tra).
     - `unimportant_emails` (lưu email không quan trọng).
     - `advertisements` (lưu email quảng cáo).
     - `updates` (lưu email cập nhật).
     - `personal` (lưu email cá nhân).
     - `security` (lưu email an ninh).
:::

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/6736](https://n8n.io/workflows/6736) hoặc copy/paste JSON từ trang này.
- Mở **n8n Editor** → Nhấn **Import Workflow** → Chọn file JSON hoặc dán JSON vào ô nhập liệu.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này có **2 phần chính**:
- **Phần 1**: Phân loại email và gửi cảnh báo Telegram.
- **Phần 2**: Trả lời email thông minh khi người dùng nhắn tin Telegram.

#### **🔹 Phần 1: Phân loại email và cảnh báo Telegram**
1. **Email Trigger (IMAP)**
   - Chọn **credentials** là `imap` (đã tạo từ Gmail).
   - Đặt **Server**: `imap.gmail.com` (hoặc `imap.mail.yourdomain.com` nếu dùng email doanh nghiệp).
   - **Port**: `993` (SSL/TLS).
   - **Username**: Email của bạn.
   - **Password**: App Password (nếu đã bật 2FA).

2. **Telegram Trigger (để bắt đầu workflow)**
   - Chọn **credentials** là `telegramApi` (API Token từ BotFather).
   - **Update**: Bật **Only for me** (để chỉ bạn mới có thể kích hoạt).

3. **Azure OpenAI Classifier (phân loại email)**
   - Chọn **credentials** là `azureOpenAiApi`.
   - **Model**: `gpt-4o-mini` (hoặc model khác nếu muốn thay đổi).
   - **Prompt**: AI sẽ phân loại email vào 5 danh mục:
     - **Security** (an ninh: thay đổi mật khẩu, đăng nhập từ địa chỉ mới).
     - **Personal** (cá nhân: email từ bạn bè, gia đình).
     - **Updates** (cập nhật: tin tức, công việc, cộng đồng).
     - **Advertisement** (quảng cáo: email marketing).
     - **Unimportant** (không quan trọng: spam, email không cần chú ý).

4. **Google Sheets (lưu dữ liệu email)**
   - Chọn **credentials** là `googleSheetsOAuth2Api`.
   - **Sheet Name**: Đặt tên chính xác với sheet trong Google Sheets (ví dụ: `emails`, `security`, `personal`...).
   - **Operation**: `append` (thêm mới) hoặc `update` (cập nhật).

5. **Telegram Alerts (gửi cảnh báo)**
   - Chọn **credentials** là `telegramApi`.
   - **Message**: Tùy chỉnh nội dung cảnh báo (ví dụ: `🚨 Email an ninh mới: [Tiêu đề]`).

#### **🔹 Phần 2: Trả lời email thông minh**
1. **Get E-Mails (lấy email chưa đọc)**
   - Chọn **credentials** là `googleSheetsOAuth2Api`.
   - **Sheet Name**: `emails` (sheet lưu email chưa đọc).
   - **Query**: Lấy email có `status = NOT CHECKED`.

2. **AI Agent (Azure OpenAI)**
   - Chọn **credentials** là `azureOpenAiApi`.
   - **Model**: `gpt-4o-mini`.
   - **System Prompt**: AI sẽ tổng hợp và trả lời email dựa trên nội dung.
   - **Tools**: AI có thể **cập nhật trạng thái email** (đánh dấu đã đọc) bằng `Update Status`.

3. **Reply To User (trả lời Telegram)**
   - Chọn **credentials** là `telegramApi`.
   - **Message**: Nội dung trả lời từ AI.

---

### **3. Kích hoạt ⚡️**
1. **Test Run** (kiểm tra workflow):
   - Nhấn **Run Workflow** và kiểm tra các node hoạt động như thế nào.
   - Đảm bảo **Google Sheets** và **Telegram** nhận được thông báo đúng.

2. **Bật Active**:
   - Sau khi test thành công, chuyển **Active** sang `ON`.

---

## ✍️ **Mẹo & gợi ý nâng cao**
:::info[CẢNH BÁO & MỆNH CHỦ]
- **Không nên dùng email chính của công ty** để test (rủi ro bị hack).
- **Nếu email nhiều**, có thể **tăng thời gian delay** giữa các lần lấy email (tránh bị Azure OpenAI giới hạn token).
- **Thay đổi model AI**: Nếu `gpt-4o-mini` quá đắt, có thể dùng `gpt-3.5-turbo` (rẻ hơn).
- **Lưu log**: Thêm node **Set** trước **Google Sheets** để lưu log debug.
- **Tự động xóa email cũ**: Thêm node **Delete Email** (IMAP) sau khi AI đã xử lý.
- **Kết hợp với Slack**: Thay vì Telegram, có thể gửi cảnh báo qua Slack.
- **Tạo dashboard**: Sử dụng **Google Data Studio** để theo dõi email đã phân loại.
:::

---

## 📌 **Kết luận**
Workflow này **giải phóng bạn khỏi việc phải mở email thủ công** và **tự động hóa toàn bộ quy trình phân loại, cảnh báo và trả lời email** bằng AI. Bạn chỉ cần:
1. **Cài đặt các credentials** (Gmail, Google Sheets, Azure OpenAI, Telegram).
2. **Import workflow** và **chỉnh sửa sheet Google Sheets** theo tên trong workflow.
3. **Bật Active** và **nhận cảnh báo Telegram** khi có email quan trọng!

**🚀 Hãy áp dụng ngay và tự động hóa email của mình!**

---
:::note[CHÚ Ý]
- Nếu gặp lỗi **CORS** với Google Sheets, kiểm tra lại **OAuth consent screen** trong Google Cloud.
- Nếu **Azure OpenAI bị giới hạn token**, giảm số lượng email được xử lý cùng một lúc.
- **Không nên dùng email chính của công ty** để test (rủi ro bị hack).
:::

---
**🎁 Mã giảm giá VPS cho n8n (Self-hosted):**
:::info[GỢI Ý HẠT ĐẦU]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng** (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::