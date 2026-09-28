---
title: "🔍 **Tự Động Theo Dõi Tệp Mới & Cập Nhật Trên Google Drive (Tất Cả Thư Mục Nested) - N8n Workflow**"
description: "Giải pháp tự động hóa 100% không code để theo dõi tất cả tệp mới hoặc được cập nhật trong Google Drive, bao gồm cả thư mục con lồng nhau. Giúp các sếp tiết kiệm thời gian, tránh bỏ sót tệp quan trọng và tự động hóa quy trình content creation."
slug: "tu-dong-theo-doi-tep-moi-cap-nhat-google-drive-n8n"
tags: [n8n, automation, google-drive, content-creation, no-code, ai-automation]
keywords: [n8n workflow google drive, tự động hóa theo dõi tệp mới, content creation automation, theo dõi tệp cập nhật google drive, n8n schedule trigger]
---

# 🚀 **Tự Động Theo Dõi Tệp Mới & Cập Nhật Trên Google Drive (Tất Cả Thư Mục Nested)**

## 💡 **Giới Thiệu: Tiết Kiệm Thời Gian & Tránh Bỏ Sót Tệp Quan Trọng**
Các sếp có biết rằng việc **quét thủ công** tất cả các tệp mới hoặc được cập nhật trong Google Drive (bao gồm cả hàng trăm thư mục con lồng nhau) có thể mất **giờ đồng hồ** mỗi tuần? Hay thậm chí, các sếp còn **bỏ sót** những tệp quan trọng vì quên kiểm tra?

**Workflow này giải quyết vấn đề đó bằng cách:**
✅ **Tự động quét tất cả tệp mới/cập nhật** trong **cả thư mục gốc và tất cả thư mục con** (nested folders).
✅ **Chạy định kỳ** (dựa vào lịch trình của các sếp) mà **không cần can thiệp thủ công**.
✅ **Lọc ra chỉ những tệp mới hoặc được sửa đổi** (trừ lần chạy đầu tiên).
✅ **Hoàn toàn không cần code**, chỉ cần cấu hình vài bước đơn giản.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đảm bảo tốc độ cao cho workflow)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần quét thủ công hàng tuần, tự động hóa toàn bộ quy trình.
- **Tránh bỏ sót tệp**: Theo dõi **tất cả tệp mới và cập nhật** trong cả thư mục con lồng nhau.
- **Chỉnh sửa linh hoạt**: Cấu hình **lịch trình chạy** (ví dụ: hàng ngày, hàng tuần) theo nhu cầu.
- **Dữ liệu chính xác**: Chỉ lấy ra **tệp mới hoặc được sửa đổi** (trừ lần chạy đầu tiên).
- **Hoàn toàn tự động**: Sau khi cấu hình, workflow **chạy độc lập** mà không cần can thiệp.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản Google Drive** (và **API Key** của Google Drive).
✔ **Thư mục gốc (root folder)** cần theo dõi (các sếp sẽ cấu hình trong workflow).
✔ **Thời gian chạy định kỳ** (ví dụ: 1 lần/ngày, 1 lần/tuần).
✔ **N8n self-hosted** (không dùng phiên bản miễn phí trên cloud).

---
:::note[LƯU Ý QUAN TRỌNG]
- **Lần chạy đầu tiên** sẽ **quét tất cả tệp** trong thư mục (do không có dữ liệu so sánh trước đó).
- **Không khuyến cáo dùng cho thư mục có >10.000 tệp** (có thể gây **performance issues**).
:::

---

## 🚀 **Cách Import & Cấu Hình Workflow**

### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow này:

