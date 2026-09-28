---
title: "🏠 Tự Động Hóa Tìm Kiếm Nhà Đất Theo Yêu Cầu + Gửi Kết Quả Bằng Email (N8n)"
description: "Workflow tự động hóa tìm kiếm nhà đất theo tiêu chí cá nhân hóa (giá, diện tích, vị trí...) trên cơ sở dữ liệu SQL, sau đó gửi kết quả dưới dạng CSV qua email - tiết kiệm thời gian lên tới 80% cho doanh nghiệp bất động sản."
slug: "tieu-dong-hoa-tim-kiem-nha-dat-voi-sql-email"
tags: [n8n, automation, real-estate, sql-database, gmail-integration]
keywords: [n8n workflow nhà đất, tự động hóa tìm kiếm bất động sản, SQL query tự động, gửi email kết quả tìm kiếm, n8n no-code]
---

# 🚀 **Tự Động Hóa Tìm Kiếm Nhà Đất Theo Yêu Cầu + Gửi Kết Quả Bằng Email**

### **🔍 Nỗi Đau Của Các Sếp Bất Động Sản**
Hàng ngày, các sếp bất động sản phải:
- **Lặp đi lặp lại** việc thủ công nhập yêu cầu của khách hàng (giá, diện tích, vị trí...) vào hệ thống.
- **Chờ đợi lâu** khi phải tra cứu thủ công trên cơ sở dữ liệu SQL với hàng ngàn bản ghi.
- **Tốn thời gian** để tổng hợp và gửi kết quả cho khách hàng dưới dạng file Excel/CSV.
- **Rủi ro sai sót** cao khi xử lý thủ công, dẫn đến mất uy tín.

