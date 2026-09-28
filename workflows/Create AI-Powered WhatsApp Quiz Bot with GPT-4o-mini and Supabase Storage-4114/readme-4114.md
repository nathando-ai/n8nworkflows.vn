---
title: "🤖 Tự Động Hóa Bot Trắc Nghiệm WhatsApp Cực Hiệu Quả Với GPT-4o-mini & Supabase - Không Cần Code!"
description: "Xây dựng bot trắc nghiệm thông minh trên WhatsApp, tự động lấy thông tin người dùng từ Supabase, tạo câu hỏi AI và gửi kết quả - hoàn toàn tự động hóa, tiết kiệm thời gian lên đến 90% cho các sếp quản lý học tập hoặc khảo sát."
slug: "tự-dộng-hoa-bot-trắc-nghiệm-whatsapp-gpt-4o-mini-supabase"
tags: [n8n, automation, ai, whatsapp, supabase, gpt-4o-mini, no-code]
keywords: [bot trắc nghiệm whatsapp tự động, n8n workflow ai, tự động hóa học tập, gpt-4o-mini n8n, supabase integration, chatbot học tập]
---

# 🚀 **Bot Trắc Nghiệm WhatsApp Cực Hiệu Quả Với AI GPT-4o-mini & Supabase**

## **Giải Pháp Cho Nỗi Đau Của Các Sếp**
Các sếp đang gặp khó khăn khi phải:
❌ **Tạo và quản lý trắc nghiệm thủ công** trên WhatsApp, mất thời gian và dễ sai sót.
❌ **Không theo dõi được thông tin người dùng** (tên, chủ đề học tập) một cách hệ thống.
❌ **Cần phải tự viết code** để kết nối WhatsApp với cơ sở dữ liệu và AI, không phải ai cũng có kỹ năng.

**Workflow này giúp:**
✅ **Tự động lấy thông tin người dùng** (tên, chủ đề học tập) từ Supabase khi họ gửi tin nhắn.
✅ **Hỏi lại thông tin thiếu** nếu người dùng chưa điền đầy đủ.
✅ **Tạo trắc nghiệm AI** với GPT-4o-mini, phù hợp với chủ đề người dùng chọn.
✅ **Gửi câu hỏi trắc nghiệm** ngay lập tức qua WhatsApp, **không cần can thiệp thủ công**.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **ổn định 24/7**, các sếp nên **self-host n8n** trên VPS riêng:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đảm bảo tốc độ nhanh cho AI)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian lên đến 90%** so với cách làm thủ công.
- **Tự động hóa trắc nghiệm** cho học sinh, nhân viên hoặc khách hàng.
- **Cá nhân hóa câu hỏi** dựa trên chủ đề học tập của người dùng.
- **Hoạt động liên tục** 24/7, không cần can thiệp người dùng.
- **Dữ liệu người dùng được lưu trữ an toàn** trên Supabase.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản WhatsApp Business API** (hoặc sử dụng **Twilio SendGrid** nếu muốn kết nối khác).
✔ **Tài khoản OpenAI** với **API Key** để sử dụng GPT-4o-mini.
✔ **Tài khoản Supabase** (miễn phí hoặc paid) với:
   - **URL Database** và **Anonymized Public Key**.
   - **Table "users"** (cần có cột: `id`, `name`, `study_topic`).
