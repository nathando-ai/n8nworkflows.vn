---
title: "📊 Tự Động Hóa Báo Cáo Doanh Thu WooCommerce Hàng Ngày Cho Slack Và Ghi Chép Lịch Sử Trên Google Sheets"
description: "Giải pháp tự động hóa hoàn toàn không cần code để gửi tóm tắt doanh thu hàng ngày từ WooCommerce đến Slack và lưu trữ dữ liệu chi tiết trên Google Sheets. Tiết kiệm thời gian, tăng tính chính xác và cung cấp khả năng phân tích dài hạn cho doanh nghiệp."
slug: "tu-dong-hoa-bao-cao-woocommerce-slack-google-sheets"
tags: [n8n, automation, ecommerce, woocommerce, google-sheets, slack, crm]
keywords: [n8n workflow woocommerce, tự động hóa báo cáo doanh thu, gửi tin nhắn Slack từ WooCommerce, ghi chép dữ liệu Google Sheets, tự động hóa bán hàng online]
---

# 🚀 **Tự Động Hóa Báo Cáo Doanh Thu WooCommerce Hàng Ngày Cho Slack & Ghi Chép Lịch Sử Trên Google Sheets**

### **🔥 Nỗi Đau Của Các Sếp**
Hàng ngày, các sếp phải:
- **Tìm kiếm thủ công** dữ liệu doanh thu từ WooCommerce trên hệ thống bán hàng.
- **Tính toán thủ công** tổng doanh thu, số lượng đơn hàng, giá trị trung bình mỗi đơn (AOV) và sản phẩm bán chạy nhất.
- **Gửi báo cáo** qua Slack hoặc email để cập nhật cho đội ngũ, mất thời gian và dễ xảy ra lỗi.
- **Không có lịch sử dữ liệu** để phân tích xu hướng bán hàng dài hạn.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động hóa hoàn toàn** việc thu thập và tính toán báo cáo hàng ngày.
✅ **Gửi báo cáo trực tiếp** đến Slack với định dạng dễ đọc.
✅ **Lưu trữ dữ liệu** trên Google Sheets để phân tích lịch sử và báo cáo định kỳ.
✅ **Chỉ cần chạy một lần/ngày**, không cần can thiệp thủ công.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính riêng tư và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần tính toán thủ công hàng ngày.
- **Chính xác 100%**: Dữ liệu lấy trực tiếp từ WooCommerce, không sai sót.
- **Báo cáo tự động**: Slack thông báo ngay khi có báo cáo mới.
- **Lịch sử dữ liệu**: Google Sheets lưu trữ tất cả báo cáo để phân tích xu hướng.
- **Cá nhân hóa**: Thêm logo, thông tin doanh nghiệp vào báo cáo Slack.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản WooCommerce**:
   - API Key và Secret Key từ **WooCommerce → Settings → API**.
   - Chọn quyền `Read` cho `Orders` (hoặc `Read/Write` nếu cần).
2. **Tài khoản Slack**:
   - OAuth Token từ **Slack API** (trong n8n, chọn `slackApi`).
   - Channel hoặc user ID để gửi báo cáo (ví dụ: `#báo-cáo-doanh-thu`).
