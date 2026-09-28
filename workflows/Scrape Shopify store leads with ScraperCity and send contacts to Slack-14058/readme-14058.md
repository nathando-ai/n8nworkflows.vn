---
title: "🚀 Tự Động Hóa Scrape Dữ Liệu Shopify & Gửi Lead Tới Slack Với ScraperCity (Không Code)"
description: "Workflow tự động hóa scrape dữ liệu từ các cửa hàng Shopify trên toàn cầu, loại bỏ lead trùng lặp và gửi kết quả trực tiếp tới Slack. Giúp các sếp tiết kiệm thời gian tìm kiếm lead B2B chất lượng, hoạt động 24/7 mà không cần viết code."
slug: "tieu-dong-hoa-scrape-shopify-va-gui-lead-toi-slack"
tags: [n8n, automation, lead-generation, scraping, slack-integration]
keywords: [n8n workflow scrape shopify, tự động hóa lead generation, scrape dữ liệu Shopify, gửi lead tới Slack, ScraperCity API]
---

# 🚀 **Scrape Dữ Liệu Shopify & Gửi Lead Tới Slack Với ScraperCity (Không Code)**

### **Giải pháp tự động hóa tìm kiếm lead B2B từ Shopify, loại bỏ trùng lặp và gửi kết quả tới Slack**
Hiện nay, việc tìm kiếm lead B2B từ các cửa hàng Shopify thủ công là một quá trình tốn thời gian, phức tạp và dễ bị bỏ lỡ. Các sếp phải tra cứu từng trang web, sao chép thông tin, và kiểm tra trùng lặp thủ công—điều này không chỉ tốn nhiều thời gian mà còn dễ gây sai sót.

