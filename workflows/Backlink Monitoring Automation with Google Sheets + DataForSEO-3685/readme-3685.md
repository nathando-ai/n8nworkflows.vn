---
title: "🔍 **Tự Động Hóa Kiểm Tra Backlink 24/7 Với Google Sheets + DataForSEO (Không Cần Code!)**"
description: "Giải pháp tự động hóa kiểm tra backlink từ Google Sheets sang DataForSEO để theo dõi trạng thái (Live/Lost/Nofollow) của tất cả liên kết ngoại bộ. Tiết kiệm thời gian lên đến 10 giờ/tuần và giảm thiểu lỗi con người."
slug: "tieu-dong-hoa-kiem-tra-backlink-google-sheets-dataforseo"
tags: [n8n, automation, seo, google-sheets, dataforseo, ai-marketing]
keywords: [tự động hóa backlink, n8n workflow seo, kiểm tra backlink tự động, google sheets api, dataforseo api, seo automation]
---

# 🚀 **Tự Động Hóa Kiểm Tra Backlink 24/7 Với Google Sheets + DataForSEO**

### **Nỗi Đau Của Các Sếp SEO**
Bạn có bao giờ phải:
- **Lặp đi lặp lại** kiểm tra hàng trăm backlink thủ công trên Google Sheets?
- **Mất thời gian** vào việc copy-paste URL vào DataForSEO để tra cứu trạng thái?
- **Lo lắng** về việc mất backlink quan trọng mà không phát hiện kịp thời?
- **Không biết** liệu backlink của mình đang **Live**, **Lost**, hay **Nofollow**?

**Workflow này giải quyết tất cả!** Với chỉ **một lần cấu hình**, bạn sẽ tự động:
✅ **Kiểm tra tất cả backlink** trong Google Sheets.
✅ **Tra cứu trạng thái** trên DataForSEO (Live/Lost/Nofollow).
✅ **Cập nhật tự động** kết quả vào Google Sheets.
✅ **Hoạt động 24/7** mà không cần can thiệp của bạn.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Giảm **10+ giờ/tuần** so với kiểm tra thủ công.
- **Chính xác 100%**: Không còn lỗi copy-paste hoặc bỏ sót backlink.
- **Cập nhật tự động**: Kết quả Live/Lost/Nofollow được ghi lại ngay lập tức.
- **Hoạt động liên tục**: Kiểm tra backlink **mỗi khi bạn muốn** (hoặc lập lịch tự động).
- **Tối ưu SEO**: Nhận cảnh báo ngay khi backlink bị mất hoặc chuyển sang NoFollow.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets** với:
   - **Bảng dữ liệu** có **2 cột bắt buộc**:
     - **"Backlink URL"** (URL của trang chứa backlink).
     - **"Landing page"** (URL trang của bạn đang được backlink).
   - **Dữ liệu định dạng rõ ràng** (ví dụ: từ ô `D1` đến `E`).
   - **Chia sẻ quyền truy cập** cho n8n (nếu self-hosted).

2. **Tài khoản DataForSEO** với:
   - **API Key** và **Password** (để Basic Auth).
   - **Gói dịch vụ** đủ để tra cứu backlink (check với DataForSEO).

