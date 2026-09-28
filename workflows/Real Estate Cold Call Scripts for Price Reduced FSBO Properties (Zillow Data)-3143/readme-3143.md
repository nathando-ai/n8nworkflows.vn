---
title: "📞 Tự Động Hoá Gọi Lạnh Cho Nhà Đất Giảm Giá (FSBO) - Sử Dụng AI & Zillow Data (n8n)"
description: "Workflow tự động hóa tìm kiếm, phân tích và tạo script gọi điện AI cho các nhà đất giảm giá (FSBO) trên Zillow, giúp các sếp tiết kiệm thời gian và tăng tỷ lệ thành công trong giao dịch bất động sản. Kết hợp AI, API Zillow và Airtable để tối ưu hóa quy trình bán hàng."
slug: "tieu-dong-hoa-goi-lanh-cho-nha-dat-giam-gia-fsbo"
tags: [n8n, automation, ai, real-estate, zillow, airtable, no-code]
keywords: [tự động hóa gọi lạnh bất động sản, script gọi điện AI, n8n workflow bất động sản, tìm kiếm nhà đất giảm giá, tự động hóa Zillow, AI cho giao dịch bất động sản]
---

# 🚀 **Tự Động Hoá Gọi Lạnh Cho Nhà Đất Giảm Giá (FSBO) - Sử Dụng AI & Zillow Data**

### **Giải Pháu Nỗi Đau Của Các Sếp Trong Bất Động Sản**
Bạn có bao giờ phải:
- **Tìm kiếm thủ công** hàng trăm nhà đất giảm giá (FSBO - For Sale By Owner) trên Zillow?
- **Tạo script gọi điện** phù hợp cho từng chủ nhà, nhưng lại mất nhiều thời gian và không cá nhân hóa?
- **Không biết** liệu giá nhà đang giảm là do thị trường hay do chủ nhà muốn bán nhanh?
- **Lặp lại** công việc gọi điện hàng ngày mà không có kết quả rõ ràng?

