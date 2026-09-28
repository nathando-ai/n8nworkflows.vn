---
title: "🔄 [Tự Động Hóa: Thay Đổi Tên Khóa (Key) Trong Dữ Liệu Như Chuyên Gia - Không Cần Code!]"
description: "Workflow này giúp các sếp tự động thay đổi tên các khóa (key) trong dữ liệu JSON hoặc object một cách nhanh chóng và chính xác, tiết kiệm thời gian xử lý thủ công. Đặc biệt phù hợp cho việc chuẩn hóa dữ liệu trước khi gửi đến API hoặc hệ thống khác."
slug: "tam-dong-hoa-thay-doi-ten-khoa-key-trong-du-lieu"
tags: [n8n, automation, no-code, data-transformation, json-processing, building-blocks]
keywords: [n8n rename keys, tự động hóa thay đổi tên khóa, xử lý dữ liệu JSON, chuyển đổi dữ liệu không code, n8n workflow cơ bản, tự động hóa dữ liệu]
---

# 🔄 **Tự Động Hóa Thay Đổi Tên Khóa (Key) Trong Dữ Liệu - Không Cần Code!**

### **Nỗi Đau Của Các Sếp Khi Xử Lý Dữ Liệu**
Các sếp đã từng gặp phải tình huống này chưa?
- **Dữ liệu từ API này** có khóa `user_name`, nhưng hệ thống khác yêu cầu `username`.
- **File JSON** từ bên ngoài có khóa `full_address`, nhưng cần chuyển thành `address_full` để phù hợp với quy trình nội bộ.
- **Dữ liệu thủ công nhập** có tên khóa không thống nhất, khiến việc tích hợp hệ thống trở nên phức tạp và tốn thời gian.

**Workflow này giải quyết tất cả!** Với chỉ **3 node đơn giản**, các sếp có thể **tự động hóa việc thay đổi tên khóa** trong dữ liệu một cách nhanh chóng, chính xác và không cần viết một dòng code nào.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần xử lý thủ công hàng trăm hàng nghìn dòng dữ liệu.
- **Chính xác 100%**: Tránh sai sót do nhập liệu hoặc thay đổi tên khóa sai.
- **Chuẩn hóa dữ liệu**: Đảm bảo dữ liệu phù hợp với yêu cầu của API hoặc hệ thống tiếp nhận.
- **Hoạt động liên tục**: Thực hiện tự động khi cần, không phụ thuộc vào thời gian làm việc của nhân viên.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow này hoạt động, các sếp chỉ cần:
- **Dữ liệu đầu vào** (có thể là JSON, object, hoặc dữ liệu từ node khác trong workflow).
- **Danh sách khóa cần thay đổi** (ví dụ: `user_name` → `username`, `full_address` → `address_full`).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow này bằng cách:
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/582) và import vào **n8n Editor**.
- **Copy/paste** JSON từ link trên vào **n8n Editor** và nhấn **Create Workflow**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này bao gồm **3 node chính**, các sếp cần chú ý đến:

##### **Node 1: Manual Trigger (On clicking 'execute')**
- **Chức năng**: Khởi động workflow thủ công khi cần.
- **Lưu ý**: Nếu muốn tự động hóa hoàn toàn, các sếp có thể thay thế bằng **node Webhook** hoặc **node Schedule** để kích hoạt theo lịch hoặc từ API bên ngoài.

##### **Node 2: Set (Set)**
- **Chức năng**: Cung cấp dữ liệu đầu vào cho node **Rename Keys**.
- **Lưu ý**:
  - **Điền dữ liệu mẫu** vào `json` hoặc `data` (ví dụ:
    ```json
    {
      "user_name": "John Doe",
      "full_address": "123 Street, City"
    }
    ```
  - Nếu dữ liệu đến từ **node khác** (ví dụ: từ API, file CSV), các sếp chỉ cần **kết nối node đó** vào node **Set** thay vì điền thủ công.

##### **Node 3: Rename Keys (Rename Keys)**
- **Chức năng**: Thay đổi tên khóa trong dữ liệu.
- **Lưu ý BẮT BUỘC**:
  - Trong trường `renameKeys`, các sếp **cần điền danh sách các cặp khóa cũ và khóa mới** dưới dạng JSON, ví dụ:
    ```json
    [
      {
        "from": "user_name",
        "to": "username"
      },
      {
        "from": "full_address",
        "to": "address_full"
      }
    ]
    ```
  - **Kiểm tra lại tên khóa** để tránh lỗi do nhập sai.

#### **3. Kích Hoạt ⚡️**
- **Test Run**: Nhấn **Execute** để kiểm tra kết quả. Dữ liệu đầu vào sẽ được chuyển đổi theo quy tắc đã thiết lập.
- **Bật Active**: Sau khi kiểm tra thành công, các sếp có thể **bật workflow** để hoạt động liên tục.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁCH DÙNG HIỆU QUẢ HƠN]
- **Kết hợp với API**: Sử dụng node **HTTP Request** để lấy dữ liệu từ API, sau đó **Set** và **Rename Keys** trước khi gửi đến hệ thống tiếp nhận.
- **Lưu log**: Thêm node **Slack** hoặc **Email** để nhận thông báo khi workflow hoàn thành hoặc gặp lỗi.
- **Tự động hóa định kỳ**: Thay thế **Manual Trigger** bằng **Schedule** để chạy workflow hàng ngày/lần tuần.
- **Chuyển đổi nhiều khóa cùng lúc**: Nếu dữ liệu có nhiều khóa cần thay đổi, các sếp có thể **tạo một danh sách lớn** trong node **Set** và áp dụng cùng một quy tắc.
:::

---

### 📌 **Kết Luận**
Workflow này là **công cụ mạnh mẽ** để các sếp **tự động hóa việc thay đổi tên khóa** trong dữ liệu một cách đơn giản và hiệu quả. Không cần viết code, không cần là chuyên gia kỹ thuật, các sếp chỉ cần **cấu hình vài bước** là có thể **chuẩn hóa dữ liệu** cho phù hợp với yêu cầu của hệ thống.

**Hãy thử ngay và tiết kiệm thời gian cho đội ngũ của mình!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::