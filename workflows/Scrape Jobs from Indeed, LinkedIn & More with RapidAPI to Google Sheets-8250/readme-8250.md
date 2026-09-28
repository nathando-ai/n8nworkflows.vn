---
title: "🔍 Tự Động Hóa Scrape Job từ Indeed, LinkedIn & 3 Nền Tảng Khác sang Google Sheets (N8N)"
description: "Tiết kiệm 10+ giờ/tháng với workflow tự động scrape job từ 4 nền tảng lớn (Indeed, LinkedIn, ZipRecruiter, Glassdoor) và lưu trữ dữ liệu vào Google Sheets. Phù hợp cho nhà tuyển dụng, headhunter và doanh nghiệp nghiên cứu thị trường nhân sự."
slug: "tieu-dong-hoa-scrape-job-rapidapi-google-sheets"
tags: [n8n, automation, market-research, rapidapi, google-sheets]
keywords: [scrape job n8n, tự động hóa tìm việc, scrape indeed linkedin glassdoor, rapidapi api jobs, google sheets automation]
---

# 🚀 **Scrape Job Listing từ Indeed, LinkedIn & 3 Nền Tảng Khác sang Google Sheets (N8N)**

### **Giải pháp tự động hóa tìm kiếm việc làm 100% không code**
Bạn là nhà tuyển dụng, headhunter, hoặc doanh nghiệp cần **đánh giá thị trường nhân sự**? Thì việc **quét thủ công** trên Indeed, LinkedIn, ZipRecruiter và Glassdoor mỗi ngày là một **công việc vô cùng tốn thời gian và dễ sai sót**. Với workflow này, bạn sẽ **tự động scrape** tất cả các job listing theo yêu cầu (vị trí, địa điểm, remote,...) và **lưu trữ dữ liệu vào Google Sheets** để phân tích dễ dàng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tháng** so với việc scrape thủ công trên 4 nền tảng.
- **Dữ liệu chính xác và cập nhật thời gian thực** từ Indeed, LinkedIn, ZipRecruiter và Glassdoor.
- **Lưu trữ tự động** vào Google Sheets với định dạng sẵn sàng phân tích.
- **Tùy chỉnh dễ dàng** theo vị trí, loại việc làm, điều kiện remote, và số lượng kết quả.
- **Không cần kỹ thuật** – chỉ cần nhập thông tin và workflow sẽ làm tất cả.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google** (để kết nối với Google Sheets).
2. **API Key của RapidAPI** (miễn phí hoặc trả phí tùy chọn):
   - [Đăng ký API Key Jobs Search Realtime Data](https://rapidapi.com/skdeveloper/api/jobs-search-realtime-data) (nên chọn plan miễn phí đầu tiên để test).
3. **Google Sheet** đã tạo sẵn (các sếp có thể tạo mới hoặc chọn sheet đã có).
4. **Tài khoản n8n** (cài đặt trên máy hoặc VPS).
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [link gốc](https://n8n.io/workflows/8250) và import vào n8n Editor.
- **Cách 2:** Copy toàn bộ JSON từ link trên và paste vào **Import Workflow** trong n8n.
- **Cách 3:** Sử dụng **n8n CLI** (nếu các sếp đã cài đặt):
  ```bash
  n8n import /path/to/workflow.json
  ```

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này bao gồm **4 node chính**, các sếp cần cấu hình như sau:

##### **Node 1: "On form submission" (n8n-nodes-base.formTrigger)**
- **Chức năng:** Hiển thị form cho người dùng nhập thông tin tìm kiếm (vị trí, từ khóa, loại việc làm, remote,...).
- **Lưu ý:**
  - Các sếp **không cần chỉnh sửa** node này, chỉ cần **bật Active** sau khi import.
  - Form sẽ tự động hiển thị khi workflow được kích hoạt.

##### **Node 2: "Scrap Active Jobs" (n8n-nodes-base.httpRequest)**
- **Chức năng:** Gửi yêu cầu API đến **RapidAPI Jobs Search Realtime Data** để scrape job listing.
- **Lưu ý BẮT BUỘC:**
  - **Headers:**
    - `x-rapidapi-key`: Điền **API Key** của RapidAPI (từ bước chuẩn bị).
    - `x-rapidapi-host`: `jobs-search-realtime-data.p.rapidapi.com`.
  - **Method:** `GET`.
  - **URL:**
    ```
    https://jobs-search-realtime-data.p.rapidapi.com/search?query={searchTerm}&location={location}&remote={remote}&page=1&limit=10
    ```
    - Thay `{searchTerm}`, `{location}`, `{remote}` bằng **JSON Path** từ node **Form Trigger** (ví dụ: `{{ $json["searchTerm"] }}`).
  - **Query Parameters:**
    - `query`: Từ khóa tìm kiếm (ví dụ: "Developer").
    - `location`: Vị trí (ví dụ: "Hà Nội").
    - `remote`: `true` (nếu tìm remote) hoặc `false` (nếu tìm offline).
    - `page`: Trang (để scrape nhiều trang, các sếp có thể thêm vòng lặp).
    - `limit`: Số lượng kết quả (mặc định 10).

##### **Node 3: "Re Format" (n8n-nodes-base.code)**
- **Chức năng:** Chỉnh sửa và định dạng lại dữ liệu từ API thành dạng phù hợp trước khi lưu vào Google Sheets.
- **Lưu ý:**
  - Các sếp **không cần chỉnh sửa mã** nếu muốn sử dụng cấu trúc mặc định.
  - Nếu cần **tùy chỉnh dữ liệu**, các sếp có thể mở node này và sửa **JavaScript** (ví dụ: trích xuất thông tin chi tiết từ job listing).

##### **Node 4: "Append In Google Sheets" (n8n-nodes-base.googleSheets)**
- **Chức năng:** Lưu dữ liệu scrape vào Google Sheets.
- **Lưu ý BẮT BUỘC:**
  - **Credentials:** Chọn `googleApi` (cần cấu hình trước trong n8n).
  - **Operation:** `append` (để thêm dữ liệu mới vào sheet).
  - **Sheet Name:** Điền tên sheet (ví dụ: "Job Listings").
  - **Range:** Điền `A1` (nếu muốn bắt đầu từ ô A1) hoặc `A2` (nếu sheet đã có dữ liệu).
  - **Headers:** Chọn `Use first row as headers` (nếu sheet mới) hoặc `Use custom headers` (nếu đã có tiêu đề).

---

#### **3. Kích hoạt ⚡️**
1. **Test Run:**
   - Nhập thông tin tìm kiếm vào form (ví dụ: "Developer", "Hà Nội", "Remote: true").
   - Chạy **Test Run** để kiểm tra dữ liệu scrape có đúng không.
   - Kiểm tra Google Sheets xem dữ liệu đã được append chưa.

2. **Bật Active:**
   - Sau khi test thành công, **bật Active** workflow.
   - Từ nay, mỗi khi có người dùng nhập form, workflow sẽ tự động scrape và lưu dữ liệu.

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁCH NÂNG CAO]
1. **Scrape nhiều trang:**
   - Thêm vòng lặp (`Loop`) sau node `Scrap Active Jobs` để scrape từ trang 1 đến trang N.
   - Ví dụ: `{{ $json["page"] }}` từ 1 đến 10.

2. **Lưu log vào Slack/Telegram:**
   - Thêm node **Slack** hoặc **Telegram Bot** sau node `Re Format` để thông báo khi scrape thành công/thất bại.

3. **Gửi báo cáo định kỳ:**
   - Sử dụng **n8n Scheduler** để chạy workflow hàng ngày/lần tuần và gửi báo cáo qua email (node **Email**).

4. **Lọc dữ liệu trước khi lưu:**
   - Trong node **Code**, các sếp có thể thêm logic lọc (ví dụ: chỉ lưu job có lương > 20M/tháng).

5. **Kết hợp với AI (LLM):**
   - Sử dụng node **LLM** (nếu các sếp có API OpenAI/Mistral) để tóm tắt mô tả công việc hoặc phân tích xu hướng thị trường.
:::

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc scrape thủ công, đồng thời cung cấp **dữ liệu chính xác và cập nhật** để phân tích thị trường nhân sự. **Chỉ cần 5 phút để setup**, sau đó workflow sẽ hoạt động tự động 24/7.

👉 **Hãy áp dụng ngay và tiết kiệm 10+ giờ/tháng!**
👉 **Cần hỗ trợ?** Đăng ký VPS n8n từ [TinoHost](https://tino.vn/vps-n8n?affid=388) để chạy workflow ổn định!

---