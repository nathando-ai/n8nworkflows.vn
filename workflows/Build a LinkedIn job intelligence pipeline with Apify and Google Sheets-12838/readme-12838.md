---
title: "🚀 Tự Động Hóa Thông Tin Vị Trí Công Việc LinkedIn: Từ Dữ Liệu Thô Sang Hiring Intelligence (Không Cần Code)"
description: "Workflow này tự động thu thập, lọc bỏ trùng lặp và lưu trữ thông tin việc làm LinkedIn vào Google Sheets, giúp các sếp theo dõi hoạt động tuyển dụng của đối thủ, phát hiện xu hướng thị trường và tối ưu chiến lược tuyển dụng chỉ trong vài phút mỗi ngày. Không cần viết code, chỉ cần cấu hình và chạy 24/7."
slug: "tieu-dong-hoa-thong-tin-vi-tri-cong-viec-linkedin"
tags: [n8n, automation, market-research, hiring-intelligence, apify, google-sheets]
keywords: [tự động hóa linkedin job, thu thập thông tin tuyển dụng, apify n8n, google sheets automation, hiring intelligence, tự động hóa không code]
---

# 🚀 **Tự Động Hóa Thông Tin Vị Trí Công Việc LinkedIn: Giải Pháp Hiring Intelligence Cho Doanh Nghiệp**

### **Nỗi Đau Của Các Sếp Hiện Nay**
Hàng ngày, các sếp phải mất **từ 1-2 giờ** để:
- Tìm kiếm thủ công các vị trí tuyển dụng trên LinkedIn của đối thủ.
- Sao chép thông tin vào Excel hoặc Google Sheets để theo dõi.
- Lọc bỏ trùng lặp và cập nhật thủ công mỗi khi có vị trí mới.
- Phân tích xu hướng tuyển dụng để điều chỉnh chiến lược nhân sự.

**Kết quả?** Thời gian quý giá bị "chôn vùi" trong công việc lặp lại, trong khi đối thủ đã tự động hóa và nắm bắt cơ hội sớm hơn.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tháng** cho việc thu thập và theo dõi thông tin tuyển dụng.
- **Dữ liệu sạch và cập nhật liên tục** (không trùng lặp, không thiếu thông tin).
- **Phát hiện xu hướng tuyển dụng** của đối thủ (ví dụ: tăng tuyển dụng ở ngành nào, vị trí nào hot).
- **Cung cấp dữ liệu cho downstream automation** (ví dụ: gửi báo cáo định kỳ cho ban lãnh đạo, tích hợp với CRM).
- **Hoạt động 24/7** mà không cần can thiệp thủ công.
:::

---
### **🔧 Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản Apify** (đăng ký miễn phí tại [apify.com](https://apify.com/)):
   - Chọn **actor "LinkedIn Jobs Scraper"** (cần có API key của Apify).
   - **Lưu ý:** Apify có giới hạn free tier (500 runs/tháng). Nếu cần chạy nhiều hơn, mua plan Pro.
2. **Tài khoản Google** (để kết nối với Google Sheets):
   - Tạo một **Google Sheet mới** với các cột sau (định dạng chuẩn):
     - `Job ID` (ID duy nhất của vị trí)
     - `Title` (Tiêu đề công việc)
     - `Company` (Tên công ty)
     - `Location` (Địa điểm)
     - `Posting Date` (Ngày đăng)
     - `Days Since Posted` (Số ngày từ khi đăng)
   - **Chia sẻ Google Sheet** với quyền "Sửa" cho n8n.
3. **Tài khoản LinkedIn** (để lấy URL của các vị trí tuyển dụng).
4. **VPS Self-hosted n8n** (để workflow chạy 24/7):
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)

