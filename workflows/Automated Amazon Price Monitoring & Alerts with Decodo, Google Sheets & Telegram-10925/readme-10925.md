---
title: "🚀 Tự Động Hóa Theo Dõi Giá Amazon & Cảnh Báo Giá Thay Đổi với Decodo, Google Sheets & Telegram"
description: "Giải pháp tự động hóa 100% không code để theo dõi giá sản phẩm Amazon, so sánh với giá cơ sở, và cảnh báo tăng/giảm giá qua Telegram/Gmail - tiết kiệm thời gian cho các sếp marketing & e-commerce lên tới 20 giờ/tuần."
slug: "tự-dộng-hoa-theo-doi-gia-amazon"
tags: [n8n, automation, e-commerce, market-research, decodo, google-sheets, telegram]
keywords: [tự động hóa giá amazon, cảnh báo giá thay đổi, decodo n8n, google sheets automation, alert price change]
---

# 🚀 **Tự Động Hóa Theo Dõi Giá Amazon & Cảnh Báo Giá Thay Đổi (Decodo + Google Sheets + Telegram)**

### **🔍 Nỗi Đau Của Các Sếp E-Commerce & Marketing**
- **Thủ công theo dõi giá hàng ngày**: Các sếp phải mất **tối thiểu 2-3 giờ/ngày** để check giá sản phẩm trên Amazon, so sánh với giá cơ sở, và cảnh báo đồng nghiệp.
- **Rủi ro bỏ lỡ cơ hội**: Giá tăng đột ngột (threat) hoặc giảm (opportunity) mà không được phát hiện kịp thời → ảnh hưởng đến chiến lược mua bán.
- **Không có báo cáo tự động**: Dữ liệu phân tán trên nhiều sheet Excel, email, hoặc Slack → khó theo dõi lịch sử và dự đoán xu hướng.
- **Tốn thời gian phản hồi**: Khi giá thay đổi, các sếp phải **tìm kiếm thủ công** sản phẩm trên Amazon và so sánh → mất thêm 15-30 phút/sự kiện.

**✅ Giải Pháp Của Workflow Này:**
Automate **tất cả quá trình** từ lấy dữ liệu Amazon → so sánh giá → cảnh báo tăng/giảm → lập lịch họp nội bộ → gửi email báo cáo **với 0 sự can thiệp của con người**. Các sếp chỉ cần **cấu hình 1 lần** và workflow sẽ hoạt động **24/7 tự động**.

---
## 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm 15-20 giờ/tuần** (tương đương **1 ngày làm việc/ngày**) cho việc theo dõi giá thủ công.
- **Cảnh báo tức thời** khi giá tăng > ngưỡng (threat) hoặc giảm > ngưỡng (opportunity) qua **Telegram/Gmail**.
- **Lập lịch họp tự động** cho đội ngũ khi có sự thay đổi lớn (giá tăng > 10%).
- **Báo cáo tự động** trên Google Sheets với lịch sử giá, % thay đổi, và link sản phẩm.
- **Không bị giới hạn API**: Workflow được tối ưu để tránh bị chặn rate limit của Decodo/Amazon.
- **Cá nhân hóa thông báo**: Chỉ cảnh báo cho người quản lý khi giá tăng đột ngột, còn giảm giá thì gửi email chi tiết cho team mua hàng.
:::

