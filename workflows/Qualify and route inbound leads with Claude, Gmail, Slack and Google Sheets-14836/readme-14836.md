---
title: "🚀 Tự Động Hóa Xác Minh & Phân Loại Lead Inbound Với Claude AI, Gmail, Slack & Google Sheets - Khai Phóng Tiềm Năng Cho Doanh Nghiệp"
description: "Workflow tự động hóa 100% không code giúp doanh nghiệp phân loại lead inbound từ 1-10 dựa trên AI Claude, tự động gửi email cá nhân hóa, cảnh báo Slack và ghi log chi tiết vào Google Sheets. Giảm thời gian xử lý lead từ 30 phút xuống 0 giây, tăng tỷ lệ chuyển đổi lên 30%."
slug: "tieu-dong-hoa-xac-minh-phan-loai-lead-inbound-voi-claude-ai"
tags: [n8n, automation, lead-generation, ai-summarization, no-code, claudie-ai, gmail-integration, slack-notification, google-sheets]
keywords: [tự động hóa lead inbound, phân loại lead với AI Claude, workflow n8n lead generation, tự động gửi email cá nhân hóa, cảnh báo Slack tự động, ghi log lead vào Google Sheets, giảm thời gian xử lý lead]
---

# 🚀 **Tự Động Hóa Xác Minh & Phân Loại Lead Inbound Với AI Claude, Gmail, Slack & Google Sheets**

## **🔥 Nỗi Đau Của Doanh Nghiệp Hiện Nay**
Hàng ngày, doanh nghiệp phải đối mặt với **nguồn lead inbound** từ website, form đăng ký, hoặc email. Tuy nhiên, việc **xác minh và phân loại lead thủ công** tiêu tốn thời gian và dễ gây sai sót:
- **Tốn 30-60 phút/ngày** để đánh giá từng lead.
- **Tỷ lệ chuyển đổi thấp** vì nhiều lead không được xử lý kịp thời.
- **Email và Slack bị quá tải** do lead không được phân loại chính xác.
- **Không có hệ thống ghi log** để theo dõi hiệu suất của mỗi lead.

