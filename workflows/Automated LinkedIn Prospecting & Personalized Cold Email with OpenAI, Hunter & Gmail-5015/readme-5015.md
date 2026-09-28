---
title: "🚀 Tự Động Hóa Tìm Kiếm LinkedIn & Gửi Email Lạnh Cá Nhân Hóa với OpenAI, Hunter & Gmail (N8N)"
description: "Workflow tự động hóa tìm kiếm liên hệ LinkedIn thông minh, tra cứu email, và gửi email lạnh cá nhân hóa bằng AI (OpenAI) để tăng tỷ lệ phản hồi cho doanh nghiệp. Giúp các sếp tiết kiệm 10+ giờ/ngày trong công việc outreach."
slug: "tu-dong-hoa-tim-kiem-linkedin-va-email-lanh-canh-nhan-hoa"
tags: [n8n, automation, sales, ai, openai, hunter.io, gmail, no-code]
keywords: [n8n workflow tự động hóa, tìm kiếm LinkedIn tự động, email lạnh cá nhân hóa, AI OpenAI cho doanh nghiệp, tự động hóa outreach, Hunter.io API, Google Sheets]
---

# 🚀 **Tự Động Hóa Tìm Kiếm LinkedIn & Gửi Email Lạnh Cá Nhân Hóa với AI (N8N)**

## **💡 Giải Pháp Cho Nỗi Đau Của Các Sếp**
Bạn đã từng phải:
- **Tìm kiếm thủ công** hàng trăm liên hệ LinkedIn để outreach?
- **Gửi email lạnh** với nội dung chung chung, tỷ lệ phản hồi chỉ ~1-2%?
- **Tra cứu email** của khách hàng tốn thời gian và không chính xác?

