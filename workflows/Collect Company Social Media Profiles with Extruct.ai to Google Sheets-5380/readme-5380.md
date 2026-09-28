---
title: "🚀 Tự Động Hóa Thu Thập & Tích Hợp Thông Tin Mạng Xã Hội Công Ty Với Extruct.ai → Google Sheets (Không Code)"
description: "Giải pháp tự động hóa 100% không cần code để thu thập, enrich và lưu trữ thông tin mạng xã hội của công ty từ tên miền, địa chỉ email, hoặc tên công ty vào Google Sheets. Tiết kiệm thời gian nghiên cứu thị trường lên đến 90% so với phương pháp thủ công."
slug: "tieu-thap-thong-tin-cong-ty-tu-extruct-ve-google-sheets"
tags: [n8n, automation, lead-generation, ai-summarization, google-sheets, extruct-ai, no-code]
keywords: [tự động hóa n8n, thu thập thông tin công ty, enrich data, google sheets automation, extruct ai, lead generation, market research]
---

# 🚀 **Tự Động Hóa Thu Thập & Tích Hợp Thông Tin Mạng Xã Hội Công Ty Với Extruct.ai → Google Sheets**

## **🔍 Nỗi Đau Của Các Sếp Trong Nghiên Cứu Thị Trường**
Bạn đã bao giờ phải mất **từ 2-5 giờ** để thu thập thông tin về các công ty như:
- **Mạng xã hội** (LinkedIn, Facebook, Twitter, Instagram)?
- **Địa chỉ email chính thức**?
- **Sản phẩm/dịch vụ**?
- **Thông tin liên hệ** (CEO, địa chỉ văn phòng)?
- **Đánh giá từ khách hàng**?

Với phương pháp **thủ công**, bạn phải:
❌ **Scraping** trang web (vi phạm chính sách của nhiều trang).
❌ **Tra cứu thủ công** trên Google, LinkedIn, Crunchbase...
❌ **Làm sạch dữ liệu** (xóa trùng, format không đồng nhất).
❌ **Lưu trữ rối loạn** trên nhiều file Excel khác nhau.

**Kết quả?** Dữ liệu **không chính xác**, **lỗi thời**, và **khó quản lý** khi cần phân tích.

---
### **🎯 Giải Pháp Của Chúng Ta: Workflow Tự Động Hóa 100% Không Code**
Với **n8n + Extruct.ai**, bạn chỉ cần:
1. **Nhập tên công ty** (hoặc email, tên miền) vào form.
2. **Extruct.ai** tự động **scraping & enrich** thông tin từ **trên 100 nguồn dữ liệu** (mạng xã hội, trang web, bài đánh giá, tin tức...).
3. **Dữ liệu được tự động cập nhật** vào **Google Sheets** với **format chuẩn**, sẵn sàng phân tích.

**Kết quả:**
✅ **Tiết kiệm 90% thời gian** so với phương pháp thủ công.
✅ **Dữ liệu chính xác, cập nhật thời gian thực**.
✅ **Không cần viết code** – chỉ cần **cấu hình 10 phút**.
✅ **Hoạt động 24/7** – không cần can thiệp của con người.
✅ **Dễ dàng tích hợp** với Slack, CRM (HubSpot, Salesforce), hoặc email báo cáo tự động.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài **n8n trên VPS riêng (Self-hosted)** để tránh giới hạn của phiên bản cloud.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** – giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ sức mạnh cho workflow này)
:::

---

## **🎯 Kết Quả Các Sếp Nhận Được**
| **Lợi Ích** | **Chi Tiết** |
|-------------|------------|
| **Tiết kiệm thời gian** | Thu thập thông tin **1 công ty chỉ trong 30 giây** thay vì 1-2 giờ thủ công. |
| **Dữ liệu chính xác** | Extruct.ai **không scraping** mà lấy từ **nguồn chính thức** (mạng xã hội, trang web công ty). |
| **Cập nhật tự động** | Khi công ty **cập nhật thông tin** (ví dụ: CEO mới), dữ liệu **tự động sync** vào Sheets. |
| **Dễ dàng phân tích** | Dữ liệu được **format chuẩn** trong Sheets, sẵn sàng **visualize** bằng Looker Studio, Power BI. |
| **Hoạt động liên tục** | Workflow **chạy 24/7** mà không cần can thiệp của con người. |

