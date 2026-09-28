---
title: "🚀 Tự Động Scrape Đánh Giá Thương Hiệu Đối Thủ & Tạo Quảng Cáo AI (Bright Data + OpenAI) - Giảm 90% Thời Gian Marketing"
description: "Workflow tự động hóa scrape đánh giá sản phẩm từ Amazon của đối thủ, tổng hợp và phân tích bằng AI, sau đó tự động tạo quảng cáo creatives (ảnh + văn bản) và gửi cho team media. Giúp các sếp tiết kiệm 90% thời gian phân tích thị trường và tối ưu hóa chiến dịch quảng cáo."
slug: "tieu-dong-scrape-danh-gia-thuong-hieu-doi-thu-tao-quang-cao-ai"
tags: [n8n, automation, marketing-automation, ai-marketing, bright-data, openai, google-sheets]
keywords: [n8n workflow scrape amazon, tự động hóa marketing, tạo quảng cáo AI, phân tích đối thủ, bright data api, openai gpt-4o-mini]
---

# 🚀 **Scrape Đánh Giá Đối Thủ & Tạo Quảng Cáo AI: Giải Pháp Tự Động Hóa Marketing 100% Không Code**

### **Nỗi Đau Của Các Sếp Marketing**
Hàng ngày, các sếp marketing phải:
- **Tốn thời gian thủ công** scrape hàng trăm đánh giá sản phẩm từ Amazon của đối thủ.
- **Phân tích thủ công** để tìm ra xu hướng, điểm mạnh/điểm yếu của sản phẩm.
- **Tạo quảng cáo creatives** từ đầu, mất nhiều thời gian và không đảm bảo tính sáng tạo.
- **Gửi email báo cáo** cho team media một cách lặp đi lặp lại, dễ bị lỡ.

