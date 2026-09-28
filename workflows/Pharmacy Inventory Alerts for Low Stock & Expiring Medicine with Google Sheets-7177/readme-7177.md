---
title: "🚨 **Cảnh Báo Thiếu Hàng & Thuốc Sắp Hết Hạn Cho Pharmacy - Tự Động Hóa 100% Không Code**"
description: "Workflow tự động hóa cảnh báo hàng tồn kho thấp và thuốc sắp hết hạn cho nhà thuốc bằng Google Sheets + Email, tiết kiệm thời gian kiểm tra thủ công hàng ngày. Giúp các sếp quản lý tồn kho hiệu quả, tránh thiếu hàng và giảm thiểu lãng phí thuốc."
slug: "pharmacy-inventory-alert-low-stock-expiry"
tags: [n8n, automation, pharmacy, google-sheets, email-alert]
keywords: [tự động hóa nhà thuốc, cảnh báo tồn kho thấp, thuốc sắp hết hạn, n8n workflow, quản lý tồn kho tự động]
---

# 🚨 **Tự Động Hóa Cảnh Báo Thiếu Hàng & Thuốc Sắp Hết Hạn Cho Pharmacy**

## **Nỗi Đau Của Các Sếp Nhà Thuốc**
Hàng ngày, các sếp phải **tốn thời gian kiểm tra thủ công** tồn kho, so sánh với ngưỡng an toàn, và **lo lắng về thuốc sắp hết hạn** (đặc biệt là thuốc đặc trị). Kết quả?
- **Thiếu hàng** → Khách hàng mất niềm tin, doanh thu giảm.
- **Thuốc hết hạn** → Lãng phí tài nguyên, vi phạm quy định y tế.
- **Làm việc thủ công** → Mệt mỏi, dễ xảy ra lỗi, không thể theo dõi 24/7.

**Workflow này giải quyết tất cả!** Với **Google Sheets + Email tự động**, các sếp sẽ **không bao giờ bỏ lỡ cảnh báo** về hàng thấp hoặc thuốc sắp hết hạn.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài **n8n trên VPS riêng** (Self-hosted) để tránh giới hạn của phiên bản cloud.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 2+ giờ/ngày** kiểm tra tồn kho thủ công.
✅ **Cảnh báo kịp thời** khi hàng dưới ngưỡng an toàn (cấu hình được).
✅ **Được thông báo 30 ngày trước** khi thuốc sắp hết hạn.
✅ **Email tự động** gửi cho quản lý, nhân viên kho.
✅ **Lưu lịch sử cảnh báo** trên Google Sheets để theo dõi.
✅ **Hoạt động 24/7** mà không cần can thiệp người dùng.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Cloud** (để kết nối với **Google Sheets**).
   - **Bước 1:** Tạo **Google Cloud Project** và kích hoạt **Google Sheets API**.
   - **Bước 2:** Tạo **Service Account** và tải **JSON Key File**.
   - **Bước 3:** Cấu hình **credentials "googleApi"** trong n8n (đường dẫn đến file JSON).
2. **Tài khoản Email SMTP** (để gửi cảnh báo).
   - **Lựa chọn:** Gmail (SMTP của Google), SendGrid, hoặc SMTP của nhà cung cấp hosting.
   - **Cấu hình credentials "smtp"** trong n8n (Host, Port, Username, Password, From Email).
3. **Google Sheet đã chuẩn bị** với **cấu trúc dữ liệu** như sau:
   | Thuốc Tên | Số Lượng | Ngưỡng An Toàn | Ngày Hết Hạn | Trạng Thái Cảnh Báo | Lần Cập Nhật |
   |-----------|----------|----------------|---------------|----------------------|----------------|
   | Paracetamol | 50       | 30             | 2025-05-15    | -                    | -              |

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Phương pháp 1:** Tải file JSON từ [link gốc](https://n8n.io/workflows/7177) và import vào **n8n Editor**.
- **Phương pháp 2:** Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/7177) và paste vào **n8n Editor** → **Import Workflow**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow gồm **6 node chính**, các sếp cần chú ý cấu hình sau:

##### **A. Node "Daily Stock Check" (Cron)**
- **Thiết lập lịch chạy:** 9:00 AM hàng ngày (hoặc thời gian phù hợp).
- **Lưu ý:** Nếu không muốn chạy hàng ngày, có thể thay bằng **Webhook** hoặc **Manual Trigger**.

