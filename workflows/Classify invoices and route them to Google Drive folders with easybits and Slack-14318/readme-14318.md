---
title: "📄 **Tự Động Hóa Xác Định & Phân Loại Hóa Đơn Với AI + Google Drive + Slack (Không Cần Code!)**"
description: "Workflow n8n tự động phân loại hóa đơn (PDF/PNG/JPEG) thành 6 loại: Y tế, Nhà hàng, Khách sạn, Thương mại, Di động, và 'Cần xem xét' với độ chính xác >90%. Hóa đơn được tự động lưu vào Google Drive theo danh mục và gửi thông báo Slack cho đội ngũ review khi cần thiết."
slug: "tieu-dong-hoa-phan-loai-hoa-don-voi-ai-google-drive-slack"
tags: [n8n, automation, invoice processing, AI classification, Google Drive, Slack integration, easybits, no-code]
keywords: [tự động hóa hóa đơn, phân loại hóa đơn bằng AI, n8n workflow, lưu hóa đơn vào Google Drive, Slack alert hóa đơn, easybits API, tự động hóa văn phòng]
---

# 🚀 **Tự Động Hóa Xác Định & Phân Loại Hóa Đơn Với AI + Google Drive + Slack**

### **Giải pháp cho những sếp mệt mỏi với việc phân loại hóa đơn thủ công**
Hàng ngày, đội ngũ tài chính của các sếp phải mất **30-60 phút** để phân loại hàng trăm hóa đơn vào các danh mục khác nhau (Y tế, Nhà hàng, Khách sạn, Thương mại, Di động...). Với **workflow này**, các sếp sẽ:
✅ **Tiết kiệm 80% thời gian** phân loại hóa đơn.
✅ **Giảm sai sót** nhờ AI phân loại với độ chính xác >90%.
✅ **Tự động lưu hóa đơn** vào Google Drive theo danh mục.
✅ **Nhận thông báo Slack** khi hóa đơn cần được review thủ công.
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **ổn định 24/7**, các sếp nên cài đặt n8n trên **VPS riêng** (Self-hosted) để tránh giới hạn của phiên bản miễn phí.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (Đảm bảo tốc độ xử lý nhanh cho AI)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Phân loại **500 hóa đơn/ngày** chỉ trong vài giây thay vì 3-4 giờ.
- **Chính xác cao**: AI phân loại với độ tin cậy **>90%** (cài đặt ngưỡng confidence từ 0.5 trở lên).
- **Tự động hóa lưu trữ**: Hóa đơn tự động được lưu vào **Google Drive** theo danh mục (Y tế, Nhà hàng, Khách sạn...).
- **Review dễ dàng**: Hóa đơn **không phân loại được** hoặc **confidence thấp** sẽ được gửi vào **folder "Cần xem xét"** và thông báo trên **Slack**.
- **Hoạt động liên tục**: Workflow chạy **24/7** mà không cần can thiệp của con người.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản easybits** (dùng để phân loại hóa đơn bằng AI):
   - [Đăng ký easybits](https://extractor.easybits.tech/) (miễn phí cho 1.000 request/tháng).
   - **Pipeline ID** và **API Key** (cách tạo ở phần **Cách import & Lưu ý khi "lên đồ"**).
2. **Tài khoản Google Drive**:
   - **Google Cloud Console** để tạo **OAuth 2.0 Client ID** và **Client Secret**.
   - **Google Drive API** được kích hoạt.
3. **Tài khoản Slack**:
   - **Slack App** với quyền `chat:write` (để gửi thông báo).
   - **Channel** dành riêng cho review (ví dụ: `#n8n-invoice-review`).
4. **VPS n8n** (nếu tự host):
   - [TinoHost](https://tino.vn/vps-n8n?affid=388) (giảm 39% với mã **VPSN8N**).
   - [BNIX](https://my.bnix.one/aff.php?aff=172) (VPS Xeon 4GB chỉ 50k/tháng).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/14318](https://n8n.io/workflows/14318) và import vào n8n Editor.
- **Copy/paste JSON** từ file vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
##### **A. Cấu hình easybits (AI phân loại)**
1. **Tạo Pipeline trên easybits**:
   - Truy cập [extractor.easybits.tech](https://extractor.easybits.tech/) và tạo **mới Pipeline**.
   - Thêm **2 field**:
     - **`document_class`** (dùng để phân loại hóa đơn):
       ```json
       {
         "prompt": "Phân loại hóa đơn này là loại nào? Chỉ trả về một trong các giá trị: 'medical_invoice', 'restaurant_invoice', 'hotel_invoice', 'trades_invoice', 'telecom_invoice', hoặc 'null' nếu không xác định được."
       }
       ```
     - **`confidence_score`** (độ tin cậy của phân loại):
       ```json
       {
         "prompt": "Trả về một số thập phân từ 0.0 đến 1.0 biểu thị độ tin cậy của phân loại trên."
       }
       ```
   - **Lưu Pipeline** và sao chép **Pipeline ID**.

2. **Cấu hình Node `easybits Extractor (Classification)`**:
   - Mở node này trong workflow.
   - Thay đổi URL thành:
     ```
     https://extractor.easybits.tech/api/pipelines/YOUR_PIPELINE_ID
     ```
   - Tạo **Bearer Auth** trong **Credentials** của n8n:
     - **Name**: `easybits-api-key`
     - **Type**: `Bearer Token`
     - **Token**: `YOUR_EASYBITS_API_KEY`
   - Gán **Bearer Auth** cho node `easybits Extractor`.

##### **B. Cấu hình Google Drive**
1. **Tạo 6 folder trong Google Drive**:
   - `Medical` (Y tế)
   - `Restaurant` (Nhà hàng)
   - `Hotel` (Khách sạn)
   - `Trades` (Thương mại)
   - `Telecom` (Di động)
   - `Needs Review` (Cần xem xét)

2. **Cấu hình OAuth 2.0 cho Google Drive**:
   - Truy cập [Google Cloud Console](https://console.cloud.google.com/).
   - Tạo **OAuth 2.0 Client ID** (dùng cho **External app**).
   - Sao chép **Client ID** và **Client Secret**.
   - Trong n8n, đi đến **Settings → Credentials** và tạo:
     - **Name**: `google-drive-oauth`
     - **Type**: `Google Drive OAuth2`
     - Điền **Client ID** và **Client Secret**.
   - Mở từng node **`Upload to [Folder] Name`** (ví dụ: `Upload to Medical Folder`) và chọn **folder tương ứng**.

##### **C. Cấu hình Slack**
1. **Tạo Slack Bot**:
   - Truy cập [api.slack.com/apps](https://api.slack.com/apps) và tạo **mới App**.
   - Chọn **OAuth & Permissions** → Thêm **scope**: `chat:write`.
   - Tạo **Bot Token** và sao chép.
   - Trong n8n, đi đến **Settings → Credentials** và tạo:
     - **Name**: `slack-bot-token`
     - **Type**: `Slack`
     - Điền **Bot Token**.
   - Mở node **`Review Message`** và chọn **channel** muốn gửi thông báo (ví dụ: `#n8n-invoice-review`).

##### **D. Cấu hình Form Upload**
- Node **`On form submission`** đã sẵn sàng chấp nhận **PDF, PNG, JPEG**.
- Các sếp có thể **cập nhật URL form** trong node này nếu muốn thay đổi đường dẫn.

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Upload một **hóa đơn mẫu** (PDF/PNG/JPEG) vào form.
   - Kiểm tra **Execution Log** để xác nhận:
     - Hóa đơn được phân loại thành loại nào (`document_type`).
     - **Confidence score** > 0.5 (nếu không, hóa đơn sẽ vào folder "Cần xem xét").
     - Hóa đơn được lưu vào **Google Drive** đúng folder.
     - Nếu confidence ≤ 0.5, **Slack sẽ gửi thông báo**.

2. **Bật Workflow**:
   - Nhấn **Active** ở góc trên bên phải của n8n Editor.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tự động gửi báo cáo hàng tháng**:
   - Thêm node **Google Sheets** để lưu lịch sử phân loại vào một bảng tính.
   - Sử dụng node **Slack** để gửi **báo cáo tổng hợp** vào cuối tháng.

2. **Kết hợp với Zoom/Teams**:
   - Thêm node **Zoom API** để tự động tạo **gặp mặt** với người review khi hóa đơn cần kiểm tra.

3. **Lưu log hoạt động**:
   - Thêm node **Google Drive (Log)** để lưu **tất cả lịch sử phân loại** vào một folder riêng.

4. **Cập nhật danh mục mới**:
   - Nếu có loại hóa đơn mới (ví dụ: `transport_invoice`), chỉ cần:
     - Thêm **category** vào easybits Pipeline.
     - Tạo **folder mới** trong Google Drive.
     - Cập nhật node **`Category Router`** để thêm điều kiện mới.

5. **Tự động xóa hóa đơn cũ**:
   - Thêm node **Google Drive (Delete)** để xóa hóa đơn đã quá hạn (ví dụ: >6 tháng).

---

### 📌 **Kết luận**
**Workflow này giải quyết hoàn toàn vấn đề phân loại hóa đơn thủ công**, giúp các sếp:
✔ **Tiết kiệm thời gian** (từ 3-4 giờ/tháng xuống còn vài phút).
✔ **Giảm sai sót** nhờ AI phân loại tự động.
✔ **Hoạt động 24/7** mà không cần can thiệp.
✔ **Tự động hóa lưu trữ** và **review** hóa đơn.

**Hãy áp dụng ngay workflow này và tự động hóa bộ phận tài chính của mình!**
👉 [Tải workflow từ n8n.io](https://n8n.io/workflows/14318)
👉 [Cài đặt VPS n8n với mã giảm giá](https://tino.vn/vps-n8n?affid=388) (VPSN8N -39%)