✔ **Credentials trong n8n**:
   - `openAiApi` (điền API Key OpenAI).
   - `supabaseApi` (điền URL và Public Key Supabase).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/4114](https://n8n.io/workflows/4114) và import vào **n8n Editor**.
- **Cách 2:** Copy toàn bộ JSON và paste vào **Create Workflow** → **Import Workflow**.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **13 node**, các sếp cần chú ý cấu hình sau:

##### **🔹 Node "WhatsApp Trigger" (Webhook)**
- **Path:** Được tự động sinh ra khi import (ví dụ: `aae5d69a-d682-4d9d-9710-a3807ca73b9c`).
- **HTTP Method:** `POST`.
- **Lưu ý:**
  - Cần **kết nối với WhatsApp Business API** (hoặc Twilio) để nhận tin nhắn.
  - **Test Webhook** bằng cách gửi tin nhắn từ số điện thoại liên kết.

##### **🔹 Node "Supabase: Fetch User Data" & "Supabase: Update User Name/Topic"**
- **Credentials:** Chọn `supabaseApi` đã cấu hình trước.
- **Table:** Đảm bảo table `users` có cột `id`, `name`, `study_topic`.
- **Query:**
  - **Fetch:** `SELECT * FROM users WHERE id = $id` (điền `$id` từ WhatsApp).
  - **Update:** `UPDATE users SET name = $name WHERE id = $id` (điền `$name` từ người dùng).

##### **🔹 Node "OpenAI Chat Model" (GPT-4o-mini)**
- **Model:** Đã mặc định là `gpt-4o-mini`.
- **Prompt Template:**
  ```plaintext
  You are a quiz generator. Create 5 multiple-choice questions about "{study_topic}" for a user named "{name}".
  Format: [Question] - A. [Option 1] | B. [Option 2] | C. [Option 3] | D. [Option 4]
  ```
- **Lưu ý:**
  - Đảm bảo **API Key OpenAI** được điền chính xác.
  - **Test prompt** trước khi chạy workflow toàn bộ.

##### **🔹 Node "AI Agent - Portuguese BR System Msg"**
- **Role:** Tự động xử lý logic (ví dụ: hỏi lại nếu người dùng chưa điền tên/topic).
- **Lưu ý:**
  - Nếu muốn **hỗ trợ tiếng Việt**, cần **cập nhật prompt** trong node này:
    ```plaintext
    If user hasn't provided name, ask: "Hello! What's your name?"
    If user hasn't provided study topic, ask: "What topic would you like to study today?"
    ```

##### **🔹 Node "Send Message to User (WhatsApp Message)"**
- **URL:** Điền **Webhook URL của WhatsApp Business API** (hoặc Twilio).
- **Payload Example:**
  ```json
  {
    "text": "Question 1: [Câu hỏi] - A. [Đáp án 1] | B. [Đáp án 2]",
    "to": "Số điện thoại người dùng"
  }
  ```

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Gửi tin nhắn từ WhatsApp với nội dung đơn giản (ví dụ: `Hello`).
   - Kiểm tra **log** trong n8n để đảm bảo workflow chạy đúng.
2. **Bật Active** workflow.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết nối với Slack/Telegram**
   - Sử dụng node **Slack** hoặc **Telegram Bot** để **báo cáo lỗi** hoặc **log hoạt động**.
2. **Lưu lịch sử câu hỏi**
   - Tạo **table mới** trong Supabase để lưu câu hỏi đã gửi cho người dùng.
3. **Cập nhật chủ đề học tập tự động**
   - Nếu người dùng chọn chủ đề mới, **cập nhật Supabase** và **tạo trắc nghiệm mới** ngay lập tức.
4. **Thêm tính năng điểm số**
   - Sử dụng **LangChain** để **chấm điểm tự động** và gửi kết quả.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc tạo trắc nghiệm thủ công, đồng thời **cải thiện trải nghiệm học tập** cho người dùng với **câu hỏi AI cá nhân hóa**. **Chỉ cần import, cấu hình và bật hoạt động** - **không cần code!**

**🚀 Hãy áp dụng ngay và tự động hóa trắc nghiệm WhatsApp của mình!**
Nếu có vấn đề, **hãy comment bên dưới** hoặc liên hệ với **n8n Community** để hỗ trợ.

---
**🔗 [Xem workflow gốc](https://n8n.io/workflows/4114) | 📌 [Cài đặt n8n Self-Hosted](https://docs.n8n.io/)**