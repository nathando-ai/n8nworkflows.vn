---
title: "📈 **Tự Động Hóa SEO Pulse Hàng Ngày: Bắt Chước Top Keyword Mover Trên Google Search Console (GSC) - Không Cần Code!**"
description: "Workflow này giúp các sếp SEO tự động theo dõi và cảnh báo những keyword/URL có sự thay đổi lớn nhất (tăng/giảm) giữa hai ngày liên tiếp trên Google Search Console, phân loại theo nhóm (brand, non-brand, content) và gửi báo cáo trực tiếp qua Slack. Tiết kiệm 5+ giờ/tháng kiểm tra thủ công!"
slug: "tieu-dong-hoa-seo-pulse-googlesearchconsole"
tags: [n8n, automation, seo, google-search-console, slack-integration, market-research]
keywords: [n8n workflow seo, tự động hóa google search console, cảnh báo keyword mover, báo cáo seo hàng ngày, seo pulse, seo automation]
---

# **🚀 Tự Động Hóa SEO Pulse Hàng Ngày: Bắt Chước Top Keyword Mover Trên Google Search Console (GSC)**

### **🔍 Nỗi Đau Của Các Sếp SEO Hàng Ngày**
Các sếp SEO thường phải:
- **Kiểm tra thủ công** dữ liệu Google Search Console (GSC) hàng ngày để so sánh performance giữa hai ngày liên tiếp.
- **Lọc thủ công** những keyword/URL có sự thay đổi lớn (tăng/giảm) trong clicks, impressions, CTR hoặc vị trí trung bình.
- **Phân loại** dữ liệu theo nhóm (brand, non-brand, content) để phân tích chi tiết.
- **Gửi báo cáo** qua Slack/email cho team, nhưng thường **quên hoặc làm trễ** vì bận công việc khác.

**Kết quả?** Các cơ hội SEO (tăng traffic, mất traffic) bị bỏ lỡ, và team phải mất **5-10 giờ/tuần** để làm việc này thủ công.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
Sau khi áp dụng workflow này, các sếp sẽ:
✅ **Tiết kiệm 5-10 giờ/tháng** không cần kiểm tra GSC thủ công.
✅ **Bắt được top keyword/URL mover** (tăng/giảm) ngay từ sáng hôm sau.
✅ **Phân loại tự động** theo nhóm (brand, non-brand, content) để phân tích nhanh.
✅ **Nhận báo cáo trực tiếp qua Slack** (hoặc email) với dữ liệu sắp xếp theo mức độ ảnh hưởng.
✅ **Cảnh báo kịp thời** về những thay đổi bất ngờ (ví dụ: keyword brand bị mất traffic do update algorithm).
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.

---
### **🔧 Yêu Cầu Cần Thiết**
Để workflow này hoạt động, các sếp cần:
1. **Tài khoản Google Search Console (GSC)** đã kết nối với domain cần theo dõi.
2. **Tài khoản Slack** (hoặc Gmail nếu muốn thay thế Slack bằng email).
3. **API Key Google OAuth 2.0** (để truy cập GSC).
4. **Slack API Token** (nếu muốn gửi báo cáo qua Slack).
5. **Danh sách keyword nhóm** (ví dụ: brand, non-brand, content) để phân loại.

---
### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/6004) hoặc copy/paste JSON từ trang này.
- Mở **n8n Editor** (n8n.io) → Nhấn **"Import"** → Dán JSON → Chọn **"Import"**.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **21 node**, nhưng các phần quan trọng nhất cần chú ý:

##### **A. Cấu Hình Google Search Console (GSC)**
- **Node `priorDay` và `lastDay`** (HTTP Request):
  - **Credentials**: Chọn `"googleOAuth2Api"` (đã cấu hình trước khi import).
  - **URL**: Được tự động lấy từ GSC API (không cần chỉnh).
  - **Query Parameters**:
    - `startDate`: Ngày trước hôm nay (ví dụ: `2024-05-20`).
    - `endDate`: Ngày hôm qua (ví dụ: `2024-05-21`).
    - `dimensions`: `query` (keyword) hoặc `page` (URL).
    - `rowLimit`: `10000` (để lấy đủ dữ liệu).
  - **Lưu ý**:
    - Nếu domain có nhiều keyword/URL, có thể tăng `rowLimit` lên `20000`.
    - **Không cần chỉnh** nếu đã import từ file JSON chính xác.

##### **B. Phân Loại Keyword Theo Nhóm (Segment Switch)**
- **Node `Segment Switch`** (Switch):
  - **Conditions**: Phân loại keyword theo **prefix** (ví dụ: `brand:` → nhóm Brand, `recipe:` → nhóm Content).
  - **Cách chỉnh**:
    1. Mở node `Segment Switch` → Nhấn **"Add Condition"**.
    2. Thêm các điều kiện như:
       - `$.query.includes("brand:")` → Nhóm **Brand**.
       - `$.query.includes("recipe:")` → Nhóm **Content**.
       - `$.query.includes("faq:")` → Nhóm **FAQ**.
    3. **Lưu ý**: Nếu không có nhóm nào phù hợp, có thể **xóa node này** và sử dụng **node `Tag KWs by Category`** (Code) để tự động gán nhãn.

