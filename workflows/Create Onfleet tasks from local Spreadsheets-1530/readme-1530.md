---
title: "🚀 Tự Động Tạo Nhiệm Vụ Onfleet Từ File Excel/Local Tự Động - Khắc Phục Vấn Đề Quản Lý Đơn Hàng Chậm Chạp"
description: "Workflow này tự động chuyển đổi dữ liệu từ file Excel/Local thành nhiệm vụ trên Onfleet, giúp các sếp tiết kiệm thời gian lên tới 80% trong quản lý đơn hàng và phân công nhân viên. Hỗ trợ hoạt động 24/7 mà không cần code."
slug: "tu-dong-tao-nhiem-vu-onfleet-tu-file-excel"
tags: [n8n, automation, onfleet, spreadsheet, no-code, sales-automation]
keywords: [tự động hóa onfleet, chuyển file excel sang onfleet, quản lý đơn hàng tự động, n8n workflow onfleet, tự động hóa logistics]
---

# 🚀 **Tự Động Tạo Nhiệm Vụ Onfleet Từ File Excel/Local - Giải Pháp Cho Doanh Nghiệp Logistics & Sales**

### **Nỗi Đau Của Các Sếp Trong Quản Lý Đơn Hàng**
Hàng ngày, các sếp phải:
- **Nhập liệu thủ công** từ file Excel vào Onfleet, tốn thời gian và dễ sai sót.
- **Phân công nhân viên** dựa trên vị trí, loại hàng, hoặc ưu tiên, nhưng lại phải làm lại mỗi khi có thay đổi.
- **Không thể tự động hóa** vì không biết cách kết nối file local với Onfleet mà không cần code.

