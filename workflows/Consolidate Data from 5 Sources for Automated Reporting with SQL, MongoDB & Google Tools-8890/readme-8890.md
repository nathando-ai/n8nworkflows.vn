---
title: "🚀 Tự Động Hoà 5 Nguồn Dữ Liệu Khác Nhau Vào Báo Cáo Google Sheets: SQL, MongoDB & Google Tools"
description: "Giải pháp tự động hóa 100% không code để hợp nhất dữ liệu từ Google Sheets, PostgreSQL, MongoDB, Microsoft SQL Server và Google Analytics vào một bảng Google Sheets duy nhất cho báo cáo hàng ngày/ngày định kỳ. Tiết kiệm 10+ giờ công mỗi tuần cho các sếp và đội ngũ marketing/analyst."
slug: "tieu-dong-hoa-5-nguon-du-lieu-vao-bao-cao-google-sheets"
tags: [n8n, automation, no-code, google-sheets, sql-mongodb, google-analytics, reporting]
keywords: [tự động hóa n8n, hợp nhất dữ liệu từ nhiều nguồn, báo cáo tự động google sheets, sql mongodb google tools, tự động hóa báo cáo hàng ngày]
---

# 🚀 **Hợp Nhất 5 Nguồn Dữ Liệu Khác Nhau Vào Báo Cáo Tự Động: Từ SQL, MongoDB Đến Google Tools**

### **Nỗi Đau Của Các Sếp Và Giải Pháp N8n**
Các sếp và đội ngũ **marketing, sales, hoặc data analyst** thường phải **tốn thời gian vô cùng** để:
- **Lấy dữ liệu** từ nhiều nguồn khác nhau (Google Sheets, cơ sở dữ liệu SQL, MongoDB, Google Analytics).
- **Sắp xếp và hợp nhất** dữ liệu từ các hệ thống không tương thích.
- **Xử lý lỗi schema** (các cột không khớp nhau, định dạng khác nhau).
- **Tạo báo cáo thủ công** hàng ngày/ngày định kỳ, dẫn đến **sai sót và mất thời gian**.

**Workflow này giải quyết tất cả vấn đề trên bằng cách:**
✅ **Tự động lấy dữ liệu** từ **5 nguồn khác nhau** (Google Sheets, PostgreSQL, MongoDB, Microsoft SQL Server, Google Analytics).
✅ **Hợp nhất và chuẩn hóa** dữ liệu một cách thông minh (thêm ID nguồn để theo dõi nguồn gốc).
✅ **Ghi kết quả vào Google Sheets** với **schema thống nhất**, sẵn sàng cho báo cáo.
✅ **Chạy tự động** theo lịch trình (ngày, tuần, tháng) **không cần can thiệp thủ công**.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này **chạy 24/7 ổn định**, các sếp nên **self-host n8n** trên VPS riêng thay vì dùng phiên bản cloud.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đảm bảo tốc độ cao cho workflow)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ công mỗi tuần** (không cần lấy dữ liệu thủ công).
- **Báo cáo chính xác 100%** (không sai sót do nhập liệu sai).
- **Theo dõi nguồn gốc dữ liệu** (mỗi dòng dữ liệu ghi rõ nguồn gốc từ Google Sheets, SQL, MongoDB...).
- **Tự động hóa hoàn toàn** (chỉ cần cấu hình 1 lần, sau đó workflow chạy tự động).
- **Dữ liệu sẵn sàng cho phân tích** (Google Sheets có thể kết nối với Looker Studio, Power BI...).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Google** (để truy cập Google Sheets, Google Analytics).
✔ **Credentials cho các cơ sở dữ liệu**:
   - **PostgreSQL**: Host, Port, Database Name, Username, Password.
   - **Microsoft SQL Server**: Server Name, Database Name, Username, Password.
   - **MongoDB**: Connection URI (bao gồm Username, Password, Database Name).
✔ **Google Sheets**:
   - **File mẫu** (để lưu kết quả cuối cùng).
   - **Sheet Name** (ví dụ: "Báo cáo tổng hợp").
   - **Dòng đầu tiên** (cần định nghĩa các cột: Name, Email, Title, Company, SourceID, ...).
✔ **API Key Google Analytics** (nếu muốn lấy dữ liệu từ GA).