**Workflow này giải quyết vấn đề đó bằng cách:**
✅ **Scrape tự động** dữ liệu từ Shopify theo các tiêu chí cụ thể (nước, số lượng lead, email, ...).
✅ **Lọc bỏ lead trùng lặp** để đảm bảo tính chính xác.
✅ **Gửi kết quả trực tiếp tới Slack** để các sếp theo dõi và hành động ngay lập tức.
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần tra cứu thủ công trên hàng ngàn cửa hàng Shopify.
- **Dữ liệu chính xác**: Loại bỏ lead trùng lặp tự động, giảm sai sót.
- **Cá nhân hóa**: Chỉnh sửa tiêu chí scrape (nước, số lượng lead, email) theo nhu cầu.
- **Hoạt động liên tục**: Workflow chạy tự động mỗi khi kích hoạt, không cần can thiệp.
- **Tích hợp Slack**: Nhận thông báo lead mới ngay trên kênh Slack, không bỏ lỡ cơ hội.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản ScraperCity**:
   - Đăng ký tại [ScraperCity](https://scrapercity.com/) và lấy **API Key** từ Dashboard.
2. **Tài khoản Slack**:
   - Tạo **OAuth Token** cho n8n (cách hướng dẫn [đây](https://api.slack.com/docs/oauth-test-tokens)).
3. **Tham số scrape**:
   - **Platform**: `shopify` (đã cấu hình sẵn).
   - **CountryCode**: Ví dụ `US`, `VN`, `DE` (mỗi nước có mã riêng).
   - **TotalLeads**: Số lượng lead muốn scrape (tối đa 1000 lead/một lần).
   - **IncludeEmails**: `true` (nếu muốn scrape email) hoặc `false`.

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/14058](https://n8n.io/workflows/14058) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/14058) và dán vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này gồm **12 node**, nhưng các bước quan trọng nhất cần chú ý:

##### **A. Cấu hình ScraperCity API**
- **Node "Start Shopify Lead Scrape"** (HTTP Request):
  - **Credentials**: Chọn **HTTP Header Auth** và điền **API Key** từ ScraperCity.
  - **Headers**:
    ```
    Authorization: Bearer [API_KEY_CỦA_BẠN]
    Content-Type: application/json
    ```
  - **Body**:
    ```json
    {
      "platform": "shopify",
      "countryCode": "US",  // Thay đổi theo nhu cầu (US, VN, DE,...)
      "totalLeads": 100,    // Số lượng lead scrape
      "includeEmails": true // true/false
    }
    ```

- **Node "Check Scrape Status"** (HTTP Request):
  - Sử dụng cùng **credentials** và **headers** như trên.
  - **URL**: `https://api.scrapercity.com/v1/jobs/{runId}/status` (được tự động lấy từ node "Store Run ID").

##### **B. Cấu hình Slack**
- **Node "Post Lead to Slack"** (Slack):
  - Chọn **OAuth Token** đã tạo trước đó.
  - **Channel**: Điền tên kênh Slack (ví dụ `#leads-shopify`).
  - **Message Format**: Workflow đã cấu hình sẵn để gửi lead dưới dạng card Slack với thông tin:
    ```
    Name: [Tên cửa hàng]
    Email: [Email] (nếu có)
    Website: [Link Shopify]
    ```

##### **C. Cấu hình "Configure Search Parameters" (Set)**
- Mở node này và chỉnh sửa:
  - `platform`: `shopify` (không thay đổi).
  - `countryCode`: Thay đổi theo nước muốn scrape (ví dụ `VN` cho Việt Nam).
  - `totalLeads`: Số lead muốn scrape (tối đa 1000).
  - `includeEmails`: `true` (nếu muốn scrape email).

##### **D. Cấu hình "Store Run ID" (Set)**
- Đảm bảo `slackChannel` trùng với tên kênh Slack đã cấu hình ở trên.

##### **E. Thời gian chờ (Wait 60 Seconds)**
- Workflow sẽ **polling** (kiểm tra trạng thái scrape) mỗi **60 giây**.
  - **Nếu muốn nhanh hơn**: Thay đổi thành `30` giây (nhưng có thể tăng tải server).
  - **Nếu muốn chậm hơn**: Thay thành `120` giây.

---

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Chọn **Execute Workflow** và chạy thử với số lượng lead nhỏ (ví dụ `10`).
   - Kiểm tra Slack xem có nhận được lead không.
2. **Bật Active**:
   - Sau khi kiểm tra thành công, chuyển workflow sang **Active**.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tích hợp với CRM**:
   - Sau khi scrape, có thể gửi lead tới **Zapier**, **Make (Integromat)**, hoặc **HubSpot** bằng cách thêm node **HTTP Request** hoặc **Zapier Webhook**.

2. **Lưu log scrape**:
   - Thêm node **Google Sheets** hoặc **Airtable** để lưu tất cả lead scrape vào bảng dữ liệu.

3. **Gửi báo cáo định kỳ**:
   - Sử dụng node **Set** + **Schedule Trigger** để chạy scrape hàng tuần/tháng và gửi báo cáo tới Slack.

4. **Scrape nhiều nước cùng lúc**:
   - Sử dụng node **Split in Batches** để chạy scrape cho nhiều `countryCode` khác nhau song song.

5. **Tự động filter lead**:
   - Trong node **Code** (Parse CSV), có thể thêm logic filter lead theo tiêu chí (ví dụ: loại bỏ lead có revenue < 1M USD).

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp cần scrape lead B2B từ Shopify một cách tự động, chính xác và không cần viết code. Bằng cách cấu hình đơn giản, các sếp có thể:
✔ **Tiết kiệm hàng giờ** tra cứu lead thủ công.
✔ **Nhận lead mới ngay trên Slack**, không bỏ lỡ cơ hội.
✔ **Cá nhân hóa** scrape theo nhu cầu (nước, số lượng, email).

**Hành động ngay!**
1. Import workflow và cấu hình theo hướng dẫn.
2. Chạy test với số lượng lead nhỏ.
3. Bật **Active** và bắt đầu tự động hóa lead generation!

---
**Cần hỗ trợ?** Đăng ký VPS n8n tại [TinoHost](https://tino.vn/vps-n8n?affid=388) với mã giảm giá **VPSN8N** để workflow chạy ổn định 24/7! 🚀