---
title: "🚀 Tự Động Hạ TikTok Bulk Sang Google Drive MÀ KHÔNG CÓ Watermark + Theo Dõi Tự Động - Giảm 100% Công Việc Thủ Công"
description: "Workflow này tự động tải xuống hàng loạt video TikTok (không có watermark), upload lên Google Drive với quyền chia sẻ công khai, và cập nhật liên kết tự động vào Google Sheet. Giúp các sếp tiết kiệm hàng giờ công việc thủ công mỗi tuần."
slug: "tieu-dong-tiktok-bulk-sang-google-drive-khong-watermark"
tags: [n8n, automation, file-management, google-drive, tiktok-downloader, no-code]
keywords: [tải video tiktok bulk, tự động hóa tiktok sang google drive, workflow n8n tiktok, tải video tiktok không watermark, tự động hóa google sheets]
---

# 🚀 **Tự Động Hạ TikTok Bulk Sang Google Drive (Không Watermark) + Theo Dõi Tự Động**

## **💥 Nỗi Đau Của Các Sếp Khi Làm Thủ Công**
Các sếp đã từng phải:
- **Tải video TikTok một một** (với watermark) bằng phần mềm hoặc trình duyệt, mất **tối thiểu 30 phút cho 10 video**.
- **Upload lên Google Drive thủ công**, sau đó **cập nhật liên kết vào Google Sheet** để theo dõi – **rất dễ quên hoặc sai sót**.
- **Không kiểm soát được watermark**, ảnh hưởng đến chất lượng video cuối cùng.
- **Phải làm lại từ đầu** nếu video bị lỗi hoặc không tải được.

**Workflow này giải quyết tất cả!** Tự động hóa **tất cả quá trình** từ tải video TikTok (không watermark) → upload Google Drive → chia sẻ công khai → cập nhật Google Sheet **với 1 cú nhấp chuột**.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 5-10 giờ/tháng** cho công việc thủ công.
✅ **Video không watermark**, chất lượng cao nhất.
✅ **Tự động chia sẻ công khai** trên Google Drive (không cần thiết lập thủ công).
✅ **Theo dõi toàn bộ quá trình** trong Google Sheet (URL TikTok → Liên kết Google Drive).
✅ **Xử lý batch** (tải nhiều video cùng lúc) với **delay tự động** để tránh bị chặn API.
✅ **An toàn & ổn định** – Không cần code, chỉ cần cấu hình đơn giản.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google** (để kết nối Google Drive & Google Sheets).
2. **Google Sheet** có **2 cột bắt buộc**:
   - `url` (địa chỉ video TikTok).
   - `driveurl` (sẽ tự động cập nhật liên kết Google Drive).
   *Ví dụ:*
   | url                          | driveurl          |
   |------------------------------|-------------------|
   | https://www.tiktok.com/...   | (trống ban đầu)   |
