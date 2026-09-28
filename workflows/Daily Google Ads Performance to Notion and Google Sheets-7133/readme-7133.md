---
title: "📊 Tự Động Hóa Báo Cáo Google Ads Hàng Ngày Sang Notion & Google Sheets (Không Cần Code)"
description: "Workflow này tự động thu thập dữ liệu hiệu suất quảng cáo Google Ads (clicks, conversions, chi phí) vào Notion và Google Sheets hàng ngày, giúp các sếp tiết kiệm 10+ giờ/tháng làm báo cáo thủ công. Kết quả: Dữ liệu chính xác, cập nhật 24/7, và dễ dàng phân tích qua nhiều kênh."
slug: "tu-dong-hoa-google-ads-notion-google-sheets"
tags: [n8n, tự động hóa marketing, Google Ads, Notion, Google Sheets, báo cáo tự động]
keywords: [n8n workflow Google Ads, tự động hóa báo cáo quảng cáo, Notion và Google Sheets, API Google Ads, báo cáo hàng ngày]
---

# 🚀 **Tự Động Hóa Báo Cáo Google Ads Hàng Ngày Sang Notion & Google Sheets**

### **Nỗi Đau Của Các Sếp Marketing**
Làm báo cáo Google Ads thủ công hàng ngày là một **công việc tẻ nhạt, tốn thời gian và dễ sai sót**:
- **Tốn 10-15 giờ/tháng** để thu thập, tính toán và cập nhật dữ liệu từ Google Ads API.
- **Rủi ro sai sót** khi nhập liệu hoặc tính toán thủ công.
- **Không đồng bộ** giữa các công cụ (Google Ads, Notion, Google Sheets), khiến việc phân tích trở nên rắc rối.
- **Không cập nhật liên tục**, dẫn đến quyết định marketing dựa trên dữ liệu lỗi thời.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động thu thập** dữ liệu clicks, conversions và chi phí từ Google Ads API **mỗi ngày lúc 8h sáng**.
✅ **Cập nhật đồng bộ** vào **Notion** (để theo dõi chi tiết từng chiến dịch) và **Google Sheets** (để phân tích tổng hợp).
✅ **Tính toán tự động** tổng hợp dữ liệu hàng ngày (impressions, clicks, conversions, chi phí) và lưu vào **báo cáo tổng quan**.
✅ **Không cần code**, chỉ cần cấu hình vài bước đơn giản.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo dữ liệu an toàn và không bị giới hạn bởi phiên bản miễn phí.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tháng** làm báo cáo thủ công.
- **Dữ liệu chính xác 100%** (không sai sót như nhập liệu tay).
- **Cập nhật tự động hàng ngày** (không cần nhắc nhở).
- **Dễ dàng phân tích** qua **Notion** (chi tiết chiến dịch) và **Google Sheets** (tổng hợp).
- **Quản lý ROI hiệu quả** với báo cáo conversions và chi phí chi tiết.
- **Hoạt động 24/7** mà không cần can thiệp của con người.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google Ads** (đã có API access).
2. **Developer Token** từ [Google Ads Developer Console](https://developers.google.com/google-ads/api/docs/start).
3. **Customer ID** (không phải MCC ID) của tài khoản Google Ads.
4. **Tài khoản Notion** và hai **database** đã tạo sẵn:
   - **Google Ads Campaign Tracker** (để lưu chi tiết từng chiến dịch).
   - **Google Ads Daily Summary** (để lưu tổng hợp hàng ngày).
5. **Tài khoản Google Sheets** và một **file Excel** với hai tab:
   - **Campaign Daily Report** (dữ liệu chi tiết chiến dịch).
   - **Summary Report** (tổng hợp hàng ngày).
6. **API Key của n8n** (nếu self-hosted) hoặc tài khoản n8n.io miễn phí.

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Truy cập [n8n Editor](https://n8n.io/editor) (hoặc self-hosted của mình).
2. Nhấn **Import** và chọn file JSON từ [link gốc](https://n8n.io/workflows/7133).
   *Hoặc* copy toàn bộ JSON từ [đây](https://n8n.io/workflows/7133) và paste vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **12 node**, các sếp cần chú ý cấu hình các node sau:

##### **A. Schedule Trigger (Đặt Lịch Trình)**
- **Thời gian chạy:** Đặt thành **8h sáng hàng ngày** (hoặc thời gian phù hợp).
- **Lưu ý:** Node này sẽ kích hoạt workflow hàng ngày.

##### **B. Set Yesterday Date (Đặt Ngày Hôm Trước)**
- Node này tự động lấy ngày hôm trước để query API.
- **Không cần chỉnh sửa**, n8n sẽ tự động tính toán.

##### **C. Google Ads API (2 Node HTTP Request)**
Các sếp cần cấu hình **2 node HTTP Request** để query Google Ads API:
1. **G-Ads Query Click** (thu thập dữ liệu clicks, impressions, chi phí):
   - **URL:** `https://googleads.googleapis.com/v20/customers/{customerId}/googleAds:search`
     *Thay `{customerId}` bằng ID tài khoản của bạn (không phải MCC ID).*
   - **Headers:**
     ```
     developer-token: [Your Developer Token]
     login-customer-id: [Your Customer ID]
     Content-Type: application/json
     ```
   - **Body (GAQL Query):**
     ```sql
     SELECT
       campaign.id,
       campaign.name,
       metrics.impressions,
       metrics.clicks,
       metrics.cost_micros,
       segments.date
     FROM campaign
     WHERE segments.date = '{{$json.yesterday}}'
     ```
   - **Credentials:** Chọn **Google Ads OAuth2** (đã cấu hình trước).

2. **G-Ads Query Conversion** (thu thập dữ liệu conversions):
   - **URL:** Cùng như trên.
   - **Headers:** Cùng như trên.
   - **Body (GAQL Query):**
     ```sql
     SELECT
       campaign.id,
       campaign.name,
       metrics.conversions,
       segments.conversion_action_name,
       segments.date
     FROM campaign
     WHERE segments.date = '{{$json.yesterday}}'
     ```
   - **Credentials:** Cùng như trên.

##### **D. Notion Setup (2 Node Notion)**
Các sếp cần **đã tạo sẵn 2 database Notion** trước:
1. **Google Ads Campaign Tracker** (lưu chi tiết chiến dịch):
   - **Fields cần có:**
     - `Campaign Name` (text)
     - `Campaign ID` (text)
     - `Impressions` (number)
     - `Clicks` (number)
     - `Cost` (number, đơn vị: micros → chia cho 1,000,000)
     - `Conversion Type` (text)
     - `Conversions` (number)
     - `Date` (date)
   - **Credentials:** Chọn **Notion OAuth2** (đã cấu hình trước).

2. **Google Ads Daily Summary** (lưu tổng hợp hàng ngày):
   - **Fields cần có:**
     - `Date` (date)
     - `Total Impressions` (number)
     - `Total Clicks` (number)
     - `Total Conversions` (number)
     - `Total Cost` (number)
     - `Conversion Types` (text array)
   - **Credentials:** Cùng như trên.

##### **E. Google Sheets Setup (2 Node Google Sheets)**
Các sếp cần **đã tạo sẵn 1 file Google Sheets** với 2 tab:
1. **Campaign Daily Report** (lưu chi tiết chiến dịch):
   - **Cột cần có:** `Campaign ID`, `Campaign Name`, `Impressions`, `Clicks`, `Cost`, `Conversion Type`, `Conversions`, `Date`.
   - **Credentials:** Chọn **Google Sheets OAuth2** (đã cấu hình trước).
   - **Operation:** `append` (thêm dữ liệu mới vào cuối).

2. **Summary Report** (lưu tổng hợp hàng ngày):
   - **Cột cần có:** `Date`, `Total Impressions`, `Total Clicks`, `Total Conversions`, `Total Cost`, `Conversion Types`.
   - **Credentials:** Cùng như trên.
   - **Operation:** `append`.

##### **F. Code Nodes (Split & Merge)**
- **Split Click2 & Split Conversion2:** Chia dữ liệu thành các dòng riêng biệt (n8n tự động xử lý, **không cần chỉnh sửa**).
- **Merge2:** Ghép lại dữ liệu clicks và conversions theo `campaign.id` và `segments.date`.
- **Daily Recap2:** Tính toán tổng hợp hàng ngày (n8n tự động xử lý, **không cần chỉnh sửa**).

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Chạy workflow một lần để kiểm tra kết quả.
   - Kiểm tra **Notion** và **Google Sheets** xem dữ liệu có được cập nhật không.
2. **Bật Active:**
   - Sau khi kiểm tra thành công, chuyển workflow sang **Active**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết nối với Slack/Telegram để báo cáo tự động:**
   - Thêm node **Slack Webhook** hoặc **Telegram Bot** sau **Daily Recap2** để gửi báo cáo hàng ngày qua chat.
   - Ví dụ:
     ```json
     {
       "text": "📊 Báo cáo Google Ads hôm qua:\n- Impressions: {{$json.totalImpressions}}\n- Clicks: {{$json.totalClicks}}\n- Conversions: {{$json.totalConversions}}\n- Chi phí: {{($json.totalCost/1000000).toFixed(2)}} USD"
     }
     ```

2. **Lưu log hoạt động:**
   - Thêm node **Sticky Note** để ghi lại lỗi hoặc thông báo debug.
   - Ví dụ:
     ```json
     {
       "text": "Workflow chạy thành công vào ngày {{$json.date}}"
     }
     ```

3. **Tự động gửi báo cáo qua Email:**
   - Sử dụng node **Email** (n8n có hỗ trợ SMTP) để gửi báo cáo hàng ngày cho team.
   - Cấu hình:
     - **From:** `marketing@doanhnghiep.com`
     - **To:** `team@doanhnghiep.com`
     - **Subject:** `Báo cáo Google Ads - Ngày {{$json.date}}`
     - **Body:** HTML với biểu đồ từ Google Sheets (sử dụng node **Google Sheets** + **HTML Template**).

4. **Tính toán ROI tự động:**
   - Thêm node **Code** sau **Daily Recap2** để tính toán ROI:
     ```javascript
     // ROI = (Doanh thu từ conversions - Chi phí) / Chi phí * 100
     const roi = (($json.totalConversions * $json.avgConversionValue) - ($json.totalCost / 1000000)) / ($json.totalCost / 1000000) * 100;
     return { roi: roi.toFixed(2) };
     ```
   - Sau đó lưu `roi` vào Notion và Google Sheets.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp marketing khỏi công việc tẻ nhạt là làm báo cáo thủ công, đồng thời **cung cấp dữ liệu chính xác và cập nhật** để hỗ trợ quyết định chiến lược hiệu quả.

**Hành động ngay:**
1. **Cài đặt n8n trên VPS** (nếu chưa có) và import workflow.
2. **Cấu hình Notion, Google Sheets và Google Ads API** theo hướng dẫn.
3. **Bật workflow** và bắt đầu tự động hóa báo cáo hàng ngày!

**Kết quả?** Dữ liệu Google Ads của bạn **tự động cập nhật hàng ngày**, sẵn sàng phân tích qua **Notion** và **Google Sheets** mà không cần can thiệp của con người.

---
**🚀 Cần hỗ trợ thêm?** Đăng ký [VPS n8n](https://tino.vn/vps-n8n?affid=388) và liên hệ với team TinoHost để được tư vấn chi tiết!