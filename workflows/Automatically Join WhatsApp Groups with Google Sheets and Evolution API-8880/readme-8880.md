---
title: "🚀 Tự Động Tham Gia Nhóm WhatsApp Từ Google Sheets Với Evolution API (Không Cần Code)"
description: "Workflow tự động hóa hoàn toàn giúp các sếp tự động tham gia nhóm WhatsApp từ danh sách mã mời trong Google Sheets, theo dõi kết quả và quản lý hiệu quả - tiết kiệm thời gian lên đến 80% so với thủ công."
slug: "tu-dong-tham-gia-nhom-whatsapp-google-sheets"
tags: [n8n, automation, whatsapp, google-sheets, evolution-api, no-code, ai-multimodal]
keywords: [tự động hóa whatsapp, n8n workflow whatsapp, tự động tham gia nhóm whatsapp, google sheets automation, evolution api n8n]
---

# 🚀 **Tự Động Tham Gia Nhóm WhatsApp Từ Google Sheets Với Evolution API**

### **Giải pháp hoàn toàn tự động hóa cho các sếp quản lý nhiều nhóm WhatsApp**
Hãy tưởng tượng một tình huống: Các sếp phải thủ công copy mã mời từ Google Sheets, mở WhatsApp, tìm kiếm nhóm và tham gia một cách mệt mỏi. **Workflow này sẽ tự động hóa toàn bộ quá trình đó!** Bằng cách kết nối Google Sheets với Evolution API (trên nền tảng n8n self-hosted), các sếp có thể:
- **Tự động tham gia nhóm WhatsApp** từ danh sách mã mời trong Google Sheets.
- **Theo dõi trạng thái** (thành công/thất bại) và **cập nhật tự động** vào bảng tính.
- **Lọc và xử lý** tối đa 50 mã mời chưa xử lý mỗi lần chạy.
- **Hoạt động 24/7** mà không cần can thiệp thủ công.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động ổn định và không bị giới hạn API, các sếp nên **self-host n8n** trên VPS riêng:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần thủ công copy-paste mã mời, giảm thời gian lên đến **80%**.
- **Chính xác 100%**: Không sai sót trong quá trình tham gia nhóm.
- **Theo dõi dễ dàng**: Tất cả kết quả (thành công/thất bại) được ghi lại trong Google Sheets.
- **Hoạt động liên tục**: Dùng **Schedule Trigger** để chạy tự động hàng ngày/hàng giờ.
- **Không giới hạn số lượng**: Xử lý tối đa **50 mã mời chưa xử lý** mỗi lần chạy.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản n8n self-hosted** (không dùng n8n.cloud vì Evolution API chỉ hỗ trợ self-hosted).
2. **Google Sheets** với:
   - **Cột mã mời (invitation code)**.
   - **Cột trạng thái (status)** để ghi kết quả (chưa xử lý, thành công, thất bại).
   - **Bảng theo dõi kết quả** (nếu muốn lưu danh sách nhóm đã tham gia).