Workflow này **tự động hóa toàn bộ quy trình** từ tìm kiếm liên hệ LinkedIn đến gửi email lạnh **cá nhân hóa** bằng AI, giúp bạn:
✅ **Tiết kiệm 10+ giờ/ngày** trong công việc outreach.
✅ **Tăng tỷ lệ phản hồi lên 10-20%** nhờ nội dung email được AI tối ưu.
✅ **Lưu trữ dữ liệu liên hệ** trên Google Sheets để theo dõi và phân tích.
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để tránh giới hạn của phiên bản cloud.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
| **Lợi Ích** | **Chi Tiết** |
|-------------|-------------|
| **Tiết kiệm thời gian** | Tự động tìm kiếm và tra cứu email cho 50+ liên hệ/ngày. |
| **Nội dung email cá nhân hóa** | AI (OpenAI) tự động viết email dựa trên thông tin LinkedIn của khách hàng. |
| **Tỷ lệ phản hồi cao** | Email được tối ưu bằng AI, tăng cơ hội được mở và trả lời. |
| **Dữ liệu liên hệ sẵn sàng** | Tất cả thông tin được lưu trên Google Sheets, dễ dàng theo dõi. |
| **Hoạt động liên tục** | Workflow chạy tự động, không cần can thiệp thủ công. |

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản Google** (để sử dụng Google Sheets và Gmail).
✔ **API Key OpenAI** (truy cập [OpenAI Platform](https://platform.openai.com/settings/organization/api-keys)).
✔ **API Key Hunter.io** (đăng ký tại [Hunter.io](https://hunter.io/)).
✔ **Cookie Google Search** (sử dụng [Cookie-Editor](https://chromewebstore.google.com/detail/cookie-editor/hlkenndednhfkekhgcdicdfddnkalmdm) để lấy).
✔ **Google Sheet** (để lưu trữ dữ liệu liên hệ).

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/5015](https://n8n.io/workflows/5015).
- **Mở n8n Editor** → Nhấn **"Import"** → Chọn file JSON vừa tải.
- **Hoặc copy/paste** JSON từ file vào Editor và nhấn **"Import"**.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
##### **A. Cấu Hình Google Search Authenticated**
- **Tại node "Google Boolean Search"** → **Header Auth**:
  - Mở **Cookie-Editor** trên Chrome → Export **Header String**.
  - Dán vào trường **Cookie** trong **Header Auth** của node này.

##### **B. Cấu Hình OpenAI**
- **Tại node "Generate a Boolean Search String"** và **"Personalized Cold-Email Generator"**:
  - Điền **API Key OpenAI** vào **Credentials** (tìm tại [OpenAI Settings](https://platform.openai.com/settings/organization/api-keys)).

##### **C. Cấu Hình Hunter.io**
- **Tại node "Hunter"**:
  - Điền **API Key Hunter.io** vào **Credentials**.
  - **Lưu ý**: Miễn phí 25 lần sử dụng/tháng (đăng ký tại [Hunter.io](https://hunter.io/)).

##### **D. Cấu Hình Gmail**
- **Tại node "Gmail"**:
  - Chọn **Credentials** là tài khoản Gmail của bạn.
  - **Email lạnh sẽ được lưu trong Drafts** để bạn kiểm tra trước khi gửi.

##### **E. Cấu Hình Google Sheets**
- **Tại node "Create a new sheet" và "Add columns to new sheet"**:
  - Đổi tên **Google Sheet** thành tên phù hợp (ví dụ: **"LinkedIn Prospects"**).
  - **Cột cần thêm**: `linkedin_url`, `first_name`, `last_name`, `email`, `context`, `domain`.

##### **F. Cấu Hình AI Prompt (Cá Nhân Hóa)**
- **Tại node "Personalized Cold-Email Generator"**:
  - **Thay đổi System Prompt** để phản ánh thông tin cá nhân của bạn (ví dụ: tên công ty, vị trí, mục đích outreach).
  - Ví dụ:
    ```json
    "You are an AI assistant for sales outreach. Your task is to generate a personalized cold email for a sales demo. Use the following context: [LinkedIn profile details]."
    ```

##### **G. Điều Chỉnh Số Lượng Kết Quả**
- **Tại node "If desired results not reached"**:
  - Thay đổi giá trị `50` thành số kết quả mong muốn (ví dụ: `100`).

---

#### **3. Kích Hoạt ⚡️**
- **Test Run** với dữ liệu mẫu:
  - Nhấn **"Execute"** trên node đầu tiên (**"Wait"**).
  - Kiểm tra **Google Sheet** để xem liệu dữ liệu đã được lưu chưa.
- **Bật Active**:
  - Chuyển trạng thái workflow từ **"Inactive"** sang **"Active"**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết Nối Slack/Telegram** để nhận thông báo khi workflow hoàn thành.
   - Sử dụng node **Slack** hoặc **Telegram Bot** để gửi tin nhắn khi email được gửi thành công.

2. **Lưu Log Hoạt Động** trên Google Sheets hoặc Firebase.
   - Thêm node **Google Sheets** hoặc **HTTP Request** để ghi lại lịch sử hoạt động.

3. **Gửi Báo Cáo Định Kỳ** về tỷ lệ phản hồi.
   - Sử dụng node **Google Sheets** + **Google Apps Script** để tự động tạo báo cáo hàng tuần.

4. **Tối Ưu Boolean Search** để lấy kết quả chính xác hơn.
   - Thay đổi **System Prompt** của OpenAI để cải thiện chất lượng tìm kiếm.

5. **Sử Dụng Multiple Sheets** cho nhiều dự án khác nhau.
   - Thay đổi tên **Google Sheet** trong node **"Create a new sheet"** cho mỗi dự án.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào công việc chiến lược hơn, trong khi AI và tự động hóa làm việc 24/7. **Thay vì mất hàng giờ tìm kiếm và viết email lạnh thủ công, bạn chỉ cần cấu hình một lần và workflow sẽ tự động hoạt động!**

🚀 **Hành động ngay**:
1. **Import workflow** vào n8n của bạn.
2. **Cấu hình các credentials** theo hướng dẫn.
3. **Bật Active** và bắt đầu tự động hóa outreach!

**Nếu gặp vấn đề, các sếp có thể liên hệ tác giả [Abhijay Vuyyuru](https://www.linkedin.com/in/abhijayvuyyuru/) để hỗ trợ!** 🎁

---
**Chúc các sếp thành công với chiến dịch outreach mới!** 💼🚀