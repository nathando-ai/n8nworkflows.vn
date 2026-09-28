---
title: "🤖 **Tự Động Hóa Phân Loại Email Gmail + AI Tóm Tắt + Thông Báo Slack Urgent (Không Cần Code!)**"
description: "Workflow tự động phân loại, tóm tắt email từ Gmail bằng GPT-4o, gửi thông báo ưu tiên lên Slack và lưu lịch sử vào Google Sheets. Giúp các sếp tiết kiệm 8+ giờ/tuần, giảm thiểu email rác và tập trung vào công việc quan trọng."
slug: "tieu-dong-hoa-phan-loai-email-gmail-ai-slack"
tags: [n8n, automation, gmail, slack, google-sheets, ai-summarization, no-code, workflow-tieu-dong-hoa]
keywords: [n8n workflow email, tự động hóa email gmail, gpt-4o tóm tắt email, phân loại email bằng ai, slack thông báo ưu tiên, google sheets lưu lịch sử email]
---

# 🚀 **Tự Động Hóa Phân Loại Email Gmail + AI Tóm Tắt + Thông Báo Slack Urgent**

---

## **💡 Bạn đã mệt mỏi với hàng trăm email hàng ngày chưa?**
Hàng ngày, các sếp phải mất **30-60 phút** chỉ để:
- Lọc email quan trọng giữa hàng trăm tin nhắn.
- Tóm tắt nội dung dài dòng để đọc sau.
- Phân loại email theo chủ đề (marketing, hỗ trợ khách hàng, báo cáo...).
- Gửi thông báo ưu tiên cho đội nhóm.

**Workflow này giải quyết tất cả!** Nó sẽ:
✅ **Tự động phân loại email** vào các nhãn (AI Agent/To Respond, AI Agent/Awaiting Reply, AI Agent/Notification...).
✅ **Tóm tắt email bằng GPT-4o** để bạn đọc nhanh trong 10 giây.
✅ **Gửi thông báo ưu tiên lên Slack** khi có email cần xử lý ngay.
✅ **Lưu lịch sử vào Google Sheets** để theo dõi và báo cáo định kỳ.

---
### **🎯 Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 8+ giờ/tuần** bằng việc tự động hóa việc phân loại và tóm tắt email.
- **Giảm thiểu email rác** với hệ thống nhãn tự động.
- **Cập nhật tức thời** với thông báo Slack cho email ưu tiên.
- **Báo cáo tự động** với Google Sheets, giúp quản lý dễ dàng hơn.
- **Cá nhân hóa** với AI tóm tắt nội dung chính xác theo ngữ cảnh.
:::

