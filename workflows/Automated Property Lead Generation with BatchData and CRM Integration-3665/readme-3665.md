---
title: "🏢 **Tự Động Hóa Sản Xuất Dữ Liệu Tiềm Năng Bất Động Sản với BatchData + CRM - Không Cần Code!**"
description: "Workflow tự động hóa tìm kiếm, lọc và phân tích bất động sản tiềm năng hàng ngày, gửi báo cáo chi tiết qua Email và Slack cho đội ngũ bán hàng. Giúp doanh nghiệp tiết kiệm 10+ giờ/ngày và tăng hiệu quả bán hàng 30%."
slug: "tieu-dong-hoa-san-xuat-du-lieu-tien-nganh-bat-dong-san"
tags: [n8n, automation, sales, crm, batchdata, ai, no-code, email-automation, slack-integration]
keywords: [tự động hóa bất động sản, workflow n8n bán hàng, tìm kiếm bất động sản tiềm năng, tự động hóa CRM, batchdata api, email alert bất động sản, slack notification sales]
---

# 🚀 **Tự Động Hóa Sản Xuất Dữ Liệu Tiềm Năng Bất Động Sản - Giúp Đội Ngũ Bán Hàng "Ngủ Ngon" Mỗi Ngày**

### **Nỗi Đau Của Các Sếp Bất Động Sản**
Hàng ngày, đội ngũ bán hàng phải:
- **Tìm kiếm thủ công** trên các trang web bất động sản (Batdongsan.vn, Sohouse.vn,...) để cập nhật danh sách nhà đất mới.
- **Lọc và đánh giá** hàng trăm tài sản dựa trên tiêu chí như **tỷ lệ vốn tự do cao, chủ sở hữu vắng mặt, vị trí chiến lược** - công việc tẻ nhạt và dễ sai sót.
- **Gửi báo cáo** qua Email hoặc Slack cho các thành viên trong team, nhưng thường **quên hoặc làm trễ** do nhiều công việc khác.
- **Mất thời gian** để tra cứu chi tiết (giá, diện tích, vị trí) của mỗi tài sản, khi mà **thời gian là tiền bạc** trong ngành bất động sản.

**Kết quả?** Đội ngũ bán hàng **mệt mỏi**, **chậm phản ứng**, và **chưa tối ưu hóa** cơ hội bán hàng tiềm năng.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
Sau khi áp dụng workflow này, các sếp sẽ:
✅ **Tiết kiệm 10-15 giờ/ngày** cho đội ngũ bán hàng (không cần tìm kiếm thủ công).
✅ **Lọc ra 100% tài sản tiềm năng** (tỷ lệ vốn tự do >30%, chủ sở hữu vắng mặt, vị trí hot) **một cách chính xác**.
✅ **Nhận báo cáo chi tiết** (giá, diện tích, vị trí, liên hệ chủ sở hữu) **tự động gửi qua Email và Slack** mỗi sáng.
✅ **Tăng hiệu quả bán hàng 30%** nhờ **cập nhật dữ liệu thời gian thực** và **các cơ hội được ưu tiên** dựa trên tiêu chí kinh doanh.
✅ **Hoạt động 24/7** - không phụ thuộc vào giờ làm việc của con người.

