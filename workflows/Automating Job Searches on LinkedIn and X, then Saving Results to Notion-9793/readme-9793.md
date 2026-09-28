---
title: "🔍 **Tự Động Hóa Tìm Việc Làm Senior Designer trên LinkedIn & X (Twitter) + Lưu Trữ vào Notion – Giúp Các Sếp Tiết Kiệm 10h/Tuần**"
description: "Workflow tự động hóa tìm kiếm và lưu trữ các cơ hội việc làm Senior Designer trên LinkedIn và X (Twitter) vào Notion hàng ngày, giúp các sếp tiết kiệm thời gian theo dõi thủ công và không bỏ lỡ bất kỳ cơ hội nào. Kết quả: Dữ liệu được cập nhật tự động, sắp xếp logic, và dễ dàng theo dõi từ mọi thiết bị."
slug: "tu-dong-hoa-tim-viec-lam-linkedin-x-notion"
tags: [n8n, automation, no-code, tìm việc làm, LinkedIn, X (Twitter), Notion, tự động hóa việc làm]
keywords: [tự động hóa tìm việc làm LinkedIn, lưu trữ việc làm vào Notion, tự động hóa X (Twitter) tìm việc, n8n workflow tìm việc, tự động hóa việc làm cho designer]
---

# 🚀 **Tự Động Hóa Tìm Việc Làm Senior Designer trên LinkedIn & X (Twitter) + Lưu Trữ vào Notion**

### **Nỗi Đau Của Các Sếp Khi Tìm Việc Làm Thủ Công**
Các sếp đang mất **từ 5-10 giờ/tuần** để:
- Quét liên tục các trang việc làm trên LinkedIn và X (Twitter) để không bỏ lỡ cơ hội.
- Sao chép và lưu trữ thông tin việc làm vào Notion/Google Sheets để theo dõi.
- Lo lắng việc bỏ lỡ việc làm do không cập nhật kịp thời.
- Phải kiểm tra lại dữ liệu thủ công để tránh trùng lặp hoặc thông tin sai.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Quét và lọc** các việc làm Senior Designer trên LinkedIn và X hàng ngày.
✅ **Lưu trữ** vào Notion với định dạng chuyên nghiệp (tên công ty, địa điểm, mô tả, link).
✅ **Báo cáo tự động** mỗi sáng để các sếp chỉ cần xem và ứng tuyển.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** thay vì dùng phiên bản Cloud.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (Đảm bảo tốc độ và ổn định)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10h/tuần**: Không phải quét thủ công trên LinkedIn và X.
- **Dữ liệu chính xác và sắp xếp logic**: Thông tin việc làm được tự động phân loại và lưu vào Notion.
- **Không bỏ lỡ cơ hội**: Workflow chạy tự động hàng ngày vào **5h sáng**, trước khi các sếp thức dậy.
- **Tùy chỉnh linh hoạt**: Chỉ cần thay đổi **từ khóa tìm kiếm** hoặc **địa điểm** mà không cần viết code.
- **Hoạt động liên tục**: Không phụ thuộc vào thời gian làm việc của cá nhân.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản LinkedIn và X (Twitter)**:
   - Để workflow có thể **quét và lấy dữ liệu** từ hai nền tảng này.
   - **Lưu ý**: LinkedIn có thể **cấm scrape** nếu phát hiện quá nhiều request từ một IP. Do đó, **VPS là bắt buộc** để tránh bị chặn.

