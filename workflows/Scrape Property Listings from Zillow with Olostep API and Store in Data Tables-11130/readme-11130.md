---
title: "🏠 Tự Động Hoàn Thành Báo Cáo Đất Đai: Scrape Dữ Liệu Bất Động Sản Zillow Và Lưu Trữ Trên Google Sheets (Không Code)"
description: "Workflow này tự động thu thập dữ liệu bất động sản từ Zillow (giá, liên kết, vị trí) bằng Olostep API, loại bỏ trùng lặp và lưu vào Google Sheets hoặc Data Table n8n. Giúp các sếp tiết kiệm 10+ giờ/tháng so sánh thị trường."
slug: "tieu-dung-san-zillow-voi-olostep-api"
tags: [n8n, automation, no-code, market-research, ai-summarization, zillow-scraper, google-sheets]
keywords: [tự động hóa n8n, scrape zillow, olostep api, lưu dữ liệu bất động sản, google sheets automation, market research tool]
---

# 🚀 **Tự Động Hoàn Thành Báo Cáo Đất Đai: Scrape Dữ Liệu Bất Động Sản Zillow Và Lưu Trữ Trên Google Sheets**

## **Nỗi Đau Của Các Sếp Trong Thị Trường Bất Động Sản**
Hàng ngày, các sếp phải **tìm kiếm thủ công** thông tin giá nhà, vị trí và liên kết Zillow cho từng dự án. Quá trình này:
✅ **Tốn thời gian**: 10+ giờ/tháng để so sánh thị trường.
✅ **Khó duy trì**: Dữ liệu không được cập nhật liên tục.
✅ **Rủi ro sai sót**: Thiếu tính chính xác khi copy/paste từ trang web.

**Workflow này giải quyết tất cả!** Nó **tự động** thu thập dữ liệu bất động sản từ Zillow, **lọc bỏ trùng lặp**, và **lưu vào Google Sheets** để phân tích dễ dàng.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tháng** so sánh thị trường.
- **Dữ liệu chính xác 100%**: Không sai sót khi copy/paste.
- **Cập nhật tự động**: Khi có thay đổi giá, hệ thống sẽ cập nhật ngay.
- **Dễ dàng phân tích**: Dữ liệu được lưu vào Google Sheets với định dạng sẵn sàng export.
- **Không cần code**: Sử dụng API Olostep để scrape Zillow **không cần browser automation**.
:::

---
### **🔧 Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần:
1. **Tài khoản Olostep API** (đăng ký tại [olostep.com](https://olostep.com/)) và **API Key**.
2. **Google Sheets** (hoặc **Data Table n8n**) để lưu trữ kết quả.
3. **n8n Self-hosted** (không dùng phiên bản miễn phí).
:::

---
### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/11130](https://n8n.io/workflows/11130) hoặc copy/paste JSON vào **n8n Editor**.
- **Nhấn "Import"** và chọn **Self-hosted n8n**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow gồm **8 node** chính, nhưng các sếp cần chú ý đến:

##### **🔹 Node "On form submission" (Form Trigger)**
- **Cấu hình**:
  - Thêm **form** với trường nhập **location** (ví dụ: *"Manhattan New York NY"*).
  - **Lưu ý**: Form này sẽ tạo URL Zillow tự động khi người dùng nhập địa chỉ.

##### **🔹 Node "scrape places" (HTTP Request)**
- **Tham số cần điền**:
  - **URL**: `https://api.olostep.com/v1/extract?url=https://www.zillow.com/homes/for_sale/{location}/r_pick?searchQueryState=%7B%22pagination%22%3A%7B%22currentPage%22%3A{page}%7D%7D`
  - **Headers**:
    - `Authorization: Bearer {OLOSTEP_API_KEY}`
    - `Content-Type: application/json`
  - **Body**:
    ```json
    {
      "schema": {
        "price": "string",
        "url": "string",
        "location": "string"
      }
    }
    ```
  - **Lưu ý**:
    - Thay `{location}` và `{page}` bằng biến từ **Form Trigger** và **Pagination**.
    - Nếu gặp **timeout 504**, xóa toàn bộ `schema` trong `llm_extract` và sử dụng **node Information Extractor** thay thế.

##### **🔹 Node "Insert row" (Data Table / Google Sheets)**
- **Chọn credentials**:
  - Nếu dùng **Google Sheets**, chọn **Google Sheets** và kết nối tài khoản.
  - Nếu dùng **Data Table n8n**, chọn **n8n Data Table** và tạo bảng mới.
- **Cấu hình cột**:
  - Đảm bảo cột `price`, `url`, `location` tồn tại trong bảng.

##### **🔹 Node "Loop Over Items" (Split In Batches)**
- **Tham số mặc định** đã đủ, không cần chỉnh sửa.

---
#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhập **location** vào form (ví dụ: *"Ho Chi Minh City"*).
   - Chạy **manual test** để kiểm tra dữ liệu scrape.
2. **Bật Active**:
   - Đánh dấu **Active** và lưu workflow.

---
### **✍️ Mẹo & Gợi Ý Nâng Cao**
:::tip[CÁCH LÀM HƠN]
1. **Gửi báo cáo định kỳ**:
   - Sử dụng **node Email** hoặc **Slack** để gửi báo cáo hàng tuần.
   - Ví dụ: *"Dữ liệu mới cập nhật từ Zillow: [link Google Sheets]"*.

2. **Lưu log scrape**:
   - Thêm **node Sticky Note** để ghi lại thời gian scrape và status.

3. **Kết hợp với AI**:
   - Sử dụng **node LLM** để **tóm tắt thị trường** từ dữ liệu scrape.

4. **Tự động cập nhật giá**:
   - Sử dụng **node Schedule** để chạy workflow hàng ngày.
:::

---
### **📌 Kết Luận**
Workflow này **giúp các sếp tự động hóa việc thu thập dữ liệu bất động sản**, tiết kiệm thời gian và **cập nhật thị trường một cách chính xác**. **Không cần code**, chỉ cần **Olostep API + Google Sheets**, bạn đã có một **công cụ market research mạnh mẽ**.

**🚀 Hãy áp dụng ngay và bắt đầu scrape Zillow trong 5 phút!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::