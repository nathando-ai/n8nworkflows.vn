---
title: "🔍 **Tự Động Scrape LinkedIn Profile Và Lưu Vào Google Sheets (Không Cần Code!)**"
description: "Workflow tự động hóa tìm kiếm và lưu trữ thông tin chi tiết từ LinkedIn (tên, vị trí, liên kết, mô tả...) vào Google Sheets chỉ với 1 lần nhập dữ liệu. Giúp các sếp tiết kiệm thời gian tìm kiếm lead, cập nhật thông tin liên tục và tối ưu hóa chiến dịch tuyển dụng/doanh nghiệp."
slug: "tieu-dong-scrape-linkedin-vao-google-sheets"
tags: [n8n, automation, lead-generation, google-sheets, linkedin-scraping, no-code]
keywords: [tự động scrape linkedin, n8n workflow lead generation, tìm kiếm profile linkedin tự động, lưu thông tin linkedin vào google sheets, api google custom search]
---

# 🚀 **Tự Động Scrape LinkedIn Profile Vào Google Sheets (Không Cần Code!)**

## **💡 Giải quyết vấn đề gì?**
Các sếp thường phải mất **giờ đồng hồ** để:
- Tìm kiếm và lọc các profile LinkedIn phù hợp với vị trí tuyển dụng hoặc đối tượng mục tiêu.
- Sao chép thủ công thông tin (tên, vị trí, liên kết, mô tả...) vào Google Sheets hoặc Excel.
- Cập nhật liên tục khi có thông tin mới xuất hiện.

**Workflow này tự động hóa toàn bộ quy trình!** Chỉ cần nhập **vị trí, ngành nghề và khu vực** vào form, hệ thống sẽ:
✅ Tìm kiếm tự động trên LinkedIn (sử dụng **Google Custom Search API**).
✅ Trích xuất thông tin chi tiết (tên, tiêu đề, liên kết profile, mô tả, hình ảnh).
✅ Lưu vào **Google Sheets** với định dạng sẵn sàng phân tích.
✅ **Tự động hóa** việc cập nhật khi có kết quả mới (không giới hạn trang).

---
### 🎯 **Kết quả các sếp nhận được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm thời gian**: Không cần tìm kiếm thủ công, tự động hóa từ A-Z.
- **Dữ liệu chính xác**: Trích xuất thông tin chính xác từ LinkedIn (không bị lỗi OCR).
- **Cập nhật liên tục**: Hệ thống tự động lấy kết quả mới khi có.
- **Sẵn sàng phân tích**: Dữ liệu được lưu vào Google Sheets với định dạng chuẩn (Name, Position, Profile Link, Description, Image, Search Criteria).
- **Tối ưu hóa tuyển dụng/doanh nghiệp**: Dễ dàng lọc và liên hệ với lead phù hợp.
:::

