---
title: "🚀 Chuyển Đổi PDF, DOC, Hình Ảnh Sang Markdown Tự Động Với Datalab.to API (Không Cần Code)"
description: "Tự động hóa chuyển đổi file PDF, DOCX, PNG, JPG sang định dạng Markdown để chuẩn bị dữ liệu cho mô hình AI/LLM. Giúp tiết kiệm thời gian, tăng hiệu suất xử lý và tích hợp dễ dàng với các workflow AI hiện đại."
slug: "chuyen-doi-file-sang-markdown-datalab-to"
tags: [n8n, automation, document-extraction, multimodal-ai, datalab-to, no-code]
keywords: [n8n workflow chuyển đổi file, tự động hóa PDF sang Markdown, API Datalab.to, xử lý văn bản AI, tự động hóa văn phòng]
---

# 🚀 **Tự Động Hóa Chuyển Đổi PDF/DOC/Hình Ảnh Sang Markdown Cho AI (Không Cần Code)**

## **🔥 Nỗi Đau Của Các Sếp Và Giải Pháp Tự Động Hóa**
Các sếp thường phải mất **giờ đồng hồ** để chuyển đổi file PDF, DOCX, hoặc hình ảnh thành định dạng Markdown để:
- **Chuẩn bị dữ liệu cho mô hình AI/LLM** (chẳng hạn như ChatGPT, Llama, hoặc các ứng dụng xử lý văn bản tự động).
- **Tạo nội dung SEO** từ tài liệu gốc mà không cần viết từ đầu.
- **Tích hợp dữ liệu vào hệ thống quản lý nội dung** (CMS) hoặc công cụ phân tích.

**Workflow này giải quyết vấn đề đó 100% tự động hóa**, chỉ cần **1 lần setup**, sau đó **chạy 24/7** mà không cần can thiệp thủ công.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm thời gian**: Chuyển đổi hàng trăm file chỉ trong vài giây thay vì nhiều giờ.
- **Chuẩn hóa dữ liệu**: Markdown là định dạng **tối ưu cho AI**, giúp mô hình hiểu và xử lý nội dung hiệu quả hơn.
- **Tích hợp dễ dàng**: Kết quả có thể được sử dụng ngay trong **LLM, Slack, Notion, hoặc các hệ thống AI khác**.
- **Hoạt động liên tục**: Workflow chạy tự động khi có file mới được nộp (ví dụ: qua form hoặc thư mục).
:::

---
## **🔧 Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Datalab.to** (đăng ký [tại đây](https://www.datalab.to/)) và **API Key**:
   - Đăng ký miễn phí để nhận **$5 credit** (đủ để thử nghiệm).
   - **Lưu ý**: Nhập thông tin thanh toán (ngay cả nếu không mua) để kích hoạt credit.
2. **File cần chuyển đổi**:
   - Hỗ trợ các định dạng: **PDF, DOCX, PNG, JPG, WEBP**.
3. **N8n Self-hosted** (không dùng phiên bản cloud để đảm bảo **ổn định 24/7**).

:::info[**Gợi ý hạ tầng cho n8n**]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
## **🚀 Cách Import & Cấu Hình Workflow**

