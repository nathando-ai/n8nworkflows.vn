---
title: "🚀 Tự Động Hóa Optimize Thời Gian Gửi Email Klaviyo & Báo Cáo Tự Động bằng Gmail (AI Tóm Tắt)"
description: "Workflow tự động phân tích lịch sử gửi email Klaviyo để xác định thời gian gửi tối ưu cho từng nhóm khách hàng, gửi báo cáo hàng tuần tự động qua Gmail với hình ảnh biểu đồ và xếp hạng. Giúp các sếp tiết kiệm 10+ giờ/tháng phân tích thủ công."
slug: "tieu-dong-hoa-optimize-thoi-gian-gui-email-klaviyo-bang-gmail"
tags: [n8n, automation, klaviyo, gmail, email-marketing, no-code, ai-summarization, self-hosted]
keywords: [n8n workflow klaviyo, tự động hóa email marketing, optimze thời gian gửi email, báo cáo klaviyo tự động, gmail automation, klaviyo api]
---

# 🚀 **Tự Động Hóa Optimize Thời Gian Gửi Email Klaviyo & Báo Cáo Tự Động bằng Gmail**

## **💡 Giải Phá Nỗi Đau Của Các Sếp**
Bạn đã bao giờ phải:
- **Phân tích thủ công** hàng trăm email gửi qua Klaviyo để tìm thời gian gửi tối ưu?
- **Mất thời gian** so sánh tỷ lệ mở và click giữa các nhóm khách hàng?
- **Không biết** liệu thời gian gửi hiện tại có thực sự hiệu quả không?
- **Bị quên** gửi báo cáo tuần cho team hoặc khách hàng?

Workflow này **giải quyết tất cả** bằng cách:
✅ **Tự động phân tích** lịch sử gửi email Klaviyo trong 90 ngày qua.
✅ **Xếp hạng thời gian gửi** dựa trên tỷ lệ mở và click cho từng nhóm khách hàng.
✅ **Gửi báo cáo HTML đẹp mắt** hàng tuần qua Gmail với biểu đồ và xếp hạng.
✅ **Cảnh báo lỗi** ngay khi workflow gặp sự cố.

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tháng** phân tích thủ công.
- **Tăng tỷ lệ mở & click** lên đến 20% bằng cách gửi email vào thời điểm tối ưu.
- **Báo cáo tự động** hàng tuần, không cần nhớ hoặc làm thủ công.
- **Hệ thống hóa dữ liệu** Klaviyo với Gmail, dễ theo dõi và chia sẻ.
- **Cảnh báo lỗi tức thời** nếu workflow gặp sự cố.
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản Klaviyo** với quyền API:
   - **API Key Private** (có scope: `campaigns:read`, `lists:read`, `metrics:read`).
   - **Tìm API Key** tại: *Klaviyo → Account → Settings → API Keys*.
2. **Tài khoản Gmail** (để nhận báo cáo và cảnh báo lỗi):
   - **OAuth2 Credential** cho hai node Gmail (Send Report và Error Alert).
   - **Địa chỉ email nhận báo cáo** (cần thay đổi trong node `Gmail — Send Report`).
   - **Địa chỉ email cảnh báo lỗi** (có thể giống hoặc khác với địa chỉ trên).
3. **Thông tin chuyển đổi (conversion_metric_id)**:
   - Nếu sử dụng **Shopify**, mặc định là `X7ghUW` (Placed Order).
   - Nếu không, tìm ID tại: *Klaviyo → Account → Settings → Custom Metrics*.
