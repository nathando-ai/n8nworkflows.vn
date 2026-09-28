---
title: "🚀 Tự Động Hóa Tìm Kiếm & Đánh Giá Cấp Thang Việc Làm Từ Nhiều Nguồn (Apify + Google Sheets)"
description: "Workflow tự động hóa thu thập và đánh giá việc làm từ 5 nguồn khác nhau (Remotive, Arbeitnow, Jobicy, LinkedIn, Naukri) theo yêu cầu kỹ thuật và vị trí, sau đó ghi vào Google Sheets. Giúp các sếp tiết kiệm thời gian lên tới 10 giờ/tuần và lọc ra những cơ hội phù hợp nhất."
slug: "tieu-dong-hoa-tim-kiem-danh-gia-viec-lam"
tags: [n8n, automation, hr, ai-summarization, apify, google-sheets]
keywords: [n8n workflow tìm việc, tự động hóa tuyển dụng, đánh giá việc làm, apify scraper, google sheets automation]
---

# 🚀 **Tự Động Hóa Thu Thập & Đánh Giá Việc Làm Từ 5 Nguồn Khác Nhau**

### **Giải quyết vấn đề gì?**
Các sếp và nhà tuyển dụng thường phải mất **giờ đồng hồ** để:
- Tìm kiếm việc làm trên nhiều trang tuyển dụng khác nhau (LinkedIn, Naukri, Jobicy...).
- Lọc và đánh giá từng công việc dựa trên yêu cầu kỹ thuật và vị trí mong muốn.
- Ghi chép thông tin vào bảng Excel/Google Sheets để theo dõi.

