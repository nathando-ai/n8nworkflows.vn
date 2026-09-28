---
title: "🤖 Tự Động Xử Lý Hình Ảnh: Phân Tách & Phát Hiện Đối Tượng + Chia Sẻ Trên Telegram & Google Drive"
description: "Workflow này tự động phân tích hình ảnh bằng AI VLM Run (phân đoạn và phát hiện đối tượng), tải xuống kết quả, và chia sẻ ngay lập tức đến Google Drive và Telegram - tiết kiệm thời gian cho các sếp lên tới 80% so với làm thủ công."
slug: "tu-dong-xu-ly-hinh-anh-phan-tach-phat-hien-doi-tuong"
tags: [n8n, automation, no-code, ai-multimodal, google-drive, telegram-bot, vlm-run]
keywords: [n8n workflow tự động hóa hình ảnh, phân đoạn ảnh AI, phát hiện đối tượng tự động, chia sẻ file Google Drive Telegram, tự động hóa no-code]
---

# 🚀 **Tự Động Xử Lý Hình Ảnh: Phân Tách & Phát Hiện Đối Tượng + Chia Sẻ Trên Telegram & Google Drive**

### **Giải pháp nào giúp các sếp:**
- **Tiết kiệm 80% thời gian** so với phân tích hình ảnh thủ công?
- **Tự động hóa toàn bộ quy trình** từ upload đến chia sẻ kết quả?
- **Nhận kết quả phân đoạn và phát hiện đối tượng** từ AI VLM Run chỉ trong vài giây?

Workflow này **không cần code**, kết hợp **AI Multimodal (VLM Run)** với **Google Drive** và **Telegram Bot** để tự động xử lý hình ảnh, phân tích, và chia sẻ kết quả đến nhiều kênh đồng thời. Dưới đây là hướng dẫn chi tiết để **cài đặt, cấu hình và vận hành** workflow này một cách hiệu quả.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng. N8n chạy trên VPS sẽ **không phụ thuộc vào internet công cộng**, đảm bảo **tốc độ và độ tin cậy cao**.

👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (Đảm bảo tốc độ xử lý nhanh cho AI)
:::

---

## 🎯 **Kết quả các sếp nhận được**
Workflow này **giải phóng thời gian** và **tăng hiệu suất** cho các sếp như sau:

:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tự động hóa toàn bộ quy trình** từ upload hình ảnh đến phân tích và chia sẻ kết quả.
✅ **Phân đoạn và phát hiện đối tượng** bằng AI VLM Run (không cần kỹ sư AI).
✅ **Chia sẻ kết quả ngay lập tức** đến **Google Drive** và **Telegram** (hoặc Slack, Email nếu mở rộng).
✅ **Không phụ thuộc vào internet công cộng** (self-hosted trên VPS).
✅ **Tiết kiệm chi phí** so với thuê dịch vụ AI chuyên dụng.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:

