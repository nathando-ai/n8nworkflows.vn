---
title: "🚀 Tự Động Hoá Scrape Dữ Liệu Bất Động Sản Idealista - Từ Danh Sách Cho Đến Chi Tiết (N8n + ScrapeGraph AI)"
description: "Workflow này tự động scrape danh sách bất động sản từ Idealista (và các trang bất động sản khác), trích xuất dữ liệu chi tiết (giá, diện tích, phòng ngủ, tiện ích...) và lưu vào Google Sheets - tiết kiệm 10+ giờ công mỗi tuần cho các sếp kinh doanh bất động sản."
slug: "tự-dộng-hoá-scrape-danh-sách-bất-dộng-sản-idealista"
tags: [n8n, automation, no-code, scrapegraph-ai, google-sheets, bất-dộng-sản, market-research]
keywords: [scrape idealista n8n, tự động hóa bất động sản, scrapegraph ai, lưu dữ liệu google sheets, danh sách nhà đất tự động]
---

# 🚀 **Scrape Dữ Liệu Bất Động Sản Idealista Tự Động - Từ Danh Sách Đến Chi Tiết**

### **Nỗi Đau Của Các Sếp Kinh Doanh Bất Động Sản**
Hàng tuần, các sếp phải:
- **Tìm kiếm thủ công** trên Idealista, Zaloan, Batdongsan.vn... để cập nhật danh sách bất động sản mới.
- **Chép tay** thông tin (giá, diện tích, phòng ngủ, tiện ích...) vào Excel/Google Sheets.
- **Lặp lại quá trình** mỗi khi có nhà đầu tư mới hoặc thị trường thay đổi.
- **Mất thời gian** lên đến **10+ giờ/tuần** cho công việc này, trong khi dữ liệu có thể được tự động hóa hoàn toàn.

