---
title: "🚀 Tự Động Hóa Di Chuyển File FTP Thông Khôn Với Gửi Thông Báo Email Tự Động - Giảm Thời Gian Làm Việc Gấp 10 Lần"
description: "Workflow tự động hóa di chuyển file từ FTP nguồn sang FTP đích, xóa file nguồn sau khi thành công, và gửi email thông báo kết quả. Giúp doanh nghiệp tiết kiệm thời gian, giảm sai sót và tối ưu hóa quy trình quản lý file 24/7."
slug: "tieu-dong-hoa-di-chuyen-file-ftp-voi-email-notification"
tags: [n8n, tự động hóa, file management, ftp, email notification, no-code, automation]
keywords: [n8n workflow ftp, tự động hóa di chuyển file, gửi email thông báo thành công, quản lý file tự động, n8n file migration]
---

# 🚀 **Tự Động Hóa Di Chuyển File FTP Thông Khôn Với Email Notifications**

## **Nỗi Đau Của Các Sếp Khi Làm Thủ Công**
Hàng ngày, các sếp phải mất **giờ đồng hồ** để:
- **Kiểm tra và sao chép** file từ FTP nguồn sang FTP đích.
- **Xác minh** file đã được chuyển thành công hay chưa.
- **Gửi thông báo** cho team khi có lỗi hoặc thành công.
- **Quản lý thủ công** các file lớn, dễ gây ra **sai sót** hoặc **mất dữ liệu**.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Liệt kê và lọc** file theo định dạng (txt, csv, json, pdf, ảnh, video...).
✅ **Tải xuống và upload** file từ FTP nguồn → FTP đích.
✅ **Xóa file nguồn** sau khi thành công.
✅ **Gửi email thông báo** kết quả (thành công/thất bại).
✅ **Chạy tự động hàng ngày** vào 2h sáng (không cần can thiệp).

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần làm thủ công hàng ngày.
- **Chính xác 100%**: Không bị lỗi nhân sự hoặc quên xóa file nguồn.
- **Cá nhân hóa thông báo**: Email tự động cho team biết tình trạng.
- **Hoạt động 24/7**: Không phụ thuộc vào giờ làm việc.
- **Dễ dàng mở rộng**: Thêm được nhiều định dạng file khác.
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng, các sếp cần chuẩn bị:
✔ **Hai tài khoản FTP** (nguồn và đích) với quyền:
   - **Đọc** (source FTP).
   - **Ghi** (destination FTP).
