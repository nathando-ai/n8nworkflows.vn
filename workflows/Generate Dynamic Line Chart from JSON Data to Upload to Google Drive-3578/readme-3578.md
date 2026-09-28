---
title: "📊 Tự Động Vẽ Biểu Đồ Line Chart Tĩnh Từ JSON & Upload Tự Động Vào Google Drive (Không Code)"
description: "Workflow này giúp các sếp tự động chuyển đổi dữ liệu JSON thành biểu đồ line chart đẹp mắt, sau đó upload tự động vào Google Drive chỉ trong vài giây. Giúp tiết kiệm thời gian phân tích dữ liệu và tự động hóa báo cáo định kỳ."
slug: "tieu-dong-ve-bieu-do-line-chart-tu-json-google-drive"
tags: [n8n, automation, no-code, google-drive, data-visualization, chart-generator]
keywords: [n8n workflow chart, tự động hóa biểu đồ, upload chart google drive, chuyển đổi json thành biểu đồ, tự động hóa báo cáo]
---

# 🚀 Tự Động Vẽ Biểu Đồ Line Chart Từ JSON & Upload Vào Google Drive (Không Code)

### **Giải pháp cho các sếp muốn tự động hóa báo cáo dữ liệu mà không cần viết một dòng code nào!**
Hãy tưởng tượng: Bạn có một tập dữ liệu JSON từ API, database, hoặc Google Sheets, nhưng muốn chuyển nó thành một **biểu đồ line chart chuyên nghiệp** để upload vào Google Drive cho báo cáo hàng ngày, hàng tuần. Thay vì mất thời gian vẽ thủ công trên Excel hay PowerPoint, **n8n giúp bạn tự động hóa toàn bộ quy trình chỉ với một workflow đơn giản!**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần thiết kế biểu đồ thủ công trên Excel/PowerPoint.
- **Chính xác 100%**: Dữ liệu tự động cập nhật từ JSON, tránh sai sót khi nhập liệu.
- **Báo cáo tự động**: Upload biểu đồ vào Google Drive định kỳ (ngày, tuần, tháng).
- **Cá nhân hóa**: Thay đổi kiểu biểu đồ, màu sắc, tiêu đề chỉ bằng một vài cú click.
- **Hoạt động liên tục**: Workflow chạy 24/7 trên VPS, không phụ thuộc vào máy tính cá nhân.
:::

