---
title: "🚀 Tự Động Hóa Scrape CV Tốt Nhất Từ RSS + Telegram Alerts - Giảm 10+ Giờ Tìm Kiếm Hàng Tuần"
description: "Workflow này tự động quét các trang tuyển dụng từ RSS/API, lọc bỏ trùng lặp, và gửi cảnh báo Telegram cho các vị trí phù hợp - tiết kiệm thời gian và tăng hiệu quả tuyển dụng 300%."
slug: "tieu-dung-rss-telegram-automation"
tags: [n8n, automation, lead-generation, recruitment, telegram-bot]
keywords: [tự động hóa tìm việc, scrape cv từ rss, telegram alert tuyển dụng, n8n workflow tuyển dụng, tự động hóa tuyển dụng không code]
---

# 🚀 **Tự Động Hóa Scrape CV Từ RSS + Telegram Alerts - Giảm 10+ Giờ Tìm Kiếm Hàng Tuần**

### **Nỗi Đau Của Các Sếp Trong Tìm Kiếm CV**
Mỗi ngày, các sếp phải:
- **Quét thủ công** hàng chục trang tuyển dụng (LinkedIn, RemoteOK, Indeed...) để tìm CV phù hợp.
- **Lọc bỏ trùng lặp** giữa các nguồn khác nhau, tốn thời gian và dễ bỏ sót.
- **Không nhận được thông báo kịp thời** khi có CV mới phù hợp, dẫn đến mất cơ hội tuyển dụng.
- **Không theo dõi được lịch sử** ứng viên đã xem xét trước đó.

