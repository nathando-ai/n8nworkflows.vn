---
title: "📊 Tự Động Hóa Báo Cáo Doanh Thu Hàng Ngày Từ Google Sheets Sang WhatsApp - Không Cần Code"
description: "Giải pháp tự động hóa hoàn toàn miễn phí giúp các sếp nhận báo cáo doanh thu hàng ngày qua WhatsApp từ Google Sheets, tiết kiệm 2+ giờ làm thủ công mỗi tuần. Kết hợp với MoltFlow để gửi tin nhắn cá nhân hóa, chính xác và hoạt động tự động 24/7."
slug: "tu-dong-hoa-bao-cao-doanh-thu-whatsapp-google-sheets"
tags: [n8n, automation, CRM, GoogleSheets, WhatsApp, MoltFlow]
keywords: [tự động hóa báo cáo doanh thu, n8n workflow, gửi báo cáo qua WhatsApp, tự động hóa Google Sheets, CRM tự động]
---

# 🚀 **Tự Động Hóa Báo Cáo Doanh Thu Hàng Ngày Từ Google Sheets Sang WhatsApp**

### **🔥 Nỗi Đau Của Các Sếp?**
- **Làm thủ công báo cáo doanh thu hàng ngày?** Tốn thời gian, dễ sai sót, và không thể cập nhật liên tục.
- **Không biết cách kết nối Google Sheets với WhatsApp?** Cần một giải pháp đơn giản, không cần code.
- **Muốn báo cáo tự động nhưng không muốn trả phí?** Workflow này hoàn toàn miễn phí và tự động hóa hoàn toàn.

