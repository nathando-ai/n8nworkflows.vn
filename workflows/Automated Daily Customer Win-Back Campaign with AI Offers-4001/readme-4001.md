---
title: "🚀 **Tự Động Hóa Chiến Dịch Win-Back Khách Hàng Hàng Ngày Với AI - Giảm Churn 30% Miễn Code**"
description: "Workflow tự động hóa hoàn toàn bằng n8n giúp các sếp phát hiện và phục hồi khách hàng có nguy cơ rời đi (churn) bằng cách gửi đề nghị khuyến mãi cá nhân hóa hàng ngày. Giảm thiểu mất mát doanh thu, tăng trải nghiệm khách hàng và tối ưu hóa thời gian marketing chỉ với 10 phút cấu hình."
slug: "tieu-dong-hoa-chien-dich-win-back-khach-hang-voi-ai"
tags: [n8n, automation, marketing-ai, no-code, google-sheets, gmail-integration]
keywords: [tự động hóa win-back khách hàng, giảm churn bằng AI, n8n workflow marketing, tự động hóa email cá nhân hóa, AI khuyến mãi tự động]
---

# 🚀 **Tự Động Hóa Chiến Dịch Win-Back Khách Hàng Hàng Ngày Với AI - Khôi Phục Khách Hàng Trước Khi Họ Rời Đi**

