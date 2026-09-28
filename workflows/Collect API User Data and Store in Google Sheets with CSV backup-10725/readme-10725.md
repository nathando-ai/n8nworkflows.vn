---
title: "🚀 Tự Động Hóa Lấy Dữ Liệu Người Dùng từ API & Lưu Trữ Trên Google Sheets Với Backup CSV - Không Cần Code"
description: "Workflow tự động hóa hoàn toàn lấy dữ liệu người dùng từ API bất kỳ (ví dụ: RandomUser API), xử lý và lưu vào Google Sheets với 2 cột: Tên & Quốc gia, đồng thời tạo bản sao lưu CSV tự động. Giúp các sếp tiết kiệm thời gian, tránh sai sót thủ công và dễ dàng chia sẻ dữ liệu."
slug: "tieu-dong-hoa-lay-du-lieu-nguoi-dung-tu-api-luu-tren-google-sheets"
tags: [n8n, automation, no-code, google-sheets, api-integration, csv-backup]
keywords: [n8n workflow tự động hóa API, lưu dữ liệu Google Sheets, backup CSV tự động, tự động hóa không cần code, lấy dữ liệu người dùng từ API]
---

# 🚀 **Tự Động Hóa Lấy Dữ Liệu Người Dùng từ API & Lưu Trữ Trên Google Sheets Với Backup CSV**

## **💡 Giải Pháp Cho Những Ai?**
Các sếp và đội ngũ IT/Marketing đang phải **làm thủ công** việc lấy dữ liệu người dùng từ API (ví dụ: danh sách khách hàng, thành viên, hoặc mẫu dữ liệu thử nghiệm như RandomUser API) và **ghi chép vào Google Sheets**? Hoặc phải **tạo bản sao lưu CSV** để phân tích sau? **Workflow này sẽ giải quyết tất cả!**

- **Tiết kiệm thời gian**: Không cần copy-paste dữ liệu từ API sang Google Sheets.
- **Tránh sai sót**: Xử lý tự động, không bị lỗi nhân sự.
- **Backup an toàn**: Tự động tạo file CSV để lưu trữ hoặc chia sẻ.
- **Dễ mở rộng**: Thêm cột mới, lọc dữ liệu, hoặc chạy tự động theo lịch.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
✅ **Dữ liệu tự động cập nhật** trên Google Sheets mỗi khi gọi API.
✅ **Bản sao lưu CSV tự động** được tạo ra để sử dụng ngoại tuyến.
✅ **Xử lý lỗi API** (nếu API trả về lỗi, workflow sẽ dừng và báo lỗi).
✅ **Dễ dàng tùy chỉnh** để lấy dữ liệu từ bất kỳ API nào có cấu trúc JSON tương tự.
✅ **Hoàn toàn không cần code** – chỉ cần cấu hình vài bước.

---
### **🔧 Yêu Cầu Cần Thiết**
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google** và **Google Sheets OAuth2 credentials** (để kết nối với Google Sheets).
2. **API endpoint** trả về dữ liệu người dùng (ví dụ: `https://randomuser.me/api/?results=10`).
3. **Environment Variables** trong n8n:
   - `BASE_URL`: Địa chỉ API bạn muốn lấy dữ liệu (ví dụ: `https://api.example.com/users`).
   - `GOOGLE_SHEET_ID`: ID của Google Sheet bạn muốn lưu dữ liệu (có thể lấy từ URL của Sheet).
4. **Google Sheet** đã chuẩn bị với **2 cột đầu tiên là "Name" và "Country"** (hoặc tùy chỉnh theo yêu cầu).

---
### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/10725](https://n8n.io/workflows/10725) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ link trên và dán vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **7 node** chính, các sếp cần chú ý cấu hình sau:

##### **🔹 Node 1: Start Workflow Manually (Bắt Đầu Tự Động)**
- **Lưu ý**: Nếu muốn chạy tự động (ví dụ: hàng ngày), thay thế **Manual Trigger** bằng **Cron Trigger** (ví dụ: `0 0 * * *` để chạy hàng ngày lúc 00:00).

##### **🔹 Node 2: Fetch User Data from API (Lấy Dữ Liệu từ API)**
- **Cấu hình**:
  - **Method**: `GET` (hoặc `POST` nếu API yêu cầu).
  - **URL**: Điền `{{$env.BASE_URL}}` (đã thiết lập trong Environment Variables).
  - **Headers**: Nếu API yêu cầu, thêm `Authorization: Bearer {{$env.API_KEY}}` (nếu có).
  - **Test**: Click **Execute Node** để kiểm tra API trả về dữ liệu như mong đợi.

##### **🔹 Node 3: Verify API Response Success (Kiểm Tra Trả Về API)**
- **Cấu hình**:
  - **Condition**: `statusCode == 200` (kiểm tra API trả về thành công).
  - **Nếu lỗi**: Workflow sẽ **dừng và báo lỗi** (Node **Stop on API Failure**).

