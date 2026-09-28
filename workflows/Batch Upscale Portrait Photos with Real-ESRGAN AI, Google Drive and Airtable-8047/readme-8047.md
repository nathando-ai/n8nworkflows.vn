---
title: "🎨 **Tự Động Hóa Upscale Ảnh Cổ Điển với AI Real-ESRGAN, Google Drive & Airtable – Không Cần Code!**"
description: "Workflow tự động hóa upscale ảnh chân dung từ Airtable lên chất lượng 4K với AI Real-ESRGAN, lưu trữ tự động trên Google Drive. Giúp các sếp tiết kiệm thời gian, nâng cao chất lượng hình ảnh cho dự án marketing, blog hoặc thương hiệu cá nhân."
slug: "tieu-dong-hoa-upscale-anh-chan-dung-ai-realesrgan"
tags: [n8n, automation, AI, Google Drive, Airtable, content-creation, no-code]
keywords: [n8n workflow upscale ảnh, tự động hóa AI ảnh, Google Drive Airtable, Real-ESRGAN tự động, nâng cấp chất lượng ảnh không code]
---

# 🚀 **Tự Động Hóa Upscale Ảnh Chân Dung với AI Real-ESRGAN, Google Drive & Airtable**

### **🔍 Nỗi Đau Của Các Sếp**
Làm việc với ảnh chân dung chất lượng thấp? Cần nâng cấp hình ảnh cho dự án marketing, blog cá nhân hay thương hiệu? Thời gian thủ công upscale từng ảnh bằng phần mềm như Photoshop hay AI online là vô cùng tốn kém, đặc biệt khi số lượng ảnh lớn. **Workflow này giải quyết vấn đề đó bằng cách tự động:**
- **Lấy ảnh từ Airtable** (không cần tải xuống thủ công).
- **Upscale chất lượng lên 4K** với AI Real-ESRGAN (không cần cài đặt phần mềm).
- **Lưu trữ tự động** lên Google Drive trong một thư mục riêng.
- **Hoạt động 24/7** mà không cần can thiệp của con người.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Upscale hàng trăm ảnh chỉ trong vài phút thay vì nhiều giờ.
- **Chất lượng chuyên nghiệp**: Ảnh được nâng cấp lên độ phân giải cao (4K) với độ nét và chi tiết tự nhiên.
- **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công, workflow chạy liên tục khi kích hoạt.
- **Dữ liệu sạch**: Ảnh được lưu trữ có hệ thống trên Google Drive, dễ dàng chia sẻ hoặc sử dụng lại.
- **Cá nhân hóa**: Thêm tên thư mục tùy chỉnh để phân loại dự án.
:::

