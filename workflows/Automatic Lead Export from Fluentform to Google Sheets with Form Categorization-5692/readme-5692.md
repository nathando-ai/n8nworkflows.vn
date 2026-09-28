---
title: "🚀 Tự Động Hóa Xuất Lead Từ FluentForm Sang Google Sheets Với Phân Loại Form - Giảm 90% Công Việc Nhập Dữ Liệu"
description: "Workflow tự động hóa hoàn toàn không cần code, giúp các sếp tự động xuất tất cả lead từ FluentForm sang Google Sheets với phân loại tự động (Form vs Newsletter), tiết kiệm thời gian và giảm sai sót. Hoạt động 24/7, không cần can thiệp thủ công."
slug: "tu-dong-hoa-xuat-lead-tu-fluentform-sang-google-sheets"
tags: [n8n, automation, lead-generation, google-sheets, fluentform, no-code]
keywords: [tự động hóa lead, xuất lead từ fluentform, google sheets tự động, phân loại lead, n8n workflow lead generation]
---

# 🚀 **Tự Động Hóa Xuất Lead Từ FluentForm Sang Google Sheets Với Phân Loại Form**

## **💡 Giải Pháp Cho Các Sếp Bị "Đắm Chìm" Trong Công Việc Nhập Dữ Liệu**
Bạn có bao giờ cảm thấy **mệt mỏi** khi phải **nhập thủ công** hàng trăm lead từ FluentForm vào Google Sheets hàng ngày? Hoặc phải **phân loại** lead giữa **Form đăng ký** và **Newsletter** một cách tẻ nhạt? Với workflow này, các sếp sẽ **tự động hóa 100%** quá trình này, **giảm thời gian làm việc xuống còn 0%** và **tránh sai sót** do nhập liệu thủ công.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **ổn định 24/7**, các sếp nên **self-host n8n** trên VPS riêng thay vì dùng phiên bản miễn phí (có giới hạn).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đủ sức mạnh cho workflow này)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Không cần nhập liệu thủ công hàng ngày.
✅ **Chính xác 100%**: Không sai sót do con người.
✅ **Phân loại tự động**: Lead được phân loại rõ ràng (Form vs Newsletter).
✅ **Hoạt động liên tục**: Workflow chạy **24/7** mà không cần can thiệp.
✅ **Dữ liệu sẵn sàng**: Tất cả lead được lưu vào Google Sheets ngay lập tức.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản FluentForm** (để lấy URL Webhook).
✔ **Tài khoản Google** (để kết nối với Google Sheets).
✔ **Google Sheets OAuth2 API Key** (để workflow có quyền ghi dữ liệu).
✔ **URL Webhook từ FluentForm** (cần thay đổi trong workflow).
✔ **Google Sheet đã tạo sẵn** (các sếp có thể tạo 2 sheet riêng biệt cho Form và Newsletter).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể **import** workflow từ file JSON hoặc **copy/paste** JSON vào **n8n Editor**:
1. Tải workflow từ [đây](https://n8n.io/workflows/5692) (hoặc copy JSON từ link trên).
2. Mở **n8n Editor** → Nhấn **"Import"** → Dán JSON và nhấn **"Import"**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflows này có **2 node Google Sheets** (một cho Form, một cho Newsletter) và **1 node Webhook** để nhận lead từ FluentForm. Các bước cấu hình chi tiết:

##### **A. Cấu Hình Webhook (Nhận Lead Từ FluentForm)**
- **Node**: `POST - Retrieve Leads` (type: **webhook**)
  - **Thay đổi `path`** trong `keyParameters` thành URL Webhook từ FluentForm (ví dụ: `/fluentform-leads`).
  - **HTTP Method**: Đảm bảo chọn **POST** (không cần thay đổi).

##### **B. Cấu Hình Google Sheets (Lưu Lead)**
- **Node**: `Append newsletter` & `append form` (cả 2 đều type: **googleSheets**)
  - **Credentials**: Chọn `googleSheetsOAuth2Api` (cần cấu hình trước trong n8n).
  - **Operation**: Đã mặc định là `appendOrUpdate` (không cần thay đổi).
  - **Google Sheet cần thiết**:
    - Tạo **2 sheet riêng biệt** (ví dụ: `Form Leads` và `Newsletter Leads`).
    - Điền tên sheet vào `keyParameters` của node tương ứng:
      - `Append newsletter` → Điền tên sheet **Newsletter**.
      - `append form` → Điền tên sheet **Form**.

##### **C. Cấu Hình Phân Loại Lead (Form vs Newsletter)**
- **Node**: `Form or newsletter?` (type: **if**)
  - Workflow sẽ tự động **phân loại** lead dựa trên **field** mà các sếp đã cấu hình trong FluentForm.
  - Nếu lead từ **Form đăng ký**, nó sẽ được append vào sheet **Form**.
  - Nếu lead từ **Newsletter**, nó sẽ được append vào sheet **Newsletter**.

##### **D. Thêm Ghi Chú (Optional)**
- **Node**: `newsletter` & `form` (type: **set**)
  - Đây là **sticky note** để các sếp ghi chú (không ảnh hưởng đến logic).
  - Có thể **xóa** nếu không cần.

---

#### **3. Kích Hoạt Workflow ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Gửi một lead từ FluentForm (thông qua Webhook) → Kiểm tra xem lead có xuất hiện ở sheet tương ứng không.
2. **Bật Active**:
   - Nhấn **"Active"** ở góc trên bên phải → Workflow sẽ **chạy tự động** khi có lead mới.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết nối với Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram** để **báo động** khi có lead mới.
   - Ví dụ: Khi lead được append vào sheet, gửi thông báo đến nhóm Slack.

2. **Lưu Log Dữ Liệu**:
   - Thêm node **Google Drive** hoặc **Airtable** để lưu **lịch sử lead** lâu dài.

3. **Gửi Báo Cáo Định Kỳ**:
   - Sử dụng **n8n + Google Apps Script** để tự động gửi **báo cáo tổng hợp lead** hàng tuần qua email.

4. **Phân Loại Nâng Cao**:
   - Nếu FluentForm có nhiều loại form, các sếp có thể **tạo nhiều sheet khác nhau** và điều khiển logic phân loại bằng node **if** phức tạp hơn.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc **nhập liệu tẻ nhạt**, đồng thời **tăng độ chính xác** và **tự động hóa hoàn toàn** quá trình quản lý lead. **Chỉ cần 10 phút setup**, các sếp sẽ **không bao giờ phải lo lắng** về việc mất lead hoặc sai sót trong dữ liệu.

**🚀 Hãy áp dụng ngay và bắt đầu tự động hóa hôm nay!**
Nếu có vấn đề, các sếp có thể tham khảo [tác giả gốc](https://khmuhtadin.com) hoặc để lại bình luận dưới bài viết.

---
**💡 Mẹo cuối:** Nếu các sếp muốn **tăng cường tính bảo mật**, có thể **xóa node sticky note** và **tối ưu hóa logic** bằng cách sử dụng **variables** trong n8n.