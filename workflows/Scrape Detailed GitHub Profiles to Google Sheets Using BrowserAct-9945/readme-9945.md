---
title: "🚀 Tự Động Hoàn Thành Báo Cáo Chi Tiết GitHub Tự Động Từ BrowserAct Sang Google Sheets (Không Cần Code)"
description: "Workflow này tự động scrape thông tin chi tiết từ hồ sơ GitHub (bao gồm profile, repositories, links liên kết) và tổ chức dữ liệu vào các báo cáo Google Sheets riêng biệt, tiết kiệm thời gian lên đến 90% so với cách làm thủ công. Phù hợp cho các sếp marketing, HR, hoặc doanh nghiệp cần phân tích tài năng kỹ thuật."
slug: "tieu-dong-hoan-thanh-bao-cao-github-browseract-google-sheets"
tags: [n8n, automation, lead-generation, browseract, google-sheets, scraping-data]
keywords: [n8n workflow github scrape, tự động hóa scrape github, báo cáo tài năng kỹ thuật, browseract n8n, google sheets tự động hóa]
---

# 🚀 **Tự Động Hoàn Thành Báo Cáo Chi Tiết GitHub Từ BrowserAct Sang Google Sheets**

### **Giải pháp cho các sếp:**
Bạn có bao giờ phải mất **tối 2-3 tiếng** để scrape và tổng hợp thông tin từ hàng chục hồ sơ GitHub của các nhà phát triển tiềm năng? Hay phải lo lắng rằng dữ liệu thu thập được **không đầy đủ, không chính xác**, hoặc **không được tổ chức** một cách chuyên nghiệp? Workflow này sẽ **tự động hóa toàn bộ quy trình**, giúp bạn:
- **Scrape** thông tin chi tiết từ GitHub (profile, repositories, links, hoạt động gần đây).
- **Tổ chức** dữ liệu vào các **báo cáo Google Sheets riêng biệt** theo từng người dùng.
- **Cập nhật Slack** khi hoàn thành scrape cho mỗi hồ sơ.
- **Tiết kiệm thời gian** lên đến **90%** so với cách làm thủ công.

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Scrape và tổng hợp dữ liệu **tự động 24/7**, không cần can thiệp thủ công.
- **Dữ liệu chính xác & toàn diện**: BrowserAct đảm bảo scrape **tất cả thông tin** từ GitHub (không bị lỗi như cách scrape thủ công).
- **Báo cáo chuyên nghiệp**: Dữ liệu được **tách thành 3 tab riêng biệt** (Profile, Repositories, Links) trong Google Sheets.
- **Cảnh báo thực thời**: Nhận thông báo Slack khi hoàn thành scrape cho mỗi hồ sơ.
- **Dễ dàng mở rộng**: Thêm/loại bỏ hồ sơ chỉ bằng cách cập nhật Google Sheet đầu vào.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản BrowserAct**:
   - [Đăng ký tài khoản miễn phí](https://www.browseract.com/) (nếu chưa có).
   - **API Key** và **Workflow ID** của template **"Scraping GitHub Users Activity & Data"**.
   - Cài đặt **n8n Community Node BrowserAct** ([hướng dẫn cài đặt](https://www.npmjs.com/package/n8n-nodes-browseract-workflows)).

2. **Google Sheets**:
   - **Tài khoản Google** và **OAuth 2.0 API Key** cho Google Sheets.
   - Một **Google Sheet đầu vào** chứa danh sách URL GitHub (cột tên: `URL`). Ví dụ:
     ```
     | URL                          |
     |------------------------------|
     | https://github.com/user1     |
     | https://github.com/user2     |
     ```

3. **Slack (không bắt buộc nhưng khuyến nghị)**:
   - **Tài khoản Slack** và **OAuth 2.0 API Key**.
   - **Channel ID** để nhận thông báo scrape.

4. **Hệ thống n8n**:
   - **Self-hosted n8n** (khuyến nghị) hoặc sử dụng n8n.cloud (miễn phí cho các sếp mới).
   - **VPS 4GB RAM** để chạy ổn định (👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) với mã giảm **VPSN8N**).
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. **Tải workflow** từ [link gốc](https://n8n.io/workflows/9945).
2. **Nhấp vào "Import"** trong n8n Editor.
3. **Chọn file JSON** và nhấn "Import".

:::note[LƯU Ý]
- Nếu sử dụng **n8n.cloud**, các sếp cần **upgrade plan** để sử dụng BrowserAct node.
- Đối với **self-hosted**, đảm bảo cài đặt **n8n-nodes-browseract-workflows** bằng lệnh:
  ```bash
  npx n8n install n8n-nodes-browseract-workflows
  ```
:::

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
#### **A. Cấu hình Credentials**
Các node quan trọng cần cấu hình:
| **Node**               | **Tham số cần điền**                          | **Lưu ý**                                                                 |
|------------------------|-----------------------------------------------|-----------------------------------------------------------------------------|
| **BrowserAct**         | `browserActApi` (API Key + Workflow ID)       | Sử dụng template **"Scraping GitHub Users Activity & Data"**.             |
| **Google Sheets**       | `googleSheetsOAuth2Api`                      | Chọn **Google Sheet đầu vào** (chứa danh sách URL) và **Sheet đầu ra**. |
| **Slack** (nếu có)     | `slackOAuth2Api` + **Channel ID**            | Điền **#channel-name** hoặc **ID channel** (tìm bằng cách paste `https://slack.com/archives/C123` vào Slack). |

#### **B. Cấu hình Node "Get row(s) in sheet"**
- **Sheet Name**: Điền tên **Google Sheet đầu vào** (chứa danh sách URL GitHub).
- **Range**: Điền `Sheet1!A2:B` (giả sử cột `URL` ở cột A, bắt đầu từ dòng 2).

#### **C. Cấu hình Node "BrowserAct"**
- **Operation**: Chọn `runTask`.
- **Task ID**: Điền **Workflow ID** của template BrowserAct (tìm trong tài khoản BrowserAct).
- **Input Data**: Sử dụng **URL** từ Google Sheet đầu vào.

#### **D. Cấu hình Node "Code" (JavaScript)**
Mã JavaScript mặc định đã được tối ưu để **parse dữ liệu từ BrowserAct** thành định dạng JSON. Các sếp **không cần chỉnh sửa** trừ khi cần thêm logic đặc biệt.

#### **E. Cấu hình Node "Create sheet"**
- **Spreadsheet ID**: Điền **ID Google Sheet đầu ra** (tìm trong URL: `https://docs.google.com/spreadsheets/d/SPREADSHEET_ID/`).
- **Name**: Đặt tên sheet theo **tên người dùng** (ví dụ: `user1-profile`).

---
### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Nhấn **"Execute workflow"** để chạy thử với **1-2 URL** đầu tiên.
   - Kiểm tra **Slack notification** và **Google Sheet đầu ra** để đảm bảo dữ liệu scrape chính xác.

2. **Bật Active**:
   - Sau khi test thành công, **bật Active workflow**.
   - **Lựa chọn**:
     - **Manual Trigger** (chạy thủ công).
     - **Schedule** (chạy tự động theo thời gian, ví dụ: hàng ngày lúc 8h sáng).

---
## ✍️ **Mẹo & gợi ý nâng cao**
### **1. Tự động hóa scrape định kỳ**
- Sử dụng **n8n Scheduler** để chạy workflow hàng ngày/tuần.
- Ví dụ: Scrape **50 hồ sơ mới** mỗi sáng thứ 2.

### **2. Gửi báo cáo định kỳ qua Email**
- Thêm **n8n-node-email** để gửi **báo cáo tổng hợp** hàng tháng.
- Sử dụng **Google Apps Script** để tự động tạo **PDF** từ Google Sheets.

### **3. Lọc hồ sơ theo tiêu chí**
- Thêm **n8n-node-code** trước khi scrape để **lọc URL** theo:
  - **Ngôn ngữ lập trình** (Python, JavaScript...).
  - **Vùng miền** (Việt Nam, Mỹ...).
  - **Hoạt động gần đây** (contribute trong 30 ngày).

### **4. Kết hợp với CRM**
- Sử dụng **n8n-node-hubspot** hoặc **n8n-node-salesforce** để **tự động thêm hồ sơ** vào CRM khi scrape xong.

### **5. Lưu log scrape**
- Thêm **n8n-node-log** để ghi lại **lịch sử scrape**, bao gồm:
  - Thời gian scrape.
  - URL thành công/thất bại.
  - Thông tin lỗi (nếu có).

---
## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp cần **tự động hóa scrape GitHub** mà không cần viết code. Với **BrowserAct + n8n + Google Sheets**, bạn sẽ:
✅ **Tiết kiệm thời gian** lên đến 90% so với cách làm thủ công.
✅ **Nhận dữ liệu chính xác** từ GitHub (không bị lỗi như cách scrape thủ công).
✅ **Tạo báo cáo chuyên nghiệp** với cấu trúc rõ ràng (Profile, Repositories, Links).
✅ **Cập nhật Slack** khi hoàn thành scrape cho mỗi hồ sơ.

**Hành động ngay!**
1. **Chuẩn bị tài khoản BrowserAct và Google Sheets** (nếu chưa có).
2. **Import workflow** và cấu hình credentials.
3. **Test Run** với 1-2 URL để đảm bảo hoạt động.
4. **Bật Active** và **lên lịch tự động hóa**!

👉 [**Tải workflow ngay**](https://n8n.io/workflows/9945) và bắt đầu tự động hóa quy trình của mình! 🚀

---
### **Cần hỗ trợ?**
- **Discord n8n**: [https://discord.com/invite/UpnCKd7GaU](https://discord.com/invite/UpnCKd7GaU)
- **BrowserAct Blog**: [https://www.browseract.com/blog](https://www.browseract.com/blog)
- **Hướng dẫn chi tiết**:
  - [Tìm API Key BrowserAct](https://www.youtube.com/watch?v=pDjoZWEsZlE)
  - [Kết nối n8n với BrowserAct](https://www.youtube.com/watch?v=RoYMdJaRdcQ)