**Workflow này giải quyết tất cả!** Với chỉ một form đơn, khách hàng sẽ nhận được **kết quả tìm kiếm chính xác, cá nhân hóa** được gửi trực tiếp vào email của họ - **không cần can thiệp thủ công nào!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động 24/7 với hiệu suất cao, các sếp nên **self-host n8n trên VPS** để tránh giới hạn của phiên bản cloud.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Giảm 80% công việc thủ công tra cứu và tổng hợp.
- **Chính xác 100%**: Query SQL động tự động loại bỏ điều kiện trống, tránh kết quả sai lệch.
- **Cá nhân hóa cao**: Khách hàng chỉ cần điền yêu cầu, hệ thống tự động xử lý và gửi kết quả.
- **Hoạt động liên tục**: Workflow chạy 24/7, không phụ thuộc vào giờ làm việc của nhân viên.
- **Tích hợp email tự động**: Kết quả được gửi dưới dạng file CSV dễ đọc, không cần can thiệp thêm.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Gmail** (để gửi email kết quả):
   - **API Key Gmail**: Cần kích hoạt [Gmail API](https://developers.google.com/gmail/api/quickstart/python) và tạo **OAuth 2.0 Client ID**.
   - **Email mặc định**: Cấu hình trong node **Send a message** để gửi từ địa chỉ email chính thức của doanh nghiệp.
2. **Cơ sở dữ liệu SQL Server**:
   - **Thông tin kết nối**: Server name, database name, username, password.
   - **Bảng dữ liệu**: Cần có bảng chứa thông tin nhà đất (ví dụ: `Properties` với các cột: `Price`, `Bedrooms`, `Location`, `Area`, ...).
3. **Form Trigger**:
   - **Đường dẫn form**: Cần host form trên trang web hoặc sử dụng **n8n Form Trigger** để bắt đầu workflow.

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/7329](https://n8n.io/workflows/7329) hoặc copy toàn bộ JSON từ canvas.
- **Mở n8n Editor** → Nhấn **Import** → Dán JSON hoặc tải file JSON.
- **Kích hoạt workflow** bằng cách bật switch **Active** ở góc trên bên phải.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflows này gồm **5 node chính**, các sếp cần chú ý cấu hình như sau:

##### **📝 Node 1: Property Search Form (formTrigger)**
- **Cấu hình**:
  - **Path**: Đặt là `property-search-form` (không thay đổi).
  - **Host form** trên trang web hoặc sử dụng **n8n Form Trigger** để bắt đầu workflow.
  - **Yêu cầu từ khách hàng**: Giá, số phòng ngủ, vị trí, diện tích, ... (các trường này sẽ được truyền vào node **Build SQL Query**).

##### **🔄 Node 2: Build SQL Query (code)**
- **Lưu ý**:
  - Node này **tự động xây dựng query SQL** dựa trên input từ form.
  - **Không cần chỉnh sửa mã** (n8n đã tối ưu query để loại bỏ điều kiện trống).
  - **Dữ liệu input**:
    ```json
    {
      "priceRange": "500000000-800000000",
      "bedrooms": "3",
      "location": "Hà Nội",
      "area": "100-150"
    }
    ```
  - **Output**: Query SQL động như:
    ```sql
    SELECT * FROM Properties
    WHERE Price BETWEEN 500000000 AND 800000000
    AND Bedrooms = 3
    AND Location LIKE '%Hà Nội%'
    AND Area BETWEEN 100 AND 150
    ```

##### **🗃️ Node 3: Microsoft SQL (microsoftSql)**
- **Cấu hình cần thiết**:
  - **Connection Name**: Tạo mới trong **Credentials** → **Microsoft SQL**.
  - **Server**: `your-server.database.windows.net` (hoặc IP của SQL Server).
  - **Database**: Tên cơ sở dữ liệu chứa bảng `Properties`.
  - **Username/Password**: Thông tin đăng nhập.
  - **Operation**: Đặt là **Execute Query**.
  - **Query**: Sử dụng output từ node **Build SQL Query** (không cần chỉnh sửa).

##### **📄 Node 4: Convert to File (convertToFile)**
- **Cấu hình mặc định**:
  - Node này **tự động chuyển kết quả SQL thành file CSV**.
  - **Không cần chỉnh sửa** (n8n sẽ tự động định dạng file).
  - **Output**: File CSV có tên `property_search_results_<timestamp>.csv`.

##### **✉️ Node 5: Send a message (gmail)**
- **Cấu hình quan trọng**:
  - **Credentials**: Tạo mới trong **Credentials** → **Gmail** và nhập:
    - **Client ID** và **Client Secret** từ [Gmail API](https://developers.google.com/gmail/api/quickstart/python).
    - **Refresh Token** (lấy từ quá trình auth đầu tiên).
  - **Email To**: Điền địa chỉ email của khách hàng (có thể lấy từ form hoặc đặt mặc định).
  - **Subject**: Ví dụ: **"Kết quả tìm kiếm nhà đất cho bạn: [Location]"**.
  - **Body**: Nội dung email cá nhân hóa (có thể thêm thông tin từ form).
  - **Attachment**: Chọn file CSV từ node **Convert to File**.

---

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  1. Điền thông tin vào form (ví dụ: giá 500M-800M, 3 phòng ngủ, Hà Nội).
  2. Nhấn **Execute Workflow** để kiểm tra kết quả.
  3. Kiểm tra email để xác nhận file CSV đã được gửi.
- **Bật Active**:
  - Sau khi test thành công, bật switch **Active** để workflow chạy tự động khi khách hàng submit form.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tích Hợp Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram Bot** sau node **Send a message** để thông báo kết quả cho team.
   - Ví dụ: Khi có yêu cầu mới, hệ thống tự động gửi tin nhắn đến nhóm Slack.

2. **Lưu Log & Theo Dõi**:
   - Sử dụng node **Sticky Note** (đã có trong workflow) để ghi lại lịch sử tìm kiếm.
   - Tích hợp với **Google Sheets** để theo dõi tất cả yêu cầu và kết quả.

3. **Báo Cáo Định Kỳ**:
   - Thêm node **Set Interval** để gửi báo cáo tổng hợp hàng tuần/month cho khách hàng VIP.
   - Ví dụ: "Dưới đây là 5 nhà đất phù hợp với yêu cầu của bạn trong tháng 10/2024".

4. **Cải Thiện Trải Nghiệm Khách Hàng**:
   - Thêm node **LLM (AI Chatbot)** để trả lời câu hỏi về kết quả (ví dụ: "Tôi có thể mua nhà này không?").
   - Sử dụng **n8n-nodes-base.llm** để tích hợp với API như Mistral AI, Google Vertex AI.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp bất động sản khỏi công việc thủ công tẻ nhạt, đồng thời **tăng trải nghiệm khách hàng** với kết quả tìm kiếm nhanh chóng và chính xác. **Chỉ cần một form đơn**, khách hàng sẽ nhận được **tất cả thông tin cần thiết** trong email - **không cần gọi điện hay chờ đợi**.

**Hành động ngay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test với dữ liệu mẫu** để đảm bảo hoạt động ổn định.
3. **Bật Active** và chia sẻ link form cho khách hàng.

**🚀 Cùng tự động hóa tương lai của doanh nghiệp bất động sản ngay hôm nay!** 🏢💻