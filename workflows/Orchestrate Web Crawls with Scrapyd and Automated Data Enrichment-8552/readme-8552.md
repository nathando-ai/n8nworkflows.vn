---
title: "🚀 Tự Động Hóa Quá Trình Crawl Web Tối Ưu với Scrapyd + Scrapy + Enrichment AI (N8n)"
description: "Workflow này tự động hóa toàn bộ chu trình crawl web từ Scrapyd: khởi động, theo dõi, thu thập, xử lý và enrich dữ liệu thành JSON cấu trúc, sẵn sàng cho tự động hóa tiếp theo. Giúp các sếp tiết kiệm 80% thời gian thủ công và đảm bảo dữ liệu chính xác, deduplicated."
slug: "tieu-dong-hoa-crawl-web-scrapyd-n8n"
tags: [n8n, automation, web-scraping, scrapyd, data-enrichment, no-code]
keywords: [n8n workflow crawl web, tự động hóa scrapy, enrich dữ liệu web, scrapyd automation, data pipeline]
---

# 🚀 **Tự Động Hóa Quá Trình Crawl Web Tối Ưu với Scrapyd + Scrapy + Enrichment AI**

## **🔍 Nỗi Đau Của Các Sếp Khi Làm Thủ Công**
Hiện nay, việc crawl website để thu thập dữ liệu sản phẩm (giá cả, thông tin chi tiết, hình ảnh...) thường là một quá trình **mệt mỏi, tốn thời gian và dễ sai sót**:
- **Khởi động và theo dõi crawl thủ công**: Các sếp phải chạy Scrapy spider qua Scrapyd, sau đó phải check status liên tục để tránh mất dữ liệu.
- **Dữ liệu rác và trùng lặp**: Sau khi crawl, dữ liệu thường chứa nhiều bản ghi trùng lặp (cùng 1 sản phẩm nhưng giá khác nhau) hoặc thiếu thông tin cấu trúc.
- **Không có dữ liệu enrich**: Dữ liệu thu thập được thường chỉ là HTML thô hoặc JSON không sắp xếp, khó sử dụng cho phân tích tiếp theo.
- **Không có log hoặc debug**: Khi crawl thất bại, các sếp phải tra cứu log thủ công, mất nhiều thời gian.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách tự động hóa toàn bộ chu trình crawl, từ khởi động đến enrich dữ liệu, với kết quả sẵn sàng sử dụng cho các hệ thống tiếp theo.**

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 80% thời gian**: Không cần theo dõi crawl thủ công, tự động hóa từ A-Z.
✅ **Dữ liệu sạch và deduplicated**: Loại bỏ trùng lặp, giữ chỉ bản ghi giá thấp nhất cho mỗi sản phẩm.
✅ **Enrich tự động**: Trích xuất thông tin cấu trúc (ID, tên sản phẩm, thương hiệu, model, giá...) và thêm metadata (domain, nguồn, timestamp).
✅ **Debug và log sẵn sàng**: Lấy được logs, screenshots và HTML dump để phân tích lỗi.
✅ **Hoạt động 24/7**: Chạy liên tục trên VPS, không phụ thuộc vào người dùng.
✅ **Sẵn sàng cho tự động hóa tiếp theo**: Dữ liệu JSON cấu trúc có thể kết nối với Slack, Email, CRM, hoặc AI để phân tích sâu hơn.
:::

---
## **🔧 Yêu Cầu Cần Thiết**
Để workflow này hoạt động, các sếp cần chuẩn bị:
### **1. Hệ Thống Scrapyd**
- **Scrapyd Server**: Đã cài đặt và chạy (n8n sẽ gửi yêu cầu crawl qua API của Scrapyd).
- **Scrapy Spider**: Đã tạo và deploy lên Scrapyd (cần cấu hình tham số như `project`, `spider`, `config_path`).
- **API Key Scrapyd**: Để n8n gửi yêu cầu crawl (thường là `scrapyd-api-key` trong config của Scrapyd).

