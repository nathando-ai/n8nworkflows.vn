---
title: "🚀 Tự Động Hóa Scrape Dữ Liệu Google Maps Sang Google Sheets - Giúp Các Sếp Tiết Kiệm 100+ Giờ/Năm"
description: "Workflow này tự động scrape thông tin doanh nghiệp từ Google Maps (restaurants, dịch vụ địa phương...) và cập nhật trực tiếp vào Google Sheets, giúp các sếp quản lý leads hiệu quả mà không cần code. Giảm thiểu công việc thủ công, tăng cường phân tích thị trường và tối ưu hóa chiến dịch marketing."
slug: "tieu-dong-hoa-scrape-google-maps-sang-google-sheets"
tags: [n8n, automation, lead-generation, google-maps, google-sheets, apify, no-code]
keywords: [tự động hóa scrape google maps, scrape dữ liệu địa phương, tự động hóa leads, google sheets tự động cập nhật, apify n8n, tự động hóa marketing địa phương]
---

# 🚀 **Scrape Dữ Liệu Google Maps Sang Google Sheets - Giải Pháp Tự Động Hóa Cho Các Sếp Quản Lý Leads**

### **Nỗi Đau Của Các Sếp Hiện Nay**
Các sếp trong lĩnh vực marketing, bán hàng hoặc kinh doanh dịch vụ địa phương thường phải **tốn thời gian quét thủ công** thông tin doanh nghiệp từ Google Maps để xây dựng danh sách leads. Những công việc như:
- Tìm kiếm và ghi chép tên cửa hàng, địa chỉ, số điện thoại, website...
- Cập nhật dữ liệu vào Google Sheets hoặc Excel để phân tích.
- Lặp lại quá trình này hàng tuần/mỗi tháng để cập nhật thông tin mới.

**Kết quả?** Thời gian và năng suất bị "chôn vùi" trong công việc thủ công, trong khi dữ liệu không được cập nhật kịp thời, làm giảm hiệu quả chiến dịch marketing và bán hàng.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
Sau khi áp dụng workflow này, các sếp sẽ:
✅ **Tiết kiệm 100+ giờ/năm** bằng cách loại bỏ công việc scrape thủ công.
✅ **Cập nhật dữ liệu tự động** mỗi khi có thay đổi trên Google Maps (ví dụ: mở cửa hàng mới, thay đổi thông tin).
✅ **Tạo danh sách leads sạch và chi tiết** với các trường dữ liệu quan trọng:
   - Tên doanh nghiệp
   - Địa chỉ (đường, mã bưu chính, thành phố)
   - Website
   - Số điện thoại
✅ **Dễ dàng phân tích và export** dữ liệu để gửi email, gọi điện hoặc phân loại leads.
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.

