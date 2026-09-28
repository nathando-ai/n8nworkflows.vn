---
title: "🚀 Tự Động Hoàn Hảo: Scrape Danh Sách Việc Làm LinkedIn & Tìm Kiếm Dấu Hiệu Tuyển Dụng Cho Doanh Nghiệp"
description: "Workflow tự động hóa 100% không code để scrape live job posts từ LinkedIn qua Bright Data, sàng lọc và gửi dữ liệu vào Google Sheets. Giúp doanh nghiệp phát hiện cơ hội tuyển dụng mới, tối ưu hóa chiến lược tuyển dụng và prospecting bán hàng. Tiết kiệm thời gian lên đến 80% so với cách làm thủ công."
slug: "tieu-dung-scrape-linkedin-job-listings"
tags: [n8n, automation, sales, hr, bright-data, google-sheets, no-code, prospecting]
keywords: [tự động hóa scrape linkedin, tìm kiếm việc làm tự động, prospecting bán hàng, tuyển dụng tự động hóa, bright data api, google sheets automation]
---

# 🚀 **Scrape LinkedIn Job Listings & Tìm Kiếm Dấu Hiệu Tuyển Dụng Cho Doanh Nghiệp**

### **Giải pháp tự động hóa hoàn hảo cho doanh nghiệp cần phát hiện cơ hội tuyển dụng mới và prospecting bán hàng hiệu quả**

