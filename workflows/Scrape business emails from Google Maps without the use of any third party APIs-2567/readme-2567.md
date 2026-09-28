---
title: "🚀 Tự Động Hoàn Hảo: Scrape Email Doanh Nghiệp Từ Google Maps Miễn Phí (Không Cần API Nữa!)"
description: "Workflow n8n tự động tìm kiếm và trích xuất email doanh nghiệp từ Google Maps dựa trên danh sách từ khóa tự động hóa, giúp các sếp tiết kiệm thời gian lên tới 80% trong việc tìm kiếm leads. Kết quả được lưu trực tiếp vào Google Sheets với định dạng chuyên nghiệp."
slug: "tieu-dung-email-googlemaps-voi-n8n"
tags: [n8n, automation, sales, marketing, google-maps-scraper, no-code, lead-generation]
keywords: [scrape email google maps, tự động hóa tìm kiếm email doanh nghiệp, n8n workflow, không cần API, tự động hóa sales marketing, trích xuất email từ Google Maps]
---

# 🚀 **Tự Động Hoàn Hảo: Scrape Email Doanh Nghiệp Từ Google Maps (Không Cần API Nữa!)**

### **Giải Phóng Thời Gian Cho Các Sếp: Từ Tìm Kiếm Email Thủ Công Sang Tự Động Hóa 100%**
Hãy tưởng tượng một ngày không phải mất **giờ đồng hồ** để tìm kiếm email của các doanh nghiệp trên Google Maps, không phải lo lắng về việc bỏ lỡ leads quan trọng, và không phải phụ thuộc vào các API tốn kém. **Workflow này giải quyết tất cả!**

Với **n8n**, các sếp có thể tự động hóa quy trình trích xuất email từ Google Maps dựa trên **danh sách từ khóa** mà các sếp tự định nghĩa. Kết quả sẽ được **lưu trực tiếp vào Google Sheets**, sẵn sàng để phân tích và tiếp cận khách hàng một cách chuyên nghiệp.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên cài đặt n8n trên **VPS riêng** (Self-hosted) để đảm bảo tốc độ và an toàn.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian lên tới 80%** – Không phải thủ công tìm kiếm email trên Google Maps.
✅ **Dữ liệu chính xác và cập nhật** – Trích xuất email từ trang web doanh nghiệp, không phải dựa vào thông tin không chính xác trên Google Maps.
✅ **Tự động hóa liên tục** – Workflow chạy **24/7** mà không cần can thiệp của con người.
✅ **Lưu trữ chuyên nghiệp** – Kết quả được ghi vào **Google Sheets** với định dạng sẵn sàng sử dụng.
✅ **Không phụ thuộc API** – Không cần trả phí cho các dịch vụ API bên thứ ba.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản Google** (để sử dụng **Google Sheets** và **Google Maps API** – mặc dù không cần API, nhưng cần tài khoản để truy cập).
✔ **Danh sách từ khóa (queries)** – Các từ khóa liên quan đến ngành nghề mà các sếp muốn tìm kiếm (ví dụ: "cửa hàng café Hà Nội", "công ty marketing TP.HCM").
✔ **Google Sheet** – Một bảng Google Sheets để lưu trữ kết quả (các sếp có thể tạo mới hoặc chọn sheet đã có).
✔ **Thời gian chờ (optional)** – Để tránh bị chặn bởi Google, các sếp có thể điều chỉnh thời gian chờ giữa các yêu cầu (mặc định là **2 giây**).

