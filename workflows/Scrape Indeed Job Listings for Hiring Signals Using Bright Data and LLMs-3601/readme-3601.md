---
title: "🚀 Tự Động Hoá Scrape Danh Sách Việc Làm Indeed với Bright Data & AI - Dự Báo Hiring Signals"
description: "Workflow tự động hóa scrape danh sách việc làm từ Indeed, phân tích và đánh giá tính phù hợp với AI, lưu kết quả vào Google Sheets. Giúp doanh nghiệp phát hiện tín hiệu tuyển dụng sớm, tiết kiệm thời gian lên tới 80% so với cách làm thủ công."
slug: "tieu-dong-hoa-scrape-danh-sach-viec-lam-indeed-bright-data-ai"
tags: [n8n, automation, hr, ai, bright-data, google-sheets, openai]
keywords: [tự động hóa scrape indeed, hiring signals, bright data api, chatgpt trong n8n, tự động hóa tuyển dụng, ai trong n8n]
---

# 🚀 **Tự Động Hoá Scrape Danh Sách Việc Làm Indeed với Bright Data & AI**

## **Giải Pháu Nỗi Đau Của Các Sếp HR**
Bạn đã bao giờ phải:
- **Tốn hàng giờ** để tìm kiếm và lọc danh sách việc làm từ Indeed?
- **Bị bỏ lỡ cơ hội** vì không phát hiện được tín hiệu tuyển dụng sớm?
- **Không biết cách đánh giá** xem một công việc phù hợp với yêu cầu của doanh nghiệp hay không?

Workflow này **tự động hóa toàn bộ quy trình**, từ scrape dữ liệu việc làm đến phân tích bằng AI, giúp các sếp:
✅ **Tiết kiệm 80% thời gian** so với cách làm thủ công
✅ **Nhận danh sách việc làm mới nhất** từ Indeed (cập nhật hàng ngày)
✅ **Đánh giá tính phù hợp** của mỗi công việc bằng AI (ChatGPT)
✅ **Lưu kết quả vào Google Sheets** để theo dõi và báo cáo

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động scrape** danh sách việc làm từ Indeed theo các tiêu chí lọc (ngành nghề, địa điểm, mức lương, công ty...)
- **Phân tích AI** từng công việc để đánh giá tính phù hợp với doanh nghiệp
- **Lưu dữ liệu** vào Google Sheets với định dạng chuyên nghiệp
- **Cập nhật liên tục** (không cần can thiệp thủ công)
- **Giảm thiểu rủi ro** bỏ lỡ cơ hội tuyển dụng
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản Bright Data** (API Key) để scrape Indeed
✔ **Tài khoản Google Sheets** (OAuth 2.0 API) để lưu kết quả
✔ **Tài khoản OpenAI** (API Key) để sử dụng ChatGPT (gpt-4o-mini)
✔ **Google Sheet mẫu** (có thể copy từ [đây](https://docs.google.com/spreadsheets/d/1vHHNShHD96AWsPnbXzlDAhPg_DbXr_Yx3wsAnQEtuyU/edit?usp=sharing))

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/3601) hoặc copy toàn bộ JSON từ trang này.
- Mở **n8n Editor** → Nhấn **Import Workflow** → Dán JSON và nhấn **Import**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow gồm **11 node**, các sếp cần chú ý cấu hình sau:

##### **A. Cấu Hình API Keys**
- **Bright Data API Key**:
  - Trong node **"HTTP Request - Post API call to Bright Data"**, điền `Authorization: Bearer <API_KEY>` vào header.
  - Tham khảo [Bright Data Docs](https://docs.brightdata.com/introduction) để lấy API Key.

- **Google Sheets OAuth 2.0**:
  - Tạo **credentials mới** trong n8n (Settings → Credentials → Add Credential → Google Sheets OAuth 2.0 API).
  - Chọn **Google Sheet mẫu** (đã copy từ link trên) và cấp quyền truy cập.

- **OpenAI API Key**:
  - Tạo **credentials mới** trong n8n (Settings → Credentials → Add Credential → OpenAI API).
  - Điền `sk-...` (API Key từ OpenAI Dashboard).

##### **B. Cấu Hình Query Scrape Indeed**
Trong node **"HTTP Request - Post API call to Bright Data"**, cấu hình object JSON như sau (ví dụ cho việc tìm kiếm "Software Engineer" tại Austin, TX):
```json
{
  "country": "US",
  "domain": "indeed.com",
  "keyword_search": "Software Engineer",
  "location": "Austin, TX",
  "date_posted": "Last 7 days",
  "posted_by": "Microsoft",
  "pay": 85000
}
```
- **Tham khảo chi tiết các field** trong phần [🔍 Indeed Jobs API – Parameter Guide](#🔍-indeed-jobs-api-parameter-guide).

##### **C. Cấu Hình AI Phân Tích**
Trong node **"OpenAI Chat Model"**, các sếp có thể tùy chỉnh **prompt** để AI đánh giá tính phù hợp của công việc. Ví dụ:
> *"Analyze this job posting and determine if it matches our company's hiring needs. Consider factors like required skills, salary range, and company reputation. Return a score (1-10) and a brief summary."*

##### **D. Cấu Hình Google Sheets**
- Node **"Google Sheets - Adding All Job Posts"** (append) và **"Google Sheets"** (update) cần chỉ định **Sheet Name** và **Range** (ví dụ: `Sheet1!A1`).
- Đảm bảo **Google Sheet** đã được chia sẻ với tài khoản n8n.

#### **3. Kích Hoạt ⚡️**
- **Test Run**: Nhấn **Run Workflow** với dữ liệu mẫu để kiểm tra kết quả.
- **Bật Active**: Sau khi kiểm tra thành công, chuyển trạng thái sang **Active**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tự động hóa định kỳ**:
   - Sử dụng **node `formTrigger`** để kích hoạt workflow hàng ngày (ví dụ: scrape việc làm mới trong 7 ngày qua).
   - Hoặc kết hợp với **node `wait`** để poll Bright Data định kỳ.

2. **Lưu log hoạt động**:
   - Thêm **node `stickyNote`** để ghi lại thời gian scrape và kết quả.

3. **Gửi báo cáo qua Slack/Email**:
   - Kết nối với **Slack Webhook** hoặc **node `email`** để thông báo khi có việc làm mới phù hợp.

4. **Tùy chỉnh AI**:
   - Thay đổi **model** trong node `lmChatOpenAi` (ví dụ: `gpt-4` nếu muốn kết quả chính xác hơn).

5. **Lọc kết quả tự động**:
   - Sử dụng **node `splitOut`** để chia dữ liệu và áp dụng logic lọc trước khi gửi vào AI.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp HR, giúp phát hiện **tín hiệu tuyển dụng sớm** và **lựa chọn ứng viên phù hợp** một cách tự động. Bắt đầu ngay với **Bright Data + AI + Google Sheets** để tối ưu hóa quy trình tuyển dụng!

👉 **Bắt đầu import workflow ngay bây giờ** và **tự động hóa việc tìm kiếm việc làm** của doanh nghiệp!

---
**🔗 Liên Hệ Hỗ Trợ**:
- [Bright Data Docs](https://docs.brightdata.com/introduction)
- [Yaron Been (Tác Giả)](https://www.linkedin.com/in/yaronbeen/)