---
### **🔧 Yêu Cầu Cần Thiết**
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Apify** (miễn phí):
   - Đăng ký tại [Apify](https://apify.com/) và tạo API Key.
   - Cài đặt **Apify Node** trong n8n (tải từ [n8n Community](https://flows.n8n.io/)).
2. **Tài khoản Google** (để kết nối với Google Sheets):
   - Cài đặt **Google Sheets Node** trong n8n.
   - Chia sẻ Google Sheet với n8n để có quyền ghi dữ liệu.
3. **Google Sheet sẵn sàng**:
   - Tạo một Sheet mới với các cột có tên **khớp với dữ liệu scrape**:
     - `Title` (Tên doanh nghiệp)
     - `Street` (Đường)
     - `Postcode` (Mã bưu chính)
     - `City` (Thành phố)
     - `Website`
     - `Phone`
4. **Từ khóa tìm kiếm Google Maps**:
   - Ví dụ: "restaurants in North Holland", "café near me", "service center [tên thành phố]".

---
### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n Community](https://n8n.io/workflows/6634) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ link trên và paste vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
##### **A. Cấu Hình Node "Run Apify Scraper"**
- **Bước 1**: Tạo **Task mới** trên Apify với từ khóa tìm kiếm (ví dụ: "restaurants in Hanoi").
  - Mô tả Task: `Scrape restaurants in Hanoi for lead generation`.
  - Chọn **Actor**: `Google Maps Scraper` (tìm kiếm trên Apify Marketplace).
- **Bước 2**: Trong node **"Run task"** của n8n:
  - Điền **Actor ID** (tìm trong URL của Actor trên Apify).
  - Chọn **Task ID** vừa tạo (hoặc để trống để tạo mới mỗi lần chạy).
  - Thêm **parameters** (nếu cần):
    ```json
    {
      "searchTerm": "restaurants in Hanoi",
      "maxItems": 100
    }
    ```

##### **Bước 3: Cấu Hình Node "Get Last Run"**
- Trong node này, chọn **Actor ID** của `Google Maps Scraper` (đã cấu hình ở trên).
- **Lưu ý**: Nếu chạy nhiều Task, hãy đảm bảo **`$json.defaultDatasetId`** trong node tiếp theo trỏ đến Dataset chính xác.

##### **Bước 4: Cấu Hình Node "Get Dataset Items"**
- Sử dụng **`$json.defaultDatasetId`** để lấy Dataset từ Task vừa chạy.
- **Lưu ý**: Nếu Dataset chưa tạo, hãy chờ Task hoàn tất (thời gian wait mặc định là 30 giây, có thể tăng lên 120 giây nếu cần).

##### **Bước 5: Kết Nối Google Sheets**
- Trong node **"Append row in sheet"**:
  - Chọn **Google Sheets OAuth2 API** đã cấu hình.
  - Chọn **Spreadsheet ID** (tìm trong URL của Sheet).
  - Chọn **Sheet Name** (ví dụ: `Leads`).
  - **Mapping dữ liệu**: Đảm bảo các cột trong Sheet khớp với trường dữ liệu từ Apify:
    ```
    Title → Tên doanh nghiệp
    Street → Đường
    Postcode → Mã bưu chính
    City → Thành phố
    Website → Website
    Phone → Số điện thoại
    ```

##### **Bước 6: Thiết Lập Node "Wait"**
- Thời gian wait mặc định là 30 giây. **Nếu Task Apify chạy lâu**, tăng thời gian lên **120 giây** để đảm bảo Dataset được tạo hoàn chỉnh.

##### **Bước 7: Manual Trigger**
- Node này dùng để **bắt đầu workflow thủ công**. Các sếp có thể thay thế bằng:
  - **Schedule Trigger** (chạy định kỳ hàng tuần).
  - **Webhook** (kích hoạt từ ứng dụng khác).

---
#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Chạy workflow với **dữ liệu mẫu** (ví dụ: từ khóa "café in Da Nang").
  - Kiểm tra Google Sheet có nhận được dữ liệu không.
- **Bật Active**:
  - Sau khi kiểm tra thành công, bật **Active** để workflow chạy tự động.

---
### **✍️ Mẹo & Gợi Ý Nâng Cao**
1. **Tự Động Hóa Hàng Tuần**:
   - Thay thế **Manual Trigger** bằng **Schedule Trigger** để chạy workflow hàng tuần (ví dụ: Chủ Nhật 8h sáng).
2. **Lưu Log & Gửi Báo Cáo**:
   - Thêm node **Slack/Email** để thông báo khi workflow hoàn tất hoặc có lỗi.
   - Ví dụ: Gửi email báo cáo số lượng leads mới được scrape.
3. **Lọc & Xử Lý Dữ Liệu**:
   - Sử dụng **Function Node** để lọc dữ liệu (ví dụ: bỏ qua doanh nghiệp đã có trong Sheet).
4. **Kết Hợp Với CRM**:
   - Sau khi scrape, đẩy dữ liệu vào **HubSpot, Zoho CRM** hoặc **Airtable** để quản lý leads.
5. **Tăng Cường Từ Khóa**:
   - Chạy nhiều Task với các từ khóa khác nhau (ví dụ: "restaurants", "café", "service center") và gộp vào một Sheet duy nhất.

---
### **📌 Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa việc scrape dữ liệu Google Maps sang Google Sheets, tiết kiệm thời gian và nâng cao hiệu quả marketing. **Không cần code**, chỉ cần cấu hình vài bước đơn giản là có thể bắt đầu sử dụng ngay!

**Hành động ngay**:
1. **Cài đặt n8n Self-hosted** trên VPS để workflow chạy 24/7 (không phụ thuộc vào n8n.cloud).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
2. **Import workflow** và bắt đầu scrape dữ liệu từ hôm nay!
3. **Mở rộng** bằng cách kết hợp với Slack, CRM hoặc hệ thống báo cáo tự động.

**Cần hỗ trợ?** Liên hệ với đội ngũ chuyên gia tại [Bedrijfautomatiseren.nl](mailto:info@bedrijfautomatiseren.nl) (đối tác chia sẻ workflow này).

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đảm bảo tốc độ và ổn định).
:::