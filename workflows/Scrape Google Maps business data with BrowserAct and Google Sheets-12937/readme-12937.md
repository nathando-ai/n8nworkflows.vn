---
title: "🚀 Tự Động Hoá Scrape Dữ Liệu Google Maps Sang Google Sheets - Market Research 24/7"
description: "Workflow tự động hóa scrape thông tin chi tiết doanh nghiệp từ Google Maps (tên, điện thoại, địa chỉ, đánh giá, website...) và lưu vào Google Sheets chỉ với 1 form đơn giản. Giúp các sếp tiết kiệm thời gian nghiên cứu thị trường, phân tích đối thủ và xây dựng danh sách lead chất lượng."
slug: "tieu-dong-hoa-scrape-google-maps-sang-google-sheets"
tags: [n8n, automation, market-research, google-maps-scraper, google-sheets, browseract]
keywords: [tự động hóa scrape google maps, n8n workflow market research, scrape dữ liệu doanh nghiệp, tự động hóa nghiên cứu thị trường, lưu dữ liệu google maps vào google sheets]
---

# 🚀 **Scrape Dữ Liệu Google Maps Sang Google Sheets - Giải Pháp Market Research Tự Động Hóa**

### **Nỗi Đau Của Các Sếp Trong Nghiên Cứu Thị Trường**
Hàng ngày, các sếp phải mất **giờ đồng hồ** để:
- Tìm kiếm và ghi chép thông tin doanh nghiệp từ Google Maps (tên, địa chỉ, điện thoại, đánh giá, website...)
- So sánh đối thủ cạnh tranh thủ công
- Cập nhật danh sách lead cho đội ngũ bán hàng
- Làm việc với dữ liệu không đồng bộ, dễ bị lỗi