**Workflow này giải quyết tất cả!** Dùng **n8n + ScrapeGraph AI**, bạn sẽ:
✅ **Scrape danh sách bất động sản** từ Idealista (hoặc bất kỳ trang bất động sản nào khác).
✅ **Trích xuất dữ liệu chi tiết** (giá, diện tích, phòng ngủ, tiện ích, hình ảnh...) bằng AI.
✅ **Lưu vào Google Sheets** với định dạng chuyên nghiệp, sẵn sàng phân tích.
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính bảo mật và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tuần**: Không cần chép tay dữ liệu nữa.
- **Dữ liệu chính xác & chi tiết**: AI trích xuất thông tin từ trang web (giá, diện tích, phòng ngủ, tiện ích, hình ảnh...).
- **Cập nhật tự động**: Hoạt động 24/7, không phụ thuộc vào thời gian làm việc.
- **Dễ dàng phân tích**: Dữ liệu được lưu vào Google Sheets với định dạng chuyên nghiệp, sẵn sàng export cho Excel/Power BI.
- **Thích ứng cao**: Chỉ cần thay đổi **URL base** và **JSON schema**, workflow có thể scrape bất kỳ trang bất động sản nào (Zaloan, Batdongsan.vn, PropertyGuru...).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản ScrapeGraph AI**:
   - Đăng ký tại [ScrapeGraph AI](https://www.scrapegraph.ai/) và lấy **API Key**.
   - **Lưu ý**: Workflow sử dụng **ScrapeGraphAI** để scrape và trích xuất dữ liệu, không phải Google Sheets.
2. **Tài khoản Google**:
   - **Google Sheets OAuth2**: Để lưu dữ liệu vào Google Sheets.
   - **Google Gemini API** (nếu muốn sử dụng AI tóm tắt dữ liệu).
3. **Google Sheet mẫu**:
   - Clone [bảng mẫu này](https://docs.google.com/spreadsheets/d/1jtMyMglBbekD9Z407q8-0vn-cDDXhM81Uj1oAZIJGX8/edit?usp=sharing) và ghi lại **Document ID** (phần cuối URL).
4. **URL trang bất động sản**:
   - Ví dụ: `https://www.idealista.it/vendita-case/verona-verona/` (đối với Idealista Italy).
   - Nếu scrape trang khác, thay đổi **base URL** và **pagination parameter** trong node **Set params**.

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/15510](https://n8n.io/workflows/15510) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/15510) và paste vào n8n Editor.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflows này gồm **2 phần chính**:
- **Phần 1**: Scrape danh sách URL của các bất động sản từ trang Idealista.
- **Phần 2**: Trích xuất dữ liệu chi tiết từ từng URL và lưu vào Google Sheets.

##### **A. Cấu Hình ScrapeGraph AI**
- **Node "Scrape listings"**:
  - Điền **API Key** của ScrapeGraph AI vào **credentials** (`scrapegraphAIApi`).
  - **URL base**: Thay đổi thành URL trang bất động sản mục tiêu (ví dụ: `https://www.idealista.it/vendita-case/verona-verona/`).
  - **Pagination parameter**: Thay đổi thành tham số phân trang của trang web (ví dụ: `page=`).

- **Node "Extract data"**:
  - Sử dụng cùng **API Key** của ScrapeGraph AI.
  - **JSON schema** đã được định sẵn để trích xuất:
    ```json
    {
      "title": "string",
      "description": "string",
      "price": "number",
      "area": "number",
      "bedrooms": "number",
      "bathrooms": "number",
      "floor": "number",
      "rooms": "number",
      "balcony": "boolean",
      "terrace": "boolean",
      "cellar": "boolean",
      "heating": "string",
      "air_conditioning": "boolean",
      "image_urls": ["string"]
    }
    ```
  - **Lưu ý**: Nếu scrape trang khác, cần **cập nhật schema** để phù hợp với cấu trúc dữ liệu của trang đó.

##### **B. Cấu Hình Google Sheets**
- **Node "Update real estate listings"**:
  - Chọn **credentials** là `googleSheetsOAuth2Api`.
  - Điền **Document ID** (từ URL Google Sheets) và **Sheet Name** (tên sheet trong bảng).
  - **Operation**: Đặt là `appendOrUpdate` để thêm hoặc cập nhật dữ liệu.
  - **Column mappings**: Đảm bảo tên cột trong Google Sheets khớp với dữ liệu trích xuất (ví dụ: `title`, `price`, `area`...).

##### **C. Cấu Hình Node "Set params"**
- **Base URL**: Thay đổi thành URL trang bất động sản mục tiêu.
- **Max pages**: Số trang muốn scrape (ví dụ: `10`).
- **Pagination parameter**: Tham số phân trang của trang web (ví dụ: `page=`).

##### **D. Node "Generate Urls" (Code)**
- Đây là node tự động tạo danh sách URL của các trang phân trang.
- **Lưu ý**: Không cần chỉnh sửa nếu sử dụng cấu trúc URL mặc định của Idealista.

---

#### **3. Kích Hoạt ⚡️**
1. **Test run dữ liệu mẫu**:
   - Chạy **Manual Trigger** và kiểm tra:
     - Danh sách URL được scrape có đầy đủ không?
     - Dữ liệu chi tiết (giá, diện tích...) có trích xuất chính xác không?
     - Dữ liệu có lưu vào Google Sheets không?
2. **Bật Active workflow**:
   - Sau khi kiểm tra thành công, bật **Active** để workflow hoạt động tự động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Lưu log hoạt động**:
   - Thêm node **Slack/Telegram** để nhận thông báo khi workflow hoàn thành hoặc gặp lỗi.
   - Ví dụ: Sau node **"Update real estate listings"**, thêm node **Slack** để gửi tin nhắn thành công.

2. **Tự động gửi báo cáo định kỳ**:
   - Sử dụng **n8n Cron Trigger** để chạy workflow hàng ngày/tuần.
   - Ví dụ: Chạy vào **7h sáng** để cập nhật dữ liệu mới nhất.

3. **Tích hợp với CRM/Email**:
   - Sau khi scrape dữ liệu, gửi **email tự động** cho nhà đầu tư với danh sách bất động sản mới.
   - Sử dụng node **Email** hoặc **Slack** để thông báo.

4. **Tối ưu tốc độ scrape**:
   - Thêm node **Wait** giữa các request để tránh bị chặn bởi trang web.
   - Cấu hình **delay** trong node **Limit** (ví dụ: `500ms` giữa các request).

5. **Chỉnh sửa JSON schema**:
   - Nếu scrape trang bất động sản khác, **cập nhật schema** trong node **"Extract data"** để trích xuất thông tin cần thiết.

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp kinh doanh bất động sản muốn:
✔ **Tiết kiệm thời gian** với việc scrape và cập nhật dữ liệu tự động.
✔ **Nhận dữ liệu chi tiết** (giá, diện tích, tiện ích...) mà không cần chép tay.
✔ **Hoạt động 24/7** mà không phụ thuộc vào thời gian làm việc.

**Hành động ngay!**
1. **Clone Google Sheet mẫu** và lấy **Document ID**.
2. **Cấu hình ScrapeGraph AI** và **Google Sheets** trong n8n.
3. **Chạy workflow** và xem dữ liệu bất động sản tự động cập nhật!

**Nếu cần hỗ trợ**, các sếp có thể liên hệ với tác giả Davide Boizza qua:
- Email: [info@n3w.it](mailto:info@n3w.it)
- LinkedIn: [@davideboizza](https://www.linkedin.com/in/davideboizza)
- YouTube: [@n3witalia](https://youtube.com/@n3witalia) (có nhiều template tự động hóa hữu ích!)

---
**Chúc các sếp thành công với việc tự động hóa scrape bất động sản!** 🚀