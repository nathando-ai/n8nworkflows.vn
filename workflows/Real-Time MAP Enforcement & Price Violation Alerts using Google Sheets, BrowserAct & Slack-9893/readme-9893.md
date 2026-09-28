---
title: "🚀 Tự Động Hóa Kiểm Tra Giá MAP Thực Tế & Cảnh Báo Vi Phạm Trên Slack (n8n + BrowserAct + Google Sheets)"
description: "Giải pháp tự động hóa 100% không code để theo dõi giá bán của các nhà phân phối, phát hiện vi phạm MAP (Minimum Advertised Price) và gửi cảnh báo chi tiết đến Slack trong thời gian thực. Tiết kiệm thời gian kiểm tra thủ công, giảm thiểu rủi ro vi phạm và tối ưu hóa giá bán cho doanh nghiệp."
slug: "tu-dong-hoa-kiem-tra-gia-map-thuc-te"
tags: [n8n, automation, no-code, market-research, browseract, google-sheets, slack-integration]
keywords: [tự động hóa kiểm tra giá MAP, n8n workflow, browseract n8n, cảnh báo vi phạm giá bán, tự động hóa bán hàng, tự động hóa thị trường]
---

# 🚀 **Tự Động Hóa Kiểm Tra Giá MAP Thực Tế & Cảnh Báo Vi Phạm Trên Slack**

### **Giải pháp cho các sếp bán hàng, marketing và quản lý sản phẩm:**
Bạn có bao giờ phải **tốn nhiều giờ** để kiểm tra giá bán của các nhà phân phối, so sánh với giá MAP (Minimum Advertised Price) của mình, và phát hiện vi phạm thủ công? Hoặc phải **lo lắng** rằng một nhà phân phối nào đó đang bán sản phẩm của bạn dưới giá quy định, gây mất uy tín và thiệt hại tài chính?

