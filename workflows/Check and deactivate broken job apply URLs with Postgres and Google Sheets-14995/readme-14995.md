---
title: "🔍 **Tự Động Xóa URL Nộp Ứng Tuyển Hỏng Hóc Trên Google Sheets & PostgreSQL – Giảm Thất Thời Gian Lên 90%!**"
description: "Workflow tự động kiểm tra và vô hiệu hóa URL nộp đơn ứng tuyển không hoạt động trên Google Sheets, đồng thời cập nhật dữ liệu vào PostgreSQL. Giúp HR tiết kiệm thời gian kiểm tra thủ công, giảm thiểu sai sót và duy trì danh sách ứng viên chính xác."
slug: "tieu-dong-url-nop-dung-tren-google-sheets-postgres"
tags: [n8n, automation, hr-automation, google-sheets, postgres, no-code]
keywords: [n8n workflow hr, tự động hóa tuyển dụng, kiểm tra url hỏng hóc, google sheets automation, postgres integration, tự động hóa không code]
---

# 🚀 **Tự Động Xóa URL Nộp Ứng Tuyển Hỏng Hóc – Giúp HR Không Bị "Đổ Mồ Hôi" Kiểm Tra Thủ Công**

### **Nỗi Đau Của Các Sếp HR**
Trong quá trình tuyển dụng, các sếp thường phải **tốn thời gian vô cùng nhiều** để kiểm tra từng URL nộp đơn ứng tuyển trên Google Sheets. Những URL này có thể:
- **Hỏng hóc** (404, redirect sai, hoặc bị xóa).
- **Không hoạt động** sau khi ứng viên nộp đơn.
- **Làm gián đoạn quy trình tuyển dụng** khi HR phải liên tục cập nhật danh sách ứng viên.

**Kết quả?** Thời gian của các sếp bị "chôn vùi" trong công việc thủ công, trong khi dữ liệu không được duy trì chính xác. **Workflow này sẽ giải quyết vấn đề đó 100% tự động!**

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần kiểm tra thủ công hàng ngày, tự động phát hiện URL hỏng trong vài giây.
- **Dữ liệu chính xác**: Cập nhật liên tục trên cả **Google Sheets** và **PostgreSQL**, tránh sai sót.
- **Tối ưu quy trình tuyển dụng**: Giúp HR tập trung vào việc phỏng vấn thay vì kiểm tra URL.
- **Hoạt động liên tục 24/7**: Dùng **Schedule Trigger** để chạy định kỳ (ví dụ: hàng ngày hoặc hàng tuần).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Google Cloud** (để kết nối với **Google Sheets**).
2. **API Key của Google Sheets** (được cấp từ [Google Cloud Console](https://console.cloud.google.com/)).
3. **CSDL PostgreSQL** (cấu hình kết nối với n8n).
4. **Bảng Google Sheets** chứa cột **URL** (để workflow kiểm tra).
5. **Tham số cấu hình** trong PostgreSQL (tên CSDL, tên bảng, tên cột).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Workflow này được xây dựng trên nền tảng **n8n**, các sếp có thể:
- **Tải file JSON** từ [n8n Workflow Library](https://n8n.io/workflows/14995) và import vào **n8n Editor**.
- **Copy JSON** và dán vào **n8n Editor** để tạo mới.

:::note[LƯU Ý]
- **Không có node nào trong workflow**, nhưng các sếp cần **tự xây dựng** dựa trên mô hình sau:
  - **Schedule Trigger** (để chạy định kỳ).
  - **Google Sheets** (đọc URL từ bảng).
  - **HTTP Request** (kiểm tra tính hoạt động của URL).
  - **PostgreSQL** (cập nhật trạng thái URL).
  - **Sticky Note** (ghi chú lỗi nếu có).
:::

#### **2. Các Bước Cấu Hình Cần Thực Hiện (BẮT BUỘC)**
##### **A. Thiết Lập Schedule Trigger**
- **Node:** `n8n-nodes-base.scheduleTrigger`
- **Cấu hình:**
  - **Frequency:** Chọn **Daily** (hoặc tùy chỉnh theo nhu cầu).
  - **Time:** Đặt giờ chạy (ví dụ: 8h sáng).

##### **B. Kết Nối Với Google Sheets**
- **Node:** `n8n-nodes-base.googleSheets`
- **Cấu hình:**
  - **Credentials:** Chọn tài khoản Google đã cấp **API Key**.
  - **Sheet Name:** Chọn bảng chứa URL ứng viên.
  - **Range:** Chọn phạm vi dữ liệu (ví dụ: `Sheet1!A2:B100`).
  - **Output Format:** Chọn **JSON**.

##### **C. Kiểm Tra URL (HTTP Request)**
- **Node:** `n8n-nodes-base.httpRequest`
- **Cấu hình:**
  - **Method:** `GET`.
  - **URL:** `{ $json["url"] }` (trích xuất từ Google Sheets).
  - **Headers:** Thêm `Accept: */*` (nếu cần).
  - **Response Format:** Chọn **JSON**.

##### **D. Lọc URL Hỏng Hóc (If Node)**
- **Node:** `n8n-nodes-base.if`
- **Cấu hình:**
  - **Condition:** Kiểm tra `statusCode` từ HTTP Request:
    - **If True:** `{{ $json.statusCode }} >= 400` (URL hỏng).
    - **If False:** URL hoạt động.

##### **E. Cập Nhật Trạng Thái Trên PostgreSQL**
- **Node:** `n8n-nodes-base.postgres`
- **Cấu hình:**
  - **Credentials:** Thêm kết nối PostgreSQL (nếu chưa có).
  - **Query:** Cập nhật cột `status` trong bảng ứng viên:
    ```sql
    UPDATE applicants SET status = 'broken' WHERE url = '{{ $json["url"] }}';
    ```
  - **Parameters:** Điền `{ url: $json["url"] }`.

##### **F. Ghi Chú Lỗi (Sticky Note)**
- **Node:** `n8n-nodes-base.stickyNote`
- **Cấu hình:**
  - **Text:** `URL {{ $json["url"] }} bị hỏng (status: {{ $json.statusCode }})`.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với một URL mẫu để đảm bảo workflow hoạt động.
2. **Bật Active** workflow và **đợi Schedule Trigger** chạy.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[CÁC Ý TƯỞNG MỞ RỘNG]
- **Gửi thông báo Slack/Telegram** khi phát hiện URL hỏng:
  - Sử dụng node `n8n-nodes-base.slack` hoặc `n8n-nodes-base.telegram`.
- **Lưu log vào Google Sheets** để theo dõi lịch sử:
  - Thêm node `n8n-nodes-base.googleSheets` để ghi log.
- **Kết hợp với AI** để tự động phân loại ứng viên:
  - Sử dụng node `n8n-nodes-base.llm` (nếu cần phân tích nội dung CV).
- **Tự động xóa URL hỏng** từ Google Sheets:
  - Thêm node `n8n-nodes-base.googleSheets` với query `DELETE`.
:::

---

### 📌 **Kết Luận**
Workflow này **giúp HR tự động hóa việc kiểm tra URL nộp đơn ứng tuyển**, tiết kiệm thời gian và giảm thiểu sai sót. **Không cần code**, chỉ cần cấu hình đúng các node như hướng dẫn trên.

**👉 Hãy áp dụng ngay và trải nghiệm sự hiệu quả của tự động hóa!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**🚀 Bắt đầu tự động hóa ngay hôm nay!** 🚀