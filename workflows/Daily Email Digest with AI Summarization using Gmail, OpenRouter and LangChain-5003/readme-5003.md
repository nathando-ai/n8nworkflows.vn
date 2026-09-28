---
title: "🚀 Tự Động Hóa Email Hàng Ngày Với Tóm Tắt AI - Giảm 50 Email/Ngày Thành 1 Báo Cáo Cực Ngắn"
description: "Workflow tự động hóa lấy tất cả email trong 24h qua, tóm tắt bằng AI (OpenRouter + LangChain), và gửi báo cáo hàng ngày vào 8h sáng - tiết kiệm 3+ giờ làm việc hàng tuần cho các sếp."
slug: "tieu-dong-hoa-email-daily-digest-ai-summarization"
tags: [n8n, automation, ai, gmail, langchain]
keywords: [tự động hóa email, tóm tắt email bằng AI, n8n workflow, OpenRouter, LangChain, báo cáo hàng ngày]
---

# 🚀 **Tự Động Hóa Email Hàng Ngày Với Tóm Tắt AI - Giảm 50 Email Thành 1 Báo Cáo Cực Ngắn**

### **Nỗi Đau Của Các Sếp**
Mỗi sáng, các sếp phải mất **30-60 phút** để:
- Quét qua **50+ email** trong hộp thư.
- Lọc bỏ spam, tin nhắn không quan trọng.
- Tóm tắt nội dung dài thành những điểm chính.
- Gửi báo cáo tổng hợp cho team.

**Kết quả?** Thời gian quý giá bị "chôn vùi" trong email, còn những thông tin quan trọng lại bị bỏ lỡ vì quá nhiều thông tin rối loạn.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 3+ giờ/ngày** bằng cách tự động hóa việc tóm tắt email.
- **Chỉ cần 1 email báo cáo** thay vì 50 tin nhắn rối loạn.
- **AI phân loại tự động**: Nhận diện updates, vấn đề cần xử lý, và hành động cần thực hiện.
- **Hoạt động 24/7**: Không cần can thiệp thủ công, chạy tự động vào 8h sáng (IST).
- **Chính xác cao**: LangChain + OpenRouter tóm tắt với logic AI, không bỏ sót chi tiết.
:::