##### **🔹 Node 4: Transform API Data to Name and Country (Xử Lý Dữ Liệu)**
- **Lưu ý quan trọng**: Node này sử dụng **Function Node** để chuyển đổi dữ liệu từ JSON phức tạp thành dạng đơn giản.
  - **Mã JavaScript mặc định** (có thể chỉnh sửa):
    ```javascript
    // Input: Raw API JSON (ví dụ: RandomUser API)
    // Output: Array của đối tượng { name: "Tên", country: "Quốc gia" }

    const results = $input.all();
    const formattedData = results.map(user => ({
      name: `${user.name.first} ${user.name.last}`,
      country: user.location.country
    }));

    return formattedData;
    ```
  - **Tùy chỉnh**: Nếu API trả về cấu trúc khác, chỉnh sửa mã để lấy trường `name` và `country` phù hợp.

##### **🔹 Node 5: Append Data to Google Sheets (Lưu Trên Google Sheets)**
- **Cấu hình**:
  - **Credentials**: Chọn **Google Sheets OAuth2** đã thiết lập trước.
  - **Spreadsheet ID**: Điền `{{$env.GOOGLE_SHEET_ID}}`.
  - **Range**: `Sheet1!A2:B` (giả sử Sheet có tên "Sheet1" và dữ liệu bắt đầu từ hàng 2).
  - **Headers**: Đảm bảo Sheet có **2 cột đầu tiên là "Name" và "Country"** (hoặc chỉnh sửa theo cấu trúc dữ liệu của bạn).

##### **🔹 Node 6: Create CSV Backup File (Tạo File CSV Backup)**
- **Cấu hình**:
  - **File Name**: `users_backup_{{$datetime.now("YYYY-MM-DD")}}.csv` (tự động tạo tên file với ngày tháng).
  - **Headers**: Chọn `Name` và `Country` (hoặc thêm cột khác nếu đã tùy chỉnh).
  - **Lưu ý**: File CSV sẽ được tạo trong **folder "Downloads"** của máy chủ n8n (nếu self-hosted) hoặc trong **Google Drive** (nếu sử dụng n8n.cloud).

##### **🔹 Node 7: Stop on API Failure (Dừng Nếu API Lỗi)**
- **Cấu hình**: Không cần thay đổi gì, node này sẽ tự động **dừng workflow** và hiển thị lỗi nếu API trả về không thành công.

---
#### **3. Kích Hoạt ⚡️**
- **Test Run**: Click **Execute Workflow** và kiểm tra:
  - Dữ liệu có được lưu vào Google Sheets không?
  - File CSV có được tạo ra không?
  - Nếu API lỗi, workflow có dừng và báo lỗi không?
- **Bật Active**: Sau khi kiểm tra thành công, bật **Active** để workflow chạy tự động khi kích hoạt.

---
### **✍️ Mẹo & Gợi Ý Nâng Cao**
1. **Chạy tự động hàng ngày**:
   - Thay thế **Manual Trigger** bằng **Cron Trigger** với biểu thức như `0 0 * * *` (lúc 00:00 hàng ngày).

2. **Lọc dữ liệu trước khi lưu**:
   - Thêm **IF Node** sau **Transform Data** để chỉ lưu dữ liệu có điều kiện (ví dụ: chỉ lưu người dùng từ quốc gia nhất định).

3. **Gửi báo cáo qua Email/Slack**:
   - Thêm **Node Email** hoặc **Node Slack** sau **Create CSV Backup** để thông báo khi backup hoàn tất.

4. **Lưu log hoạt động**:
   - Thêm **Node Database** (ví dụ: PostgreSQL) để lưu lịch sử chạy workflow.

5. **Tùy chỉnh cột trong Google Sheets**:
   - Nếu muốn thêm cột mới (ví dụ: "Email", "Điện thoại"), chỉnh sửa **Function Node** để trả về thêm trường dữ liệu và cập nhật **Range** trong **Google Sheets Node**.

---
### **📌 Kết Luận**
Workflow này giúp các sếp **tự động hóa hoàn toàn** việc lấy dữ liệu từ API và lưu trữ trên Google Sheets với **bản sao lưu CSV tự động**, tiết kiệm thời gian và tránh sai sót. **Chỉ cần 5 phút cấu hình**, bạn đã có một hệ thống tự động hóa chuyên nghiệp!

**👉 Bắt đầu ngay bằng cách import workflow và tùy chỉnh theo nhu cầu của mình!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**💬 Cần hỗ trợ?** Hãy để lại comment bên dưới hoặc liên hệ với cộng đồng n8n trên [Discord](https://discord.gg/n8n)!