**Workflow này tự động hóa toàn bộ quy trình** bằng cách:
✅ **Thu thập** việc làm từ **5 nguồn** (miễn phí và trả phí).
✅ **Đánh giá** độ phù hợp với yêu cầu kỹ thuật và vị trí của bạn.
✅ **Sắp xếp** theo thứ tự ưu tiên (độ phù hợp + ngày đăng).
✅ **Ghi vào Google Sheets** để theo dõi liên tục.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không phải thủ công tìm kiếm trên nhiều trang.
- **Độ chính xác cao**: Đánh giá tự động dựa trên yêu cầu kỹ thuật và vị trí.
- **Cập nhật liên tục**: Thu thập việc làm mới mỗi khi có yêu cầu mới.
- **Dữ liệu tập trung**: Tất cả thông tin được ghi vào **Google Sheets** dễ theo dõi.
- **Lọc bỏ việc không phù hợp**: Giảm thiểu thời gian xem xét những công việc không liên quan.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản Apify** (miễn phí):
   - [Đăng ký Apify](https://console.apify.com/)
   - Lấy **API Key** từ: [https://console.apify.com/settings/integrations](https://console.apify.com/settings/integrations)
   - **Phê duyệt quyền cho Actor Naukri**:
     [https://console.apify.com/actors/GLb4E7UrStD7XLJxO?approvePermissions=true](https://console.apify.com/actors/GLb4E7UrStD7XLJxO?approvePermissions=true)

2. **Google Sheets**:
   - Tạo một **Google Sheet mới** và chia sẻ với n8n (quyền chỉnh sửa).
   - **ID của Google Sheet** (để điền vào node cuối cùng).

3. **Credentials trong n8n**:
   - **Google Sheets OAuth2**: Cấu hình trong **Credentials** của n8n (nếu chưa có).
   - **Apify API Key**: Điền vào **HTTP Request** của 2 node `Apify LinkedIn` và `Apify Naukri`.

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải workflow JSON** từ [đây](https://n8n.io/workflows/15998) (hoặc copy/paste JSON từ link trên).
- Trong **n8n Editor**, nhấn **Import** và chọn file JSON.
- **Hoặc** copy toàn bộ JSON và paste vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow có **13 node**, nhưng các bước quan trọng nhất cần chú ý:

##### **A. Cấu hình Form Trigger (Bắt đầu)**
- Node này **thu thập yêu cầu tìm kiếm** từ người dùng:
  - **Job Role** (ví dụ: *Software Engineer*).
  - **Tech Stack** (ví dụ: *React, Node.js*).
  - **Country** (để lọc việc làm theo quốc gia).
- **Lưu ý**: Các giá trị này sẽ được lưu vào biến `_jobRole`, `_techStack`, `_country` để sử dụng trong các API sau.

##### **B. Cấu hình 5 Node Scraper (Thu thập dữ liệu)**
Workflow sử dụng **5 nguồn khác nhau**:
| **Node**               | **Loại API**       | **URL API (cần thay đổi)**                                                                 | **Lưu ý**                                                                 |
|------------------------|--------------------|-------------------------------------------------------------------------------------------|---------------------------------------------------------------------------|
| Scrape Remotive        | Free API           | `https://remotive.com/api/jobs` (tham khảo API chính thức)                               | Không cần API Key.                                                       |
| Scrape Arbeitnow       | Free API           | `https://arbeitnow.com/api/jobs` (tham khảo API chính thức)                               | Không cần API Key.                                                       |
| Scrape Jobicy          | Free API           | `https://jobicy.com/api/jobs` (tham khảo API chính thức)                                 | Không cần API Key.                                                       |
| **Apify LinkedIn**     | **Paid Scraper**   | `https://api.apify.com/v2/acts/hMvNSpz3JnHgl5jkh/run-sync-get-dataset-items?token=<API_KEY>&timeout=120` | **Thay thế `<API_KEY>` bằng API Key của bạn**.                          |
| **Apify Naukri**       | **Paid Scraper**   | `https://api.apify.com/v2/acts/codemaverick~naukri-job-scraper-latest/run-sync-get-dataset-items?token=<API_KEY>&timeout=120` | **Thay thế `<API_KEY>` bằng API Key của bạn**.                          |

##### **C. Cấu hình Google Sheets (Xuất dữ liệu)**
- Node cuối cùng **ghi dữ liệu vào Google Sheets**.
- **Cần điền**:
  - **Google Sheets ID** (tìm trong URL của Google Sheet, ví dụ: `d/1AbCdEfGhIjKlMnOpQrStUvWxYz/` → `1AbCdEfGhIjKlMnOpQrStUvWxYz`).
  - **Sheet Name** (tên tab trong Google Sheet, mặc định là `Sheet1`).
  - **Operation**: Đặt là `append` (thêm mới dữ liệu).

##### **D. Node Code (Đánh giá & Sắp xếp)**
- Node `Normalize Score and Sort` **chứa mã JavaScript** để:
  - **Normalize**: Chuyển đổi định dạng dữ liệu từ các API khác nhau thành một mẫu thống nhất.
  - **Đánh giá độ phù hợp**: So sánh với `_jobRole` và `_techStack` (sử dụng từ đồng nghĩa).
  - **Lọc bỏ** việc làm không phù hợp.
  - **Sắp xếp** theo độ phù hợp và ngày đăng.
- **Không cần chỉnh sửa** (nếu không muốn tự code).

#### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **Run Workflow** và nhập yêu cầu tìm kiếm (ví dụ: *Software Engineer, React, Vietnam*).
   - Kiểm tra **Google Sheets** xem dữ liệu có được ghi không.
2. **Bật Active**:
   - Sau khi test thành công, chuyển **Active** sang `ON`.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack Webhook** hoặc **Telegram Bot** để thông báo khi có việc làm mới phù hợp.
2. **Lưu log hoạt động**:
   - Sử dụng node **HTTP Request** để gửi dữ liệu đến **Google Drive** hoặc **AWS S3** để lưu trữ lâu dài.
3. **Tự động gửi báo cáo định kỳ**:
   - Sử dụng **n8n Cron Trigger** để chạy workflow hàng ngày và gửi báo cáo qua email.
4. **Cải thiện độ chính xác**:
   - Nếu node `Normalize Score and Sort` không phù hợp, các sếp có thể **chỉnh sửa mã JavaScript** để thêm logic đánh giá phù hợp hơn.

---

### 📌 **Kết luận**
Workflow này **giúp các sếp tự động hóa quy trình tìm kiếm việc làm**, tiết kiệm thời gian và tăng hiệu quả tuyển dụng. **Chỉ cần 5 phút để cấu hình**, sau đó workflow sẽ hoạt động **mỗi khi có yêu cầu mới**.

**Hãy áp dụng ngay và không phải lo lắng về việc bỏ lỡ cơ hội việc làm phù hợp!** 🚀

---
:::note[Lưu ý cuối cùng]
- **Apify có giới hạn miễn phí**: Nếu sử dụng quá nhiều, cần nâng cấp tài khoản.
- **Google Sheets có giới hạn hàng**: Nếu quá nhiều dữ liệu, cân nhắc sử dụng **Google BigQuery** hoặc **Excel Online**.
- **Nếu gặp lỗi**, kiểm tra **log trong node HTTP Request** và **Google Sheets OAuth2**.
:::