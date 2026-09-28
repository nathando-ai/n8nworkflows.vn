---
title: "🔄 Chuyển HTML sang PDF + Nén File Tự Động - Giải Pháp Tiết Kiệm Thời Gian Cho Các Sếp"
description: "Tự động hóa quy trình chuyển đổi HTML thành PDF và nén file PDF với công cụ CustomJS API, giúp các sếp tiết kiệm thời gian và tối ưu dung lượng file. Hoạt động liên tục 24/7 mà không cần code."
slug: "chuyen-html-sang-pdf-nen-file-tu-dong"
tags: [n8n, automation, no-code, pdf-toolkit, customjs, design]
keywords: [n8n workflow chuyển HTML sang PDF, tự động hóa PDF, nén file PDF, công cụ chuyển đổi HTML, API CustomJS]
---

# 🚀 Chuyển HTML sang PDF + Nén File Tự Động - Không Cần Code!

### 💡 **Nỗi Đau Của Các Sếp**
Các sếp thường phải mất thời gian quý báu để:
- Chuyển đổi các trang web hoặc nội dung HTML thành file PDF để chia sẻ.
- Nén file PDF để tiết kiệm dung lượng, đặc biệt khi phải gửi qua email hoặc lưu trữ.
- Lặp lại quá trình này hàng tuần, hàng tháng, gây mất hiệu suất.

**Giải pháp?** Một workflow tự động hóa hoàn toàn với **n8n + CustomJS PDF Toolkit** sẽ giúp các sếp:
✅ **Chuyển đổi HTML sang PDF chỉ với một cú nhấp chuột**.
✅ **Nén file PDF để giảm dung lượng** (tối ưu cho lưu trữ và chia sẻ).
✅ **Hoạt động liên tục 24/7** mà không cần can thiệp thủ công.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần chuyển đổi thủ công, nén file PDF chỉ trong giây lát.
- **Tối ưu dung lượng**: File PDF được nén nhỏ hơn, thuận tiện cho lưu trữ và chia sẻ.
- **Chính xác 100%**: Không sai sót như khi làm thủ công.
- **Hoạt động tự động**: Hoạt động liên tục, không phụ thuộc vào giờ làm việc.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow này hoạt động, các sếp cần:
1. **Tài khoản CustomJS API**:
   - Đăng ký tại [CustomJS](https://customjs.com/) và lấy **API Key**.
   - Thêm **credentials** trong n8n với tên `customJsApi` và gắn API Key vào.
2. **URL HTML hoặc nội dung HTML**:
   - Có thể là một trang web công khai (URL) hoặc nội dung HTML trực tiếp.
3. **n8n Self-hosted** (khuyến nghị):
   - Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng**.
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Truy cập [n8n Workflows](https://n8n.io/workflows/3869) và tải file JSON.
2. Trong n8n Editor, nhấn **Import Workflow** và chọn file JSON tải xuống.
   *Hoặc* copy toàn bộ JSON và dán vào **Import Workflow** trong tab **Workflow**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này bao gồm **5 node** chính, các sếp cần chú ý cấu hình sau:

##### **Node 1: "Set PDF URL" (Code)**
- **Mục đích**: Đặt URL của file HTML hoặc nội dung HTML cần chuyển đổi.
- **Cách cấu hình**:
  - Mở node **Code** và chỉnh sửa mã như sau (thay thế `https://example.com` bằng URL thực tế):
    ```javascript
    return [
      {
        json: {
          html: '<html><body><h1>Hello World</h1></body></html>', // Hoặc URL: "https://example.com"
          url: "https://example.com" // Chọn một trong hai: nội dung HTML hoặc URL
        }
      }
    ];
    ```
  - **Lưu ý**:
    - Nếu sử dụng **nội dung HTML trực tiếp**, bỏ comment `url` và chỉ giữ phần `html`.
    - Nếu sử dụng **URL**, bỏ comment `html` và chỉ giữ phần `url`.

##### **Node 2: "HTML to PDF" (CustomJS HTML2PDF)**
- **Mục đích**: Chuyển đổi HTML thành PDF.
- **Cấu hình**:
  - Chọn **credentials** là `customJsApi` (đã thêm API Key trước đó).
  - Node này sẽ tự động xử lý chuyển đổi từ dữ liệu đầu vào (HTML/URL).

##### **Node 3 & 4: "Compress PDF file" (CustomJS CompressPDF)**
- **Mục đích**: Nén file PDF để giảm dung lượng.
- **Cấu hình**:
  - Chọn **credentials** là `customJsApi`.
  - Node này sẽ tự động nén file PDF thành binary và trả về kết quả.

##### **Node 5: "When clicking ‘Test workflow’" (Manual Trigger)**
- **Mục đích**: Khởi động workflow thủ công.
- **Cách sử dụng**:
  - Nhấn nút **Test Workflow** để chạy thử với dữ liệu đã cấu hình.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhấn **Test Workflow** để kiểm tra quá trình chuyển đổi và nén.
   - Kiểm tra **output** để đảm bảo file PDF được tạo và nén thành công.
2. **Bật Active**:
   - Sau khi test thành công, chuyển workflow sang **Active** để hoạt động tự động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Gửi PDF qua Email/Slack**:
   - Kết hợp với node **Email** hoặc **Slack** để tự động gửi file PDF đã nén cho đội nhóm.
2. **Lưu Log & Theo Dõi**:
   - Sử dụng node **Google Sheets** hoặc **Airtable** để lưu lịch sử chuyển đổi và nén file.
3. **Chuyển Đổi Batch**:
   - Tạo một **Webhook** để nhận danh sách URL HTML và xử lý batch tự động.
4. **Tích Hợp với CRM**:
   - Gửi file PDF cho khách hàng qua **Zapier** hoặc **Make (Integromat)** khi có đơn hàng mới.
:::

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa quy trình chuyển đổi HTML sang PDF và nén file một cách **nhanh chóng, chính xác và không cần code**. Với **n8n + CustomJS**, các sếp không chỉ tiết kiệm thời gian mà còn tối ưu hóa lưu trữ và chia sẻ file.

**Hãy áp dụng ngay và tự động hóa công việc của mình!** 🚀

---
:::note[LƯU Ý CUỐI CUNG]
- Nếu gặp lỗi, kiểm tra lại **credentials** của CustomJS API và **URL/nội dung HTML** đầu vào.
- Để workflow hoạt động 24/7, **self-hosted n8n** là lựa chọn tối ưu nhất.
:::