### **2. API Keys và Credentials**
| Node | Tham Số Cần Điền | Ghi Chú |
|------|------------------|---------|
| **run_job** | `URL Scrapyd API` | Ví dụ: `http://<your-scrapyd-server>/schedule.json` |
| **job_list** | `URL Scrapyd API` | Ví dụ: `http://<your-scrapyd-server>/listjobs.json` |
| **check_items** | `URL Scrapyd API` | Ví dụ: `http://<your-scrapyd-server>/getjobresult.json` |
| **job_log** | `URL Scrapyd API` | Ví dụ: `http://<your-scrapyd-server>/getjoblogs.json` |
| **DL-html / DL-screenshots** | `URL lưu trữ** | Nếu muốn lưu HTML hoặc screenshot vào cloud (S3, Google Drive, FTP...). |

### **3. Webhook (Nếu Sử Dụng)**
- **URL Webhook**: Để workflow trả về kết quả crawl dưới dạng JSON (có thể kết nối với Slack, Email, hoặc hệ thống khác).

---
## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Cách 1: Import từ File JSON**
1. Tải workflow từ [n8n.io/workflows/8552](https://n8n.io/workflows/8552) (chọn **Export as JSON**).
2. Trên n8n Editor, nhấn **Import** và chọn file JSON vừa tải.
3. Chọn **Create new workflow** và nhấn **Import**.

#### **Cách 2: Copy/Paste JSON**
1. Mở n8n Editor và tạo workflow mới.
2. Nhấn **Import** → **Paste JSON** và dán toàn bộ mã JSON từ workflow.
3. Chọn **Create new workflow**.

---
### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **21 node**, nhưng các node **quan trọng nhất** cần cấu hình kỹ là:

#### **🔹 Node `run_job` (HTTP Request)**
- **Method**: `POST`
- **URL**: `http://<your-scrapyd-server>/schedule.json`
- **Headers**:
  ```json
  {
    "Authorization": "Basic <scrapyd-api-key>",
    "Content-Type": "application/json"
  }
  ```
- **Body (JSON)**:
  ```json
  {
    "project": "your_project_name",
    "spider": "your_spider_name",
    "settings": {
      "config": "path/to/your/config.json"
    },
    "args": {
      "q": "{{$input}}",  // Tham số search từ input (ví dụ: từ webhook)
      "sci": "100",
      "prs": "10",
      "pages": "5"
    }
  }
  ```
  - **Lưu ý**: Thay thế `your_project_name`, `your_spider_name` và `path/to/your/config.json` theo cấu hình của Scrapyd.

#### **🔹 Node `filter_job` (Code)**
- **Lógica**: Lọc job mới tạo trong danh sách `job_list` để theo dõi status.
- **Mã JavaScript**:
  ```javascript
  // Kiểm tra job mới nhất có status "running" hay "pending"
  const newJob = $input.all().find(job => job.status === "running" || job.status === "pending");
  if (!newJob) {
    return { json: { status: "no_job_running" } };
  }
  return { json: { job_id: newJob.job_id } };
  ```

#### **🔹 Node `check_job_status` (If)**
- **Điều kiện**:
  - **Nếu status = "finished"**: Tiến hành thu thập kết quả (`check_items`).
  - **Nếu status = "running"**: Chờ 5 giây (`Wait3`) rồi kiểm tra lại.
  - **Nếu status = "error"**: Gửi cảnh báo (có thể kết nối với Slack/Email).

#### **🔹 Node `Filter-result` (Code)**
- **Lógica**: Xử lý JSONL thu thập từ `check_items` để:
  1. **Deduplicate** bằng URL (giả sử có field `url`).
  2. **Trích xuất thông tin cấu trúc**:
     ```json
     {
       "id": "{{$json.id}}",
       "partNo": "{{$json.partNo}}",
       "make": "{{$json.make}}",
       "model": "{{$json.model}}",
       "partName": "{{$json.partName}}",
       "price": "{{$json.price}}",
       "domain": "{{$input.domain}}",
       "source": "{{$input.source}}",
       "timestamp": "{{new Date().toISOString()}}"
     }
     ```
  3. **Sắp xếp** theo giá tăng dần (`price`).