---
### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/12838](https://n8n.io/workflows/12838) và import vào n8n Editor.
- **Cách 2:** Copy toàn bộ JSON từ link trên và paste vào **Import Workflow** trong n8n.
- **Cách 3:** Sử dụng **n8n CLI** (nếu tự host):
  ```bash
  n8n import workflow.json --name "LinkedIn Job Intelligence"
  ```

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **7 node chính**, các sếp cần chú ý cấu hình như sau:

##### **🔹 Node 1: Manual Trigger (Hoặc Cron Trigger)**
- **Tên node:** `Manual trigger (can be replaces to cron trigger)`
- **Cách cấu hình:**
  - Để mặc định là **Manual Trigger** (để test ban đầu).
  - Sau khi test thành công, **thay bằng Cron Trigger** để chạy tự động (ví dụ: hàng ngày lúc 8h sáng).
    - **Cú pháp Cron:** `0 8 * * *` (lúc 8h00 hàng ngày).
  - **Lưu ý:** Nếu dùng Cron, cần **đăng ký một URL Webhook** để n8n gọi API khi trigger.

##### **🔹 Node 2: Extract LinkedIn Data Using Apify**
- **Tên node:** `Extract linkedin data using Apify`
- **Cấu hình chi tiết:**
  - **Credentials:** Chọn `apifyOAuth2Api` (đã cấu hình trước khi import).
  - **Key Parameters:**
    - `operation`: Đặt thành `"Run actor and get dataset"` (mặc định).
    - `actorId`: `linkedin-jobs-scraper` (không cần thay đổi).
    - **Input Data (JSON):**
      ```json
      {
        "startUrls": ["https://www.linkedin.com/jobs/view/123456789"], // Thay bằng URL vị trí tuyển dụng
        "maxItems": 100, // Số lượng vị trí muốn lấy (mặc định 100)
        "proxy": "apify-proxy" // Sử dụng proxy của Apify
      }
      ```
  - **Lưu ý:**
    - **Paste ít nhất 1 URL** của vị trí tuyển dụng LinkedIn vào `startUrls`.
    - Nếu muốn lấy nhiều vị trí, thêm nhiều URL vào mảng `startUrls` (tối đa 10 URL).
    - **Không cần API Key** vì Apify đã tích hợp trong credentials.

##### **🔹 Node 3: Looping (Split In Batches)**
- **Tên node:** `Looping`
- **Cấu hình:**
  - **Batch Size:** Đặt thành **50** (giúp workflow ổn định hơn).
  - **Lưu ý:** Nếu Apify trả về nhiều dữ liệu, node này sẽ chia thành batch để xử lý hiệu quả.

##### **🔹 Node 4 & 5: Search & Append to Google Sheets**
- **Node 4:** `Search for existing records in Gsheet`
  - **Credentials:** `googleSheetsOAuth2Api`.
  - **Key Parameters:**
    - `operation`: `read`.
    - **Range:** Đặt thành `Sheet1!A:F` (đảm bảo trùng với cột trong Google Sheet).
    - **Query:** Sử dụng công thức `=ARRAYFORMULA(IFERROR(VLOOKUP($A2:$A, {A:A, ROW(A:A)}, 2, FALSE), ""))` để tìm trùng lặp.
  - **Output:** Node này trả về danh sách **Job ID** đã tồn tại trong Google Sheet.

- **Node 5:** `Append new rows to Gsheet`
  - **Credentials:** `googleSheetsOAuth2Api`.
  - **Key Parameters:**
    - `operation`: `append`.
    - **Range:** Đặt thành `Sheet1!A:F` (cùng với Node 4).
    - **Data:** Chọn `json` từ Node 3 (dữ liệu mới từ Apify).
  - **Lưu ý:**
    - **Chỉ append dữ liệu mới** (không trùng với Node 4).
    - **Cột `Job ID`** phải là duy nhất để tránh trùng lặp.