**Giải pháp của chúng tôi:**
Workflow này **tự động** lấy dữ liệu doanh thu từ Google Sheets, tính toán tổng doanh thu, số lượng đơn hàng và sản phẩm bán chạy nhất, rồi gửi báo cáo dưới dạng tin nhắn WhatsApp **mỗi ngày lúc 6h chiều**. Dùng **MoltFlow** để gửi tin nhắn một cách cá nhân hóa và chuyên nghiệp.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 2+ giờ/ngày** làm thủ công báo cáo.
- **Dữ liệu chính xác 100%** từ Google Sheets, không sai sót.
- **Báo cáo tự động** mỗi ngày lúc 6h chiều, không quên.
- **Cá nhân hóa tin nhắn** với MoltFlow, dễ đọc và chuyên nghiệp.
- **Hoạt động liên tục** 24/7, không cần can thiệp.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản MoltFlow** (đăng ký tại [molt.waiflow.app](https://molt.waiflow.app)).
2. **Tài khoản Google Sheets** với bảng dữ liệu có các cột:
   - **Date** (Ngày)
   - **Product** (Sản phẩm)
   - **Amount** (Số lượng/Doanh thu)
   - **Customer** (Khách hàng)
3. **API Key của MoltFlow** (để gửi tin nhắn WhatsApp).
4. **Credentials OAuth2 cho Google Sheets** (để n8n đọc dữ liệu).
5. **Số điện thoại WhatsApp** của người nhận báo cáo.

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [link gốc](https://n8n.io/workflows/13486) và import vào n8n Editor.
- **Cách 2:** Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/13486) và paste vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **5 node** chính. Dưới đây là hướng dẫn chi tiết:

##### **Node 1: Every Day 6 PM (scheduleTrigger)**
- **Chức năng:** Khởi động workflow hàng ngày lúc 6h chiều.
- **Lưu ý:** Không cần chỉnh sửa gì, chỉ cần **bật Active**.

##### **Node 2: Read Sales Data (googleSheets)**
- **Chức năng:** Đọc dữ liệu từ Google Sheets.
- **Cấu hình:**
  - **Credentials:** Chọn `googleSheetsOAuth2Api` (đã cấu hình trước khi import).
  - **Sheet URL:** Điền link của Google Sheet (ví dụ: `https://docs.google.com/spreadsheets/d/.../edit`).
  - **Range:** Điền `Sheet1!A:D` (hoặc tên sheet và phạm vi cột của bạn).
  - **Operation:** Đảm bảo chọn `read`.

##### **Node 3: Build Report (code)**
- **Chức năng:** Xử lý logic tính toán và xây dựng nội dung báo cáo.
- **Lưu ý:** Các sếp **phải chỉnh sửa mã JavaScript** trong node này:
  ```javascript
  // Thay thế các biến sau:
  const YOUR_SESSION_ID = "your_moltflow_session_id"; // Lấy từ MoltFlow
  const YOUR_PHONE = "0123456789"; // Số điện thoại WhatsApp của bạn (không dấu)
  const sheetData = $input.all(); // Dữ liệu từ Google Sheets

  // Tính toán tổng doanh thu, số đơn hàng và sản phẩm bán chạy
  const totalRevenue = sheetData.reduce((sum, row) => sum + parseFloat(row.Amount), 0);
  const orderCount = sheetData.length;
  const topProduct = sheetData.reduce((max, row) => row.Amount > max.Amount ? row : max, sheetData[0]);

  // Xây dựng tin nhắn báo cáo
  const message = `
  📊 **BÁO CÁO DOANH THU HÔM NAY**
  📅 Ngày: ${new Date().toLocaleDateString('vi-VN')}

  💰 **Tổng Doanh Thu:** ${totalRevenue.toLocaleString()} VNĐ
  📦 **Số Đơn Hàng:** ${orderCount}
  🏆 **Sản Phẩm Bán Chạy:** ${topProduct.Product} (${topProduct.Amount} đơn)
  `;

  return { json: { message } };
  ```
  - **Lưu ý:** Đảm bảo cột `Amount` trong Google Sheets là số (không phải văn bản).

##### **Node 4: Send Report via WhatsApp (httpRequest)**
- **Chức năng:** Gửi tin nhắn WhatsApp bằng MoltFlow API.
- **Cấu hình:**
  - **Method:** POST
  - **URL:** `https://api.molt.waiflow.app/send`
  - **Headers:**
    - `Content-Type: application/json`
    - `X-API-Key: YOUR_MOLTFLOW_API_KEY` (điền API Key từ MoltFlow).
  - **Body (JSON):**
    ```json
    {
      "session_id": "{{ $node["Build Report"].json.message.YOUR_SESSION_ID }}",
      "phone": "{{ $node["Build Report"].json.message.YOUR_PHONE }}",
      "message": "{{ $node["Build Report"].json.message }}"
    }
    ```
  - **Credentials:** Chọn `httpHeaderAuth` (đã cấu hình trước).

##### **Node 5: Done (code)**
- **Chức năng:** Node này không cần chỉnh sửa, chỉ để kết thúc workflow.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run:** Chạy workflow với dữ liệu mẫu để kiểm tra:
   - Kiểm tra **Node 2** có đọc dữ liệu từ Google Sheets không.
   - Kiểm tra **Node 3** có tính toán đúng không.
   - Kiểm tra **Node 4** có gửi tin nhắn WhatsApp thành công không.
2. **Bật Active:** Sau khi test thành công, **bật Active** workflow.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Thêm Logs:** Sử dụng node `stickyNote` để ghi lại lỗi hoặc thông báo debug.
2. **Gửi Báo Cáo Định Kỳ:** Thay đổi thời gian trong `scheduleTrigger` (ví dụ: 8h sáng) nếu muốn nhận báo cáo sớm hơn.
3. **Kết Nối Slack/Email:** Sử dụng node `slack` hoặc `email` để gửi báo cáo đồng thời.
4. **Lưu Lịch Sử:** Sử dụng node `googleDrive` để lưu báo cáo hàng ngày vào một file Excel.
5. **Cá Nhân Hóa Tin Nhắn:** Thêm thông tin khách hàng hoặc sản phẩm đặc biệt vào tin nhắn.

---
### 📌 **Kết Luận**
Workflow này giúp các sếp **tự động hóa hoàn toàn** quá trình báo cáo doanh thu, tiết kiệm thời gian và giảm thiểu sai sót. **Chỉ cần 5 phút setup**, sau đó workflow sẽ hoạt động tự động mỗi ngày.

**Hành động ngay:**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test run** để đảm bảo hoạt động đúng.
3. **Bật Active** và **quên đi việc báo cáo thủ công!**

👉 **Bắt đầu tự động hóa ngay [tại đây](https://n8n.io/workflows/13486)**!