##### **C. Lọc Top Mover (Top Movers Filter)**
- **Node `Top Movers Filter`, `Top Movers Filter1`, `Top Movers Filter2`, `Top Movers Filter3`** (Code):
  - **Logic mặc định**:
    - Lọc keyword/URL có **sự thay đổi >= 100 clicks tuyệt đối** hoặc **>= 30% thay đổi tương đối**.
    - **Cách chỉnh**:
      - Mở node `Top Movers Filter` → Nhấn **"Edit"** → Sửa code theo nhu cầu:
        ```javascript
        // Ví dụ: Lọc keyword có delta clicks >= 50
        if (Math.abs(json["priorDay"]["clicks"] - json["lastDay"]["clicks"]) >= 50) {
          return json;
        }
        return null;
        ```
      - **Lưu ý**: Nếu muốn thay đổi ngưỡng, chỉnh số `50` hoặc `30` trong code tương ứng.

##### **D. Gửi Báo Cáo Qua Slack (Top DoD Movers Alert)**
- **Node `Top DoD Movers Alert`, `Top DoD Movers Alert1`, `Top DoD Movers Alert2`, `Top DoD Movers Alert3`** (Slack):
  - **Credentials**: Chọn `"slackApi"` (đã cấu hình trước).
  - **Message Format**:
    - **Mặc định**: Gửi danh sách top mover theo nhóm (Brand, Non-Brand, Content) với format:
      ```
      🚀 **Top Movers (Brand) - Day Over Day**
      - Keyword: [keyword] | Delta Clicks: +120 | Delta CTR: +5%
      ```
    - **Cách chỉnh**:
      - Mở node → Nhấn **"Edit"** → Sửa **`message`** trong tab **"Parameters"**.
      - **Lưu ý**: Nếu muốn gửi qua **email** thay vì Slack, thay thế node Slack bằng **node `n8n-nodes-base.email`**.

##### **E. Định Nghĩa Ngày (Define Days)**
- **Node `Define Days`** (Code):
  - **Logic**: Tính ngày trước hôm nay (`priorDay`) và ngày hôm qua (`lastDay`).
  - **Không cần chỉnh** nếu đã import từ file JSON chính xác.

##### **F. Gộp Dữ liệu (Merge)**
- **Node `Merge` và `Merge Days`** (Merge/Code):
  - **Chức năng**: Gộp dữ liệu từ hai ngày để so sánh.
  - **Không cần chỉnh** nếu import từ file JSON.

---
#### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run**:
   - Nhấn **"Run Workflow"** → Chọn **"Test"** → Nhập dữ liệu mẫu (nếu có).
   - Kiểm tra **Slack** hoặc **email** để xem báo cáo có xuất hiện không.
2. **Bật Active**:
   - Sau khi test thành công, nhấn **"Active"** để workflow chạy tự động hàng ngày.

---
### **✍️ Mẹo & Gợi Ý Nâng Cao**
1. **Thay Thế Slack Bằng Email**:
   - Thay thế các node `Top DoD Movers Alert` bằng **node `n8n-nodes-base.email`**.
   - Cấu hình **SMTP** (ví dụ: Gmail) trong **Credentials**.

2. **Lưu Log Dữ liệu**:
   - Thêm **node `n8n-nodes-base.googleSheets`** sau `Merge` để lưu dữ liệu vào Google Sheets.
   - **Cách làm**:
     - Import node `Google Sheets` → Chọn sheet cần lưu → Chọn **"Append Row"** (thêm hàng mới).

3. **Cảnh Báo Trên Telegram**:
   - Thay thế node Slack bằng **node `n8n-nodes-base.telegram`**.
   - Cấu hình **Telegram Bot Token** và **Chat ID** trong **Credentials**.

4. **Tùy Chỉnh Ngưỡng Lọc**:
   - Mở các node `Top Movers Filter` → Sửa code để thay đổi ngưỡng lọc (ví dụ: từ `100 clicks` thành `50 clicks`).

5. **Phân Loại Theo URL Pattern**:
   - Thay vì phân loại theo keyword, có thể phân loại theo **URL path** (ví dụ: `/recipe/`, `/faq/`).
   - **Cách làm**:
     - Mở node `Segment Switch` → Thêm điều kiện mới:
       ```javascript
       $.pageUrl.includes("/recipe/") → Nhóm Content
       ```

---
### **📌 Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp SEO muốn:
✔ **Tự động hóa** việc theo dõi top mover hàng ngày.
✔ **Nhận báo cáo kịp thời** qua Slack/email.
✔ **Tiết kiệm thời gian** để tập trung vào chiến lược SEO.

**Hành động ngay hôm nay!**
1. **Import workflow** từ [đây](https://n8n.io/workflows/6004).
2. **Cấu hình GSC và Slack** (hoặc email).
3. **Bật Active** và bắt đầu **bắt chước top mover** mỗi sáng!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**Chia sẻ và like nếu bài viết hữu ích!** 🚀
**Có thắc mắc?** Để comment bên dưới, mình sẽ hỗ trợ ngay!