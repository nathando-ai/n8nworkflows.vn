---
title: "🚀 Tự Động Hóa Tìm Kiếm Công Việc Freelance Hàng Ngày Với Bright Data & n8n (Không Cần Code)"
description: "Workflow tự động hóa tìm kiếm và lưu trữ công việc freelance từ We Work Remotely hàng ngày vào Google Sheets, giúp bạn tiết kiệm thời gian và không bỏ lỡ cơ hội nào. Đặc biệt phù hợp cho freelancer, nhà tuyển dụng và người tìm việc remote."
slug: "tieu-dong-hoa-tim-kiem-cong-viec-freelance-voi-n8n"
tags: [n8n, automation, no-code, ai, freelance, remote-jobs, bright-data, google-sheets]
keywords: [tự động hóa tìm việc freelance, n8n workflow, scrap website, tìm việc remote, bright data, google sheets automation, công việc không cần code]
---

# 🚀 **Tự Động Hóa Tìm Kiếm Công Việc Freelance Hàng Ngày Với Bright Data & n8n**

## **Nỗi Đau Của Các Sếp**
Bạn có bao giờ phải:
- **Tốn thời gian** mỗi ngày để quét các trang tuyển dụng như We Work Remotely (WWR)?
- **Bỏ lỡ cơ hội** vì không theo dõi thường xuyên?
- **Phải copy-paste** thông tin công việc vào Google Sheets hoặc Excel?
- **Khó khăn với bot** khi scrap website vì bị chặn IP?