---
### **🔧 Yêu Cầu Cần Thiết**
Để workflow này hoạt động, các sếp cần chuẩn bị:
📌 **API Key BatchData** (dùng để truy vấn dữ liệu bất động sản).
📌 **Tài khoản SMTP** (để gửi Email tự động, ví dụ: Gmail, SendGrid, hoặc SMTP của nhà cung cấp hosting).
📌 **Credentials Slack** (để gửi thông báo vào kênh team).
📌 **Danh sách Email** của các thành viên trong đội ngũ bán hàng (để nhận báo cáo hàng ngày).

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để tránh giới hạn của phiên bản miễn phí.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. Tải workflow từ [đây](https://n8n.io/workflows/3665) (ấn nút **"Export"**).
2. Trên **n8n Editor**, nhấn **"Import"** và chọn file JSON vừa tải.
3. Chọn **"Import"** để hoàn tất.

#### **Phương pháp 2: Copy/Paste JSON**
1. Trên trang workflow gốc, nhấn **"Export"** để lấy mã JSON.
2. Trên **n8n Editor**, nhấn **"Import"** → **"Paste JSON"** và dán mã vào.
3. Chọn **"Import"** để hoàn tất.

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**

#### **🔹 Node 1: Schedule Market Scan (scheduleTrigger)**
- **Cấu hình lịch chạy**: Đặt thời gian chạy hàng ngày (ví dụ: **7h sáng** để báo cáo được gửi trước khi bắt đầu làm việc).
- **Lưu ý**: Nếu dùng phiên bản miễn phí, chỉ chạy được **1 lần/ngày**.

#### **🔹 Node 2: BatchData API Configuration (set)**
- **Thêm API Key**:
  - Nhấn **"Add"** trong node này.
  - Chọn **"BatchData API Key"** (nếu chưa có, tạo tại [BatchData](https://batchdata.io/)).
  - Điền **API Key** vào trường `apiKey`.
- **Cấu hình tiêu chí tìm kiếm**:
  - Thay đổi `location`, `propertyType`, `minEquityPercentage` (ví dụ: `minEquityPercentage: 30` để lọc tài sản có vốn tự do >30%).

#### **🔹 Node 3 & 4: Query BatchData Properties (httpRequest) + Get Previous Results (code)**
- **Node `httpRequest`**:
  - Đảm bảo **API Key** đã điền đúng trong node `BatchData API Configuration`.
  - Kiểm tra **URL API** của BatchData (nếu cần thay đổi, cập nhật ở đây).
- **Node `code` (Get Previous Results)**:
  - Đây là **lógica so sánh** giữa dữ liệu mới và cũ.
  - **Không cần chỉnh sửa** trừ khi muốn thay đổi cách so sánh (ví dụ: thêm tiêu chí mới).

#### **🔹 Node 5: Compare Results (code)**
- **Lógica mặc định** đã lọc ra tài sản **mới** hoặc **có thay đổi** (ví dụ: giá giảm, chủ sở hữu thay đổi).
- **Không cần chỉnh sửa** trừ khi muốn thay đổi tiêu chí so sánh.

#### **🔹 Node 6: Split Properties (splitOut)**
- **Chia dữ liệu** thành các tài sản riêng lẻ để lọc và xử lý.
- **Không cần chỉnh sửa**.

#### **🔹 Node 7: Filter High Potential (filter)**
- **Tiêu chí mặc định**:
  - `equityPercentage > 30` (tỷ lệ vốn tự do >30%).
  - `absenteeOwner: true` (chủ sở hữu vắng mặt).
  - `priceDrop: true` (giá giảm).
- **Cách chỉnh sửa**:
  - Nhấn **"Edit"** trong node này.
  - Thay đổi `jsonpath` hoặc `condition` để phù hợp với chiến lược kinh doanh của doanh nghiệp.

#### **🔹 Node 8: Get Property Details (httpRequest)**
- **Lấy chi tiết** của mỗi tài sản (giá, diện tích, vị trí, liên hệ chủ sở hữu).
- **Không cần chỉnh sửa** trừ khi BatchData thay đổi API.

#### **🔹 Node 9: Format Email Content (set)**
- **Định dạng nội dung Email**:
  - Thay đổi `subject`, `body` để phù hợp với brand của doanh nghiệp.
  - Thêm **Google Maps link** (nếu cần) bằng cách sử dụng `{{ $node["Get Property Details"].jsonpath("$.location.googleMapsUrl") }}`.

#### **🔹 Node 10: Send Email Alert (emailSend)**
- **Cấu hình SMTP**:
  - Nhấn **"Add"** → **"SMTP"**.
  - Điền:
    - **Host**: `smtp.gmail.com` (nếu dùng Gmail).
    - **Port**: `587`.
    - **Username**: Email của bạn.
    - **Password**: App Password (nếu dùng Gmail, tạo tại [My Account](https://myaccount.google.com/apppasswords)).
  - **Người nhận**: Thay đổi `to` thành danh sách Email của đội ngũ bán hàng (ví dụ: `["team@doanhnghiep.com"]`).

#### **🔹 Node 11: Post to Slack (slack)**
- **Cấu hình Slack**:
  - Nhấn **"Add"** → **"Slack"**.
  - Chọn **workspace** và **channel** (ví dụ: `#bds-leads`).
  - **Thêm token**: Tạo tại [Slack API](https://api.slack.com/apps) và chọn **"Bot Token"**.
  - **Thay đổi message format** (nếu muốn thay đổi cách hiển thị thông báo).

---

### **3. Kích Hoạt ⚡️**
1. **Test Run** (kiểm tra trước khi chạy thực tế):
   - Nhấn **"Run Workflow"** và chọn **1 tài sản mẫu** để kiểm tra Email và Slack.
   - Kiểm tra **Email** và **Slack** để đảm bảo nội dung đúng.
2. **Bật Active**:
   - Sau khi test thành công, nhấn **"Active"** ở góc trên bên phải.

---

## **✍️ Mẹo & Gợi Ý Nâng Cao**

### **1. Kết Hợp với CRM (HubSpot, Pipedrive, Salesforce)**
- **Sử dụng node `httpRequest`** để gửi dữ liệu tiềm năng vào CRM.
- **Cách làm**:
  - Thêm node `httpRequest` sau `Send Email Alert`.
  - Cấu hình **API Key của CRM** và **endpoint** (ví dụ: `POST /api/v1/leads`).
  - **Lưu ý**: Các CRM thường có API khác nhau, cần tham khảo [đọc tài liệu](https://developers.hubspot.com/docs/api/crm/leads).

### **2. Lưu Log Dữ Liệu (Google Sheets hoặc Airtable)**
- **Sử dụng node `googleSheets`** để lưu tất cả dữ liệu tiềm năng vào bảng Excel.
- **Cách làm**:
  - Thêm node `googleSheets` sau `Filter High Potential`.
  - Chọn **Sheet** và **range** (ví dụ: `Sheet1!A1`).
  - **Lợi ích**: Dễ dàng theo dõi lịch sử và phân tích dữ liệu dài hạn.

### **3. Gửi Báo Cáo Định Kỳ (Tuần/Tháng)**
- **Sử dụng node `scheduleTrigger`** để chạy workflow hàng tuần/tháng.
- **Cách làm**:
  - Thêm node `scheduleTrigger` mới.
  - Cấu hình **lịch chạy** (ví dụ: **Mỗi thứ 2 sáng 8h**).
  - **Thêm node `emailSend`** để gửi báo cáo tổng hợp.

### **4. Thêm Tiêu Chí Tùy Chỉnh**
- **Ví dụ**: Lọc tài sản có **vị trí gần trường học** hoặc **căn hộ cao cấp**.
- **Cách làm**:
  - Chỉnh sửa `filter` trong node `Filter High Potential`.
  - Thêm điều kiện mới (ví dụ: `{{ $json["schoolDistance"] }} < 500`).

### **5. Tích Hợp với Google Maps (Hiển Thị Trên Bản Đồ)**
- **Sử dụng node `set`** để thêm link Google Maps vào Email/Slack.
- **Cách làm**:
  - Trong node `Format Email Content`, thêm:
    ```json
    "googleMapsUrl": "https://www.google.com/maps?q={{ $node["Get Property Details"].jsonpath("$.latitude") }},{{ $node["Get Property Details"].jsonpath("$.longitude") }}"
    ```

---

## **📌 Kết Luận**
Workflow này **giải phóng đội ngũ bán hàng** khỏi công việc tẻ nhạt, **tăng hiệu quả bán hàng** nhờ dữ liệu chính xác và **tự động hóa hoàn toàn** quá trình tìm kiếm, lọc và báo cáo.

**Hành động ngay hôm nay:**
1. **Cài đặt n8n trên VPS** (để workflow chạy 24/7).
2. **Import workflow** và **cấu hình API Key, Email, Slack**.
3. **Bật Active** và **nhận báo cáo hàng ngày**!

**🚀 Chúc các sếp thành công với chiến lược bán hàng tự động hóa!** 🏢💼

---
**🔗 [Xem workflow gốc](https://n8n.io/workflows/3665) | [Tải file JSON](https://n8n.io/workflows/3665/export)**