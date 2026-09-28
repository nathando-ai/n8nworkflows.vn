---
title: "🎨 **Tự Động Xóa Nền Hình Ảnh Trên Google Drive Với AI - Không Cần Code!**"
description: "Workflow tự động hóa xóa nền, thêm padding và tùy chỉnh kích thước cho tất cả hình ảnh mới được upload lên Google Drive. Giúp các sếp tiết kiệm thời gian và nâng cao chất lượng hình ảnh sản phẩm, banner marketing chỉ trong vài giây."
slug: "tu-dong-xoa-nen-hinh-anh-google-drive-ai"
tags: [n8n, automation, ai, google-drive, e-commerce, design]
keywords: [tự động hóa xóa nền hình ảnh, n8n workflow google drive, AI xóa nền tự động, tự động hóa marketing, tự động hóa e-commerce]
---

# 🚀 **Tự Động Xóa Nền Hình Ảnh Trên Google Drive Với AI - Không Cần Code!**

Hãy tưởng tượng một tình huống: Các sếp đang bán hàng trên Shopify, Lazada hay Facebook Shop, nhưng phải mất **giờ đồng hồ** để xóa nền cho hàng trăm hình ảnh sản phẩm thủ công? Hoặc khi cần chuẩn bị banner quảng cáo, phải mất công chỉnh sửa từng ảnh một? **Workflow này sẽ giải quyết tất cả những vấn đề đó!**

Với **Automatic Background Removal for Images in Google Drive**, các sếp có thể **tự động hóa toàn bộ quy trình** từ khi hình ảnh mới được upload lên Google Drive đến khi nhận được hình ảnh đã xóa nền, thêm padding và tùy chỉnh kích thước. **Không cần viết một dòng code nào!** Dùng AI của Photoroom kết hợp với n8n, workflow này sẽ hoạt động **24/7**, tiết kiệm thời gian và nâng cao chất lượng hình ảnh cho mọi dự án marketing, e-commerce hay thiết kế.

---
### 🎯 **Kết quả các sếp nhận được**
:::tip[**LỢI ÍCH CỐT LÕI**]
✅ **Tiết kiệm thời gian**: Xóa nền cho hàng trăm hình ảnh chỉ trong vài giây thay vì mất giờ.
✅ **Chất lượng chuyên nghiệp**: Hình ảnh có nền trong suốt hoặc nền màu đồng nhất, phù hợp với mọi nền tảng (Shopify, Instagram, banner quảng cáo).
✅ **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công, workflow chạy liên tục khi có hình ảnh mới.
✅ **Tùy chỉnh linh hoạt**: Chọn kích thước output, màu nền, và padding theo yêu cầu.
✅ **Nâng cao hiệu suất marketing**: Hình ảnh sản phẩm chuyên nghiệp giúp tăng tỷ lệ chuyển đổi và engagement.
:::

