---
title: "🏡 **Tự Động Hóa Danh Sách Nhà Đất "Hot Deal" Hàng Ngày Từ Zillow → Google Sheets → Email (Không Cần Code!)**"
description: "Workflow tự động hóa lấy dữ liệu nhà đất giá rẻ hàng ngày từ Zillow API, tính toán ROI, lưu vào Google Sheets và gửi báo cáo email tự động. Giúp các sếp đầu tư bất động sản tiết kiệm thời gian theo dõi thị trường 24/7."
slug: "tieu-dong-hoa-danh-sach-nha-dat-zillow-google-sheets-email"
tags: [n8n, automation, real-estate, zillow-api, google-sheets, gmail, no-code]
keywords: [tự động hóa nhà đất, zillow api n8n, google sheets tự động, email báo cáo bất động sản, đầu tư bất động sản tự động]
---

# 🚀 **Tự Động Hóa "Hot Deal" Nhà Đất Hàng Ngày: Từ Zillow → Google Sheets → Email (Không Cần Code!)**

### **Nỗi Đau Của Các Sếp Đầu Tư Bất Động Sản**
Bạn có bao giờ phải:
- **Tra cứu thủ công** hàng trăm trang web nhà đất mỗi ngày để tìm "hot deal"?
- **Lưu trữ dữ liệu** vào Excel/GSheets một cách rườm rà, dễ bị lỗi?
- **Quên theo dõi** những cơ hội đầu tư vì bị mất trong email hoặc file?
- **Không biết** liệu một căn nhà giá rẻ có thực sự "lợi nhuận" hay không?