- **Mã JavaScript**:
  ```javascript
  const items = $input.all();
  const uniqueItems = [];
  const seenUrls = new Set();

  items.forEach(item => {
    if (!seenUrls.has(item.url)) {
      seenUrls.add(item.url);
      uniqueItems.push({
        id: item.id,
        partNo: item.partNo,
        make: item.make,
        model: item.model,
        partName: item.partName,
        price: item.price,
        domain: $input.domain,
        source: $input.source,
        timestamp: new Date().toISOString()
      });
    }
  });

  // Sắp xếp theo giá tăng dần
  uniqueItems.sort((a, b) => a.price - b.price);
  return { json: uniqueItems };
  ```

#### **🔹 Node `DL-html` và `DL-screenshots` (HTTP Request)**
- **Nếu muốn lưu HTML hoặc screenshot**:
  - Cấu hình URL lên **Google Drive, S3, hoặc FTP**.
  - Ví dụ cho `DL-html`:
    ```json
    {
      "method": "POST",
      "url": "https://www.googleapis.com/upload/drive/v3/files?uploadType=multipart",
      "headers": {
        "Authorization": "Bearer {{$env.GOOGLE_DRIVE_API_KEY}}",
        "Content-Type": "application/json"
      },
      "body": {
        "name": "crawl_${$input.timestamp}.html",
        "parents": ["{{$env.GOOGLE_DRIVE_FOLDER_ID}}"]
      }
    }
    ```

#### **🔹 Node `Respond to Webhook` (respondToWebhook)**
- **Cấu hình**:
  - **Method**: `POST`
  - **Headers**:
    ```json
    {
      "Content-Type": "application/json"
    }
    ```
  - **Body**: Trả về JSON enrich đã xử lý:
    ```json
    {
      "status": "success",
      "data": "{{$input}}",
      "timestamp": "{{new Date().toISOString()}}"
    }
    ```

---
### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhấn **Execute Workflow** và nhập tham số search (ví dụ: `"iphone 15"`).
   - Kiểm tra các node quan trọng (`check_job_status`, `Filter-result`, `Respond to Webhook`).
2. **Bật Active**:
   - Sau khi test thành công, chuyển workflow sang **Active**.

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**
### **1. Kết Nối với Slack/Telegram**
- Sử dụng node **Slack** hoặc **Telegram Bot** để gửi cảnh báo khi:
  - Crawl hoàn thành.
  - Crawl thất bại (status `error`).
  - Dữ liệu trống (`empty_result`).

### **2. Lưu Log vào Email**
- Sử dụng node **Email** để gửi log (`job_log`) định kỳ (ví dụ: hàng ngày).

### **3. Tự Động Xóa Job Cũ**
- Thêm node **HTTP Request** để gọi API Scrapyd để xóa job cũ sau khi crawl xong:
  ```json
  {
    "method": "POST",
    "url": "http://<your-scrapyd-server>/delete.json",
    "body": {
      "job_id": "{{$input.job_id}}"
    }
  }
  ```

### **4. Kết Nối với AI (LLM) để Trích Xuất Thông Tin**
- Sử dụng node **LLM** (ví dụ: Mistral, GPT-4) để enrich dữ liệu thêm thông tin như:
  - **Tóm tắt sản phẩm** (summary).
  - **Phân loại sản phẩm** (category).
  - **Phân tích giá cả** (trend).

### **5. Lưu Dữ Liệu vào Database**
- Kết nối với **PostgreSQL, MySQL, hoặc MongoDB** để lưu dữ liệu enrich vào bảng/collection.

---
## **📌 Kết Luận**
Workflow này là **công cụ hoàn hảo** cho các sếp cần tự động hóa quá trình crawl web một cách **chuyên nghiệp, sạch sẽ và hiệu quả**. Bằng cách kết hợp **Scrapyd, Scrapy, và n8n**, các sếp không chỉ tiết kiệm thời gian mà còn đảm bảo dữ liệu **được enrich, deduplicated và sẵn sàng sử dụng** cho các hệ thống tiếp theo.

### **🔥 Bước Tiếp Theo**
1. **Cài đặt Scrapyd** và deploy spider (nếu chưa có).
2. **Import workflow** và cấu hình API keys.
3. **Test với dữ liệu mẫu** và điều chỉnh logic trong node `Filter-result`.
4. **Kết nối với Slack/Email** để nhận thông báo.
5. **Chạy liên tục** trên VPS để crawl 24/7!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**🚀 Hãy tự động hóa crawl web của mình ngay hôm nay!** 🚀