---
### 🔧 **Yêu cầu cần thiết**
:::info[**CHUẨN BỊ**]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Drive** và **OAuth 2.0 API Key** đã được cấu hình trong n8n.
   - Hướng dẫn cài đặt: [Google Drive OAuth 2.0](https://developers.google.com/drive/api/v3/quickstart/python)
2. **API Key của Photoroom** (dùng để xóa nền hình ảnh).
   - Mua API Key tại: [Photoroom API](https://www.photoroom.com/api/playground)
   - **Mã giảm giá 10% cho các sếp**: **N8NAI10** (áp dụng khi đăng ký tại [đây](https://www.photoroom.com/api/pricing))
3. **Folder Google Drive** để lưu trữ hình ảnh đầu vào và output.
   - **Lưu ý**: Folder đầu vào phải được **chia sẻ** với tài khoản OAuth 2.0 của n8n.
4. **Tham số tùy chỉnh** (cần điền trong node **Config**):
   - **Background Color** (HEX hoặc tên màu như `white`, `transparent`).
   - **Output Size**: Chọn giữa **Original Size** hoặc **Fixed Size** (ví dụ: `1000x1000`).
   - **Padding**: Thiết lập phần padding mặc định (ví dụ: `5%`).
   - **Folder Output**: URL của folder Google Drive để lưu hình ảnh đã xử lý.
:::

---
### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. **Tải file JSON** từ [đây](https://n8n.io/workflows/2529) (hoặc sao chép từ link trên).
2. Trong **n8n Editor**, nhấn **Import** và chọn file JSON.
   - **Hoặc**:
     - Mở **n8n Editor** → **Create Workflow** → **Import from JSON** → Dán JSON từ file.
3. Sau khi import, workflow sẽ hiển thị **12 node** như trong danh sách dưới đây.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này bao gồm **12 node chính**, mỗi node có vai trò quan trọng. Dưới đây là hướng dẫn chi tiết để cấu hình:

##### **A. Cấu hình Node "Config" (Set)**
- **Vai trò**: Lưu trữ các tham số tùy chỉnh như màu nền, kích thước output, padding, và folder output.
- **Cách thiết lập**:
  - Nhấn **double-click** vào node **Config**.
  - Điền các giá trị sau:
    ```json
    {
      "backgroundColor": "#FFFFFF", // Màu nền (HEX hoặc "transparent")
      "outputSize": "fixed", // "original" hoặc "fixed"
      "fixedSize": "1000x1000", // Kích thước cố định (nếu chọn "fixed")
      "padding": 5, // Padding (%) mặc định
      "outputFolderUrl": "https://drive.google.com/drive/folders/1ABCDEFGHIJKLMNOPQRSTUVWXYZ" // URL folder output
    }
    ```
  - **Lưu ý**: URL folder output phải là **folder Google Drive** đã được chia sẻ với tài khoản OAuth 2.0 của n8n.

##### **B. Cấu hình Node "Watch for new images" (Google Drive Trigger)**
- **Vai trò**: Theo dõi folder Google Drive và kích hoạt workflow khi có hình ảnh mới được upload.
- **Cách thiết lập**:
  - Nhấn **double-click** vào node này.
  - Chọn **Credentials**: `googleDriveOAuth2Api` (đã cấu hình trước).
  - Trong **Folder ID**, điền **ID của folder đầu vào** (có thể lấy từ URL folder, ví dụ: `1ABCDEFGHIJKLMNOPQRSTUVWXYZ` trong `https://drive.google.com/drive/folders/1ABCDEFGHIJKLMNOPQRSTUVWXYZ`).
  - Chọn **File Types**: `Images` (để chỉ theo dõi hình ảnh).
  - **Lưu ý**: Folder này **không thể là folder root** của Google Drive.

##### **C. Cấu hình Node "remove background" và "remove background fixed size" (HTTP Request)**
- **Vai trò**: Gửi yêu cầu API đến Photoroom để xóa nền hình ảnh.
- **Cách thiết lập**:
  - Trong cả hai node này, cần thiết lập **Header Authentication** với API Key của Photoroom.
  - Nhấn **double-click** vào node → **Headers** → Thêm:
    ```json
    {
      "Authorization": "Bearer YOUR_PHOTOROOM_API_KEY"
    }
    ```
    (Thay `YOUR_PHOTOROOM_API_KEY` bằng API Key đã mua).
  - **Lưu ý**:
    - Node **remove background** dùng cho hình ảnh **kích thước gốc**.
    - Node **remove background fixed size** dùng cho hình ảnh **đã resize** (nếu chọn `outputSize: fixed`).

##### **D. Cấu hình Node "Upload Picture to Google Drive" và "Upload Picture to Google Drive1"**
- **Vai trò**: Upload hình ảnh đã xử lý (xóa nền) về Google Drive.
- **Cách thiết lập**:
  - Chọn **Credentials**: `googleDriveOAuth2Api`.
  - Trong **Folder ID**, điền **ID của folder output** (lấy từ `outputFolderUrl` trong node Config).
  - **Lưu ý**: Folder này phải **khác với folder đầu vào** để tránh lặp lại.

##### **E. Cấu hình Node "check which output size method is used" (If)**
- **Vai trò**: Xác định hình ảnh sẽ được xử lý theo kích thước gốc hay kích thước cố định.
- **Cách thiết lập**:
  - Node này **không cần chỉnh sửa** vì logic đã được viết sẵn trong workflow.

##### **F. Cấu hình Node "loop all over your images" (Split In Batches)**
- **Vai trò**: Xử lý hình ảnh theo batch để tránh quá tải API.
- **Cách thiết lập**:
  - Thiết lập **Batch Size**: `1` (mặc định) hoặc tăng lên nếu có nhiều hình ảnh.
  - **Lưu ý**: Nếu batch size quá lớn, có thể gặp lỗi API. Mặc định `1` là an toàn.

---
#### **3. Kích hoạt ⚡️ Workflow**
1. **Test Run** với một hình ảnh mẫu:
   - Upload một hình ảnh test vào folder đầu vào.
   - Chạy workflow và kiểm tra kết quả trong folder output.
2. **Bật Active**:
   - Sau khi kiểm tra thành công, nhấn **Active** để workflow chạy tự động khi có hình ảnh mới.

---
### ✍️ **Mẹo & gợi ý nâng cao**
:::tip[**CÁC Ý TƯỞNG MỞ RỘNG**]
1. **Gửi hình ảnh đã xử lý đến Slack/Telegram**:
   - Sử dụng node **Slack** hoặc **Telegram Bot** để thông báo khi hình ảnh đã xử lý xong.
   - Ví dụ: "📸 Hình ảnh [Tên file] đã xóa nền thành công! Kết quả tại: [Link Google Drive]".

2. **Tích hợp với Shopify/Lazada**:
   - Sau khi xóa nền, tự động upload hình ảnh lên **Shopify Product Media** hoặc **Lazada Product Images** bằng node **Shopify API** hoặc **Lazada API**.

3. **Phân tích hình ảnh với AI (ChatGPT)**:
   - Sử dụng node **LLM (ChatGPT)** để phân tích mô tả sản phẩm từ hình ảnh (ví dụ: "Đây là một chiếc ổ bi kích thước 608").
   - Cần thêm node **LLM** và cấu hình prompt:
     ```json
     {
       "prompt": "Describe the product in this image in detail. Focus on color, size, and material."
     }
     ```

4. **Lưu log hoạt động**:
   - Sử dụng node **Google Sheets** hoặc **Airtable** để ghi lại lịch sử xử lý hình ảnh (ngày upload, tên file, trạng thái).

5. **Tùy chỉnh padding động**:
   - Thay vì sử dụng padding cố định, có thể tính toán padding dựa trên kích thước hình ảnh bằng node **Set** và công thức:
     ```json
     {
       "padding": "{{ $node["Get Image Size"].json["width"] * 0.05 }}"
     }
     ```

6. **Chuyển đổi định dạng file**:
   - Thêm node **Edit Image** để chuyển đổi hình ảnh từ PNG sang JPG (nếu cần) trước khi upload.
:::

---
### 📌 **Kết luận**
Workflow **Automatic Background Removal for Images in Google Drive** là **giải pháp hoàn hảo** cho các sếp bán hàng online, marketer hoặc nhà thiết kế muốn **tự động hóa quy trình xử lý hình ảnh** mà không cần viết code. Với **AI xóa nền Photoroom** và **tự động hóa n8n**, các sếp có thể:
✔ **Tiết kiệm hàng giờ** mỗi tuần cho việc chỉnh sửa hình ảnh thủ công.
✔ **Nâng cao chất lượng hình ảnh** cho sản phẩm, banner và marketing.
✔ **Hoạt động 24/7** mà không cần can thiệp.

**Hành động ngay hôm nay!**
1. **Cài đặt n8n Self-hosted** trên VPS để workflow chạy ổn định:
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
2. **Import workflow** và cấu hình theo hướng dẫn trên.
3. **Upload hình ảnh đầu tiên** vào Google Drive và xem kết quả thần tốc!

**Chia sẻ workflow này với đồng nghiệp của các sếp để cùng tự động hóa công việc!** 🚀