### **1. Import Workflow 📥**
Các sếp có thể **import** workflow từ file JSON hoặc **copy/paste** JSON vào **n8n Editor**:
- **Tải file JSON** từ [đây](https://n8n.io/workflows/7887) (nút "Export").
- Mở **n8n Editor** → Nhấn **"Import"** → Dán JSON hoặc tải file.

### **2. Các Bước Cấu Hình BẮT BUỘC**
Workflow gồm **6 node chính**, các sếp cần chú ý cấu hình như sau:

#### **🔹 Node 1: "On form submission" (formTrigger)**
- **Mục đích**: Nhận file từ **form n8n** (hoặc thay thế bằng **HTTP Request** nếu muốn nhận file từ bên ngoài).
- **Cấu hình**:
  - Chọn **type**: `Form`.
  - Thêm **fields** để chọn file (ví dụ: `file` với type `File`).
  - **Lưu ý**: Nếu muốn nhận file từ **Google Drive/Dropbox**, thay thế bằng node **HTTP Request** với URL upload.

#### **🔹 Node 2 & 3: "Send to Datalab API" (httpRequest)**
- **Mục đích**: Gửi file lên **Datalab.to API** để chuyển đổi sang Markdown.
- **Cấu hình**:
  - **URL**: `https://api.datalab.to/v1/marker`
  - **Headers**:
    - `X-API-Key`: Điền **API Key** từ Datalab.to.
    - `Content-Type`: `multipart/form-data`.
  - **Body (Payload)**:
    - Thêm **file** từ node trước (node `formTrigger`).
    - **Lưu ý**: Theo [API reference](https://www.datalab.to/redoc#operation/marker_api_v1_marker_post), có thể thêm tham số tùy chỉnh như `format=markdown`.
  - **Example payload**:
    ```json
    {
      "file": "{{$node["On form submission"].json["file"]}}",
      "format": "markdown"
    }
    ```

#### **🔹 Node 4: "Set Fields" (set)**
- **Mục đích**: Lưu trữ kết quả tạm thời trước khi xử lý tiếp.
- **Cấu hình**:
  - Thêm **fields** cần lưu (ví dụ: `markdownContent`, `fileName`).
  - **Lưu ý**: Node này giúp **truyền dữ liệu** sang node tiếp theo.

#### **🔹 Node 5: "Wait" (wait)**
- **Mục đích**: Chờ kết quả từ API (tránh lỗi timeout).
- **Cấu hình**:
  - **Thời gian chờ**: **10-30 giây** (thời gian xử lý phụ thuộc vào kích thước file).
  - **Lưu ý**: Nếu file lớn, tăng thời gian chờ lên **60 giây**.

#### **🔹 Node 6: "Switch" (switch)**
- **Mục đích**: Kiểm tra kết quả API:
  - Nếu thành công (`success`), chuyển sang node tiếp theo (ví dụ: **Slack/Email**).
  - Nếu thất bại (`failed`), chuyển sang **node Wait** để thử lại.
- **Cấu hình**:
  - **Condition 1**: `{{$json["status"] === "success"}}` → Chuyển sang node thành công.
  - **Condition 2**: `{{$json["status"] === "failed"}}` → Chuyển sang node **Wait** để thử lại.

---
### **3. Kích Hoạt Workflow ⚡️**
1. **Test Run** với một file mẫu:
   - Nộp file lên **form n8n** (hoặc gọi API nếu dùng HTTP Request).
   - Kiểm tra **log** trong n8n để xác nhận kết quả.
2. **Bật Active**:
   - Nhấn **"Active"** trên canvas.
   - **Lưu ý**: Nếu dùng **formTrigger**, workflow sẽ chạy khi có submission.

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**
### **1. Tích Hợp Với Slack/Telegram**
- Sau khi chuyển đổi thành công, **gửi kết quả** qua Slack/Telegram để thông báo:
  ```json
  {
    "text": "File {{$node["On form submission"].json["fileName"]}} đã chuyển đổi thành Markdown thành công!",
    "attachments": [
      {
        "color": "#28a745",
        "text": "{{$node["Set Fields"].json["markdownContent"]}}"
      }
    ]
  }
  ```

### **2. Lưu Log Vào Google Sheets**
- Sử dụng **Google Sheets** để theo dõi lịch sử chuyển đổi:
  - Node **HTTP Request** → Gửi dữ liệu lên API Google Sheets.
  - **Example payload**:
    ```json
    {
      "values": [
        [
          "{{$node["On form submission"].json["fileName"]}}",
          "{{$node["Set Fields"].json["markdownContent"]}}",
          "{{new Date().toISOString()}}"
        ]
      ]
    }
    ```

### **3. Chuyển Đổi Batch (Lô File)**
- Sử dụng **node `List Files`** (n8n-nodes-base.fileSystem) để quét thư mục và chuyển đổi **tất cả file** trong đó.
- **Cấu hình**:
  - Thêm node **`List Files`** trước `formTrigger`.
  - Sử dụng **`Loop`** để xử lý từng file.

### **4. Tối Ưu Hóa API Key**
- Nếu dùng nhiều workflow, **tạo credentials riêng** cho Datalab.to trong n8n:
  - **Settings → Credentials → Add Credential** (type: `HTTP Header Auth`).
  - Đặt tên: `Datalab-API-Key` và điền **API Key**.

---
## **📌 Kết Luận**
Workflow này giúp **các sếp tự động hóa chuyển đổi file sang Markdown chỉ trong vài phút setup**, sau đó **chạy tự động** mà không cần can thiệp. **Kết quả** là:
✅ **Tiết kiệm thời gian** so với làm thủ công.
✅ **Chuẩn hóa dữ liệu** cho AI/LLM.
✅ **Tích hợp dễ dàng** với Slack, Google Sheets, hoặc các hệ thống khác.

**Hãy thử ngay và tự động hóa quy trình của mình!** 🚀

---
### **🔗 Liên Hệ Với Chuyên Gia (Nếu Cần Hỗ Trợ)**
Nếu các sếp cần **cấu hình chi tiết hơn** hoặc **tùy chỉnh workflow**, có thể liên hệ với tác giả:
- **Email**: [joseph@uppfy.com](mailto:joseph@uppfy.com)
- **Twitter**: [@juppfy](https://x.com/juppfy)