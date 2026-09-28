---
title: "📥 Tự Động Hạ Tải File PDF Khi Nhận Yêu Cầu HTTP - Cách Tạo API Download File Miễn Code"
description: "Workflow này tự động trả về file PDF (hoặc bất kỳ file nào) khi nhận yêu cầu GET HTTP, giúp các sếp tiết kiệm thời gian quản lý tài liệu và cải thiện trải nghiệm người dùng. Đặc biệt phù hợp cho website, CRM hoặc hệ thống nội bộ."
slug: "tieu-dong-hoa-api-download-file"
tags: [n8n, automation, no-code, api-download, file-management, self-hosted]
keywords: [n8n workflow download file, tự động hóa API trả file, tự động hóa quản lý tài liệu, n8n webhook download, tự động hóa website]
---

# 🚀 **Tự Động Hạ Tải File PDF Khi Nhận Yêu Cầu HTTP (API Download File)**

### **Giải pháp nào cho các sếp khi phải thủ công gửi file cho khách hàng qua email hoặc link chia sẻ?**
Hãy tưởng tượng một tình huống: Khách hàng gửi yêu cầu tải file PDF (hoặc tài liệu khác) thông qua website, nhưng các sếp phải:
- **Tìm kiếm và gửi file thủ công** qua email hoặc link chia sẻ (Google Drive/Dropbox).
- **Quản lý nhiều yêu cầu đồng thời**, dẫn đến trễ hạn hoặc sai sót.
- **Không thể cá nhân hóa** trải nghiệm tải file (ví dụ: gửi file khác nhau cho từng khách hàng).

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Trả về file PDF (hoặc bất kỳ file nào)** khi nhận yêu cầu GET HTTP.
✅ **Không cần viết code**, chỉ cần cấu hình trên n8n.
✅ **Hoạt động 24/7** trên VPS riêng, không phụ thuộc vào máy chủ của bạn.
✅ **Cá nhân hóa** bằng cách truyền tham số (ví dụ: `?file=contract_2024.pdf`).

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **ổn định và an toàn**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** thay vì dùng phiên bản cloud.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đủ sức mạnh cho workflow này)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không phải tìm kiếm và gửi file thủ công.
- **Trải nghiệm người dùng tốt hơn**: Khách hàng tải file ngay lập tức khi truy cập link.
- **An toàn và kiểm soát**: File chỉ được trả về khi có yêu cầu hợp lệ (không phải chia sẻ link công khai).
- **Dễ mở rộng**: Có thể kết hợp với **Slack/Telegram** để thông báo khi file được tải.
- **Hoạt động liên tục**: Không phụ thuộc vào giờ làm việc của các sếp.
:::

---

### 🔧 **Yêu cầu cần thiết**
Để workflow này hoạt động, các sếp cần:
1. **File PDF (hoặc file khác)** muốn trả về, được lưu trên **máy chủ VPS** hoặc **URL công khai** (ví dụ: Google Drive, Dropbox).
2. **n8n Self-hosted** (cài đặt trên VPS).
3. **Thông tin cấu hình**:
   - **Đường dẫn API**: `https://[domain-cua-ban]/download-pdf` (do node Webhook định nghĩa).
   - **File mẫu**: Ví dụ `contract.pdf`, `invoice_2024.pdf` (có thể thay đổi bằng tham số GET).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
