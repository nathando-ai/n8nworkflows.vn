---
title: "🚀 Tự Động Hóa Theo Dõi Thị Trường Công Việc Upwork: Scraper → Google Sheets (Không Cần Code)"
description: "Workflow tự động hóa 24/7 để scrap tất cả công việc mới trên Upwork, lọc dữ liệu cần thiết và ghi vào Google Sheets để theo dõi xu hướng thị trường. Giúp freelancer, nhà tuyển dụng và doanh nghiệp tiết kiệm thời gian lên tới 10 giờ/tuần."
slug: "tu-dong-hoa-theo-doi-cong-viec-upwork"
tags: [n8n, automation, upwork, google-sheets, apify, no-code]
keywords: [tự động hóa upwork, scrap công việc upwork, theo dõi xu hướng thị trường, n8n workflow, tự động hóa không code]
---

# 🚀 **Tự Động Hóa Theo Dõi Thị Trường Công Việc Upwork: Scraper → Google Sheets**

## **🔍 Nỗi Đau Của Các Sếp**
Bạn là freelancer, nhà tuyển dụng hoặc doanh nghiệp cần theo dõi xu hướng thị trường công việc trên Upwork? Thì việc **quét thủ công hàng ngày** để cập nhật công việc mới, lọc thông tin cần thiết và ghi vào bảng tính là **tốn thời gian và dễ bỏ lỡ cơ hội**. Với workflow này, bạn sẽ:
✅ **Tiết kiệm 10+ giờ/tuần** không phải quét website.
✅ **Nhận dữ liệu sạch** (tên công việc, kỹ năng, ngày đăng, link) được tự động sắp xếp.
✅ **Theo dõi xu hướng thị trường** bằng cách phân tích dữ liệu trên Google Sheets.
✅ **Cập nhật liên tục** 24/7 mà không cần can thiệp thủ công.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính bảo mật và khả năng mở rộng.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%**: Không cần can thiệp thủ công, workflow chạy tự động theo lịch trình.
- **Dữ liệu sạch và chuẩn**: Lọc ra thông tin cần thiết (tên công việc, kỹ năng, ngày đăng, link) và sắp xếp theo định dạng dễ đọc.
- **Theo dõi xu hướng thị trường**: Dữ liệu được ghi vào Google Sheets, giúp phân tích xu hướng công việc, kỹ năng hot và thời điểm đăng công việc.
- **Cập nhật liên tục**: Nhận thông tin mới nhất ngay khi công việc mới được đăng trên Upwork.
- **Tích hợp dễ dàng**: Sau khi hoàn thành, bạn có thể kết nối với Slack, Telegram, hoặc Airtable để nhận thông báo ngay khi có công việc mới.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Upwork** (để xác thực scraper).
2. **Tài khoản Apify** (để sử dụng actor scraper Upwork):
   - [Tạo tài khoản Apify miễn phí](https://apify.com/)
   - [Tìm và sử dụng actor "Upwork Jobs Scraper"](https://apify.com/actor/upwork-jobs-scraper) (hoặc tạo actor riêng với filter kỹ năng).
3. **Tài khoản Google Sheets** và **OAuth 2.0 API Key** để kết nối với Google Sheets:
   - [Cài đặt OAuth 2.0 cho Google Sheets](https://developers.google.com/sheets/api/quickstart/python).
4. **Workflow n8n** (cài đặt trên máy chủ hoặc VPS).
5. **Thời gian** để cấu hình và test workflow (khoảng 15-30 phút).
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. Tải workflow từ [n8n.io/workflows/4734](https://n8n.io/workflows/4734) (ấn "Download JSON").
2. Trên giao diện n8n Editor, nhấn **"Import"** và chọn file JSON vừa tải.
3. Chọn **"Create new workflow"** và nhấn **"Import"**.

#### **Phương pháp 2: Copy/Paste JSON**
1. Trên trang [n8n.io/workflows/4734](https://n8n.io/workflows/4734), nhấn **"Copy JSON"** (góc trên bên phải).
2. Trên n8n Editor, nhấn **"Import"** → **"Paste JSON"** và dán nội dung vừa copy.
3. Chọn **"Create new workflow"** và nhấn **"Import"**.

---
### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **4 node chính**, mỗi node cần cấu hình cụ thể như sau:

#### **🕒 Node 1: `Check Upwork Jobs - Trigger` (ScheduleTrigger)**
- **Cấu hình**:
  - Chọn **"Schedule"** như trigger.
  - Thiết lập **thời gian chạy** (ví dụ: **mỗi 1 giờ** hoặc **mỗi ngày**).
  - **Lưu ý**: Thời gian chạy phải phù hợp với nhu cầu theo dõi (ví dụ: chạy vào giờ làm việc để tránh tải quá nhiều dữ liệu).
  - **Mẹo**: Để tránh trùng lặp, bạn có thể chạy vào **giờ không cao điểm** (ví dụ: 3h sáng).

#### **🌐 Node 2: `Fetch Upwork Jobs using Apify` (HTTP Request)**
- **Cấu hình**:
  - **Method**: `POST`.
  - **URL**: URL của actor Apify (ví dụ: `https://api.apify.com/v2/actors/<actor-id>/runs`).
    - Để lấy **actor ID**, mở actor trên Apify → URL sẽ có dạng `https://apify.com/<actor-id>/upwork-jobs-scraper`.
  - **Headers**:
    - `Authorization`: `Bearer <API_TOKEN>` (lấy từ [Apify Dashboard](https://apify.com/accounts/settings)).
    - `Content-Type`: `application/json`.
  - **Body (JSON)**:
    ```json
    {
      "input": {
        "keywords": ["AI", "Python", "Design"], // Thêm các keyword cần theo dõi
        "limit": 50, // Số lượng công việc scrap mỗi lần
        "proxy": "apify" // Sử dụng proxy của Apify để tránh bị chặn
      }
    }
    ```
  - **Lưu ý**:
    - Thay thế `<actor-id>` và `<API_TOKEN>` bằng thông tin thực tế.
    - Nếu muốn **lọc kỹ năng cụ thể**, chỉnh sửa phần `keywords` trong `input`.
    - **Proxy**: Apify cung cấp proxy miễn phí, nhưng nếu scrap nhiều, có thể cần mua gói premium.

#### **✏️ Node 3: `Format scrape Data` (Set)**
- **Cấu hình**:
  - Node này **lọc và định dạng dữ liệu** từ Apify.
  - **Cách cấu hình**:
    1. Nhấn **"Add Item"** và chọn **"Set"** (nếu chưa có).
    2. **Thêm các field cần giữ**:
       - `title` → `Job Title`.
       - `description` → `Description` (nếu cần).
       - `skills` → `Skills`.
       - `postedDate` → `Posted Date` (định dạng lại thành `YYYY-MM-DD`).
       - `link` → `Link`.
    3. **Xóa field không cần thiết** (ví dụ: `client`, `budget`).
  - **Mẹo**: Sử dụng **Expressions** để định dạng ngày:
    ```plaintext
    {{ $json.postedDate | date('YYYY-MM-DD') }}
    ```

#### **📄 Node 4: `Log Jobs to Google Sheets` (Google Sheets)**
- **Cấu hình**:
  - **Credentials**: Chọn `googleSheetsOAuth2Api` (đã cấu hình trước).
  - **Operation**: `append` (thêm dữ liệu vào cuối sheet).
  - **Sheet Name**: Tên sheet cần ghi dữ liệu (ví dụ: `Upwork Jobs`).
  - **Range**: `A1` (để ghi từ ô A1).
  - **Headers**: Chọn **"Use first row as headers"** (để tự động tạo cột).
  - **Data**: Chọn **"JSON"** và chọn **fields** đã định dạng ở Node 3.
  - **Lưu ý**:
    - Đảm bảo **sheet đã tồn tại** và có **cột phù hợp** với fields của Node 3.
    - Nếu sheet chưa có, bạn có thể **tạo sheet mới** bằng cách:
      1. Nhấn **"Create new sheet"** trong Google Sheets.
      2. Thiết lập tên sheet và cột (ví dụ: `Job Title`, `Skills`, `Posted Date`, `Link`).

---
### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhấn **"Run Workflow"** để kiểm tra dữ liệu.
   - Kiểm tra **Google Sheets** xem dữ liệu có được ghi không.
2. **Active Workflow**:
   - Sau khi test thành công, nhấn **"Active"** để workflow chạy tự động theo lịch trình.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[CÁCH TIẾP CẬN THÊM]
1. **Nhận thông báo khi có công việc mới**:
   - Thêm **node Slack/Telegram** sau Node 4 để gửi thông báo khi có công việc mới.
   - **Cách làm**:
     - Thêm node **Slack Webhook** hoặc **Telegram Bot**.
     - Sử dụng **Expressions** để lọc công việc mới:
       ```plaintext
       {{ $json.postedDate > new Date('2023-10-01') }}
       ```
2. **Lọc và phân loại công việc**:
   - Sử dụng **node Conditional (IF)** để phân loại công việc theo kỹ năng (ví dụ: AI, Design, Marketing).
   - **Cách làm**:
     - Thêm node **Conditional** sau Node 3.
     - Tạo điều kiện:
       - Nếu `Skills` chứa `"AI"` → Ghi vào sheet `AI Jobs`.
       - Nếu `Skills` chứa `"Design"` → Ghi vào sheet `Design Jobs`.
3. **Tạo báo cáo định kỳ**:
   - Sử dụng **node Google Sheets** để tạo **báo cáo tổng hợp** (ví dụ: số lượng công việc theo tháng).
   - **Cách làm**:
     - Thêm node **Google Sheets** mới với **operation = "update"** (chỉnh sửa ô cụ thể).
     - Sử dụng **Expressions** để tính toán:
       ```plaintext
       {{ $json.length }} // Số lượng công việc mới
       ```
4. **Deduplicate (loại bỏ trùng lặp)**:
   - Sử dụng **node Set** hoặc **Google Apps Script** để loại bỏ công việc đã tồn tại.
   - **Cách làm**:
     - Thêm node **Set** trước Node 4.
     - Sử dụng **Expressions** để kiểm tra trùng lặp:
       ```plaintext
       {{ !$json.link.includes($previousOutput.link) }}
       ```
5. **Kết nối với Airtable**:
   - Thay thế node **Google Sheets** bằng **Airtable** để có giao diện dashboard đẹp hơn.
   - **Cách làm**:
     - Thêm node **Airtable** và cấu hình như với Google Sheets.
     - Sử dụng **base** và **table** phù hợp.

---

## 📌 **Kết Luận**
Workflow **Automated Job Market Tracker** là giải pháp **tự động hóa hoàn hảo** để theo dõi xu hướng thị trường công việc trên Upwork mà **không cần viết một dòng code**. Với việc chỉ cần **cấu hình vài bước**, các sếp sẽ:
✔ **Tiết kiệm thời gian** để tập trung vào công việc chính.
✔ **Nhận dữ liệu sạch** và dễ phân tích.
✔ **Cập nhật liên tục** mà không cần can thiệp thủ công.

**Hãy áp dụng ngay workflow này và bắt đầu theo dõi thị trường công việc một cách thông minh!** 🚀

---
**💡 Cần hỗ trợ thêm?**
- Liên hệ tác giả: [Yaron Been](https://www.linkedin.com/in/yaronbeen/)
- Xem thêm tutorial: [YouTube - Yaron Been](https://www.youtube.com/@YaronBeen/videos)