**Workflow này giải quyết tất cả!** Với chỉ **1 lần setup**, bạn sẽ nhận được:
✅ **Danh sách nhà đất giá rẻ hàng ngày** từ Zillow API (không cần crawl thủ công).
✅ **Tính toán ROI (Return on Investment)** tự động cho từng căn nhà.
✅ **Lưu trữ dữ liệu** vào Google Sheets với định dạng chuyên nghiệp.
✅ **Gửi báo cáo email tự động** vào mỗi sáng (9h), bao gồm top 5 "hot deal" hàng ngày.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**3 Lợi Ích Cốt Lõi**]
- **Tiết kiệm 10+ giờ/tuần** so với cách làm thủ công.
- **Không bỏ lỡ bất kỳ cơ hội nào** nhờ tự động hóa 24/7.
- **Quản lý đầu tư chuyên nghiệp** với dữ liệu sạch, có tính toán ROI chi tiết.
- **Cập nhật thị trường bất động sản** một cách khoa học, không phụ thuộc vào cảm nhận cá nhân.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Zillow API**:
   - Đăng ký API key tại [Zillow Developer Portal](https://www.zillow.com/howto/api/APIOverview.htm).
   - Lưu ý: Zillow có giới hạn API call/month (thường ~1000 call/free tier). Nếu cần nhiều hơn, nâng cấp lên paid plan.
2. **Tài khoản Google**:
   - **Google Sheets**: Tạo 1 file mới để lưu dữ liệu (cấu trúc sẽ được tự động tạo).
   - **Google OAuth 2.0 Credentials**: Cài đặt cho n8n (hướng dẫn [đây](https://docs.n8n.io/integrations/built-in/nodes/n8n-nodes-base.googleSheets/)).
3. **Tài khoản Gmail**:
   - **OAuth 2.0 Credentials** cho n8n (hướng dẫn [đây](https://docs.n8n.io/integrations/built-in/nodes/n8n-nodes-base.gmail/)).
   - Địa chỉ email để nhận báo cáo hàng ngày.
4. **VPS Self-Hosted (khuyến nghị)**:
   - Workflow chạy hàng ngày (9h sáng), nên **không nên chạy trên n8n.cloud** (dừng khi offline).
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) với mã giảm **VPSN8N** (giảm 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (ổn định, tốc độ cao).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/3030) hoặc copy toàn bộ JSON từ trang này.
- Mở **n8n Editor** → Nhấn **"Import"** → Dán JSON hoặc tải file `.json`.
- **Không cần chỉnh sửa** cấu trúc workflow (n8n sẽ tự động tạo nodes).

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflows này có **8 node chính**, nhưng chỉ **3 node cần cấu hình chi tiết**:

##### **A. Node "Set Parameters" (Set)**
- **Chỉnh sửa tham số Zillow API**:
  ```json
  {
    "city": "Ho Chi Minh", // Thay bằng thành phố muốn theo dõi (ví dụ: "New York", "Hanoi")
    "maxPrice": 500000000, // Giá tối đa (đơn vị: VND hoặc USD, tùy API)
    "minBedrooms": 2,     // Số phòng ngủ tối thiểu
    "minBathrooms": 2,    // Số phòng tắm tối thiểu
    "minSquareFeet": 100 // Diện tích tối thiểu (sqft)
  }
  ```
  - **Lưu ý**: Zillow API trả về dữ liệu theo **USD** (nếu là Mỹ) hoặc **VND** (nếu là Việt Nam). Đảm bảo đơn vị phù hợp.

##### **B. Node "Zillow Search" (HTTP Request)**
- **Không cần chỉnh sửa** nếu đã điền API key vào **Credentials** của node `httpRequest`.
- **Kiểm tra**:
  - URL: `https://www.zillow.com/webservice/GetSearchResults.htm?zws-id=YOUR_API_KEY&citystatezip=Ho+Chi+Minh&rentzestimate=true`
  - **Headers**:
    - `Content-Type: application/x-www-form-urlencoded`

##### **C. Node "Google Sheets" (googleSheets)**
- **Chọn Credentials**:
  - Chọn OAuth 2.0 Credentials đã cài đặt trước đó.
- **Chỉnh sửa Sheet Name**:
  - Thay `RealEstateDeals` thành tên file của bạn (ví dụ: `MyHotDeals2024`).
- **Cấu trúc tự động tạo**:
  - Workflow sẽ tạo **2 sheet**:
    1. `Deals` (lưu tất cả dữ liệu).
    2. `Top5Deals` (top 5 "hot deal" hàng ngày).

##### **D. Node "Gmail" (gmail)**
- **Chọn Credentials**:
  - Chọn OAuth 2.0 Credentials của Gmail.
- **Chỉnh sửa Email**:
  - Điền địa chỉ email muốn nhận báo cáo (ví dụ: `daututien@gmail.com`).
- **Chủ đề Email**:
  - Thay `🏡 Top 5 Hot Deals - [City]` thành tên phù hợp (ví dụ: `🏠 Top 5 Nhà Đất Giá Rẻ HCM - [Ngày]`).

##### **E. Node "Investment Calculator" (Code)**
- **Không cần chỉnh sửa** nếu muốn sử dụng công thức mặc định tính ROI.
- **Nếu muốn thay đổi**:
  - Mở tab **Code** → Sửa logic trong `javascript` (ví dụ: thay đổi tỷ lệ lợi nhuận mục tiêu).
  - Ví dụ công thức mặc định:
    ```javascript
    // ROI = (Thu nhập thuê - Chi phí) / Chi phí đầu tư * 100%
    const roi = ((rentZestimate * 12) - (price * 0.2)) / price * 100;
    ```

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Nhấn **"Execute Workflow"** → Chọn **node "9am Trigger"** → Nhấn **"Execute"**.
  - Kiểm tra:
    - **Google Sheets**: Dữ liệu có được lưu không?
    - **Gmail**: Email báo cáo có được gửi không?
- **Bật Active**:
  - Sau khi test thành công, chuyển **node "9am Trigger"** sang **Active**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Lọc theo khu vực cụ thể**:
   - Thay `citystatezip` trong node `Zillow Search` bằng mã quận/huyện (ví dụ: `Ho+Chi+Minh+District+1`).
   - **Lưu ý**: Zillow API hỗ trợ lọc theo quận, nhưng cần tra cứu mã chính xác.

2. **Gửi báo cáo đến Slack/Telegram**:
   - Thêm node `slack` hoặc `telegramBot` sau node `Gmail` để thông báo ngay khi có "hot deal".

3. **Lưu log hoạt động**:
   - Thêm node `stickyNote` để ghi lại lỗi hoặc thành công (ví dụ: `Workflow ran at [date] - [status]`).

4. **Tính toán chi phí khác**:
   - Trong node `Investment Calculator`, thêm chi phí khác như:
     - Thuế sở hữu.
     - Chi phí sửa chữa.
     - Chi phí quản lý.

5. **Tự động xóa dữ liệu cũ**:
   - Thêm node `googleSheets` sau với **Action: Delete Row** để xóa dữ liệu cũ hơn 30 ngày.

---

### 📌 **Kết Luận: Bắt Đầu Tự Động Hóa Ngay!**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào **strategy đầu tư** thay vì việc tra cứu thủ công. Với **chỉ 30 phút setup**, bạn sẽ:
✔ **Không bỏ lỡ bất kỳ cơ hội nào**.
✔ **Có dữ liệu đầu tư chuyên nghiệp**.
✔ **Tiết kiệm hàng trăm giờ/năm**.

**Hành động ngay!**
1. **Đăng ký VPS** để chạy workflow 24/7 (không phụ thuộc vào n8n.cloud).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Bật Active** và bắt đầu nhận báo cáo hàng ngày!

**Cần hỗ trợ?**
- Trả lời comment dưới bài viết hoặc liên hệ [T Zero](https://n8n.io/workflows/3030) để cập nhật.

---
**#TựĐộngHóaBấtĐộngSản #N8NVietnam #ZillowAPI #GoogleSheetsAutomation**