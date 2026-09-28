---
title: "🔍 **Tự Động Hóa Phân Tích SEO On-Page & Ghi Log Tự Động Với RapidAPI & Google Sheets (N8n)**
description: "Giải pháp tự động hóa phân tích SEO chi tiết cho website từ URL đầu vào, thu thập dữ liệu về lưu lượng truy cập, DA/PA, backlinks và phân tích đối thủ, ghi log vào Google Sheets. Tiết kiệm thời gian lên đến 80% cho các sếp Marketing & SEO."
slug: "tieu-dong-hoa-phan-tich-seo-on-page-voi-rapidapi-google-sheets"
tags: [n8n, automation, seo, rapidapi, google-sheets, market-research, no-code]
keywords: [n8n workflow seo, tự động hóa phân tích seo, rapidapi api seo, google sheets seo, phân tích backlink tự động, phân tích đối thủ seo]
---

# 🚀 **Tự Động Hóa Phân Tích SEO On-Page & Ghi Log Tự Động Với RapidAPI & Google Sheets**

### **Giải pháp SEO cho các sếp không còn phải "bò" thủ công**
Hãy tưởng tượng một tình huống: Bạn là một chuyên gia SEO hoặc quản lý marketing, phải phân tích hàng chục website hàng tuần để so sánh lưu lượng truy cập, Domain Authority (DA), Page Authority (PA), backlinks và chiến lược của đối thủ. Quá trình này không chỉ tốn thời gian mà còn dễ mắc lỗi do tính thủ công cao. **Workflow này sẽ tự động hóa toàn bộ quy trình đó chỉ với một form nhập URL!**

Với **Automated On-Page SEO Analysis**, các sếp có thể:
✅ **Nhập URL website** → **Workflow tự động** thu thập dữ liệu từ RapidAPI (Semrush API mockup).
✅ **Ghi log tất cả kết quả** vào Google Sheets theo **4 tab chuyên biệt**:
   - **Website Traffic** (lưu lượng truy cập, bounce rate, users).
   - **DA/PA** (Domain Authority, Page Authority, spam score, organic traffic).
   - **Backlinks Overview** (số lượng backlinks, domain rating).
   - **Backlinks & Competitor Analysis** (danh sách backlinks chi tiết + phân tích đối thủ).