**Workflow này giải quyết tất cả!** Chỉ với **1 form đơn giản**, bạn có thể:
✅ **Scrape dữ liệu chi tiết** từ Google Maps (tên, điện thoại, địa chỉ, đánh giá, website, review mới nhất...)
✅ **Lưu tự động vào Google Sheets** với định dạng sẵn sàng phân tích
✅ **Tiết kiệm 10-20 giờ/tháng** cho việc nghiên cứu thị trường
✅ **Cập nhật liên tục** khi có thay đổi mới (mới mở cửa, đánh giá mới, thay đổi thông tin)

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Thay vì scrape thủ công, chỉ cần nhập **1 form** là dữ liệu tự động xuất hiện trong Google Sheets.
- **Dữ liệu chính xác & cập nhật**: BrowserAct scrape theo yêu cầu thực thời, không bị giới hạn như scrape thủ công.
- **Dễ dàng phân tích**: Dữ liệu được lưu vào Google Sheets với **cột sẵn sàng cho pivot table, chart, hoặc export Excel**.
- **Hoạt động 24/7**: Workflow chạy tự động, không cần can thiệp của con người.
- **Dùng cho nhiều mục đích**: Lead generation, nghiên cứu đối thủ, xây dựng danh sách nhà cung cấp, phân tích thị trường địa phương.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản n8n Self-hosted** (cài trên VPS hoặc máy chủ riêng)
✔ **API Key BrowserAct**:
   - Đăng ký tại [BrowserAct](https://browseract.ai/) và tạo **API Key** để kết nối với n8n.
   - Hướng dẫn chi tiết: [Tạo API Key BrowserAct](https://docs.browseract.com/docs/api-keys)
✔ **Google Sheets OAuth2 Credentials**:
   - Tạo tại [Google Cloud Console](https://console.cloud.google.com/) và cấp quyền cho n8n.
   - Hướng dẫn: [Cài đặt OAuth2 cho Google Sheets](https://developers.google.com/sheets/api/quickstart/python)
✔ **Google Sheets mẫu** (đã được chia sẻ trong workflow):
   - [Mẫu Google Sheets](https://docs.google.com/spreadsheets/d/1_B3-9dUA0XNCirVcA9qr-zeSXK_zkZRoW8xXt7vQflA/copy) (được chia sẻ sẵn, các sếp chỉ cần **duplicate** và cập nhật URL).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
**Bước 1:** Tải workflow từ [n8n.io/workflows/12937](https://n8n.io/workflows/12937) hoặc [tải file JSON](https://raw.githubusercontent.com/n8n-io/workflows/master/workflows/12937.json) (nếu có).

**Bước 2:** Trong **n8n Editor**, chọn **"Import"** và chọn file JSON vừa tải.

**Bước 3:** Workflow sẽ hiển thị với **5 node** chính:
- **On form submission** (form nhập liệu)
- **Run a workflow and wait for its result** (BrowserAct scrape)
- **Extract from File** (xử lý dữ liệu)
- **Append or update row in sheet** (lưu vào Google Sheets)
- **Get Data** (node hỗ trợ)

---

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
##### **Node 1: "On form submission" (Form Nhập Liệu)**
- **Không cần chỉnh sửa** (n8n sẽ tự tạo URL form).
- **URL form** sẽ được hiển thị sau khi workflow active (dùng để submit yêu cầu scrape).

##### **Node 2: "Run a workflow and wait for its result" (BrowserAct)**
- **Tham số quan trọng**:
  - **Credentials**: Chọn **"browserActApi"** (đã cấu hình trước khi import).
  - **BrowserAct Workflow ID**:
    - **Bước 1**: Import **template BrowserAct** từ [đây](https://www.browseract.com/template-share/template-of-googlemaps-detail-scraper-2026-01-20/626dfc97051f46dc9ee0d0f33642387a).
    - **Bước 2**: Copy **Workflow ID** từ URL của template (vd: `626dfc97051f46dc9ee0d0f33642387a`).
    - **Bước 3**: Dán vào trường **Workflow ID** trong node này.
  - **Input Data**:
    - Node này sẽ nhận **location** và **business category** từ form (vd: "Hà Nội", "Café").

##### **Node 3: "Extract from File" (Xử Lý Dữ Liệu)**
- **Không cần chỉnh sửa** (n8n tự động xử lý dữ liệu từ BrowserAct).

##### **Node 4: "Append or update row in sheet" (Lưu Vào Google Sheets)**
- **Tham số quan trọng**:
  - **Credentials**: Chọn **"googleSheetsOAuth2Api"** (đã cấu hình trước).
  - **Spreadsheet URL**: Điền **URL của Google Sheets đã duplicate** (vd: `https://docs.google.com/spreadsheets/d/1_B3-9dUA0XNCirVcA9qr-zeSXK_zkZRoW8xXt7vQflA/edit`).
  - **Sheet Name**: Chọn **tab** trong Google Sheets (vd: "Scraped Data").
  - **Operation**: Đã mặc định là **"appendOrUpdate"** (thêm hoặc cập nhật hàng).

##### **Node 5: "Get Data" (Node Hỗ Trợ)**
- **Không cần chỉnh sửa** (n8n sử dụng node này để truyền dữ liệu giữa các node).

---

#### **3. Kích Hoạt ⚡️**
**Bước 1:** Kích hoạt workflow bằng cách:
- Nhấn **"Active"** ở góc trên bên phải của canvas.
- **Test run** với dữ liệu mẫu:
  - Mở **URL form** (hiển thị sau khi active).
  - Nhập **Location** (vd: "Hà Nội") và **Business Category** (vd: "Café").
  - Nhấn **Submit**.
  - Kiểm tra **Google Sheets** để xem dữ liệu đã được scrape và lưu thành công.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tự động scrape định kỳ**:
   - Sử dụng **n8n Node "Schedule"** để chạy workflow hàng ngày/tuần (vd: scrape mới nhất mỗi sáng 7h).
   - Hướng dẫn: [Cài đặt Schedule Node](https://docs.n8n.io/integrations/builtins/nodes/n8n-nodes-base.schedule.html).

2. **Gửi báo cáo tự động qua Email/Slack**:
   - Kết nối với **n8n Node "Email"** hoặc **"Slack"** để thông báo khi có dữ liệu mới.
   - Ví dụ: Gửi **daily report** về top 5 doanh nghiệp mới mở cửa.

3. **Lọc và phân tích dữ liệu**:
   - Sử dụng **Google Sheets Apps Script** để tự động:
     - Tính **trung bình đánh giá**.
     - Lọc doanh nghiệp có **đánh giá > 4.5**.
     - Tạo **báo cáo pivot table** tự động.

4. **Scrape nhiều khu vực cùng lúc**:
   - Tạo **form nhiều trường** (vd: "Location 1", "Location 2", "Category").
   - Sử dụng **n8n Node "Loop"** để scrape song song.

5. **Lưu log scrape**:
   - Kết nối với **n8n Node "Database"** (vd: PostgreSQL) để lưu lịch sử scrape và theo dõi lỗi.

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp cần:
✔ **Nghiên cứu thị trường nhanh chóng** (scrape Google Maps trong giây lát).
✔ **Cập nhật lead liên tục** (dữ liệu tự động lưu vào Google Sheets).
✔ **Tiết kiệm thời gian** (không cần scrape thủ công).

**Hành động ngay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test với 1-2 khu vực** để đảm bảo hoạt động.
3. **Áp dụng cho dự án market research** của mình!

**🚀 Cùng tự động hóa việc scrape Google Maps ngay hôm nay!** Các sếp có thể tham khảo thêm tại:
- [Tutorial chi tiết trên YouTube](https://youtu.be/6M3HyfOYzVI)
- [BrowserAct Official](https://browseract.ai/)
- [Google Sheets Template](https://docs.google.com/spreadsheets/d/1_B3-9dUA0XNCirVcA9qr-zeSXK_zkZRoW8xXt7vQflA/copy)