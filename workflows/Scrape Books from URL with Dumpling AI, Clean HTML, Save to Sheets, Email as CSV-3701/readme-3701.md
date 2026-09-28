---
title: "📚 Tự Động Hoàn Thành: Scrape Sách Từ URL → Lọc Giá → Xuất CSV → Gửi Email (Dumpling AI + n8n)"
description: "Workflow tự động hóa lấy dữ liệu sách từ website, sắp xếp theo giá, chuyển thành CSV và gửi email tự động - tiết kiệm 100% thời gian thủ công cho các sếp quản lý sách, thư viện hoặc shop online."
slug: "tieu-dong-hoan-thanh-scrape-sach-tu-url-den-email-csv"
tags: [n8n, automation, scraping, dumpling-ai, google-sheets, gmail, csv]
keywords: [scrape sách từ website, tự động hóa lấy dữ liệu sách, Dumpling AI n8n, export sách thành CSV, gửi email tự động với n8n]
---

# 🚀 **Tự Động Hoàn Thành: Scrape Sách Từ Website → Lọc Giá → Xuất CSV → Gửi Email (Dumpling AI + n8n)**

### **Nỗi Đau Của Các Sếp**
Các sếp quản lý sách, thư viện, hoặc shop online thường phải:
- **Lấy dữ liệu sách thủ công** từ website (thời gian mất từ 30 phút đến 2 giờ/tuần).
- **Lọc và sắp xếp sách theo giá** để phân loại hoặc báo cáo.
- **Xuất dữ liệu thành CSV** để phân tích hoặc gửi cho khách hàng.
- **Gửi email với file CSV** để báo cáo định kỳ.

**Workflow này giải quyết tất cả trong 1 lần setup, hoạt động tự động 24/7!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tháng** không phải lấy dữ liệu thủ công.
- **Sắp xếp sách theo giá tự động**, không cần sort Excel.
- **Xuất CSV sạch sẽ**, dễ dàng phân tích hoặc gửi cho khách hàng.
- **Gửi email tự động** với file CSV đính kèm, không cần nhớ gửi.
- **Hoạt động liên tục**, không phụ thuộc vào thời gian làm việc.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google Cloud** (để kích hoạt API Gmail, Sheets và Drive).
2. **Tài khoản Dumpling AI** (để scrape website).
3. **Tài khoản Gmail** (để gửi email tự động).
4. **Google Sheet** (để lưu URL sách cần scrape).
5. **API Key của Dumpling AI** (để kết nối với node `httpRequest`).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Truy cập [n8n.io](https://n8n.io/) và đăng nhập vào tài khoản.
2. Vào **Workflow** → **Create New Workflow**.
3. Nhấp vào **Import** và chọn file JSON (hoặc paste JSON từ [link gốc](https://n8n.io/workflows/3701)).
4. Sau khi import, workflow sẽ hiển thị 8 node như mô tả dưới đây.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Dưới đây là **các node quan trọng** cần cấu hình kỹ lưỡng:

##### **🔹 Node 1: Trigger - Watches For New URL in Spreadsheet**
- **Cấu hình**:
  - Chọn **Google Sheets Trigger** và chọn **Sheet** chứa URL sách.
  - Cấu hình **Trigger Type** là **"Row added"** (khi có dòng mới được thêm vào).
  - **Column Name** phải là cột chứa URL (ví dụ: `URL_Sách`).

##### **🔹 Node 2: Scrape Website Content with Dumpling AI**
- **Cấu hình**:
  - Chọn **HTTP Request** và cấu hình như sau:
    - **Method**: `POST`
    - **URL**: `https://api.dumpling.ai/scrape` (hoặc URL API của Dumpling AI).
    - **Headers**:
      ```json
      {
        "Authorization": "Bearer YOUR_DUMPLING_API_KEY",
        "Content-Type": "application/json"
      }
      ```
    - **Body**:
      ```json
      {
        "url": "{{$node["Trigger- Watches For new URL in Spreadsheet"].json["URL_Sách"]}}"
      }
      ```
  - **Lưu ý**: Thay thế `YOUR_DUMPLING_API_KEY` bằng API Key của Dumpling AI.

##### **🔹 Node 3 & 4: Extract All Books & Extract Individual Book Price**
- **Cấu hình**:
  - **Extract All Books**:
    - Chọn **HTML** và cấu hình **CSS Selector** là `li.row > li` (lấy tất cả sách trong trang).
  - **Extract Individual Book Price**:
    - Chọn **HTML** và cấu hình **CSS Selector** là `.price_color` (lấy giá sách).
    - **Lưu ý**: Nếu website có cấu trúc khác, cần điều chỉnh CSS Selector phù hợp.

##### **🔹 Node 5: Sort by Price**
- **Cấu hình**:
  - Chọn **Sort** và cấu hình:
    - **Field**: `price` (trường chứa giá sách).
    - **Order**: `desc` (sắp xếp từ cao đến thấp).

##### **🔹 Node 6: Convert to CSV File**
- **Cấu hình**:
  - Chọn **Convert to File** và cấu hình:
    - **Format**: `CSV`.
    - **File Name**: `sach_{{$node["Trigger- Watches For new URL in Spreadsheet"].json["URL_Sách"].split("/").pop()}}.csv`.

##### **🔹 Node 7: Send CSV via Email**
- **Cấu hình**:
  - Chọn **Gmail** và cấu hình:
    - **Credentials**: `gmailOAuth2` (đã cấu hình trước).
    - **To**: Email nhận (ví dụ: `quanlysach@example.com`).
    - **Subject**: `Dữ liệu sách mới - {{$node["Trigger- Watches For new URL in Spreadsheet"].json["URL_Sách"].split("/").pop()}}`.
    - **Body**: `Xin chào, đây là dữ liệu sách mới được scrape từ {{$node["Trigger- Watches For new URL in Spreadsheet"].json["URL_Sách"]}}.`
    - **Attachments**: Chọn file CSV từ node `Convert to CSV File`.

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với một URL mẫu:
   - Thêm URL vào Google Sheet.
   - Chạy workflow và kiểm tra email có nhận được file CSV không.
2. **Bật Active** workflow nếu test thành công.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram** để thông báo khi scrape xong.
2. **Lưu Log Dữ Liệu**:
   - Thêm node **Google Sheets** để lưu log scrape (thời gian, URL, số sách).
3. **Gửi Báo Cáo Định Kỳ**:
   - Sử dụng **Google Calendar** kết hợp với **n8n** để gửi báo cáo hàng tuần/tháng.
4. **Tự Động Cập Nhật Google Sheet**:
   - Thêm node **Google Sheets** để ghi dữ liệu sách vào sheet khác (dùng cho phân tích).

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc thủ công, đồng thời **tăng tính chính xác** và **cá nhân hóa** dữ liệu sách. **Chỉ cần thêm URL vào Google Sheet, workflow sẽ tự động scrape, sắp xếp, xuất CSV và gửi email!**

**Hãy áp dụng ngay và tiết kiệm 10+ giờ/tháng!** 🚀

---
**🔗 [Tải workflow nguyên bản](https://n8n.io/workflows/3701)** (nếu cần tham khảo thêm).