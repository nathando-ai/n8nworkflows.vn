---
title: "🚀 Tự Động Trích Xuất Thông Tin Sản Phẩm Từ Website Và Lưu Trữ Trên Google Sheets (Không Cần Code)"
description: "Workflow tự động hóa trích xuất thông tin sản phẩm (tên, giá, mô tả) từ URL trên Google Sheets bằng Dumpling AI, tiết kiệm thời gian nghiên cứu thị trường lên đến 80%. Hoạt động 24/7, không cần can thiệp thủ công."
slug: "tieu-dong-trich-xuat-thong-tin-san-pham-dumpling-ai"
tags: [n8n, automation, market-research, ai-summarization, google-sheets, dumpling-ai]
keywords: [n8n workflow tự động hóa, trích xuất dữ liệu website, Dumpling AI, nghiên cứu thị trường, tự động hóa Google Sheets]
---

# 🚀 **Tự Động Trích Xuất Thông Tin Sản Phẩm Từ Website Và Lưu Trữ Trên Google Sheets**

### **Giải pháp cho các sếp không còn phải "copy-paste" thủ công nữa!**
Hãy tưởng tượng: Bạn chỉ cần **nhập URL sản phẩm** vào một Google Sheet, workflow sẽ tự động:
✅ **Trích xuất** tên sản phẩm, giá, mô tả từ trang web
✅ **Phân tách** nếu trang web chứa nhiều sản phẩm
✅ **Lưu trữ** dữ liệu sạch vào một sheet mới **"product details"**
**Kết quả?** Tiết kiệm **80% thời gian** so với cách làm thủ công, đồng thời giảm thiểu sai sót.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **ổn định 24/7**, các sếp nên **self-host n8n** trên VPS. Nếu chưa có, hãy đăng ký ngay:
👉 [VPS TinoHost (Mã giảm giá: **VPSN8N** - 39% off)](https://tino.vn/vps-n8n?affid=388)
👉 [VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần copy-paste thủ công từ hàng trăm trang web.
- **Dữ liệu chính xác**: Dumpling AI trích xuất thông tin với độ chính xác cao.
- **Hoạt động liên tục**: Workflow chạy tự động khi có URL mới trong Google Sheets.
- **Dữ liệu sạch**: Thông tin được phân tách và lưu trữ theo cấu trúc nhất quán.
- **Tích hợp AI**: Sử dụng Dumpling AI để tự động hóa trích xuất thông tin phức tạp.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets** (và **API OAuth2** đã cấu hình trong n8n).
2. **API Key của Dumpling AI** (để kết nối với node `httpRequest`).
3. **Một Google Sheet** chứa cột `URL` (các sếp sẽ nhập URL sản phẩm vào đây).
4. **Một sheet mới** tên **"product details"** (để lưu kết quả trích xuất).

---
### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/6950](https://n8n.io/workflows/6950) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/6950) và paste vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này gồm **4 node chính**, các sếp cần chú ý cấu hình như sau:

##### **Node 1: Watch New Website URL in Google Sheets (googleSheetsTrigger)**
- **Cấu hình**:
  - **Credentials**: Chọn `googleSheetsTriggerOAuth2Api` (đã cấu hình trước).
  - **Sheet Name**: Chọn **sheet chứa URL** (ví dụ: `"input_urls"`).
  - **Trigger Column**: Chọn cột chứa **URL** (ví dụ: `"URL"`).
  - **Trigger Condition**: Chọn **"New row"** (để workflow kích hoạt khi có URL mới).

##### **Node 2: Extract Product Info with Dumpling AI (httpRequest)**
- **Cấu hình**:
  - **Method**: `POST`.
  - **URL**: `https://api.dumpling.ai/scrape` (hoặc URL API của Dumpling AI).
  - **Headers**:
    - `Authorization`: `Bearer <API_KEY_DUMPLING_AI>` (điền API Key của mình).
    - `Content-Type`: `application/json`.
  - **Body (JSON)**:
    ```json
    {
      "url": "{{$json.url}}",
      "fields": ["productName", "price", "productDescription"]
    }
    ```
    *(`{{$json.url}}` là biến động từ node trước, trích xuất từ cột URL trong Google Sheets.)*

##### **Node 3: Split Extracted Products (splitOut)**
- **Cấu hình**:
  - **Split By**: Chọn `"products"` (nếu Dumpling AI trả về nhiều sản phẩm trong một JSON).
  - **Output Path**: `{{$json.products}}` (đảm bảo dữ liệu được phân tách thành các item riêng lẻ).

##### **Node 4: Append Product Info to Google Sheets (googleSheets)**
- **Cấu hình**:
  - **Credentials**: Chọn `googleSheetsOAuth2Api` (khác với node trigger).
  - **Sheet Name**: Chọn **"product details"** (sheet lưu kết quả).
  - **Operation**: `append` (để thêm dữ liệu mới vào cuối sheet).
  - **Data Format**: Chọn **"JSON"** và điền cấu trúc dữ liệu tương ứng (ví dụ: `{{$json.productName}}`, `{{$json.price}}`, `{{$json.productDescription}}`).

---
#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Thêm một URL vào sheet `input_urls` và chạy **Test Run** để kiểm tra workflow.
   - Kiểm tra sheet `product details` xem dữ liệu có được lưu đúng không.
2. **Bật Active**:
   - Sau khi test thành công, **bật Active** để workflow chạy tự động khi có URL mới.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tích hợp Slack/Telegram**:
   - Thêm node `slack` hoặc `telegram` sau node `googleSheets` để **báo cáo kết quả** khi trích xuất thành công.
   - Ví dụ: `{"text": "🚀 Trích xuất thành công sản phẩm: {{$json.productName}} từ URL: {{$json.url}}"}`.

2. **Lưu log hoạt động**:
   - Thêm node `stickyNote` để ghi lại **lịch sử hoạt động** (ví dụ: thời gian trích xuất, URL, status).

3. **Gửi báo cáo định kỳ**:
   - Sử dụng node `googleSheets` kết hợp với `googleCalendar` để **tạo báo cáo hàng tuần** về sản phẩm mới.

4. **Tối ưu Dumpling AI**:
   - Nếu Dumpling AI không trích xuất đầy đủ, thử **cấu hình lại `fields`** trong body request (ví dụ: thêm `"brand"`, `"rating"`).

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp trong việc nghiên cứu thị trường, đồng thời **giảm thiểu sai sót** khi trích xuất dữ liệu từ website. **Chỉ cần nhập URL vào Google Sheets**, workflow sẽ tự động làm tất cả!

**Hành động ngay**:
1. **Self-host n8n** trên VPS để workflow chạy 24/7.
2. **Cấu hình API Dumpling AI** và Google Sheets.
3. **Import workflow** và bắt đầu tự động hóa!

👉 [Tải workflow từ n8n.io](https://n8n.io/workflows/6950) và **cài đặt ngay**!