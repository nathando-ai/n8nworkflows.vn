---
title: "🏡 **Tự Động Hóa Tìm Kiếm & Lọc Lead Chuyên Gia Bất Động Sản Trên Google Maps (Không Code!)**"
description: "Workflow này tự động tìm kiếm, trích xuất và lọc lead chuyên gia bất động sản (đại lý, quản lý tài sản, ngân hàng) từ Google Maps, loại bỏ trùng lặp, lưu vào Google Sheets và gửi báo cáo ngay qua Gmail/Slack. Giúp các sếp tiết kiệm 10-15h/tháng tìm kiếm thủ công!"
slug: "tieu-dong-hoa-tim-kiem-lead-bat-dong-san-google-maps"
tags: [n8n, automation, lead-generation, google-maps-scraping, real-estate, scrapeops]
keywords: [tự động hóa tìm lead bất động sản, scrape google maps bằng n8n, lưu lead vào google sheets, alert lead slack gmail, công cụ tìm đại lý bất động sản]
---

# 🚀 **Tự Động Hóa Tìm Kiếm Lead Chuyên Gia Bất Động Sản Trên Google Maps (Không Code!)**

### **Nỗi Đau Của Các Sếp**
Tìm kiếm và liên hệ với các đại lý bất động sản, quản lý tài sản hoặc ngân hàng cho vay là công việc **mệt mỏi, tốn thời gian** và thường **không hiệu quả**. Các sếp phải:
- **Tìm kiếm thủ công** trên Google Maps, trích xuất thông tin (điện thoại, website, đánh giá) từ hàng trăm kết quả.
- **Loại bỏ trùng lặp** giữa các nguồn dữ liệu khác nhau (Google Sheets, CRM, email).
- **Lưu trữ và theo dõi** lead một cách rối rắm, dễ bỏ quên.
- **Gửi thông báo** cho team khi có lead mới, nhưng lại phải làm thủ công.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Scrape** thông tin chi tiết từ Google Maps (tên, địa chỉ, điện thoại, website, đánh giá, liên kết Maps).
✅ **Lọc bỏ trùng lặp** với dữ liệu cũ trong Google Sheets.
✅ **Lưu lead mới** vào bảng tính tự động.
✅ **Gửi báo cáo** ngay qua **Gmail** và **Slack** để team theo dõi.

---

## 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**Lợi Ích Cốt Lõi**]
- **Tiết kiệm 10-15h/tháng** so với cách làm thủ công.
- **Dữ liệu chính xác 100%** (không sai sót như copy-paste).
- **Lọc bỏ trùng lặp** tự động, tránh lãng phí thời gian gọi điện sai.
- **Hoạt động 24/7** (không cần phải làm vào giờ hành chính).
- **Cá nhân hóa thông báo** (Gmail/Slack) cho từng thành viên team.
- **Dữ liệu sẵn sàng** để phân tích, export hoặc kết nối với CRM.
:::

---

