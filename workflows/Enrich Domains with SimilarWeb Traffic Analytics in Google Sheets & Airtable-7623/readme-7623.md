---
title: "🚀 Tự động làm giàu dữ liệu tên miền (Domain Enrichment) với SimilarWeb Traffic Analytics trên Google Sheets và Airtable"
description: "Hướng dẫn xây dựng workflow n8n tự động lấy dữ liệu lưu lượng truy cập từ SimilarWeb API khi có domain mới trên Google Sheets, sau đó đồng bộ kết quả về Google Sheets và Airtable."
slug: "tu-dong-lam-giau-du-lieu-ten-mien-similarweb-google-sheets-airtable"
tags: [n8n, automation, similarweb, google-sheets, airtable, market-research]
keywords: [n8n workflow, similarweb api, domain enrichment, tự động hóa marketing, google sheets n8n]
---

# 🚀 Tự động làm giàu dữ liệu tên miền với SimilarWeb Traffic Analytics

Việc nghiên cứu đối thủ cạnh tranh, phân tích thị trường hoặc chấm điểm khách hàng tiềm năng (Lead Scoring) dựa trên lượng truy cập website thường ngốn rất nhiều thời gian thủ công. Các sếp thường phải copy từng tên miền, tra cứu trên SimilarWeb, rồi lại copy-paste các chỉ số như Global Rank, tổng lượt truy cập, thời gian trên trang... vào Google Sheets hoặc Airtable.

Bài toán này sẽ được giải quyết triệt để 100% tự động bằng workflow n8n do **Avkash Kakdiya** (iTechNotion) xây dựng. Ngay khi các sếp thêm một tên miền mới vào Google Sheets, hệ thống sẽ tự động gọi SimilarWeb API, bóc tách các chỉ số traffic cốt lõi và cập nhật ngược lại vào Google Sheets cũng như đồng bộ sang Airtable.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Không cần thao tác thủ công, chỉ cần nhập tên miền vào Google Sheets.
- **Dữ liệu traffic chi tiết:** Tự động lấy các chỉ số đắt giá như Xếp hạng toàn cầu (Global Rank), Xếp hạng quốc gia, Tổng lượt truy cập hàng tháng, Tỷ lệ thoát (Bounce Rate)...
- **Đa nền tảng:** Dữ liệu sau khi làm giàu (enriched) được cập nhật đồng thời vào Google Sheets và lưu trữ dự phòng tại Airtable.
- **Tối ưu thời gian nghiên cứu:** Giúp đội ngũ Sales và Marketing chấm điểm và lọc danh sách khách hàng tiềm năng cực kỳ nhanh chóng.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ TRƯỚC KHI BẮT ĐẦU]
- **Tài khoản n8n** (Self-hosted hoặc n8n Cloud).
- **Google Sheets:** File chứa danh sách tên miền cần phân tích.
- **SimilarWeb API Key:** Tài khoản SimilarWeb có quyền truy cập API để lấy dữ liệu lưu lượng truy cập.
- **Airtable Account:** (Tùy chọn) Nếu các sếp muốn đồng bộ dữ liệu sang cơ sở dữ liệu Airtable.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ trang chính thức của n8n (ID: `7623`) và import trực tiếp vào n8n Editor của mình bằng cách chọn **Add workflow** -> **Import from File**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động trơn tru, các sếp cần cấu hình chính xác các node sau:

1. **🟢 Sheet Trigger: New Domain (`googleSheetsTrigger`)**:
   - Kết nối tài khoản Google thông qua **OAuth2**.
   - Chọn đúng file Google Sheets và trang tính (Sheet Name) dùng để theo dõi danh sách tên miền mới.

2. **🧼 Clean Domain URL (`set`)**:
   - Node này có nhiệm vụ chuẩn hóa định dạng URL (loại bỏ `https://`, `www`, dấu `/` ở cuối) để SimilarWeb API có thể đọc chính xác.

3. **🌐 Fetch Analysis (SimilarWeb API) (`httpRequest`)**:
   - Cấu hình phương thức gọi API tới SimilarWeb.
   - Thêm SimilarWeb API Key vào phần Header hoặc Authentication của yêu cầu HTTP.

4. **📊 Extract Key Traffic Metrics (`code`)**:
   - Node JavaScript này giúp bóc tách và lọc ra các chỉ số quan trọng từ JSON thô của SimilarWeb như: *Global Rank, Country Rank, Monthly Visits, Avg Visit Duration, Top Traffic Sources, Device Split*.

5. **📤 Update Sheet with Traffic Data (`googleSheets`)**:
   - Kết nối tài khoản Google Sheets.
   - Chọn thao tác (operation) là **Update** để ghi đè hoặc bổ sung các chỉ số traffic vừa phân tích vào đúng dòng chứa tên miền đó.

6. **📁 Export to Airtable (Optional) (`airtable`)**:
   - Nếu không dùng Airtable, các sếp có thể tắt (disable) hoặc xóa node này.
   - Nếu dùng, hãy cấu hình Base và Table tương ứng, chọn operation là **Create** để lưu trữ log dữ liệu.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và thêm thử một tên miền vào Google Sheets để kiểm tra log hoạt động.
- Nếu dữ liệu trả về chính xác, hãy gạt công tắc sang **Active** để hệ thống tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Thêm node Telegram hoặc Slack ở cuối workflow để bắn thông báo về máy mỗi khi một tên miền mới được phân tích thành công.
- **Xử lý lỗi (Error Handling):** Thêm Error Trigger để bắt trường hợp SimilarWeb API trả về lỗi (do tên miền không tồn tại hoặc hết quota) nhằm tránh làm gián đoạn workflow.
- **Lưu trữ lịch sử:** Thay vì chỉ update dòng cũ, các sếp có thể cấu hình lưu thành một lịch sử theo tháng để theo dõi sự tăng trưởng traffic của đối thủ qua thời gian.

### 📌 Kết luận
Workflow Enrich Domains with SimilarWeb là một trợ thủ đắc lực cho các nhà quản lý, đội ngũ Growth Hacking và Sales trong việc tự động hóa quá trình nghiên cứu thị trường. Hãy triển khai ngay để tiết kiệm hàng chục giờ làm việc thủ công mỗi tuần!