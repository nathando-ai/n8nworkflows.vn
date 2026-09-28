---
title: "🚀 Tự Động Kiểm Tra & Vô Hiệu Hóa Link Nghi Ngờ Trong CV & Google Sheets (Postgres + No-Code)"
description: "Workflow tự động hóa kiểm tra định kỳ (mỗi 3 ngày) tất cả các link ứng tuyển trong cơ sở dữ liệu PostgreSQL và Google Sheets, vô hiệu hóa link chết (404/soft-404) để duy trì chất lượng dữ liệu và trải nghiệm ứng viên. Giúp tiết kiệm 10+ giờ công mỗi tháng cho bộ phận HR."
slug: "tieu-dong-kiem-tra-link-nghi-ngo-postgres-google-sheets"
tags: [n8n, automation, no-code, postgresql, google-sheets, data-cleaning]
keywords: [tự động hóa kiểm tra link, vô hiệu hóa link chết, postgresql n8n, google sheets automation, data hygiene, no-code workflow]
---

# 🚀 **Tự Động Kiểm Tra & Vô Hiệu Hóa Link Nghi Ngờ Trong CV (Postgres + Google Sheets)**

### **Nỗi Đau Của Các Sếp HR**
Bạn có bao giờ phải mất **10+ giờ** mỗi tháng để:
- **Kiểm tra thủ công** hàng trăm link ứng tuyển trong CV?
- **Sửa chữa hoặc vô hiệu hóa** link chết (404/soft-404) gây mất uy tín cho doanh nghiệp?
- **Cập nhật lại** dữ liệu trong cả cơ sở dữ liệu PostgreSQL **và** Google Sheets?

**Workflow này giải quyết tất cả!** Với **tự động hóa 100% không cần code**, bạn sẽ:
✅ **Kiểm tra định kỳ** (mỗi 3 ngày) tất cả link ứng tuyển.
✅ **Vô hiệu hóa tự động** link chết (404/soft-404) trong **PostgreSQL và Google Sheets**.
✅ **Tiết kiệm 10+ giờ công/tháng** cho bộ phận HR.
✅ **Duy trì chất lượng dữ liệu** và trải nghiệm ứng viên.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần kiểm tra thủ công hàng tuần.
- **Chất lượng dữ liệu cao**: Vô hiệu hóa link chết ngay khi phát hiện.
- **Cập nhật đồng bộ**: Thay đổi trạng thái trong **PostgreSQL và Google Sheets** một lúc.
- **Tự động hóa hoàn toàn**: Chỉ cần **cài đặt 1 lần**, workflow chạy tự động mỗi 3 ngày.
- **Duy trì uy tín**: Tránh tình trạng ứng viên gặp link chết khi ứng tuyển.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản PostgreSQL** (để kết nối với cơ sở dữ liệu chứa thông tin CV).
✔ **Google Sheets API Key** (để cập nhật trạng thái trong bảng tính).
✔ **Thông tin kết nối**:
   - **PostgreSQL**: Host, Port, Database Name, Username, Password.
   - **Google Sheets**: Resource ID (ID của file Google Sheets), Sheet Name (tên trang tính).
