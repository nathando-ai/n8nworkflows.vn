---
title: "🔄 **Tự Động Hóa Sync Dữ Liệu MySQL → Google Sheets Với Kiểm Soát Trùng Lặp (Không Cần Code!)**"
description: "Giải pháp hoàn hảo để đồng bộ hóa tự động 50 bản ghi từ cơ sở dữ liệu MySQL sang Google Sheets hàng giờ, tránh trùng lặp và tiết kiệm thời gian quản lý dữ liệu cho các sếp. Hoạt động 24/7 mà không cần can thiệp thủ công."
slug: "tieu-dong-hoa-sync-mysql-google-sheets-trang-lap"
tags: [n8n, automation, mysql, google-sheets, duplicate-prevention, no-code, database-sync]
keywords: [n8n workflow mysql google sheets, tự động hóa đồng bộ dữ liệu, tránh trùng lặp trong google sheets, tự động hóa quản lý cơ sở dữ liệu, sync mysql google sheets tự động]
---

# 🚀 **Tự Động Hóa Sync Dữ Liệu MySQL → Google Sheets Với Kiểm Soát Trùng Lặp**

### **Nỗi Đau Của Các Sếp Khi Làm Thủ Công**
Các sếp thường phải **tốn thời gian quý báu** để:
- **Chuyển dữ liệu** từ MySQL sang Google Sheets thủ công hàng ngày/tuần.
- **Lo lắng về trùng lặp** khi đồng bộ nhiều lần, dẫn đến dữ liệu sai lệch.
- **Không có thời gian** để tập trung vào việc phân tích hoặc tối ưu hóa dữ liệu.

**Giải pháp này giúp các sếp:**
✅ **Tự động đồng bộ 50 bản ghi** từ MySQL sang Google Sheets **mỗi giờ** (hoặc thời gian tùy chọn).
✅ **Tránh trùng lặp hoàn toàn** bằng cách cập nhật trạng thái `sync = 1` cho các bản ghi đã đồng bộ.
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.
✅ **Tiết kiệm thời gian** lên đến **5-10 giờ/tuần** cho các sếp.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm thời gian** lên đến **5-10 giờ/tuần** so với cách làm thủ công.
- **Dữ liệu chính xác 100%** nhờ kiểm soát trùng lặp tự động.
- **Hoạt động liên tục** mà không cần can thiệp, giảm thiểu lỗi người dùng.
- **Dễ dàng mở rộng** để đồng bộ nhiều bảng hoặc thêm logic xử lý khác.
- **Không cần viết code** – chỉ cần cấu hình trong n8n.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI BẮT ĐẦU**]
Để workflow này hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản MySQL** (cung cấp **host, username, password, database name** và **table name** để lấy dữ liệu).
2. **Tài khoản Google Sheets** (cung cấp **OAuth 2.0 credentials** để ghi dữ liệu).
3. **Google Sheet đã tồn tại** (hoặc tạo mới) với **cấu trúc cột phù hợp** với dữ liệu từ MySQL.
4. **Cột `sync` trong bảng MySQL** (để lưu trạng thái đã đồng bộ, mặc định là `0`).
5. **n8n Self-hosted** (không dùng phiên bản miễn phí trên cloud để đảm bảo hoạt động 24/7).

:::note[**Gợi ý hạ tầng cho n8n**]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể **import workflow** từ file JSON hoặc **copy/paste JSON** vào n8n Editor.

