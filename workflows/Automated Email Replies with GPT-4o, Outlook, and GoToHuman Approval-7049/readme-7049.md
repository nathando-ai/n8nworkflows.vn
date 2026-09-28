---
title: "🤖 Trợ lý Email Tự động hóa với GPT-4o + Outlook + Xác nhận GoToHuman - Giảm 80% Thời gian Trả Lời Email"
description: "Workflow tự động hóa trả lời email thông minh bằng GPT-4o, kết hợp với Outlook và hệ thống xác nhận GoToHuman để đảm bảo chất lượng cao, tiết kiệm thời gian và giảm thiểu sai sót cho doanh nghiệp."
slug: "tro-ly-email-tu-dong-hoa-gpt-4o-outlook-goto-human"
tags: [n8n, automation, no-code, ai-chatbot, microsoft-outlook, goto-human, gpt-4o, email-automation]
keywords: [tự động hóa email n8n, trả lời email tự động bằng AI, workflow n8n Outlook, GPT-4o tự động hóa, xác nhận email GoToHuman, tiết kiệm thời gian trả lời email]
---

# 🚀 Trợ lý Email Tự động hóa với GPT-4o, Outlook và Xác nhận GoToHuman

## 📩 **Giải quyết vấn đề gì?**
Các sếp và nhân viên marketing, hỗ trợ khách hàng hay quản lý dự án thường phải mất **giờ đồng hồ** mỗi ngày để trả lời email, đặc biệt là khi phải xử lý lượng lớn tin nhắn hàng ngày. Với **Workflow này**, các sếp sẽ:
- **Tự động hóa 80% quá trình trả lời email** bằng trí tuệ nhân tạo GPT-4o.
- **Xác nhận chất lượng** qua hệ thống GoToHuman trước khi gửi, đảm bảo nội dung chuyên nghiệp và phù hợp với brand.
- **Tiết kiệm thời gian** để tập trung vào công việc chiến lược hơn.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 5-8 giờ/ngày** trả lời email thủ công.
- **Chất lượng cao nhất** với hệ thống xác nhận GoToHuman.
- **Cá nhân hóa phản hồi** nhờ GPT-4o hiểu ngữ cảnh email.
- **Hoạt động liên tục** 24/7, không phụ thuộc vào giờ làm việc.
- **Giảm sai sót** và phản hồi không phù hợp.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản Microsoft Outlook** (đã kết nối OAuth2).
2. **API Key OpenAI** (để sử dụng GPT-4o).
3. **Tài khoản GoToHuman** (để xác nhận nội dung email).
4. **Email cá nhân** (để AI trả lời với tên và brand của các sếp).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/7049](https://n8n.io/workflows/7049) và import vào n8n Editor.
- **Cách 2:** Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/7049) và dán vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
##### **A. Cấu hình Outlook**
- **Node:** `Microsoft Outlook` (search) và `Microsoft Outlook1` (reply).
- **Bước 1:** Tạo **credentials OAuth2** cho Outlook:
  - Đăng nhập tài khoản Outlook vào n8n.
  - Chọn **Microsoft Outlook OAuth2** trong **Credentials**.
- **Bước 2:** Cập nhật **searchQuery** trong Code Node:
  ```javascript
  const today = new Date();
  today.setHours(0, 0, 0, 0);
  return [{ json: { searchQuery: `received:${today.toISOString().split('T')[0]}` } }];
  ```
  - Thay thế `-from:rbreen@ynteractive.com` bằng **email cá nhân** của các sếp.

##### **B. Cấu hình OpenAI (GPT-4o)**
- **Node:** `openai` (lmChatOpenAi).
- **Bước 1:** Tạo **credentials OpenAI** trong n8n:
  - Đăng nhập tài khoản OpenAI và lấy **API Key**.
  - Thêm vào **openAiApi** trong **Credentials**.
- **Bước 2:** Xác nhận **model** là `gpt-4o` (đã mặc định).

##### **C. Cấu hình GoToHuman**
- **Node:** `gotoHuman`.
- **Bước 1:** Tạo **credentials GoToHuman**:
  - Đăng ký tài khoản [GoToHuman](https://gotohuman.com/).
  - Thêm **gotoHumanApi** vào **Credentials**.
- **Bước 2:** Cập nhật **Review Template** trong GoToHuman để phù hợp với schema:
  ```json
  {
    "email": "{{ $json.email }}",
    "OriginalEmail": "{{ $json.body.content }}"
  }
  ```

##### **D. Cấu hình Prompt AI**
- **Node:** `AI Agent: Create caption for linkedin` (agent).
- **Prompt mặc định** đã được tối ưu:
  ```plaintext
  subject: {{ $json.subject }}
  body: {{ $json.body.content }}
  ```
  - AI sẽ trả lời với **tên của các sếp (Robert Breen)** và phong cách chuyên nghiệp.

##### **E. Cấu hình Node IF (Decision)**
- **Node:** `If`.
- **Cấu hình điều kiện:**
  - **Nếu status = "approved"**: Gửi email trả lời.
  - **Nếu status = "rejected"**: Quay lại vòng lặp để sửa đổi.

#### **3. Kích hoạt ⚡️**
- **Bước 1:** Chạy **Test Run** với email mẫu để kiểm tra.
- **Bước 2:** Bật **Active** workflow và chọn **Manual Trigger** để kích hoạt thủ công hoặc sử dụng **Cron Node** để tự động chạy hàng ngày.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm **Node Slack/Telegram** để thông báo khi email đã được xác nhận và gửi đi.
2. **Lưu log hoạt động**:
   - Sử dụng **Node Code** để ghi log vào **Google Sheets** hoặc **Airtable** để theo dõi lịch sử.
3. **Gửi báo cáo định kỳ**:
   - Tạo **Workflow riêng** để tổng hợp số lượng email đã tự động hóa và chất lượng phản hồi.
4. **Cải thiện Prompt AI**:
   - Tùy chỉnh **System Prompt** để phù hợp với **brand voice** của doanh nghiệp (ví dụ: chuyên nghiệp, thân thiện, hoặc kỹ thuật).

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa email mà không mất chất lượng. Với **GPT-4o + Outlook + GoToHuman**, các sếp sẽ:
✅ **Tiết kiệm thời gian** để tập trung vào công việc chiến lược.
✅ **Đảm bảo phản hồi chuyên nghiệp** qua hệ thống xác nhận.
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.

**Hãy áp dụng ngay và trải nghiệm sự khác biệt!** 🚀
---
**Cần hỗ trợ?** Liên hệ với tác giả:
- [LinkedIn](https://www.linkedin.com/in/robert-breen-29429625/)
- Email: **robert@ynteractive.com**