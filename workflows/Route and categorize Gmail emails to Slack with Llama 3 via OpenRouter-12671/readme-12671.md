---
title: "🤖 Tự Động Hóa Email Gmail → Slack Với AI Llama 3: Phân Loại & Chuyển Đạo Tự Động (Không Cần Code)"
description: "Workflow tự động hóa chuyển email Gmail sang Slack với phân loại thông minh bằng AI Llama 3 (OpenRouter), tạo/đăng ký kênh Slack tự động, tiết kiệm 10+ giờ/ngày cho bộ phận Admin, Customer Support và Sales. Hoạt động 24/7 mà không cần can thiệp thủ công."
slug: "tieu-dong-hoa-email-gmail-slack-ai-llama-3"
tags: [n8n, automation, ai-workflow, gmail, slack, llama-3, openrouter, ticket-management, ai-summarization]
keywords: [n8n workflow gmail slack, tự động hóa email, phân loại email bằng AI, Llama 3 OpenRouter, tự động tạo kênh Slack, tự động hóa customer support]
---

# 🚀 **Tự Động Hóa Email Gmail → Slack Với AI Llama 3: Phân Loại & Chuyển Đạo Tự Động**

### **Giải pháp cho các sếp:**
- **Bộ phận Admin:** Tiết kiệm 5-10 giờ/ngày chuyển email giữa Gmail và Slack.
- **Customer Support:** Phân loại tự động email (Support, HR, Finance...) vào kênh Slack riêng biệt.
- **Sales/Marketing:** Theo dõi email quan trọng từ khách hàng trong kênh Slack chuyên dụng.
- **Quản lý dự án:** Tự động tạo kênh Slack mới khi có chủ đề mới xuất hiện.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo bảo mật và tính liên tục.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian:** Tự động chuyển email từ Gmail sang Slack **không cần can thiệp thủ công**.
- **Phân loại thông minh:** AI Llama 3 phân loại email vào **kênh Slack phù hợp** (Sales, Support, HR, Finance...).
- **Tạo kênh tự động:** Nếu chủ đề mới xuất hiện, hệ thống **tự động tạo kênh Slack mới** và đăng ký.
- **Báo cáo 24/7:** Email được chuyển và lưu trữ trong Slack với **Block Kit** (hỗ trợ tương tác qua nút trả lời).
- **Không bị trùng lặp:** Hệ thống **kiểm tra và loại bỏ email đã xử lý** để tránh trùng lặp.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Gmail:**
   - Đăng ký **OAuth 2.0** cho Gmail (n8n sẽ lấy email mới và metadata).
   - **Không** bao gồm spam và draft trong quá trình lấy dữ liệu.