---
### **🔧 Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản Airtable**:
   - Một bảng dữ liệu (base) chứa ảnh chân dung trong cột tên **`PortraitFotoAuswahl`** (định dạng URL hoặc file ảnh).
   - **Token API Airtable** (tạo tại [Airtable API Docs](https://airtable.com/api)).
2. **Tài khoản Google Drive**:
   - **OAuth 2.0 API Key** (cấu hình tại [Google Cloud Console](https://console.cloud.google.com/)).
3. **Tài khoản Replicate** (dịch vụ API upscale ảnh):
   - **API Key** từ [Replicate](https://replicate.com/) (đăng ký miễn phí).
4. **Tài khoản n8n Self-hosted** (không dùng phiên bản cloud):
   - Đăng ký VPS tại [TinoHost](https://tino.vn/vps-n8n?affid=388) (mã giảm giá: **VPSN8N**) hoặc [BNIX](https://my.bnix.one/aff.php?aff=172) (VPS Xeon 4GB chỉ 50k/tháng).
:::

---
## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/8047](https://n8n.io/workflows/8047) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ link trên và dán vào **Import Workflow** trong n8n.
- **Cách 3**: Sử dụng **n8n CLI** (nếu tự host):
  ```bash
  n8n import /path/to/workflow.json
  ```

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **9 node** quan trọng, các sếp cần cấu hình kỹ lưỡng như sau:

#### **🔹 Node 1: Manual Trigger (Kích Hoạt Bằng Tay)**
- **Lưu ý**: Node này chỉ dùng để test hoặc kích hoạt workflow một lần. Sau đó, các sếp có thể thay thế bằng **Webhook** hoặc **Schedule Trigger** để tự động chạy định kỳ.

#### **🔹 Node 2 & 5: Google Drive (Tạo Thư Mục & Upload Ảnh)**
- **Credentials**: Chọn `googleDriveOAuth2Api` (đã cấu hình trước khi import).
- **Node "Create folder"**:
  - **Folder Name**: Điền tên thư mục tùy chỉnh (ví dụ: `Upscaled_Portraits_2024`).
  - **Parent Folder ID**: Nếu muốn tạo thư mục con, điền ID của thư mục cha (tìm tại [Google Drive API](https://developers.google.com/drive/api/v3/reference/files)).
- **Node "Upload to Google Drive"**:
  - **File Path**: Sử dụng biến `{{$node["Loop Over Items"].json["fileUrl"]}}` (được lấy từ Airtable).
  - **Folder ID**: Sử dụng biến `{{$node["Create folder"].json["id"]}}` (ID của thư mục mới tạo).

#### **🔹 Node 3: Split In Batches (Chia Batch Ảnh)**
- **Batch Size**: Đặt số lượng ảnh xử lý cùng một lúc (ví dụ: **5 ảnh/lần**) để tránh quá tải API.
- **Lưu ý**: Nếu Airtable có nhiều ảnh, workflow sẽ tự động chia thành batch.

#### **🔹 Node 4 & 6: Replicate Upscaler (AI Real-ESRGAN)**
- **Credentials**: Chọn `httpHeaderAuth` (đã cấu hình API Key Replicate).
- **Node "Replicate Upscaler"**:
  - **URL**: `https://api.replicate.com/v1/predictions`
  - **Headers**:
    ```
    Authorization: Bearer {{ $credentials["httpHeaderAuth"]["apiKey"] }}
    Content-Type: application/json
    ```
  - **Body (JSON)**:
    ```json
    {
      "input": {
        "image": "{{ $node["Loop Over Items"].json["fileUrl"] }}",
        "scale": 4.0,
        "model": "real-esrgan:9f5664cff67197838f8a5c7e49f2e0a03fb56ab40aa4ddffc4a9076a7e9600e3"
      }
    }
    ```
  - **Lưu ý**:
    - Thay đổi `scale` (giá trị >1) để điều chỉnh độ phóng to (ví dụ: `2.0` cho 2x, `4.0` cho 4x).
    - Model `real-esrgan` là mô hình AI mặc định của Replicate.

#### **🔹 Node 7: Code (Lấy URL Ảnh Upscale)**
- **Script**:
  ```javascript
  // Lấy URL ảnh upscale từ response của Replicate
  return {
    json: {
      fileUrl: `https://cdn.replicate.delivery/${$node["Replicate Upscaler"].json["uuid"]}/out.png`
    }
  };
  ```
- **Lưu ý**: URL này sẽ được sử dụng để tải ảnh xuống Google Drive.

#### **🔹 Node 8: Airtable (Lấy Dữ Liệu Ảnh)**
- **Credentials**: Chọn `airtableTokenApi`.
- **Base ID & Table Name**: Điền ID của bảng Airtable và tên cột `PortraitFotoAuswahl`.
- **Filter**: Để trống hoặc thêm điều kiện lọc (ví dụ: chỉ lấy ảnh chưa được upscale).

#### **🔹 Node 9: Code (Set Folder ID Google Drive)**
- **Script**:
  ```javascript
  // Trả về ID của thư mục Google Drive để upload ảnh
  return {
    json: {
      folderId: "{{ $node["Create folder"].json["id"] }}"
    }
  };
  ```
- **Lưu ý**: Node này đảm bảo ảnh được upload vào thư mục đúng.

---
### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Chọn **Execute Workflow** và nhập một ảnh mẫu từ Airtable để kiểm tra.
   - Kiểm tra log để đảm bảo không có lỗi API hoặc cấu hình sai.
2. **Bật Active**:
   - Sau khi test thành công, chuyển workflow sang **Active** để tự động chạy khi kích hoạt.

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**
:::info[TIẾP CẬN HƠN]
1. **Tự Động Hóa Định Kỳ**:
   - Thay thế **Manual Trigger** bằng **Schedule Trigger** (cấu hình tại [n8n Docs](https://docs.n8n.io/integrations/builtins/triggers/schedule/)) để chạy workflow hàng ngày/tuần.
2. **Gửi Báo Cáo Slack/Email**:
   - Thêm node **Slack** hoặc **Email** sau khi upscale thành công để thông báo kết quả.
   - Ví dụ: `{{ $node["Upload to Google Drive"].json["fileName"] }} đã được upscale và lưu tại: {{ $node["Upload to Google Drive"].json["webContentLink"] }}`.
3. **Lưu Log Lịch Sử**:
   - Sử dụng node **Sticky Note** hoặc **Google Sheets** để ghi lại lịch sử upscale (ngày, ảnh, trạng thái).
4. **Tối Ưu API Replicate**:
   - Nếu gặp lỗi rate limit, giảm `Batch Size` hoặc sử dụng **Retry Logic** trong node `Replicate Upscaler`.
5. **Tự Động Xóa Ảnh Cũ**:
   - Thêm node **Google Drive Delete** sau khi upload ảnh mới để giữ gìn không gian.
:::

---
## **📌 Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp cần tự động hóa quá trình upscale ảnh chân dung với chất lượng cao, tiết kiệm thời gian và công sức. **Không cần code**, chỉ cần cấu hình API và import workflow là có thể sử dụng ngay.

👉 **Bắt đầu ngay!**
1. **Cài đặt n8n Self-hosted** trên VPS (đăng ký tại [TinoHost](https://tino.vn/vps-n8n?affid=388) với mã giảm giá **VPSN8N**).
2. **Import workflow** và cấu hình API theo hướng dẫn.
3. **Kích hoạt tự động hóa** và xem ảnh của mình được nâng cấp lên chất lượng 4K chỉ trong vài giây!

**Chia sẻ kết quả với chúng tôi bằng #n8nVietnam trên Twitter/X hoặc Facebook để được hỗ trợ thêm!** 🚀