---
## 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
### **1. Tài Khoản & API Keys**
| Dịch Vụ               | Thông Tin Cần Thiết                                                                 | Ghi Chú                                  |
|-----------------------|-------------------------------------------------------------------------------------|-------------------------------------------|
| **Decodo**            | API Key (trong [Decodo Dashboard](https://decodo.com/))                              | Cần quyền truy cập API.                 |
| **Google Sheets**     | OAuth 2.0 Credentials (trong [Google Cloud Console](https://console.cloud.google.com/)) | Cần quyền chỉnh sửa sheet.              |
| **Google Calendar**   | OAuth 2.0 Credentials (trong [Google Cloud Console](https://console.cloud.google.com/)) | Cần quyền tạo sự kiện.                  |
| **Gmail**             | OAuth 2.0 Credentials (trong [Google Cloud Console](https://console.cloud.google.com/)) | Địa chỉ email chính thức của công ty.   |
| **Telegram**          | API Token (trong [@BotFather](https://t.me/BotFather)) + Chat ID của nhóm quản lý   | Cần tạo bot Telegram riêng.              |

### **2. Google Sheet Mẫu**
- **Cột bắt buộc**:
  - `url` (link sản phẩm Amazon).
  - `baseline price (usd)` (giá cơ sở để so sánh).
  - *(Tùy chọn)* `threshold` (ngưỡng cảnh báo, mặc định là 5%).
- **Ví dụ**:
  | url                          | baseline price (usd) | threshold (%) |
  |------------------------------|----------------------|--------------|
  | https://www.amazon.com/dp/B08K5J1X1L | 49.99               | 5            |

---
## 🚀 **Cách Import & Cấu Hình Workflow**

### **1. Import Workflow 📥**
#### **Phương Pháp 1: Import từ File JSON**
1. **Tải workflow** từ [n8n.io/workflows/10925](https://n8n.io/workflows/10925) (chọn "Download JSON").
2. **Mở n8n Editor** (trên self-hosted hoặc n8n.cloud).
3. Nhấn **"Import"** → Chọn file JSON vừa tải → **"Import Workflow"**.

#### **Phương Pháp 2: Copy/Paste JSON**
1. Mở file JSON từ [n8n.io/workflows/10925](https://n8n.io/workflows/10925) (chọn "Copy JSON").
2. Trong n8n Editor, nhấn **"Import"** → **"Paste JSON"** → Dán và nhấn **"Import"**.

---
### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflows này có **11 node**, nhưng các sếp chỉ cần chú ý đến **5 node quan trọng** sau:

#### **🔹 Node 1: Schedule Trigger (Lập Lịch Khởi Động)**
- **Cấu hình**:
  - **Interval**: Chọn **1-4 giờ** (để tránh bị rate limit của Decodo).
  - **Named Schedule**: Ghi tên như `amazon_price_monitor` để dễ quản lý.
  - **Timezone**: Chọn timezone phù hợp với công ty (ví dụ: `Asia/Ho_Chi_Minh`).
- **Lưu ý**:
  - **Không đặt quá thường** (ví dụ: 15 phút) để tránh bị chặn API của Decodo.

#### **🔹 Node 2: Get row(s) in sheet (Lấy Dữ liệu từ Google Sheets)**
- **Cấu hình**:
  - **Credentials**: Chọn `googleSheetsOAuth2Api` (đã cấu hình trước).
  - **Sheet ID**: Điền ID sheet của bạn (tìm trong URL sheet: `https://docs.google.com/spreadsheets/d/[ID]/edit`).
  - **Range**: Điền `Sheet1!A2:B` (giả sử dữ liệu từ hàng 2).
  - **Columns**: Chọn `url, baseline price (usd)` (nếu sheet có cột `threshold`, chọn thêm).
- **Lưu ý**:
  - **Kiểm tra sheet** có cột `url` và `baseline price (usd)` không? Nếu thiếu, workflow sẽ lỗi.

#### **🔹 Node 3: Decodo (Lấy Giá Thực Tế từ Amazon)**
- **Cấu hình**:
  - **Credentials**: Chọn `decodoApi` (đã cấu hình API Key).
  - **Operation**: Để mặc định là `amazon`.
  - **Parameters**:
    - `url`: Lấy từ cột `url` trong Google Sheets.
    - `product_id`: *(Tùy chọn)* Nếu muốn lấy sản phẩm cụ thể.
- **Lưu ý**:
  - **Rate Limit**: Decodo cho phép **500 request/ngày**. Nếu workflow chạy quá thường, Decodo có thể tạm ngừng API.
  - **Error Handling**: Nếu Decodo trả về lỗi (ví dụ: URL không hợp lệ), workflow sẽ **bỏ qua sản phẩm đó** và tiếp tục.

#### **🔹 Node 4: Calculate Price Changes (Tính Toán % Thay Đổi Giá)**
- **Code Node** (mặc định đã có trong workflow):
  ```javascript
  // Giả sử input có:
  // - $json.decodo.current_price (giá hiện tại từ Decodo)
  // - $json.googleSheets.baseline_price (giá cơ sở từ sheet)
  // - $json.googleSheets.threshold (ngưỡng cảnh báo, mặc định 5%)

  // Tính toán
  const priceDiff = $json.decodo.current_price - $json.googleSheets.baseline_price;
  const percentChange = ($json.decodo.current_price / $json.googleSheets.baseline_price - 1) * 100;

  // Định nghĩa route
  if ($json.googleSheets.threshold === undefined) {
    $json.threshold = 5; // Mặc định
  }

  if (percentChange > $json.threshold) {
    $json.route = "High"; // Giá tăng quá ngưỡng
  } else if (percentChange < -$json.threshold) {
    $json.route = "Low";  // Giá giảm quá ngưỡng
  } else {
    $json.route = "Normal"; // Giá ổn định
  }

  // Trả về kết quả
  return {
    price_diff: priceDiff,
    percent_change: percentChange.round(2),
    route: $json.route,
    current_price: $json.decodo.current_price,
    baseline_price: $json.googleSheets.baseline_price,
  };
  ```
- **Lưu ý**:
  - **Kiểm tra giá cơ sở**: Nếu `baseline_price` là `0`, workflow sẽ **bỏ qua sản phẩm** để tránh lỗi chia cho 0.
  - **Làm tròn % thay đổi**: Giá trị `% change` được làm tròn đến **2 chữ số thập phân**.

#### **🔹 Node 5: Price Routing (Xác Định Loại Cảnh Báo)**
- **Cấu hình**:
  - **Switch Case**:
    - **`High`**: Giá tăng > ngưỡng → chuyển đến **Set Meeting** (lập lịch họp) và **Send Message to Top Management** (Telegram).
    - **`Low`**: Giá giảm > ngưỡng → chuyển đến **Email Stakeholders** (Gmail).
    - **`Normal`**: Giá ổn định → chuyển đến **No Operation** (bỏ qua).

#### **🔹 Node 6: Set Meeting (Lập Lịch Họp cho Giá Tăng)**
- **Cấu hình**:
  - **Credentials**: Chọn `googleCalendarOAuth2Api`.
  - **Parameters**:
    - **Summary**: `🚨 Giá sản phẩm tăng đột ngột: [Product Name]`.
    - **Description**:
      ```
      Giá sản phẩm **[Product Name]** (URL: [$json.decodo.url]) đã tăng từ **$[$json.googleSheets.baseline_price] USD** lên **$[$json.decodo.current_price] USD** (+$[$json.price_diff.round(2)] USD, **+$[$json.percent_change]%**).

      **Ngưỡng cảnh báo**: $[$json.threshold]%.
      **Người cần tham gia**: [@Người Quản Lý 1], [@Người Quản Lý 2].
      ```
    - **Start Time**: Thời gian hiện tại + 15 phút (để team có thời gian chuẩn bị).
    - **End Time**: Thời gian hiện tại + 30 phút.
    - **Time Zone**: Chọn timezone của công ty.

#### **🔹 Node 7: Send Message to Top Management (Telegram)**
- **Cấu hình**:
  - **Credentials**: Chọn `telegramApi`.
  - **Parameters**:
    - **Chat ID**: ID của nhóm Telegram quản lý (tìm bằng cách gửi tin nhắn cho bot và copy ID từ URL).
    - **Message**:
      ```
      🚨 **GIÁ TĂNG ĐỘT NGỘT** 🚨
      **Sản phẩm**: [$json.decodo.title]
      **URL**: [$json.decodo.url]
      **Giá cơ sở**: $[$json.googleSheets.baseline_price] USD
      **Giá hiện tại**: $[$json.decodo.current_price] USD
      **Thay đổi**: +$[$json.price_diff.round(2)] USD (+$[$json.percent_change]%)
      **Ngưỡng cảnh báo**: $[$json.threshold]%
      ```

#### **🔹 Node 8: Email Stakeholders (Gmail)**
- **Cấu hình**:
  - **Credentials**: Chọn `gmailOAuth2`.
  - **Parameters**:
    - **To**: Email của team mua hàng (ví dụ: `team-purchasing@company.com`).
    - **Subject**: `🔽 Giá sản phẩm [$json.decodo.title] giảm xuống [$json.decodo.current_price] USD`.
    - **HTML Body**:
      ```html
      <div style="font-family: Arial, sans-serif; max-width: 600px;">
        <h2>🔽 Giá sản phẩm đã giảm</h2>
        <p><strong>Tên sản phẩm:</strong> [$json.decodo.title]</p>
        <p><strong>URL:</strong> <a href="$[$json.decodo.url]">[$json.decodo.url]</a></p>
        <p><strong>Giá cơ sở:</strong> $[$json.googleSheets.baseline_price] USD</p>
        <p><strong>Giá hiện tại:</strong> $[$json.decodo.current_price] USD</p>
        <p><strong>Thay đổi:</strong> -$[$json.price_diff.round(2)] USD (-$[$json.percent_change]%)</p>
        <p><strong>Ngưỡng cảnh báo:</strong> $[$json.threshold]%</p>
        <p>📌 <strong>Hành động khuyến nghị:</strong>
          <ul>
            <li>Xác nhận đơn hàng với giá mới.</li>
            <li>Kiểm tra nguồn cung để tránh thiếu hàng.</li>
          </ul>
        </p>
        <p>Trân trọng,<br>Hệ thống Tự Động Hóa Giá Amazon</p>
      </div>
      ```
    - **CC/BCC**: *(Tùy chọn)* Email của người quản lý dự án.

---
### **3. Kích Hoạt Workflow ⚡️**
1. **Test Run** (kiểm tra trước khi bật):
   - Nhấn **"Run Workflow"** với dữ liệu mẫu (ví dụ: 1 sản phẩm có giá tăng).
   - Kiểm tra:
     - **Telegram**: Có nhận được tin nhắn không?
     - **Google Calendar**: Có sự kiện mới không?
     - **Gmail**: Có email không?
     - **Google Sheets**: Có cập