---
:::note[LƯU Ý QUAN TRỌNG]
- **Không cần API** – Workflow này **không sử dụng API nào** của Google, nên không bị giới hạn về số lượng yêu cầu.
- **Tốc độ nhanh** – Với VPS, workflow có thể chạy **liên tục** mà không bị gián đoạn.
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể **import** workflow từ file JSON hoặc **copy/paste** JSON vào **n8n Editor**:
1. Mở **n8n Editor** trên trang web hoặc máy chủ self-hosted.
2. Nhấp vào **"Import"** và chọn file JSON (hoặc paste JSON từ [đây](https://n8n.io/workflows/2567)).
3. Chọn **"Import"** để hoàn tất.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **18 node** và cần cấu hình một số phần quan trọng:

##### **A. Cấu Hình "Run workflow" (Manual Trigger)**
- **Node:** *"Run workflow" (manualTrigger)*
- **Cách làm:**
  1. Mở node này và nhấp vào **"Edit"** (bút chì).
  2. Thêm **danh sách từ khóa** vào trường `data` (ví dụ: `["café Hà Nội", "công ty marketing TP.HCM", "cửa hàng điện thoại"]`).
  3. **Lưu** và kích hoạt workflow.

##### **B. Cấu Hình Google Sheets**
- **Node:** *"Save emails to Google Sheet" (googleSheets)*
- **Cách làm:**
  1. Nhấp vào **"Credentials"** và chọn tài khoản Google đã kết nối.
  2. Trong **"Key Parameters"**, chọn:
     - **Operation:** `append` (thêm dữ liệu mới vào sheet).
     - **Sheet Name:** Tên sheet mà các sếp muốn lưu kết quả (ví dụ: `Email_Leads`).
     - **Range:** `A1:A` (để ghi dữ liệu từ hàng đầu tiên).
  3. **Lưu** và kiểm tra sheet để đảm bảo kết nối thành công.

##### **C. Cấu Hình Thời Gian Chờ (Optional)**
- **Node:** *"Wait between executions" (wait)*
- **Cách làm:**
  - Mặc định là **2 giây**, nhưng các sếp có thể tăng lên (ví dụ: **5 giây**) để tránh bị chặn bởi Google.
  - Nhấp vào node và chỉnh sửa giá trị `duration` (ví dụ: `5000` ms = 5 giây).

##### **D. Cấu Hình Scraper (Workflow Con)**
- **Node:** *"Execute scraper for query" (executeWorkflow)*
- **Cách làm:**
  - Workflow con này sẽ tự động chạy khi có yêu cầu từ node *"Run workflow"*.
  - Các sếp **không cần chỉnh sửa** workflow con này, chỉ cần đảm bảo nó được **kích hoạt**.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run (Kiểm Tra Dữ Liệu Mẫu):**
   - Nhấp vào nút **"Execute"** trên node *"Run workflow"* để chạy thử với một từ khóa.
   - Kiểm tra **Google Sheets** xem kết quả có xuất hiện không.
2. **Bật Active Workflow:**
   - Sau khi kiểm tra thành công, các sếp có thể **bật workflow** để chạy liên tục.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tối Ưu Hóa Danh Sách Từ Khóa:**
   - Sử dụng **ChatGPT** để tự động sinh ra danh sách từ khóa phù hợp (xem [video hướng dẫn](https://youtu.be/HaiO-UeiKBA)).
   - Ví dụ: Nếu các sếp kinh doanh **thiết bị y tế**, có thể sử dụng từ khóa như:
     ```
     ["cửa hàng thiết bị y tế Hà Nội", "công ty bán máy xạ hình TP.HCM", "siêu thị y tế Bình Dương"]
     ```

2. **Lọc Email Chỉnh Xác:**
   - Workflow đã có **regex mặc định** để lọc email không hợp lệ, nhưng các sếp có thể **cập nhật** nó trong node *"Filter irrelevant emails"* để phù hợp với ngành nghề.
   - Ví dụ: Nếu các sếp muốn **bỏ email từ domain @gmail.com**, có thể chỉnh sửa regex như:
     ```regex
     ^[^\s@]+@(?!gmail\.com$)[^\s@]+$
     ```

3. **Gửi Kết Quả Sang Slack/Email:**
   - Sau khi lưu vào Google Sheets, các sếp có thể **kết nối với Slack** hoặc **gửi email tự động** thông báo khi có dữ liệu mới.
   - **Cách làm:**
     - Thêm node **Slack** hoặc **Email** sau node *"Save emails to Google Sheet"*.
     - Cấu hình để gửi thông báo khi có dữ liệu mới.

4. **Lưu Log Hoạt Động:**
   - Để theo dõi quá trình chạy, các sếp có thể thêm node **Google Drive** hoặc **Google Docs** để lưu **log** của workflow.
   - Ví dụ: Lưu thông tin như:
     ```
     - Thời gian chạy: [YYYY-MM-DD HH:MM:SS]
     - Từ khóa: [café Hà Nội]
     - Số email trích xuất: [15]
     - Trạng thái: [Thành công/Không thành công]
     ```

---

### 📌 **Kết Luận: Hãy Bắt Đầu Tự Động Hóa Ngay!**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào **strategy marketing** và **tăng trưởng doanh nghiệp** thay vì mất công tìm kiếm email thủ công. Với **n8n**, các sếp có thể:
✔ **Tự động hóa 100%** quy trình trích xuất email.
✔ **Không phụ thuộc API** và không bị giới hạn số lượng.
✔ **Lưu trữ dữ liệu chuyên nghiệp** vào Google Sheets.
✔ **Kết nối với nhiều dịch vụ khác** (Slack, Email, CRM...).

**Hành động ngay hôm nay!**
1. **Import workflow** vào n8n.
2. **Cấu hình Google Sheets** và danh sách từ khóa.
3. **Bật workflow** và bắt đầu **tự động hóa tìm kiếm leads**!

👉 [Tải workflow từ n8n.io](https://n8n.io/workflows/2567)
👉 [Xem video hướng dẫn chi tiết](https://youtu.be/HaiO-UeiKBA)

**Các sếp sẵn sàng tự động hóa chưa?** 🚀