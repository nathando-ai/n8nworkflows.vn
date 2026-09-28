---
title: "🚀 Chuyển PDF thành PNG Tự Động với PDF.co API (Hỗ Trợ Tất Cả Trang) - Không Cần Code!"
description: "Workflow tự động hóa chuyển đổi PDF thành PNG với chất lượng cao, hỗ trợ tất cả trang trong tài liệu, tiết kiệm thời gian và giảm thiểu sai sót cho các sếp. Áp dụng ngay để xử lý hàng trăm tài liệu chỉ trong vài giây!"
slug: "chuyen-doi-pdf-sang-png-voi-pdfco-api"
tags: [n8n, automation, no-code, pdf-to-png, pdf-co-api, tự động hóa văn phòng]
keywords: [n8n workflow chuyển đổi PDF, tự động hóa PDF sang PNG, PDF.co API, xử lý đa trang PDF, tự động hóa văn phòng không code]
---

# 🚀 **Chuyển PDF thành PNG Tự Động với PDF.co API (Hỗ Trợ Tất Cả Trang)**

### **📌 Nỗi Đau Của Các Sếp Khi Chuyển PDF sang PNG**
Các sếp thường phải mất **thời gian và công sức** để chuyển đổi PDF thành PNG thủ công, đặc biệt khi tài liệu có **trang số lớn** hoặc **được gửi hàng loạt**. Các vấn đề thường gặp bao gồm:
- **Sai sót trong quá trình chuyển đổi** (chất lượng kém, mất trang).
- **Tốn thời gian** (một tài liệu 50 trang có thể mất đến **30 phút** nếu làm thủ công).
- **Không hỗ trợ tự động hóa** (phải làm lại mỗi khi có tài liệu mới).
- **Không tối ưu hóa không gian lưu trữ** (PNG thường nhỏ hơn PDF khi được nén).

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Chuyển đổi toàn bộ trang PDF thành PNG** (không bỏ sót trang nào).
✅ **Tự động hóa hoàn toàn** (không cần can thiệp thủ công).
✅ **Nén kết quả thành ZIP** để tiết kiệm dung lượng lưu trữ.
✅ **Hỗ trợ hàng loạt tài liệu** (chỉ cần upload một lần, hệ thống xử lý tất cả).

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm thời gian**: Xử lý **hàng trăm tài liệu chỉ trong vài giây** thay vì mất giờ.
- **Chất lượng ổn định**: Không bị lỗi mất trang hoặc sai lệch hình ảnh.
- **Tự động hóa hoàn toàn**: Chỉ cần upload PDF, hệ thống làm tất cả.
- **Tối ưu dung lượng**: Kết quả được nén thành ZIP để lưu trữ hiệu quả.
- **Hỗ trợ đa trang**: Chuyển đổi **tất cả trang** trong một tài liệu duy nhất.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI BẮT ĐẦU**]
Để workflow hoạt động, các sếp cần:
1. **Tài khoản PDF.co API**:
   - Đăng ký miễn phí tại: [https://pdf.co/](https://pdf.co/)
   - Lấy **API Key** từ Dashboard (trong mục **API Keys**).
   - *Lưu ý*: Workflow này sử dụng **gói miễn phí** (có giới hạn số lượng yêu cầu/ngày).

2. **File PDF cần chuyển đổi**:
   - Có thể là **file từ máy tính**, **Google Drive**, hoặc **URL trực tiếp**.
   - Workflow có sẵn **2 ví dụ PDF** để test (không cần file riêng).

3. **N8n Self-hosted (khuyến nghị)**:
   - Để workflow chạy **24/7** mà không bị giới hạn của phiên bản cloud.
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow này:
- **Tải file JSON** từ [n8n.io/workflows/3847](https://n8n.io/workflows/3847) và import vào **n8n Editor**.
- **Copy JSON** từ link trên và **paste** vào **Create Workflow** trong n8n.

:::note[**Lưu ý quan trọng**]
- Nếu sử dụng **n8n Cloud**, lưu ý **gói miễn phí** có giới hạn số lượng yêu cầu API.
- Để **tối ưu hiệu suất**, các sếp nên **self-host** n8n trên VPS.
:::

---

#### **2. Các Bước Cấu Hình BẮT BUỘC**
Workflows này có **19 node**, nhưng chỉ **5 node chính** cần chú ý cấu hình:

##### **🔹 Node 1: "Get Presigned Upload URL (PDF.co)"**
- **Loại node**: `httpRequest`
- **Cấu hình**:
  - **Method**: `POST`
  - **URL**: `https://api.pdf.co/v2/pdf/convert/to/image`
  - **Headers**:
    ```
    {
      "x-pdfco-api-key": "API_KEY_CỦA_BẠN",
      "Content-Type": "application/json"
    }
    ```
  - **Body (JSON)**:
    ```json
    {
      "url": "URL_CỦA_FILE_PDF",
      "format": "png",
      "split": true
    }
    ```
  - *Lưu ý*: Thay `API_KEY_CỦA_BẠN` bằng key từ PDF.co và `URL_CỦA_FILE_PDF` bằng đường dẫn PDF (có thể là URL trực tiếp hoặc URL từ Presigned URL sau).

##### **🔹 Node 2: "Upload PDF to Presigned URL"**
- **Loại node**: `httpRequest`
- **Cấu hình**:
  - **Method**: `PUT`
  - **URL**: `Presigned_URL` (trả về từ node 1).
  - **Headers**:
    ```
    {
      "Content-Type": "application/pdf"
    }
    ```
  - **Body**: **Binary data** của file PDF (được truyền từ node trước).

##### **🔹 Node 3: "Convert PDF to PNG (PDF.co)"**
- **Loại node**: `httpRequest`
- **Cấu hình**:
  - **Method**: `POST`
  - **URL**: `https://api.pdf.co/v2/pdf/convert/to/image`
  - **Headers**:
    ```
    {
      "x-pdfco-api-key": "API_KEY_CỦA_BẠN",
      "Content-Type": "application/json"
    }
    ```
  - **Body (JSON)**:
    ```json
    {
      "url": "URL_TRẢ_VỀ_TỪ_NODE_2",
      "format": "png",
      "split": true
    }
    ```

##### **🔹 Node 4: "Compress into zip file"**
- **Loại node**: `compression`
- **Cấu hình**:
  - **Format**: `zip`
  - **File name**: `output_$(date +%Y%m%d).zip` (tự động đặt tên theo ngày).

##### **🔹 Node 5: "Loop over pdf files" (Nếu xử lý nhiều file)**
- **Loại node**: `splitInBatches`
- **Cấu hình**:
  - **Batch size**: `1` (để xử lý từng file một).
  - **Input**: Danh sách URL PDF (có thể từ Google Drive, Dropbox, hoặc URL trực tiếp).

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với **2 ví dụ PDF** đã có sẵn trong workflow:
   - Node **"GET example PDF files"** sẽ lấy 2 file mẫu.
   - Node **"Download example PDF Files"** sẽ tải xuống và xử lý.
2. **Bật Active** workflow sau khi kiểm tra thành công.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[**CÁCH ÁP DỤNG THỰC TIỆN**]
1. **Kết hợp với Google Drive/OneDrive**:
   - Sử dụng **node `google-drive`** để tự động lấy file PDF từ thư mục chia sẻ.
   - Cấu hình **webhook** để workflow chạy khi có file mới được upload.

2. **Gửi kết quả qua Slack/Email**:
   - Sau khi nén ZIP, sử dụng **node `slack`** hoặc **node `email`** để thông báo kết quả.
   - Ví dụ: *"Xử lý PDF thành công! Kết quả đã nén và gửi về [link]."*

3. **Lưu log cho theo dõi**:
   - Sử dụng **node `stickyNote`** để ghi lại lịch sử xử lý (file nào đã xử lý, thời gian, trạng thái).

4. **Tự động xóa file PDF sau xử lý**:
   - Thêm **node `httpRequest`** để gọi API xóa file từ Google Drive/PDF.co sau khi chuyển đổi.

5. **Tối ưu API Key**:
   - Sử dụng **node `set`** để lưu API Key vào **Credentials** của n8n để tránh phải nhập lại.
   - Cách làm:
     - Tạo **Credentials** mới trong n8n (Settings > Credentials).
     - Chọn loại **`API Key`** và nhập `API_KEY_CỦA_BẠN`.
     - Trong node `httpRequest`, chọn **Credentials** này thay vì nhập trực tiếp.
:::

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** để các sếp tự động hóa **chuyển đổi PDF sang PNG** một cách **nhanh chóng, chính xác và không cần code**. Bằng cách sử dụng **PDF.co API** và **n8n**, các sếp có thể:
✔ **Tiết kiệm hàng giờ** mỗi tuần.
✔ **Tránh sai sót** do chuyển đổi thủ công.
✔ **Tối ưu dung lượng lưu trữ** với file ZIP.
✔ **Xử lý hàng loạt file** chỉ với một cú nhấp chuột.

**🚀 Hãy áp dụng ngay workflow này và tự động hóa công việc của mình!**
Nếu có vấn đề, các sếp có thể liên hệ với tác giả **Ludwig** qua [LinkedIn](https://www.linkedin.com/in/ludwiggerdes/) hoặc [website](https://www.ludwiggerdes.com/) (nếu có).

---
**🔥 Mẹo cuối**: Để workflow chạy **24/7** mà không bị giới hạn, các sếp nên **self-host n8n** trên VPS. 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) với mã giảm giá **VPSN8N**!