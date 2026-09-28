---
title: "🎨 **Tự Động Hóa Dịch Vụ Khôi Phục Hình Ảnh Vintage Bằng AI Gemini + n8n (Miễn Code!)**"
description: "Workflow này tự động khôi phục, sửa chữa các hình ảnh cũ bị hư hại (nứt, xé, mất chi tiết) thành chất lượng mới bằng AI Gemini, sau đó lưu kết quả lên Google Drive. Giúp các sếp tiết kiệm thời gian và nâng cao chất lượng hình ảnh cho dự án, marketing, hoặc bảo tồn di sản."
slug: "tieu-dong-hoa-khoi-phuc-hinh-anh-ai-gemini-n8n"
tags: [n8n, automation, ai-gemini, image-editing, google-drive, no-code]
keywords: [tự động hóa hình ảnh bằng AI, khôi phục hình ảnh vintage, n8n workflow gemini, sửa chữa hình ảnh bằng AI, lưu hình ảnh lên Google Drive]
---

# 🚀 **Tự Động Hóa Dịch Vụ Khôi Phục Hình Ảnh Vintage Bằng AI Gemini + n8n**

### **Giới thiệu**
Có bao giờ các sếp phải mất nhiều giờ để sửa chữa, khôi phục hình ảnh cũ bị nứt, xé, hoặc mất chi tiết cho dự án? Hay khi làm việc với hình ảnh vintage cần phục hồi để marketing? **Workflow này giải quyết vấn đề đó 100% tự động hóa, chỉ cần 1 lần setup!**

