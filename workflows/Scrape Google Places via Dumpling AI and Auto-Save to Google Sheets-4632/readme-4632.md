---
title: "🚀 Tự Động Scrape Danh Sách Google Places Với Dumpling AI & Lưu Trữ Tự Động Vào Google Sheets"
description: "Workflow tự động hóa hàng ngày để lấy danh sách địa điểm từ Google Maps thông qua Dumpling AI, sau đó lưu trữ dữ liệu chi tiết (tên, địa chỉ, đánh giá, danh mục, số điện thoại, website) vào Google Sheets. Giúp các sếp tiết kiệm thời gian và xây dựng danh sách leads địa phương một cách hiệu quả."
slug: "tự-dộng-scrape-google-places-dumpling-ai-google-sheets"
tags: [n8n, automation, AI, Google Maps, Google Sheets, Dumpling AI, lead generation]
keywords: [tự động hóa scrape Google Places, Dumpling AI n8n, lưu trữ dữ liệu địa điểm, tự động hóa lead generation, tự động hóa hàng ngày]
---

# 🚀 **Tự Động Scrape Danh Sách Google Places Với Dumpling AI & Lưu Trữ Tự Động Vào Google Sheets**

### **💡 Giải quyết vấn đề gì?**
Các sếp thường phải tốn thời gian thủ công tìm kiếm và ghi chép thông tin các địa điểm như nhà hàng, cửa hàng, dịch vụ y tế, hoặc cơ sở giáo dục trên Google Maps. Thông tin này thường được sử dụng để xây dựng danh sách leads, phân tích thị trường, hoặc nghiên cứu đối thủ. Với workflow này, **các sếp có thể tự động hóa toàn bộ quá trình** bằng cách:
- **Lấy danh sách từ các từ khóa** (ví dụ: "best dentist in Houston") từ một Google Sheet.
- **Scrape thông tin chi tiết** (tên, địa chỉ, đánh giá, danh mục, số điện thoại, website) từ Google Maps thông qua API của Dumpling AI.
- **Lưu trữ tự động** vào một Google Sheet khác, sẵn sàng để phân tích hoặc sử dụng trong chiến dịch marketing.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần thủ công nhập liệu hàng ngày.
- **Dữ liệu chính xác và cập nhật**: Thông tin được scrape từ Google Maps, đảm bảo tính mới mẻ.
- **Tự động hóa hoàn toàn**: Workflow chạy tự động hàng ngày vào 13h (giá trị mặc định).
- **Dễ dàng phân tích**: Dữ liệu được lưu vào Google Sheets, có thể kết nối với Google Data Studio hoặc Power BI.
- **Xây dựng danh sách leads**: Thông tin chi tiết về địa điểm giúp các sếp xây dựng chiến lược marketing hoặc nghiên cứu thị trường hiệu quả.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Dumpling AI**:
   - API Key của Dumpling AI (để gọi API `search-places`).
   - [Đăng ký tài khoản Dumpling AI](https://dumpling.ai/) và lấy API Key từ Dashboard.
2. **Google Sheets**:
   - **Sheet1**: Chứa danh sách từ khóa cần scrape (ví dụ: "best dentist in Houston", "top cafes in Hanoi").
   - **Sheet2**: Để lưu trữ kết quả scrape (tên, địa chỉ, đánh giá, danh mục, số điện thoại, website).
   - **Quản lý quyền**: Cung cấp quyền "Editor" cho n8n để truy cập cả hai Sheet.
3. **Tài khoản Google OAuth2**:
   - Cấu hình OAuth2 cho Google Sheets trong n8n (thông tin chi tiết trong phần **Cách import & Lưu ý**).
4. **n8n Self-hosted**:
   - Workflow này yêu cầu n8n được cài đặt trên VPS để chạy 24/7.

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow bằng hai cách:
- **Tải file JSON**:
  1. Tải workflow từ [n8n.io/workflows/4632](https://n8n.io/workflows/4632) (chọn "Download JSON").
  2. Trên n8n Editor, nhấn **Import** và chọn file JSON vừa tải.
- **Copy/Paste JSON**:
  1. Copy toàn bộ mã JSON từ [n8n.io/workflows/4632](https://n8n.io/workflows/4632) (chọn "Copy JSON").
  2. Trên n8n Editor, nhấn **Import** và chọn **Paste JSON**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này gồm **5 node chính**, các sếp cần cấu hình kỹ lưỡng như sau:

##### **Node 1: Run Every Day at 1 PM (scheduleTrigger)**
- **Không cần chỉnh sửa**: Workflow mặc định chạy hàng ngày vào 13h (UTC). Nếu cần thay đổi thời gian, các sếp có thể chỉnh sửa trong **Settings** của node này.

##### **Node 2: Scrape Google Places with Dumpling AI (httpRequest)**
- **Tham số quan trọng**:
  - **Method**: `POST`.
  - **URL**: `https://api.dumpling.ai/v1/search-places`.
  - **Headers**:
    - `Authorization`: `Bearer {API_KEY_DUMPLING_AI}` (thay `{API_KEY_DUMPLING_AI}` bằng API Key của Dumpling AI).
    - `Content-Type`: `application/json`.
  - **Body (JSON)**:
    ```json
    {
      "query": "{{ $node["Fetch Search Terms from Sheet"].json["query"] }}"
    }
    ```
    - `$node["Fetch Search Terms from Sheet"].json["query"]` là từ khóa được lấy từ Sheet1 (cần cấu hình trong **Node 5**).
  - **Lưu ý**:
    - Nếu Dumpling AI yêu cầu thêm headers hoặc body khác, các sếp cần cập nhật theo hướng dẫn của API.

##### **Node 3: Split Resulting Places List (splitOut)**
- **Không cần chỉnh sửa**: Node này tự động chia danh sách kết quả scrape thành các mục riêng lẻ để xử lý tiếp.

##### **Node 4: Save Scraped Data to Sheet (googleSheets)**
- **Tham số quan trọng**:
  - **Operation**: `append` (lưu trữ dữ liệu mới vào cuối Sheet).
  - **Sheet Name**: `Sheet2` (thay đổi nếu Sheet có tên khác).
  - **Range**: `A1` (địa chỉ đầu tiên của Sheet để append).
  - **Headers**: Bật tùy chọn này để n8n tự động tạo header cho cột (tên, địa chỉ, đánh giá, danh mục, số điện thoại, website).
  - **Credentials**: Chọn `googleSheetsOAuth2Api` (cần cấu hình trước trong n8n).

##### **Node 5: Fetch Search Terms from Sheet (googleSheets)**
- **Tham số quan trọng**:
  - **Operation**: `get` (lấy dữ liệu từ Sheet).
  - **Sheet Name**: `Sheet1` (Sheet chứa danh sách từ khóa).
  - **Range**: `A1:A` (cột A, toàn bộ dữ liệu).
  - **Credentials**: Chọn `googleSheetsOAuth2Api` (giống Node 4).
  - **Lưu ý**:
    - Sheet1 cần có **cột A** chứa danh sách từ khóa (ví dụ: "best dentist in Houston", "top cafes in Hanoi").
    - Các sếp có thể thêm nhiều từ khóa vào Sheet1 để workflow scrape tất cả.

---

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Nhấn **Run Workflow** để kiểm tra dữ liệu mẫu.
   - Kiểm tra kết quả trong **Sheet2** để đảm bảo dữ liệu scrape và lưu trữ chính xác.
2. **Bật Active**:
   - Sau khi test thành công, chuyển trạng thái workflow sang **Active**.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tăng cường tính năng báo cáo**:
   - Thêm node **Slack/Telegram** để gửi thông báo khi workflow chạy thành công hoặc thất bại.
   - Ví dụ: Sau khi lưu dữ liệu vào Sheet2, thêm node **Slack** để gửi tin nhắn như:
     > *"Workflow scrape Google Places đã hoàn tất! Đã lấy {{ $node["Split Resulting Places List"].json.length }} địa điểm mới."*

2. **Lưu log hoạt động**:
   - Sử dụng node **stickyNote** để ghi lại thông tin debug hoặc log hoạt động (ví dụ: số lượng địa điểm scrape thành công/thất bại).

3. **Tự động gửi báo cáo định kỳ**:
   - Kết hợp với **Google Apps Script** để tự động gửi báo cáo tổng hợp (ví dụ: số lượng địa điểm mới mỗi tháng) qua email.

4. **Tối ưu hóa từ khóa**:
   - Các sếp có thể thêm cột **Priority** vào Sheet1 để ưu tiên scrape từ khóa quan trọng hơn (ví dụ: "best dentist in Houston" có Priority = 1, "cafe in Hanoi" có Priority = 2).
   - Sau đó, sử dụng node **Function** để lọc từ khóa theo Priority trước khi scrape.

5. **Xử lý lỗi**:
   - Thêm node **Set** để kiểm tra lỗi từ Dumpling AI và chuyển hướng đến node **Slack/Email** để báo cáo lỗi.

---

### 📌 **Kết luận**
Workflow này giúp các sếp **tự động hóa hoàn toàn quá trình scrape và lưu trữ thông tin địa điểm từ Google Maps**, tiết kiệm thời gian và nâng cao hiệu quả trong việc xây dựng danh sách leads hoặc phân tích thị trường. **Hãy áp dụng ngay để bắt đầu tự động hóa công việc hàng ngày của mình!**

👉 **Bắt đầu ngay**:
1. Cài đặt n8n trên VPS (nếu chưa có).
2. Import workflow và cấu hình các API Key.
3. Chạy thử và theo dõi kết quả trong Google Sheets!

---
**Chia sẻ và phản hồi**:
Nếu các sếp có bất kỳ câu hỏi hoặc cần hỗ trợ, hãy để lại comment bên dưới hoặc liên hệ qua [n8n Community](https://community.n8n.io/). Chúc các sếp thành công! 🚀