**Workflow này giải quyết tất cả!** Chỉ cần **1 file Excel/Local**, hệ thống sẽ tự động tạo nhiệm vụ trên Onfleet, phân công cho nhân viên, và cập nhật trạng thái theo thời gian thực.

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần nhập liệu thủ công, giảm thiểu sai sót lên tới **80%**.
- **Chính xác & tự động hóa**: Dữ liệu từ Excel được chuyển sang Onfleet **một cách chính xác**, không cần can thiệp.
- **Hoạt động 24/7**: Workflow chạy liên tục, ngay cả khi các sếp nghỉ ngơi.
- **Cá nhân hóa phân công**: Dựa trên cột "Nhân Viên" trong Excel, nhiệm vụ sẽ tự động gán cho người phù hợp.
- **Kết nối dễ dàng**: Hỗ trợ file Excel/Local, không cần API phức tạp.
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần:
1. **Tài khoản Onfleet** và **API Key** của Onfleet (đăng ký tại [Onfleet](https://www.onfleet.com/)).
2. **File Excel/Local** chứa dữ liệu nhiệm vụ (cấu trúc mẫu sẽ được hướng dẫn dưới đây).
3. **n8n Self-hosted** (không dùng phiên bản miễn phí vì cần đọc file local).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
### 📄 **Cấu Trúc File Excel Cần Thiết**
File Excel phải có **các cột sau** (định dạng mẫu):
| **Cột**          | **Mô Tả**                          | **Ví Dụ**                     |
|-------------------|-------------------------------------|-------------------------------|
| `Title`           | Tiêu đề nhiệm vụ                   | "Giao hàng cho khách ABC"     |
| `Description`     | Mô tả chi tiết                      | "Hàng: 100 sản phẩm, địa chỉ: 123 Đường ABC" |
| `Location`        | Địa chỉ giao hàng                  | "123 Đường ABC, Quận 1, TP.HCM" |
| `Driver`          | Nhân viên phân công                | "Nguyễn Văn A"                |
| `Status`          | Trạng thái mặc định (nếu có)       | "Chưa bắt đầu"                |

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/1530) hoặc copy toàn bộ JSON dưới đây vào **n8n Editor**:
  ```json
  {
    "nodes": [
      {
        "parameters": {
          "operation": "create"
        },
        "name": "Onfleet",
        "type": "onfleet",
        "credentials": {
          "onfleetApi": ""
        }
      },
      {
        "name": "Read Binary File",
        "type": "readBinaryFile"
      },
      {
        "name": "Spreadsheet File1",
        "type": "spreadsheetFile"
      }
    ],
    "connections": {
      "Spreadsheet File1": {
        "main": [
          [
            {
              "annotation": "Read Binary File"
            },
            "Read Binary File"
          ]
        ]
      },
      "Read Binary File": {
        "main": [
          [
            {
              "annotation": "Onfleet"
            },
            "Onfleet"
          ]
        ]
      }
    }
  }
  ```
- **Chọn "Import"** và chọn file JSON đã tải.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
##### **a) Node "Spreadsheet File1" (Đọc File Excel)**
- **Thiết lập Credentials**:
  - Chọn **"Local File"** (do file nằm trên máy chủ VPS).
  - **Đường dẫn file**: Điền đường dẫn **tương đối** hoặc **tương đối từ thư mục n8n** (ví dụ: `./data/tasks.xlsx`).
  - **Sheet Name**: Điền tên sheet trong file Excel (ví dụ: `Sheet1`).

##### **b) Node "Read Binary File" (Nếu cần đọc file từ máy chủ)**
- **Nếu file nằm trên VPS**:
  - Chọn **"Binary File"** và điền **đường dẫn file** (ví dụ: `/home/user/n8n/data/tasks.xlsx`).
  - **Thiết lập "File Path"** và **"File Name"** chính xác.

##### **c) Node "Onfleet" (Tạo Nhiệm Vụ)**
- **Thiết lập Credentials**:
  - Chọn **"onfleetApi"** (đã cấu hình trước khi import).
  - **API Key**: Điền **API Key** từ Onfleet (tìm trong **Settings > API Keys**).
- **Mappings (BẮT BUỘC ĐIỀN ĐÚNG)**:
  - **`Title`** → `$json["Title"]` (hoặc tên cột trong file Excel).
  - **`Description`** → `$json["Description"]`.
  - **`Location`** → `$json["Location"]`.
  - **`Driver`** → `$json["Driver"]` (để Onfleet biết phân công cho ai).
  - **`Status`** (nếu có) → `$json["Status"]`.

---
#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Chọn **"Test"** trên node **Onfleet** để kiểm tra dữ liệu đầu vào.
   - Nếu thành công, sẽ xuất hiện **ID nhiệm vụ** trên Onfleet.
2. **Bật Active**:
   - Chuyển **Active** thành **"ON"** để workflow chạy tự động.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁCH LÀM NGOÀI]
- **Gửi thông báo Slack/Telegram khi nhiệm vụ được tạo**:
  - Thêm node **Slack** hoặc **Telegram Bot** sau node **Onfleet**.
  - Cấu hình **webhook** và gửi tin nhắn tự động khi có nhiệm vụ mới.
- **Lưu log hoạt động**:
  - Thêm node **Google Sheets** hoặc **Airtable** để ghi lại lịch sử nhiệm vụ.
- **Chạy định kỳ**:
  - Sử dụng **Trigger: Schedule** để chạy workflow hàng ngày/lần một tuần.
- **Tích hợp với Google Sheets**:
  - Thay vì file local, đọc trực tiếp từ **Google Sheets** bằng node **Google Sheets**.
:::

---
### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc nhập liệu thủ công, đồng thời **tăng cường hiệu quả quản lý đơn hàng** với Onfleet. **Chỉ cần 1 file Excel**, hệ thống sẽ tự động tạo và phân công nhiệm vụ, giúp doanh nghiệp **hoạt động mượt mà hơn**.

**🚀 Hãy áp dụng ngay và trải nghiệm sự tự động hóa hoàn toàn!**
Nếu có vấn đề, các sếp có thể **comment dưới bài viết** hoặc liên hệ với **James Li** (tác giả) qua [n8n Community](https://community.n8n.io/).

---
**🎁 Bonus**: Các sếp có thể kết hợp với workflow **Auto Update Onfleet Status** để tự động cập nhật trạng thái nhiệm vụ khi nhân viên hoàn thành. 🚚💨