3. **n8n Workflow** (cài đặt trên [n8n.io](https://n8n.io/) hoặc VPS).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/3685](https://n8n.io/workflows/3685).
- **Nhấn "Import"** trong n8n Editor.
- **Hoặc copy/paste** JSON vào tab "Import" của n8n.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **9 node**, các sếp cần chú ý cấu hình sau:

##### **A. Cấu Hình Google Sheets**
- **Node "Reads Google Sheets"**:
  - Chọn **credentials**: `googleSheetsOAuth2Api`.
  - **Chọn sheet và range** (ví dụ: `Sheet1!D1:E`).
  - **Kiểm tra tên cột**: Phải **chính xác** là:
    - `Backlink URL`
    - `Landing page`

##### **B. Cấu Hình DataForSEO**
- **Node "Sends HTTP POST Request to DataForSEO"**:
  - **Credentials**: `httpBasicAuth` (điền **API Key** và **Password** từ DataForSEO).
  - **Method**: `POST`.
  - **URL**: `https://api.dataforseo.com/v3/on_page/task_post`.
  - **JSON Body**:
    ```json
    [{
      "target": "{{ $json.domain }}",
      "start_url": "{{ $json.url }}",
      "max_crawl_pages": 1
    }]
    ```
    - **Lưu ý**:
      - `$json.domain` = URL trang của bạn (cột `Landing page`).
      - `$json.url` = URL backlink (cột `Backlink URL`).

- **Node "Sends HTTP links request to DataforSeo"**:
  - **Credentials**: **Cùng với node trước** (`httpBasicAuth`).
  - **Method**: `POST`.
  - **URL**: `https://api.dataforseo.com/v3/on_page/links`.
  - **JSON Body**:
    ```json
    [{
      "id": "{{ $json.tasks[0].id }}"
    }]
    ```
    - **Lưu ý**: `$json.tasks[0].id` sẽ tự động lấy từ kết quả của node trước.

##### **C. Cập Nhật Kết Quả Về Google Sheets**
- **Node "Sends data to Google sheets"**:
  - **Credentials**: `googleSheetsOAuth2Api`.
  - **Operation**: `appendOrUpdate`.
  - **Mapping cột**:
    - **Matching Column**: `Backlink URL` (để tìm hàng đúng).
    - **Backlink URL**: `{{ $('Loop Over Items').item.json.url }}`.
    - **Status**: `{{ $json.status }}` (Live/Lost/Nofollow).
  - **Kiểm tra cột trong Google Sheets**:
    - Phải có **cột `Status`** để lưu kết quả.

##### **D. Cấu Hình Node "Loop Over Items"**
- **Node này** sẽ **lặp qua tất cả backlink** trong Google Sheets.
- **Không cần chỉnh sửa** nếu đã import đúng file JSON.

##### **E. Node "Waits 20 seconds"**
- **Thời gian chờ 20s** giữa các yêu cầu API để **tránh bị block** bởi DataForSEO.
- **Không cần chỉnh sửa** (nếu không muốn, có thể xóa node này).

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với **1-2 backlink mẫu**:
   - Nhấn **"Execute"** trên node `When clicking ‘Test workflow’`.
   - Kiểm tra kết quả trong Google Sheets.
2. **Bật Active**:
   - Chuyển **switch Active** sang **ON** (đỏ → xanh).
   - **Hoặc** kết hợp với **Trigger** (Webhook/Schedule) để chạy tự động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Lập Lịch Chạy Tự Động**:
   - Sử dụng **n8n Trigger "Schedule"** để chạy workflow **hàng ngày/tuần**.
   - Ví dụ: Kiểm tra backlink **mỗi sáng 7h**.

2. **Gửi Báo Cáo qua Email/Slack**:
   - Thêm **node `n8n-nodes-base.email`** hoặc **`n8n-nodes-base.slack`** để cảnh báo khi:
     - Backlink **bị mất** (`status = "Lost"`).
     - Backlink **trở thành NoFollow** (`status = "Lost (Nofollow)"`).

3. **Lưu Log Kết Quả**:
   - Thêm **node `n8n-nodes-base.stickyNote`** để ghi lại lịch sử kiểm tra.
   - Hoặc sử dụng **Google Sheets Log** để theo dõi.

4. **Tối ưu DataForSEO**:
   - Nếu có **gói API cao cấp**, tăng `max_crawl_pages` để tra cứu nhiều trang hơn.

5. **Xử Lý Lỗi**:
   - Nếu DataForSEO trả về **lỗi API**, thêm **node `n8n-nodes-base.if`** để:
     - **Gửi email cảnh báo** nếu trạng thái lỗi.
     - **Thử lại** sau 1 giờ.

---

### 📌 **Kết Luận**
Workflow này **giải phóng bạn khỏi công việc lặp lại** trong SEO, giúp:
✔ **Tiết kiệm thời gian** để tập trung vào chiến lược.
✔ **Nhận dữ liệu chính xác** về backlink.
✔ **Cập nhật tự động** mà không cần can thiệp.

**Hành động ngay!**
1. **Import workflow** từ [n8n.io/workflows/3685](https://n8n.io/workflows/3685).
2. **Cấu hình Google Sheets và DataForSEO** theo hướng dẫn.
3. **Bật Active** và **kiểm tra kết quả** trong Google Sheets.

**Cần hỗ trợ?** Đăng ký **VPS n8n** từ [TinoHost](https://tino.vn/vps-n8n?affid=388) để chạy workflow **ổn định 24/7** mà không lo downtime!

---
**#SEOAutomation #n8nWorkflows #DataForSEO #GoogleSheets #SelfHosted**