✔ **Query SQL** để lấy danh sách link ứng tuyển (nếu chưa có, tham khảo phần **Cách cấu hình**).

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/14807](https://n8n.io/workflows/14807) (chọn **Download JSON**).
2. **Mở n8n Editor** (trên VPS hoặc n8n.io).
3. **Nhấn "Import"** và chọn file JSON vừa tải.
4. **Chọn "Import"** để hoàn tất.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Tải JSON** từ link trên.
2. **Mở n8n Editor** → **Create New Workflow** → **Paste JSON**.
3. **Nhấn "Create"** để tạo workflow.

---
### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**

#### **🔹 Node 1: ⏰ Every 3 Days (Schedule Trigger)**
- **Không cần chỉnh sửa**, workflow sẽ chạy tự động mỗi **3 ngày 1 lần**.

#### **🔹 Node 2: 📥 Fetch Active Jobs (PostgreSQL)**
- **Cấu hình kết nối PostgreSQL**:
  - **Host**: `your-postgres-host.com`
  - **Port**: `5432` (mặc định)
  - **Database**: `your-database-name`
  - **Username/Password**: Điền thông tin từ tài khoản PostgreSQL của bạn.
- **Query SQL**:
  ```sql
  SELECT * FROM jobs WHERE status = 'active';
  ```
  *(Nếu bảng có tên khác, thay thế `jobs` và điều chỉnh điều kiện lọc.)*

#### **🔹 Node 3: 🔧 Prepare URLs (Code Node)**
- **Không cần chỉnh sửa**, node này chuẩn bị dữ liệu cho bước kiểm tra link.

#### **🔹 Node 4: 🔗 Check URLs (HTTP Request)**
- **Không cần chỉnh sửa**, node này gửi **HEAD request** để kiểm tra tính hợp lệ của link.

#### **🔹 Node 5: 🧠 Find Dead Jobs (Code Node)**
- **Không cần chỉnh sửa**, node này phân tích kết quả và xác định link chết (404/soft-404).
- **Nếu cần tùy chỉnh**:
  - Mở node này và chỉnh sửa logic trong **JavaScript** để phù hợp với trang web của bạn (ví dụ: kiểm tra redirect 301/302).

#### **🔹 Node 6: 🔀 Has Dead Jobs? (If Node)**
- **Không cần chỉnh sửa**, node này kiểm tra xem có link chết nào không.

#### **🔹 Node 7: ❌ Mark Inactive (PostgreSQL)**
- **Cấu hình query SQL để cập nhật trạng thái**:
  ```sql
  UPDATE jobs
  SET status = 'inactive'
  WHERE id = $json[0].id;
  ```
  *(Thay thế `id` và `status` theo cấu trúc bảng của bạn.)*

#### **🔹 Node 8: 📊 Mark Inactive (Google Sheets)**
- **Cấu hình Google Sheets**:
  - **Resource ID**: ID của file Google Sheets (thường là chuỗi dài trong URL: `https://docs.google.com/spreadsheets/d/ID_FILE/edit`).
  - **Sheet Name**: Tên trang tính (ví dụ: `Sheet1`).
  - **Range**: `A2:D` (điều chỉnh theo cột chứa ID và trạng thái).
  - **Append/Update**: Chọn **Append** (nếu muốn thêm dữ liệu mới) hoặc **Update** (nếu muốn cập nhật trực tiếp).

---
### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **Run Workflow** và kiểm tra kết quả.
   - Đảm bảo **PostgreSQL và Google Sheets** được cập nhật đúng.
2. **Bật Active**:
   - Sau khi test thành công, **nhấn "Active"** để workflow chạy tự động mỗi 3 ngày.

---
## ✍️ **Mẹo & Gợi Ý Nâng Cao**

### **1. Kết Nối với Slack/Telegram để Báo Cáo**
- **Thêm node Slack/Telegram** sau **Node 6 (Has Dead Jobs?)** để thông báo khi phát hiện link chết.
- **Cách làm**:
  - Thêm **Node Slack** (hoặc Telegram) vào workflow.
  - Kết nối với tài khoản Slack/Telegram của bạn.
  - Đặt **Message Template**:
    ```json
    {
      "text": "🚨 Đã phát hiện {{ $node["Has Dead Jobs?"].json["deadJobs"] | length }} link chết trong CV!"
    }
    ```

### **2. Lưu Log Kiểm Tra vào Google Sheets**
- **Thêm node Google Sheets** để ghi lại lịch sử kiểm tra (ngày giờ, số link chết, ID CV).
- **Query mẫu**:
  ```sql
  INSERT INTO logs (date, dead_jobs_count, job_id)
  VALUES ($json[0].date, $json[0].deadJobs.length, $json[0].id);
  ```

### **3. Gửi Báo Cáo Định Kỳ qua Email**
- **Thêm node Email** (ví dụ: **SendGrid** hoặc **Gmail SMTP**) để gửi báo cáo hàng tuần.
- **Nội dung email**:
  ```markdown
  **Báo cáo tự động hóa kiểm tra link (Ngày: {{ $node["Schedule Trigger"].json["$date"] }}):**
  - Tổng số CV kiểm tra: {{ $node["Fetch Active Jobs"].json.length }}
  - Số link chết phát hiện: {{ $node["Has Dead Jobs?"].json["deadJobs"] | length }}
  ```

### **4. Tùy Chỉnh Thời Gian Kiểm Tra**
- **Đổi từ "Every 3 Days" thành "Every Day"** (nếu cần kiểm tra thường xuyên hơn).
- **Cách làm**:
  - Mở **Node 1 (Schedule Trigger)** → Chọn **Every Day** thay vì **Every 3 Days**.

---
## 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp HR khỏi công việc **kiểm tra link thủ công**, đồng thời **đảm bảo chất lượng dữ liệu** và **trải nghiệm ứng viên** tốt nhất. **Chỉ cần cài đặt 1 lần**, workflow sẽ **chạy tự động mỗi 3 ngày**, vô hiệu hóa link chết ngay khi phát hiện.

**Hành động ngay hôm nay!**
1. **Import workflow** theo hướng dẫn trên.
2. **Cấu hình PostgreSQL và Google Sheets**.
3. **Bật Active** và **nhận kết quả tự động hóa ngay!**

👉 **Bạn có thắc mắc gì?** Hãy để lại comment dưới đây, tôi sẽ hỗ trợ chi tiết! 🚀