2. **API Key OpenRouter:**
   - Tạo tài khoản trên [OpenRouter](https://openrouter.ai/) và lấy **API Key**.
   - Chọn mô hình **`meta-llama/llama-3-70b-instruct`** (đã cấu hình sẵn trong workflow).

3. **Slack App:**
   - Tạo **Slack App** với các quyền:
     - `channels:read`, `channels:write`, `chat:write`, `users:read`.
   - Lấy **Bot Token OAuth** và thêm vào n8n dưới **credentials `slackApi`**.

4. **Danh sách danh mục email (optional):**
   - Nếu muốn AI phân loại email theo danh sách cụ thể (ví dụ: Sales, Support, HR), các sếp có thể **cập nhật prompt** trong node `Find Category`.

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/12671](https://n8n.io/workflows/12671) và import vào n8n Editor.
- **Cách 2:** Copy toàn bộ JSON từ link trên và **paste** vào **Import Workflow** trong n8n.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow có **18 node**, nhưng các sếp cần chú ý đến **các node quan trọng sau**:

#### **A. Node Gmail Trigger (`Capture Gmail Event`)**
- **Cấu hình:**
  - Chọn **credentials `gmailOAuth2`** (đã đăng ký trước).
  - **Lọc email:** Chỉ lấy email **unread** và **không phải spam/draft**.
  - **Thời gian refresh:** Cấu hình **lấy email mỗi 1 phút** (đã mặc định).

#### **B. Node AI Phân Loại (`Find Category`)**
- **Cấu hình:**
  - Sử dụng **credentials `openRouterApi`** (API Key OpenRouter).
  - **Prompt mặc định** đã tối ưu hóa để phân loại email vào danh mục:
    - Sales, Support, HR, Finance, Admin, Marketing, Logistics...
  - **Nếu muốn thay đổi danh mục:** Sửa node `StickyNote` (gắn liền với node `Find Category`) để cập nhật danh sách.

#### **C. Node Slack (`Create Slack Channel`, `Join Slack Channel`, `Post Message in Channel`)**
- **Cấu hình chung:**
  - Sử dụng **credentials `slackApi`** (Bot Token OAuth).
  - **Kiểm tra kênh tồn tại:** Node `Check Channel Exist` sẽ **kiểm tra danh sách kênh Slack** trước khi tạo mới.
  - **Trường hợp kênh không tồn tại:** Node `Create Slack Channel` sẽ **tự động tạo kênh mới** và **đăng ký người dùng** vào kênh.

#### **D. Node Block Kit (Trang trí tin nhắn Slack)**
- **Cấu hình:**
  - Tin nhắn Slack sẽ có **cấu trúc Block Kit** với:
    - Tiêu đề: Tiêu đề email.
    - Nội dung: Nội dung email.
    - **Nút trả lời:** Bao gồm **thread ID** của email (sẵn sàng cho workflow tương tác sau này).

#### **E. Node Loại bỏ trùng lặp (`Filter + Deduplicate Validation`)**
- **Cấu hình:**
  - Node **Code** này sẽ **kiểm tra và loại bỏ email đã xử lý** trước khi chuyển tiếp.
  - **Lưu ý:** Nếu email đã được chuyển trước, nó sẽ **bị bỏ qua** để tránh trùng lặp.

---

### **3. Kích hoạt ⚡️**
1. **Test Run:**
   - Gửi **email mẫu** (ví dụ: email Sales, Support) từ Gmail.
   - Kiểm tra:
     - Email có được chuyển sang Slack không?
     - Kênh Slack có được tạo/tạo sẵn không?
     - Tin nhắn Slack có cấu trúc Block Kit không?

2. **Bật Active:**
   - Sau khi test thành công, **bật workflow** và **đặt lịch chạy tự động** (mặc định là mỗi 1 phút).

---

## ✍️ **Mẹo & gợi ý nâng cao**
1. **Tích hợp với Google Sheets (Log Email):**
   - Thêm node **Google Sheets** sau node `Post Message in Channel` để **lưu log email** vào bảng tính.
   - **Cách làm:**
     - Thêm node `n8n-nodes-base.googleSheets`.
     - Cấu hình **credentials `googleSheetsOAuth2`** và **Sheet Name**.
     - Lưu các trường: `Email ID`, `Subject`, `Category`, `Slack Channel`.

2. **Tự động gửi báo cáo hàng ngày:**
   - Sử dụng **n8n Cron Trigger** để chạy workflow **mỗi ngày 8h sáng**, gửi **tóm tắt email mới** qua Slack/Email.

3. **Tích hợp với Notion/ClickUp:**
   - Sau khi email được chuyển sang Slack, **tự động tạo task** trong Notion/ClickUp bằng node `n8n-nodes-base.notion` hoặc `n8n-nodes-base.clickup`.

4. **Cập nhật danh mục AI:**
   - Nếu có **danh mục mới** (ví dụ: "Legal"), cập nhật **prompt** trong node `Find Category` bằng cách chỉnh sửa **StickyNote** gắn liền.

5. **Tự động phản hồi email:**
   - Sử dụng **n8n Webhook** để **nhận tin nhắn từ Slack** (qua nút trả lời) và **tự động trả lời email** bằng node `n8n-nodes-base.email`.

---

## 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc **chuyển email thủ công** giữa Gmail và Slack, đồng thời **phân loại tự động** email vào kênh Slack phù hợp. Với **AI Llama 3**, hệ thống **hiểu ngữ cảnh** và **tạo kênh mới** khi cần thiết, giúp **tối ưu hóa quản lý thông tin** cho doanh nghiệp.

**🚀 Hãy áp dụng ngay và tiết kiệm 10+ giờ/ngày cho đội ngũ!**
Nếu có vấn đề, các sếp có thể **liên hệ với Intuz** (tác giả workflow) qua [website](https://intuz.com/) để hỗ trợ tối ưu hóa thêm.

---
**#TựĐộngHóa #n8n #AIWorkflows #SlackAutomation #GmailAutomation**