---
### **🔧 Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow này hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Gmail** (đã kích hoạt Gmail API và OAuth2).
2. **API Key OpenRouter** (đăng ký tại [OpenRouter](https://openrouter.ai/)).
3. **Danh sách người nhận** (cấu hình trong biến môi trường hoặc node Gmail).
4. **n8n Self-hosted** (không dùng phiên bản miễn phí để đảm bảo chạy 24/7).
:::

---
### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/5003](https://n8n.io/workflows/5003) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/5003) và paste vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflows này gồm **7 node** quan trọng, các sếp cần cấu hình kỹ như sau:

##### **A. Node "Daily 8AM Trigger" (n8n-nodes-base.scheduleTrigger)**
- **Thời gian chạy**: **8h sáng IST (7h UTC)** (thứ 2 đến thứ 6).
- **Lưu ý**:
  - Đảm bảo **timezone** trong n8n được đặt đúng (UTC+7 cho Việt Nam).
  - Nếu muốn chạy khác giờ, chỉnh `cron` trong node này (ví dụ: `0 1 8 * * 1-5` cho 8h sáng thứ 2-6).

##### **B. Node "Fetch Emails - Past 24 Hours" (n8n-nodes-base.gmail)**
- **Operation**: `getAll` (lấy tất cả email trong 24h qua).
- **Credentials**:
  - Chọn **Gmail OAuth2** đã cấu hình trước.
  - **Scope**: `https://www.googleapis.com/auth/gmail.readonly` (đọc email).
- **Lưu ý**:
  - Đảm bảo tài khoản Gmail đã **bật Gmail API** (cài đặt tại [Google Cloud Console](https://console.cloud.google.com/)).
  - Nếu email quá nhiều, có thể **lọc theo label** (ví dụ: chỉ lấy email từ "Work").

##### **C. Node "OpenRouter Chat Model" (n8n-nodes-langchain.lmChatOpenRouter)**
- **Credentials**:
  - Chọn **openRouterApi** (đã cấu hình trước với `OPENROUTER_KEY`).
- **Parameters**:
  - **Model**: Chọn mô hình phù hợp (ví dụ: `openrouter/mistral-7b`).
  - **Temperature**: 0.7 (để kết quả logic hơn).
  - **Max Tokens**: 500 (đủ cho tóm tắt email dài).
- **Lưu ý**:
  - Nếu API OpenRouter bị lỗi, thử mô hình khác (ví dụ: `openrouter/mistral-7b-instruct`).
  - **Giá API**: ~$0.0005/1000 tokens (rẻ, phù hợp cho tóm tắt email).

##### **D. Node "Email Summarizer" (n8n-nodes-langchain.agent)**
- **Prompt Template**:
  ```plaintext
  Tóm tắt email dưới dạng:
  1. **Updates**: Các tin tức mới (ví dụ: dự án hoàn thành, meeting sắp tới).
  2. **Issues**: Vấn đề cần giải quyết (ví dụ: khách hàng phản hồi, lỗi hệ thống).
  3. **Actions**: Hành động cần thực hiện (ví dụ: "Xác nhận với Team X", "Gửi file Y").
  ```
- **Memory Buffer (Simple Memory)**:
  - Node này giúp AI **nhớ** email trước đó (nếu muốn tích hợp lịch sử).
  - **Window Size**: 3 (lưu 3 email gần nhất để AI so sánh).
- **Lưu ý**:
  - Nếu AI tóm tắt không chính xác, chỉnh **prompt** hoặc thử mô hình khác.

##### **E. Node "Send Summary - Morning" (n8n-nodes-base.gmail)**
- **Credentials**: Chọn **Gmail OAuth2** (cùng tài khoản đã lấy email).
- **Recipients**: Điền **địa chỉ email** của team (ví dụ: `team@quantana.vn`).
- **Subject**: `📊 Daily Digest - [Ngày]` (ví dụ: `📊 Daily Digest - 10/10/2024`).
- **Body Template**:
  ```plaintext
  Chào các sếp,

  Đây là **báo cáo tóm tắt email hàng ngày** (8h sáng IST):

  {{ $json["summary"].body }}

  Trân trọng,
  AI Assistant
  ```
- **Lưu ý**:
  - **Kiểm tra email mẫu** trước khi gửi thật.
  - Nếu email gửi không thành công, check **credentials Gmail** và **quyền API**.

---
#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Chọn **Run Workflow** và kiểm tra:
     - Email có được lấy không?
     - AI có tóm tắt chính xác không?
     - Email báo cáo có gửi được không?
2. **Bật Active**:
   - Sau khi test thành công, **bật Active** cho node **Daily 8AM Trigger**.

---
### **✍️ Mẹo & Gợi Ý Nâng Cao**
1. **Gửi Báo Cáo Sang Slack/Telegram**:
   - Thêm node **Slack Webhook** hoặc **Telegram Bot** sau node **Send Summary** để thông báo ngay khi có báo cáo mới.
   - **Cài đặt**:
     - Node **Slack**: Chọn **Webhook URL** từ Slack (Settings > Custom Integrations > Incoming Webhooks).
     - Node **Telegram**: Sử dụng API Bot Telegram và cấu hình `chat_id`.

2. **Lưu Log Lịch Sử**:
   - Thêm node **StickyNote** (n8n-nodes-base.stickyNote) để lưu **email gốc** và **tóm tắt AI** vào database.
   - **Cách làm**:
     - Node **StickyNote** > Chọn **Create/Update** > Điền `emailId` và `summary` vào fields.
     - Sau đó, **query** lại log nếu cần tra cứu.

3. **Tự Động Xóa Email Sau Tóm Tắt**:
   - Thêm node **Gmail (Delete)** sau khi gửi báo cáo để **xóa email đã tóm tắt** (giảm bộ nhớ).
   - **Lưu ý**: Chỉ xóa email **trong 24h** (không xóa email quan trọng).

4. **Cập Nhật Thời Gian Chạy**:
   - Nếu muốn chạy **ngày thứ 7**, chỉnh `cron` trong node **Daily 8AM Trigger** thành:
     ```plaintext
     0 1 8 * * 0-6  # Chạy từ thứ 2 đến chủ nhật
     ```

---
### **📌 Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc quét email hàng ngày, thay vào đó chỉ cần **1 email báo cáo tóm tắt** vào 8h sáng. Với **AI tóm tắt bằng LangChain + OpenRouter**, nội dung được phân loại rõ ràng (Updates, Issues, Actions), giúp quyết định nhanh chóng.

**👉 Hành động ngay**:
1. **Cài n8n Self-hosted** trên VPS (để chạy 24/7).
2. **Import workflow** và cấu hình Gmail + OpenRouter.
3. **Test run** và bật tự động hóa!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**💡 Chia sẻ ý kiến**: Các sếp có thể **cải tiến workflow** này thêm nhiều tính năng như gửi báo cáo sang **Notion** hoặc **Google Sheets** để dễ theo dõi. Hãy **like và share** nếu bài viết hữu ích! 🚀