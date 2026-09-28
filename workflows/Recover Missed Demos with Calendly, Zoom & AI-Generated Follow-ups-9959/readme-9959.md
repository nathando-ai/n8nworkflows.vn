---
title: "🚀 Tự Động Hóa Khôi Phục Cuộc Demo Bị Trễ Hẹn Với Calendly, Zoom & AI - Không Cần Code"
description: "Workflow này tự động theo dõi cuộc demo đã đặt lịch trên Calendly, kiểm tra sự tham dự trên Zoom, và tự động gửi tin nhắn khôi phục AI cá nhân hóa cho khách hàng không tham dự. Giúp doanh nghiệp tiết kiệm thời gian, tăng tỷ lệ chuyển đổi và cải thiện trải nghiệm khách hàng."
slug: "tieu-dong-hoa-khoi-phuc-cuoc-demo-bi-tre-han"
tags: [n8n, automation, lead-nurturing, ai-chatbot, crm-automation, zoom, calendly, openai]
keywords: [tự động hóa doanh nghiệp, khôi phục cuộc demo trễ hẹn, n8n workflow, zoom api, calendly automation, ai chatbot, tự động hóa lead nurturing]
---

# 🚀 **Tự Động Hóa Khôi Phục Cuộc Demo Bị Trễ Hẹn Với Calendly, Zoom & AI**

## **💡 Giới Thiệu: Nỗi Đau Của Doanh Nghiệp Và Giải Pháp Tự Động Hóa**
Các sếp đã từng gặp phải tình huống này chưa? Một khách hàng đã đặt lịch demo nhưng **không tham dự**, khiến thời gian và cơ hội bán hàng bị lãng phí. Thậm chí, việc theo dõi và khôi phục lại khách hàng này thường phải làm thủ công, tốn thời gian và dễ bị bỏ quên.

**Workflow này giải quyết vấn đề đó bằng cách:**
✅ **Tự động theo dõi tất cả cuộc demo** được đặt lịch trên Calendly.
✅ **Kiểm tra sự tham dự** trên Zoom và phân biệt giữa khách hàng tham dự và không tham dự.
✅ **Sử dụng AI (OpenAI) tạo tin nhắn khôi phục cá nhân hóa** để liên lạc lại với khách hàng không tham dự.
✅ **Gửi thông báo ngay lập tức** cho đội ngũ qua Slack và (tùy chọn) gửi email khôi phục.
✅ **Cập nhật CRM (HubSpot)** để theo dõi hoạt động của khách hàng.