**Workflow này giải quyết tất cả đó!** Với **n8n**, các sếp có thể:
✅ **Tự động quét** các trang tuyển dụng từ RSS/API theo lịch trình.
✅ **Lọc bỏ trùng lặp** bằng Google Sheets.
✅ **Nhận cảnh báo Telegram** ngay khi có CV mới phù hợp.
✅ **Lưu lịch sử** để không bỏ sót ứng viên cũ.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy 24/7 mà không gián đoạn, các sếp nên cài **n8n trên VPS riêng** (Self-hosted) để đảm bảo tính ổn định và bảo mật.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tuần** không phải quét thủ công các trang tuyển dụng.
- **Chỉ nhận thông báo CV mới** phù hợp với tiêu chí của doanh nghiệp (vị trí, địa điểm, mức lương...).
- **Không bỏ sót ứng viên** nhờ hệ thống deduplicate tự động.
- **Lưu trữ lịch sử** tất cả CV đã xem xét trên Google Sheets.
- **Hoạt động liên tục** 24/7, không phụ thuộc vào thời gian làm việc của cá nhân.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets** (để lưu trữ lịch sử CV và deduplicate).
2. **Bot Telegram** (để nhận cảnh báo):
   - Tạo bot tại [@BotFather](https://t.me/BotFather) và lấy **API Token**.
   - Lấy **Chat ID** của tài khoản Telegram muốn nhận thông báo (có thể dùng [@userinfobot](https://t.me/userinfobot)).
3. **URL RSS/API của trang tuyển dụng** muốn theo dõi (ví dụ: RemoteOK, Arbeitnow, LinkedIn, Indeed...).
4. **Danh sách từ khóa lọc** (vị trí, địa điểm, từ loại trừ).
5. **API Key của n8n** (nếu tự host).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/13464](https://n8n.io/workflows/13464) và import vào n8n Editor.
- **Cách 2:** Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/13464) và dán vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **11 node**, các sếp cần chú ý cấu hình các node sau:

##### **🌐 Fetch Job Posts (HTTP Request)**
- **URL:** Thay thế bằng URL RSS/API của trang tuyển dụng muốn theo dõi.
  - **Ví dụ:**
    - RemoteOK: `https://remoteok.com/api`
    - Arbeitnow: `https://www.arbeitnow.com/api/job-board-api`
    - RSS từ LinkedIn/Indeed: `https://www.linkedin.com/jobs/feed/rss?...`
- **Headers:** Nếu API yêu cầu, thêm `Authorization` hoặc `User-Agent`.
- **Method:** Đặt thành `GET`.

##### **🔧 Parse & Extract Jobs (Code Node)**
- **Lưu ý:** Node này **không cần chỉnh sửa** nếu dữ liệu từ API/RSS đã chuẩn.
- Nếu dữ liệu không chuẩn, các sếp cần chỉnh sửa **JavaScript** trong node này để extraxt các trường:
  - `title`, `company`, `location`, `url`, `salary`, `tags`, `posted_date`.

##### **🎯 Keyword Filter (Code Node)**
- **Cấu hình từ khóa:**
  - Thay thế `targetRoles` (danh sách vị trí cần tìm).
  - Thay thế `targetLocations` (địa điểm).
  - Thay thế `excludeTerms` (từ loại trừ).
  - **Ví dụ:**
    ```javascript
    const targetRoles = ["Fullstack Developer", "Backend Engineer", "DevOps"];
    const targetLocations = ["Remote", "Hà Nội", "TP.HCM"];
    const excludeTerms = ["Intern", "Part-time", "Freelance"];
    ```

##### **📋 Read Seen Jobs (Google Sheets)**
- **Chọn Credential:** Kết nối tài khoản Google Sheets của mình.
- **Spreadsheet ID:** Lấy từ URL của Google Sheets (phần giữa `https://docs.google.com/spreadsheets/d/[SPREADSHEET_ID]/edit`).
- **Sheet Name:** Đặt tên sheet là `Seen_Jobs` (hoặc chỉnh theo cấu hình trong node).

##### **🆕 New Jobs Only? (If Node)**
- **Điều kiện:** Node này sẽ **bỏ qua** các CV đã tồn tại trong Google Sheets.

##### **📊 Log New Jobs (Google Sheets)**
- **Chọn Credential:** Cùng tài khoản Google Sheets như trên.
- **Spreadsheet ID:** Giống với node `Read Seen Jobs`.
- **Sheet Name:** Đặt tên sheet là `New_Jobs` (hoặc chỉnh theo cấu hình).
- **Columns cần có:**
  | Column Name       | Type    |
  |-------------------|---------|
  | Title             | Text    |
  | Company name      | Text    |
  | Location          | Text    |
  | Url               | Text    |
  | Description       | Text    |
  | Posted date       | Date    |
  | Salary            | Text    |
  | Matched Role      | Text    |
  | Scraped date      | Date    |

##### **📲 Telegram Alert (Telegram Node)**
- **Chọn Credential:** Kết nối bot Telegram với **API Token** và **Chat ID**.
- **Message Format:** Node này sẽ tự động gửi tin nhắn với định dạng:
  ```
  🚀 **New Job Alert!**
  **Title:** [Tên CV]
  **Company:** [Công ty]
  **Location:** [Địa điểm]
  **Salary:** [Mức lương]
  **Apply:** [Link apply]
  ```

##### **💤 No New Jobs (Code Node)**
- **Lưu ý:** Node này **không cần chỉnh sửa** nếu muốn workflow ngừng khi không có CV mới.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run:** Chạy **manual test** với một số dữ liệu mẫu để kiểm tra workflow.
2. **Bật Active:** Sau khi kiểm tra thành công, **bật Active** để workflow chạy tự động theo lịch trình.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Theo Dõi Nhiều Trang Tuyển Dụng:**
   - Thêm **nhiều node HTTP Request** cho các trang khác nhau (ví dụ: RemoteOK, Arbeitnow, WeWorkRemotely) và **merge** kết quả bằng node **Set**.
2. **Lọc Theo Mức Lương:**
   - Thêm điều kiện lọc mức lương trong node **Keyword Filter** bằng JavaScript:
     ```javascript
     const minSalary = 15000000; // 15 triệu/tháng
     const maxSalary = 30000000; // 30 triệu/tháng
     ```
3. **Gửi Cảnh Báo Đến Slack/Discord:**
   - Thay thế node **Telegram** bằng **Slack** hoặc **Discord Webhook**.
4. **Sử Dụng AI Lọc CV:**
   - Thêm node **LLM** (như Mistral, Google Vertex AI) để **đánh giá và xếp hạng** CV trước khi gửi cảnh báo.
5. **Lưu Log Chi Tiết:**
   - Thêm node **Google Sheets** hoặc **Database** để lưu **log chi tiết** mỗi lần scrape (thời gian, số lượng CV, lỗi...).

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc quét thủ công CV, đồng thời **tăng hiệu quả tuyển dụng** nhờ hệ thống tự động lọc và cảnh báo. **Chỉ cần 10 phút cấu hình**, các sếp sẽ **nhận được CV phù hợp ngay lập tức** mà không phải lo bỏ sót hoặc trùng lặp.

**Hành động ngay:**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Thay thế URL và từ khóa** phù hợp với doanh nghiệp.
3. **Bật Active** và **nhận CV tốt nhất** mỗi ngày!

---
**🚀 Cảm ơn các sếp đã sử dụng n8n để tự động hóa công việc!** Nếu có vấn đề, hãy để lại comment dưới đây. 👇