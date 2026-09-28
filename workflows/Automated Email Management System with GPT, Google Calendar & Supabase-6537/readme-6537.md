---
title: "🤖 Hệ Thống Quản Lý Email Tự Động Hóa Với GPT, Google Calendar & Supabase – Giảm 80% Thời Gian Xử Lý Email"
description: "Workflow tự động hóa hoàn toàn cho doanh nghiệp, tự động phân loại, trả lời email leads, kiểm tra lịch Google Calendar và gửi thông báo Telegram – giúp các sếp tự động hóa inbox mà không cần code."
slug: "he-thong-quan-ly-email-tu-dong-hoa-gpt-google-calendar-supabase"
tags: [n8n, automation, no-code, ai-agent, gmail, google-calendar, supabase, telegram-bot, ai-rag, marketing-agency]
keywords: [tự động hóa email n8n, ai quản lý inbox, tự động trả lời email leads, workflow gmail google calendar, supabase vector db, chatbot tự động hóa doanh nghiệp, tự động hóa marketing agency]
---

# 🚀 **Hệ Thống Quản Lý Email Tự Động Hóa Với GPT, Google Calendar & Supabase**

## **📧 Bỏ Tự Xử Lý Email – AI Làm Mọi Việc Cho Bạn!**
Hàng ngày, các sếp phải mất **3-5 giờ** để xử lý email: phân loại, trả lời leads, kiểm tra lịch hẹn, và theo dõi khách hàng. **Workflow này tự động hóa toàn bộ quy trình** bằng AI, Google Calendar và cơ sở dữ liệu vector Supabase – giúp bạn **tiết kiệm 80% thời gian**, tập trung vào việc phát triển kinh doanh thay vì làm việc thủ công.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính riêng tư và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tự động phân loại email** (Sales, Client Comm, Billing, Reports, Other) chỉ trong vài giây.
✅ **Trả lời leads tự động** với lịch hẹn từ Google Calendar (không cần bạn can thiệp).
✅ **Trả lời FAQ từ cơ sở tri thức** (Supabase) mà không cần viết lại từ đầu.
✅ **Thông báo Telegram thực thời** khi có email mới cần xử lý.
✅ **Tiết kiệm 80% thời gian** cho việc xử lý email hàng ngày.
✅ **Hoạt động 24/7** – không cần phải mở máy tính để kiểm tra inbox.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Gmail** (đã cấu hình OAuth 2.0 cho n8n).
✔ **API Key OpenAI** (để sử dụng GPT-4.1 hoặc GPT-4.1-mini).
✔ **Google Calendar API** (để kiểm tra lịch hẹn tự động).
✔ **Supabase Account** (để lưu trữ cơ sở tri thức vector).
✔ **Telegram Bot Token** (để nhận thông báo).
✔ **N8n Self-hosted** (không dùng phiên bản cloud để đảm bảo an toàn dữ liệu).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/6537](https://n8n.io/workflows/6537) hoặc copy/paste JSON từ trang này.
- Mở **n8n Editor** → Nhấn **"Import"** → Chọn file JSON hoặc dán JSON vào ô.
- **Kích hoạt workflow** bằng cách bật nút **"Active"** ở góc trên bên phải.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **34 node** và hoạt động theo logic sau:
1. **Gmail Trigger** → Nhận tất cả email mới vào inbox.
2. **Text Classifier** → Phân loại email vào danh mục (Sales, Client Comm, Billing, Reports, Other).
3. **AI Agents** (Calendar Agent & Knowledge Agent) → Trả lời tự động hoặc kiểm tra lịch.
4. **Supabase Vector Store** → Lưu trữ và tra cứu tri thức từ tài liệu doanh nghiệp.
5. **Telegram Bot** → Gửi thông báo khi có email mới cần xử lý.

##### **Cấu hình chi tiết các node quan trọng:**
| **Node**               | **Lưu ý cấu hình**                                                                 | **Tham số cần điền**                          |
|------------------------|-----------------------------------------------------------------------------------|-----------------------------------------------|
| **Gmail Trigger**      | Chọn tài khoản Gmail đã cấu hình OAuth 2.0.                                      | `gmailOAuth2`                                 |
| **OpenAI Chat Model**  | Chọn mô hình `gpt-4.1` hoặc `gpt-4.1-mini` (tùy budget).                          | `openAiApi` (API Key OpenAI)                  |
| **Google Calendar**    | Cấu hình OAuth 2.0 cho Google Calendar.                                           | `googleCalendarOAuth2Api`                     |
| **Supabase Vector Store** | Thêm URL và API Key của Supabase.                                               | `supabaseApi` (URL + Key)                     |
| **Telegram Bot**       | Nhập `Bot Token` từ @BotFather Telegram.                                         | `telegramApi` (Token)                        |
| **Labels Gmail**       | Đảm bảo các label (Sales, Client Comm, etc.) đã tồn tại trong Gmail.              | Không cần cấu hình thêm.                     |

##### **Cách cấu hình AI Agents:**
- **Calendar Agent** sẽ kiểm tra lịch Google Calendar và **draft email** với thời gian trống.
- **Knowledge Agent** sẽ tra cứu từ **Supabase Vector Store** và trả lời dựa trên tri thức doanh nghiệp.
- **Structured Output Parser** đảm bảo AI trả lời theo định dạng chuẩn (JSON).

#### **3. Kích hoạt ⚡️**
- **Test Run** với email mẫu (ví dụ: một email từ lead mới).
- **Bật Active** sau khi kiểm tra workflow hoạt động ổn định.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tăng tính cá nhân hóa**:
   - Thêm **các biến động** (như tên khách hàng) vào email draft bằng **Code Node**.
   - Ví dụ: `{{ $json["name"] }}` để chào tên khách hàng.

2. **Thêm Slack/Email Alerts**:
   - Thay vì Telegram, các sếp có thể **gửi thông báo Slack** bằng node `slackWebhook`.
   - Hoặc **gửi email tự động** bằng node `gmail` với `operation: send`.

3. **Lưu log hoạt động**:
   - Sử dụng **Sticky Note Node** để ghi lại lịch sử phản hồi của AI.
   - Hoặc kết nối với **Google Sheets** để theo dõi tất cả email đã xử lý.

4. **Escalate (xử lý thủ công)**:
   - Nếu AI không chắc chắn, **chuyển email sang danh mục "Other"** và gửi thông báo Telegram:
     *"Email này cần review thủ công. Kiểm tra tại: [link Gmail]."*

5. **Tối ưu hóa Supabase**:
   - Nếu cơ sở tri thức lớn, **tăng size vector store** để AI trả lời chính xác hơn.
   - Sử dụng **embeddings OpenAI** để cải thiện chất lượng tra cứu.

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp, marketing agency và doanh nghiệp cần **tự động hóa inbox** mà không cần viết code. Bằng cách kết hợp **AI (GPT), Google Calendar và Supabase**, hệ thống này **phân loại, trả lời và quản lý email tự động** – giúp bạn **tiết kiệm thời gian, tăng hiệu suất và giảm stress**.

**Hành động ngay!**
1. **Import workflow** vào n8n của mình.
2. **Cấu hình các API Key** (Gmail, OpenAI, Google Calendar, Supabase, Telegram).
3. **Test với email mẫu** và **bật Active**.
4. **Tận hưởng inbox tự động hóa!**

👉 **Bạn có thể tùy chỉnh workflow này** để phù hợp với nhu cầu cụ thể của doanh nghiệp. Nếu cần hỗ trợ, liên hệ với tác giả **Abdul Mir** qua [builtbyabdul@gmail.com](mailto:builtbyabdul@gmail.com) hoặc [website](https://www.builtbyabdul.com/).

**Chúc các sếp thành công với inbox tự động hóa!** 🚀