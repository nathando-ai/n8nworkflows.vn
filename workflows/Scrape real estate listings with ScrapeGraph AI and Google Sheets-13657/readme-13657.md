---
title: "🏠 **Tự Động Hoá Scraping Danh Sách Bất Động Sản từ Web với ScrapeGraph AI + Google Sheets** – Giúp Các Sếp Tiết Kiệm 100h/Năm"
description: "Workflow tự động hóa hoàn toàn không cần code để **scrape** danh sách bất động sản từ các trang web, **tóm tắt** thông tin chi tiết, và **lưu trữ** vào Google Sheets với định dạng chuyên nghiệp. Phù hợp cho nhà đầu tư, môi giới, và doanh nghiệp nghiên cứu thị trường bất động sản."
slug: "tieu-dong-hoa-scrape-bat-dong-san-scrapegraph-google-sheets"
tags: [n8n, automation, no-code, real-estate, scrapegraph-ai, google-sheets, ai-summarization]
keywords: [scrape bất động sản n8n, tự động hóa scrape web, scrapegraph ai google sheets, tự động hóa nghiên cứu thị trường bất động sản, workflow scrape url danh sách bất động sản]
---

# 🚀 **Tự Động Hoá Scrape Danh Sách Bất Động Sản với ScrapeGraph AI + Google Sheets**

