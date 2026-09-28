---
title: "🤖 Tự Động Tạo Vấn Đề Linear từ Email Hỗ Trợ Gmail - AI Triaging Tickets"
description: "Workflow tự động hóa 100% không code chuyển đổi email hỗ trợ Gmail thành vấn đề Linear với AI phân loại, gán nhãn và đánh giá độ ưu tiên tự động. Giúp đội ngũ hỗ trợ tiết kiệm 80% thời gian triaging và tập trung vào giải quyết vấn đề thực sự."
slug: "tieu-dong-tao-van-de-linear-tu-email-gmail"
tags: [n8n, automation, ai-powered, linear, gmail, support, no-code, ai-triaging]
keywords: [n8n workflow tự động hóa, tạo vấn đề Linear từ email, AI phân loại ticket, tự động hóa hỗ trợ khách hàng, triaging ticket bằng AI, n8n self-hosted]
---

# 🚀 **Tự Động Tạo Vấn Đề Linear từ Email Hỗ Trợ Gmail với AI Triaging**

### **Giải pháp cho các sếp:**
Hiện nay, đội ngũ hỗ trợ của các sếp thường phải mất **gần 30-40% thời gian** để đọc, phân loại và gán nhãn cho các yêu cầu từ khách hàng. Với **Workflow này**, các sếp sẽ tự động hóa toàn bộ quy trình triaging ticket bằng AI, chuyển đổi email hỗ trợ thành vấn đề trong Linear với:
✅ **Nhãn tự động** (Priority, Type, Status)
✅ **Tiêu đề và mô tả tổng hợp** từ nội dung email
✅ **Không cần code** – chỉ cần cấu hình API và cài đặt n8n
✅ **Hoạt động 24/7** – không phụ thuộc vào giờ làm việc

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo bảo mật và tính liên tục.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian triaging**: AI tự động phân loại và gán nhãn cho ticket.
- **Chính xác cao**: AI hiểu ngữ cảnh và tổng hợp thông tin từ email thành vấn đề Linear chi tiết.
- **Cá nhân hóa và ưu tiên**: Mỗi ticket được đánh giá độ ưu tiên và nhãn phù hợp.
- **Hoạt động liên tục**: Workflow chạy tự động theo lịch trình, không phụ thuộc vào nhân viên.
- **Kết nối Gmail + Linear**: Tích hợp hoàn chỉnh giữa hệ thống email và công cụ quản lý dự án.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Gmail** (đặc biệt là inbox dành riêng cho hỗ trợ, ví dụ: `support@domain.com`).
2. **API Key OpenAI** (để sử dụng mô hình AI GPT-4o-mini).
3. **Tài khoản Linear** và **API Key Linear** (để tạo vấn đề tự động).
4. **n8n Self-hosted** (cài đặt trên VPS hoặc máy chủ riêng).
5. **Dữ liệu mẫu** (nếu muốn test trước khi chạy thực tế).
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Bước 1:** Tải workflow từ [n8n.io/workflows/3899](https://n8n.io/workflows/3899) hoặc sao chép JSON từ trang này.
- **Bước 2:** Mở **n8n Editor** và chọn **Import Workflow** → Dán JSON hoặc tải file JSON.
- **Bước 3:** Chọn **Active** để kích hoạt workflow.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **8 node** chính, các sếp cần chú ý cấu hình sau:

##### **A. Cấu hình Gmail (Node: "Get Recent Messages")**
- **Credentials:** Chọn `gmailOAuth2` (cần tạo OAuth 2.0 cho Gmail).
- **Filter:** Đặt `to:support@example.com` (thay bằng email hỗ trợ của doanh nghiệp).
- **Operation:** Chọn `getAll` để lấy tất cả tin nhắn mới.

##### **B. Cấu hình AI Triaging (Nodes: "OpenAI Chat Model" + "Structured Output Parser")**
- **Credentials:** Chọn `openAiApi` (điền API Key OpenAI).
- **Model:** Chọn `gpt-4o-mini` (mô hình miễn phí và hiệu quả).
- **System Prompt (gợi ý):**
  ```plaintext
  You are an AI assistant for triaging support tickets. For each email, extract:
  1. Title (summary of the issue)
  2. Priority (high/medium/low)
  3. Labels (e.g., "bug", "feature request", "question")
  4. Description (formatted in Markdown)
  ```
- **Output Parser:** Chọn `outputParserStructured` để AI trả về định dạng JSON.

##### **C. Cấu hình Linear (Node: "Create Issue in Linear.App")**
- **Credentials:** Chọn `linearApi` (điền API Key Linear).
- **Fields cần điền:**
  - `title`: Từ kết quả AI (Title).
  - `description`: Từ kết quả AI (Description).
  - `priority`: Từ kết quả AI (Priority).
  - `labels`: Từ kết quả AI (Labels).

##### **D. Các node khác cần chú ý:**
- **"Mark as Seen" (removeDuplicates):** Đảm bảo mỗi email chỉ được xử lý **1 lần**.
- **"Markdown" (node chuyển đổi HTML → Markdown):** Để AI dễ đọc nội dung email.
- **"Schedule Trigger" (node chạy định kỳ):** Cần cấu hình thời gian chạy (ví dụ: **mỗi 15 phút**).

#### **3. Kích hoạt ⚡️**
- **Bước 1:** Test run với **dữ liệu mẫu** (ví dụ: 1 email hỗ trợ).
- **Bước 2:** Kiểm tra kết quả trên **Linear** và **Gmail**.
- **Bước 3:** Bật **Active** và chạy theo lịch trình.

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Kết nối với Slack/Telegram:**
   - Thêm node **Slack** hoặc **Telegram Bot** để thông báo khi có ticket mới.
   - Ví dụ: `New ticket created in Linear: [Title] (Priority: High)`

2. **Lưu log hoạt động:**
   - Thêm node **Google Sheets** hoặc **Notion** để ghi lại lịch sử triaging.

3. **Tự động gán người xử lý:**
   - Sử dụng node **Linear Assign** để gán ticket cho nhân viên phù hợp.

4. **Phân loại email tự động:**
   - Nếu inbox không chỉ hỗ trợ, thêm node **IF** để lọc email theo từ khóa (ví dụ: "hỗ trợ" → xử lý, "báo giá" → bỏ qua).

5. **Cập nhật trạng thái tự động:**
   - Thêm node **Linear Update** để tự động cập nhật trạng thái khi AI phân loại.
:::

---

### 📌 **Kết luận**
Workflow này **giải phóng đội ngũ hỗ trợ** khỏi công việc triaging lặp đi lặp lại, giúp họ tập trung vào **giải quyết vấn đề thực sự** của khách hàng. Với **AI triaging**, các sếp sẽ:
✔ **Tiết kiệm thời gian** (từ 30-40% cho mỗi ngày).
✔ **Tăng độ chính xác** (AI hiểu ngữ cảnh hơn con người).
✔ **Cải thiện trải nghiệm khách hàng** (ticket được xử lý nhanh chóng).

**Hành động ngay!**
1. **Cài đặt n8n Self-hosted** trên VPS (sử dụng mã giảm giá **VPSN8N**).
2. **Import workflow** và cấu hình API.
3. **Test run** với email mẫu.
4. **Bật Active** và bắt đầu tự động hóa!

---
**Cần hỗ trợ thêm?**
- **Join Discord n8n:** [https://discord.com/invite/XPKeKXeB7d](https://discord.com/invite/XPKeKXeB7d)
- **Forum n8n:** [https://community.n8n.io/](https://community.n8n.io/)
- **Liên hệ tác giả:** [hello@jimle.uk](mailto:hello@jimle.uk)

🚀 **Happy Automating!** 🚀