## **💡 Nỗi Đau Của Các Sếp: Khách Hàng Rời Đi Mà Chưa Kịp Phục Hồi**
Bạn đã bao giờ cảm thấy **không kịp thời** để phục hồi khách hàng đang có nguy cơ rời đi (churn) vì quá bận với công việc hàng ngày? Hay **không biết cách** tạo ra đề nghị khuyến mãi cá nhân hóa mà vẫn tiết kiệm chi phí? Với **Automated Daily Customer Win-Back Campaign**, các sếp sẽ:
- **Phát hiện khách hàng có nguy cơ rời đi** dựa trên dữ liệu hành vi mua hàng (chỉ trong 1 phút).
- **Tạo đề nghị khuyến mãi AI** phù hợp với từng khách hàng (được tối ưu hóa bởi **Google Gemini**).
- **Gửi email tự động** với nội dung cá nhân hóa, **không cần viết code** hay thuê nhân viên marketing.
- **Giảm tỷ lệ churn** lên đến **30%** chỉ trong vài tuần, đồng thời **tiết kiệm thời gian** lên đến **20 giờ/tuần**.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **liên tục 24/7** mà không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng. Với chi phí thấp, các sếp sẽ có hệ thống **ổn định, an toàn và không phụ thuộc vào cloud miễn phí** (có thể bị ngắt kết nối bất kỳ lúc nào).
👉 **[Đăng ký VPS TinoHost - Giảm 39%](https://tino.vn/vps-n8n?affid=388)** (Mã giảm giá: **VPSN8N**)
👉 **[VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (Đảm bảo tốc độ cao, phù hợp cho AI)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Giảm tỷ lệ churn** lên đến **30%** trong 30 ngày đầu tiên (dựa trên dữ liệu thực tế từ các doanh nghiệp sử dụng).
✅ **Tiết kiệm thời gian** lên đến **20 giờ/tuần** (không cần phải thủ công lọc khách hàng và viết email).
✅ **Cá nhân hóa hoàn toàn** mỗi đề nghị khuyến mãi dựa trên **lịch sử mua hàng, điểm số churn và sở thích** của khách.
✅ **Hoạt động tự động 24/7** mà không cần can thiệp của con người.
✅ **Dữ liệu theo dõi chi tiết** trong Google Sheets để phân tích hiệu quả chiến dịch.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets** (để lưu trữ dữ liệu khách hàng và log hoạt động).
   - **Sheet 1:** "Customer Data" (dữ liệu khách hàng với các trường như `customer_id`, `predicted_churn_score`, `preferred_categories`, `user_mail`).
   - **Sheet 2:** "SYSTEM_LOG" (để ghi log tất cả hoạt động của workflow).
2. **Tài khoản Gmail** (để gửi email khuyến mãi tự động).
3. **API Key Google Gemini** (để sử dụng AI tạo đề nghị khuyến mãi).
   - **Lấy API Key:** [Google AI Studio](https://makersuite.google.com/app/apikey)
4. **Dữ liệu khách hàng** (các sếp cần chuẩn bị **trường dữ liệu chính xác** như trong **Example Customer Data** dưới đây).

---
:::info[CHUẨN BỊ DỮ LIỆU KHÁCH HÀNG]
Dữ liệu khách hàng phải có **các trường sau** để workflow hoạt động:
```json
{
  "customer_id": "CUST_001",
  "last_purchase_date": "2024-01-10T10:00:00Z",
  "purchase_frequency_days": 90,
  "user_mail": "example@mail.com",
  "days_since_last_purchase": 110,
  "total_spent_usd": 55.0,
  "preferred_categories": ["Kitap", "Ofis Malzemeleri"],
  "predicted_churn_score": 0.85,
  "profile_tags": ["inactive_long_time", "low_spender"]
}
```
- **`predicted_churn_score`** (giá trị từ 0 đến 1, càng cao càng nguy cơ rời đi).
- **`preferred_categories`** (danh sách danh mục sản phẩm khách hàng thích).
- **`user_mail`** (email để gửi đề nghị khuyến mãi).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow này:
- **Tải file JSON** từ [n8n.io/workflows/4001](https://n8n.io/workflows/4001) và import vào **n8n Editor**.
- **Copy JSON** từ trang trên và **dán vào n8n Editor** (tab "Import").

👉 **Hướng dẫn chi tiết:**
1. Mở **n8n Editor** (trang chủ của n8n).
2. Nhấn **"Import"** ở góc trên bên phải.
3. Chọn **"From JSON"** và dán nội dung JSON từ [đây](https://n8n.io/workflows/4001).
4. Nhấn **"Import"** để workflow xuất hiện trên canvas.

---

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Sau khi import, các sếp cần **cấu hình lại các node quan trọng** như sau:

##### **🔹 Node 1: Scheduled Start (Bắt Đầu Hàng Ngày)**
- **Thiết lập lịch chạy:** Chọn **"Daily"** và thời gian phù hợp (ví dụ: **8h sáng** để không làm phiền khách hàng).
- **Lưu ý:** Nếu muốn chạy **ngày nào cũng được**, có thể chọn **"Every 24 hours"**.

##### **🔹 Node 2: Fetch Customer Data from Sheet (Lấy Dữ liệu Khách Hàng)**
- **Chọn Google Sheets Credentials:** Chọn **"googleSheetsOAuth2Api"** (đã cấu hình trước khi import).
- **Thiết lập Sheet Name:** Điền tên **exact** của sheet chứa dữ liệu khách hàng (**"Customer Data"**).
- **Range:** Điền `"Customer Data!A1:Z"` (hoặc điều chỉnh theo cột dữ liệu thực tế).

##### **🔹 Node 3: Filter High Churn Risk & No Campaign Customers (Lọc Khách Hàng Có Nguy Cơ Rời Đi)**
- **Cấu hình điều kiện lọc:**
  - `predicted_churn_score > 0.7` (khách hàng có nguy cơ cao rời đi).
  - `created_campaign_date` **không tồn tại** (khách hàng chưa được gửi đề nghị trước đó).
- **Lưu ý:** Nếu trường `created_campaign_date` không tồn tại, các sếp cần **thêm trường này vào sheet** và **điền giá trị rỗng** cho khách hàng chưa được gửi email.

##### **🔹 Node 4: Generate Win-Back Offer (Tạo Đề Nghị Khuyến Mãi Bằng AI)**
- **Cấu hình Prompt cho Google Gemini:**
  - Các sếp **không cần chỉnh sửa** nếu muốn sử dụng **prompt mặc định** (đã tối ưu hóa).
  - Nếu muốn **cải thiện chất lượng đề nghị**, có thể thay đổi prompt như sau:
    ```json
    "prompt": "Tạo một đề nghị khuyến mãi cá nhân hóa cho khách hàng có nguy cơ rời đi. Dựa trên các thông tin sau:
    - Khách hàng ID: {{$node["Fetch Customer Data from Sheet"].json["customer_id"]}}
    - Điểm số nguy cơ rời đi: {{$node["Fetch Customer Data from Sheet"].json["predicted_churn_score"]}}
    - Danh mục sản phẩm ưa thích: {{$node["Fetch Customer Data from Sheet"].json["preferred_categories"]}}
    - Tổng tiền đã tiêu: {{$node["Fetch Customer Data from Sheet"].json["total_spent_usd"]}}

    Đề nghị phải bao gồm:
    1. Tiêu đề hấp dẫn (ví dụ: 'Đặc biệt dành cho bạn: 20% giảm giá trên danh mục yêu thích!')
    2. Nội dung khuyến mãi (đặc biệt, bonus điểm, hoặc giảm giá)
    3. Lời kêu gọi hành động (CTA) rõ ràng (ví dụ: 'Nhấp vào đây để kích hoạt ngay!')
    4. Thời hạn áp dụng (ví dụ: 'Chỉ áp dụng trong 7 ngày đầu tiên')

    Trả về kết quả dưới dạng JSON với các trường:
    {
      "offer_title": "string",
      "offer_details": "string",
      "expiry_date": "YYYY-MM-DD",
      "discount_type": "string"
    }"
    ```
- **Chọn Credentials:** Chọn **"googlePalmApi"** (API Key Google Gemini đã cấu hình trước).

##### **🔹 Node 5: Send Win-Back Offer via Email (Gửi Email Khuyến Mãi)**
- **Chọn Gmail Credentials:** Chọn **"gmailOAuth2"** (tài khoản Gmail đã liên kết).
- **Thiết lập Email Template:**
  - **Subject:** `{{$json["offer_title"]}} - Đặc biệt dành cho bạn!`
  - **Body HTML:** Các sếp có thể sử dụng **template mặc định** hoặc tùy chỉnh như sau:
    ```html
    <h2>{{$json["offer_title"]}}</h2>
    <p>{{$json["offer_details"]}}</p>
    <p><strong>Thời hạn áp dụng:</strong> {{$json["expiry_date"]}}</p>
    <p><a href="https://your-website.com/claim-offer?code={{$node["Fetch Customer Data from Sheet"].json["customer_id"]}}">Kích hoạt khuyến mãi ngay!</a></p>
    ```
- **Lưu ý:** Đảm bảo **đường link** trong email dẫn đến trang web hợp lệ.

##### **🔹 Node 6 & 7: Log 'Not Found' (Ghi Log Nếu Không Tìm Thấy Khách Hàng)**
- **Không cần chỉnh sửa** nếu muốn sử dụng **log mặc định**.
- **Sheet Name:** Đảm bảo **"SYSTEM_LOG"** tồn tại và có **các cột** như `timestamp`, `status`, `customer_id`.

---

#### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run (Kiểm Tra Dữ liệu Mẫu):**
   - Nhấn **"Run"** trên node **"Scheduled Start"** để kiểm tra workflow với **dữ liệu mẫu**.
   - Kiểm tra **email** và **Google Sheets** để đảm bảo:
     - Email được gửi đúng.
     - Dữ liệu được ghi log chính xác.
2. **Bật Active:**
   - Sau khi test thành công, **bật "Active"** trên node **"Scheduled Start"**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[CÁCH TIẾP CẬN THÊM]
1. **Kết Nối Với Slack/Telegram:**
   - Thêm **node Slack/Telegram** sau **"Send Win-Back Offer"** để **báo cáo ngay khi email được gửi thành công**.
   - **Cài đặt:** Tạo **webhook** từ Slack/Telegram và thêm node **"Slack Webhook"** hoặc **"Telegram Bot"**.

2. **Lưu Log Chi Tiết Hơn:**
   - Thêm **cột mới** vào **"SYSTEM_LOG"** như:
     - `offer_sent`: `YES/NO`
     - `email_status`: `SUCCESS/FAILED`
   - Sử dụng **node "Set"** để cập nhật trạng thái.

3. **Tự Động Gửi Báo Cáo Hàng Tuần:**
   - Thêm **node "Schedule Trigger"** mới để chạy **tối thứ 7** và gửi **báo cáo tổng hợp** về:
     - Số lượng khách hàng được phục hồi.
     - Tỷ lệ mở email.
     - Doanh thu từ khuyến mãi.

4. **Tối Ưu Hóa AI với Prompt Tùy Chỉnh:**
   - Nếu muốn **đề nghị khuyến mãi phù hợp với mùa vụ**, các sếp có thể **cập nhật prompt** để bao gồm:
     ```json
     "season": "summer" // hoặc "winter", "holiday"
     ```
   - Ví dụ:
     ```json
     "prompt": "Tạo đề nghị khuyến mãi mùa hè cho khách hàng..."
     ```

5. **Phân Loại Khách Hàng Theo Điểm Số Churn:**
   - Sử dụng **node "Filter"** thêm để phân loại khách hàng:
     - **Churn Score > 0.9:** Đề nghị **giảm giá 30%**.
     - **Churn Score 0.7-0.9:** Đề nghị **bonus điểm**.
     - **Churn Score < 0.7:** Đề nghị **miễn phí vận chuyển**.

---

### 📌 **Kết Luận: Bắt Đầu Tự Động Hóa Win-Back Khách Hàng Ngay Hôm Nay!**
Với **Automated Daily Customer Win-Back Campaign**, các sếp đã có **công cụ hoàn hảo** để:
✔ **Phục hồi khách hàng trước khi họ rời đi** (giảm churn).
✔ **Tiết kiệm thời gian** cho đội ngũ marketing.
✔ **Tăng doanh thu** từ khách hàng cũ.

**Bước đầu tiên:** Import workflow và **cấu hình theo