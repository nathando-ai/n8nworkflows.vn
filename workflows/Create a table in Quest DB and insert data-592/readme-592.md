---
title: "🚀 Tự Động Hoàn Thành Bảng Dữ Liệu QuestDB Và Chèn Dữ Liệu Mới - Không Cần Code"
description: "Workflow này giúp các sếp tự động tạo bảng trong QuestDB và chèn dữ liệu mới chỉ với một cú nhấp chuột, tiết kiệm thời gian và giảm thiểu lỗi thủ công. Đặc biệt phù hợp cho các team engineering cần xử lý dữ liệu hiệu quả."
slug: "tự-dộng-hoàn-thành-bảng-dữ-liệu-questdb"
tags: [n8n, automation, questdb, no-code, database, engineering]
keywords: [n8n workflow questdb, tự động hóa questdb, tạo bảng và chèn dữ liệu questdb, tự động hóa database, n8n engineering]
---

# 🚀 Tự Động Tạo Bảng và Chèn Dữ Liệu vào QuestDB - Không Cần Code

### **Nỗi Đau Thực Tế Của Các Sếp**
Các sếp và kỹ sư phần mềm thường phải mất thời gian quý báu để thủ công tạo bảng trong cơ sở dữ liệu và chèn dữ liệu mới. Quá trình này không chỉ tốn thời gian mà còn dễ mắc lỗi, đặc biệt khi phải làm lại nhiều lần. **Workflow này giải quyết vấn đề này bằng cách tự động hóa toàn bộ quy trình chỉ với một cú nhấp chuột!**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 Kết Quả Các Sếp Nhận Được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần thủ công tạo bảng và chèn dữ liệu.
- **Chính xác cao**: Tránh sai sót do nhập liệu thủ công.
- **Hoạt động liên tục**: Tự động hóa hoàn toàn, không phụ thuộc vào thời gian làm việc.
- **Dễ dàng mở rộng**: Chỉ cần thay đổi dữ liệu đầu vào mà không cần sửa code.
:::

---

### 🔧 Yêu Cầu Cần Thiết
:::info[CHUẨN BỊ]
- **Tài khoản QuestDB**: Các sếp cần có một tài khoản QuestDB hoạt động và **API Key** để kết nối.
- **n8n Self-hosted**: Workflow này yêu cầu n8n được cài đặt trên máy chủ riêng (không dùng phiên bản cloud miễn phí).
- **Dữ liệu mẫu**: Để test, các sếp cần chuẩn bị một tập dữ liệu mẫu để chèn vào bảng.
:::

---

### 🚀 Cách Import & Lưu Ý Khi "Lên Đồ"

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Truy cập [n8n Editor](https://n8n.io/editor).
2. Nhấp vào **Import Workflow** và chọn file JSON hoặc dán JSON từ [link gốc](https://n8n.io/workflows/592).
3. Chọn **Create Workflow** để bắt đầu.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này bao gồm **4 node chính**, các sếp cần chú ý cấu hình như sau:

##### **Node 1: Manual Trigger (Bắt Đầu Tự Động)**
- **Tên node**: "On clicking 'execute'"
- **Lưu ý**: Node này chỉ hoạt động khi các sếp nhấp vào nút **"Execute"** trong n8n Editor.

##### **Node 2: Set (Cấu Hình Dữ Liệu)**
- **Tên node**: "Set"
- **Lưu ý**:
  - Các sếp cần **cấu hình dữ liệu đầu vào** cho bảng mới (ví dụ: tên bảng, cột, kiểu dữ liệu).
  - Ví dụ:
    ```json
    {
      "tableName": "dữ_liệu_mới",
      "columns": [
        {"name": "id", "type": "INTEGER"},
        {"name": "tên", "type": "VARCHAR(100)"},
        {"name": "giá_trị", "type": "FLOAT"}
      ]
    }
    ```

##### **Node 3 & 4: QuestDB (Thực Thi Query)**
- **Tên node**: "QuestDB" (tạo bảng) và "QuestDB1" (chèn dữ liệu)
- **Lưu ý**:
  - **Credentials**: Chọn **"questDb"** trong danh sách credentials đã cấu hình trước.
  - **Node "QuestDB"**:
    - **Operation**: Chọn **"executeQuery"**.
    - **Query**: Dùng để tạo bảng mới (ví dụ: `CREATE TABLE IF NOT EXISTS dữ_liệu_mới (id INTEGER, tên VARCHAR(100), giá_trị FLOAT)`).
  - **Node "QuestDB1"**:
    - **Operation**: Chọn **"executeQuery"** (hoặc **"insert"** nếu sử dụng API mới).
    - **Query**: Dùng để chèn dữ liệu (ví dụ: `INSERT INTO dữ_liệu_mới (tên, giá_trị) VALUES ('dữ_liệu_test', 100.5)`).

##### **Cách Kết Nối QuestDB**
1. Vào **Credentials** trong n8n Editor.
2. Nhấp **Add Credential** → Chọn **"QuestDB"**.
3. Điền thông tin:
   - **Host**: `http://<IP_CỦA_MÁY_CHỦ>:`<PORT> (ví dụ: `http://123.456.789.0:8812`)
   - **Username**: Tên người dùng QuestDB.
   - **Password**: Mật khẩu QuestDB.
   - **Database**: Tên cơ sở dữ liệu (nếu có).

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhấp vào nút **"Execute"** để chạy workflow với dữ liệu mẫu.
   - Kiểm tra kết quả trong **QuestDB** để đảm bảo bảng và dữ liệu được tạo/chèn thành công.
2. **Bật Active**:
   - Sau khi test thành công, chuyển workflow sang trạng thái **"Active"** để tự động hóa liên tục.

---

### ✍️ Mẹo & Gợi Ý Nâng Cao
1. **Tự Động Chèn Dữ Liệu Từ API/Excel**:
   - Sử dụng **Node HTTP Request** để lấy dữ liệu từ API hoặc **Node Google Sheets** để đọc từ Excel, rồi kết nối với **QuestDB** để chèn tự động.

2. **Gửi Báo Cáo Kết Quả**:
   - Kết hợp với **Node Slack/Telegram** để thông báo khi workflow hoàn thành thành công hoặc gặp lỗi.

3. **Lưu Log Dữ Liệu**:
   - Sử dụng **Node Set** để lưu dữ liệu đầu vào và kết quả vào một bảng khác trong QuestDB để theo dõi lịch sử.

4. **Sử Dụng Cron Job**:
   - Nếu cần chạy định kỳ (ví dụ: hàng ngày), các sếp có thể kết hợp với **Node Cron** để tự động kích hoạt workflow.

---

### 📌 Kết Luận
Workflow này giúp các sếp **tạo bảng và chèn dữ liệu vào QuestDB một cách nhanh chóng, chính xác và tự động hóa hoàn toàn**. Không cần viết code, chỉ cần cấu hình vài bước là có thể tiết kiệm thời gian và giảm thiểu lỗi. **Hãy thử ngay và nâng cao hiệu suất làm việc của team engineering của mình!**

👉 **Bắt đầu tự động hóa ngay hôm nay!** [Tải workflow từ đây](https://n8n.io/workflows/592).