---
### 🔧 **Yêu cầu cần thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI SỬ DỤNG**]
Để workflow hoạt động, các sếp cần:
1. **Tài khoản Google** (để kết nối Google Sheets và Custom Search API).
2. **API Key và Search Engine ID (CX)** của **Google Custom Search API**:
   - [Cách đăng ký API Key](https://programmablesearchengine.google.com/about/)
   - **Lưu ý**: API này **không hỗ trợ scrape LinkedIn trực tiếp**, nhưng kết hợp với **Google Custom Search**, nó giúp tìm kiếm kết quả LinkedIn như người dùng nhập vào trình duyệt.
3. **Google Sheet** có **cột chuẩn** (tên, vị trí, liên kết profile, mô tả, hình ảnh, thông tin tìm kiếm).
4. **VPS n8n** (để chạy workflow 24/7):
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
## **🚀 Cách Import & Lưu ý khi "Lên đồ"**

### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/11693](https://n8n.io/workflows/11693) và import vào **n8n Editor**.
- **Cách 2**: Copy toàn bộ JSON từ link trên và **paste** vào **Import Workflow** trong n8n.

### **2. Các bước cấu hình BẮT BUỘC**
Workflow gồm **9 node**, nhưng các node quan trọng cần chỉnh như sau:

#### **🔹 Node 1: "On form submission" (formTrigger)**
- **Mục đích**: Nhận dữ liệu từ form (vị trí, ngành nghề, khu vực).
- **Lưu ý**:
  - Cấu hình **form** với các trường:
    - `position` (vị trí cần tìm).
    - `industry` (ngành nghề).
    - `region` (khu vực).
  - **Kết nối** với node tiếp theo (`HTTP Request`).

#### **🔹 Node 2: "HTTP Request" (httpRequest)**
- **Mục đích**: Gửi yêu cầu tìm kiếm đến **Google Custom Search API**.
- **Cấu hình cần chỉnh**:
  - **Credentials**: Chọn `httpBasicAuth` (nếu cần).
  - **URL**: `https://www.googleapis.com/customsearch/v1`
  - **Headers**:
    ```json
    {
      "Content-Type": "application/json",
      "Authorization": "Bearer YOUR_API_KEY"
    }
    ```
  - **Body (JSON)**:
    ```json
    {
      "q": "$$.json.position + \"site:linkedin.com/in\"",
      "cx": "YOUR_SEARCH_ENGINE_ID",
      "searchType": "web",
      "num": 10
    }
    ```
    - Thay `YOUR_API_KEY` và `YOUR_SEARCH_ENGINE_ID` từ Google Custom Search.
    - `$$.json.position` là dữ liệu từ form (vị trí cần tìm).

#### **🔹 Node 3 & 4: "Code in JavaScript" (code)**
- **Mục đích**: Xử lý kết quả tìm kiếm và trích xuất thông tin LinkedIn.
- **Lưu ý**:
  - Node này **sử dụng JavaScript** để:
    - Lọc kết quả có liên quan đến LinkedIn.
    - Trích xuất thông tin như **tên, tiêu đề, liên kết profile, mô tả**.
  - **Không cần chỉnh sửa** nếu import từ file JSON (n8n đã tự động hóa logic).

#### **🔹 Node 5: "Wait" (wait)**
- **Mục đích**: Đợi kết quả từ API trước khi xử lý tiếp.
- **Thời gian chờ**: Đặt **5-10 giây** để đảm bảo API trả về đầy đủ dữ liệu.

#### **🔹 Node 6: "Pagination Check" (if)**
- **Mục đích**: Kiểm tra có kết quả trang tiếp theo không.
- **Cấu hình**:
  - Nếu `nextPageToken` tồn tại → tiếp tục tìm kiếm trang sau.
  - Nếu không → dừng workflow.

#### **🔹 Node 7 & 8: "Edit Fields" (set)**
- **Mục đích**: Chuẩn hóa dữ liệu trước khi lưu vào Google Sheets.
- **Lưu ý**:
  - Đảm bảo các trường như `Name`, `Position`, `Profile Link` được định dạng đúng.

#### **🔹 Node 9: "Append or update row in sheet" (googleSheets)**
- **Mục đích**: Lưu dữ liệu vào Google Sheets.
- **Cấu hình cần chỉnh**:
  - **Credentials**: Chọn `googleSheetsOAuth2Api`.
  - **File Google Sheets**: Chọn file đã chuẩn bị.
  - **Sheet Name**: Chọn tab cần lưu.
  - **Columns**: Đảm bảo các cột (`Name`, `Position`, `Profile Links`, `Description`, `Image Link`, `Searched Position`, `Searched Industry`, `Searched Region`) tồn tại.

---
### **⚡️ Kích hoạt Workflow**
1. **Test Run** với dữ liệu mẫu:
   - Nhập vào form: `position: "Marketing Manager"`, `industry: "Tech"`, `region: "Vietnam"`.
   - Kiểm tra kết quả trong Google Sheets.
2. **Bật Active** workflow.

---
## **✍️ Mẹo & Gợi ý Nâng Cao**
:::info[**TIẾP CẬN HƠN**]
1. **Kết nối với Slack/Telegram**:
   - Thêm node `slack` hoặc `telegram` để thông báo khi có kết quả mới.
2. **Lưu log hoạt động**:
   - Sử dụng node `set` để lưu lịch sử tìm kiếm vào Google Sheets.
3. **Tự động hóa định kỳ**:
   - Sử dụng **n8n Cron Trigger** để chạy workflow hàng ngày/tuần.
4. **Tối ưu API**:
   - Nếu vượt quá giới hạn API, sử dụng **Google Custom Search API với quota cao**.
5. **Xử lý lỗi**:
   - Thêm node `if` để kiểm tra lỗi và gửi thông báo khi API không trả về kết quả.
:::

---
## **📌 Kết luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc tìm kiếm thủ công trên LinkedIn. **Chỉ cần nhập yêu cầu tìm kiếm**, hệ thống sẽ tự động:
✔ Tìm kiếm và trích xuất profile.
✔ Lưu vào Google Sheets với định dạng sẵn sàng phân tích.
✔ **Hoạt động 24/7** khi chạy trên VPS.

**🚀 Hành động ngay!**
1. **Đăng ký VPS** để tự động hóa workflow.
2. **Import workflow** và cấu hình API.
3. **Nhập dữ liệu tìm kiếm** và xem kết quả xuất hiện trong Google Sheets!

**💡 Lưu ý**: Do Google Custom Search API **không hỗ trợ scrape LinkedIn trực tiếp**, workflow này **tìm kiếm kết quả như người dùng nhập vào trình duyệt**. Nếu cần scrape LinkedIn **trực tiếp**, các sếp cần sử dụng **API khác** (như **Phantombuster** hoặc **Apify**) và kết hợp với n8n.

---
**🔗 [Xem workflow gốc](https://n8n.io/workflows/11693)** | **🛠️ [Cài đặt VPS n8n](https://tino.vn/vps-n8n?affid=388)**