Workflow này **giải quyết tất cả** bằng cách tự động hóa toàn bộ quy trình: từ tìm kiếm, lọc theo kỹ năng, đến lưu trữ vào Google Sheets — **không cần viết một dòng code nào!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính bảo mật và khả năng mở rộng.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Không phải quét website hàng ngày.
✅ **Tự động hóa hoàn toàn**: Chỉ cần cấu hình 1 lần, workflow chạy tự động hàng ngày.
✅ **Lọc theo kỹ năng**: Chỉ lấy công việc phù hợp với kỹ năng của bạn.
✅ **Lưu trữ sạch sẽ**: Thông tin công việc được append vào Google Sheets với định dạng rõ ràng.
✅ **Không bị chặn bot**: Sử dụng Bright Data để scrap website an toàn.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Bright Data** (để scrap website an toàn):
   - [Đăng ký Bright Data](https://get.brightdata.com/1tndi4600b25) (tôi sẽ nhận commission nhỏ từ link này để hỗ trợ tạo nội dung miễn phí).
2. **Tài khoản Google Sheets** (để lưu trữ dữ liệu công việc).
3. **API Key Bright Data** (để cấu hình trong node HTTP Request).
4. **Google Sheets OAuth 2.0 Credentials** (để kết nối với Google Sheets).
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Mở [n8n Editor](https://n8n.io/editor).
2. Nhấn **Import** và chọn file JSON hoặc paste JSON từ [link gốc](https://n8n.io/workflows/5214).
3. Chọn **Create Workflow**.

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **5 node chính**, các sếp cần chú ý cấu hình như sau:

#### **🕒 Node 1: Run Scraper Daily (Trigger)**
- **Loại Node**: `scheduleTrigger`
- **Cấu Hình**:
  - Chọn **Daily** và thời gian chạy (ví dụ: 8h sáng).
  - **Không cần thay đổi gì** nếu muốn chạy hàng ngày tự động.

#### **🖋️ Node 2: Set Skill Filter (Set)**
- **Loại Node**: `set`
- **Cấu Hình**:
  - **Key**: `skill` (hoặc tên tùy ý).
  - **Value**: Điền **kỹ năng** bạn muốn tìm kiếm (ví dụ: `"Python"`, `"UI/UX"`, `"Marketing Digital"`).
  - **Lưu ý**: Nếu muốn tìm nhiều kỹ năng, có thể cấu hình thêm node `set` hoặc sử dụng biểu thức logic.

#### **🌍 Node 3: Scrape WWR with Bright Data (HTTP Request)**
- **Loại Node**: `httpRequest`
- **Cấu Hình**:
  - **Method**: `GET`
  - **URL**: `https://weworkremotely.com/remote-jobs` (hoặc URL khác của WWR).
  - **Headers**:
    - `User-Agent`: `Mozilla/5.0 (compatible; BrightdataScraper/1.0; +http://example.com/bot-info)`
    - `Authorization`: `Bearer YOUR_BRIGHT_DATA_API_KEY` (điền API Key từ Bright Data).
  - **Body**: Trống.
  - **Lưu ý**:
    - Thay `YOUR_BRIGHT_DATA_API_KEY` bằng API Key của bạn.
    - Nếu URL thay đổi, cần cập nhật trong node này.

#### **🧾 Node 4: Extract Jobs from HTML (HTML)**
- **Loại Node**: `html` (với `operation: extractHtmlContent`)
- **Cấu Hình**:
  - **HTML**: Dữ liệu từ node `Scrape WWR with Bright Data`.
  - **XPath/CSS Selector**: Các sếp cần **tìm kiếm và cấu hình** để trích xuất thông tin công việc như:
    - Tiêu đề công việc (`h2` hoặc `div.job-title`).
    - Công ty (`div.company-name`).
    - Link công việc (`a.job-link`).
    - Mô tả công việc (nếu cần).
  - **Lưu ý**:
    - Nếu không biết XPath/CSS Selector, có thể sử dụng **DevTools (F12)** trên trình duyệt để inspect và sao chép.
    - Ví dụ XPath cho tiêu đề công việc: `//h2[@class="job-title"]/text()`.

#### **📄 Node 5: Save Jobs to Google Sheets (Google Sheets)**
- **Loại Node**: `googleSheets` (với `operation: append`)
- **Cấu Hình**:
  - **Credentials**: Chọn `googleSheetsOAuth2Api` (đã cấu hình trước).
  - **Spreadsheet ID**: ID của Google Sheet bạn muốn lưu dữ liệu (có thể tìm trong URL của sheet).
  - **Sheet Name**: Tên tab trong Google Sheet (ví dụ: `"Công Việc Freelance"`).
  - **Range**: `A1` (hoặc tùy chỉnh).
  - **Data**: Dữ liệu từ node `Extract Jobs from HTML`.
  - **Lưu ý**:
    - Đảm bảo Google Sheet đã được chia sẻ với tài khoản OAuth2 của n8n.
    - Cấu hình **header** trong Google Sheets để trùng khớp với dữ liệu trích xuất (ví dụ: `Tiêu đề Công Việc`, `Công Ty`, `Link`).

---

### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhấn **Run Workflow** để kiểm tra dữ liệu mẫu.
   - Kiểm tra Google Sheets xem dữ liệu có được append đúng không.
2. **Bật Active**:
   - Sau khi kiểm tra thành công, chuyển trạng thái workflow sang **Active**.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Kết nối với Slack/Telegram**:
   - Thêm node `slack` hoặc `telegram` để thông báo khi có công việc mới.
2. **Lưu Log**:
   - Thêm node `set` hoặc `file` để lưu lịch sử scrap vào file JSON hoặc database.
3. **Báo Cáo Định Kỳ**:
   - Sử dụng node `scheduleTrigger` kết hợp với `googleSheets` để gửi báo cáo tổng hợp hàng tuần.
4. **Lọc Công Việc Theo Mức Lương**:
   - Thêm node `set` để lọc công việc có mức lương từ `X` trở lên.
5. **Tích Hợp với Notion/ClickUp**:
   - Thay vì Google Sheets, có thể lưu vào Notion hoặc ClickUp để quản lý dự án.
:::

---

## 📌 **Kết Luận**
Workflow này **giải phóng thời gian** của các sếp để tập trung vào những việc quan trọng hơn, đồng thời **không bỏ lỡ bất kỳ cơ hội công việc nào** trên We Work Remotely. Với **Bright Data**, bạn không phải lo lắng về việc bị chặn bot, và với **n8n**, toàn bộ quy trình được tự động hóa **không cần viết code**.

**Hãy import workflow ngay hôm nay và bắt đầu tìm kiếm công việc freelance một cách thông minh!** 🚀

---
**Nếu có thắc mắc, các sếp có thể liên hệ với tác giả Yaron Been qua:**
- [LinkedIn](https://www.linkedin.com/in/yaronbeen/)
- [YouTube](https://www.youtube.com/@YaronBeen/videos)