### **1. Tài khoản & API Keys**
| **Dịch vụ**          | **Thông tin cần thiết**                                                                 | **Lưu ý**                                                                 |
|-----------------------|------------------------------------------------------------------------------------------|---------------------------------------------------------------------------|
| **VLM Run**           | API Key từ [VLM Run](https://vlm.run/)                                                   | Đăng ký tài khoản và lấy API Key từ Dashboard.                          |
| **Google Drive**      | OAuth2 Credentials (Client ID & Secret)                                                 | Cấu hình **Google Drive API** và cấp quyền **Upload File**.              |
| **Telegram Bot**      | Bot Token + Chat ID (của nhóm hoặc cá nhân)                                             | Tạo bot trên [@BotFather](https://t.me/BotFather) và lấy Chat ID.         |
| **n8n Workflow**      | Credentials trong n8n (cấu hình trong **Credentials Manager**)                          | Thêm **3 credentials** mới: `vlmRunApi`, `googleDriveOAuth2Api`, `telegramApi`. |

### **2. Hệ thống**
- **VPS** (để self-host n8n) với **RAM ≥ 4GB** (khuyến nghị **Xeon** để xử lý AI nhanh).
- **n8n phiên bản mới nhất** (cập nhật từ [n8n.io](https://n8n.io/)).
- **Node VLM Run** (cài đặt từ [n8n-io/n8n-nodes-vlmrun](https://github.com/n8n-io/n8n-nodes-vlmrun)).

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/11246](https://n8n.io/workflows/11246) (chọn **Export as JSON**).
2. **Mở n8n Editor** → **Import Workflow** → Chọn file JSON vừa tải.
3. **Chọn "Import"** → Workflow sẽ được tạo với **9 nodes** như mô tả.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Copy toàn bộ JSON** từ [n8n.io/workflows/11246](https://n8n.io/workflows/11246) (chọn **Export as JSON**).
2. **Mở n8n Editor** → **Create New Workflow** → Chọn **Import from JSON**.
3. **Dán JSON** và chọn **Import**.

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **🔹 Cấu hình Credentials**
Trước khi kích hoạt workflow, các sếp **phải cấu hình 3 credentials** trong **Credentials Manager** của n8n:

| **Credentials**       | **Cách cấu hình**                                                                 |
|-----------------------|-----------------------------------------------------------------------------------|
| **`vlmRunApi`**      | - **Type:** `ApiKey` <br> - **Key:** `apiKey` <br> - **Value:** API Key từ VLM Run. |
| **`googleDriveOAuth2Api`** | - **Type:** `Google Drive OAuth2` <br> - **Client ID & Secret:** Từ Google Cloud Console. <br> - **Scopes:** `https://www.googleapis.com/auth/drive.file` (Upload File). |
| **`telegramApi`**    | - **Type:** `Telegram` <br> - **Token:** Bot Token từ @BotFather. <br> - **Chat ID:** ID của nhóm/người dùng (lấy bằng `/start` trong Telegram). |

#### **🔹 Cấu hình Node VLM Run**
- **Node "VLM Run (Segmentation)"** và **"VLM Run (Detection)"**:
  - **Credentials:** Chọn `vlmRunApi`.
  - **Operation:** `executeAgent` (đã mặc định).
  - **Payload:** Sử dụng **default payload** từ workflow (không cần chỉnh sửa nếu muốn sử dụng mô hình mặc định của VLM Run).

#### **🔹 Cấu hình Node Code (Trích xuất URL)**
- **Node "Code"** (là **Code Node** trong n8n):
  - **Script:** Sử dụng **regex** để trích xuất **signed URL đầy đủ** từ payload của VLM Run.
  - **Lưu ý:** Nếu API của VLM Run thay đổi, **cần cập nhật regex** để tránh lỗi download.
  - **Mẫu code tham khảo:**
    ```javascript
    // Trích xuất signed URL từ payload
    const url = $input.all()[0].json.output.url;
    const fullUrl = url.replace(/^https:\/\/storage\.googleapis\.com\//, 'https://storage.googleapis.com/');
    return { json: { url: fullUrl } };
    ```

#### **🔹 Cấu hình Node Download Image**
- **Node "Download Image"** (HTTP Request):
  - **Method:** `GET`.
  - **URL:** Được truyền từ **Code Node** (trích xuất từ signed URL).
  - **Headers:** Không cần thêm (n8n sẽ tự động xử lý).

#### **🔹 Cấu hình Webhook (Nếu cần gọi từ bên ngoài)**
- **Node "Webhook for Segmented Image"** và **"Webhook for Detected Image"**:
  - **Path:** `/image_segmentation` và `/image_detection`.
  - **HTTP Method:** `POST`.
  - **Lưu ý:** Nếu không cần gọi từ bên ngoài, **có thể bỏ qua** và chỉ sử dụng **Form Trigger**.

---

### **3. Kích hoạt ⚡️ Workflow**
1. **Test Run** với một hình ảnh mẫu:
   - Upload một hình ảnh bất kỳ qua **Form Trigger**.
   - Kiểm tra **log** của workflow để đảm bảo:
     - VLM Run xử lý thành công.
     - Signed URL được trích xuất đúng.
     - Hình ảnh được tải xuống và chia sẻ đến **Google Drive** và **Telegram**.
2. **Bật Active** workflow nếu test thành công.

---

## ✍️ **Mẹo & gợi ý nâng cao**

### **1. Mở rộng kênh chia sẻ kết quả**
- **Gửi Email** (thay vì Telegram):
  - Sử dụng **Node Gmail** để gửi kết quả qua Email.
  - Cấu hình **OAuth2** cho Gmail trong **Credentials Manager**.
- **Chia sẻ trên Slack**:
  - Sử dụng **Node Slack** để gửi thông báo và file kết quả.

### **2. Lưu log và báo cáo**
- **Node StickyNote** (đã có trong workflow):
  - Dùng để **ghi chú** hoặc **lưu log** cho mỗi lần xử lý.
  - Có thể mở rộng để **lưu vào Google Sheets** hoặc **Firebase**.
- **Báo cáo định kỳ**:
  - Sử dụng **Node Schedule** (n8n Pro) để **tự động chạy workflow hàng ngày** và gửi báo cáo.

### **3. Tối ưu hóa AI VLM Run**
- **Chọn mô hình phù hợp**:
  - Nếu hình ảnh phức tạp, thử **mô hình lớn hơn** (nếu VLM Run hỗ trợ).
  - Cấu hình **payload** trong VLM Run để **tăng độ chính xác** (ví dụ: `temperature`, `max_tokens`).
- **Cắt hình ảnh trước khi upload**:
  - Sử dụng **Node Image Processing** (n8n Pro) để **cắt vùng quan tâm** trước khi gửi đến VLM Run.

### **4. Bảo mật**
- **Khóa Webhook** (nếu không cần gọi từ bên ngoài):
  - Sử dụng **Node HTTP Request** với **Authentication** (API Key) để bảo mật.
- **Xóa file tạm thời**:
  - Sau khi chia sẻ, có thể **xóa file trong Google Drive** bằng **Node Google Drive (Delete File)**.

---

## 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp bằng cách **tự động hóa toàn bộ quy trình xử lý hình ảnh** từ upload đến phân tích và chia sẻ kết quả. Với **AI VLM Run**, **Google Drive** và **Telegram Bot**, các sếp có thể:
✔ **Phân đoạn và phát hiện đối tượng** chỉ trong vài giây.
✔ **Chia sẻ kết quả ngay lập tức** đến nhiều kênh.
✔ **Không phụ thuộc vào internet công cộng** (self-hosted).

**Hành động ngay hôm nay!**
1. **Cài đặt VPS** và **self-host n8n** (để workflow chạy 24/7).
2. **Import workflow** và **cấu hình credentials**.
3. **Test với hình ảnh mẫu** và **bật Active**.
4. **Mở rộng** bằng cách thêm **Email, Slack, hoặc báo cáo tự động**.

**🚀 [Tải workflow ngay](https://n8n.io/workflows/11246) và tự động hóa công việc của mình!**