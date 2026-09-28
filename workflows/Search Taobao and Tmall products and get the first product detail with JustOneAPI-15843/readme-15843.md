---
title: "🛒 Tự Động Tìm Kiếm Sản Phẩm Taobao/Tmall & Lấy Chi Tiết Đầu Tiên Với JustOneAPI (Không Code)"
description: "Workflow tự động hóa tìm kiếm sản phẩm trên Taobao và Tmall, lấy chi tiết sản phẩm đầu tiên với API JustOneAPI - tiết kiệm thời gian nghiên cứu thị trường lên đến 80%. Phù hợp cho doanh nghiệp eCommerce, nhà phân phối và nhà nghiên cứu thị trường."
slug: "tu-dong-tim-kiem-taobao-tmall-justoneapi"
tags: [n8n, automation, market-research, taobao, tmall, justoneapi, api-integration]
keywords: [tự động hóa tìm kiếm taobao, api justoneapi n8n, nghiên cứu thị trường taobao, lấy chi tiết sản phẩm taobao tự động, workflow n8n ecommerce]
---

# 🚀 **Tự Động Tìm Kiếm Sản Phẩm Taobao/Tmall & Lấy Chi Tiết Đầu Tiên Với JustOneAPI**

### **Giải Phẫu Nỗi Đau Của Các Sếp**
Hàng ngày, các sếp phải **tìm kiếm thủ công** sản phẩm trên Taobao và Tmall để nghiên cứu giá cả, xu hướng, hoặc tìm kiếm nguồn hàng mới. Quá trình này **tốn thời gian, dễ sai sót**, và không thể thực hiện liên tục 24/7. **Workflow này tự động hóa toàn bộ quy trình** bằng cách:
✅ **Tìm kiếm sản phẩm** theo từ khóa trên cả Taobao và Tmall.
✅ **Lấy chi tiết sản phẩm đầu tiên** (giá, mô tả, hình ảnh, stock) bằng API JustOneAPI.
✅ **Cung cấp dữ liệu sạch** để phân tích thị trường, so sánh giá, hoặc xuất khẩu dữ liệu.

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Thay vì mất 30-60 phút tìm kiếm thủ công, chỉ cần **1 click** để lấy dữ liệu chi tiết.
- **Dữ liệu chính xác**: Tránh sai sót khi copy-paste từ trang web.
- **Hoạt động liên tục**: Chạy 24/7 trên VPS, không phụ thuộc vào thời gian làm việc.
- **Dễ dàng mở rộng**: Thêm từ khóa, thay đổi API, hoặc kết nối với Slack/Telegram để báo cáo tự động.
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần:
1. **Tài khoản JustOneAPI**:
   - Đăng ký tại [JustOneAPI](https://www.justoneapi.com/) và lấy **API Key**.
   - **Mã giảm giá 10%**: Sử dụng mã `N8NAPI10` khi đăng ký.
2. **VPS để self-host n8n** (không dùng phiên bản miễn phí trên cloud):
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).
3. **Không cần kỹ thuật**: Workflow đã cấu hình sẵn, chỉ cần điền API Key và từ khóa.
:::

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/15843](https://n8n.io/workflows/15843) và import vào **n8n Editor**.
- **Cách 2**: Copy toàn bộ JSON từ link trên và dán vào **Create Workflow** trong n8n.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **9 node**, nhưng chỉ có **3 node quan trọng** cần cấu hình:

##### **A. Node "Set API and Search Parameters" (Node `set`)**
- **Cần thiết**: Điền **API Key** của JustOneAPI vào trường `JustOneAPIKey`.
- **Tham số mặc định**:
  ```json
  {
    "JustOneAPIKey": "API_KEY_CỦA_BẠN",
    "searchKeyword": "iphone 15",  // Thay đổi từ khóa tìm kiếm
    "limit": 10,                   // Số sản phẩm trả về (mặc định 10)
    "region": "cn"                 // Địa bàn: "cn" (Trung Quốc) hoặc "tw" (Đài Loan)
  }
  ```
- **Lưu ý**: Nếu muốn tìm kiếm trên **Tmall**, thay `region: "cn"` thành `region: "tw"`.

##### **B. Node "Search Taobao/Tmall Products" (Node `httpRequest`)**
- **Endpoint mặc định**:
  ```
  https://api.justoneapi.com/taobao/search
  ```
- **Headers**:
  - `Authorization`: `Bearer {{ $json["JustOneAPIKey"] }}`
  - `Content-Type`: `application/json`
- **Body**:
  ```json
  {
    "keyword": "{{ $json["searchKeyword"] }}",
    "limit": {{ $json["limit"] }},
    "region": "{{ $json["region"] }}"
  }
  ```

##### **C. Node "Fetch Product Details by ID" (Node `httpRequest`)**
- **Endpoint**:
  ```
  https://api.justoneapi.com/taobao/item/get
  ```
- **Headers**:
  - `Authorization`: `Bearer {{ $json["JustOneAPIKey"] }}`
  - `Content-Type`: `application/json`
- **Body**:
  ```json
  {
    "item_id": "{{ $json["item_id"] }}"  // ID sản phẩm được trích xuất từ node trước
  }
  ```

##### **D. Node "Build Product Detail Output" (Node `code`)**
- **Lưu ý**: Node này **không cần chỉnh sửa** vì đã cấu hình sẵn để trích xuất dữ liệu từ API.

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Chọn **Run Workflow** và nhập từ khóa (ví dụ: `iphone 15`).
   - Kiểm tra **Output** để đảm bảo dữ liệu trả về chính xác.
2. **Bật Active**:
   - Sau khi test thành công, **bật Active** để workflow chạy tự động khi kích hoạt thủ công.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::note[CÁCH THỂ HIỆN THỰC TẾ]
1. **Kết nối với Slack/Telegram**:
   - Thêm node **Slack Webhook** hoặc **Telegram Bot** để nhận thông báo khi workflow hoàn thành.
   - Ví dụ: Gửi tin nhắn như:
     ```
     📢 **Kết quả tìm kiếm "iphone 15" trên Taobao**:
     - Giá: ¥6,999
     - Stock: 123
     - Link: [Taobao Link](https://taobao.com/...)
     ```
2. **Lưu log vào Google Sheets/Excel**:
   - Thêm node **Google Sheets** để ghi dữ liệu tìm kiếm vào bảng tính.
   - Dễ dàng theo dõi lịch sử và phân tích xu hướng.
3. **Tự động hóa định kỳ**:
   - Sử dụng **n8n Cron Trigger** để chạy workflow hàng ngày/tuần (ví dụ: tìm kiếm từ khóa mới mỗi sáng).
4. **So sánh giá giữa Taobao và Tmall**:
   - Sao chép workflow và thay đổi `region` từ `cn` sang `tw` để so sánh giá trên hai nền tảng.
:::

---
### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc tìm kiếm thủ công, đồng thời **cung cấp dữ liệu chính xác** để ra quyết định kinh doanh. **Chỉ cần 5 phút setup**, bạn đã có một công cụ tự động hóa mạnh mẽ cho nghiên cứu thị trường Taobao/Tmall.

👉 **Bắt đầu ngay**:
1. Đăng ký **JustOneAPI** và lấy API Key.
2. Import workflow và điền thông tin.
3. **Kích hoạt** và bắt đầu tìm kiếm sản phẩm tự động!

---
**💡 Mẹo cuối**: Nếu muốn **tìm kiếm nhiều từ khóa cùng lúc**, các sếp có thể **sao chép workflow** và thay đổi từ khóa trong node `Set API and Search Parameters`. Hoặc sử dụng **n8n Queue** để chạy nhiều workflow song song!