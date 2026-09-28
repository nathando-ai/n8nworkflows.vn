---
title: "🚀 Tự Động Hóa Xếp Loại & Phân Tích Lead Tối Tiến Với GPT-4o-mini: Google Sheets → Airtable → HubSpot"
description: "Workflow tự động hóa 24/7 phân tích và phân loại lead từ Google Sheets, đồng bộ hóa dữ liệu sang Airtable và HubSpot với AI GPT-4o-mini, tiết kiệm 10+ giờ công mỗi tuần cho bộ phận Sales/Marketing."
slug: "tieu-dong-hoa-xep-loai-phan-tich-lead-gpt-4o-mini"
tags: [n8n, automation, ai, lead-generation, crm, google-sheets, airtable, hubspot, gpt-4o-mini, no-code]
keywords: [tự động hóa lead generation, phân tích lead với AI, đồng bộ Google Sheets Airtable HubSpot, workflow n8n AI, tự động hóa sales funnel, phân loại lead bằng GPT-4o-mini]
---

# 🚀 **Tự Động Hóa Xếp Loại & Phân Tích Lead Tối Tiến Với GPT-4o-mini: Google Sheets → Airtable → HubSpot**

## **🔍 Nỗi Đau Của Các Sếp: Lead "Lơ Mơ" & Thời Gian "Chìm Đắm" Trong Dữ Liệu**
Hàng ngày, bộ phận Sales/Marketing của các sếp phải:
- **Lọc thủ công** hàng trăm lead từ Google Sheets, Airtable hay HubSpot để tìm ra những cá nhân phù hợp với mục tiêu.
- **Phân loại lead** dựa trên chức vụ, cấp bậc, và ngành nghề – một công việc tẻ nhạt, dễ mắc sai sót, và tốn thời gian **10+ giờ/tuần**.
- **Đồng bộ hóa dữ liệu** giữa nhiều nền tảng (Google Sheets, Airtable, HubSpot) một cách thủ công, dẫn đến **trùng lặp thông tin** và **sai lệch dữ liệu**.
- **Bỏ lỡ cơ hội** vì không phân tích được **độ phù hợp** của lead với chiến lược marketing hiện tại.