Hiện nay, việc tìm kiếm và theo dõi các cơ hội tuyển dụng trên LinkedIn là một công việc tốn thời gian và phức tạp. Các sếp thường phải dành hàng giờ mỗi ngày để:
- Quét thủ công danh sách việc làm trên LinkedIn.
- Lọc ra những vị trí phù hợp với nhu cầu tuyển dụng hoặc prospecting.
- Lưu trữ và theo dõi các cơ hội mới để không bỏ lỡ cơ hội.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động scrape** tất cả các việc làm mới trên LinkedIn theo các tiêu chí lọc của bạn.
✅ **Sàng lọc và sắp xếp** dữ liệu một cách chính xác, loại bỏ thông tin thừa.
✅ **Gửi dữ liệu vào Google Sheets** để theo dõi và phân tích dễ dàng.
✅ **Tiết kiệm thời gian** lên đến 80% so với cách làm thủ công.
✅ **Cung cấp dữ liệu mới nhất** để doanh nghiệp có thể nhanh chóng ứng tuyển hoặc tiếp cận khách hàng tiềm năng.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần quét thủ công hàng ngày, tự động cập nhật dữ liệu mới nhất.
- **Dữ liệu chính xác và sạch**: Loại bỏ HTML, sắp xếp dữ liệu theo cấu trúc nhất quán.
- **Tối ưu hóa tuyển dụng**: Phát hiện nhanh chóng các vị trí tuyển dụng mới phù hợp với nhu cầu.
- **Prospecting bán hàng hiệu quả**: Tìm kiếm các công ty đang tuyển dụng (điều này thường đồng nghĩa với sự phát triển và nhu cầu mua hàng).
- **Dữ liệu dễ theo dõi**: Tất cả thông tin được lưu vào Google Sheets, sẵn sàng để phân tích và sử dụng.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Bright Data**:
   - API Key của Bright Data để scrape dữ liệu từ LinkedIn.
   - Tham khảo [Bright Data API Reference](https://www.brightdata.com/docs/dataset-api) để biết cách sử dụng.
2. **Tài khoản Google Sheets**:
   - Một Google Sheet đã được tạo sẵn (sử dụng [template này](https://docs.google.com/spreadsheets/d/1_jbr5zBllTy_pGbogfGSvyv1_0a77I8tU-Ai7BjTAw4/edit?usp=sharing) để bắt đầu).
   - OAuth2 credentials đã được kết nối trong n8n.
3. **n8n Workflow**:
   - Tài khoản n8n (cả phiên bản cloud lẫn self-hosted đều được hỗ trợ).
   - Các node cần thiết đã được cài đặt (n8n-nodes-base, n8n-nodes-googleSheets).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** của workflow từ [đây](https://n8n.io/workflows/3580) hoặc copy/paste JSON từ trang này vào n8n Editor.
- **Cách import**:
  1. Mở n8n Editor.
  2. Nhấn vào nút **"Import"** ở góc trên bên phải.
  3. Chọn file JSON hoặc dán JSON vào ô nhập liệu.
  4. Nhấn **"Import"** để hoàn tất.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Sau khi import, các sếp cần cấu hình các node quan trọng như sau:

##### **A. Node "On form submission - Discover Jobs" (formTrigger)**
- **Mục đích**: Nhận dữ liệu từ form để scrape LinkedIn.
- **Lưu ý**:
  - Nếu không muốn sử dụng form, có thể bỏ qua node này và thay thế bằng một **HTTP Request** với body JSON cố định (xem phần **Customize It** dưới đây).
  - Các trường cần điền trong form:
    - **Location**: Ví dụ: "New York", "Berlin".
    - **Keyword**: Ví dụ: "Marketing Manager", "Data Analyst".
    - **Country**: Mã ISO 2 chữ, ví dụ: "US", "DE".
    - **Time Range**: "Past 24 hours" hoặc "Last 7 days" (khuyến nghị).
    - **Job Type**: "Full-time", "Part-time", "Contract".
    - **Experience Level** (tùy chọn): "Entry", "Mid", "Senior".
    - **Remote** (tùy chọn): "Remote", "On-site", "Hybrid".
    - **Company** (tùy chọn): Tên công ty cụ thể, ví dụ: "Google".

##### **B. Node "HTTP Request - Post API call to Bright Data" (httpRequest)**
- **Mục đích**: Gửi yêu cầu POST đến Bright Data để bắt đầu scrape dữ liệu.
- **Cấu hình**:
  - **Method**: POST.
  - **URL**: `https://dataset.brightdata.com/api/v1/datasets/{dataset_id}/snapshots`.
    - Thay `{dataset_id}` bằng ID của dataset LinkedIn Job Listings trên Bright Data.
  - **Headers**:
    ```
    Authorization: Bearer YOUR_BRIGHT_DATA_API_KEY
    Content-Type: application/json
    ```
  - **Body**: Sử dụng JSON mẫu sau (điền vào `{{ $json.Location }}`, `{{ $json.Keyword }}`, ... từ form):
    ```json
    {
      "location": "{{ $json.Location }}",
      "keyword": "{{ $json.Keyword }}",
      "country": "{{ $json.Country }}",
      "time_range": "{{ $json.TimeRange }}",
      "job_type": "{{ $json.JobType }}",
      "experience_level": "{{ $json.ExperienceLevel }}",
      "remote": "{{ $json.Remote }}",
      "company": "{{ $json.Company }}"
    }
    ```

##### **C. Node "Wait - Polling Bright Data" (wait)**
- **Mục đích**: Chờ đợi dữ liệu từ Bright Data hoàn tất (thường mất 1-3 phút).
- **Cấu hình**:
  - Thời gian chờ mặc định là 60 giây, có thể điều chỉnh nếu Bright Data trả về chậm.

##### **D. Node "If - Checking status of Snapshot" (if)**
- **Mục đích**: Kiểm tra trạng thái scrape đã hoàn tất hay chưa.
- **Lưu ý**:
  - Node này sẽ kiểm tra trường `status` trong response từ Bright Data.
  - Nếu `status` là `"completed"`, workflow sẽ tiếp tục; nếu chưa, sẽ tiếp tục chờ.

##### **E. Node "HTTP Request - Getting data from Bright Data" (httpRequest)**
- **Mục đích**: Lấy dữ liệu scrape từ Bright Data.
- **Cấu hình**:
  - **Method**: GET.
  - **URL**: `https://dataset.brightdata.com/api/v1/datasets/{dataset_id}/snapshots/{snapshot_id}`.
    - Thay `{dataset_id}` và `{snapshot_id}` bằng ID cụ thể từ response trước đó.
  - **Headers**:
    ```
    Authorization: Bearer YOUR_BRIGHT_DATA_API_KEY
    ```

##### **F. Node "Code - Cleaning Up" (code)**
- **Mục đích**: Xử lý và sắp xếp dữ liệu trước khi gửi vào Google Sheets.
- **Lưu ý**:
  - Node này sử dụng JavaScript để:
    - Biến flat các trường nested (ví dụ: `job_poster`).
    - Loại bỏ HTML từ mô tả việc làm.
  - **Mã mẫu** (có thể chỉnh sửa theo nhu cầu):
    ```javascript
    // Flatten nested fields
    const flattenedData = $input.all().map(item => {
      const job = item.data.job;
      return {
        job_title: job.title,
        company_name: job.company.name,
        location: job.location.city || job.location.region,
        salary_min: job.salary ? job.salary.min : null,
        apply_link: job.apply_link,
        job_description_plain: job.description.replace(/<[^>]*>/g, ''),
        // Thêm các trường khác theo nhu cầu
      };
    });
    return { json: { data: flattenedData } };
    ```

##### **G. Node "Google Sheets - Adding All Job Posts" (googleSheets)**
- **Mục đích**: Gửi dữ liệu vào Google Sheets.
- **Cấu hình**:
  - **Operation**: Append (thêm dữ liệu mới vào cuối sheet).
  - **Sheet Name**: Tên sheet đã được tạo sẵn (ví dụ: "Job Listings").
  - **Headers**: Các trường cần gửi vào sheet (ví dụ: `job_title`, `company_name`, `location`, ...).
  - **Credentials**: Chọn `googleSheetsOAuth2Api` đã kết nối trước đó.

##### **H. Node "Edit Fields" (set)**
- **Mục đích**: Chỉnh sửa hoặc thêm trường dữ liệu nếu cần.
- **Lưu ý**:
  - Có thể bỏ qua node này nếu dữ liệu đã được sắp xếp hoàn chỉnh trong node Code.

---

#### **3. Kích hoạt ⚡️**
1. **Test run dữ liệu mẫu**:
   - Điền thông tin vào form (hoặc chỉnh sửa body HTTP Request).
   - Chạy workflow với **Test Execution** để kiểm tra kết quả.
2. **Bật Active workflow**:
   - Sau khi kiểm tra thành công, chuyển workflow sang trạng thái **Active**.

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁC Ý TƯỚNG MỞ RỘNG]
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram** để thông báo khi có việc làm mới phù hợp.
   - Ví dụ: Gửi tin nhắn khi có việc làm ở vị trí "CMO" tại "Google" với mức lương từ 200M+.

2. **Lưu log hoạt động**:
   - Sử dụng node **HTTP Request** để gửi dữ liệu scrape vào một database hoặc service log như **Airtable** hoặc **Firebase**.

3. **Gửi báo cáo định kỳ**:
   - Thêm node **Google Sheets** hoặc **Email** để tự động gửi báo cáo tổng hợp về việc làm mới mỗi tuần.

4. **Tối ưu hóa prospecting**:
   - Sử dụng node **Code** để thêm các trường đánh giá (ví dụ: `priority_score`) dựa trên các tiêu chí như mức lương, vị trí, hoặc công ty.
   - Ví dụ: Cấp điểm cao hơn cho việc làm ở công ty đang tuyển nhiều vị trí.

5. **Kết hợp với CRM**:
   - Gửi dữ liệu vào **HubSpot**, **Salesforce**, hoặc **Zoho CRM** để quản lý lead tuyển dụng hoặc prospecting.

6. **Tự động hóa ứng tuyển**:
   - Sử dụng node **Email** hoặc **SMS** để tự động gửi ứng tuyển cho các việc làm phù hợp.

---

### 📌 **Kết luận**
Workflow này là giải pháp **tự động hóa hoàn hảo** để các sếp không cần phải quét thủ công danh sách việc làm trên LinkedIn. Bằng cách scrape và sàng lọc dữ liệu, workflow cung cấp **dữ liệu mới nhất và chính xác** để hỗ trợ tuyển dụng hoặc prospecting bán hàng.

**Hãy áp dụng ngay workflow này để:**
- **Tiết kiệm thời gian** và tập trung vào những việc quan trọng hơn.
- **Phát hiện cơ hội tuyển dụng mới** nhanh chóng và chính xác.
- **Tối ưu hóa chiến lược prospecting** bằng cách tiếp cận các công ty đang tuyển dụng.

**Bắt đầu từ hôm nay!** 🚀
Nếu có bất kỳ câu hỏi hoặc gặp khó khăn, các sếp có thể liên hệ với tác giả qua [email](mailto:Yaron@nofluff.online) hoặc tham khảo thêm tại [YouTube](https://www.youtube.com/@YaronBeen/videos) và [LinkedIn](https://www.linkedin.com/in/yaronbeen/).