Kết quả? **Tiết kiệm thời gian, tăng tỷ lệ chuyển đổi và cải thiện trải nghiệm khách hàng một cách hoàn toàn tự động!**

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để tránh giới hạn của phiên bản miễn phí.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần theo dõi thủ công mỗi cuộc demo.
- **Tăng tỷ lệ chuyển đổi**: Khôi phục khách hàng không tham dự một cách tự động và cá nhân hóa.
- **Cải thiện trải nghiệm khách hàng**: Tin nhắn AI được tối ưu hóa, không giống như email thông thường.
- **Hoạt động liên tục**: Workflow chạy 24/7, không phụ thuộc vào nhân viên.
- **Tích hợp CRM**: Cập nhật trạng thái khách hàng trên HubSpot (tùy chọn).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản Calendly** (API Token).
✔ **Tài khoản Zoom** (OAuth Server-to-Server credentials).
✔ **Tài khoản OpenAI** (API Key cho AI tạo tin nhắn).
✔ **Tài khoản Slack** (tùy chọn, để thông báo đội ngũ).
✔ **Tài khoản Email** (tùy chọn, để gửi email khôi phục).
✔ **Tài khoản HubSpot** (tùy chọn, để cập nhật CRM).
✔ **Bảng dữ liệu (Data Table) trong n8n** với các cột:
   - `meeting_id` (string/number)
   - `email` (string)
   - `status` (string: 'pending', 'attended', 'no_show')
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể **import workflow từ file JSON** hoặc **copy/paste JSON vào n8n Editor**:
1. Tải file JSON từ [n8n.io/workflows/9959](https://n8n.io/workflows/9959).
2. Mở **n8n Editor** → Nhấn **Import** → Chọn file JSON.
3. Hoặc copy toàn bộ JSON và dán vào **Import Workflow** trong Editor.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **2 đường dẫn chính**:
- **Đường dẫn Booking (đặt lịch)**: Theo dõi khi khách hàng đặt lịch demo.
- **Đường dẫn Attendance (sự tham dự)**: Kiểm tra xem khách hàng có tham dự không.

##### **🔹 Cấu Hình Calendly Webhook (One-Time Setup)**
1. **Node: "Manual Setup Trigger"** → Nhấn **Execute Workflow** để tạo webhook Calendly.
2. **Node: "Get Calendly Organization"** → Điền **API Token Calendly** vào `Authorization` header.
3. **Node: "Create Calendly Webhook"** → Điền **URI webhook** từ n8n (thường là `https://<your-n8n-instance>/webhook/cal-uri-get`).

##### **🔹 Cấu Hình Zoom Webhook (Critical!)**
1. **Node: "Zoom Webhook Validator"** → Điền **Zoom Webhook Secret** vào `code` node.
   - **Lấy Zoom Webhook Secret**:
     - Mở **Zoom Dashboard** → **Developer** → **Webhooks**.
     - Tạo một **new webhook** với endpoint là `https://<your-n8n-instance>/webhook/zoom-meeting-ended`.
     - Copy **Secret** và dán vào node `Zoom Webhook Validator`.
2. **Node: "Get Zoom Access Token"** → Điền **Zoom OAuth Credentials**:
   - **Account ID**, **Client ID**, **Client Secret** (từ **Zoom Marketplace**).
   - **Scopes**: `meeting:read:past_meeting:admin`.
3. **Node: "Update Attendance Status"** → Đảm bảo `meeting_id` trong Zoom và Calendly **khớp nhau**.

##### **🔹 Cấu Hình AI (OpenAI)**
1. **Node: "AI Generate Follow-Up Messages"** → Điền **OpenAI API Key**.
2. **Prompt AI** (có thể chỉnh sửa để phù hợp với brand):
   ```json
   {
     "role": "system",
     "content": "You are a professional sales assistant. Generate a personalized follow-up email for a missed demo. Include key points from the meeting and a clear call-to-action."
   }
   ```

##### **🔹 Cấu Hình Slack & Email (Tùy Chọn)**
1. **Node: "Notify Team in Slack"** → Điền **Token Slack** và **Channel**.
2. **Node: "Send Recovery Email"** → Điền **Tài khoản SMTP** (Gmail, SendGrid, etc.).

##### **🔹 Cấu Hình HubSpot (Tùy Chọn)**
1. **Node: "Update CRM Deal"** → Điền **API Key HubSpot** và **Domain**.

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Tạo một **cuộc demo giả** trên Calendly.
   - Kiểm tra xem workflow có **cập nhật trạng thái** và **gửi tin nhắn** không.
2. **Bật Active workflow** khi đã kiểm tra xong.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tích Hợp Telegram/Email Khác**:
   - Thay thế Slack bằng **Telegram Bot** hoặc **Email khác** để thông báo.
2. **Lưu Log Hoạt Động**:
   - Sử dụng **n8n-nodes-base.log** để ghi lại tất cả hoạt động của workflow.
3. **Gửi Báo Cáo Định Kỳ**:
   - Tạo một **workflow mới** để tổng hợp dữ liệu no-show và gửi báo cáo hàng tuần.
4. **Tối Ưu AI**:
   - Chỉnh sửa **prompt AI** để phù hợp với **tone của brand** (ví dụ: chuyên nghiệp, thân thiện, hài hước).
5. **Tự Động Cập Nhật CRM**:
   - Nếu khách hàng **khôi phục lại**, tự động cập nhật trạng thái trong HubSpot.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp và đội ngũ marketing/sales, đồng thời **tăng tỷ lệ chuyển đổi** bằng cách tự động khôi phục khách hàng không tham dự. **Không cần code**, chỉ cần cấu hình đúng các bước trên, workflow sẽ hoạt động **một cách hoàn toàn tự động**.

**Hãy áp dụng ngay và xem kết quả!** 🚀
Nếu có vấn đề, các sếp có thể **comment dưới bài viết** hoặc liên hệ với cộng đồng n8n để hỗ trợ.

---
**🔗 [Tải workflow gốc từ n8n.io](https://n8n.io/workflows/9959)**
**📌 [Hướng dẫn chi tiết Zoom OAuth](https://marketplace.zoom.us/docs/api-reference/zoom-api/oauth)**
**💡 [Cách lấy API Token Calendly](https://calendly.com/developers/api)**