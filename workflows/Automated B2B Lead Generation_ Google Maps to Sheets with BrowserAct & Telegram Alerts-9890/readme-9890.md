---
title: "🚀 Tự Động Hóa Sinh Lập Lead B2B Từ Google Maps Sang Google Sheets Với BrowserAct & Thông Báo Telegram Thực Tế"
description: "Workflow này tự động hóa việc tìm kiếm và thu thập thông tin doanh nghiệp địa phương từ Google Maps, lưu trữ vào Google Sheets và gửi thông báo Telegram ngay lập tức. Giúp các sếp tiết kiệm thời gian lên tới 10 giờ/tuần và giảm thiểu sai sót trong quá trình thu thập lead."
slug: "tu-dong-hoa-lead-b2b-googlemaps-sang-google-sheets"
tags: [n8n, automation, lead-generation, browseract, google-maps-scraping, telegram-notification]
keywords: [n8n workflow lead generation, tự động hóa tìm kiếm lead B2B, Google Maps scraping, lưu lead vào Google Sheets, thông báo Telegram tự động]
---

# 🚀 **Tự Động Hóa Sinh Lập Lead B2B Từ Google Maps Sang Google Sheets Với BrowserAct & Telegram**

### **Giải Pháp Cho Các Sếp Bán Hàng & Marketing**
Bạn đã bao giờ phải tốn thời gian vô cùng để tìm kiếm và thu thập thông tin các cửa hàng, dịch vụ địa phương từ Google Maps? Hay phải mất nhiều giờ để nhập liệu vào Google Sheets hoặc CRM? **Workflow này sẽ tự động hóa toàn bộ quá trình đó chỉ trong vài giây!**