✅ **Tiết kiệm thời gian lên đến 80%** so với cách làm thủ công.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo dữ liệu an toàn và không bị giới hạn bởi phiên bản miễn phí.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần nhập liệu thủ công, phân tích nhanh chóng trong vài giây.
- **Dữ liệu chính xác & toàn diện**: Thu thập từ API Semrush (mockup) bao gồm traffic, DA/PA, backlinks và phân tích đối thủ.
- **Ghi log tự động**: Tất cả kết quả được ghi vào Google Sheets theo cấu trúc rõ ràng, dễ theo dõi.
- **Cá nhân hóa**: Thêm trường `country` (nếu cần) để phân tích lưu lượng theo quốc gia.
- **Hoạt động liên tục**: Workflow chạy 24/7 trên VPS, không phụ thuộc vào phiên bản miễn phí của n8n.io.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản RapidAPI** (để sử dụng API mockup của Semrush):
   - [Đăng ký tài khoản miễn phí RapidAPI](https://rapidapi.com/) (nếu chưa có).
   - **API Keys** cho các endpoint:
     - `webtraffic.php` (lưu lượng truy cập).
     - `dapa.php` (DA/PA, spam score).
     - `backlink.php` (backlinks).
     - `competitor.php` (phân tích đối thủ).
   - *Lưu ý*: Workflow sử dụng **API mockup** (không cần trả phí), nhưng các sếp có thể thay thế bằng API thực của Semrush nếu có.

2. **Tài khoản Google Cloud Platform (GCP)**:
   - [Tạo tài khoản Google Cloud](https://cloud.google.com/) và **bật Google Sheets API**.
   - **Tạo Service Account** và **JSON Key File** để kết nối với Google Sheets.
   - **Cấu hình credentials** trong n8n với tên `googleApi` (sẽ được hướng dẫn chi tiết sau).

3. **Google Sheets**:
   - Tạo một **bộ Google Sheets mới** với **4 tab** có tên:
     - `Website Traffic`
     - `DA PA`
     - `Backlinks Overview`
     - `Backlinks & Competitor Analysis`
   - **Chia sẻ sheet** với quyền **Editor** cho service account của Google.

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow bằng **2 cách**:
- **Tải file JSON** từ [n8n.io/workflows/7367](https://n8n.io/workflows/7367) và import vào n8n Editor.
- **Copy/paste JSON** từ link trên vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Sau khi import, các sếp cần **cấu hình lại các node quan trọng** như sau:

##### **A. Cấu hình Node `formTrigger` (On form submission)**
- **Thay đổi URL của form** (nếu muốn host riêng):
  - Mở node `On form submission` → Tab **Advanced** → Thay đổi `url` thành URL của trang web cá nhân (ví dụ: `https://tên-domain.com/seo-form`).
  - *Lưu ý*: Nếu không thay đổi, form sẽ được host trên n8n.io (không khuyến nghị cho dữ liệu nhạy cảm).

##### **B. Cấu hình Node `httpRequest` (API RapidAPI)**
Tất cả các node `httpRequest` (từ `Website Traffic Cheker` đến `Competitors Analysis`) cần **điền API Key** và **URL API**:
1. Mở node `Website Traffic Cheker`:
   - Tab **Credentials** → Chọn `rapidApi` (nếu đã tạo credentials trước đó).
   - Tab **Request Configuration**:
     - **Method**: `POST`
     - **URL**: `https://webtraffic.php` (đây là URL mockup, các sếp có thể thay thế bằng API thực của Semrush).
     - **Headers**:
       ```
       {
         "Content-Type": "application/json",
         "X-RapidAPI-Key": "{{$json["rapidApiKey"]}}"
       }
       ```
     - **Body**:
       ```json
       {
         "website": "{{$json["website"]}}",
         "country": "{{$json["country"] || "US"}}"
       }
       ```
2. **Lặp lại cho các node khác**:
   - `Website Metrics DA PA`: Thay đổi URL thành `https://dapa.php`.
   - `Top Baclinks`: Thay đổi URL thành `https://backlink.php`.
   - `Competitors Analysis`: Thay đổi URL thành `https://competitor.php`.

   *Lưu ý*: Nếu sử dụng **API thực của Semrush**, các sếp cần:
   - Đăng ký API key tại [Semrush API](https://developers.semrush.com/).
   - Thay đổi URL thành các endpoint chính thức (ví dụ: `https://api.semrush.com/...`).

##### **C. Cấu hình Node `googleSheets`**
Tất cả các node `googleSheets` (từ `DA PA` đến `Competitor Analysis`) cần **điền credentials**:
1. Mở node `DA PA`:
   - Tab **Credentials** → Chọn `googleApi` (credentials đã tạo trước đó).
   - Tab **Request Configuration**:
     - **Spreadsheet ID**: Lấy từ URL của Google Sheets (ví dụ: `1AbCdEfGhIjKlMnOpQrStUvWxYz`).
     - **Sheet Name**: Điền tên tab tương ứng (`DA PA`, `Website Traffic`, v.v.).
     - **Range**: Điền `A1` (n8n sẽ tự động append dữ liệu từ hàng 1).
     - **Headers**: Điền các tiêu đề cột (ví dụ: `Website, Visits, Users, Bounce Rate` cho tab `Website Traffic`).

   *Lưu ý*: Các sếp cần **điền tiêu đề cột** cho mỗi tab trong Google Sheets trước khi chạy workflow.

##### **D. Cấu hình Node `code` (Re-Format)**
Các node `code` (từ `Re-Format` đến `Re-Format 5`) **không cần chỉnh sửa** nếu sử dụng JSON gốc. Tuy nhiên, nếu cần thay đổi logic:
1. Mở node `Re-Format`:
   - Tab **Code**:
     ```javascript
     // Ví dụ: Trích xuất dữ liệu từ traffic API
     return {
       json: {
         visits: data.semrushAPI.trafficSummary[0].visits,
         users: data.semrushAPI.trafficSummary[0].users,
         bounceRate: data.semrushAPI.trafficSummary[0].bounceRate,
       }
     };
     ```
   - *Lưu ý*: Các sếp có thể **xem code chi tiết** trong file JSON gốc và chỉnh sửa nếu cần.

##### **E. Cấu hình `Global Storage`**
- Node này **không cần chỉnh sửa**, nhưng các sếp có thể thêm trường `country` vào form nếu muốn phân tích theo quốc gia.

---

#### **3. Kích hoạt ⚡️**
1. **Test run dữ liệu mẫu**:
   - Nhập một URL website vào form (ví dụ: `https://example.com`).
   - Chạy workflow và kiểm tra **Google Sheets** để xem dữ liệu đã ghi log chưa.
   - *Lưu ý*: Nếu gặp lỗi, kiểm tra:
     - API Key có đúng không?
     - Google Sheets có chia sẻ quyền Editor cho service account không?
     - Các tab trong Google Sheets có tên đúng không?

2. **Bật Active workflow**:
   - Sau khi test thành công, chuyển workflow sang **Active**.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Thêm trường `country` vào form**:
   - Mở node `formTrigger` → Tab **Advanced** → Thêm trường `country` (dropdown chọn quốc gia).
   - Cấu hình trong `Global Storage` để lưu `country` vào execution JSON.

2. **Gửi báo cáo định kỳ qua Email/Slack**:
   - Thêm node `n8n-nodes-base.email` hoặc `n8n-nodes-base.slack` sau `Competitor Analysis` để gửi báo cáo tự động hàng tuần.

3. **Lưu log lỗi**:
   - Thêm node `n8n-nodes-base.slack` hoặc `n8n-nodes-base.telegram` để báo lỗi nếu workflow bị crash.

4. **Tích hợp với Google Drive**:
   - Thêm node `n8n-nodes-base.googleDrive` để lưu bản sao lưu của Google Sheets hàng ngày.

5. **Tự động phân tích nhiều website**:
   - Sử dụng node `n8n-nodes-base.set` để lưu danh sách website vào `Global Storage` và chạy workflow cho từng URL.

---

### 📌 **Kết luận**
Workflow **Automated On-Page SEO Analysis** là **giải pháp hoàn hảo** cho các sếp Marketing & SEO muốn **tự động hóa phân tích website** mà không cần viết code. Với chỉ **một form nhập URL**, workflow sẽ:
✔ Thu thập **tất cả dữ liệu SEO quan trọng** (traffic, DA/PA, backlinks, đối thủ).
✔ **Ghi log tự động** vào Google Sheets theo cấu trúc rõ ràng.
✔ **Tiết kiệm thời gian** và giảm thiểu lỗi so với cách làm thủ công.

**Hành động ngay!**
1. Import workflow vào n8n.
2. Cấu hình API Key và Google Sheets.
3. Nhập URL website đầu tiên và **xem kết quả tự động hóa!**

👉 [Tải workflow JSON](https://n8n.io/workflows/7367) và bắt đầu tự động hóa SEO của bạn!