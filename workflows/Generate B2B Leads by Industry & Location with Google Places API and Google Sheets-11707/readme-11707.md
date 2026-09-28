---
title: "🚀 Tự Động Sinh Ra Danh Bạ Lead B2B Theo Ngành Hàng & Địa Phân Biệt Với Google Places API + Google Sheets"
description: "Workflow này tự động tìm kiếm, trích xuất và lưu trữ thông tin chi tiết (tên công ty, điện thoại, website, địa chỉ) của các doanh nghiệp B2B theo ngành nghề và vị trí địa lý từ Google Maps, giúp các sếp tiết kiệm hàng giờ công sức tra cứu thủ công mỗi tháng. Kết quả là danh sách lead sạch, cập nhật và sẵn sàng để outreach."
slug: "tieu-dong-sinh-ra-danh-ba-lead-b2b-google-places-api"
tags: [n8n, automation, lead-generation, google-places-api, google-sheets, no-code]
keywords: [tự động hóa lead B2B, tìm kiếm doanh nghiệp theo ngành, Google Places API n8n, tự động hóa tra cứu địa chỉ, workflow lead generation]
---

# 🚀 **Tự Động Sinh Ra Danh Bạ Lead B2B Theo Ngành & Địa Phân Biệt – Không Cần Code**

### **Nỗi Đau Của Các Sếp Hiện Nay**
Hàng tháng, các sếp và đội ngũ marketing/sales phải mất **từ 5-10 giờ** để tra cứu thủ công danh sách doanh nghiệp B2B theo ngành nghề và vị trí địa lý (ví dụ: "Công ty kế toán tại Hà Nội" hoặc "Cơ sở sản xuất dược phẩm tại TP.HCM"). Thông tin thu thập được thường **không đầy đủ, lỗi thời, hoặc trùng lặp**, khiến quá trình outreach trở nên **chậm chạp và không hiệu quả**.

Workflow này **giải quyết tất cả** bằng cách:
✅ **Tự động tìm kiếm** trên Google Maps với **3 trang kết quả** (tránh bỏ sót).
✅ **Trích xuất thông tin chi tiết** (tên công ty, điện thoại, website, địa chỉ) trong **vài giây**.
✅ **Lưu trữ tự động** vào Google Sheets với **cấu trúc sạch**, sẵn sàng để xuất khẩu hoặc tích hợp CRM.
✅ **Hoạt động 24/7** – không cần can thiệp thủ công.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[**3 Lợi Ích Cốt Lõi**]
- **Tiết kiệm 80% thời gian** so với tra cứu thủ công (từ 10h/tháng xuống còn 2h).
- **Danh sách lead sạch** – không trùng lặp, cập nhật từ Google Maps.
- **Dữ liệu chi tiết** (điện thoại, website, địa chỉ) để outreach hiệu quả.
- **Hoạt động tự động** – chỉ cần nhập yêu cầu (ngành + địa điểm) là hệ thống làm việc.
:::