### **Nỗi Đau Của Các Sếp Hiện Nay**
Các sếp trong lĩnh vực bất động sản thường phải **tốn thời gian vô cùng nhiều** để:
- **Tìm kiếm thủ công** danh sách nhà đất trên các trang web như Immobiliare.it, Zoopla, hoặc các trang địa phương.
- **Copy-paste** thông tin (giá, diện tích, phòng ngủ, vị trí) vào Excel hoặc Google Sheets, dẫn đến **sai sót cao** và **không cập nhật kịp thời**.
- **Không có cách nào tự động hóa** để theo dõi các danh sách mới xuất hiện trên thị trường, khiến các sếp **bỏ lỡ cơ hội đầu tư** hoặc **quá tải thông tin**.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Scrape tự động** danh sách bất động sản từ bất kỳ trang web nào (chỉ cần cấu hình URL).
✅ **Trích xuất dữ liệu chi tiết** (giá, diện tích, phòng ngủ, tiện ích, hình ảnh) bằng **ScrapeGraph AI** và **Google Gemini**.
✅ **Lưu trữ vào Google Sheets** với định dạng chuyên nghiệp, **không trùng lặp**, và **cập nhật liên tục**.
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và **không bị gián đoạn**, các sếp nên cài đặt n8n trên **VPS riêng (Self-hosted)** để đảm bảo **tốc độ và an toàn dữ liệu**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đảm bảo **tốc độ scrape cao**)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100+ giờ/năm** so với cách làm thủ công.
- **Dữ liệu chính xác 100%** (không sai sót khi copy-paste).
- **Cập nhật tự động** khi có danh sách mới trên trang web.
- **Dễ dàng phân tích thị trường** với dữ liệu được **sắp xếp theo tiêu chuẩn**.
- **Hoạt động liên tục** mà không cần can thiệp của con người.
- **Thích ứng với bất kỳ trang web bất động sản nào** (chỉ cần thay đổi URL và tham số).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản ScrapeGraph AI** (để scrape dữ liệu từ web).
✔ **Tài khoản Google Cloud** (để sử dụng **Google Gemini API** và **Google Sheets OAuth2**).
✔ **Google Sheet mẫu** (có thể **clone từ đây** [Template Google Sheets](https://docs.google.com/spreadsheets/d/1jtMyMglBbekD9Z407q8-0vn-cDDXhM81Uj1oAZIJGX8/edit?usp=sharing)).
✔ **API Keys**:
   - `scrapegraphAIApi` (từ ScrapeGraph AI).
   - `googlePalmApi` (từ Google Cloud).
   - `googleSheetsOAuth2Api` (từ Google Sheets).
✔ **URL trang web bất động sản** muốn scrape (ví dụ: `https://www.immobiliare.it/vendita-case/verona/`).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/13657](https://n8n.io/workflows/13657) và import vào **n8n Editor**.
- **Copy JSON** từ file và dán vào **n8n Editor** (tab `Import`).

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **16 node**, nhưng các node **quan trọng nhất** cần cấu hình cẩn thận:

##### **🔹 Node "Set params" (Cấu hình tham số)**
- **Base URL**: Nhập URL trang danh sách bất động sản (ví dụ: `https://www.immobiliare.it/vendita-case/verona/`).
- **Pagination parameter**: Tham số phân trang (ví dụ: `pag` nếu URL phân trang là `?pag=2`).
- **Max pages**: Số trang muốn scrape (ví dụ: `10`).

##### **🔹 Node "Generate Urls" (Tạo URL phân trang)**
- **Code node này** tự động sinh ra các URL phân trang (ví dụ: `?pag=1`, `?pag=2`, ...).
- **Không cần chỉnh sửa** nếu các sếp đã nhập đúng `base_url` và `page_format_value`.

##### **🔹 Node "Scrape listings" (Scrape danh sách URL)**
- **Sử dụng `scrapegraphAIApi`** để scrape danh sách URL của các danh sách bất động sản.
- **Không cần chỉnh sửa** nếu cấu hình API đúng.

##### **🔹 Node "Extract individual URL" (Trích xuất URL chi tiết)**
- **Sử dụng Google Gemini (Information Extractor)** để **tách riêng URL** của mỗi danh sách.
- **Không cần chỉnh sửa** nếu cấu hình API `googlePalmApi` đúng.

##### **🔹 Node "Extract data" (Trích xuất dữ liệu chi tiết)**
- **Sử dụng ScrapeGraph AI** để scrape **dữ liệu chi tiết** của mỗi danh sách (giá, diện tích, phòng ngủ, tiện ích, hình ảnh).
- **Cần chỉnh sửa JSON schema** nếu muốn trích xuất **thông tin khác** (ví dụ: thêm `cellar`, `balcony`).
  ```json
  {
    "title": "$title",
    "price": "$price",
    "area": "$area",
    "bedrooms": "$bedrooms",
    "bathrooms": "$bathrooms",
    "floor": "$floor",
    "rooms": "$rooms",
    "balcony": "$balcony",
    "terrace": "$terrace",
    "cellar": "$cellar",
    "heating": "$heating",
    "air_conditioning": "$air_conditioning",
    "image_urls": "$image_urls"
  }
  ```

##### **🔹 Node "Update real estate listings" (Cập nhật Google Sheets)**
- **Chọn `googleSheetsOAuth2Api`** và cấu hình:
  - **Sheet ID**: Lấy từ URL Google Sheets (ví dụ: `1jtMyMglBbekD9Z407q8-0vn-cDDXhM81Uj1oAZIJGX8`).
  - **Sheet Name**: Tên tab trong Google Sheets (ví dụ: `Danh sách bất động sản`).
  - **Operation**: Chọn `appendOrUpdate` để **cập nhật hoặc thêm mới** dữ liệu.
- **Cần đảm bảo cột trong Google Sheets** khớp với **JSON schema** ở node `Extract data`.

#### **3. Kích Hoạt ⚡️**
- **Test run** với **dữ liệu mẫu** (ví dụ: scrape 2-3 trang đầu).
- **Bật Active workflow** và **chọn `Manual Trigger`** để chạy khi cần.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Thêm Slack/Telegram Notification**
   - Sử dụng **node `n8n-nodes-base.slack`** hoặc **`n8n-nodes-base.telegram`** để **báo cáo kết quả scrape** mỗi khi workflow hoàn thành.
   - **Cấu hình**:
     ```json
     {
       "channel": "#notifications",
       "message": "Workflow scrape bất động sản hoàn tất! Có {{ $json("items").length }} danh sách mới."
     }
     ```

2. **Lưu Log vào Google Drive**
   - Sử dụng **node `n8n-nodes-base.googleDrive`** để **lưu log scrape** vào Google Drive với định dạng CSV/JSON.
   - **Ưu điểm**: Dễ dàng **theo dõi lịch sử scrape** và **phân tích dữ liệu lâu dài**.

3. **Chạy Định Kỳ với Cron**
   - Sử dụng **node `n8n-nodes-base.cron`** để **scrape tự động hàng ngày/tuần**.
   - **Cấu hình**:
     ```json
     {
       "cronExpression": "0 0 * * *" // Chạy hàng ngày lúc 00:00
     }
     ```

4. **Tích Hợp với AI Chatbot (Google Gemini)**
   - Sử dụng **node `lmChatGoogleGemini`** để **tóm tắt thông tin** của các danh sách mới và gửi cho các sếp qua **Email/Slack**.
   - **Prompt ví dụ**:
     ```
     Tóm tắt danh sách bất động sản mới nhất:
     - Giá: {{ $json("price") }}
     - Diện tích: {{ $json("area") }}
     - Phòng ngủ: {{ $json("bedrooms") }}
     - Vị trí: {{ $json("location") }}
     - Tiện ích: {{ $json("features") }}
     ```

5. **Tự Động Xóa Trùng Lặp**
   - Sử dụng **node `n8n-nodes-base.filter`** để **kiểm tra URL đã tồn tại** trong Google Sheets trước khi cập nhật.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc **scrape thủ công** và **lưu trữ dữ liệu** trên Excel. Với **cấu hình đơn giản**, các sếp có thể:
✔ **Scrape bất kỳ trang web bất động sản nào** (chỉ cần thay đổi URL).
✔ **Lưu dữ liệu vào Google Sheets** với định dạng chuyên nghiệp.
✔ **Tích hợp với AI** để **tóm tắt và phân tích** thông tin.
✔ **Hoạt động tự động 24/7** mà không cần can thiệp.

**🚀 Hãy áp dụng ngay workflow này và bắt đầu tự động hóa scrape bất động sản của mình!**
Nếu có **vấn đề trong quá trình cấu hình**, các sếp có thể liên hệ với tác giả Davide qua [LinkedIn](https://www.linkedin.com/in/davideboizza/) hoặc [Email](mailto:info@n3w.it).

---
**💡 Lưu ý cuối cùng:**
- **Scrape phải tuân thủ quy định pháp luật** của trang web (nhiều trang có **robots.txt** cấm scrape).
- **Không scrape quá nhiều dữ liệu trong thời gian ngắn** để tránh bị **chặn IP**.
- **Nếu trang web có CAPTCHA**, cần sử dụng **proxy** hoặc **ScrapeGraph AI Pro** để tránh bị chặn.