**Workflow này giải quyết tất cả!** Với công nghệ **Bright Data** (scrape an toàn) và **OpenAI GPT-4o-mini** (AI sáng tạo), các sếp chỉ cần **nhấn một nút**, workflow sẽ tự động:
✅ **Scrape** tất cả đánh giá mới nhất của đối thủ trên Amazon.
✅ **Tổng hợp & phân tích** bằng AI để rút ra **pain points** (điểm yếu) và **opportunities** (cơ hội).
✅ **Tạo quảng cáo creatives** (ảnh + văn bản) phù hợp với khách hàng mục tiêu.
✅ **Gửi tự động** cho team media qua email.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian** so với cách làm thủ công.
- **Tính chính xác cao** với AI phân tích dữ liệu thực tế từ Amazon.
- **Quảng cáo cá nhân hóa** dựa trên feedback khách hàng thực sự.
- **Hoạt động 24/7** mà không cần can thiệp của con người.
- **Dữ liệu tập trung** trên Google Sheets, dễ theo dõi và báo cáo.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Bright Data** (để scrape Amazon):
   - [Đăng ký Bright Data](https://brightdata.com/) (mã giảm giá: **N8NBRIGHT** - giảm 20%).
   - **Lưu ý**: Bright Data yêu cầu **Proxy Residential** để scrape Amazon an toàn. Các sếp nên chọn gói **Bright Data Scraper** (từ 100$/tháng).
   - **API Key**: Tạo tại [Bright Data Dashboard](https://dashboard.brightdata.com/).

2. **Tài khoản OpenAI**:
   - [Đăng ký OpenAI](https://platform.openai.com/signup) và lấy **API Key**.
   - **Model**: Workflow sử dụng **GPT-4o-mini** (rẻ và hiệu quả).

3. **Tài khoản Google Sheets**:
   - **Bắt buộc** sử dụng **template** của tác giả (liên kết dưới đây).
   - **Quản lý quyền**: Cung cấp quyền **Edit** cho workflow.

4. **Tài khoản Gmail** (để gửi email báo cáo):
   - Cần **OAuth 2.0** để workflow có thể gửi email tự động.

5. **Link Amazon của đối thủ**:
   - Các sếp cần **điền URL sản phẩm** của đối thủ vào node **Form Trigger** (hướng dẫn chi tiết dưới đây).

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [liên kết gốc](https://n8n.io/workflows/3624) hoặc copy toàn bộ JSON dưới đây vào **n8n Editor**.
- **Cách import**:
  1. Mở **n8n Editor** (trang chủ của workflow).
  2. Nhấn **Import** → **Paste JSON** → Dán toàn bộ mã JSON.
  3. Nhấn **Import**.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflows này có **12 node**, nhưng các sếp cần chú ý đặc biệt đến **5 node quan trọng** sau:

##### **A. Node "On form submission - Amazon Reviews" (Form Trigger)**
- **Mục đích**: Nhận input là **URL sản phẩm Amazon** của đối thủ.
- **Cách cấu hình**:
  - Nhấn **Edit** → **Credentials** → Chọn **Google Sheets OAuth 2.0** (đã cấu hình trước).
  - **Key Parameters**:
    - **Sheet Name**: Điền tên sheet trong template (ví dụ: **"Competitor Reviews"**).
    - **Range**: Điền `"Sheet1!A1"` (để lưu dữ liệu scrape).

##### **B. Node "HTTP Request - Post API call to Bright Data" (HTTP Request)**
- **Mục đích**: Gửi yêu cầu scrape đến Bright Data.
- **Cách cấu hình**:
  - **URL**: `https://api.brightdata.com/scraper/api/v1/start-snapshot`
  - **Headers**:
    - `Authorization`: `Bearer {{ $credentials.brightDataApi.apiKey }}`
    - `Content-Type`: `application/json`
  - **Body (JSON)**:
    ```json
    {
      "url": "{{ $json.url }}",  // URL sản phẩm Amazon từ Form Trigger
      "scraper_type": "amazon",
      "scraper_options": {
        "scrape_reviews": true,
        "max_reviews": 100,
        "scrape_review_details": true
      }
    }
    ```
  - **Lưu ý**: Thay thế `{{ $credentials.brightDataApi.apiKey }}` bằng **API Key** của Bright Data.

##### **C. Node "If - Checking status of Snapshot" (If)**
- **Mục đích**: Kiểm tra liệu dữ liệu đã scrape xong chưa.
- **Cách cấu hình**:
  - **Condition**: `{{ $node["HTTP Request - Getting data from Bright Data"].json()["status"] === "completed" }}`
  - **Nếu true**: Chạy node tiếp theo để lấy dữ liệu.

##### **D. Node "OpenAI Chat Model" (lmChatOpenAi)**
- **Mục đích**: Tạo **tóm tắt đánh giá** bằng AI.
- **Cách cấu hình**:
  - **Credentials**: Chọn **OpenAI API** (đã cấu hình trước).
  - **Key Parameters**:
    - **Model**: `gpt-4o-mini` (đã mặc định).
    - **Prompt**:
      ```plaintext
      Tóm tắt các đánh giá mới nhất về sản phẩm {{ $json.productName }} từ Amazon.
      Trích ra:
      1. 3 điểm mạnh (Strengths) của sản phẩm.
      2. 3 điểm yếu (Weaknesses) của sản phẩm.
      3. 2 xu hướng (Trends) nổi bật trong đánh giá.
      4. Gợi ý cải tiến cho sản phẩm.
      Đảm bảo trả lời ngắn gọn và có cấu trúc.
      ```
  - **Lưu ý**: Thay thế `{{ $json.productName }}` bằng tên sản phẩm từ Bright Data.

##### **E. Node "OpenAI - Generating image" (openAi)**
- **Mục đích**: Tạo **ảnh quảng cáo creatives** dựa trên pain points.
- **Cách cấu hình**:
  - **Credentials**: Chọn **OpenAI API**.
  - **Key Parameters**:
    - **Resource**: `image`
    - **Prompt**:
      ```plaintext
      Tạo một ảnh quảng cáo kích thước 1080x1080 phù hợp với khách hàng B2C.
      - Điểm yếu chính của sản phẩm: {{ $json.weaknesses }}
      - Phong cách: "Weird and Fun" với các đối tượng kỳ lạ như:
        - Trái cây có mặt người
        - Đồ vật hoạt hình hóa
        - Bối cảnh hài hước
      - Màu sắc: Sáng và tươi vui.
      - Giao diện: Đơn giản, dễ đọc.
      ```
  - **Lưu ý**:
    - Thay thế `{{ $json.weaknesses }}` bằng dữ liệu từ node **Basic LLM Chain**.
    - **Chi phí**: Tạo ảnh DALL·E có chi phí (~0.02$/ảnh). Các sếp nên **set budget** trong OpenAI.

##### **F. Node "Gmail - Sending creative to Media Buyers" (gmail)**
- **Mục đích**: Gửi **quảng cáo creatives** (ảnh + văn bản) cho team media.
- **Cách cấu hình**:
  - **Credentials**: Chọn **Gmail OAuth 2.0**.
  - **Key Parameters**:
    - **To**: Địa chỉ email của team media (ví dụ: `media@company.com`).
    - **Subject**: `🚀 Quảng cáo mới: {{ $json.productName }} - Tạo từ feedback khách hàng`.
    - **Body**:
      ```plaintext
      Xin chào Team Media,

      Dưới đây là **quảng cáo creatives** mới cho sản phẩm **{{ $json.productName }}**, được tạo tự động từ phân tích đánh giá Amazon.

      **Tóm tắt điểm yếu chính**:
      {{ $json.summary }}

      **Ảnh quảng cáo**:
      ![Ảnh]({{ $json.imageUrl }})

      **Link sản phẩm**: {{ $json.amazonUrl }}

      Chúc các sếp thành công với chiến dịch!
      ```
  - **Lưu ý**:
    - Thay thế `{{ $json.summary }}`, `{{ $json.imageUrl }}`, `{{ $json.amazonUrl }}` bằng dữ liệu từ node trước.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhấn **Run Workflow** và điền **URL sản phẩm Amazon** của đối thủ vào Form Trigger.
   - Kiểm tra **Google Sheets** xem dữ liệu scrape có đúng không.
   - Kiểm tra **email** xem quảng cáo có được gửi đúng không.

2. **Bật Active**:
   - Sau khi test thành công, nhấn **Active** để workflow chạy tự động mỗi khi có dữ liệu mới.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[CÁCH LÀM TIẾP]
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack Webhook** hoặc **Telegram Bot** để thông báo khi có dữ liệu mới.
   - **Cách làm**:
     - Tạo **Slack App** tại [api.slack.com](https://api.slack.com/apps) và lấy **Webhook URL**.
     - Thêm node **HTTP Request** với URL Slack và body:
       ```json
       {
         "text": "🚀 Đã scrape xong sản phẩm: {{ $json.productName }}. Kết quả: {{ $json.summary }}"
       }
       ```

2. **Lưu log hoạt động**:
   - Thêm node **Google Sheets** để lưu **log hoạt động** (thời gian scrape, status, lỗi...).
   - **Cách làm**:
     - Tạo sheet mới tên **"Logs"** với cột: `Timestamp, ProductName, Status, Error`.
     - Sử dụng node **Google Sheets (Append)** để ghi dữ liệu.

3. **Tự động gửi báo cáo định kỳ**:
   - Thêm node **n8n-nodes-base.cron** để chạy workflow hàng tuần.
   - **Cách làm**:
     - Thêm node **Cron Trigger** với lịch `0 0 * * 0` (từng Chủ Nhật lúc 00:00).
     - Kết nối với node **Form Trigger** để scrape sản phẩm mới nhất.

4. **Tối ưu hóa chi phí OpenAI**:
   - Sử dụng **GPT-4o-mini** thay vì GPT-4 để giảm chi phí.
   - **Lưu ý**: GPT-4o-mini có độ chính xác cao hơn GPT-3.5 nhưng rẻ hơn.

5. **Tạo nhiều template quảng cáo**:
   - Thay đổi **prompt** trong node **OpenAI Chat Model** để tạo nhiều phiên bản quảng cáo khác nhau (ví dụ: phiên bản hài hước, phiên bản nghiêm túc).

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp marketing muốn:
✔ **Tiết kiệm thời gian** khỏi việc scrape và phân tích thủ công.
✔ **Tạo quảng cáo sáng tạo** dựa trên feedback thực tế của khách hàng.
✔ **Tự động hóa hoàn toàn** quá trình báo cáo cho team media.

**Hành động ngay!**
1. **Đăng ký Bright Data** và **OpenAI** (mã giảm giá đã cung cấp).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Test với sản phẩm đối thủ** và bắt đầu tự động hóa marketing!

**Nếu gặp vấn đề**, các sếp có thể liên hệ tác giả tại:
- [Yaron Been - LinkedIn](https://www.linkedin.com/in/yaronbeen/)
- [YouTube](https://www.youtube.com/@YaronBeen/videos)

---
**Chúc các sếp thành công với chiến dịch marketing tự động hóa!** 🚀