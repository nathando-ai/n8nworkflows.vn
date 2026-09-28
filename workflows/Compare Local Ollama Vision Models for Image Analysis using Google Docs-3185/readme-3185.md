---
title: "🚀 So Sánh & Phân Tích Hình Ảnh Bằng Ollama Vision Models (Local) - Tự Động Hóa Trên Google Docs"
description: "Workflow tự động hóa 100% không code giúp các sếp phân tích hình ảnh chi tiết bằng các mô hình Ollama Vision Models (cài đặt local) và lưu kết quả vào Google Docs. Giúp tiết kiệm thời gian, tăng độ chính xác và hỗ trợ quyết định dựa trên dữ liệu."
slug: "so-sanh-phan-tich-hinh-anh-bang-ollama-vision-models"
tags: [n8n, automation, ai, ollama, google-docs, google-drive, no-code]
keywords: [n8n workflow ollama, phân tích hình ảnh AI, tự động hóa Google Docs, mô hình vision local, Ollama Vision Models, giải pháp AI không code]
---

# 🚀 **So Sánh & Phân Tích Hình Ảnh Bằng Ollama Vision Models (Local) - Tự Động Hóa Trên Google Docs**

### **🔍 Nỗi Đau Của Các Sếp Khi Phân Tích Hình Ảnh Thông Thường**
Các sếp thường phải:
- **Làm thủ công** phân tích hình ảnh (ví dụ: ảnh bất động sản, sản phẩm, hoặc tài liệu kỹ thuật) bằng cách copy-paste vào các công cụ AI cloud (mất thời gian và chi phí).
- **Không kiểm soát được dữ liệu** khi sử dụng các mô hình AI trên cloud, lo ngại về bảo mật và độ chính xác.
- **Không có cách nào để so sánh** hiệu suất của các mô hình vision khác nhau trên cùng một hình ảnh.
- **Không tích hợp được kết quả** vào workflow làm việc hiện tại (ví dụ: Google Docs, Slack, hoặc CRM).

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Sử dụng mô hình Ollama Vision Models (cài đặt local)** → Không phụ thuộc vào cloud, tiết kiệm chi phí và bảo mật dữ liệu.
✅ **So sánh kết quả phân tích** của nhiều mô hình khác nhau trên cùng một hình ảnh.
✅ **Lưu kết quả vào Google Docs** với định dạng markdown, dễ đọc và chia sẻ.
✅ **Tự động hóa toàn bộ quy trình** chỉ với một cú nhấp chuột.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần phân tích hình ảnh thủ công, chỉ cần upload ảnh và nhận kết quả chi tiết trong vài giây.
- **Độ chính xác cao**: Sử dụng mô hình Ollama Vision Models (cài đặt local) để phân tích chi tiết về đối tượng, văn bản, và bối cảnh trong ảnh.
- **So sánh mô hình**: Xem kết quả phân tích của nhiều mô hình khác nhau trên cùng một hình ảnh để chọn mô hình phù hợp nhất.
- **Tích hợp với Google Docs**: Kết quả được lưu dưới dạng markdown, dễ đọc và chia sẻ trong nhóm.
- **Bảo mật dữ liệu**: Không cần upload ảnh lên cloud, tất cả xử lý diễn ra trên máy chủ local của các sếp.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Môi trường Ollama local**:
   - Cài đặt [Ollama](https://ollama.com/) trên máy chủ hoặc VPS.
   - Pull các mô hình vision Ollama (ví dụ: `ollama pull granite3.2-vision`, `ollama pull llama3.2-vision`).
2. **Tài khoản Google**:
   - Tài khoản Google với quyền truy cập vào **Google Drive** và **Google Docs**.
   - **API Key** và **Credentials OAuth2** cho Google Drive và Google Docs trong n8n.
3. **Hình ảnh cần phân tích**:
   - Ảnh đã upload lên **Google Drive** và có **ID file** (có thể lấy từ liên kết chia sẻ).
4. **File JSON của workflow** (tải từ [n8n.io/workflows/3185](https://n8n.io/workflows/3185)).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow bằng cách:
- **Tải file JSON** từ [n8n.io/workflows/3185](https://n8n.io/workflows/3185) và import vào n8n Editor.
- **Copy/paste JSON** từ file vào n8n Editor (đảm bảo không có lỗi syntax).

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow gồm **13 node**, các sếp cần chú ý cấu hình các node sau:

##### **🔹 Node "Download Image File from Google Drive"**
- **Credentials**: Chọn `googleDriveOAuth2Api` (đã cấu hình trước trong n8n).
- **File ID**: Điền **ID file** của ảnh từ Google Drive (lấy từ liên kết chia sẻ, ví dụ: `1AbCdEfGhIjKlMnOpQrStUvWxYz`).
- **Operation**: Đảm bảo chọn `download`.

##### **🔹 Node "List of Vision Models"**
- **Danh sách mô hình**: Cập nhật danh sách mô hình Ollama Vision Models đã pull (ví dụ: `["granite3.2-vision", "llama3.2-vision"]`).
- **Format**: Danh sách phải là mảng JSON, mỗi phần tử là tên mô hình.

##### **🔹 Node "General Image Prompt" & "Real Estate Spreadsheet Prompt"**
- **Prompt**: Cập nhật nội dung prompt phù hợp với mục đích phân tích (ví dụ:
  ```json
  {
    "prompt": "Analyze this image in detail. Describe objects, text, and spatial relationships. Output in markdown format."
  }
  ```
  Hoặc cho mục đích bất động sản:
  ```json
  {
    "prompt": "Describe the real estate property in this image. Note key features, room layout, and potential improvements."
  }
  ```

##### **🔹 Node "Save Image Descriptions to Google Docs"**
- **Credentials**: Chọn `googleDocsOAuth2Api`.
- **File Google Docs**: Điền **ID file Google Docs** muốn lưu kết quả (tạo trước trong Google Docs).
- **Operation**: Chọn `update` để thêm nội dung mới vào file.

##### **🔹 Node "Manual Trigger"**
- **Test Run**: Nhấn nút **"Test workflow"** để chạy thử với dữ liệu mẫu.

#### **3. Kích Hoạt ⚡️**
- Sau khi cấu hình xong, **bật Active workflow**.
- Kết quả phân tích sẽ tự động lưu vào Google Docs với định dạng markdown.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tích Hợp với Slack/Telegram**:
   - Thêm node **Slack/Telegram** để thông báo kết quả phân tích ngay khi hoàn thành.
   - Ví dụ: Sau khi lưu vào Google Docs, gửi link file qua Slack với thông báo:
     ```json
     {
       "text": "📊 Kết quả phân tích hình ảnh đã hoàn thành! Xem tại: [Link Google Docs]"
     }
     ```

2. **Lưu Log & Theo Dõi Lịch Sử**:
   - Thêm node **Sticky Note** để lưu log phân tích (tên mô hình, thời gian chạy, kết quả).
   - Ví dụ:
     ```json
     {
       "note": {
         "model": "{{$node["Loop Over Ollama Models"].json["model"]}}",
         "timestamp": "{{$node["Loop Over Ollama Models"].json["timestamp"]}}",
         "result": "{{$node["Save Image Descriptions to Google Docs"].json}}"
       }
     }
     ```

3. **Tự Động Hoá Định Kỳ**:
   - Sử dụng **n8n Trigger** (ví dụ: **HTTP Request** hoặc **Schedule Node**) để chạy workflow định kỳ (ví dụ: hàng tuần phân tích ảnh mới).
   - Ví dụ:
     ```json
     {
       "cron": "0 0 * * 1", // Chạy vào thứ Hai hàng tuần
       "httpMethod": "GET",
       "url": "https://your-n8n-instance.com/webhook/trigger-image-analysis"
     }
     ```

4. **So Sánh Kết Quả Giữa Mô Hình**:
   - Thêm node **Set** để so sánh độ chính xác của các mô hình (ví dụ: đếm từ khóa xuất hiện trong kết quả).
   - Ví dụ:
     ```json
     {
       "json": {
         "model_performance": {
           "granite3.2-vision": "{{$node["Loop Over Ollama Models"].json["granite3.2-vision"].length}}",
           "llama3.2-vision": "{{$node["Loop Over Ollama Models"].json["llama3.2-vision"].length}}"
         }
       }
     }
     ```

---

### 📌 **Kết Luận**
Workflow **"So Sánh & Phân Tích Hình Ảnh Bằng Ollama Vision Models"** là giải pháp **tự động hóa AI không code** hoàn hảo cho các sếp muốn:
✔ **Phân tích hình ảnh chi tiết** mà không phụ thuộc vào cloud.
✔ **So sánh hiệu suất** của nhiều mô hình vision khác nhau.
✔ **Lưu kết quả vào Google Docs** với định dạng dễ đọc.
✔ **Tiết kiệm thời gian và chi phí** so với cách làm thủ công.

**Hành động ngay hôm nay!**
1. Cài đặt **Ollama** và pull mô hình vision.
2. Import workflow vào n8n và cấu hình các node quan trọng.
3. Upload ảnh vào Google Drive và chạy thử!

**Nếu các sếp cần hỗ trợ thêm**, hãy liên hệ với [n8n Community](https://community.n8n.io/) hoặc chia sẻ phản hồi trong [forum](https://forum.n8n.io/). Chúc các sếp thành công! 🚀