3. **API Key TikTok Downloader** (miễn phí từ [RapidAPI](https://rapidapi.com/apidojo/api/tiktok-downloader/)).
4. **VPS Self-hosted n8n** (để workflow chạy 24/7).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).
:::

---

## 🚀 **Cách Import & Cấu Hình Workflow**

### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/6171](https://n8n.io/workflows/6171) và import vào **n8n Editor**.
- **Copy JSON** từ link trên và **dán vào n8n Editor** (tab "Import").

:::note[LƯU Ý]
- **Không cần chỉnh sửa JSON** nếu đã import hoàn chỉnh.
- **Không cần cài thêm node** vì workflow đã sử dụng các node cơ bản của n8n.
:::

---

### **2. Các Bước Cấu Hình BẮT BUỘC 📌**

#### **🔹 Node 1: Manual Trigger (Bắt Đầu Tự Động)**
- **Không cần cấu hình**, chỉ cần **bấm "Execute workflow"** để chạy thủ công.

#### **🔹 Node 2: Get Data From Google Sheets**
- **Credentials**: Chọn `googleApi` (đã cấu hình trước khi import).
- **Sheet Name**: Điền tên **Google Sheet** chứa danh sách video TikTok.
- **Range**: Điền `Sheet1!A:B` (giả sử dữ liệu ở Sheet1, cột A là `url`, cột B là `driveurl`).
- **Output Format**: Chọn `JSON`.

#### **🔹 Node 3: Loop Over Items (Xử Lý Batch)**
- **Không cần cấu hình**, node này tự động **lặp qua từng dòng** trong Google Sheet.

#### **🔹 Node 4: Call TikTok Downloader (API TikTok)**
- **Method**: `POST`.
- **URL**: `https://tiktok-downloader.p.rapidapi.com/dlvideo/`
- **Headers**:
  - `X-RapidAPI-Key`: Điền **API Key TikTok Downloader** (mua từ RapidAPI).
  - `X-RapidAPI-Host`: `tiktok-downloader.p.rapidapi.com`.
- **Body (JSON)**:
  ```json
  {
    "url": "{{$node["Get Data From Google Sheets"].json["url"]}}"
  }
  ```
  *(Lấy URL từ Google Sheet và gửi đến API).*

#### **🔹 Node 5: Wait (Delay Tránh Rate Limit)**
- **Time**: Đặt **5 giây** (giúp tránh bị chặn API khi tải nhiều video).
- **Không cần cấu hình thêm**.

#### **🔹 Node 6: Download File (Tải Video TikTok)**
- **Method**: `GET`.
- **URL**: `{{$node["Call TikTok Downloader"].json["medias"][1]["url"]}}` *(Lấy URL video từ API TikTok Downloader).*
- **Response Format**: `Binary` (để tải file video).

#### **🔹 Node 7: Upload File In Google Drive**
- **Credentials**: Chọn `googleApi`.
- **File**: Chọn **Binary data** từ node Download File.
- **Folder**: Chọn **Root** (hoặc folder tùy chọn).
- **File Name**: `{{$node["Get Data From Google Sheets"].json["url"].split("/").pop()}}.mp4` *(Tên file tự động từ URL TikTok).*

#### **🔹 Node 8: Set Public Permission Google Drive**
- **Credentials**: Chọn `googleApi`.
- **File ID**: Lấy từ **Output của node Upload File In Google Drive** (`id`).
- **Permission**: `anyone` (chia sẻ công khai).

#### **🔹 Node 9: Update Row In Google Sheet**
- **Credentials**: Chọn `googleApi`.
- **Sheet Name**: Điền tên **Google Sheet** (như Node 2).
- **Range**: `Sheet1!A:B` (cùng với Node 2).
- **Operation**: `update`.
- **Value**:
  - `url`: Giá trị cũ (không đổi).
  - `driveurl`: `{{$node["Upload File In Google Drive"].json["webViewLink"]}}` *(Liên kết Google Drive công khai).*

#### **🔹 Node 10: Sleep (Delay Giả Lệ)**
- **Time**: **10 giây** (giúp tránh quá tải server khi xử lý batch).

---

### **3. Kích Hoạt Workflow ⚡️**
1. **Test Run** với **1-2 video** để kiểm tra:
   - Video có tải xuống không?
   - File có upload lên Google Drive không?
   - Liên kết `driveurl` có cập nhật không?
2. **Bật Active** nếu test thành công.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**

### **🔹 Mở Rộng Cho Nhóm Làm Việc**
- **Chia sẻ Google Sheet** cho toàn bộ team để **ai cũng có thể thêm video**.
- **Tạo 1 sheet riêng cho mỗi dự án** (ví dụ: `TikTok_2024_Q1`).

### **🔹 Theo Dõi Log & Báo Cáo**
- **Thêm node `Set`** sau node Download File để lưu **log lỗi** (ví dụ: video không tải được).
- **Gửi báo cáo định kỳ** bằng **Slack/Email** (sử dụng node `n8n-nodes-base.slack` hoặc `n8n-nodes-base.email`).

### **🔹 Optimize Speed**
- **Tăng delay** (Node Wait) nếu gặp **rate limit** (ví dụ: 10 giây thay vì 5 giây).
- **Chia batch nhỏ hơn** (ví dụ: 5 video/lần) nếu server chậm.

### **🔹 Tự Động Chạy Hàng Ngày**
- **Kết nối với n8n Cloud** hoặc **cài trên VPS** để chạy **tự động hàng ngày** (sử dụng **cron job**).

---

## 📌 **Kết Luận**
Workflow này **giải phóng hoàn toàn công việc thủ công** khi tải TikTok bulk sang Google Drive, **không watermark**, và **tự động cập nhật theo dõi**. Các sếp chỉ cần:
1. **Chuẩn bị Google Sheet** với danh sách video.
2. **Import workflow** và cấu hình API.
3. **Bấm "Execute"** và **xem kết quả** trong vài phút!

**🚀 Hãy áp dụng ngay để tiết kiệm thời gian và nâng cao hiệu suất!**
Nếu có vấn đề, **hãy comment bên dưới** hoặc liên hệ với **Sk developer** qua [n8n.io](https://n8n.io/workflows/6171).