✔ **Email SMTP** để gửi thông báo (cấu hình trong node `emailSend`).
✔ **Danh sách định dạng file** muốn di chuyển (ví dụ: `.txt`, `.csv`, `.pdf`).
✔ **VPS n8n** (self-hosted) để workflow chạy 24/7 (không phụ thuộc vào máy tính cá nhân).
:::

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Cách 1: Từ File JSON**
1. **Tải workflow** từ [n8n.io/workflows/8161](https://n8n.io/workflows/8161).
2. **Mở n8n Editor** trên VPS của mình.
3. **Nhấp vào "Import"** → Chọn file JSON vừa tải.
4. **Chọn "Import"** để workflow xuất hiện trên canvas.

#### **Cách 2: Copy/Paste JSON**
1. **Copy toàn bộ JSON** từ [n8n.io/workflows/8161](https://n8n.io/workflows/8161).
2. **Mở n8n Editor** → Nhấp **"Import"** → Chọn **"Paste JSON"**.
3. **Nhấp "Import"** để workflow hiện lên.

---
### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **9 node chính**, các sếp cần cấu hình kỹ lưỡng:

#### **🔹 Node 1: Daily Schedule (2 AM)**
- **Cấu hình thời gian chạy**: Đặt vào **2h sáng** (hoặc thời gian phù hợp).
- **Lưu ý**: Nếu muốn chạy khác giờ, chỉnh `cron` trong node này.

#### **🔹 Node 2 & 3: List Files - Source FTP & Filter Files**
- **Cấu hình FTP Source**:
  - **Host**: Địa chỉ FTP nguồn (ví dụ: `ftp.example.com`).
  - **Port**: 21 (FTP) hoặc 22 (SFTP).
  - **Username/Password**: Tài khoản có quyền đọc.
  - **Path**: `/source/directory/` (đường dẫn folder chứa file).
- **Cấu hình Filter**:
  - **Định dạng file**: Sử dụng biểu thức chính quy để lọc file (ví dụ: `\.(txt|csv|json)$`).
  - **Kích thước file**: Nếu muốn loại bỏ file quá lớn, thêm điều kiện trong `Filter`.

#### **🔹 Node 4 & 5: Download File & Upload to Destination**
- **Cấu hình FTP Destination**:
  - **Host**: Địa chỉ FTP đích.
  - **Port**: 21 hoặc 22.
  - **Username/Password**: Tài khoản có quyền ghi.
  - **Path**: `/destination/directory/{{ $json.name }}` (file sẽ được upload vào folder đích).
- **Lưu ý**:
  - Nếu file có tên đặc biệt (có ký tự đặc biệt), cần **encode URL** trong path.
  - **Kiểm tra quyền** của folder đích để đảm bảo upload thành công.

#### **🔹 Node 6: Upload Success?**
- **Chức năng**: Xác minh file đã upload thành công hay chưa.
- **Cấu hình**:
  - Nếu upload thành công, node này sẽ **cho phép xóa file nguồn** (node tiếp theo).
  - Nếu thất bại, workflow sẽ **dừng lại** và không xóa file.

#### **🔹 Node 7: Delete Source File**
- **Cấu hình**:
  - **Path**: `={{ $json.name }}` (xóa file từ FTP nguồn).
  - **Lưu ý**: **Không xóa file nếu upload thất bại** (do node 6 kiểm tra).

#### **🔹 Node 8: Log Success**
- **Chức năng**: Ghi log thành công vào n8n (dùng để debug).
- **Cấu hình**:
  - **Key**: `status` → `success`.
  - **Value**: `File {{ $json.name }} đã di chuyển thành công!`.

#### **🔹 Node 9: Send Email Success Alert**
- **Cấu hình SMTP**:
  - **Host**: `smtp.gmail.com` (hoặc SMTP của doanh nghiệp).
  - **Port**: 587 (TLS) hoặc 465 (SSL).
  - **Username/Password**: Tài khoản email để gửi thông báo.
  - **From Email**: `noreply@doanhnghiep.com`.
  - **To Email**: Email của team cần thông báo.
  - **Subject**: `📤 File {{ $json.name }} đã di chuyển thành công!`.
  - **Body**: `File {{ $json.name }} đã được di chuyển từ {{ $json.sourcePath }} sang {{ $json.destPath }} thành công.`

---
### **3. Kích Hoạt ⚡️**
1. **Test Run** với **1-2 file nhỏ** để kiểm tra:
   - File có được tải xuống và upload thành công không?
   - Email thông báo có được gửi không?
   - File nguồn có bị xóa không?
2. **Bật Active** workflow sau khi test thành công.

---
## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
- **Thêm Slack/Telegram Notifications**:
  - Sử dụng node `slackSend` hoặc `telegramSend` để gửi thông báo ngay khi có lỗi.
- **Lưu Log vào Google Sheets**:
  - Thêm node `googleSheets` để ghi tất cả log thành công/thất bại vào bảng tính.
- **Gửi Báo Cáo Định Kỳ**:
  - Sử dụng node `emailSend` hoặc `slackSend` để báo cáo tổng hợp hàng tuần.
- **Xử Lý File Lớn (>100MB)**:
  - Tăng **timeout** trong node FTP (ví dụ: 10 phút cho file >500MB).
  - Sử dụng **chunking** (tách file thành nhiều phần nhỏ) nếu cần.
- **Kiểm Tra File Trước Khi Xóa**:
  - Thêm node `set` để so sánh checksum (MD5/SHA1) giữa file nguồn và đích trước khi xóa.
:::

---
## 📌 **Kết Luận**
Workflow này **giải phóng thời gian** của các sếp khỏi công việc lặp đi lặp lại, **giảm sai sót** và **tối ưu hóa quy trình quản lý file**. Với **cấu hình đơn giản** và **khả năng mở rộng**, nó hoàn toàn phù hợp cho doanh nghiệp cần **tự động hóa FTP** một cách an toàn và hiệu quả.

**🚀 Hãy áp dụng ngay và tiết kiệm thời gian cho team của mình!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**💡 Lưu ý cuối cùng**: Trước khi chạy trên sản phẩm, **test với file mẫu** và **monitor log** để đảm bảo không có lỗi!