3. **Tài khoản Google Sheets**:
   - OAuth 2.0 Credentials từ [Google Cloud Console](https://console.cloud.google.com/).
   - File Google Sheets đã tạo sẵn với **bảng dữ liệu** để ghi chép (cột: `Ngày`, `Doanh Thu`, `Số Lượng Đơn`, `AOV`, `Sản Phẩm Bán Chạy`).
4. **n8n Workflow**:
   - Tài khoản n8n (self-hosted hoặc n8n.cloud).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/12901](https://n8n.io/workflows/12901) hoặc copy toàn bộ JSON từ trang này.
- **Mở n8n Editor** và chọn **Import Workflow** → Dán JSON hoặc tải file `.json`.
- **Kích hoạt workflow** bằng cách bật nút **Active** ở góc trên bên phải.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **10 node** quan trọng, các sếp cần cấu hình như sau:

##### **A. Schedule Trigger (Động cơ chạy hàng ngày)**
- **Node**: `Daily Schedule`
- **Cấu hình**:
  - Chọn **Cron Schedule**: `0 0 * * *` (chạy lúc 00:00 hàng ngày).
  - **Lưu ý**: Nếu muốn chạy vào giờ khác (ví dụ 8h sáng), thay đổi thành `0 8 * * *`.

##### **B. WooCommerce API (Lấy dữ liệu đơn hàng)**
- **Node**: `Fetch WooCommerce Orders`
- **Cấu hình**:
  - Chọn **Credentials**: `wooCommerceApi` (đã tạo trước).
  - **Operation**: `getAll` (lấy tất cả đơn hàng).
  - **Resource**: `order` (loại dữ liệu là đơn hàng).

##### **C. Filter Paid Orders (Lọc đơn đã thanh toán)**
- **Node**: `Filter Paid Orders`
- **Cấu hình**:
  - **Filter Condition**:
    ```json
    {
      "status": ["completed", "processing"]
    }
    ```
  - **Lưu ý**: Chỉ giữ đơn hàng có `status` là `completed` (đã thanh toán) hoặc `processing` (đang xử lý).

##### **D. Last 24h Orders (Lọc đơn trong 24h)**
- **Node**: `Last 24h Orders` (Code Node)
- **Mã JavaScript**:
  ```javascript
  const now = new Date();
  const twentyFourHoursAgo = new Date(now.getTime() - 24 * 60 * 60 * 1000);

  return $input.all().filter(order => {
    const orderDate = new Date(order.date_created);
    return orderDate >= twentyFourHoursAgo;
  });
  ```
  - **Lưu ý**: Node này sử dụng `date_created` của đơn hàng để lọc.

##### **E. Tính Toán Doanh Thu, AOV & Top Products (3 Code Node)**
Các sếp **không cần chỉnh sửa** mã trong các node này, nhưng cần hiểu logic:
1. **Calculate Revenue + AOV**:
   - Tính tổng doanh thu (`total`) và trung bình mỗi đơn (`average_order_value`).
2. **Calculate Top Products**:
   - Xếp hạng sản phẩm theo số lượng bán ra.
3. **Finalize Data**:
   - Định dạng dữ liệu thành một object dễ đọc.

##### **F. Merge Metrics (Gộp dữ liệu)**
- **Node**: `Merge Metrics`
- **Cấu hình**:
  - Chọn **Merge Strategy**: `All` (gộp tất cả dữ liệu từ các node trước).

##### **G. Send Slack Summary (Gửi báo cáo Slack)**
- **Node**: `Send Slack Summary`
- **Cấu hình**:
  - **Credentials**: `slackApi`.
  - **Message Format** (gợi ý):
    ```json
    {
      "text": "📊 **Báo cáo doanh thu WooCommerce - Ngày :date**",
      "blocks": [
        {
          "type": "section",
          "text": {
            "type": "mrkdwn",
            "text": `*Doanh Thu:* $${{ $json["total_revenue"] }} (${{ $json["order_count"] }} đơn)`
          }
        },
        {
          "type": "section",
          "text": {
            "type": "mrkdwn",
            "text": `*AOV:* $${{ $json["average_order_value"].toFixed(2) }}`
          }
        },
        {
          "type": "section",
          "text": {
            "type": "mrkdwn",
            "text": `*Top 3 Sản Phẩm:*\n- {{ $json["top_products"][0].name }} ({{ $json["top_products"][0].count }} đơn)\n- {{ $json["top_products"][1].name }} ({{ $json["top_products"][1].count }} đơn)\n- {{ $json["top_products"][2].name }} ({{ $json["top_products"][2].count }} đơn)`
          }
        }
      ],
      "attachments": [
        {
          "color": "#36a64f",
          "title": "Chi tiết",
          "text": `*Ngày:* {{ $json["date"] }}\n*Doanh Thu:* $${{ $json["total_revenue"] }}\n*Số Đơn:* {{ $json["order_count"] }}`
        }
      ]
    }
    ```
  - **Lưu ý**:
    - Thay `{{ $json["key"] }}` bằng tên chính xác trong dữ liệu (kiểm tra bằng **Test Run**).
    - Thêm logo doanh nghiệp vào `blocks` nếu cần.

##### **H. Append to Google Sheets (Ghi chép dữ liệu)**
- **Node**: `Append or update row in sheet`
- **Cấu hình**:
  - **Credentials**: `googleSheetsOAuth2Api`.
  - **File**: Chọn file Google Sheets đã tạo.
  - **Sheet Name**: Chọn sheet muốn ghi dữ liệu (ví dụ: `Báo cáo Doanh Thu`).
  - **Range**: `A1` (nếu sheet trống) hoặc `A2:A` (nếu đã có dữ liệu).
  - **Data Format**:
    ```json
    {
      "Ngày": "{{ $json["date"] }}",
      "Doanh Thu": "{{ $json["total_revenue"] }}",
      "Số Lượng Đơn": "{{ $json["order_count"] }}",
      "AOV": "{{ $json["average_order_value"].toFixed(2) }}",
      "Top 3 Sản Phẩm": "{{ $json["top_products"].map(p => `${p.name} (${p.count} đơn)`).join('; ') }}"
    }
    ```
  - **Lưu ý**:
    - Đảm bảo **cột trong Google Sheets** trùng khớp với keys trên.
    - Nếu sheet đã có dữ liệu, chọn **`appendOrUpdate`** để thêm hàng mới.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Chọn nút **Test** trên node `Daily Schedule`.
   - Kiểm tra **Slack** và **Google Sheets** xem báo cáo có xuất hiện không.
2. **Bật Active**:
   - Sau khi test thành công, bật **Active** để workflow chạy tự động hàng ngày.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Thêm Logo & Thông Tin Doanh Nghiệp**:
   - Tạo một **image URL** của logo và thêm vào `blocks` trong Slack:
     ```json
     {
       "type": "image",
       "image_url": "https://tên-domain.com/logo.png",
       "alt_text": "Logo Công Ty"
     }
     ```

2. **Gửi Báo Cáo Email (Ngoài Slack)**:
   - Thêm node **`n8n-nodes-base.email`** sau node Slack để gửi báo cáo email tự động.

3. **Lưu Log Lịch Sử**:
   - Thêm node **`n8n-nodes-base.http`** để ghi log vào một file JSON hoặc cơ sở dữ liệu (ví dụ: Firebase, Airtable).

4. **Báo Cáo Định Kỳ (Tuần/Tháng)**:
   - Sử dụng **Schedule Trigger** với cron khác (ví dụ: `0 0 1 * *` để chạy hàng tháng vào ngày 1).

5. **Tích Hợp với Google Analytics**:
   - Thêm node **`n8n-nodes-base.googleAnalytics`** để so sánh dữ liệu WooCommerce với traffic website.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** của các sếp khỏi công việc tính toán và báo cáo thủ công, đồng thời cung cấp **dữ liệu chính xác và lịch sử** để ra quyết định kinh doanh thông minh. **Chỉ cần import, cấu hình và bật chạy** – hệ thống sẽ tự động cập nhật báo cáo hàng ngày!

**🚀 Hành động ngay**:
1. Import workflow vào n8n của mình.
2. Cấu hình WooCommerce, Slack và Google Sheets.
3. **Test và bật Active** để bắt đầu tự động hóa!

---
**💡 Cần hỗ trợ?** Đăng ký **hỗ trợ kỹ thuật n8n** tại [n8n.io/support](https://n8n.io/support) hoặc liên hệ với **WeblineIndia** (tác giả của workflow) qua [website](https://www.weblineindia.com/).