##### **B. Node "Fetch Stock Data" (Google Sheets)**
- **Chọn credentials:** `googleApi` (đã cấu hình trước).
- **Tham số quan trọng:**
  - **Spreadsheet ID:** ID của Google Sheet (tìm trong URL: `https://docs.google.com/spreadsheets/d/[ID]/edit`).
  - **Sheet Name:** Tên tab trong Google Sheet (ví dụ: "Inventory").
  - **Range:** `Sheet1!A:E` (đảm bảo bao gồm tất cả cột cần kiểm tra).

##### **C. Node "Check Expiry Date and Low Stock" (Code)**
- **Mã JavaScript mặc định** đã kiểm tra:
  - **Số lượng < Ngưỡng An Toàn** → Đánh dấu `Trạng Thái Cảnh Báo = "Low Stock"`.
  - **Ngày Hết Hạn < 30 ngày** → Đánh dấu `Trạng Thái Cảnh Báo = "Expiring Soon"`.
- **Lưu ý:** Nếu cấu trúc Google Sheet khác, các sếp cần **sửa mã** trong node này.

##### **D. Node "Update Google Sheet" (Google Sheets)**
- **Chọn credentials:** `googleApi`.
- **Tham số:**
  - **Operation:** `update` (cập nhật trạng thái cảnh báo).
  - **Range:** `Sheet1!D2:D` (cột "Trạng Thái Cảnh Báo").

##### **E. Node "Send Email Alert" (Email Send)**
- **Chọn credentials:** `smtp` (đã cấu hình trước).
- **Tham số quan trọng:**
  - **To:** Email của quản lý hoặc nhân viên kho (ví dụ: `quanly@pharmacy.com`).
  - **Subject:** `"🚨 CẢNH BÁO: [Thuốc Tên] - [Trạng Thái]"` (ví dụ: `"🚨 CẢNH BÁO: Paracetamol - Thiếu Hàng"`).
  - **Body:** Nội dung email tự động (có thể tùy chỉnh thêm thông tin như số lượng còn lại, ngày hết hạn).

##### **F. Node "Wait For All Data" (Wait)**
- **Thời gian chờ:** 5 giây (đảm bảo dữ liệu từ Google Sheets được tải đầy đủ).

#### **3. Kích Hoạt ⚡️**
- **Test Run:** Chạy thử với dữ liệu mẫu để kiểm tra email cảnh báo.
- **Bật Active:** Sau khi kiểm tra thành công, **bật workflow** để chạy tự động hàng ngày.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tự động gửi báo cáo hàng tuần:**
   - Thêm **node Cron** chạy vào cuối tuần (ví dụ: Chủ Nhật 8:00 AM).
   - Sử dụng **node Code** để tổng hợp dữ liệu và gửi **Email tổng hợp** về tình trạng tồn kho.

2. **Kết nối với Slack/Telegram:**
   - Thêm **node Slack** hoặc **Telegram Bot** để cảnh báo ngay khi có sự kiện.

3. **Lưu log cảnh báo:**
   - Thêm **node Google Sheets** mới để ghi lại **lịch sử cảnh báo** (ngày giờ, loại cảnh báo, hành động đã thực hiện).

4. **Cấu hình ngưỡng cảnh báo động:**
   - Sử dụng **node Code** để tính toán ngưỡng an toàn dựa trên **thời gian sử dụng trung bình** của từng loại thuốc.

5. **Gửi cảnh báo SMS:**
   - Kết nối với **Twilio** hoặc **Viber API** để gửi tin nhắn SMS cho nhân viên.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp nhà thuốc, **tránh thiếu hàng và lãng phí thuốc**, đồng thời **tăng cường hiệu quả quản lý tồn kho** một cách hoàn toàn tự động. **Không cần code, không cần chuyên gia IT** – chỉ cần **n8n + Google Sheets + Email**, các sếp đã có một **hệ thống cảnh báo thông minh** hoạt động 24/7.

**🚀 Hãy áp dụng ngay và bắt đầu tự động hóa nhà thuốc của mình!**
Nếu có vấn đề, các sếp có thể **comment bên dưới** hoặc liên hệ với **Oneclick AI Squad** qua [đây](https://n8n.io/workflows/7177).

---
**#TựĐộngHóaPharmacy #N8NWorkflows #QuảnLýTồnKho #ThuốcSắpHếtHạn**