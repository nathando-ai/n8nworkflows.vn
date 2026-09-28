---
title: "📄 Tự Động Chuyển Tệp Scan Sang Nextcloud Miễn Phí - Khắc Phục Nỗi Đau Quản Lý Tài Liệu"
description: "Workflow tự động hóa hoàn toàn không code giúp các sếp tự động chuyển tất cả tài liệu quét từ máy scan sang Nextcloud trong giây lát, tiết kiệm thời gian và tránh mất mát dữ liệu."
slug: "tu-dong-chuyen-tep-scan-sang-nextcloud"
tags: [n8n, tự động hóa văn phòng, nextcloud, scanservjs, it-ops]
keywords: [n8n workflow tự động hóa, chuyển file scan sang nextcloud, tự động hóa văn phòng, quản lý tài liệu, scanservjs api]
---

# 🚀 **Tự Động Chuyển Tệp Scan Sang Nextcloud - Giải Pháp Tiết Kiệm Thời Gian Cho Văn Phòng**

### **Nỗi Đau Của Các Sếp**
Hàng ngày, các sếp phải mất thời gian quét và chuyển các tài liệu giấy sang định dạng số để lưu trữ trên Nextcloud. Quá trình này không chỉ tốn thời gian mà còn dễ gây lỗi nhân sự (quên chuyển file, sai tên file, mất mát dữ liệu). **Workflow này tự động hóa toàn bộ quy trình, chỉ cần một máy scan kết nối với ScanservJS và Nextcloud.**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động 24/7, các sếp nên cài n8n trên **VPS riêng** (Self-hosted) để đảm bảo tính ổn định và bảo mật.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
- **Tiết kiệm thời gian**: Không cần phải chuyển file thủ công sau mỗi lần scan.
- **Chính xác 100%**: Tệp được tự động đặt tên và lưu vào Nextcloud theo quy tắc.
- **Hoạt động liên tục**: Workflow chạy tự động theo lịch trình hoặc khi có file mới scan.
- **Giảm thiểu lỗi**: Không còn quên chuyển file hoặc sai tên folder.

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Máy scan USB** kết nối với máy tính.
2. **ScanservJS** (Phần mềm quét tài liệu với API hỗ trợ).
3. **Tài khoản Nextcloud** với quyền API.
4. **n8n Self-hosted** (cài đặt trên VPS hoặc máy chủ riêng).
5. **API Key của Nextcloud** (để kết nối với Nextcloud).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Bước 1**: Tải file JSON của workflow từ [n8n.io/workflows/3861](https://n8n.io/workflows/3861).
- **Bước 2**: Mở **n8n Editor** và nhấn **"Import"** → Chọn file JSON vừa tải.
- **Bước 3**: Workflow sẽ hiển thị với 4 node chính:
  - **Schedule Trigger** (khởi động theo lịch).
  - **HTTP Request** (gửi yêu cầu đến ScanservJS).
  - **Nextcloud** (upload file vào Nextcloud).
  - **HTTP Request1** (xử lý phản hồi từ ScanservJS).

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
##### **a) Cấu Hình Node "Nextcloud"**
- **Credentials**: Chọn **"nextCloudApi"** (đã cấu hình trước khi import).
- **Path**: Đặt theo định dạng `=/Scans/{{ $json.name }}` (đảm bảo folder `Scans` tồn tại trên Nextcloud).
- **File Name**: Sử dụng `{{ $json.name }}` để tự động đặt tên file từ ScanservJS.

##### **b) Cấu Hình Node "HTTP Request" (liên kết với ScanservJS)**
- **Method**: POST
- **URL**: Điền URL API của ScanservJS (ví dụ: `http://localhost:3000/api/scans`).
- **Headers**: Thêm `Content-Type: application/json`.
- **Body**: Chọn **Raw** và nhập:
  ```json
  {
    "action": "getScans"
  }
  ```
  (Lấy danh sách file mới scan từ ScanservJS).

##### **c) Cấu Hình Node "Schedule Trigger"**
- **Frequency**: Chọn **Every 5 minutes** (hoặc tùy chỉnh theo nhu cầu).
- **Timezone**: Đặt theo giờ máy chủ.

##### **d) Node "HTTP Request1" (xử lý phản hồi)**
- **Method**: GET (nếu cần lấy chi tiết file).
- **URL**: Điền URL API của ScanservJS để lấy thông tin file (ví dụ: `http://localhost:3000/api/scans/{{ $node["HTTP Request"].json["id"] }}`).

#### **3. Kích Hoạt ⚡️**
- **Bước 1**: Nhấn **"Run"** để test với dữ liệu mẫu.
- **Bước 2**: Kiểm tra Nextcloud để xác nhận file đã upload thành công.
- **Bước 3**: Bật **"Active"** để workflow chạy tự động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết nối với Slack/Telegram**: Thêm node **Slack** hoặc **Telegram** để thông báo khi có file mới scan.
2. **Lưu Log**: Sử dụng node **StickyNote** để ghi lại lịch sử upload.
3. **Gửi Báo Cáo Định Kỳ**: Tạo một workflow phụ để tổng hợp và gửi báo cáo số lượng file scan hàng tháng.
4. **Tự Động Xóa File Tạm**: Sau khi upload thành công, thêm node **HTTP Request** để xóa file tạm trên ScanservJS.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc lặp lại, đồng thời **giảm thiểu sai sót** khi chuyển file. **Chỉ cần một máy scan và ScanservJS, bạn đã có một hệ thống tự động hóa hoàn chỉnh!**
👉 **Hãy import ngay và bắt đầu tự động hóa văn phòng của mình!**

---
**💡 Lưu ý cuối cùng**: Nếu gặp vấn đề, hãy kiểm tra lại **URL API của ScanservJS** và **quyền API của Nextcloud**. Nếu cần hỗ trợ, liên hệ với tác giả [Joachim Hummel](https://n8n.io/workflows/3861) hoặc cộng đồng n8n.