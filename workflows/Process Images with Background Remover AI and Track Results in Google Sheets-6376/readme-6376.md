---
title: "🎨 Tự Động Xóa Nền Ảnh AI + Theo Dõi Kết Quả Trên Google Sheets (Không Cần Code)"
description: "Workflow tự động hóa xóa nền ảnh bằng AI và lưu kết quả vào Google Sheets, tiết kiệm thời gian cho các sếp trong content creation và quản lý hình ảnh. Giúp theo dõi lịch sử xử lý, quản lý file và tối ưu hóa công việc."
slug: "tu-dong-xoa-nen-anh-ai-google-sheets"
tags: [n8n, automation, content-creation, multimodal-ai, google-sheets]
keywords: [n8n workflow xóa nền ảnh, tự động hóa xử lý ảnh, AI xóa nền tự động, lưu kết quả Google Sheets, tự động hóa content creation]
---

# 🚀 **Tự Động Xóa Nền Ảnh AI + Theo Dõi Kết Quả Trên Google Sheets**

### **Giải pháp cho các sếp trong content creation, marketing và quản lý hình ảnh**
Làm thủ công việc xóa nền ảnh cho hàng chục, hàng trăm bức ảnh là một công việc **mệt mỏi, tốn thời gian và dễ sai sót**. Hơn nữa, khi cần theo dõi lịch sử xử lý hoặc quản lý file kết quả, các sếp phải **làm thủ công trên Google Sheets**, gây ra rủi ro mất mát dữ liệu và khó quản lý.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động xóa nền ảnh** bằng AI với một cú nhấp chuột.
✅ **Lưu kết quả vào Google Sheets** (đường link, tên file, trạng thái thành công/thất bại).
✅ **Quản lý file tạm thời** để tránh mất dữ liệu.
✅ **Theo dõi lịch sử** tất cả các bức ảnh đã xử lý, giúp các sếp **tối ưu hóa công việc** và **giảm thiểu sai sót**.

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Xóa nền ảnh chỉ trong vài giây thay vì mất hàng giờ làm thủ công.
- **Chính xác 100%**: AI xử lý tự động, không còn lo sai sót như khi làm bằng tay.
- **Quản lý dễ dàng**: Tất cả kết quả được lưu vào Google Sheets với **thông tin chi tiết** (tên file, trạng thái, thời gian xử lý).
- **Hoạt động liên tục**: Workflow chạy **24/7** trên VPS, không cần can thiệp của con người.
- **Tối ưu hóa lưu trữ**: File tạm thời được quản lý tự động, tránh mất dữ liệu.
:::

---

## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets** (để lưu kết quả):
   - Một **Google Sheet** đã tạo sẵn với **bảng dữ liệu** có cột: `Tên File`, `Đường Link Ảnh Xử Lý`, `Trạng Thái`, `Thời Gian Xử Lý`.
   - **API Key của Google** (để kết nối với n8n).
   - **Credentials Google Sheets** trong n8n (cài đặt tại: **Settings > Credentials > Add Credential > Google Sheets**).