Bằng công nghệ **AI Gemini** (Google) và nền tảng **n8n**, workflow sẽ:
✅ **Tải hình ảnh từ URL** (hoặc webhook) → **Khôi phục bằng AI** → **Lưu kết quả lên Google Drive** (hoặc bất kỳ nơi nào).
✅ **Giảm chi phí thời gian** từ hàng giờ/lần xuống **giây phút**.
✅ **Chất lượng chuyên nghiệp** như sử dụng Photoshop AI, nhưng **không cần kỹ năng code**.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy 24/7 ổn định, các sếp nên **self-host n8n** trên VPS. Dưới đây là 2 lựa chọn uy tín với **mã giảm giá độc quyền**:
👉 **[TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã: **VPSN8N** - giảm tới **39%** cho gói 4GB RAM)
👉 **[BNIX](https://my.bnix.one/aff.php?aff=172)** (VPS Xeon 4GB chỉ **50k/tháng**)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Khôi phục **30 hình ảnh chỉ trong 5 phút** thay vì 30 giờ làm thủ công.
- **Chất lượng cao**: AI Gemini tự động **xóa nứt, đắp lại vùng mất, cải thiện độ nét**.
- **Tích hợp hoàn hảo**: Hoạt động liên tục 24/7, không cần can thiệp.
- **Dễ dàng mở rộng**: Sử dụng **webhook** để tích hợp với Telegram, Slack, hoặc ứng dụng nội bộ.
- **Lưu trữ an toàn**: Kết quả tự động lưu lên **Google Drive** (hoặc Dropbox, AWS S3...).
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google** (để sử dụng **Gemini API** và **Google Drive OAuth**).
2. **API Key Gemini** (cần đăng ký tại [Google AI Studio](https://aistudio.google.com/)).
3. **Google Drive** (để lưu kết quả khôi phục).
4. **n8n Self-hosted** (cài đặt trên VPS hoặc máy chủ riêng).

---
### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n Workflow](https://n8n.io/workflows/4815) hoặc copy toàn bộ mã JSON dưới đây vào **n8n Editor**.
- **Cách import**:
  1. Mở **n8n Editor** → Nhấn **"Import"** → Chọn file JSON.
  2. **Hoặc** copy toàn bộ mã JSON vào ô **"Paste JSON"** và nhấn **"Import"**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **9 node** chính, các sếp cần cấu hình như sau:

| **Node**                     | **Lưu ý cấu hình**                                                                 | **Tham số cần điền**                          |
|------------------------------|-----------------------------------------------------------------------------------|-----------------------------------------------|
| **Manual Trigger**           | Khởi động workflow thủ công (hoặc thay bằng **Webhook** để tự động hóa).         | -                                             |
| **Set (Sample Images)**      | Thêm **URL hình ảnh** cần khôi phục (hoặc sử dụng **Webhook** để nhận từ bên ngoài). | `json: {"url": "https://example.com/image.jpg"}` |
| **Split Out**                | Chia nhỏ dữ liệu để xử lý từng hình ảnh riêng biệt.                              | -                                             |
| **HTTP Request (Download)**  | Tải hình ảnh từ URL xuống.                                                       | `Method: GET`, `URL: {{ $node["Sample Images"].json["url"] }}` |
| **Gemini Image Restoration** | **Cấu hình API Key** và **prompt** cho AI.                                        | - **Credentials**: Chọn `googlePalmApi` (đã cấu hình trước).<br>- **Prompt**: `"Restore this vintage photo to near-perfect condition. Remove all cracks, tears, and missing sections. Enhance details and colors."` |
| **Extract from File**        | Chuyển dữ liệu hình ảnh từ **base64** sang **binary** để AI xử lý.                 | `Operation: binaryToProperty`                 |
| **Set (Get Image Contents)** | Chuẩn bị dữ liệu cho bước khôi phục.                                             | -                                             |
| **Convert to File**          | Chuyển kết quả AI từ **base64** sang **binary** để lưu.                          | `Operation: toBinary`                         |
| **Google Drive**             | **Cấu hình OAuth2** và chọn **folder lưu kết quả**.                               | - **Credentials**: Chọn `googleDriveOAuth2Api`.<br>- **Folder ID**: ID thư mục Google Drive của bạn. |

##### **Cách cấu hình API Key Gemini**
1. Đăng ký **Google AI Studio** tại [đây](https://aistudio.google.com/).
2. Tạo **API Key** và thêm vào **n8n Credentials**:
   - Trong **n8n Editor** → Nhấn **"Credentials"** → **"Add"** → Chọn **"Google Palm API"**.
   - Điền **API Key** và tên credentials là `googlePalmApi`.

##### **Cách cấu hình Google Drive**
1. Tạo **OAuth2 Client ID** tại [Google Cloud Console](https://console.cloud.google.com/).
2. Trong **n8n Editor** → **"Credentials"** → **"Add"** → Chọn **"Google Drive OAuth2 API"**.
3. Điền **Client ID** và **Client Secret**, sau đó **authorize** với tài khoản Google.
4. Chọn **folder** muốn lưu kết quả trong node **Google Drive**.

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Nhấn **"Execute"** để chạy thử với **1 hình ảnh mẫu**.
   - Kiểm tra kết quả trong **Google Drive** (hoặc log trong n8n).
2. **Bật Active**:
   - Sau khi kiểm tra thành công, **bật "Active"** để workflow chạy tự động.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tích hợp Webhook** để nhận hình ảnh từ **Telegram, Slack, hoặc ứng dụng web**:
   - Thay **Manual Trigger** bằng **HTTP Request (Webhook)**.
   - Cấu hình **URL Webhook** trong Telegram/Slack và gửi hình ảnh qua đó.

2. **Lưu log hoạt động**:
   - Thêm **Slack/Email Notifications** để nhận thông báo khi workflow hoàn thành.

3. **Tối ưu hóa prompt**:
   - Thử các **prompt khác** để cải thiện kết quả:
     - `"Enhance this old photo with AI, remove all scratches and improve color saturation."`
     - `"Make this image look like it was taken in 2024, with modern lighting and sharpness."`

4. **Sử dụng nhiều hình ảnh cùng lúc**:
   - Thay vì **1 hình ảnh**, các sếp có thể **tải batch** từ Google Drive hoặc URL danh sách.

5. **Lưu kết quả lên Dropbox/AWS S3**:
   - Thay node **Google Drive** bằng **Dropbox** hoặc **AWS S3** tương tự.

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc **sửa chữa hình ảnh thủ công**, đồng thời **nâng cao chất lượng** với công nghệ AI tiên tiến. **Không cần code**, chỉ cần **1 lần setup** là có thể tự động hóa hoàn toàn!

👉 **Bắt đầu ngay**:
1. **Import workflow** từ [đây](https://n8n.io/workflows/4815).
2. **Cấu hình API Key** và **Google Drive**.
3. **Test Run** và **bật Active** để khôi phục hình ảnh tự động!

**Chia sẻ kết quả của các sếp với tôi qua [LinkedIn](https://www.linkedin.com/in/jimleuk/) để tôi có thể cải thiện workflow hơn!** 🚀

---
**⚠️ Lưu ý về phí Gemini**:
- Mỗi hình ảnh khôi phục **tốn ~$0.039 USD** (giá tại thời điểm viết bài). Các sếp nên **kiểm tra lại giá tại [Google AI Pricing](https://ai.google.dev/pricing)**.