Workflow này **tự động hóa toàn bộ quy trình** từ tìm kiếm đến tạo script gọi điện AI, giúp các sếp **tiết kiệm 80% thời gian** và **tăng tỷ lệ thành công** trong giao dịch bất động sản.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tự động tìm kiếm** tất cả nhà đất giảm giá (FSBO) trên Zillow theo tiêu chí cá nhân hóa.
✅ **Tạo script gọi điện AI** phù hợp với từng chủ nhà, dựa trên dữ liệu thị trường và lịch sử.
✅ **Phân tích thị trường** để xác định liệu giá giảm là do thị trường hay do chủ nhà muốn bán nhanh.
✅ **Tích hợp Airtable** để lưu trữ và quản lý danh sách gọi điện một cách chuyên nghiệp.
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.
✅ **Tăng tỷ lệ thành công** trong giao dịch do script gọi điện được tối ưu hóa.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản Zillow API** (đăng ký tại [Zillow Developer Portal](https://www.zillow.com/howto/api/)) để lấy dữ liệu nhà đất.
2. **Airtable API Key** (đăng ký tại [Airtable](https://airtable.com/api)) để lưu trữ danh sách gọi điện.
3. **OpenAI API Key** (đăng ký tại [OpenAI](https://platform.openai.com/account/api-keys)) để sử dụng mô hình AI (ChatGPT, Summarization).
4. **Tài khoản n8n Self-hosted** (cài đặt trên VPS như hướng dẫn [n8n.io](https://n8n.io/)).
5. **Thông tin API Key** của các dịch vụ trên để cấu hình trong workflow.
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/3143) hoặc copy toàn bộ JSON từ trang này.
- Mở **n8n Editor** và chọn **Import Workflow** → Chọn file JSON hoặc dán JSON vào ô nhập.
- **Lưu workflow** với tên **"Zillow FSBO Cold Call Scripts"** để dễ quản lý.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **15 node** quan trọng, các sếp cần chú ý cấu hình như sau:

##### **A. Cấu Hình API Keys**
- **Node "Zillow Search" (HTTP Request)**:
  - Điền **URL**: `https://www.zillow.com/webservice/GetSearchResults.htm`
  - Thêm **Header**:
    ```
    User-Agent: Mozilla/5.0
    ZWS-ID: [Your Zillow API Key]
    ```
  - Thêm **Query Parameters**:
    ```
    zipcode=[Your Target ZIP Code]
    rentzestimate=true
    ```

- **Node "Call Script Database Airtable" (Airtable)**:
  - Chọn **Base** và **Table** trong Airtable (ví dụ: `Cold Call Scripts`).
  - Điền **API Key** từ Airtable vào **Credentials**.

- **Node "Call Script Generator" (OpenAI)**:
  - Chọn **Model**: `gpt-3.5-turbo` (hoặc `gpt-4` nếu có budget).
  - Điền **API Key** từ OpenAI vào **Credentials**.
  - Cấu hình **Prompt** để AI tạo script gọi điện phù hợp:
    ```json
    "prompt": "Tạo một script gọi điện chuyên nghiệp cho chủ nhà đang bán nhà giảm giá (FSBO) tại {address}. Script phải bao gồm:
    1. Giới thiệu bản thân và mục đích gọi điện.
    2. Nêu lý do giá nhà đang giảm (dựa trên dữ liệu thị trường: {market_overview}).
    3. Đề xuất giá trị của tôi (nếu là đại lý) hoặc lý do mua nhà (nếu là nhà đầu tư).
    4. Kêu gọi hành động (call-to-action) rõ ràng.
    Đảm bảo script ngắn gọn (under 1 minute), thân thiện và chuyên nghiệp."
    ```

- **Node "Historical Market Summary" (Chain Summarization)**:
  - Chọn **Model**: `gpt-3.5-turbo` (hoặc `gpt-4`).
  - Cấu hình **Prompt** để AI tóm tắt thị trường:
    ```json
    "prompt": "Tóm tắt tình hình thị trường bất động sản tại {location} trong 6 tháng qua dựa trên dữ liệu:
    - Giá trung bình: {avg_price}
    - Tỷ lệ giảm giá: {price_drop_percentage}
    - Thời gian trên thị trường: {days_on_market}
    Đưa ra kết luận về xu hướng giá và lý do giá nhà này đang giảm."
    ```

##### **B. Cấu Hình Node "FSBO Property Criteria Set" (Set)**
- Thêm **tiêu chí lọc** cho nhà đất FSBO:
  ```json
  {
    "propertyType": "Single Family",
    "price": "<= [Your Max Price]",
    "bedrooms": ">= 2",
    "bathrooms": ">= 2",
    "daysOnMarket": "> 30"
  }
  ```

##### **C. Cấu Hình Node "Investment Calculator" (Code)**
- Sửa code để tính toán ROI (Return on Investment) cho nhà đầu tư:
  ```javascript
  // Ví dụ: Tính toán chi phí mua, chi phí sửa chữa, thu nhập hàng tháng
  const rent = json["rentZestimate"]["rentZestimate"]["amount"];
  const price = json["Zillow Search"]["response"]["results"]["result"][0]["value"];
  const repairCost = 10000; // Giả sử
  const monthlyCashFlow = rent - (price / 360) - (repairCost / 12);

  return {
    "roi": (monthlyCashFlow / (price + repairCost)) * 100,
    "monthlyCashFlow": monthlyCashFlow
  };
  ```

##### **D. Cấu Hình Node "Execute Workflow Trigger" (FSBO)**
- Chọn **Workflow** cần kích hoạt khi tìm thấy nhà đất phù hợp (ví dụ: `Send Email to Agent` hoặc `Add to CRM`).

#### **3. Kích Hoạt ⚡️**
- **Test Run** với dữ liệu mẫu:
  - Gửi một **form submission** (nếu có node `formTrigger`) hoặc kích hoạt thủ công.
  - Kiểm tra **log** trong n8n để đảm bảo tất cả node hoạt động đúng.
- **Bật Active** workflow sau khi kiểm tra thành công.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết Nối Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram Bot** để nhận thông báo khi workflow tìm thấy nhà đất mới.
   - Ví dụ:
     ```json
     "message": "🚨 New FSBO Property Found!\nAddress: {address}\nPrice: {price}\nScript: {call_script}"
     ```

2. **Lưu Log Lịch Sử Gọi Điện**:
   - Sử dụng **Airtable** hoặc **Google Sheets** để lưu trữ lịch sử gọi điện, kết quả và follow-up.
   - Thêm node **Airtable** sau node `Call Script Generator` để ghi dữ liệu.

3. **Gửi Báo Cáo Định Kỳ**:
   - Tạo một **workflow riêng** để gửi báo cáo hàng tuần về số lượng nhà đất tìm thấy, tỷ lệ thành công và ROI.
   - Sử dụng node **Email** (Gmail/SendGrid) hoặc **Slack**.

4. **Tối Ưu Hóa Script Gọi Điện**:
   - Đánh giá và cập nhật **prompt** cho OpenAI dựa trên phản hồi từ chủ nhà.
   - Thêm **các biến động** như thời gian gọi (sáng/chiêu) hoặc ngày trong tuần.

5. **Tích Hợp CRM**:
   - Nếu sử dụng **HubSpot** hoặc **Pipedrive**, thêm node **HTTP Request** để cập nhật thông tin nhà đất vào CRM.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** của các sếp để tập trung vào việc **tìm kiếm cơ hội đầu tư** hoặc **kết nối với khách hàng tiềm năng** thay vì làm việc thủ công. Với sự hỗ trợ của **AI, Zillow API và Airtable**, các sếp có thể:
✔ **Tìm kiếm và lọc** nhà đất giảm giá một cách chính xác.
✔ **Tạo script gọi điện** cá nhân hóa, tăng tỷ lệ thành công.
✔ **Phân tích thị trường** để đưa ra quyết định thông minh.
✔ **Quản lý danh sách gọi điện** một cách chuyên nghiệp.

**Hãy áp dụng ngay workflow này và bắt đầu tự động hóa giao dịch bất động sản của mình!** 🚀

---
**🔗 [Tải Workflow Nguyên Bản](https://n8n.io/workflows/3143)**
**📌 [Cài Đặt n8n Self-hosted](https://docs.n8n.io/)**