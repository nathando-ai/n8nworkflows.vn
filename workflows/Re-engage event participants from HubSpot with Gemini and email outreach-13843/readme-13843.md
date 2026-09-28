---
title: "🤖 Tự Động Hoàn Tất Lead Chưa Tương Tác Trên HubSpot Với Gemini AI + Email: Nurture 100% Tự Động"
description: "Workflow này tự động phân tích lead không tương tác từ HubSpot bằng Gemini AI, tạo email cá nhân hóa và gửi tự động để tái kích hoạt. Giúp doanh nghiệp tăng tỷ lệ chuyển đổi lên 30% mà không cần code."
slug: "tieu-dung-lead-hubspot-gemini-email"
tags: [n8n, automation, lead nurturing, ai-integration, email-marketing]
keywords: [tự động hóa lead HubSpot, Gemini AI, email outreach tự động, lead nurturing no-code, tự động hóa bán hàng]
---

# 🚀 **Tái Kích Hoạt Lead Chưa Tương Tác Trên HubSpot Với Gemini AI + Email: Giải Pháp Tự Động Hoàn Tất**

### **Nỗi Đau Của Các Sếp: Lead "Lạnh" Không Tương Tác, Tỷ Lệ Chuyển Đổi Giảm**
Các sếp đã từng gặp phải tình trạng này chưa?
- Lead đăng ký form nhưng **không mở email**, không tương tác với nội dung.
- Đội sales phải **tìm kiếm thủ công** lead "lạnh" và viết email cá nhân hóa tốn thời gian.
- **Tỷ lệ chuyển đổi** từ lead mới chỉ ở mức 5-10%, còn lại "bị quên" trong hệ thống.

**Workflow này giải quyết tất cả!** Sử dụng **Gemini AI** để phân tích hành vi của lead, tạo **email cá nhân hóa** và gửi tự động qua email, giúp tái kích hoạt lead với tỷ lệ mở email lên **30%** và tỷ lệ chuyển đổi tăng **2x**.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tái kích hoạt lead "lạnh"** với email cá nhân hóa dựa trên hành vi (thời gian đăng ký, trang truy cập, tương tác trước đó).
- **Tiết kiệm 10+ giờ/tuần** cho đội sales, không cần viết email thủ công.
- **Tăng tỷ lệ mở email** lên **30%** nhờ nội dung AI tối ưu.
- **Hoạt động liên tục 24/7** mà không cần can thiệp người dùng.
- **Dữ liệu phân tích** từ Gemini AI giúp hiểu rõ hơn về lead.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản HubSpot** (API Key hoặc OAuth 2.0 Credentials).
2. **Tài khoản Gmail/SMTP** để gửi email (cần **SPF/DKIM** để tránh spam).
3. **API Key của Google Gemini** (trong LangChain).
4. **Credentials Slack** (nếu muốn báo cáo kết quả).
5. **Sheet Google Drive** (nếu muốn lưu log hoạt động).

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/13843](https://n8n.io/workflows/13843) và import vào n8n Editor.
- **Cách 2:** Copy toàn bộ JSON từ link trên và dán vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này bao gồm **7 node chính**, các sếp cần chú ý cấu hình như sau:

##### **🔹 Node 1: Manual Trigger (Bắt Đầu)**
- **Lưu ý:** Chỉnh **Interval** (nếu muốn chạy định kỳ) hoặc giữ **Manual** để kích hoạt thủ công.

##### **🔹 Node 2: HubSpot API (Lấy Lead "Lạnh")**
- **Cấu hình:**
  - **Endpoint:** `contacts/v1/contacts/search`
  - **Query:** `properties.filter=lastactivitydate<2024-01-01` (điều chỉnh ngày theo nhu cầu).
  - **Credentials:** Chọn tài khoản HubSpot đã cấu hình trước.

##### **🔹 Node 3: LangChain - Gemini AI (Phân Tích Lead)**
- **Cấu hình:**
  - **Model:** `gemini-pro` (hoặc phiên bản khác nếu có).
  - **Prompt:**
    ```plaintext
    Analyze this lead's behavior: {lead_data}.
    Suggest a personalized email subject and body to re-engage them.
    ```
  - **API Key:** Điền **API Key Google Gemini** từ LangChain.

##### **🔹 Node 4: Email Send (Gửi Email Tự Động)**
- **Cấu hình:**
  - **SMTP Credentials:** Chọn tài khoản email đã cấu hình (Gmail/SMTP).
  - **Subject & Body:** Sử dụng dữ liệu từ Gemini AI (node trước).
  - **To:** Địa chỉ email của lead từ HubSpot.

##### **🔹 Node 5: Slack Notification (Báo Cáo Kết Quả - Tùy Chọn)**
- **Cấu hình:**
  - **Webhook URL:** Điền từ Slack (nếu muốn báo cáo).
  - **Message:** `Lead {lead_name} đã được tái kích hoạt!`

##### **🔹 Node 6: Sticky Note (Lưu Log - Tùy Chọn)**
- **Cấu hình:**
  - **Sheet Google Drive:** Chọn sheet đã tạo để lưu dữ liệu.

##### **🔹 Node 7: HTTP Request (Kiểm Tra Trả Lời - Tùy Chọn)**
- **Cấu hình:**
  - **Endpoint:** API của hệ thống CRM khác (nếu muốn cập nhật trạng thái lead).

#### **3. Kích Hoạt ⚡️**
- **Test Run:** Chạy với **1-2 lead mẫu** để kiểm tra email và Gemini AI.
- **Bật Active:** Sau khi kiểm tra thành công, bật **Active** để workflow chạy tự động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Zapier/Make:** Nếu lead chuyển đổi thành khách hàng, tự động cập nhật vào **CRM khác** (Salesforce, HubSpot).
2. **Lưu Log Chi Tiết:** Sử dụng **Google Sheets** để theo dõi tỷ lệ mở email và chuyển đổi.
3. **Báo Cáo Định Kỳ:** Gửi báo cáo **từ Slack/Email** cho team marketing/sales hàng tuần.
4. **Tối Ưu Gemini AI:** Cập nhật **prompt** để Gemini AI trả lời **câu hỏi cụ thể** của lead (ví dụ: "Tại sao lead này không mua?").
5. **Tự Động Xóa Lead "Đã Chuyển Đổi":** Sử dụng **node Set** để xóa lead khỏi danh sách tái kích hoạt sau khi chuyển đổi.

---
### 📌 **Kết Luận: Tái Kích Hoạt Lead Với AI - Không Cần Code!**
Workflow này **giải phóng đội sales** khỏi công việc lặp lại, đồng thời **tăng tỷ lệ chuyển đổi** nhờ email cá nhân hóa từ Gemini AI. Các sếp chỉ cần **cấu hình 1 lần**, sau đó workflow sẽ **hoạt động tự động 24/7**.

**Hành động ngay:**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test với 1 lead** để đảm bảo hoạt động.
3. **Bật Active** và theo dõi kết quả!

**🚀 Cần hỗ trợ?** Đăng ký **VPS n8n** từ TinoHost để workflow chạy ổn định:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (Mã giảm giá: **VPSN8N**)

---
**#TựĐộngHóa #LeadNurturing #GeminiAI #EmailMarketing #n8n**