---
### **🔧 Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản và API Key**:
   - **Gmail**: Tài khoản chính để đọc email (cần **OAuth 2.0**).
   - **Slack**: Tài khoản và **API Token** của workspace Slack.
   - **OpenAI**: **API Key** của GPT-4o (đăng ký tại [openai.com](https://openai.com)).
   - **Google Sheets**: Tài khoản Google và **OAuth 2.0** cho Google Drive.

2. **Cấu hình Gmail**:
   - **Tạo các nhãn (labels)** trong Gmail với định dạng:
     ```
     AI Agent/To Respond
     AI Agent/Awaiting Reply
     AI Agent/Notification
     AI Agent/Marketing
     AI Agent/Other
     ```
   - **Cấu hình nhãn này** trong **Settings > Labels** của Gmail.

3. **Google Sheets**:
   - Tạo **một file Google Sheets** với **2 tab**:
     - **Sheet1**: Lưu tất cả email đã xử lý (cột: **From | Summary | Intent | Category | TimeStamp | Urgency**).
     - **Sheet2**: Lưu email mới nhất cho **báo cáo hàng ngày**.
   - **Chia sẻ file** với n8n bằng cách cấp quyền **Đọc/Ghi**.

4. **Slack**:
   - Chọn **channel** muốn nhận thông báo ưu tiên và báo cáo hàng ngày.
   - Cấu hình **Slack App** trong n8n với **OAuth 2.0**.

---
### **🚀 Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/6588](https://n8n.io/workflows/6588) hoặc copy toàn bộ JSON từ trang này.
- Trong **n8n Editor**, chọn **Import** và dán JSON vào.
- **Kích hoạt chế độ "Active"** sau khi import xong.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **16 node**, các sếp cần chú ý cấu hình sau:

##### **🔹 Node "Get many messages" (Gmail)**
- **Credentials**: Chọn `gmailOAuth2` đã cấu hình trước.
- **Operation**: Đảm bảo chọn `getAll` để lấy tất cả email mới.

##### **🔹 Node "Message a model1" (OpenAI)**
- **Credentials**: Chọn `openAiApi` với API Key của GPT-4o.
- **Prompt**: Workflow đã cấu hình sẵn, **không cần chỉnh sửa** (nếu muốn tùy chỉnh, mở node `code` sau này).
- **Model**: Đảm bảo chọn **GPT-4o** (hoặc GPT-4 nếu không có).

##### **🔹 Node "If1" (Phân loại email)**
- **Điều kiện**: Workflow sẽ tự động phân loại email vào nhãn dựa trên **Intent** (xem node `Calculate Intent`).
- **Lưu ý**: Nếu email không phân loại được, nó sẽ được nhắc vào nhãn `AI Agent/Other`.

##### **🔹 Node "Add label to message2 & message3" (Gmail)**
- **Credentials**: Chọn `gmailOAuth2`.
- **Labels**: Đảm bảo nhãn đã tạo trong Gmail (như `AI Agent/To Respond`, `AI Agent/Awaiting Reply`...).

##### **🔹 Node "Send a message2 & message3" (Slack)**
- **Credentials**: Chọn `slackOAuth2Api`.
- **Channel**: Chọn **channel** muốn nhận thông báo.
- **Message Format**: Workflow tự động tạo thông báo với:
  - **Tên người gửi**.
  - **Tóm tắt AI**.
  - **Độ ưu tiên (Urgency)**.

##### **🔹 Node "Append row in sheet1 & sheet2" (Google Sheets)**
- **Credentials**: Chọn `googleSheetsOAuth2Api`.
- **Sheet Name**: Đảm bảo tên sheet chính xác (`Sheet1` và `Sheet2`).
- **Columns**: Workflow sẽ tự động thêm dữ liệu vào các cột đã định nghĩa.

##### **🔹 Node "Calculate Intent" (Code)**
- **Lưu ý**: Node này sử dụng **AI để phân loại email** vào các category như:
  - `Support` (hỗ trợ khách hàng).
  - `Marketing` (quảng cáo).
  - `Follow-up` (theo dõi).
  - `Other` (khác).
- **Nếu muốn tùy chỉnh**, mở node này và chỉnh sửa logic trong **JavaScript**.

##### **🔹 Node "Daily Digest Preparation" (Code)**
- **Lưu ý**: Node này tạo **báo cáo hàng ngày** từ `Sheet2` và gửi lên Slack.
- **Thời gian chạy**: Bằng node `Wait` (cấu hình mặc định là **1 giờ**).

---

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Chọn **Run Once** để kiểm tra workflow với email mẫu.
   - Kiểm tra:
     - Email có được phân loại không?
     - Slack có nhận thông báo không?
     - Google Sheets có cập nhật dữ liệu không?

2. **Bật Active**:
   - Sau khi test thành công, **bật chế độ Active**.
   - Workflow sẽ chạy **tự động** theo lịch (mặc định **1 giờ/lần**).

---
### **✍️ Mẹo & gợi ý nâng cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Tùy chỉnh Prompt cho GPT-4o**:
   - Mở node `Message a model1` và chỉnh sửa **Prompt** để AI tóm tắt chi tiết hơn hoặc ngắn gọn hơn.

2. **Thêm thông báo Telegram**:
   - Sử dụng **node Telegram Bot** để gửi thông báo ưu tiên lên Telegram cùng Slack.

3. **Lưu log chi tiết**:
   - Thêm **node Log** để ghi lại lỗi hoặc email bị bỏ qua.

4. **Báo cáo định kỳ**:
   - Sử dụng **node Schedule Trigger** để chạy báo cáo hàng tuần/tháng thay vì hàng ngày.

5. **Phân loại email theo người gửi**:
   - Sử dụng **node Code** để thêm logic phân loại email theo domain (ví dụ: `@gmail.com` → `Personal`, `@company.com` → `Work`).

6. **Kết hợp với Notion/Zapier**:
   - Thay vì Google Sheets, có thể lưu dữ liệu vào **Notion** hoặc **Airtable** cho giao diện thân thiện hơn.

---
### **📌 Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn:
✔ **Tự động hóa email** mà không cần viết code.
✔ **Tiết kiệm thời gian** với AI tóm tắt và phân loại.
✔ **Cập nhật tức thời** với thông báo Slack.
✔ **Theo dõi lịch sử** với Google Sheets.

**Hãy import ngay và bắt đầu tự động hóa inbox của mình!** 🚀
Nếu có vấn đề, hãy **comment bên dưới** hoặc liên hệ với tác giả [Siddhant](https://n8n.io/workflows/6588) để hỗ trợ.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**Bắt đầu tự động hóa ngay hôm nay!** 💻✨