##### **🔹 Node 6: Condition to Remove Dup in Gsheet**
- **Tên node:** `Condition to remove dup in gsheet`
- **Cấu hình:**
  - **Condition:** Kiểm tra nếu `Job ID` **không tồn tại** trong danh sách từ Node 4.
  - **Nếu đúng:** Chuyển dữ liệu sang Node 7 để xử lý.
  - **Nếu sai:** Bỏ qua (đã tồn tại trong Google Sheet).

##### **🔹 Node 7: Choose Data Field That Are Relevant**
- **Tên node:** `Choose data field that are relevant`
- **Cấu hình:**
  - **Set:** Chọn các trường cần lưu vào Google Sheet (ví dụ: `title`, `company`, `location`, `postingDate`).
  - **Lưu ý:** Đảm bảo các trường này **khớp với cột trong Google Sheet**.

---
#### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run:**
   - Nhập **1 URL vị trí tuyển dụng** vào Node 2.
   - Chạy **Test Execution** để kiểm tra dữ liệu.
   - Kiểm tra Google Sheet có cập nhật dữ liệu mới không.
2. **Bật Active:**
   - Sau khi test thành công, **bật Active** và chuyển sang **Cron Trigger** (nếu muốn tự động).

---
### **✍️ Mẹo & Gợi Ý Nâng Cao**
1. **Tích Hợp Slack/Telegram để báo cáo:**
   - Thêm node **Slack** hoặc **Telegram Bot** sau Node 7 để gửi thông báo khi có vị trí mới.
   - Ví dụ: `"Có [X] vị trí tuyển dụng mới từ [Company]!"`.

2. **Lưu Log Dữ Liệu:**
   - Thêm node **Set** hoặc **Google Drive** để lưu lịch sử dữ liệu (giúp theo dõi và phân tích sau này).

3. **Tự Động Cập Nhật Thường Xuyên:**
   - Sử dụng **Cron Trigger** với lịch chạy hàng ngày (ví dụ: `0 8 * * *`).
   - **Lưu ý:** Apify có giới hạn free tier (500 run/tháng), nên cân nhắc plan Pro nếu cần chạy nhiều hơn.

4. **Phân Tích Xu Hướng Tuyển Dụng:**
   - Sử dụng **Google Apps Script** hoặc **Power BI** để tạo báo cáo tự động từ Google Sheet.
   - Ví dụ: Báo cáo số lượng vị trí mới mỗi tháng, ngành nghề hot nhất.

5. **Kết Hợp với CRM:**
   - Sử dụng node **Zapier** hoặc **Make (Integromat)** để chuyển dữ liệu từ Google Sheet vào CRM (ví dụ: HubSpot, Salesforce).

---
### **📌 Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc lặp lại, đồng thời cung cấp **dữ liệu chính xác và cập nhật** về hoạt động tuyển dụng của đối thủ. Bằng cách tự động hóa quá trình thu thập và lưu trữ thông tin, các sếp có thể:
✅ **Phát hiện xu hướng tuyển dụng sớm** để điều chỉnh chiến lược nhân sự.
✅ **Tiết kiệm thời gian** để tập trung vào việc phân tích và ra quyết định.
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.

**Hành động ngay!**
1. **Chuẩn bị tài khoản Apify và Google Sheets** (nếu chưa có).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Test và bật Active** để bắt đầu thu thập dữ liệu tự động.

**🚀 Cần hỗ trợ thêm?** Liên hệ với [Ahmed Salama](https://n8n.io/workflows/12838) để đặt lịch tư vấn xây dựng workflow phù hợp với doanh nghiệp của các sếp!

---
**🔗 Tài Liệu tham khảo:**
- [Tutorial Video](https://youtu.be/tXvcCoM5igQ) (Giải thích chi tiết cách cấu hình).
- [Apify LinkedIn Jobs Scraper](https://apify.com/ahmedsalama/linkedin-jobs-scraper/overview).
- [Cách cấu hình Cron Trigger trong n8n](https://docs.n8n.io/integrations/trigger/n8n-nodes-base.cron-time/).