3. **API Key Evolution API**:
   - [Tải Evolution API](https://github.com/adi1090x/evolution) và **self-host** trên máy chủ.
   - Cấu hình **credentials** trong n8n với tên `evolutionApi`.
4. **Google Sheets OAuth2 API Key**:
   - Tạo trong [Google Cloud Console](https://console.cloud.google.com/) và cấu hình trong n8n với tên `googleSheetsOAuth2Api`.

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/8880](https://n8n.io/workflows/8880) và import vào n8n Editor.
- **Copy JSON** từ link trên và dán vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này có **13 node** quan trọng, các sếp cần chú ý cấu hình như sau:

##### **A. Schedule Trigger (Đặt lịch chạy)**
- **Cấu hình**:
  - Chọn **frequency** (ví dụ: **daily at 8 AM**).
  - Đặt **timezone** phù hợp với khu vực của các sếp.
- **Lưu ý**:
  - Nếu muốn chạy **ngay lập tức**, các sếp có thể **bỏ qua node này** và kích hoạt bằng **Webhook** (node `n8n-nodes-base.http`).

##### **B. Lire invitation code (Đọc mã mời từ Google Sheets)**
- **Cấu hình**:
  - Chọn **Google Sheets OAuth2 credentials** (`googleSheetsOAuth2Api`).
  - Chọn **Sheet Name** và **Range** (ví dụ: `Sheet1!A2:B100`).
  - **Column to read**: Chọn cột chứa **mã mời** (ví dụ: `A`).
  - **Column to update status**: Chọn cột **trạng thái** (ví dụ: `B`).
- **Lưu ý**:
  - Đảm bảo **cột trạng thái** có giá trị mặc định là **"Chưa xử lý"** (`"pending"`).

##### **C. 50 premiers non traités (Lọc 50 mã mời chưa xử lý)**
- **Cấu hình**:
  - Node này **lọc** các mã mời có trạng thái = `"pending"`.
  - **Bật "Limit to 50 items"** để xử lý tối đa 50 mã mỗi lần.
- **Lưu ý**:
  - Nếu muốn xử lý nhiều hơn 50 mã, các sếp cần **cập nhật số lượng** trong node `splitInBatches`.

##### **D. Fetch groups (Lấy thông tin nhóm)**
- **Cấu hình**:
  - Chọn **credentials** `evolutionApi`.
  - **Operation**: `fetch-groups`.
  - **Input**: Chọn **output từ node "Lire invitation code"**.
- **Lưu ý**:
  - Node này **kiểm tra tính hợp lệ** của mã mời và **lấy thông tin nhóm** trước khi tham gia.

##### **E. Join group (Tham gia nhóm)**
- **Cấu hình**:
  - Chọn **credentials** `evolutionApi`.
  - **Operation**: `join-group`.
  - **Input**: Chọn **output từ node "Fetch groups"**.
- **Lưu ý**:
  - Nếu **thất bại**, Evolution API sẽ trả về lỗi, và workflow sẽ **cập nhật trạng thái thành "Thất bại"** (`"failed"`).

##### **F. Cập nhật trạng thái (Mis a jour statut)**
- **Cấu hình**:
  - Chọn **Google Sheets OAuth2 credentials**.
  - **Operation**: `update`.
  - **Input**: Chọn **output từ node "Join group"** (để cập nhật trạng thái).
- **Lưu ý**:
  - Các sếp cần **điền chính xác** cột và hàng trong Google Sheets.

##### **G. Remplir liste (Thêm vào danh sách đã tham gia)**
- **Cấu hình**:
  - Chọn **Google Sheets OAuth2 credentials**.
  - **Operation**: `append`.
  - **Input**: Chọn **output từ node "Join group"** (để ghi danh sách nhóm đã tham gia).
- **Lưu ý**:
  - Các sếp cần **tạo một sheet mới** để lưu danh sách này (ví dụ: `Joined_Groups`).

##### **H. Merge (Gộp dữ liệu)**
- **Cấu hình**:
  - Node này **gộp** các output từ các node trước để **tránh lỗi merge**.
- **Lưu ý**:
  - **Không cần chỉnh sửa** node này, chỉ cần **bật Active**.

---

#### **3. Kích hoạt ⚡️**
1. **Test run** với **1-2 mã mời mẫu** để kiểm tra:
   - Node `Join group` có hoạt động không?
   - Trạng thái trong Google Sheets có được cập nhật không?
2. **Bật Active workflow** và **đợi Schedule Trigger chạy** (hoặc kích hoạt bằng Webhook).

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack/Telegram** để **báo cáo kết quả** mỗi lần chạy (ví dụ: "Đã tham gia 30/50 nhóm thành công").
   - **Cách làm**:
     ```json
     {
       "node": "n8n-nodes-base.slack",
       "operation": "sendMessage",
       "text": "🚀 Workflow tự động tham gia WhatsApp đã hoàn thành!\n- Thành công: {{ $node["Join group"].jsonpath("$.success") }}\n- Thất bại: {{ $node["Join group"].jsonpath("$.failed") }}"
     }
     ```

2. **Lưu log chi tiết**:
   - Thêm node **Google Sheets** để **ghi log** tất cả các lỗi (ví dụ: mã mời không hợp lệ, lỗi API).
   - **Cấu hình**:
     ```json
     {
       "node": "n8n-nodes-base.googleSheets",
       "operation": "append",
       "sheetName": "Logs",
       "range": "A:A",
       "data": {
         "timestamp": "{{ $node["Join group"].jsonpath("$.timestamp") }}",
         "code": "{{ $node["Lire invitation code"].jsonpath("$.code") }}",
         "error": "{{ $node["Join group"].jsonpath("$.error") }}"
       }
     }
     ```

3. **Gửi báo cáo định kỳ**:
   - Sử dụng **Schedule Trigger** để chạy **mỗi tuần** và gửi **báo cáo tổng hợp** qua email (node `n8n-nodes-base.email`).
   - **Cách làm**:
     ```json
     {
       "node": "n8n-nodes-base.email",
       "to": "email@doanhnghiep.com",
       "subject": "Báo cáo tự động tham gia WhatsApp - Tuần {{ $date.format("YYYY-MM-DD") }}",
       "html": "Xin chào,\n\nTổng kết tuần này:\n- Thành công: {{ $node["Merge"].jsonpath("$.success") }}\n- Thất bại: {{ $node["Merge"].jsonpath("$.failed") }}\n\nXin cảm ơn!"
     }
     ```

4. **Optimize Performance**:
   - **Thêm node `Wait`** giữa các bước để **tránh bị chặn API** của Evolution.
   - **Cấu hình**:
     ```json
     {
       "node": "n8n-nodes-base.wait",
       "time": 2000 // Chờ 2 giây giữa các yêu cầu
     }
     ```

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc mệt mỏi là **tham gia nhóm WhatsApp thủ công**. Với **Google Sheets + Evolution API**, các sếp có thể:
✅ **Tự động hóa 100%** quá trình tham gia nhóm.
✅ **Theo dõi kết quả** một cách dễ dàng.
✅ **Hoạt động 24/7** mà không cần can thiệp.

**Hành động ngay hôm nay!**
1. **Self-host n8n** và **cài Evolution API**.
2. **Import workflow** và **cấu hình Google Sheets**.
3. **Bật Schedule Trigger** và **đợi tự động hóa hoạt động!**

👉 **Bắt đầu tự động hóa ngay bây giờ!** [Tải workflow](https://n8n.io/workflows/8880) và **cài đặt VPS** với mã giảm giá **VPSN8N** để tiết kiệm chi phí! 🚀