---

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Drive** và **OAuth 2.0 API Key** của Google Drive (để upload file).
   - Hướng dẫn tạo OAuth 2.0: [Google Cloud Console](https://console.cloud.google.com/apis/credentials)
2. **Dữ liệu JSON** (có thể là:
   - Dữ liệu mẫu trong workflow (để test).
   - Dữ liệu từ **API** (HTTP Request node).
   - Dữ liệu từ **Google Sheets** (Google Sheets node).
   - Dữ liệu từ **database** (Postgres/MongoDB node).
3. **n8n Self-hosted** (để chạy workflow 24/7).
:::

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/3578](https://n8n.io/workflows/3578) và import vào **n8n Editor**.
- **Cách 2**: Copy toàn bộ JSON từ link trên và paste vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này có **4 node chính**, nhưng các sếp cần chú ý cấu hình **2 node quan trọng**:

##### **A. Node "Edit Fields: Set JSON data to test" (n8n-nodes-base.set)**
- **Mục đích**: Cung cấp dữ liệu mẫu để vẽ biểu đồ.
- **Cách chỉnh**:
  - Mở node này và chỉnh sửa phần `JSON` như sau (đảm bảo `labels` và `salesData` có cùng số lượng):
    ```json
    {
      "labels": ["Jan", "Feb", "Mar", "Apr", "May"],
      "salesData": [120, 190, 150, 250, 290]
    }
    ```
  - **Lưu ý**:
    - Nếu dùng **dữ liệu thực tế**, thay thế node này bằng:
      - **HTTP Request** (nếu lấy từ API).
      - **Google Sheets** (nếu lấy từ bảng Google).
      - **Postgres/MongoDB** (nếu lấy từ database).
    - Sau khi lấy dữ liệu, **sử dụng node "Set" khác** để định dạng lại thành cấu trúc `{labels, salesData}`.

##### **B. Node "Google Drive: Upload File" (n8n-nodes-base.googleDrive)**
- **Mục đích**: Upload biểu đồ đã tạo vào Google Drive.
- **Cách chỉnh**:
  1. Vào **Credentials** của node này và chọn `googleDriveOAuth2Api` (đã tạo trước đó).
  2. Chọn **Folder** muốn upload (hoặc tạo mới).
  3. **Tên file**: Đặt tên tự động (ví dụ: `BieuDoDoanhThu_{{ $node["QuickChart"].json["timestamp"] }}.png`).
  4. **File Type**: Chọn `PNG` (định dạng mặc định của QuickChart).

##### **C. Node "QuickChart" (n8n-nodes-base.quickChart)**
- **Mục đích**: Vẽ biểu đồ từ dữ liệu JSON.
- **Cách chỉnh**:
  - **Chart Type**: Đổi từ `line` sang `bar`, `pie`, `doughnut` nếu muốn.
  - **Customize**:
    - **Title**: Thêm tiêu đề (ví dụ: `"Doanh Thu Quý 1/2024"`).
    - **Colors**: Thay đổi màu cho biểu đồ (mã hex hoặc tên màu).
    - **Axes**: Đổi tên cho trục X/Y (ví dụ: `Trục X: Tháng`, `Trục Y: Doanh Thu (triệu USD)`).
  - **Datasets (nếu dùng nhiều dòng dữ liệu)**:
    - Mở `Dataset Options` → `Add option` → `Add dataset`.
    - Thêm biểu đồ thứ 2 bằng cách set `Data` từ một mảng khác (ví dụ: `{{ $json.jsonData.salesData2 }}`).

##### **D. Node "When clicking ‘Test workflow’" (n8n-nodes-base.manualTrigger)**
- **Mục đích**: Khởi động workflow thủ công (để test).
- **Lưu ý**:
  - Sau khi cấu hình xong, **click vào nút "Test"** để chạy workflow.
  - Nếu muốn **chạy tự động**, thay thế bằng **Schedule Trigger** (n8n-nodes-base.schedule).

---

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Click **Run Workflow** để kiểm tra biểu đồ được tạo ra và upload vào Google Drive.
   - Kiểm tra file trong Google Drive (đường dẫn đã chọn).
2. **Bật Active**:
   - Sau khi test thành công, **bật Active** để workflow chạy tự động.

---

### ✍️ Mẹo & gợi ý nâng cao
:::tip[CÁCH DÙNG THỰC TẾ]
1. **Lấy dữ liệu từ API**:
   - Thay thế node `Set` bằng **HTTP Request** (n8n-nodes-base.httpRequest) để lấy JSON từ API.
   - Ví dụ: `GET https://api.example.com/data` → `Response Body` → `Set` (định dạng lại thành `{labels, salesData}`).

2. **Lấy dữ liệu từ Google Sheets**:
   - Sử dụng **Google Sheets node** (n8n-nodes-base.googleSheets) để lấy dữ liệu từ bảng.
   - Sau đó, dùng **Set node** để chuyển đổi thành cấu trúc `{labels, salesData}`.

3. **Gửi biểu đồ qua Slack/Telegram**:
   - Thay thế node `Google Drive` bằng **Slack/Telegram node** (n8n-nodes-base.slack hoặc n8n-nodes-base.telegram).
   - Chuyển đổi file PNG thành **Base64** (n8n-nodes-base.base64) trước khi gửi.

4. **Lưu log và báo cáo định kỳ**:
   - Sử dụng **Google Sheets node** để ghi lại lịch sử biểu đồ đã tạo.
   - Kết hợp với **Schedule Trigger** để chạy workflow hàng ngày.

5. **Tạo nhiều biểu đồ cùng lúc**:
   - Sử dụng **Loop node** (n8n-nodes-base.loop) để xử lý nhiều tập dữ liệu JSON khác nhau.
   - Ví dụ: Tạo biểu đồ cho từng sản phẩm trong danh sách.

6. **Tự động cập nhật biểu đồ hàng tháng**:
   - Sử dụng **Schedule Trigger** (n8n-nodes-base.schedule) để chạy workflow vào ngày đầu tháng.
   - Thay đổi dữ liệu JSON từ **Google Sheets** (cập nhật từ file Excel).
:::

---

### 📌 Kết luận
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa báo cáo dữ liệu mà không cần viết code. Bạn có thể:
✅ **Tạo biểu đồ từ JSON** (API, database, Google Sheets).
✅ **Upload tự động vào Google Drive**.
✅ **Cập nhật định kỳ** (ngày, tuần, tháng).
✅ **Cá nhân hóa biểu đồ** (màu sắc, tiêu đề, kiểu biểu đồ).

**Hành động ngay hôm nay!**
1. **Import workflow** vào n8n của mình.
2. **Chỉnh sửa dữ liệu** và cấu hình Google Drive.
3. **Test và bật Active** để bắt đầu tự động hóa báo cáo!

👉 [Tải workflow nguyên bản](https://n8n.io/workflows/3578) và bắt đầu ngay! 🚀

---
**Cần hỗ trợ thêm?**
- **Join Cộng đồng n8n Việt Nam**: [Facebook Group](https://www.facebook.com/groups/n8nvietnam/)
- **Hỏi đáp nhanh**: [Discord n8n](https://discord.gg/n8n)