Với công nghệ **BrowserAct** kết hợp **n8n**, bạn có thể:
- **Scrape** thông tin doanh nghiệp từ Google Maps theo khu vực và ngành nghề cụ thể.
- **Lưu trữ** lead vào Google Sheets **không trùng lặp**.
- **Nhận thông báo Telegram** ngay khi có lead mới, giúp bạn phản hồi nhanh chóng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Thu thập lead từ Google Maps chỉ trong vài giây thay vì nhiều giờ thủ công.
- **Dữ liệu chính xác**: Không sai sót do nhập liệu tay, tránh trùng lặp lead.
- **Thông báo tức thời**: Nhận thông báo Telegram ngay khi có lead mới, phản hồi nhanh chóng với khách hàng tiềm năng.
- **Hoạt động liên tục**: Sử dụng **Cron Node** để chạy tự động hàng ngày, tuần hoặc tháng.
- **Tích hợp dễ dàng**: Kết nối với Google Sheets và Telegram một cách đơn giản.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản BrowserAct**:
   - Đăng ký tại [BrowserAct](https://www.browseract.com/) và tạo **API Key**.
   - Cài đặt **Template “Google Maps Local Lead Finder”** trong tài khoản BrowserAct.
2. **Tài khoản Google Sheets**:
   - Tạo một **Google Sheet** để lưu lead (các sếp có thể tạo một sheet mới hoặc chọn sheet đã có).
   - Cấu hình **OAuth 2.0** cho Google Sheets trong n8n.
3. **Tài khoản Telegram**:
   - Tạo một **chatbot Telegram** hoặc sử dụng chat cá nhân.
   - Lấy **Chat ID** của bot/chat để nhận thông báo.
4. **n8n Workflow**:
   - Cài đặt **n8n Self-hosted** (nên sử dụng VPS để lưu trữ ổn định).
   - Cài đặt **BrowserAct Node** cho n8n (tải từ [n8n Community](https://community.n8n.io/)).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Truy cập [n8n Editor](https://n8n.io/editor).
2. Nhấp vào **"Import"** và chọn file JSON từ [link gốc](https://n8n.io/workflows/9890).
   *Hoặc* copy toàn bộ JSON từ [đây](https://n8n.io/workflows/9890) và dán vào **"Import from JSON"**.
3. Sau khi import, workflow sẽ hiển thị trên canvas.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **6 node chính**, các sếp cần chú ý cấu hình như sau:

##### **🔹 Node 1: Manual Trigger (Bắt Đầu Tự Động)**
- **Chức năng**: Khởi động workflow thủ công (hoặc sau này thay thế bằng **Cron Node**).
- **Lưu ý**: Nếu muốn chạy tự động, các sếp cần thêm **Cron Node** và cấu hình lịch chạy (ví dụ: hàng ngày lúc 8h sáng).

##### **🔹 Node 2 & 3: BrowserAct (Scrape Google Maps)**
- **Node 2: Run a workflow task**
  - **Cấu hình**:
    - **Credentials**: Chọn `browserActApi` (đã cấu hình trước).
    - **Parameters**:
      - `Location`: Điền **khu vực** bạn muốn scrape (ví dụ: "Brooklyn, New York").
      - `Business_Category`: Điền **ngành nghề** (ví dụ: "Baby Care", "Café", "Phòng khám").
      - `Extracted_Data`: Số lượng lead muốn scrape (ví dụ: `100`).
      - `Template_ID`: Điền **ID của template “Google Maps Local Lead Finder”** (tìm trong BrowserAct).
  - **Lưu ý**: Các sếp có thể thay đổi `Location` và `Business_Category` để scrape lead theo nhu cầu.

- **Node 3: Get details of a workflow task**
  - **Chức năng**: Chờ scraping hoàn tất trước khi xử lý tiếp.
  - **Lưu ý**: Node này **không cần cấu hình thêm**, chỉ cần để mặc định.

##### **🔹 Node 4: Code (JavaScript) – Parse & Split Data**
- **Chức năng**: Chuyển dữ liệu thô từ BrowserAct thành format n8n có thể xử lý (mỗi lead là một item riêng).
- **Lưu ý**:
  - **Không cần chỉnh sửa** nếu các sếp sử dụng template đã có sẵn.
  - Nếu muốn thay đổi logic, các sếp có thể mở node này và xem mã JavaScript:
    ```javascript
    // Dữ liệu đầu vào từ BrowserAct (dạng text thô)
    const rawData = $input.all();
    const businesses = rawData[0].json.output.split("\n").filter(item => item.trim().length > 0);

    // Tạo danh sách lead riêng lẻ
    const leads = businesses.map(business => ({
      Name: business.split("|")[0].trim(),
      Address: business.split("|")[1].trim(),
      Phone: business.split("|")[2].trim(),
      Rating: business.split("|")[3]?.trim() || "N/A",
      Category: business.split("|")[4]?.trim() || "N/A"
    }));

    // Trả về danh sách lead cho node tiếp theo
    return leads.map(lead => ({
      json: { lead }
    }));
    ```
  - **Cách sửa**: Nếu dữ liệu từ BrowserAct có định dạng khác, các sếp cần chỉnh sửa mã để phù hợp.

##### **🔹 Node 5: Google Sheets (Lưu Lead)**
- **Cấu hình**:
  - **Credentials**: Chọn `googleSheetsOAuth2Api` (đã cấu hình trước).
  - **Parameters**:
    - **Sheet Name**: Điền tên **tab** trong Google Sheet (ví dụ: "Leads").
    - **Range**: Điền `A1` (nếu sheet trống) hoặc `A2:A` (nếu đã có header).
    - **Operation**: Chọn `appendOrUpdate` (tránh trùng lặp).
  - **Lưu ý**:
    - Các sếp cần **tạo một sheet mới** hoặc chọn sheet đã có.
    - **Header** trong sheet phải khớp với trường dữ liệu từ BrowserAct (ví dụ: `Name`, `Address`, `Phone`, `Rating`, `Category`).

##### **🔹 Node 6: Telegram (Thông Báo Lead Mới)**
- **Cấu hình**:
  - **Credentials**: Chọn `telegramApi` (đã cấu hình trước).
  - **Parameters**:
    - **Chat ID**: Điền **Chat ID** của bot/chat Telegram (các sếp có thể lấy bằng cách gửi tin nhắn cho bot `@getidsbot`).
    - **Message**: Thay đổi nội dung thông báo (ví dụ: `🚀 Lead mới từ ${location}: ${lead.Name}`).
  - **Lưu ý**:
    - Nếu muốn gửi **hình ảnh** hoặc **file**, các sếp cần thêm node **Set** trước để định dạng dữ liệu.
    - Ví dụ thông báo mẫu:
      ```
      🚀 **Lead mới từ Brooklyn!**
      Tên: [Tên Doanh Nghiệp]
      Địa chỉ: [Địa chỉ]
      Điện thoại: [Số điện thoại]
      Đánh giá: [Sao]
      ```

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhấp vào **"Execute Workflow"** để chạy thử.
   - Kiểm tra **Google Sheets** và **Telegram** để xác nhận lead đã được lưu và thông báo.
2. **Bật Active**:
   - Sau khi kiểm tra thành công, các sếp có thể **bật workflow** để hoạt động liên tục.
   - **Nếu muốn tự động hóa**:
     - Thêm **Cron Node** vào đầu workflow.
     - Cấu hình lịch chạy (ví dụ: `0 8 * * *` để chạy hàng ngày lúc 8h).

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tự Động Hóa Hàng Ngày**:
   - Thay thế **Manual Trigger** bằng **Cron Node** để chạy workflow theo lịch (ví dụ: hàng tuần để cập nhật lead mới).
   - Cấu hình trong **Cron Node**:
     ```
     0 8 * * 1-5  # Chạy từ thứ 2 đến thứ 6 lúc 8h sáng
     ```

2. **Lưu Log & Theo Dõi**:
   - Thêm **Set Node** trước **Telegram Node** để lưu thông tin lead vào **Google Sheets Log** (để theo dõi lịch sử).
   - Ví dụ:
     ```json
     {
       "json": {
         "timestamp": $datetime.now(),
         "lead": $input.all()[0].json.lead,
         "status": "success"
       }
     }
     ```

3. **Kết Hợp Với Slack**:
   - Thay vì Telegram, các sếp có thể sử dụng **Slack Node** để thông báo lead qua Slack.
   - Cấu hình trong **Slack Node**:
     - **Credentials**: `slackApi`.
     - **Channel**: `#leads`.
     - **Message**: `📌 Lead mới: ${lead.Name}`.

4. **Lọc Lead Theo Đánh Giá**:
   - Sử dụng **Code Node** để lọc chỉ lead có **đánh giá ≥ 4 sao** trước khi lưu vào Google Sheets.
   - Mã ví dụ:
     ```javascript
     const leads = $input.all().map(item => item.json.lead);
     const highRatingLeads = leads.filter(lead => lead.Rating >= 4);

     return highRatingLeads.map(lead => ({
       json: { lead }
     }));
     ```

5. **Gửi Email Cho Lead**:
   - Thêm **Email Node** (ví dụ: Gmail) để tự động gửi email chào hàng cho lead mới.
   - Cấu hình trong **Email Node**:
     - **To**: `$input.all()[0].json.lead.Phone` (hoặc email nếu có).
     - **Subject**: `Xin chào từ [Tên Doanh Nghiệp]!`.
     - **Body**: `Thông tin chi tiết về dịch vụ của chúng tôi...`.

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp bán hàng, marketing hoặc doanh nghiệp cần tự động hóa việc thu thập lead từ Google Maps. Với **BrowserAct + n8n + Telegram**, bạn không chỉ tiết kiệm thời gian mà còn **tăng cường hiệu quả bán hàng** bằng cách phản hồi lead ngay lập tức.

**Hành động ngay hôm nay!**
1. **Cài đặt n8n Self-hosted** trên VPS (nên chọn TinoHost hoặc BNIX với mã giảm giá).
2. **Cấu hình BrowserAct, Google Sheets và Telegram**.
3. **Import workflow** và chạy thử.
4. **Thay thế Manual Trigger bằng Cron Node** để tự động hóa.

**Nếu gặp khó khăn**, các sếp có thể tham khảo:
- [BrowserAct Discord](https://discord.com/invite/UpnCKd7GaU)
- [Blog BrowserAct](https://www.browseract.com/blog)
- [Video hướng dẫn](https://youtu.be/--hqPhb83kg)

**Chúc các sếp thành công với việc tự động hóa lead generation!** 🚀