4. **Hệ thống tự động hóa n8n** (Self-hosted):
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).
:::

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. Tải workflow từ [n8n.io/workflows/15552](https://n8n.io/workflows/15552) (chọn **Export JSON**).
2. Trên n8n Editor, nhấn **Import** → Chọn file JSON vừa tải.
3. Xác nhận import hoàn tất.

#### **Phương pháp 2: Copy/Paste JSON**
1. Trên trang workflow trên n8n.io, nhấn **Export JSON** → Copy toàn bộ mã.
2. Trên n8n Editor, nhấn **Import** → Chọn **Paste JSON** và dán mã vào.
3. Xác nhận import.

---
### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này có **5 điểm cần cấu hình kỹ** để hoạt động chính xác:

#### **🔑 1. Cấu Hình Klaviyo API Key**
- **Node**: `Get Sent Campaigns`, `Fetch Lists`, `Get Campaign Stats`.
- **Hướng dẫn**:
  1. Mở node `Get Sent Campaigns` → Tab **Credentials**.
  2. Chọn **Create New** → Nhập tên (ví dụ: `Klaviyo API`).
  3. Chọn loại **HTTP Request** → Nhập **API Key** từ Klaviyo.
  4. Lặp lại cho hai node còn lại (`Fetch Lists` và `Get Campaign Stats`).

#### **📧 2. Cấu Hình Gmail OAuth2**
- **Node**: `Gmail — Send Report` và `Gmail — Error Alert`.
- **Hướng dẫn**:
  1. Mở node `Gmail — Send Report` → Tab **Credentials**.
  2. Nhấn **Create New** → Chọn **Gmail OAuth2**.
  3. Đăng nhập tài khoản Gmail muốn nhận báo cáo.
  4. Lặp lại cho node `Gmail — Error Alert` (sử dụng tài khoản khác nếu muốn cảnh báo riêng).
  5. **Lưu ý**: Hai node này **không thể dùng chung credential** để đảm bảo cảnh báo lỗi hoạt động.

#### **📧 3. Địa Chỉ Email Nhận Báo Cáo**
- **Node**: `Gmail — Send Report`.
- **Hướng dẫn**:
  - Mở tab **Options** → Tìm trường `To` (địa chỉ email nhận báo cáo).
  - Thay đổi từ `user@example.com` thành địa chỉ của bạn (ví dụ: `marketing@doanhnghiep.com`).

#### **📧 4. Địa Chỉ Email Cảnh Báo Lỗi**
- **Node**: `Gmail — Error Alert`.
- **Hướng dẫn**:
  - Mở tab **Options** → Tìm trường `To` (địa chỉ email cảnh báo).
  - Thay đổi từ `user@example.com` thành địa chỉ monitoring (có thể giống hoặc khác với địa chỉ báo cáo).

#### **📊 5. Chuyển Đổi Metric ID (Nếu Không Sử Dụng Shopify)**
- **Node**: `Get Campaign Stats`.
- **Hướng dẫn**:
  1. Mở node `Get Campaign Stats` → Tab **Options**.
  2. Tìm trường **Body** → Thay đổi `X7ghUW` thành ID của bạn (tìm tại *Klaviyo → Account → Settings → Custom Metrics*).
  3. **Lưu ý**: Nếu không thay đổi, workflow sẽ sử dụng mặc định Shopify.

---
### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run** (kiểm tra trước khi chạy chính thức):
   - Nhấn **Run Workflow** → Chọn **Test Execution**.
   - Kiểm tra các node quan trọng:
     - `Get Sent Campaigns` (có trả về dữ liệu không?).
     - `Gmail — Send Report` (báo cáo có gửi được không?).
     - `Error Trigger` (nếu có lỗi, có cảnh báo không?).
2. **Bật Active**:
   - Sau khi test thành công, nhấn **Active** để workflow chạy tự động hàng tuần.

---
## ✍️ **Mẹo & Gợi Ý Nâng Cao**

### **1. Thêm Báo Cáo Định Kỳ Cho Team**
- **Cách làm**:
  - Sử dụng node **Schedule Trigger** thêm để chạy workflow vào ngày khác (ví dụ: Thứ 3 hàng tuần).
  - Cấu hình **Gmail — Send Report** gửi cho nhiều địa chỉ (ví dụ: `team@doanhnghiep.com`).

### **2. Lưu Log Lỗi Vào Google Sheets**
- **Cách làm**:
  - Thêm node **Google Sheets** sau `Error Trigger`.
  - Cấu hình ghi lỗi vào sheet mới với cột: `Thời gian`, `Lỗi`, `Node bị lỗi`.

### **3. Kết Nối Slack/Telegram Cảnh Báo Lỗi**
- **Cách làm**:
  - Thêm node **Slack Webhook** hoặc **Telegram Bot** sau `Error Trigger`.
  - Cấu hình gửi tin nhắn cảnh báo khi workflow lỗi.

### **4. Tùy Chỉnh Thời Gian Gửi Báo Cáo**
- **Cách làm**:
  - Mở node **Schedule — Weekly Monday** → Thay đổi thời gian (ví dụ: 9h sáng thay vì 8h).

### **5. Thêm Biểu Đồ Tương Tác (Interactive Chart)**
- **Cách làm**:
  - Thay node `Format Email Report` bằng **Google Charts** hoặc **Tableau**.
  - Sử dụng API của Klaviyo để vẽ biểu đồ trực tiếp trong email.

---
## 📌 **Kết Luận**
Workflow này **giúp các sếp tự động hóa toàn bộ quy trình phân tích và báo cáo Klaviyo**, tiết kiệm thời gian và tăng hiệu quả marketing. **Chỉ cần cấu hình 5 bước đơn giản**, workflow sẽ tự động:
✔ **Phân tích** thời gian gửi tối ưu.
✔ **Gửi báo cáo** hàng tuần qua Gmail.
✔ **Cảnh báo lỗi** ngay khi có sự cố.

**Hành động ngay hôm nay!**
1. **Cài đặt n8n trên VPS** (để workflow chạy 24/7).
2. **Import workflow** và cấu hình Klaviyo + Gmail.
3. **Bật Active** và bắt đầu tự động hóa!

👉 [**Tải workflow ngay**](https://n8n.io/workflows/15552) và bắt đầu tối ưu hóa email marketing của bạn!