---
### **🔧 Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI CHẠY**]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Google Cloud** với:
   - **Places API** (Text Search + Place Details) được **bật và có thanh toán** (miễn phí 200$ đầu tiên).
   - **API Key** từ [Google Cloud Console](https://console.cloud.google.com/).
2. **Tài khoản Google Sheets** với:
   - **OAuth 2.0** được cấu hình trong n8n (hướng dẫn [đây](https://docs.n8n.io/integrations/builtins/nodes/n8n-nodes-base.googleSheets.html#credentials)).
   - **Bảng tính mới** có **4 cột** (tên công ty, điện thoại, website, địa chỉ).
3. **n8n Self-hosted** (không dùng phiên bản cloud để tránh giới hạn API).

👉 **🎁 Mã giảm giá VPS cho n8n (Self-hosted)**
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) với mã **VPSN8N** (giảm tới 39%).
👉 [VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (ổn định cho workflow).
:::

---
### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/11707](https://n8n.io/workflows/11707) hoặc copy/paste JSON từ trang này.
- Trong **n8n Editor**, nhấn **Import** và dán JSON vào.
- **Kích hoạt chế độ "Active"** sau khi import.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **13 node** với logic phân chia rõ ràng. Các bước quan trọng cần điều chỉnh:

##### **A. Cấu Hình API Key Google Places**
- **3 node HTTP Request** (`Text Search Page 1/2/3` và `Get Place Details`) **cần điền API Key** vào header:
  ```json
  {
    "Authorization": "Bearer YOUR_API_KEY_HERE"
  }
  ```
  - **Lấy API Key** từ [Google Cloud Console](https://console.cloud.google.com/apis/credentials).
  - **Không quên bật 2 API**:
    - **Places API** (Text Search + Place Details).
    - **Bật thanh toán** để tránh bị giới hạn.

##### **B. Cấu Hình Google Sheets**
- **Node `Append rows in the Google Sheet`** cần:
  - **`documentId`**: ID của file Google Sheets (tham khảo [hướng dẫn lấy ID](https://support.google.com/docs/answer/1052017)).
  - **`sheetName`**: Tên sheet (ví dụ: "Lead_B2B").
  - **Credentials**: Chọn OAuth 2.0 đã cấu hình trước.

##### **C. Cấu Hình Form Trigger (Yêu Cầu Input)**
- **Node `Submit Search Query`** (Form Trigger) sẽ **yêu cầu người dùng nhập**:
  - **Ngành nghề** (ví dụ: "Công ty kế toán").
  - **Địa điểm** (ví dụ: "Hà Nội").
- **Kết quả**: Workflow sẽ tự động tìm kiếm và lưu trữ dữ liệu.

##### **D. Thời Gian Chờ (Wait Nodes)**
- **2 node `Wait 5s`** giữa các trang kết quả để **tránh bị giới hạn API quota**.
  - Nếu gặp lỗi `next_page_token` không hoạt động, **tăng thời gian chờ lên 10s**.

---
#### **3. Kích Hoạt & Test 🔥**
1. **Test Run** với một query nhỏ (ví dụ: "Công ty luật TP.HCM").
2. **Kiểm tra Google Sheets** để xem dữ liệu đã được append chưa.
3. **Bật chế độ Active** nếu test thành công.

---
### **✍️ Mẹo & Gợi Ý Nâng Cao**
:::info[**CÁCH LÀM HƠN HIỆU QUẢ**]
1. **Thêm Node Email/Slack** để **báo cáo kết quả** khi workflow hoàn thành:
   - Sử dụng node `n8n-nodes-base.email` hoặc `n8n-nodes-base.slack` sau node `Append rows in the Google Sheet`.
   - Ví dụ: Gửi email tổng hợp danh sách lead mới mỗi ngày.

2. **Lọc & Dedupe Dữ Liệu**:
   - Thêm node `n8n-nodes-base.filter` trước khi append vào Sheets để **loại bỏ trùng lặp**.
   - Cấu hình điều kiện: `json["name"] !== previousItem.json["name"]`.

3. **Tích Hợp CRM**:
   - Sau khi dữ liệu ở Sheets, sử dụng node `n8n-nodes-base.httpRequest` để **push vào HubSpot, Salesforce, hoặc CRM khác**.
   - Ví dụ: Gửi dữ liệu JSON sang API của CRM với header `Content-Type: application/json`.

4. **Tăng Số Trang Kết Quả**:
   - Hiện workflow hỗ trợ **3 trang**, nhưng có thể **thêm node `Wait` và `Text Search`** để lấy thêm trang 4, 5 nếu cần.

5. **Lưu Log & Monitoring**:
   - Thêm node `n8n-nodes-base.stickyNote` để ghi lại **thời gian chạy, số lead tìm thấy, và lỗi (nếu có)**.
   - Dùng node `n8n-nodes-base.httpRequest` để **gửi log lên Google Drive hoặc Notion**.
:::

---
### **📌 Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc tra cứu lead thủ công, đồng thời **cung cấp dữ liệu chính xác và chi tiết** để outreach hiệu quả. **Chỉ cần nhập ngành + địa điểm**, hệ thống sẽ tự động làm việc 24/7!

👉 **Bắt đầu ngay**:
1. **Cài đặt n8n Self-hosted** trên VPS (sử dụng mã giảm giá **VPSN8N**).
2. **Import workflow** và cấu hình API Key, Google Sheets.
3. **Test với query đầu tiên** và **bắt đầu tự động hóa lead B2B**!

---
**💡 Gợi Ý Tiếp Theo**:
- **Kết hợp với AI** (n8n + LLM) để **tự động phân loại lead** theo độ ưu tiên.
- **Tự động gửi email outreach** bằng node `n8n-nodes-base.email` sau khi lead được tìm thấy.
- **Tạo dashboard** bằng Google Data Studio để theo dõi số lead mới mỗi tháng.

**Chúc các sếp thành công!** 🚀