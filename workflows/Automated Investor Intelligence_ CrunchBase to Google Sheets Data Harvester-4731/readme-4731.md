---
title: "🚀 Tự Động Hóa Thu Thập Dữ Liệu Nhà Đầu Tư từ Crunchbase Sang Google Sheets (Không Cần Code)"
description: "Workflow tự động hóa 100% miễn phí giúp các sếp startup, đầu tư hoặc marketing tự động lấy dữ liệu nhà đầu tư từ Crunchbase hàng ngày và lưu vào Google Sheets để phân tích chiến lược đầu tư, outreach hoặc benchmarking. Giúp tiết kiệm thời gian lên đến 10 giờ/tuần và giảm thiểu sai sót nhân sự."
slug: "tieu-dong-hoa-thu-thap-du-lieu-nha-dau-tu-crunchbase-sang-google-sheets"
tags: [n8n, automation, crunchbase, google-sheets, no-code, startup, finance, marketing]
keywords: [tự động hóa crunchbase, lấy dữ liệu nhà đầu tư tự động, google sheets automation, workflow n8n finance, tự động hóa đầu tư, thu thập dữ liệu startup]
---

# 🚀 **Tự Động Hóa Thu Thập Dữ Liệu Nhà Đầu Tư từ Crunchbase Sang Google Sheets (Không Cần Code)**

## **📌 Nỗi Đau Của Các Sếp Startup & Nhà Đầu Tư**
Bạn có bao giờ phải:
- **Tốn thời gian** tìm kiếm và copy-paste dữ liệu nhà đầu tư từ Crunchbase hàng ngày?
- **Lo lắng về độ chính xác** khi thu thập thông tin thủ công?
- **Không có thời gian** để phân tích xu hướng đầu tư mới từ các nhà đầu tư hàng đầu?
- **Mất trắng** cơ hội liên lạc với nhà đầu tư quan trọng vì không có danh sách cập nhật?