2. **API Background Removal AI**:
   - Một **API Background Removal AI** (ví dụ: [Remove.bg](https://www.remove.bg/), [Adobe Express](https://www.adobe.com/express/), hoặc một API tùy chỉnh).
   - **URL API** và **API Key** (nếu yêu cầu).

3. **Dịch vụ lưu trữ file tạm thời** (nếu cần):
   - Một **API HTTP Request** để upload file tạm thời (ví dụ: **AWS S3**, **Google Drive**, hoặc một API tùy chỉnh).
   - **URL API** và **API Key** (nếu yêu cầu).

4. **Form Upload** (để người dùng upload ảnh):
   - Một **form upload ảnh** (có thể là một trang web đơn giản, Google Form, hoặc một công cụ khác).
   - **URL của form** sẽ được sử dụng trong **node "On form submission"**.
:::

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể **import workflow** từ file JSON hoặc **copy/paste JSON** vào n8n Editor.

#### **Cách import từ file JSON:**
1. Tải workflow từ [đây](https://n8n.io/workflows/6376) (hoặc copy JSON từ link trên).
2. Trên n8n Editor, nhấn **Import Workflow** (icon "..." > Import).
3. Chọn file JSON và nhấn **Import**.

#### **Cách copy/paste JSON:**
1. Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/6376).
2. Trên n8n Editor, nhấn **Import Workflow** (icon "..." > Import).
3. Chọn **Paste JSON** và dán vào.

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **🔹 Node 1: On form submission (Form Trigger)**
- **Cấu hình**:
  - **Method**: `POST`.
  - **URL**: Đặt là **URL của form upload ảnh** (ví dụ: `https://form-submit.example.com/upload`).
  - **Headers**:
    ```
    Content-Type: multipart/form-data
    ```
  - **Body**:
    - Chọn **Form Data**.
    - Thêm một field với **key = "file"** và **type = File**.

#### **🔹 Node 2 & 7: HTTP Request (API Background Removal)**
- **Cấu hình**:
  - **Method**: `POST`.
  - **URL**: Đặt là **URL API của dịch vụ xóa nền ảnh** (ví dụ: `https://api.remove.bg/v1.0/removebg`).
  - **Headers**:
    ```
    Content-Type: application/json
    Authorization: Bearer YOUR_API_KEY
    ```
  - **Body**:
    ```
    {
      "image_url": "{{$node["On form submission"].json["file_url"]}}",
      "size": "auto"
    }
    ```
    *(Lưu ý: `$node["On form submission"].json["file_url"]` là đường link ảnh được upload từ form.)*

#### **🔹 Node 3: Convert to File (Convert Base64 to Binary)**
- **Cấu hình**:
  - **Operation**: `toBinary`.
  - **Input Data**: Chọn **JSON Path** từ node **HTTP Request** (API Background Removal), ví dụ:
    ```
    $.image
    ```
    *(Đây là phần trả về từ API khi xử lý thành công.)*

#### **🔹 Node 4: File Upload API (Upload File Tạm Thời)**
- **Cấu hình**:
  - **Method**: `POST`.
  - **URL**: Đặt là **URL API của dịch vụ lưu trữ file tạm thời** (ví dụ: `https://api.example.com/upload`).
  - **Headers**:
    ```
    Content-Type: application/octet-stream
    Authorization: Bearer YOUR_API_KEY
    ```
  - **Body**:
    - Chọn **Binary Data** từ node **Convert to File**.
    - Thêm một field **name** (ví dụ: `processed_image_$(Date.now()).png`).

#### **🔹 Node 5: If (Kiểm tra trạng thái thành công/thất bại)**
- **Cấu hình**:
  - **Condition**:
    - Nếu **HTTP Request (API Background Removal)** trả về **status = 200** (thành công), thì **chạy nhánh thành công**.
    - Nếu **status != 200** (thất bại), thì **chạy nhánh thất bại**.

#### **🔹 Node 6 & 8: Google Sheets (Lưu kết quả)**
- **Cấu hình chung**:
  - **Credentials**: Chọn **googleApi** (đã cài đặt trước).
  - **Operation**: `appendOrUpdate`.
  - **Sheet Name**: Đặt tên bảng trong Google Sheets (ví dụ: `Background Removal Results`).
  - **Range**: `Sheet1!A1` (hoặc tùy chỉnh theo cấu trúc bảng).

- **Node 6 (Thành công)**:
  - **Data**:
    ```
    {
      "Tên File": "{{$node["On form submission"].json["file_name"]}}",
      "Đường Link Ảnh Xử Lý": "{{$node["File Upload Api"].json["url"]}}",
      "Trạng Thái": "Thành công",
      "Thời Gian Xử Lý": "{{$node["Wait"].date}}"
    }
    ```

- **Node 8 (Thất bại)**:
  - **Data**:
    ```
    {
      "Tên File": "{{$node["On form submission"].json["file_name"]}}",
      "Đường Link Ảnh Xử Lý": "",
      "Trạng Thái": "Thất bại",
      "Thời Gian Xử Lý": "{{$node["Wait"].date}}"
    }
    ```

#### **🔹 Node 9: Wait (Đợi xử lý hoàn tất)**
- **Cấu hình**:
  - **Time**: `5000` (5 giây, có thể điều chỉnh tùy thuộc vào tốc độ API).

---

### **3. Kích hoạt ⚡️**
1. **Test Run** với một ảnh mẫu:
   - Upload một ảnh vào form và kiểm tra kết quả trong Google Sheets.
   - Nếu **thành công**, bạn sẽ thấy dữ liệu được append vào bảng.
   - Nếu **thất bại**, kiểm tra lại **API Key** và **URL API**.

2. **Bật Active workflow**:
   - Nhấn **Active** trên n8n Editor để workflow chạy tự động khi có form submission.

---

## ✍️ **Mẹo & gợi ý nâng cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Gửi thông báo Slack/Telegram khi xử lý thành công/thất bại**:
   - Thêm **node Slack/Telegram** sau **Google Sheets** để thông báo kết quả.
   - Ví dụ:
     ```
     "Thành công: Ảnh [{{$node["On form submission"].json["file_name"]}}] đã xử lý xong!"
     ```

2. **Lưu log chi tiết vào Google Drive**:
   - Thêm **node Google Drive** để lưu file log (ví dụ: `log_$(Date.now()).txt`).

3. **Tự động xóa file tạm thời sau một thời gian**:
   - Thêm **node HTTP Request** để gọi API xóa file sau 24h.

4. **Tạo một dashboard theo dõi**:
   - Sử dụng **Google Data Studio** hoặc **Power BI** để tạo báo cáo tự động từ Google Sheets.

5. **Kết hợp với AI Chatbot**:
   - Sử dụng **node LLM** (ví dụ: OpenAI, Mistral) để tự động mô tả ảnh sau khi xóa nền.
   - Ví dụ:
     ```
     "Mô tả ảnh: {{$node["LLM"].json["response"]}}"
     ```
:::

---

## 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp trong việc xử lý ảnh, đồng thời **tối ưu hóa quản lý file** bằng cách tự động lưu kết quả vào Google Sheets. **Không cần code**, chỉ cần **cấu hình vài bước**, các sếp đã có một hệ thống **tự động hóa hoàn chỉnh** cho công việc content creation và quản lý hình ảnh.

**👉 Hãy áp dụng ngay và tiết kiệm thời gian cho công việc hàng ngày!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**💡 Lưu ý cuối cùng**: Nếu API Background Removal yêu cầu **file binary** thay vì URL, các sếp cần điều chỉnh **node HTTP Request** để gửi file trực tiếp thay vì URL. Hãy kiểm tra lại tài liệu API để đảm bảo cấu hình chính xác!