**Bước 1:** Tải file JSON từ [n8n.io/workflows/6261](https://n8n.io/workflows/6261) hoặc sử dụng mã JSON dưới đây:

```json
{
  "nodes": [
    {
      "parameters": {
        "operation": "select",
        "query": "SELECT * FROM your_table_name LIMIT 50 WHERE sync = 0"
      },
      "name": "Select rows from a table",
      "type": "mySql",
      "credentials": {
        "mySql": "your_mysql_credentials"
      }
    },
    {
      "parameters": {
        "operation": "append",
        "sheetName": "Sheet1",
        "range": "A1:Z1000"
      },
      "name": "Append row in sheet",
      "type": "googleSheets",
      "credentials": {
        "googleSheetsOAuth2Api": "your_google_sheets_credentials"
      }
    },
    {
      "parameters": {
        "operation": "update",
        "query": "UPDATE your_table_name SET sync = 1 WHERE id IN ({{$node["Select rows from a table"].json["data"][0].id}})"
      },
      "name": "Update rows in a table",
      "type": "mySql",
      "credentials": {
        "mySql": "your_mysql_credentials"
      }
    },
    {
      "name": "Schedule Trigger Every n Mins",
      "type": "scheduleTrigger",
      "parameters": {
        "function": "minute",
        "time": "*/60" // Thay đổi thành thời gian đồng bộ mong muốn (ví dụ: */30 cho 30 phút)
      }
    },
    {
      "name": "No Operation, do nothing",
      "type": "noOp"
    },
    {
      "name": "Check if new record returned",
      "type": "if",
      "parameters": {
        "condition": "={{$node["Select rows from a table"].json["data"].length > 0}}"
      }
    }
  ],
  "connections": {
    "scheduleTrigger": ["Check if new record returned"],
    "Check if new record returned": ["Select rows from a table"],
    "Select rows from a table": ["Append row in sheet"],
    "Append row in sheet": ["Update rows in a table"],
    "Update rows in a table": ["No Operation, do nothing"]
  }
}
```

**Bước 2:** Mở **n8n Editor** → Chọn **Import Workflow** → Dán JSON hoặc tải file JSON.

---

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Các sếp **cần chỉnh sửa** các tham số sau để workflow hoạt động chính xác:

##### **A. Node `Select rows from a table` (MySQL)**
- **Tham số `query`:**
  ```sql
  SELECT * FROM your_table_name LIMIT 50 WHERE sync = 0
  ```
  - Thay `your_table_name` bằng **tên bảng** trong MySQL.
  - Cột `sync` phải tồn tại và mặc định là `0` (chưa đồng bộ).
  - Thay `LIMIT 50` nếu muốn lấy nhiều hơn 50 bản ghi.

##### **B. Node `Append row in sheet` (Google Sheets)**
- **Tham số `sheetName`:** Tên của **Google Sheet** muốn đồng bộ.
- **Tham số `range`:** Địa chỉ ô bắt đầu ghi dữ liệu (ví dụ: `A1:Z1000`).
  - **Lưu ý:** Cấu trúc cột trong Google Sheets **phải khớp** với kết quả từ MySQL.

##### **C. Node `Update rows in a table` (MySQL)**
- **Tham số `query`:**
  ```sql
  UPDATE your_table_name SET sync = 1 WHERE id IN ({{$node["Select rows from a table"].json["data"][0].id}})
  ```
  - Thay `your_table_name` bằng tên bảng.
  - **Cột `id`** phải tồn tại trong bảng MySQL (hoặc thay bằng cột khóa chính khác).
  - **Lưu ý:** Nếu bảng có nhiều cột ID, cần điều chỉnh phần `id` trong query.

##### **D. Node `Schedule Trigger`**
- **Tham số `time`:** Thay đổi thời gian đồng bộ (ví dụ: `*/30` cho **30 phút/lần**).
  - Cú pháp:
    - `*/60` → Đồng bộ **mỗi giờ**.
    - `*/30` → Đồng bộ **mỗi 30 phút**.
    - `*/15` → Đồng bộ **mỗi 15 phút**.

##### **E. Node `Check if new record returned` (If)**
- **Tham số `condition`:**
  ```json
  ={{$node["Select rows from a table"].json["data"].length > 0}}
  ```
  - Nếu không có bản ghi mới (`sync = 0`), workflow sẽ **bỏ qua** phần đồng bộ.

---

#### **3. Kích Hoạt ⚡️**
**Bước 1:** **Test Run** với dữ liệu mẫu:
- Chọn **Run Workflow** và kiểm tra kết quả trong **Google Sheets** và **MySQL**.

**Bước 2:** **Bật Active Workflow:**
- Đảm bảo **Schedule Trigger** được kích hoạt và **Active** trong n8n.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[**CÁCH TIẾP CẬN HƠN**]
1. **Thêm Log Lịch Sử Đồng Bộ:**
   - Sử dụng **node `stickyNote`** để ghi lại thời gian đồng bộ và số bản ghi đã xử lý.
   - Ví dụ:
     ```json
     "parameters": {
       "text": "Đồng bộ thành công tại {{ $datetime.now('YYYY-MM-DD HH:mm:ss') }}. Số bản ghi: {{ $node["Select rows from a table"].json["data"].length }}"
     }
     ```

2. **Gửi Báo Cáo Định Kỳ qua Email/Slack:**
   - Kết hợp với **node `email`** hoặc **node `slack`** để thông báo khi có lỗi hoặc đồng bộ thành công.

3. **Đồng Bộ Nhiều Bảng:**
   - Sử dụng **node `mySql`** để lấy dữ liệu từ nhiều bảng và **node `switch`** để phân loại trước khi ghi vào Google Sheets.

4. **Lọc Dữ Liệu Trước Khi Đồng Bộ:**
   - Sử dụng **node `function`** để thêm logic lọc (ví dụ: chỉ đồng bộ dữ liệu mới trong ngày).

5. **Sử Dụng API Key An Toàn:**
   - Nếu MySQL hoặc Google Sheets yêu cầu **API Key**, các sếp nên **mã hóa** trong n8n bằng **node `set`** hoặc **environment variables**.
:::

---

### 📌 **Kết Luận**
Workflow này **giải quyết hoàn toàn** vấn đề đồng bộ dữ liệu từ MySQL sang Google Sheets **một cách tự động, tránh trùng lặp và tiết kiệm thời gian** cho các sếp.

**Hành động ngay hôm nay:**
1. **Chuẩn bị tài khoản MySQL và Google Sheets**.
2. **Import workflow** và **cấu hình** theo hướng dẫn.
3. **Bật Schedule Trigger** và **để nó hoạt động 24/7!**

**🚀 CÓ THỂ CẦN GỢI Ý HOẶC TRỢ GIÚP KHÁC?** Hãy để lại **comment** bên dưới hoặc liên hệ với chúng tôi để hỗ trợ chi tiết! 😊