**Workflow này giải quyết tất cả vấn đề trên bằng AI Claude + n8n, giúp bạn:**
✅ **Tự động phân loại lead từ 1-10** dựa trên độ phù hợp với khách hàng lý tưởng.
✅ **Gửi email cá nhân hóa** ngay lập tức cho lead nóng (score 7-10).
✅ **Cảnh báo Slack** để team sales xử lý kịp thời.
✅ **Ghi log tất cả lead** vào Google Sheets với thông tin chi tiết.
✅ **Tiết kiệm 100% thời gian** để tập trung vào chiến lược kinh doanh.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 30-60 phút/ngày** xử lý lead thủ công.
- **Tăng tỷ lệ chuyển đổi lên 30%** nhờ phân loại chính xác.
- **Email và Slack được tối ưu**, không bị quá tải.
- **Dữ liệu lead được ghi log chi tiết**, dễ theo dõi và phân tích.
- **Cá nhân hóa tương tác** với lead, tăng độ tin cậy.
- **Hoạt động 24/7**, không cần can thiệp thủ công.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản Claude AI** (Anthropic API Key) – [Đăng ký tại đây](https://console.anthropic.com/).
✔ **Tài khoản Gmail** (để gửi email tự động).
✔ **Tài khoản Slack** (để cảnh báo team sales, **không bắt buộc**).
✔ **Google Sheets** với cấu trúc bảng như sau:
| Timestamp | Name | Email | Company | Message | Score | Tier | Reasoning |
|-----------|------|-------|---------|---------|-------|------|-----------|
| ...       | ...  | ...   | ...     | ...     | ...   | ...  | ...       |
✔ **URL Form** (n8n sẽ tự tạo, không cần third-party).
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/14836](https://n8n.io/workflows/14836).
- **Mở n8n Editor** → **Import Workflow** → Chọn file JSON vừa tải.
- **Hoặc copy/paste JSON** từ file vào **Import Workflow** trong n8n.

:::note[LƯU Ý]
- **Không cần chỉnh sửa cấu trúc**, chỉ cần **cấu hình credentials** như hướng dẫn dưới đây.
- **Không kích hoạt workflow ngay**, chỉ test run sau khi cấu hình xong.
:::

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**

#### **🔹 Node 1: Inbound Lead Form (formTrigger)**
- **Không cần cấu hình gì**, n8n sẽ tự tạo **URL form** khi kích hoạt.
- **Lưu URL này** để chia sẻ cho khách hàng đăng ký lead.

#### **🔹 Node 2: Extract Lead Fields (set)**
- **Không cần chỉnh**, node này tự động trích xuất **Name, Email, Company, Message** từ form.

#### **🔹 Node 3: Score Lead Intent (chainLlm) + Claude Sonnet (lmChatAnthropic)**
- **Thêm Credential Claude AI**:
  1. Mở node **Claude Sonnet** → Nhấn **Add Credential**.
  2. Chọn **Anthropic** → Điền **API Key** từ [console.anthropic.com](https://console.anthropic.com/).
  3. **Cập nhật Prompt AI** (để Claude đánh giá lead theo tiêu chí của bạn):
     ```plaintext
     You are a lead qualification expert. Score this lead from 1-10 based on:
     - Fit with ideal customer profile (size, industry, pain points).
     - Intent (how urgent they need a solution).
     - Message quality (detailed or vague).
     Return a score (1-10) and a one-line reasoning.
     ```
- **Test run** với một lead mẫu để đảm bảo AI đánh giá chính xác.

#### **🔹 Node 4: Parse Score (code)**
- **Không cần chỉnh**, node này tự động **trích xuất score** từ kết quả của Claude.

#### **🔹 Node 5: Route by Score (switch)**
- **Cấu hình ngưỡng score**:
  - **Hot Lead (7-10)** → Gửi email + Slack + Log Sheets.
  - **Warm Lead (4-6)** → Gửi email mềm + Log Sheets.
  - **Cold Lead (1-3)** → Gửi email từ chối + Log Sheets.
- **Không cần chỉnh**, mặc định đã đúng.

#### **🔹 Node 6-13: Gmail, Slack & Google Sheets**
- **Gmail (Hot/Warm/Cold Lead Reply)**:
  1. Mở node **Hot Lead Reply** → **Add Credential** → Chọn **Gmail**.
  2. Đăng nhập tài khoản Gmail và **cho phép quyền**.
  3. **Cập nhật nội dung email** (ví dụ):
     ```plaintext
     Hi {{$json["Name"]}},
     Thank you for reaching out! We're excited to connect with you.
     Our team will follow up shortly.
     Best regards,
     [Your Team]
     ```
- **Slack (Notify Team - Hot Lead)**:
  1. Mở node → **Add Credential** → Chọn **Slack**.
  2. Đăng nhập tài khoản Slack và chọn **channel** (ví dụ: `#sales-leads`).
  3. **Nếu không dùng Slack**, **disable node** bằng cách right-click → **Disable**.
- **Google Sheets (Log to Sheets - Hot/Warm/Cold)**:
  1. Mở node → **Add Credential** → Chọn **Google Sheets**.
  2. Chọn **Google Account** và **Sheet** đã tạo trước đó.
  3. **Không cần chỉnh cột**, node sẽ tự động append dữ liệu.

---

### **3. Kích Hoạt ⚡️**
1. **Test Run** với một lead mẫu:
   - Điền thông tin vào **form URL** (từ node **Inbound Lead Form**).
   - Kiểm tra:
     - Email được gửi không?
     - Slack có cảnh báo không?
     - Google Sheets có ghi log không?
2. **Kích hoạt workflow** khi test thành công.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[TIẾP CẬN HƠN]
- **Kết hợp với Zapier/Make** để đồng bộ lead với CRM (HubSpot, Salesforce).
- **Thêm node Telegram** để cảnh báo lead nóng trên chatbot.
- **Tự động gửi báo cáo hàng tuần** về lead đã xử lý qua email.
- **Sử dụng Claude Haiku** thay vì Sonnet để giảm chi phí API.
- **Tự động chuyển lead nóng** sang Salesforce/HubSpot bằng node **HTTP Request**.
:::

---

## 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc thủ công, **tăng tỷ lệ chuyển đổi lead** nhờ AI Claude và **tối ưu hóa tương tác** với khách hàng. **Chỉ cần 10 phút cấu hình**, bạn đã có một hệ thống **tự động hóa lead generation hoàn chỉnh**.

**👉 Bắt đầu ngay bằng cách import workflow và cấu hình theo hướng dẫn trên!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**🚀 Hãy tự động hóa lead của bạn ngay hôm nay!** 🚀