**Bước 1:** Tải workflow từ [đây](https://n8n.io/workflows/1920) hoặc copy JSON dưới đây vào **n8n Editor**:
```json
{
  "nodes": [
    {
      "parameters": {
        "path": "download-pdf",
        "method": "GET"
      },
      "name": "On GET request",
      "type": "n8n-nodes-base.webhook",
      "typeVersion": 1,
      "position": [
        250,
        300
      ]
    },
    {
      "parameters": {
        "url": "https://example.com/path/to/your/file.pdf",
        "method": "GET",
        "options": {}
      },
      "name": "Fetch binary file",
      "type": "n8n-nodes-base.httpRequest",
      "typeVersion": 1,
      "position": [
        450,
        300
      ]
    },
    {
      "parameters": {},
      "name": "Respond with attachment",
      "type": "n8n-nodes-base.respondToWebhook",
      "typeVersion": 1,
      "position": [
        650,
        300
      ]
    }
  ],
  "connections": [
    {
      "from": "On GET request",
      "to": "Fetch binary file"
    },
    {
      "from": "Fetch binary file",
      "to": "Respond with attachment"
    }
  ]
}
```
**Bước 2:** Dán JSON vào **n8n Editor** và nhấn **Import**.

---

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này có **3 node chính**, các sếp cần cấu hình kỹ lưỡng:

##### **Node 1: "On GET request" (Webhook)**
- **Tên node**: "On GET request"
- **Cấu hình**:
  - **Path**: Đặt là `download-pdf` (đường dẫn API sẽ là `https://[domain]/download-pdf`).
  - **Method**: Chọn **GET** (phù hợp cho yêu cầu tải file).
  - **Credentials**: Chọn **None** (hoặc thêm xác thực nếu cần).

##### **Node 2: "Fetch binary file" (HTTP Request)**
- **Tên node**: "Fetch binary file"
- **Cấu hình**:
  - **URL**: Điền **đường dẫn file** bạn muốn trả về:
    - **Nếu file trên máy chủ VPS**:
      `http://localhost:5678/path/to/your/file.pdf` (đảm bảo file có thể truy cập từ VPS).
    - **Nếu file trên Google Drive/Dropbox**:
      Sử dụng **URL chia sẻ công khai** (ví dụ: `https://drive.google.com/uc?id=FILE_ID`).
    - **Nếu file trên URL khác**:
      Đảm bảo URL đó **cho phép tải file** (không phải chỉ hiển thị).
  - **Method**: Chọn **GET**.
  - **Headers (nếu cần)**: Nếu file yêu cầu xác thực, thêm headers như `Authorization: Bearer [TOKEN]`.

##### **Node 3: "Respond with attachment" (Respond to Webhook)**
- **Tên node**: "Respond with attachment"
- **Cấu hình**:
  - **File to send**: Chọn **`Binary`** từ node trước (`Fetch binary file`).
  - **File name**: Đặt tên file trả về (ví dụ: `contract.pdf`).
  - **Content type**: Chọn **`application/pdf`** (hoặc `application/octet-stream` nếu file không phải PDF).

---
#### **3. Kích hoạt ⚡️**
**Bước 1:** Test workflow với **dữ liệu mẫu**:
1. Nhấn **Run Workflow** trong n8n Editor.
2. Kiểm tra **Output** của node cuối (`Respond with attachment`) để đảm bảo file trả về đúng.

**Bước 2:** Bật **Active** workflow.

**Bước 3:** Test từ bên ngoài:
- Mở trình duyệt và truy cập:
  `https://[domain-cua-ban]/download-pdf`
- Nếu cấu hình đúng, file sẽ tự động tải xuống.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Cá nhân hóa file tải**:
   - Thêm tham số GET vào URL, ví dụ:
     `https://[domain]/download-pdf?file=contract_2024.pdf`
   - Sử dụng **node `Set`** để xử lý tham số và thay đổi URL trong node `HTTP Request`.

2. **Gửi thông báo khi file tải**:
   - Kết nối với **Slack/Telegram** bằng node `webhook` để thông báo khi có yêu cầu tải file.

3. **Lưu log tải file**:
   - Thêm node **`Set`** để ghi thông tin (IP, thời gian tải) vào **Google Sheets** hoặc **Database**.

4. **Xác thực người dùng**:
   - Thêm **API Key** hoặc **JWT** vào yêu cầu GET để chỉ cho người dùng hợp lệ tải file.

5. **Mở rộng cho nhiều file**:
   - Sử dụng **node `Switch`** để chọn file tải dựa trên tham số GET.

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** để tự động hóa việc trả file khi nhận yêu cầu HTTP, giúp các sếp:
✔ **Tiết kiệm thời gian** quản lý tài liệu.
✔ **Cải thiện trải nghiệm người dùng** với tải file tức thì.
✔ **Hoạt động 24/7** trên VPS riêng.

**Hãy áp dụng ngay!** Nếu có vấn đề, các sếp có thể:
- **Comment dưới bài viết** để được hỗ trợ.
- **Xem video hướng dẫn** từ [n8n.io](https://n8n.io/workflows/1920).

**🚀 Chúc các sếp thành công!**