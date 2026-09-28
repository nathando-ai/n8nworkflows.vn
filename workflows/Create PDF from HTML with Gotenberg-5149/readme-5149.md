---
title: "📄 Tự Động Tạo PDF từ HTML bằng Gotenberg - Không Cần Code!"
description: "Workflow tự động hóa hoàn toàn chuyển đổi HTML sang PDF với chất lượng chuyên nghiệp, tiết kiệm thời gian và giảm thiểu sai sót cho các sếp. Hoạt động liên tục 24/7, kết hợp với Gotenberg - giải pháp chuyển đổi tài liệu hàng đầu."
slug: "tay-dong-tao-pdf-tu-html-bang-gotenberg"
tags: [n8n, automation, no-code, gotenberg, pdf-generator, docker]
keywords: [n8n workflow pdf, tự động hóa tạo PDF, convert HTML to PDF, Gotenberg API, tự động hóa văn phòng]
---

# 🚀 **Tự Động Tạo PDF từ HTML với Gotenberg - Không Cần Code!**

### **Giải pháp nào giúp các sếp:**
- **Tiết kiệm hàng giờ** viết tay hoặc sử dụng phần mềm chuyển đổi PDF thủ công?
- **Chuyển đổi HTML sang PDF** với chất lượng chuyên nghiệp, **không cần kỹ năng code**?
- **Hoạt động tự động 24/7** mà không lo lỗi nhân sự?

Workflow này **giải quyết tất cả** bằng cách kết hợp **n8n** (tự động hóa không code) và **Gotenberg** (dịch vụ chuyển đổi tài liệu chuyên nghiệp). Dù là báo cáo hàng tháng, tài liệu marketing hay tài liệu nội bộ, các sếp chỉ cần cung cấp **HTML** và **tên file**, workflow sẽ tự động tạo PDF hoàn chỉnh với metadata tùy chỉnh (tên tác giả, tiêu đề, ngày tạo...).

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần viết tay hoặc sử dụng phần mềm chuyển đổi thủ công.
- **Chất lượng chuyên nghiệp**: PDF được tạo với định dạng chuẩn, hỗ trợ metadata tùy chỉnh.
- **Hoạt động liên tục**: Workflow chạy tự động 24/7, không phụ thuộc vào nhân sự.
- **Tích hợp dễ dàng**: Hoàn toàn không cần code, chỉ cần cấu hình đơn giản.
- **Docker-friendly**: Hoạt động ổn định khi n8n và Gotenberg cùng chạy trên Docker.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần:
1. **Gotenberg Service**:
   - Cài đặt và chạy **Gotenberg** trên Docker (hướng dẫn chi tiết dưới đây).
   - **URL mặc định**: `http://gotenberg:3000` (nếu n8n và Gotenberg cùng mạng Docker).
   - **Nếu Gotenberg hosted ngoài**: Cập nhật URL trong node `Convert to PDF with Gotenberg`.

2. **Docker Compose** (nếu tự host n8n):
   - Thêm dịch vụ Gotenberg vào `docker-compose.yml`:
     ```yaml
     gotenberg:
       image: gotenberg/gotenberg:8
       restart: always
     ```
   - Khởi động lại stack Docker sau khi thêm dịch vụ.

3. **Input cho workflow**:
   - **Cấu trúc JSON đầu vào**:
     ```json
     {
       "html": "<h1>Hello World</h1><p>Nội dung HTML của bạn...</p>",
       "file_name": "báo-cáo-tháng-12"
     }
     ```
   - **Yêu cầu**:
     - `html`: Chuỗi HTML đầy đủ cần chuyển đổi.
     - `file_name`: Tên file output (không cần thêm `.pdf`).
---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/5149) và import vào n8n Editor.
- **Copy/paste JSON** từ file vào n8n Editor (tab "Import/Export").

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **3 node chính**, các sếp cần chú ý cấu hình như sau:

##### **Node 1: Create index.html (convertToFile)**
- **Chức năng**: Chuyển đổi dữ liệu HTML đầu vào thành file tạm thời.
- **Lưu ý**:
  - Node này **không cần cấu hình thêm**, chỉ cần đảm bảo input có trường `html`.

