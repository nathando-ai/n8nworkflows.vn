---
title: "🔍 Tự Động Hóa Khám Phá Profile LinkedIn Theo Vai Trò - OSINT & Red Teaming Cho Doanh Nghiệp"
description: "Workflow tự động hóa khám phá thông tin chuyên gia LinkedIn theo vai trò công việc, kết hợp với Google Search API để thu thập dữ liệu OSINT (Open-Source Intelligence) và hỗ trợ cho các đội ngũ Red Teaming. Giúp các sếp tiết kiệm thời gian lên tới 80% trong việc tìm kiếm và phân tích thông tin nhân sự."
slug: "tieu-dong-hoa-kham-pha-profile-linkedin-theo-vai-tro"
tags: [n8n, automation, lead-generation, osint, red-teaming, google-search-api, google-sheets]
keywords: [tự động hóa n8n, tìm kiếm nhân sự LinkedIn, OSINT, red teaming, google search api, google sheets automation]
---

# 🚀 Tự Động Hóa Khám Phá Profile LinkedIn Theo Vai Trò - Giải Pháp OSINT & Red Teaming Cho Doanh Nghiệp

### **📌 Nỗi Đau Của Các Sếp Trong Tìm Kiếm Thông Tin Nhân Sự**
Bạn có bao giờ phải mất hàng giờ, thậm chí cả ngày để tìm kiếm và phân tích thông tin về các chuyên gia trong ngành, đối thủ cạnh tranh, hay các nhân sự có vai trò quan trọng trên LinkedIn? Thông tin này thường được sử dụng để:
- **Lead Generation**: Tìm kiếm các nhà quyết định (Decision-Makers) trong các công ty mục tiêu.
- **Threat Intelligence**: Phân tích các chuyên gia có khả năng gây nguy hiểm cho doanh nghiệp (Red Teaming).
- **OSINT (Open-Source Intelligence)**: Thu thập thông tin công khai để hỗ trợ các hoạt động an ninh mạng hoặc nghiên cứu thị trường.

Với việc làm thủ công, không chỉ tốn thời gian mà còn dễ bị bỏ lỡ thông tin quan trọng, và kết quả thường không được chính xác hoặc cập nhật kịp thời. **Workflow này sẽ tự động hóa toàn bộ quá trình, giúp các sếp tiết kiệm thời gian và nâng cao hiệu quả công việc.**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động ổn định 24/7, các sếp nên cài đặt n8n trên một VPS riêng (Self-hosted) để đảm bảo tính riêng tư và hiệu suất tối ưu.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 Kết Quả Các Sếp Nhận Được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa việc tìm kiếm và phân tích thông tin LinkedIn, giảm thiểu công việc thủ công lên tới **80%**.
- **Chính xác và toàn diện**: Sử dụng Google Search API để thu thập thông tin từ nhiều nguồn khác nhau, không chỉ giới hạn ở LinkedIn.
- **Cập nhật liên tục**: Workflow có thể được kích hoạt định kỳ hoặc thủ công để thu thập thông tin mới nhất.
- **Hỗ trợ Red Teaming**: Dữ liệu thu thập được lưu vào Google Sheets, giúp các đội ngũ an ninh mạng phân tích và đánh giá rủi ro từ các chuyên gia có khả năng gây nguy hiểm.
- **Tích hợp dễ dàng**: Kết quả được lưu vào Google Sheets, thuận tiện cho việc phân tích và báo cáo.
:::

---