---

## **🔧 Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✅ **Tài khoản Extruct.ai** (miễn phí **2,500 credit** để test).
✅ **API Key của Extruct.ai** (tạo tại [API Page](https://app.extruct.ai/api)).
✅ **Tài khoản Google** (để kết nối với Google Sheets).
✅ **Google Sheets template** (sẽ được hướng dẫn copy).
✅ **VPS (nếu tự host)** – **Không bắt buộc** nhưng **khuyến khích** để workflow chạy 24/7.

---
## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/5380](https://n8n.io/workflows/5380).
2. **Nhấp vào "Import"** trong n8n Editor.
3. **Chọn file JSON** và nhấn **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Mở n8n Editor** và tạo **workflow mới**.
2. **Nhấn "Import"** → **"From JSON"**.
3. **Dán JSON** từ [đây](https://n8n.io/workflows/5380) và nhấn **Import**.

---
### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**

#### **🔹 Bước 1: Cấu Hình Extruct.ai**
1. **Tạo tài khoản Extruct.ai** tại [www.extruct.ai](https://www.extruct.ai/) (miễn phí **2,500 credit**).
2. **Tạo API Key**:
   - Mở [API Page](https://app.extruct.ai/api).
   - Nhấn **"Create New Token"** và sao lưu **Bearer Token**.
3. **Cấu hình HTTP Request nodes**:
   - Mở **3 node HTTP Request** trong workflow (`Enrich form input`, `Get status`, `Get data`).
   - Trong **Authentication**, chọn **httpBearerAuth**.
   - Nhập **Bearer Token** vừa tạo vào **Value** của `httpBearerAuth`.

#### **🔹 Bước 2: Cấu Hình Google Sheets**
1. **Mở Google Sheets template**:
   - [Lấy bản template](https://docs.google.com/spreadsheets/d/1eeQ7VIbZ94z2ji9NqRT0bXS8bNtixWbUDopOQeM005w/edit?usp=sharing).
   - **Nhấn "File" → "Make a copy"** để tạo bản sao riêng.
2. **Kết nối Google Sheets với n8n**:
   - Trong node **Google Sheets**, nhấn **"Add"** để kết nối tài khoản Google.
   - Chọn **bản sao của bạn** (không phải template gốc).
   - Chọn **operation = "appendOrUpdate"**.
3. **Cấu hình Table ID của Extruct**:
   - Mở [Extruct table template](https://app.extruct.ai/tables/shared/VfGemEC1BujAIJx8).
   - **Tìm ID Table** trong URL (ví dụ: `VfGemEC1BujAIJx8`).
   - Trong node **Set Variables**, tìm **key `tableId`** và điền **ID Table** vừa copy.

#### **🔹 Bước 3: Match Output Columns**
1. **Chạy workflow 1 lần với dữ liệu mẫu** (ví dụ: nhập tên công ty "TinoHost").
2. **Sau khi chạy**, mở **Google Sheets** và kiểm tra:
   - Các **cột mới** sẽ tự động xuất hiện (nếu không, **refresh** lại).
3. **Kéo và thả (drag & drop)** các trường từ **input form** vào **cột tương ứng** trong Sheets:
   - Ví dụ: `companyName` → **Cột "Tên Công Ty"**.
   - `email` → **Cột "Email"**.
   - `socialMedia` → **Cột "Mạng Xã Hội"**.
4. **Đặt "Column to match on" = "Company name"** (để tránh trùng lặp).

#### **🔹 Bước 4: Format Dữ liệu (Node Code)**
1. Mở node **Format last input** (type: `code`).
2. **Sửa code** để đảm bảo dữ liệu được **format chuẩn** (nếu cần):
   ```javascript
   // Ví dụ: Chuyển đổi JSON thành format dễ đọc
   return {
     json: {
       ...node.inputData[0].json,
       formattedData: JSON.stringify(node.inputData[0].json.data, null, 2)
     }
   };
   ```
   *(Nếu không cần thay đổi, bỏ qua bước này.)*

---
### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run**:
   - Nhấn **"Execute"** với **dữ liệu mẫu** (ví dụ: tên công ty "Google").
   - Kiểm tra **Google Sheets** xem dữ liệu có xuất hiện không.
2. **Bật Active**:
   - Chuyển **switch** từ **"Inactive"** sang **"Active"**.
3. **Sử dụng Form**:
   - Mở **URL Form** (được hiển thị trong node `formTrigger`).
   - Nhập **tên công ty** và nhấn **Submit**.
   - **Dữ liệu sẽ tự động cập nhật** vào Sheets trong **vài giây**.

---

## **✍️ Mẹo & Gợi Ý Nâng Cao**

### **🔹 Tích Hợp Slack/Telegram Báo Cáo Kết Quả**
- **Cài node Slack/Telegram** sau node `Import to Sheets`.
- **Gửi thông báo** khi có dữ liệu mới:
  ```json
  {
    "text": `📊 Thông tin công ty "${companyName}" đã được enrich!\n🔗 Xem chi tiết: ${googleSheetsUrl}`
  }
  ```

### **🔹 Lưu Log Lịch Sử Thu Thập**
- **Thêm node `Set`** sau `Import to Sheets` để lưu **thời gian, người thực hiện**:
  ```json
  {
    "timestamp": new Date().toISOString(),
    "user": "admin@example.com",
    "company": node.inputData[0].json.companyName
  }
  ```
- **Dùng node `googleSheets`** để ghi vào **bảng log** riêng.

### **🔹 Gửi Báo Cáo Định Kỳ (Hàng Tuần/Hàng Tháng)**
- **Sử dụng node `Set` + `googleSheets`** để **tính tổng, lọc dữ liệu**.
- **Gửi email tự động** bằng **node `email`** hoặc **Slack alert**.

### **🔹 Tích Hợp Với CRM (HubSpot, Salesforce)**
- **Thay thế node `googleSheets`** bằng **node `hubspot`** hoặc **`salesforce`**.
- **Cập nhật thông tin công ty** trực tiếp vào CRM.

---
## **📌 Kết Luận: Bắt Đầu Tự Động Hóa Ngay Hôm Nay!**

### **🚀 Tại Sao Các Sếp Nên Sử Dụng Workflow Này?**
| **Phương Pháp** | **Thời Gian** | **Chính Xác** | **Khó Khăn** | **Tự Động** |
|----------------|--------------|--------------|-------------|------------|
| **Thủ Công** | 1-5 giờ/công ty | ❌ Thấp | ❌ Scraping vi phạm pháp luật | ❌ Không |
| **Extruct + n8n** | **30s/công ty** | ✅ Cao (dữ liệu từ nguồn chính thức) | ❌ Không cần code | ✅ 24/7 |

### **🔥 Bước Đầu Tiên: Cài Đặt & Test**
1. **Tạo tài khoản Extruct.ai** ([Đăng ký miễn phí](https://www.extruct.ai/)).
2. **Import workflow** vào n8n.
3. **Chạy test** với **1-2 công ty** (ví dụ: "TinoHost", "FPT").
4. **Kiểm tra Google Sheets** xem dữ liệu có xuất hiện không.

### **💡 Nếu Có Vấn Đề?**
- **Trung tâm hỗ trợ Extruct.ai**: [Chat trên website](https://www.extruct.ai/chat).
- **Community n8n**: [Discord n8n](https://discord.gg/n8n).
- **TinoHost**: [Hỗ trợ VPS](https://tino.vn/support) (nếu tự host).

---
### **🎁 Bonus: Tăng Cường Dữ liệu với Extruct Pro**
- **2,500 credit miễn phí** đã đủ để test.
- **Nâng cấp Extruct Pro** (từ **$29/month**) để:
  - **Thu thập nhiều công ty hơn** (không giới hạn credit).
  - **Lấy dữ liệu từ nhiều nguồn sâu hơn** (ví dụ: tin tức, bài đánh giá chi tiết).

---
**🚀 Hành động ngay hôm nay!**
**Tiết kiệm 90% thời gian nghiên cứu thị trường** và **cập nhật dữ liệu công ty một cách tự động** – **không cần viết code!**

**[Bắt đầu với Extruct.ai → n8n → Google Sheets](https://www.extruct.ai/)**