##### **Node 2: Convert to PDF with Gotenberg (httpRequest)**
- **Chức năng**: Gửi yêu cầu API đến Gotenberg để chuyển đổi HTML thành PDF.
- **Cấu hình quan trọng**:
  - **URL**: Mặc định là `http://gotenberg:3000/api/convert` (nếu Gotenberg trên cùng mạng Docker).
    - **Nếu Gotenberg hosted ngoài**: Thay thế bằng URL chính xác (ví dụ: `https://api.gotenberg.app`).
  - **Headers**:
    - `Content-Type: application/json`.
  - **Body Parameters**:
    ```json
    {
      "url": "http://gotenberg:3000/api/convert",
      "body": {
        "html": "{{ $node["Create index.html"].json }}",
        "format": "pdf",
        "metadata": {
          "Author": "Tên tác giả",
          "Title": "Tiêu đề tài liệu",
          "Subject": "Chủ đề"
        }
      }
    }
    ```
    - **Tham số `metadata`**: Tùy chỉnh thông tin PDF (tác giả, tiêu đề, chủ đề...).
  - **Authentication**: Nếu Gotenberg yêu cầu API key, thêm vào headers (`Authorization: Bearer <API_KEY>`).

##### **Node 3: Create PDF from HTML (executeWorkflowTrigger)**
- **Chức năng**: Trả về file PDF đã tạo.
- **Lưu ý**:
  - Node này **không cần cấu hình**, chỉ cần đảm bảo node trước đó chạy thành công.

#### **3. Kích hoạt ⚡️**
1. **Test run** với dữ liệu mẫu:
   ```json
   {
     "html": "<h1>Báo cáo doanh thu</h1><p>Quý 1/2024</p>",
     "file_name": "báo-cáo-doanh-thu"
   }
   ```
2. **Bật Active workflow** trong n8n Editor.

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Tích hợp với Slack/Telegram**:
   - Sau khi tạo PDF, gửi kết quả qua Slack/Telegram thông báo hoàn tất.
   - **Node sử dụng**: `n8n-nodes-base.slack` hoặc `n8n-nodes-base.telegram`.

2. **Lưu log và báo cáo định kỳ**:
   - Sử dụng node `n8n-nodes-base.googleSheets` hoặc `n8n-nodes-base.sftp` để lưu lịch sử tạo PDF.
   - **Ví dụ**: Lưu tên file, ngày tạo, và metadata vào Google Sheets.

3. **Tự động tạo PDF từ email**:
   - Sử dụng node `n8n-nodes-base.imap` để lấy email chứa HTML, sau đó chuyển đổi thành PDF.
   - **Cấu hình**: Cấu hình IMAP để lấy email từ Gmail/Outlook, sau đó truyền vào workflow này.

4. **Tùy chỉnh thêm metadata động**:
   - Sử dụng node `n8n-nodes-base.function` để động tính metadata (ví dụ: ngày tạo tự động).
   - **Ví dụ**:
     ```javascript
     return {
       metadata: {
         Author: "Automation Team",
         Title: `Báo cáo - ${new Date().toLocaleDateString()}`,
         Subject: "Tự động hóa PDF"
       }
     };
     ```

5. **Chuyển đổi nhiều file HTML cùng lúc**:
   - Sử dụng node `n8n-nodes-base.set` để loop qua danh sách HTML và tạo PDF cho từng file.
   - **Node sử dụng**: `n8n-nodes-base.loop`.
---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn **tự động hóa tạo PDF từ HTML** mà không cần code. Với **Gotenberg** đảm bảo chất lượng chuyên nghiệp và **n8n** hoạt động 24/7, các sếp sẽ tiết kiệm thời gian, giảm thiểu sai sót và nâng cao hiệu suất làm việc.

**Hành động ngay!**
1. Cài đặt **Gotenberg** trên Docker (nếu chưa có).
2. Import workflow và cấu hình URL Gotenberg.
3. Test run với dữ liệu mẫu và **bật Active** để tự động hóa!

---
**💡 Lưu ý cuối cùng**:
- Nếu gặp lỗi **CORS** hoặc **timeout**, kiểm tra lại URL Gotenberg và cấu hình Docker.
- Đối với **Gotenberg hosted ngoài**, đảm bảo API key được cấu hình đúng trong headers.