### 🔧 Yêu Cầu Cần Thiết
:::info[CHUẨN BỊ]
Để workflow này hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Google**: Để sử dụng Google Sheets và Google Search API.
   - **Google Sheets**: Tạo một bảng mới với tên **RedOps_Targets** (hoặc tùy chỉnh theo yêu cầu).
   - **Google Search API**: Đăng ký API key tại [Google Cloud Console](https://console.cloud.google.com/) và kích hoạt dịch vụ **Custom Search JSON API**.
2. **Tài khoản LinkedIn**: Không cần API key, nhưng các sếp cần có tài khoản LinkedIn để truy cập thông tin công khai.
3. **Thông tin tìm kiếm**: Danh sách các từ khóa hoặc vai trò công việc (ví dụ: "Chief Technology Officer", "Security Architect", "Product Manager") để tìm kiếm trên LinkedIn.
:::

---

### 🚀 Cách Import & Lưu Ý Khi "Lên Đồ"

#### 1. Import Workflow 📥
Các sếp có thể import workflow này bằng hai cách:
- **Tải file JSON**: Tải workflow từ [n8n.io](https://n8n.io/workflows/6508) và import vào n8n Editor.
- **Copy/Paste JSON**: Sao chép mã JSON từ file và dán vào n8n Editor để tạo workflow mới.

#### 2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌
Sau khi import, các sếp cần cấu hình các node quan trọng như sau:

##### **🔹 Node "⚡ Trigger SocialGraph" (Manual Trigger)**
- **Mục đích**: Kích hoạt workflow thủ công.
- **Lưu ý**: Đảm bảo node này được kết nối với node tiếp theo ("🧠 Set Search Queries").

##### **🔹 Node "🧠 Set Search Queries" (Set)**
- **Mục đích**: Đặt các từ khóa tìm kiếm (ví dụ: "Chief Technology Officer", "Security Architect").
- **Cấu hình**:
  - Thêm các giá trị vào trường `json` dưới dạng mảng JSON:
    ```json
    [
      "Chief Technology Officer",
      "Security Architect",
      "Product Manager",
      "Cybersecurity Analyst"
    ]
    ```
  - Các sếp có thể tùy chỉnh danh sách này theo nhu cầu cụ thể của dự án.

##### **🔹 Node "🔁 Split Queries" (Split In Batches)**
- **Mục đích**: Chia danh sách từ khóa thành các batch nhỏ để xử lý hiệu quả.
- **Cấu hình**:
  - Thiết lập số lượng batch phù hợp (ví dụ: 5 batch cho 20 từ khóa).
  - Đảm bảo node này được kết nối với node "🌐 Google Search API".

##### **🔹 Node "🌐 Google Search API" (HTTP Request)**
- **Mục đích**: Thực hiện tìm kiếm trên Google với các từ khóa đã chia batch.
- **Cấu hình**:
  - **URL**: `https://www.googleapis.com/customsearch/v1`
  - **Method**: `POST`
  - **Headers**:
    ```
    Content-Type: application/json
    Authorization: Bearer YOUR_GOOGLE_API_KEY
    ```
  - **Body (JSON)**:
    ```json
    {
      "q": "{{$node["🔁 Split Queries"].json[\"item\"]}} site:linkedin.com",
      "cx": "YOUR_CUSTOM_SEARCH_ENGINE_ID",
      "key": "{{$credentials["Google Search API"].apiKey}}"
    }
    ```
    - **YOUR_CUSTOM_SEARCH_ENGINE_ID**: Tham khảo tại [Google Custom Search JSON API](https://programmablesearchengine.google.com/about/).
    - **YOUR_GOOGLE_API_KEY**: Điền API key từ Google Cloud Console.
  - **Lưu ý**: Đảm bảo node này được kết nối với node "🧪 Extract Profiles".

##### **🔹 Node "🧪 Extract Profiles" (Set)**
- **Mục đích**: Lọc và trích xuất thông tin liên quan đến profile LinkedIn từ kết quả tìm kiếm.
- **Cấu hình**:
  - Sử dụng **Expression** để lọc kết quả (ví dụ: trích xuất liên kết profile LinkedIn):
    ```javascript
    $json["items"].map(item => ({
      profile_url: item.link,
      title: item.title,
      description: item.snippet
    }))
    ```
  - Các sếp có thể tùy chỉnh logic trích xuất theo nhu cầu.

##### **🔹 Node "📄 Append to RedOps_Targets" (Google Sheets)**
- **Mục đích**: Lưu kết quả tìm kiếm vào Google Sheets.
- **Cấu hình**:
  - **Credentials**: Chọn tài khoản Google đã đăng ký.
  - **Sheet Name**: Điền tên bảng là **RedOps_Targets** (hoặc tùy chỉnh).
  - **Range**: Chọn ô bắt đầu ghi dữ liệu (ví dụ: `A1`).
  - **Data**: Chọn `json` từ node "🧪 Extract Profiles".
  - **Lưu ý**: Đảm bảo bảng Google Sheets đã được tạo trước và chia sẻ cho tài khoản n8n.

---

#### 3. Kích Hoạt ⚡️
- **Test Run**: Kích hoạt node "⚡ Trigger SocialGraph" và chạy thử với một batch nhỏ để kiểm tra kết quả.
- **Bật Active**: Sau khi kiểm tra thành công, bật workflow để hoạt động liên tục.

---

### ✍️ Mẹo & Gợi Ý Nâng Cao
1. **Tích Hợp Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram Bot** để thông báo kết quả tìm kiếm ngay khi hoàn thành.
   - Ví dụ: Gửi thông báo khi có kết quả mới được thêm vào Google Sheets.

2. **Lưu Log**:
   - Sử dụng node **Sticky Note** để ghi lại lịch sử tìm kiếm và kết quả, giúp theo dõi và phân tích lâu dài.

3. **Báo Cáo Định Kỳ**:
   - Kết hợp với node **Google Calendar** hoặc **n8n Schedule** để tự động kích hoạt workflow hàng tuần hoặc hàng tháng, cập nhật thông tin mới nhất.

4. **Tùy Chỉnh Từ Khóa**:
   - Các sếp có thể tự động hóa việc cập nhật danh sách từ khóa từ một nguồn khác (ví dụ: Google Sheets hoặc API khác) bằng cách sử dụng node **HTTP Request** hoặc **Google Sheets**.

5. **Phân Tích Dữ Liệu**:
   - Sau khi dữ liệu được lưu vào Google Sheets, các sếp có thể sử dụng **Google Data Studio** hoặc **Power BI** để tạo báo cáo phân tích chi tiết về các profile đã thu thập.

---

### 📌 Kết Luận
Workflow này là giải pháp hoàn hảo cho các sếp cần tự động hóa việc tìm kiếm và phân tích thông tin chuyên gia LinkedIn theo vai trò công việc. Với việc kết hợp Google Search API và Google Sheets, workflow không chỉ tiết kiệm thời gian mà còn cung cấp dữ liệu chính xác và cập nhật, hỗ trợ cho các hoạt động **Lead Generation**, **Threat Intelligence**, và **Red Teaming**.

**Hãy áp dụng ngay workflow này và nâng cao hiệu quả công việc của đội ngũ an ninh mạng hoặc marketing của bạn!** 🚀

---