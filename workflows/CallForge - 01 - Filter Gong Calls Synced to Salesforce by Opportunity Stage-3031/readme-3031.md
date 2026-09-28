---
title: "🚀 **Lọc Gọi Điện Gong Tích Hợp Salesforce Theo Stage: Tự Động Học & Lọc Gọi Quý Giá Cho Sales**"
description: "Workflow tự động hóa lọc gọi điện từ Gong đã đồng bộ vào Salesforce theo stage (Meeting Booked/Discovery), giúp Sales chỉ xem gọi quan trọng, tiết kiệm 80% thời gian phân tích. Kết hợp AI và Salesforce để tối ưu pipeline doanh thu."
slug: "luc-gong-calls-salesforce-theo-stage"
tags: [n8n, automation, salesforce, gong, ai-workflow]
keywords: [tự động hóa gọi điện Gong, lọc gọi điện Salesforce, workflow Sales, AI trong Sales, tự động hóa CRM]
---

# 🚀 **Lọc Gọi Điện Gong Tích Hợp Salesforce Theo Stage: Tự Động Học & Lọc Gọi Quý Giá Cho Sales**

### **Nỗi Đau Của Các Sếp Sales**
Hàng ngày, các sếp Sales phải mất **giờ đồng hồ** để lọc và phân tích hàng trăm cuộc gọi từ Gong trong Salesforce. Nhiều cuộc gọi không liên quan đến stage quan trọng (chẳng hạn như *Meeting Booked* hoặc *Discovery*) làm **gián đoạn tập trung** và **tốn thời gian** cho việc phân tích thực sự. Kết quả?
- **Tỷ lệ chuyển đổi giảm** vì bỏ lỡ gọi quan trọng.
- **Dữ liệu không được tối ưu** vì phải lọc thủ công.
- **AI không được khai thác** để tự động phân loại gọi.

**Workflow này giải quyết vấn đề bằng cách:**
✅ **Tự động lọc gọi điện** theo stage quan trọng (Meeting Booked/Discovery).
✅ **Tích hợp AI** để xử lý và chuyển đổi gọi thành dữ liệu có giá trị.
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo **tính bảo mật và ổn định**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** phân tích gọi điện không quan trọng.
- **Chỉ xem gọi có stage Meeting Booked/Discovery**, tăng **tỷ lệ chuyển đổi**.
- **Dữ liệu được tự động phân loại** theo AI, giảm sai sót thủ công.
- **Hoạt động liên tục** (dự kiến chạy hàng giờ) mà không cần can thiệp.
- **Tích hợp Salesforce & Gong** một cách thông minh, không cần code.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Gong** với **API Key** (để lấy gọi điện).
✔ **Tài khoản Salesforce** với **OAuth2 API Key** (để lấy đối tượng Custom Object).
✔ **Workflow CallForge Preprocessor** (nếu chưa có, phải tạo trước).
✔ **Dữ liệu test** (gọi điện mẫu trong Salesforce để kiểm tra).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/3031](https://n8n.io/workflows/3031) và import vào **n8n Editor**.
- **Cách 2:** Copy toàn bộ JSON từ [đây](https://uploads.n8n.io/templates/callforgeshadow.json) và paste vào **n8n Editor** → **Import Workflow**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **9 node chính**, các sếp cần chú ý đến:

##### **A. Node "Get Gong Call" (n8n-nodes-base.gong)**
- **Credentials:** Chọn `gongApi` (đã cấu hình trước khi import).
- **Key Parameters:**
  - `operation`: Đặt là `get`.
  - **Lưu ý:** Nếu API Key không đúng, node này sẽ **không lấy được gọi điện**.

##### **B. Node "Get all custom Salesforce Gong Objects" (n8n-nodes-base.salesforce)**
- **Credentials:** Chọn `salesforceOAuth2Api`.
- **Key Parameters:**
  - `operation`: `getAll`.
  - `resource`: `customObject`.
  - **Lưu ý:** Đảm bảo **Custom Object** trong Salesforce có tên đúng với **Gong Call Object** (thường là `Gong_Call__c` hoặc tương tự).

##### **C. Node "Check if Primary Opportunity Contains Value" & "Check if Opportunity Stage is Meeting Booked or Discovery" (n8n-nodes-base.if)**
- **Cấu hình điều kiện:**
  - Node **IF 1** kiểm tra nếu `Primary Opportunity` có giá trị.
  - Node **IF 2** lọc stage là `Meeting Booked` hoặc `Discovery`.
  - **Lưu ý:** Nếu stage không đúng, gọi điện sẽ **bị bỏ qua**.

##### **D. Node "Pass to Gong Call Preprocessor" (n8n-nodes-base.executeWorkflow)**
- **Workflow liên kết:** Đảm bảo đã tạo **CallForge Preprocessor** trước và chọn nó ở đây.
- **Lưu ý:** Nếu workflow này chưa được tạo, **node này sẽ lỗi**.

##### **E. Node "Run Hourly" (n8n-nodes-base.scheduleTrigger)**
- **Cấu hình:** Đặt thời gian chạy là **mỗi giờ** (hoặc tùy chỉnh theo nhu cầu).
- **Lưu ý:** Nếu không muốn chạy tự động, có thể **bỏ node này** và sử dụng **Manual Trigger** thay thế.

#### **3. Kích Hoạt ⚡️**
- **Test Run:** Chạy thử với **dữ liệu mẫu** (gọi điện đã đồng bộ vào Salesforce).
- **Bật Active:** Sau khi kiểm tra thành công, **bật workflow** để chạy tự động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram:**
   - Thêm node **Slack/Telegram** để **báo cáo gọi quan trọng** ngay khi được lọc.
   - Ví dụ: *"Gọi mới từ Lead ABC (Stage: Meeting Booked) đã được xử lý!"*

2. **Lưu Log Dữ Liệu:**
   - Thêm node **Google Sheets** hoặc **Airtable** để **lưu lịch sử gọi** đã được lọc.
   - Giúp **theo dõi hiệu suất** và **tối ưu pipeline**.

3. **Tích Hợp AI Tự Động:**
   - Nếu có **LLM (AI Chatbot)**, có thể thêm node **n8n-nodes-base.llm** để **tóm tắt gọi** và gửi cho Sales.
   - Ví dụ: *"AI đã tóm tắt gọi: Khách hàng quan tâm đến tính năng X, đề xuất gặp lại vào ngày Y."*

4. **Báo Cáo Định Kỳ:**
   - Sử dụng **node Schedule Trigger** để gửi **báo cáo tuần/month** về gọi quan trọng cho Team Sales.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp Sales khỏi việc lọc gọi điện thủ công, đồng thời **tối ưu hóa pipeline** bằng cách chỉ tập trung vào gọi có stage quan trọng. **Kết hợp AI và Salesforce**, nó giúp **tăng tỷ lệ chuyển đổi** và **giảm sai sót**.

**Hành động ngay:**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test với dữ liệu mẫu** trước khi bật chạy tự động.
3. **Tích hợp thêm Slack/Google Sheets** để tối ưu hóa hơn.

**🚀 Cùng tự động hóa Sales ngay hôm nay!** 🚀