#### **Cách 1: Từ File JSON**
1. **Tải workflow** từ [đây](https://n8n.io/workflows/9209) (nút "Export").
2. **Mở n8n Editor** (trên VPS hoặc n8n.io).
3. Nhấn **"Import"** → Chọn file JSON vừa tải → **"Import"**.

#### **Cách 2: Copy/Paste JSON**
1. **Tải workflow** từ [đây](https://n8n.io/workflows/9209) và copy toàn bộ JSON.
2. Trong **n8n Editor**, nhấn **"Import"** → Chọn **"Paste JSON"** → Dán và nhấn **"Import"**.

---

### **2. Các Bước Cấu Hình Bắt Buộc 📌**

#### **🔹 Bước 1: Cấu Hình Google Drive Credentials**
1. **Tạo API Key Google Drive**:
   - Đăng nhập [Google Cloud Console](https://console.cloud.google.com/).
   - Tạo **API Key** cho **Google Drive API**.
   - Cấp quyền **"Drive API"** cho tài khoản.
2. **Thêm credentials vào n8n**:
   - Trong **n8n Editor**, nhấn **"Credentials"** → **"Add"** → **"Google Drive"**.
   - Điền **API Key** vừa tạo và **thư mục gốc (root folder ID)**.

#### **🔹 Bước 2: Đặt Thư Mục Gốc (Root Folder)**
- Trong **2 node Google Drive** có **hình chữ nhật đỏ** (nó là **"List folders"** và **"List all files"**):
  - Mở node → Tab **"Advanced"** → Điền **ID của thư mục gốc** (có thể lấy từ liên kết Google Drive: `https://drive.google.com/drive/folders/[ID]`).
  - **Lưu ý**: Các sếp phải **điền ID vào cả 2 node** này.

#### **🔹 Bước 3: Cấu Hình Lịch Trình Chạy (Schedule Trigger)**
1. Mở node **"Schedule Trigger"**.
2. Cấu hình **lịch trình chạy** (ví dụ: `0 0 * * *` = chạy hàng ngày lúc 00:00).
3. **Lưu ý**:
   - **Lần chạy đầu tiên** sẽ **quét tất cả tệp** (do không có dữ liệu so sánh).
   - Sau đó, workflow **chỉ lấy ra tệp mới hoặc được cập nhật**.

#### **🔹 Bước 4: Kiểm Tra & Bật Workflow**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **"Run Workflow"** để kiểm tra nếu có lỗi.
   - Kiểm tra **log** trong tab **"Execution"**.
2. **Bật Active**:
   - Sau khi kiểm tra thành công, nhấn **"Active"** để workflow chạy tự động theo lịch.

---

### **3. Các Node Quan Trọng & Giải Thích**
| **Tên Node** | **Chức Năng** | **Cần Chỉnh Sửa Gì?** |
|--------------|--------------|----------------------|
| **Schedule Trigger** | Xác định lịch trình chạy (ví dụ: hàng ngày). | **Cần chỉnh** thời gian chạy. |
| **List folders** (2 node) | Liệt kê tất cả thư mục trong **root folder** và **subfolders**. | **Cần điền ID root folder**. |
| **List all files** | Lấy danh sách tất cả tệp trong thư mục. | **Không cần chỉnh** (n8n tự lấy). |
| **If folders exist** | Kiểm tra nếu có thư mục con → tiếp tục quét. | **Không cần chỉnh**. |
| **ExecuteWorkflowTrigger** | Khởi động lại workflow để quét **subfolders**. | **Không cần chỉnh**. |
| **Wait** | Đợi cho đến khi so sánh tệp hoàn tất. | **Không cần chỉnh**. |
| **Outputs new or updated files** (Code Node) | Lọc ra **tệp mới hoặc được cập nhật**. | **Không cần chỉnh** (n8n tự xử lý). |

---

### **✍️ Mẹo & Gợi Ý Nâng Cao**
1. **Gửi kết quả qua Email/Slack**:
   - Thêm **node Email** hoặc **Slack** sau node **"Outputs new or updated files"** để **báo cáo tự động** khi có tệp mới.
   - Ví dụ: Gửi **danh sách tệp mới** qua Email hàng ngày.

2. **Lưu log vào Google Sheets**:
   - Thêm **node Google Sheets** để **ghi chép lịch sử** tệp mới/cập nhật.
   - Có thể **tự động tạo báo cáo** định kỳ.

3. **Kết hợp với AI (LLM) để phân tích nội dung**:
   - Sử dụng **node LLM** (ví dụ: Mistral, Llama) để **tóm tắt** hoặc **phân loại** tệp mới.
   - Ví dụ: Nếu có tệp **PDF/Word**, AI có thể **trích xuất nội dung chính** và gửi cho các sếp.

4. **Chia nhỏ thư mục lớn**:
   - Nếu thư mục có **>5.000 tệp**, các sếp có thể **chia nhỏ** thành nhiều root folder nhỏ hơn để tránh **performance issues**.

5. **Bật debug mode**:
   - Trong **n8n Editor**, bật **"Debug Mode"** để **xem chi tiết** mỗi node hoạt động như thế nào.

---

### **📌 Kết Luận: Áp Dụng Ngay Để Tiết Kiệm Thời Gian!**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc **quét thủ công** tệp trên Google Drive, đồng thời **tránh bỏ sót** những tệp quan trọng. Với **cấu hình đơn giản** và **lịch trình tự động**, các sếp có thể **focusing vào công việc chiến lược** thay vì công việc lặp lại.

**Bắt đầu ngay bằng cách:**
1. **Import workflow** từ [đây](https://n8n.io/workflows/9209).
2. **Cấu hình Google Drive credentials** và **root folder**.
3. **Chỉnh lịch trình chạy** theo nhu cầu.
4. **Bật Active** và **quên việc quét tệp thủ công**!

---
**Cần hỗ trợ?** Liên hệ với **Ossian Madisson** (tác giả workflow) qua:
📧 **ossian@smultronstudio.com**
🔗 [Website Smultron Studio](https://smultronstudio.com)