**Workflow này sẽ giúp các sếp:**
✅ **Tự động hóa 100% quá trình kiểm tra giá** trên các trang web của nhà phân phối.
✅ **Phát hiện vi phạm MAP trong thời gian thực** và gửi cảnh báo chi tiết đến Slack.
✅ **Tiết kiệm thời gian** từ hàng giờ/lần xuống còn **không cần can thiệp** (chỉ cần bật workflow).
✅ **Cá nhân hóa cảnh báo** cho từng trường hợp (giá thấp hơn MAP, sản phẩm hết hàng, lỗi scraping).
✅ **Hoạt động 24/7** mà không cần nhân viên theo dõi.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính bảo mật và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần kiểm tra thủ công hàng ngày, giảm thiểu sai sót.
- **Chính xác 100%**: Dữ liệu giá được scrap từ trang web thực tế, không phụ thuộc vào báo cáo của nhà phân phối.
- **Cảnh báo tức thời**: Nhận thông báo vi phạm trên Slack ngay khi phát hiện, giúp phản ứng nhanh chóng.
- **Tối ưu hóa giá bán**: Đảm bảo giá bán của các nhà phân phối không vi phạm MAP, bảo vệ lợi nhuận của doanh nghiệp.
- **Dễ dàng mở rộng**: Thêm hoặc loại bỏ nhà phân phối chỉ cần chỉnh sửa Google Sheet.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản BrowserAct**:
   - [Đăng ký miễn phí](https://www.browseract.com/) và tạo **API Key**.
   - Tải và cài đặt **n8n Community Node BrowserAct** từ [npmjs](https://www.npmjs.com/package/n8n-nodes-browseract-workflows).
   - **Template BrowserAct**: Sử dụng template có tên **"MAP (Minimum Advertised Price) Violation Alerts"**.

2. **Google Sheets**:
   - Một bảng Google Sheets chứa các cột sau:
     - `Reseller_URL` (URL sản phẩm trên trang web nhà phân phối).
     - `Reseller_Name` (Tên nhà phân phối).
     - `Product_SKU` (Mã sản phẩm).
     - `AP_Price` (Giá MAP chính thức của doanh nghiệp).

3. **Tài khoản Slack**:
   - Một **Slack Workspace** và **Channel ID** để gửi cảnh báo.
   - **Credentials OAuth2** cho Slack trong n8n.

4. **n8n Workflow**:
   - Cài đặt **n8n Community Node BrowserAct** (nếu chưa có).
   - Tạo một **Workflow mới** trong n8n Editor.

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào n8n Editor:
- **Tải file JSON** từ [n8n.io/workflows/9893](https://n8n.io/workflows/9893) (nếu có).
- **Hoặc copy toàn bộ JSON** từ [link gốc](https://n8n.io/workflows/9893) và dán vào **Import Workflow** trong n8n Editor.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Sau khi import, các sếp cần **cấu hình chi tiết** các node quan trọng:

##### **A. Schedule Trigger**
- **Thiết lập lịch chạy**: Chọn tần suất (ví dụ: **mỗi giờ** hoặc **mỗi ngày**).
- **Lưu ý**: Thời gian chạy nên trùng với giờ hoạt động của các trang web nhà phân phối để tránh lỗi scraping.

##### **B. Get row(s) in sheet (Google Sheets)**
- **Chọn Credentials**: Chọn `googleSheetsOAuth2Api` đã cấu hình trước.
- **Chọn Sheet và Range**:
  - **Sheet Name**: Tên của bảng Google Sheets chứa danh sách nhà phân phối.
  - **Range**: Chọn toàn bộ dữ liệu (ví dụ: `Sheet1!A:D`).
- **Lưu ý**: Đảm bảo cột `AP_Price` chứa giá MAP chính xác (số nguyên hoặc số thập phân).

##### **C. Loop Over Items (splitInBatches)**
- **Kích hoạt**: Đảm bảo node này được **bật** để workflow xử lý từng nhà phân phối một cách riêng biệt.
- **Lưu ý**: Nếu không kích hoạt, workflow có thể xử lý sai dữ liệu (trộn lẫn giữa các nhà phân phối).

##### **D. Run a workflow task (BrowserAct)**
- **Chọn Credentials**: Chọn `browserActApi` đã cấu hình.
- **Chọn Workflow ID**: Điền **ID của template BrowserAct** (template **"MAP (Minimum Advertised Price) Violation Alerts"**).
- **Điền tham số**:
  - **URL**: Sử dụng `{{$node["Get row(s) in sheet"].json[].Reseller_URL}}` (đường dẫn động đến cột `Reseller_URL` từ Google Sheets).
  - **Lưu ý**: Đảm bảo template BrowserAct đã được cấu hình để scrap giá sản phẩm từ trang web nhà phân phối.

##### **E. If (Kiểm tra vi phạm giá)**
- **Điều kiện**: So sánh giá scrap (`Price`) với giá MAP (`AP_Price`).
  - Nếu `Price < AP_Price`, workflow sẽ chuyển sang node **Send a message** để gửi cảnh báo.
- **Lưu ý**: Đảm bảo giá trong `Price` là số nguyên (nếu cần, sử dụng **Code Node** để chuyển đổi kiểu dữ liệu).

##### **F. If1 (Kiểm tra sản phẩm hết hàng)**
- **Điều kiện**: Kiểm tra nếu giá scrap trả về **"NoData"** (sản phẩm không tìm thấy).
- **Lưu ý**: Nếu sản phẩm hết hàng, workflow sẽ gửi cảnh báo riêng biệt trên Slack.

##### **G. Send a message (Slack)**
- **Chọn Credentials**: Chọn `slackOAuth2Api`.
- **Cấu hình Slack Message**:
  - **Channel ID**: Điền **ID của Channel Slack** muốn gửi cảnh báo (ví dụ: `#map-violations`).
  - **Thông điệp mẫu**:
    ```json
    {
      "text": "🚨 **Violation Alert**: {{$node["Get row(s) in sheet"].json[].Reseller_Name}} is selling below MAP!",
      "blocks": [
        {
          "type": "section",
          "text": {
            "type": "mrkdwn",
            "text": "*Violation Detected!*\nReseller: <{{$node["Get row(s) in sheet"].json[].Reseller_URL}}|{{$node["Get row(s) in sheet"].json[].Reseller_Name}}>\nProduct SKU: {{$node["Get row(s) in sheet"].json[].Product_SKU}}\nCurrent Price: ${{$json["Price"]}}\nMAP Price: ${{$node["Get row(s) in sheet"].json[].AP_Price}}"
          }
        }
      ]
    }
    ```
- **Lưu ý**: Đảm bảo **Channel ID** trong cả hai node Slack (`Send a message` và `Send a message1`) trùng nhau.

##### **H. Code Node (Nếu cần xử lý dữ liệu)**
- **Mục đích**: Chuyển đổi hoặc xử lý dữ liệu trước khi so sánh (ví dụ: loại bỏ ký tự tiền tệ, chuyển đổi kiểu dữ liệu).
- **Mẫu mã JavaScript**:
  ```javascript
  // Ví dụ: Loại bỏ ký tự $ và chuyển đổi thành số
  return {
    Price: parseFloat($input.all().Price.replace(/[^\d.]/g, ''))
  };
  ```

#### **3. Kích hoạt ⚡️**
- **Test Run**: Chạy **Test Run** với một nhà phân phối mẫu để kiểm tra workflow hoạt động như thế nào.
- **Bật Active**: Sau khi kiểm tra thành công, **bật Active** workflow để nó chạy tự động theo lịch.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tăng cường cảnh báo**:
   - Thêm **node Email** để gửi cảnh báo đến email cá nhân của các sếp.
   - Sử dụng **node Merge** để kết hợp dữ liệu vi phạm từ nhiều nhà phân phối vào một báo cáo tổng hợp.

2. **Lưu log vi phạm**:
   - Thêm **node Google Sheets** sau node Slack để ghi lại tất cả vi phạm vào một bảng riêng (ví dụ: `Violation_Log`).
   - Cấu hình cột: `Date`, `Reseller_Name`, `Product_SKU`, `Current_Price`, `MAP_Price`, `Status`.

3. **Tự động phản hồi**:
   - Sử dụng **node Slack** để gửi **tin nhắn tự động** yêu cầu nhà phân phối xác nhận việc vi phạm.
   - Ví dụ:
     ```json
     {
       "text": "Please confirm if the price of <{{$node["Get row(s) in sheet"].json[].Product_SKU}}|{{$node["Get row(s) in sheet"].json[].Product_SKU}}> is correct. MAP Price: ${{$node["Get row(s) in sheet"].json[].AP_Price}}"
     }
     ```

4. **Báo cáo định kỳ**:
   - Sử dụng **node Schedule Trigger** để chạy workflow **mỗi tuần** và gửi **báo cáo tổng hợp** về vi phạm qua Slack hoặc email.
   - Dữ liệu báo cáo có thể lấy từ **Google Sheets Log**.

5. **Kết hợp với CRM**:
   - Nếu sử dụng **HubSpot, Salesforce** hoặc **Zoho CRM**, thêm node tương ứng để cập nhật thông tin vi phạm vào hệ thống CRM.

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa kiểm tra giá MAP, phát hiện vi phạm và phản ứng nhanh chóng. Với **n8n + BrowserAct + Google Sheets + Slack**, các sếp không chỉ tiết kiệm thời gian mà còn **tăng cường kiểm soát giá bán**, bảo vệ lợi nhuận và duy trì uy tín thương hiệu.

**Hành động ngay hôm nay!**
1. **Chuẩn bị tài khoản** BrowserAct, Google Sheets và Slack.
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Bật Active** và để workflow làm việc cho bạn!

**Nếu gặp khó khăn**, tham khảo các video hướng dẫn từ [BrowserAct](https://www.youtube.com/c/BrowserAct) hoặc liên hệ cộng đồng n8n trên [Discord](https://discord.com/invite/UpnCKd7GaU).

---
**🚀 Chúc các sếp thành công với việc tự động hóa!**