**Workflow này giải quyết tất cả!** Với chỉ **4 node đơn giản**, bạn sẽ tự động:
✅ **Lấy dữ liệu nhà đầu tư từ Crunchbase** hàng ngày (không cần mở trình duyệt).
✅ **Lọc và định dạng** thông tin quan trọng (tên, mô tả, vị trí, giai đoạn đầu tư).
✅ **Lưu tự động vào Google Sheets** để phân tích, báo cáo hoặc outreach.
✅ **Tiết kiệm thời gian lên đến 10 giờ/tuần** và giảm thiểu sai sót.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo dữ liệu an toàn và không bị giới hạn bởi phiên bản miễn phí.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần copy-paste thủ công hàng ngày (giảm 10+ giờ/tuần).
- **Dữ liệu chính xác**: Tránh sai sót khi thu thập thông tin từ trang web.
- **Cập nhật liên tục**: Dữ liệu nhà đầu tư được tự động sync hàng ngày.
- **Sẵn sàng phân tích**: Google Sheets được cập nhật tự động, giúp dễ dàng tạo báo cáo, dashboard hoặc chiến lược outreach.
- **Hoạt động 24/7**: Workflow chạy tự động mà không cần can thiệp của bạn.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Crunchbase Pro** (để truy cập API).
   - [Đăng ký Crunchbase Pro](https://www.crunchbase.com/) (nếu chưa có).
   - **Lấy API Key**:
     - Truy cập [Crunchbase Developer Portal](https://data.crunchbase.com/docs).
     - Tạo một **API Key** mới và lưu lại.
2. **Tài khoản Google Sheets** và **OAuth 2.0 Credentials** để kết nối với Google Drive.
   - Hướng dẫn tạo OAuth 2.0:
     - Mở [Google Cloud Console](https://console.cloud.google.com/).
     - Tạo một **Project mới** → **Enable Google Sheets API**.
     - Tạo **OAuth Client ID** (dạng "Desktop App") và lưu **Client ID** và **Client Secret**.
3. **Google Sheet sẵn sàng** để lưu dữ liệu (tên sheet phải được chỉ định trong workflow).
4. **Tài khoản n8n** (cài đặt trên VPS hoặc dùng phiên bản miễn phí trên [n8n.io](https://n8n.io/)).
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/4731](https://n8n.io/workflows/4731) (chọn "Export").
2. **Mở n8n Editor** (trên VPS hoặc n8n.io).
3. Nhấn **"Import"** → Chọn file JSON vừa tải.
4. Workflow sẽ xuất hiện trên canvas.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Tải JSON** từ link trên.
2. Mở **n8n Editor** → Nhấn **"Import"** → Chọn **"Paste JSON"**.
3. Dán nội dung JSON và nhấn **"Import"**.

---

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
#### **Node 1: Daily Investor Data Trigger (Schedule Trigger)**
- **Cấu hình lịch chạy**:
  - Nhấn **"Edit"** trên node này.
  - Chọn **schedule** (ví dụ: `0 8 * * *` để chạy hàng ngày lúc 8h sáng UTC).
  - Lưu ý: **Thời gian UTC** (nếu bạn ở Việt Nam, hãy điều chỉnh phù hợp, ví dụ `0 15 * * *` để chạy lúc 2h chiều UTC = 9h sáng Việt Nam).

#### **Node 2: Fetch Crunchbase Investor Data (HTTP Request)**
- **Cấu hình API Key**:
  - Nhấn **"Edit"** trên node.
  - Trong **"Headers"**, thêm:
    ```
    Authorization: Bearer YOUR_CRUNCHBASE_API_KEY
    ```
    (Thay `YOUR_CRUNCHBASE_API_KEY` bằng API Key của bạn).
  - Trong **"Body"**, đảm bảo payload là:
    ```json
    {
      "filter": {
        "type": "investor"
      },
      "fields": [
        "name",
        "short_description",
        "location_identifiers",
        "investment_stage"
      ]
    }
    ```
  - **Method**: POST.
  - **URL**: `https://data.crunchbase.com/graphql`.

- **Lưu ý**:
  - Nếu Crunchbase API yêu cầu **IP Whitelisting**, hãy liên hệ hỗ trợ của Crunchbase để thêm IP VPS của bạn vào danh sách cho phép.
  - Nếu gặp lỗi **CORS**, có thể cần cấu hình proxy hoặc sử dụng **n8n Proxy**.

#### **Node 3: Extract Investor Fields (Code)**
- **Không cần chỉnh sửa** (nếu bạn muốn giữ nguyên logic mặc định).
- **Nếu muốn tùy chỉnh**:
  - Nhấn **"Edit"** trên node → **"Code"**.
  - Thay đổi biến `fields` trong JavaScript để lấy thông tin khác (ví dụ: `funding_rounds`, `industry`).
  - Ví dụ:
    ```javascript
    const fields = [
      "name",
      "short_description",
      "location_identifiers",
      "investment_stage",
      "funding_rounds"
    ];
    ```

#### **Node 4: Append to Investor Sheet (Google Sheets)**
- **Cấu hình OAuth 2.0**:
  - Nhấn **"Edit"** → **"Credentials"**.
  - Chọn **"googleSheetsOAuth2Api"** (nếu chưa có, tạo mới trong **Credentials** của n8n).
  - Nhập **Client ID** và **Client Secret** từ Google Cloud Console.
- **Cấu hình Sheet**:
  - Trong **"Operation"**, chọn **"Append"** (để thêm dữ liệu mới vào cuối sheet).
  - Trong **"Spreadsheet ID"**, nhập ID của Google Sheet bạn muốn lưu dữ liệu.
    - **Lấy ID Sheet**:
      - Mở Google Sheet → URL sẽ có dạng: `https://docs.google.com/spreadsheets/d/ID_SHEET/edit#gid=0`.
      - **ID Sheet** là phần sau `/d/` và trước `/edit`.
  - Trong **"Sheet Name"**, nhập tên sheet (ví dụ: `"Investors"`).
  - Trong **"Range"**, nhập `A1` (nếu muốn bắt đầu từ ô A1).
  - **Headers**: Chọn **"Use first row as headers"** (để tự động tạo tiêu đề cột).

- **Lưu ý**:
  - Đảm bảo **Google Sheet** đã được chia sẻ với tài khoản email liên kết với OAuth 2.0 của bạn.
  - Nếu sheet chưa có tiêu đề, node sẽ tự động tạo từ dữ liệu đầu tiên.

---

### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run**:
   - Nhấn **"Run"** trên node **Daily Investor Data Trigger** để chạy thử.
   - Kiểm tra **Google Sheet** xem dữ liệu có được append không.
   - Nếu có lỗi, kiểm tra lại **API Key**, **OAuth Credentials** và **URL Sheet**.
2. **Bật Active**:
   - Sau khi test thành công, nhấn **"Active"** trên node **Daily Investor Data Trigger** để workflow chạy tự động theo lịch.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
### **1. Tự Động Gửi Báo Cáo Email Khi Có Dữ Liệu Mới**
- **Thêm Node Email** (ví dụ: **SendGrid** hoặc **Gmail SMTP**).
- **Cấu hình**:
  - Sau node **Append to Investor Sheet**, thêm node **HTTP Request** để gọi API của SendGrid/Gmail.
  - Nội dung email có thể bao gồm:
    ```
    "Xin chào! Dữ liệu nhà đầu tư mới đã được cập nhật vào Google Sheets. Link: [LINK_SHEET]."
    ```

### **2. Lưu Log Dữ Liệu Trên Slack/Telegram**
- **Thêm Node Slack/Telegram**:
  - Sau node **Extract Investor Fields**, thêm node **Slack Webhook** hoặc **Telegram Bot**.
  - Gửi thông báo:
    ```
    "🚀 Dữ liệu nhà đầu tư mới được cập nhật! Tổng số nhà đầu tư: [COUNT]."
    ```

### **3. Lọc Dữ Liệu Theo Giai Đoạn Đầu Tư**
- **Tùy chỉnh Node Code**:
  - Trong node **Extract Investor Fields**, thêm logic lọc nhà đầu tư theo giai đoạn (ví dụ: chỉ lấy `investment_stage: "Seed"`).
  - Ví dụ:
    ```javascript
    const investors = data.body.data.investors.filter(investor =>
      investor.investment_stage === "Seed"
    );
    ```

### **4. Tạo Dashboard Từ Google Sheets**
- **Kết nối với Data Studio/Tableau**:
  - Sau khi dữ liệu được append vào Google Sheets, bạn có thể:
    - Mở **Google Data Studio** → Kết nối với Sheet.
    - Tạo **dashboard** để theo dõi xu hướng đầu tư của các nhà đầu tư.

### **5. Backup Dữ Liệu Hàng Tuần**
- **Thêm Node Google Drive**:
  - Sau node **Append to Investor Sheet**, thêm node **Google Drive** để sao lưu file Excel/CSV hàng tuần.
  - Cấu hình:
    - **Operation**: "Create file".
    - **File Name**: `Investors_Backup_YYYY-MM-DD.xlsx`.
    - **Content**: Dữ liệu từ node trước.

---

## 📌 **Kết Luận**
Workflow này là **công cụ mạnh mẽ** giúp các sếp startup, nhà đầu tư và chuyên gia marketing:
✅ **Tự động hóa thu thập dữ liệu** từ Crunchbase mà không cần code.
✅ **Tiết kiệm thời gian** và giảm thiểu sai sót.
✅ **Cập nhật liên tục** dữ liệu để phân tích chiến lược đầu tư.
✅ **Hoạt động 24/7** mà không cần can thiệp của bạn.

**Hành động ngay!**
1. **Cài đặt n8n** trên VPS (nếu chưa có).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Bật Active** và bắt đầu tự động hóa!

**Nếu gặp vấn đề**, hãy liên hệ với tác giả Yaron Been qua:
- [LinkedIn](https://www.linkedin.com/in/yaronbeen/)
- [YouTube](https://www.youtube.com/@YaronBeen/videos)
- Email: **Yaron@nofluff.online**

---
**Chúc các sếp thành công với việc tự động hóa dữ liệu nhà đầu tư!** 🚀💼