2. **Tài khoản Notion**:
   - Một **database Notion** đã sẵn sàng để lưu trữ việc làm.
   - **Mã API Notion**: Tạo từ [Notion API](https://www.notion.so/my-integrations) để kết nối với n8n.

3. **API Keys và Credentials**:
   - **Twitter API Key**: Đăng ký tại [Twitter Developer Portal](https://developer.twitter.com/).
   - **LinkedIn không cung cấp API chính thức**, workflow này **scrape công khai** (xem **Lưu ý về pháp lý** ở cuối bài).

4. **n8n Instance**:
   - **Self-hosted** (khuyến nghị) hoặc **n8n Cloud** (miễn phí cho dự án cá nhân).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow:
- **Tải file JSON** từ [đây](https://n8n.io/workflows/9793) và import vào n8n Editor.
- **Copy JSON** từ file và **paste** vào n8n Editor (đường dẫn: `https://[your-n8n-instance]/workflow/import`).

:::note[Lưu ý khi import]
- Nếu dùng **n8n Cloud**, các sếp cần **chuyển sang self-hosted** để tránh bị giới hạn request.
- **Không sao chép từ trang web** (do có lỗi format), chỉ nên dùng file JSON hoặc copy từ editor.
:::

---

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflows này có **2 phần chính**: **LinkedIn** và **X (Twitter)**. Mỗi phần cần cấu hình kỹ lưỡng:

##### **A. Cấu Hình LinkedIn Job Search**
1. **Node "Set Search Criteria1"**:
   - **Tham số cần chỉnh**:
     - `search_keywords`: Danh sách **tên công việc** muốn tìm (ví dụ: `senior product designer, UX lead, design manager`).
     - `excluded_keywords`: Từ khóa **bỏ qua** (ví dụ: `contract, freelance`).
     - `location`: **Địa điểm** (ví dụ: `remote, Vietnam, Singapore`).
     - `r86400`: Lọc việc làm trong **24h** (có thể thay đổi thành `r604800` cho **tuần**).
     - `DD`: Sắp xếp theo **mới nhất**.

   ```json
   {
     "search_keywords": "senior designer, product design lead, UX designer",
     "excluded_keywords": "contract, freelance, internship",
     "location": "remote, Vietnam",
     "r86400": true,
     "sortBy": "DD"
   }
   ```

2. **Node "Limit1"**:
   - **Thiết lập giới hạn số việc làm** để tránh quá tải (mặc định **10 việc/lần**).
   - Nếu muốn lấy nhiều hơn, tăng `maxItems` (nhưng **cẩn thận với rate limit** của LinkedIn).

3. **Node "Wait"**:
   - **Thời gian chờ giữa các request** (mặc định **10s**) để tránh bị chặn.
   - Nếu LinkedIn **cấm IP**, tăng thời gian chờ lên **30s-60s**.

4. **Node "Parse Jobs1" và "Extract Poster Info2"**:
   - Đây là **code nodes** tự động **trích xuất** thông tin từ HTML của LinkedIn.
   - **Không cần chỉnh** trừ khi LinkedIn thay đổi **cấu trúc trang** (xem **Lưu ý về pháp lý**).

##### **B. Cấu Hình X (Twitter) Job Search**
1. **Node "Search Twitter Job Posts"**:
   - **Kết nối Twitter API**:
     - Vào **n8n Credentials** → Thêm **Twitter OAuth2**.
     - Đăng ký API tại [Twitter Developer](https://developer.twitter.com/) và điền:
       - `Consumer Key`
       - `Consumer Secret`
       - `Access Token`
       - `Access Token Secret`
   - **Tham số tìm kiếm**:
     - `query`: `job "senior designer" OR "product design lead" -filter:retweets` (tùy chỉnh theo nhu cầu).

2. **Node "Parse and Filter Jobs"**:
   - **Lọc việc làm hợp lệ** (có tiêu đề, mô tả, link).
   - **Không cần chỉnh** trừ khi muốn thay đổi logic lọc.

3. **Node "Save to Notion Database"**:
   - **Kết nối Notion API**:
     - Vào **n8n Credentials** → Thêm **Notion API**.
     - Chọn **database Notion** đã tạo (cần **đặt tên chính xác** như trong Notion).
   - **Tham số lưu trữ**:
     - `databaseId`: ID của database Notion (tìm trong URL của database).
     - `properties`: Cấu trúc dữ liệu (tên công việc, công ty, mô tả, link).

---

#### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run**:
   - Chạy **manual test** với **dữ liệu mẫu** để kiểm tra:
     - Có lấy được việc làm không?
     - Dữ liệu có lưu vào Notion đúng không?
   - Nếu gặp lỗi, kiểm tra:
     - **Rate limit** (LinkedIn/Twitter).
     - **Cấu trúc Notion database** (phải khớp với `properties` trong node Notion).

2. **Bật Active**:
   - Sau khi test thành công, **bật Active** cho cả hai **schedule trigger**:
     - `Everyday @5am1` (LinkedIn).
     - `Everyday @5:15am` (X).

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tự động Gửi Báo Cáo Hàng Ngày**:
   - Kết nối với **Slack/Telegram** để nhận **tin nhắn thông báo** mỗi sáng khi workflow chạy.
   - **Cách làm**:
     - Thêm **node Slack/Telegram** sau `Save to Notion`.
     - Gửi tin nhắn: `📌 [Số việc làm mới] đã được lưu vào Notion: [Link database]`.

2. **Lưu Log Lịch Sử**:
   - Thêm **node StickyNote** để ghi lại **lịch sử chạy** (thời gian, số việc tìm được, lỗi nếu có).
   - **Ưu điểm**: Dễ dàng **debug** nếu workflow bị lỗi.

3. **Tùy Chỉnh Thời Gian Chạy**:
   - Nếu muốn chạy **không phải vào 5h sáng**, chỉnh **schedule trigger** thành:
     - `Every 2 hours` (mỗi 2h).
     - `Every Monday to Friday at 9am` (chỉ chạy vào giờ làm việc).

4. **Lọc Việc Làm Theo Mức Lương**:
   - Thêm **node Filter** sau `Parse Jobs1` để lọc việc làm có **mức lương > X triệu/tháng**.
   - **Ví dụ**:
     ```json
     {
       "jsonpath": "$[*].description",
       "operator": "contains",
       "value": "$10M"
     }
     ```

5. **Kết Nối với Google Sheets**:
   - Thay vì Notion, các sếp có thể **lưu vào Google Sheets** để dễ dàng **sắp xếp và phân tích**.
   - **Cách làm**:
     - Thay node `notion` bằng `googleSheets`.
     - Cấu hình **sheet và sheet name** tương ứng.

---

### 📌 **Lưu Ý Quan Trọng**
1. **Pháp Lý & Rate Limit**:
   - **LinkedIn không cung cấp API chính thức**, workflow này **scrape công khai**.
   - **Rủi ro**:
     - LinkedIn **có thể chặn IP** nếu request quá nhiều.
     - **Giải pháp**: Sử dụng **VPS + delay giữa request**.
   - **X (Twitter)** có **rate limit**, không nên chạy quá **100 request/phút**.

2. **Cập Nhật Cấu Trúc HTML**:
   - Nếu LinkedIn **thay đổi trang**, **code nodes** (`Parse Jobs1`, `Extract Poster Info2`) có thể **bị lỗi**.
   - **Giải pháp**:
     - Kiểm tra **HTML source** của trang việc làm.
     - Chỉnh sửa **code trong nodes** nếu cần.

3. **Notion Database Cần Chuẩn Bị**:
   - **Cấu trúc database** phải khớp với `properties` trong node Notion.
   - **Ví dụ**:
     ```
     - Title (Text)
     - Company (Text)
     - Location (Select)
     - Salary (Number)
     - Description (Rich Text)
     - Link (URL)
     ```

4. **Backup Workflow**:
   - **Luôn export JSON** của workflow sau khi cấu hình xong.
   - **Lưu ở đâu?**
     - Google Drive.
     - GitHub (nếu công khai).
     - File local (n8n có tính năng **export/import**).

---

### 🎯 **Kết Luận: Hãy Tự Động Hóa Ngay!**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào **ứng tuyển và phỏng vấn** thay vì **quét việc làm thủ công**. Với **cấu hình đơn giản** và **tùy chỉnh linh hoạt**, nó phù hợp cho:
✔ **Designer, Product Manager** tìm việc mới.
✔ **Doanh nghiệp** muốn theo dõi thị trường tuyển dụng.
✔ **Freelancer** muốn cập nhật cơ hội remote.

**Bước đầu tiên**: **Import workflow** và **cấu hình Notion**. Sau đó, chỉ cần **bật Active** và **quên đi việc tìm việc thủ công**!

👉 **[Tải workflow ngay](https://n8n.io/workflows/9793)** và bắt đầu tự động hóa việc tìm việc của mình! 🚀

---
**Chia sẻ ý kiến**: Các sếp có thể **tùy chỉnh thêm** gì khác cho workflow này? Để lại comment bên dưới! 👇