**Workflow này giải quyết tất cả!** Sử dụng **GPT-4o-mini** (mô hình AI tối ưu chi phí của OpenAI), nó **tự động phân loại lead** theo chức vụ, cấp bậc, và ngành nghề, đồng thời **cập nhật đồng bộ** dữ liệu sang **Google Sheets, Airtable, và HubSpot** – **không cần viết một dòng code nào!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và **không bị gián đoạn**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để tránh phụ thuộc vào phiên bản cloud có giới hạn.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** – giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đảm bảo tốc độ xử lý nhanh cho AI)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 10+ giờ/tuần** cho bộ phận Sales/Marketing – **tự động hóa 100% quá trình phân loại lead**.
✅ **Chính xác cao** – AI phân tích lead theo **ngôn ngữ tự nhiên**, tránh sai sót của con người.
✅ **Dữ liệu đồng bộ hóa tự động** giữa **Google Sheets, Airtable, và HubSpot** – **không còn trùng lặp, không còn sai lệch**.
✅ **Cập nhật liên tục** – Workflow chạy **mỗi giờ**, đảm bảo lead mới luôn được phân tích và xử lý kịp thời.
✅ **Cá nhân hóa marketing** – Biết chính xác **chức vụ, cấp bậc, và ngành nghề** của mỗi lead để tối ưu chiến dịch.
✅ **Giảm chi phí** – Sử dụng **GPT-4o-mini** (rẻ hơn GPT-4) nhưng vẫn đảm bảo độ chính xác cao.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
| **Tài Khoản/Dịch Vụ**       | **Tham Số Cần Thiết**                          | **Lưu Ý** |
|-----------------------------|-----------------------------------------------|-----------|
| **Google Sheets**            | - File Google Sheets chứa lead (cột **Status = "Pending"**) <br> - Thông tin **Name, Email** (cột bắt buộc) | Chỉ đọc và cập nhật cột **Function, Seniority, Reviewed**. |
| **Airtable**                | - Base Airtable (CRM) <br> - Table chứa lead <br> - Cột **Email** (để upsert) | Workflow sẽ **upsert** (thêm/mà cập nhật) lead theo Email. |
| **HubSpot**                 | - API Key HubSpot <br> - Domain HubSpot | Workflow sẽ **tạo/mà cập nhật** contact trong HubSpot. |
| **OpenAI API Key**           | - API Key từ [OpenAI](https://platform.openai.com/) | Chọn mô hình **gpt-4o-mini** (rẻ và hiệu quả). |
| **n8n Self-hosted**         | - VPS với **4GB RAM trở lên** (để chạy AI ổn định) | Khuyến cáo sử dụng **VPS Xeon** để tối ưu tốc độ. |

---
:::note[CHUẨN BỊ TRƯỚC KHI CHẠY]
- **Kiểm tra dữ liệu Google Sheets**:
  - Cột **Status** phải có giá trị **"Pending"** để workflow đọc.
  - Cột **Name** và **Email** **không được bỏ trống**.
  - Nếu có cột **Title, Company, LinkedIn**, workflow sẽ **điền mặc định** nếu thiếu.
- **Airtable & HubSpot**:
  - Đảm bảo **cột Email** tồn tại trong cả hai nền tảng để **upsert** và **sync** dữ liệu.
  - Nếu chưa có, tạo **table mới** trong Airtable và **contact list** trong HubSpot.
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
**Bước 1:** Tải workflow từ [n8n.io/workflows/7128](https://n8n.io/workflows/7128) (chọn **Download JSON**).
**Bước 2:** Trên **n8n Editor**, nhấn **Import** → Chọn file JSON vừa tải.
**Bước 3:** Workflow sẽ hiển thị **10 nodes** như trong danh sách dưới đây.

---
#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflows này có **10 nodes chính**, mỗi node đều cần cấu hình kỹ lưỡng. Dưới đây là **hướng dẫn chi tiết** cho từng node quan trọng:

##### **🕒 Node 1: ⏰ Run Every Hour (Schedule Trigger)**
- **Cấu hình**:
  - **Frequency**: Chọn **Hourly** (mỗi giờ).
  - **Time**: Chọn giờ phù hợp (ví dụ: **8h sáng** để bắt đầu ngày làm việc).
- **Lưu ý**:
  - Nếu muốn chạy **ngày nào đó**, chọn **Cron expression** như `0 8 * * *` (mỗi ngày lúc 8h).

##### **📄 Node 2: 📄 Read Pending Contacts (Google Sheets)**
- **Cấu hình**:
  - **Credentials**: Chọn **Google Sheets** đã cấu hình trước.
  - **Operation**: Chọn **Get rows**.
  - **Sheet Name**: Chọn **tên sheet** chứa lead.
  - **Query**: Điền:
    ```json
    {
      "Status": "Pending",
      "Name": {"isNotNull": true},
      "Email": {"isNotNull": true}
    }
    ```
- **Lưu ý**:
  - Nếu sheet có **header khác**, chỉnh sửa **Query** tương ứng.
  - Nếu muốn **lọc thêm điều kiện**, mở rộng **Query** (ví dụ: `Company: {"isNotNull": true}`).

##### **🧪 Node 3: 🧪 Filter Name & Email (Filter)**
- **Cấu hình**:
  - **Condition**: Chọn **JSONPath** → `$.Name` và `$.Email` **không được null**.
  - **If**: Chọn **true** (chỉ giữ lead có Name và Email).
- **Lưu ý**:
  - Nếu có lead **không có Name hoặc Email**, nó sẽ **bị loại bỏ tự động**.

##### **🧹 Node 4: 🧹 Clean Contact Data (Code)**
- **Cấu hình**:
  - Mở **Code Editor**, chỉnh sửa để **điền mặc định** cho các trường thiếu:
    ```javascript
    // Điền mặc định cho trường thiếu
    if (!$.Title) $.Title = "Unknown";
    if (!$.Company) $.Company = "Unknown";
    if (!$.LinkedIn) $.LinkedIn = "";
    ```
- **Lưu ý**:
  - Nếu muốn **điền giá trị khác**, chỉnh sửa đoạn code này.

##### **🧠 Node 5: 🧠 LLM - GPT-4o-mini (Agent)**
- **Cấu hình**:
  - **Credentials**: Chọn **OpenAI** đã cấu hình (API Key).
  - **Model**: Chọn **gpt-4o-mini**.
  - **Prompt**: Workflow đã tự động cấu hình, **không cần chỉnh sửa** (nếu muốn thay đổi, mở **Sticky Note** để xem).
- **Lưu ý**:
  - Nếu **API Key hết hạn**, workflow sẽ **bị lỗi**. Đảm bảo **API Key hoạt động**.

##### **🧩 Node 6: 🧩 Parse or Fallback Role Tags (Code)**
- **Cấu hình**:
  - Mở **Code Editor**, kiểm tra logic **parse** kết quả từ AI:
    ```javascript
    // Parse kết quả từ AI và thêm fallback nếu cần
    if ($.Function && $.Seniority) {
      // Nếu AI phân loại thành công, giữ kết quả
    } else {
      // Nếu AI thất bại, sử dụng keyword fallback
      $.Function = "Unknown";
      $.Seniority = "Unknown";
    }
    ```
- **Lưu ý**:
  - Nếu muốn **thay đổi logic fallback**, chỉnh sửa đoạn code này.

##### **🧠 Node 7: 🧠 Classify Role & Seniority (lmChatOpenAi)**
- **Cấu hình**:
  - **Credentials**: Chọn **OpenAI**.
  - **Model**: **gpt-4o-mini**.
  - **Prompt**: Workflow đã tự động cấu hình để **phân loại chức vụ và cấp bậc** dựa trên:
    - **Title** (ví dụ: "CTO", "Marketing Manager").
    - **Company** (ngành nghề).
    - **LinkedIn** (nếu có).
  - **Response Format**: AI trả về **JSON** với các trường:
    ```json
    {
      "Function": "CTO/VP/Marketing Director/Engineering Lead/Other",
      "Seniority": "Executive/Senior/Junior/Unknown",
      "Department": "Tech/Marketing/Sales/HR/Other"
    }
    ```
- **Lưu ý**:
  - Nếu **AI trả về kết quả không hợp lệ**, node **fallback** sẽ hoạt động (đã cấu hình ở Node 6).

##### **📊 Node 8: 📊 Update Contact in Sheet (Google Sheets)**
- **Cấu hình**:
  - **Credentials**: Chọn **Google Sheets**.
  - **Operation**: Chọn **Append or Update**.
  - **Sheet Name**: Chọn **tên sheet** chứa lead.
  - **Row Data**: Chọn **JSONPath** → `$.` (cập nhật toàn bộ dữ liệu).
  - **Update Columns**: Chọn các cột cần cập nhật:
    - `Function`, `Seniority`, `Reviewed` (đặt giá trị `true`).
- **Lưu ý**:
  - Nếu **cột không tồn tại**, Google Sheets sẽ **tự động tạo**.

##### **🔁 Node 9: 🔁 Sync to Airtable (Airtable)**
- **Cấu hình**:
  - **Credentials**: Chọn **Airtable**.
  - **Operation**: Chọn **Upsert**.
  - **Base ID**: ID của **Base Airtable**.
  - **Table Name**: Tên **table** chứa lead.
  - **Record ID Field**: Chọn **Email** (để **upsert** theo Email).
  - **Record Data**: Chọn **JSONPath** → `$.` (đồng bộ toàn bộ dữ liệu).
- **Lưu ý**:
  - Nếu **Email trùng**, Airtable sẽ **cập nhật** thay vì thêm mới.

##### **📬 Node 10: 📬 Push to HubSpot (HubSpot)**
- **Cấu hình**:
  - **Credentials**: Chọn **HubSpot**.
  - **Operation**: Chọn **Create or Update Contact**.
  - **Email**: Chọn **JSONPath** → `$.Email`.
  - **Properties**: Chọn **JSONPath** → `$.` (đồng bộ toàn bộ dữ liệu).
- **Lưu ý**:
  - Nếu **contact không tồn tại**, HubSpot sẽ **tạo mới**.
  - Nếu **contact đã tồn tại**, HubSpot sẽ **cập nhật**.

---
#### **3. Kích Hoạt ⚡️ Workflow**
**Bước 1:** **Test Run** với **dữ liệu mẫu**:
- Nhấn **Execute Node** trên **Node 1 (⏰ Run Every Hour)**.
- Kiểm tra **Output** của từng node để đảm bảo **không lỗi**.
- Nếu có **lỗi**, kiểm tra lại **credentials** và **cấu hình**.

**Bước 2:** **Bật Active**:
- Nhấn **Active** trên góc trên bên phải.
- Workflow sẽ **chạy tự động mỗi giờ** (hoặc theo thời gian đã cấu hình).

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
#### **1. Thêm Slack/Telegram Notification**
- **Cách làm**:
  - Thêm **Node Slack/Telegram** sau **Node 10 (📬 Push to HubSpot)**.
  - Cấu hình để **gửi thông báo** khi workflow hoàn thành thành công hoặc lỗi.
  - **Dữ liệu gửi**: `Workflow đã hoàn thành thành công! Tải xuống [link Google Sheets](https://docs.google.com/spreadsheets/d/...)`.

#### **2. Lưu Log Lỗi & Gửi Email Hàng Ngày**
- **Cách làm**:
  - Thêm **Node Code** sau **Node 10** để **lưu log lỗi** vào Google Sheets