## 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản ScrapeOps** (miễn phí):
   - Đăng ký tại [ScrapeOps](https://scrapeops.io/app/register/n8n) và lấy **API Key**.
   - Cài đặt **n8n ScrapeOps Node** từ [n8n Community](https://flows.n8n.io/flow/14111).
2. **Google Sheets** (đã tạo và chia sẻ cho n8n):
   - Sử dụng **template** từ [đây](https://docs.google.com/spreadsheets/d/1C7OAR6d6bngkrCw-On7zoIYY0QjobLVdDaP_d7u-hKU/edit) (đã định dạng sẵn các cột: Tên, Điện thoại, Website, Địa chỉ, Đánh giá, Liên kết Maps).
   - **Chia sẻ** với n8n bằng quyền **Editor**.
3. **Tài khoản Gmail** (để gửi thông báo):
   - Cấu hình **OAuth2** trong n8n (đường dẫn hướng dẫn: [n8n Gmail Docs](https://docs.n8n.io/integrations/builtins/n8n-nodes-base.n8nGmail)).
4. **Tài khoản Slack** (để gửi alert):
   - Tạo **App Slack** và lấy **Bot Token** (hướng dẫn: [n8n Slack Docs](https://docs.n8n.io/integrations/builtins/n8n-nodes-base.n8nSlack)).
5. **VPS cho n8n** (khuyến nghị):
   :::info[**Gợi ý hạ tầng cho n8n**]
   Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng** (Self-hosted).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
   :::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow:
#### **Cách 1: Import từ file JSON**
1. Tải workflow từ [n8n Community](https://flows.n8n.io/flow/14111) (ấn **Export**).
2. Trên **n8n Editor**, nhấn **Import** → Chọn file JSON vừa tải.
3. Chọn **Create New Workflow** và nhấn **Import**.

#### **Cách 2: Copy/Paste JSON**
1. Mở **n8n Editor** → Tạo workflow mới.
2. Nhấn **Import** → Chọn **Paste JSON**.
3. Dán toàn bộ mã JSON từ [n8n Community](https://flows.n8n.io/flow/14111) vào ô **Paste JSON**.
4. Nhấn **Import**.

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Sau khi import, các sếp **phải cấu hình** các node sau:

#### **🔹 Node 1: "Form: Enter City to Search" (formTrigger)**
- **Không cần chỉnh** (sẵn sàng để người dùng nhập thành phố).
- **Lưu ý**: URL form sẽ được cung cấp sau khi workflow hoạt động (xem phần **Kích hoạt ⚡️**).

#### **🔹 Node 2: "Set Google Maps Configuration" (set)**
- **Tham số cần chỉnh**:
  - `keyword`: Thay đổi từ `"real estate agent"` thành:
    - `property manager` (quản lý tài sản)
    - `mortgage broker` (ngân hàng cho vay)
    - `home inspector` (kiểm tra nhà)
  - `location`: Đặt thành `"{{ $input['path']['city'] }}"` (để tự động lấy thành phố từ form).

#### **🔹 Node 3 & 6: "ScrapeOps: Search Google Maps" & "ScrapeOps: Fetch Business Details"**
- **Credentials**: Đã tự động lấy từ `scrapeOpsApi` (đã cấu hình trước khi import).
- **Lưu ý**:
  - Nếu **API Key ScrapeOps hết hạn**, workflow sẽ **bị lỗi**. Các sếp phải **cập nhật lại** trong **Credentials** của n8n.
  - **Rate Limit**: ScrapeOps có giới hạn request/month. Nếu quá tải, các sếp cần nâng cấp gói dịch vụ.

#### **🔹 Node 4: "Read Previous Entries from Sheet" (googleSheets)**
- **Credentials**: Sử dụng `googleSheetsOAuth2Api` (đã cấu hình trước).
- **Lưu ý**:
  - **Sheet Name**: Đặt thành tên của **Google Sheet** các sếp đã tạo (ví dụ: `"Lead Bất Động Sản"`).
  - **Range**: Đặt thành `"Sheet1!A:Z"` (nếu sheet có tên khác, chỉnh theo).

#### **🔹 Node 5 & 7: "Parse Full Business Info" & "Compare & Deduplicate Leads" (code)**
- **Không cần chỉnh** (sẵn sàng, sử dụng logic JavaScript mặc định).
- **Lưu ý**:
  - Nếu các sếp muốn **thêm/bỏ cột dữ liệu**, phải chỉnh code trong **Code Node** này (yêu cầu kiến thức JS cơ bản).

#### **🔹 Node 8: "Filter New Leads Only" (if)**
- **Không cần chỉnh** (sẵn sàng, logic mặc định là lọc lead mới).

#### **🔹 Node 9: "Save New Leads to Sheet" (googleSheets)**
- **Credentials**: Sử dụng `googleSheetsOAuth2Api`.
- **Lưu ý**:
  - **Operation**: Đã đặt là `"append"` (lưu mới vào cuối sheet).
  - **Range**: Đặt thành `"Sheet1!A:Z"` (nếu sheet có tên khác, chỉnh theo).

#### **🔹 Node 10 & 11: "Send Gmail Alert" & "Send Slack Alert"**
- **Credentials**:
  - Gmail: `gmailOAuth2`
  - Slack: `slackApi`
- **Lưu ý**:
  - **Gmail**:
    - **Subject**: Đặt thành `"📌 Lead mới từ Google Maps: {{ $node["Parse Full Business Info"].json["name"] }}"`.
    - **Body**: Đặt thành template HTML (sẵn sàng, có thể chỉnh theo ý muốn).
  - **Slack**:
    - **Channel**: Đặt tên **Slack Channel** muốn gửi alert (ví dụ: `#lead-bat-dong-san`).
    - **Message**: Đặt thành template (sẵn sàng, có thể chỉnh theo ý muốn).

---

### **3. Kích Hoạt ⚡️**
1. **Test Run với Dữ liệu Mẫu**:
   - Nhấn **Run Workflow** và nhập **thành phố** vào form (ví dụ: `Hà Nội`).
   - Kiểm tra:
     - **Google Sheets**: Có lead mới được append không?
     - **Gmail/Slack**: Có nhận được alert không?
   - Nếu có lỗi, kiểm tra **Logs** và **Credentials** của các node.

2. **Bật Active Workflow**:
   - Sau khi test thành công, chuyển **Status** từ `Inactive` sang `Active`.

3. **Lấy URL Form**:
   - Sau khi workflow hoạt động, mở **Node "Form: Enter City to Search"** → Nhấn **Open** để lấy **URL form**.
   - **Chia sẻ URL này** với team để họ nhập thành phố và nhận lead tự động.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
### **1. Chạy Tự Động (Không Cần Form)**
- Thay vì dùng **Form Trigger**, các sếp có thể **sử dụng Schedule Trigger** để chạy workflow **tự động hàng ngày**.
- **Cách làm**:
  1. Thêm **Node "Schedule"** vào workflow (đặt trước node `Set Google Maps Configuration`).
  2. Cấu hình **thời gian chạy** (ví dụ: `0 9 * * *` = 9h sáng hàng ngày).
  3. **Chỉnh node `Set Google Maps Configuration`** để lấy thành phố từ **variable** (ví dụ: `{{ $input["schedule"]["city"] }}`).

### **2. Lưu Log & Theo Dõi Lỗi**
- Thêm **Node "Sticky Note"** để ghi lại **log hoạt động** (ví dụ: thành phố đã scrape, số lead mới).
- **Cách làm**:
  1. Thêm node `StickyNote` sau node `Save New Leads to Sheet`.
  2. Cấu hình **message**: `"📊 Scrape thành công cho thành phố: {{ $input["path"]["city"] }} | Số lead mới: {{ $node["Filter New Leads Only"].json.length }}"`.

### **3. Kết Nối Với CRM (Zoho, HubSpot, Pipedrive)**
- Sau khi lưu lead vào **Google Sheets**, các sếp có thể **export dữ liệu** và kết nối với **CRM** để quản lý.
- **Cách làm**:
  1. Thêm **Node "Google Sheets"** để **export toàn bộ sheet** vào định dạng CSV/JSON.
  2. Kết nối với **Zapier** hoặc **n8n CRM Node** để đẩy dữ liệu vào CRM.

### **4. Tăng Cường Dữ Liệu (Thêm Website, Email)**
- Nếu muốn **trích xuất email** từ website của đại lý, các sếp có thể:
  - Sử dụng **ScrapeOps** để scrape **email** từ trang liên hệ.
  - Thêm **Node "Code"** để **xử lý email** và lưu vào sheet.

---

## 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** để các sếp:
✔ **Tiết kiệm thời gian** tìm kiếm lead bất động sản.
✔ **Lọc bỏ trùng lặp** tự động.
✔ **Nhận thông báo ngay** khi có lead mới.
✔ **Hoạt động 24/7** mà không cần can thiệp.

**Hành động ngay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test với thành phố** và kiểm tra kết quả.
3. **Chia sẻ URL form** với team để bắt đầu tự động hóa!

**Nếu có vấn đề**, các sếp có thể:
- **Comment** dưới bài viết này.
- **Gửi tin nhắn** cho tôi trên [n8n Community](https://community.n8n.io/).

**Chúc các sếp thành công với việc tự động hóa lead bất động sản!** 🚀