---
:::note[LƯU Ý QUAN TRỌNG]
- **Không cần biết code** để sử dụng workflow này.
- **Workflow chỉ chạy khi có dữ liệu mới** (không ghi đè dữ liệu cũ).
- **Nếu dữ liệu trong nguồn thay đổi**, workflow sẽ tự động lấy lại và cập nhật.
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
**Cách 1: Từ file JSON**
1. Tải workflow từ [n8n.io/workflows/8890](https://n8n.io/workflows/8890) (chọn **Download JSON**).
2. Mở **n8n Editor** (trên VPS hoặc n8n.cloud).
3. Nhấn **Import** → Chọn file JSON vừa tải.
4. Workflow sẽ xuất hiện trên canvas.

**Cách 2: Copy/Paste JSON**
1. Mở **n8n Editor**.
2. Nhấn **Import** → Chọn **Paste JSON**.
3. Dán JSON từ [n8n.io/workflows/8890](https://n8n.io/workflows/8890) (chọn **Copy JSON**).
4. Nhấn **Import**.

---

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflows này có **14 nodes**, nhưng **các node quan trọng nhất** cần cấu hình kỹ là:

##### **🔹 Node Schedule Trigger (Động cơ chạy theo lịch)**
- **Cấu hình**:
  - **Frequency**: Chọn **Daily** (hàng ngày) hoặc **Weekly** (hàng tuần).
  - **Time**: Đặt giờ chạy (ví dụ: 8h sáng để báo cáo sẵn sàng vào buổi sáng).
  - **Time Zone**: Chọn múi giờ phù hợp (ví dụ: Asia/Ho_Chi_Minh).

##### **🔹 Node Google Sheets Source (Lấy dữ liệu từ Google Sheets)**
- **Cấu hình**:
  - **Credentials**: Chọn tài khoản Google đã kết nối.
  - **Spreadsheet ID**: Tìm trong URL của file Google Sheets (ví dụ: `1AbCdEfGhIjKlMnOpQrStUvWxYz`).
  - **Sheet Name**: Tên sheet chứa dữ liệu (ví dụ: "Dữ liệu khách hàng").
  - **Range**: Chọn phạm vi dữ liệu (ví dụ: `A1:Z1000`).

##### **🔹 Node PostgreSQL & Microsoft SQL Server (Lấy dữ liệu từ cơ sở dữ liệu)**
- **Cấu hình chung**:
  - **Host**: Địa chỉ IP/VPS của cơ sở dữ liệu.
  - **Port**: Thường là `5432` (PostgreSQL) hoặc `1433` (SQL Server).
  - **Database Name**: Tên cơ sở dữ liệu.
  - **Username & Password**: Tài khoản admin hoặc có quyền truy cập.
- **Query**:
  - **PostgreSQL**: Ví dụ:
    ```sql
    SELECT * FROM customers WHERE created_at > NOW() - INTERVAL '7 days';
    ```
  - **Microsoft SQL Server**: Ví dụ:
    ```sql
    SELECT * FROM Leads WHERE status = 'active';
    ```

##### **🔹 Node MongoDB (Lấy dữ liệu từ MongoDB)**
- **Cấu hình**:
  - **Connection URI**: Địa chỉ kết nối (ví dụ: `mongodb://user:pass@host:27017/dbname`).
  - **Collection**: Tên collection (ví dụ: `customers`).
  - **Query**: Lọc dữ liệu (ví dụ: `{ "status": "active" }`).

##### **🔹 Node Google Analytics (Lấy dữ liệu từ GA)**
- **Cấu hình**:
  - **Credentials**: Chọn tài khoản Google Analytics đã kết nối.
  - **View ID**: Tìm trong URL của GA (ví dụ: `ga:12345678`).
  - **Date Range**: Chọn khoảng thời gian (ví dụ: `7daysAgoToday`).

##### **🔹 Node Merge (Hợp nhất dữ liệu)**
- **Lưu ý**:
  - Workflow **tự động thêm SourceID** vào mỗi dòng dữ liệu để theo dõi nguồn gốc.
  - Nếu **schema không khớp**, dữ liệu sẽ bị bỏ qua (cần kiểm tra trong **Node Process Merged Data**).

##### **🔹 Node Process Merged Data (Xử lý dữ liệu)**
- **Lưu ý**:
  - Node này **chỉnh sửa và chuẩn hóa** dữ liệu (ví dụ: đổi tên cột, loại bỏ dữ liệu trống).
  - **Mở node này** và kiểm tra **JavaScript code** để đảm bảo:
    - Các cột **Name, Email, Title, Company** có định dạng thống nhất.
    - **SourceID** được thêm vào mỗi dòng.

##### **🔹 Node Final Google Sheet (Ghi kết quả vào Google Sheets)**
- **Cấu hình**:
  - **Spreadsheet ID**: Địa chỉ file Google Sheets **mẫu** (đã chuẩn bị trước).
  - **Sheet Name**: Tên sheet lưu kết quả (ví dụ: "Báo cáo tổng hợp").
  - **Range**: Chọn từ **dòng 2** (dòng 1 là tiêu đề).
  - **Operation**: Chọn **Append or Update** (cập nhật nếu dữ liệu đã tồn tại).

---

#### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run** (kiểm tra dữ liệu mẫu):
   - Nhấn **Run Workflow** và chọn **Test Execution**.
   - Kiểm tra **Google Sheets** có xuất dữ liệu không.
2. **Bật Active**:
   - Sau khi test thành công, **bật Active** trên node **Schedule Trigger**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Thêm Slack/Telegram Notifications**:
   - Sử dụng **node Slack** hoặc **Telegram Bot** để thông báo khi workflow chạy thành công/thất bại.
   - **Cách làm**:
     - Thêm node **Slack** hoặc **Telegram Bot** sau **Final Google Sheet**.
     - Gửi tin nhắn: `📊 Báo cáo đã cập nhật thành công! Dữ liệu mới: {{ $json("$.length") }} dòng`.

2. **Lưu Log Dữ Liệu**:
   - Sử dụng **node StickyNote** hoặc **Google Drive** để lưu lịch sử chạy.
   - **Cách làm**:
     - Thêm node **StickyNote** sau **Final Google Sheet**.
     - Lưu thông tin: `Workflow chạy vào {{ $node["Schedule Trigger"].date }} với {{ $json("$.length") }} dòng mới`.

3. **Tự động Gửi Báo Cáo qua Email**:
   - Kết hợp với **node Email** (Gmail/SMTP) để gửi báo cáo định kỳ.
   - **Cách làm**:
     - Thêm node **Gmail** sau **Final Google Sheet**.
     - Gửi email với **link trực tiếp** đến Google Sheets.

4. **Tùy Chỉnh Query SQL/MongoDB**:
   - Nếu dữ liệu trong cơ sở dữ liệu thay đổi, **cập nhật query** trong các node tương ứng.
   - Ví dụ: Thay đổi điều kiện lọc trong **PostgreSQL** để lấy dữ liệu mới nhất.

5. **Sử Dụng Looker Studio cho Báo Cáo Tương Tác**:
   - Kết nối **Google Sheets** kết quả với **Looker Studio** để tạo dashboard tương tác.
   - **Cách làm**:
     - Mở **Looker Studio** → Tạo báo cáo mới → Kết nối với Google Sheets.
     - Chọn sheet "Báo cáo tổng hợp" và tạo biểu đồ.

---

### 📌 **Kết Luận: Tự Động Hóa Báo Cáo Hàng Ngày Với N8n**
Workflow này **giải phóng thời gian** cho các sếp và đội ngũ **từ việc lấy dữ liệu thủ công** sang **tự động hóa hoàn toàn** với **5 nguồn dữ liệu khác nhau**.

**Bước đầu tiên:**
1. **Cài đặt n8n trên VPS** (để workflow chạy 24/7).
2. **Import workflow** và **cấu hình các node** theo hướng dẫn.
3. **Bật Active** và **chờ nó làm việc cho bạn!**

**Kết quả?**
✅ **Báo cáo tự động** hàng ngày/ngày định kỳ.
✅ **Dữ liệu chính xác** và **sẵn sàng phân tích**.
✅ **Tiết kiệm 10+ giờ công** mỗi tuần.

**🚀 Hãy tự động hóa ngay hôm nay!** Nếu có vấn đề, **hãy comment bên dưới** hoặc liên hệ với **iTechNotion** (tác giả của workflow) để hỗ trợ.

---
**📌 Xem thêm:**
- [Tutorial Cài n8n trên VPS](https://docs.n8n.io/hosting/self-hosting-on-a-vps/)
- [Hướng dẫn kết nối Google Sheets với n8n](https://docs.n8n.io/integrations/builtins/googleSheets/)
- [Tự động hóa với Google Analytics](https://docs.n8n.io/integrations/builtins/googleAnalytics/)