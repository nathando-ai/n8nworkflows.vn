---
title: "🚀 Tự Động Tạo Khách Hàng & Gắn Nhóm (Segment) Trên Customer.io MỚI CHỈ VỚI 1 CLICK"
description: "Workflow này giúp các sếp tự động tạo khách hàng mới và gán họ vào nhóm (segment) trên Customer.io chỉ bằng 1 nút bấm, tiết kiệm thời gian và giảm thiểu lỗi thủ công. Phù hợp cho các doanh nghiệp bán hàng, marketing cần quản lý khách hàng hiệu quả."
slug: "tu-dong-tao-khach-hang-va-segment-tren-customerio"
tags: [n8n, automation, customerio, marketing, sales, no-code]
keywords: [n8n workflow customerio, tự động hóa marketing, tạo khách hàng tự động, segment khách hàng, n8n tự động hóa bán hàng]
---

# 🚀 **Tự Động Tạo Khách Hàng & Gắn Nhóm (Segment) Trên Customer.io – Không Cần Code!**

### **Nỗi Đau Của Các Sếp Khi Làm Thủ Công**
Hàng ngày, các sếp phải:
- **Nhập liệu khách hàng mới** vào hệ thống Customer.io một cách thủ công → **Tốn thời gian** và dễ **lỗi nhầm**.
- **Gán khách hàng vào nhóm (segment)** theo tiêu chí (ví dụ: khách hàng mới, khách hàng VIP) → **Khó theo dõi** và **không tự động hóa**.
- **Phải nhớ các bước phức tạp** để tạo khách hàng và cập nhật segment → **Giảm hiệu suất** và **tăng stress**.

**Workflow này giải quyết tất cả!** Chỉ với **1 nút bấm**, các sếp có thể:
✅ **Tạo khách hàng mới** trên Customer.io một cách **tự động và chính xác**.
✅ **Gắn khách hàng vào nhóm (segment)** theo yêu cầu (ví dụ: "Khách hàng mới", "Khách hàng VIP").
✅ **Tiết kiệm thời gian** lên đến **30 phút/ngày** cho đội ngũ marketing & sales.
✅ **Giảm thiểu lỗi** do nhập liệu sai hoặc quên gán segment.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này **chạy 24/7** mà không bị gián đoạn, các sếp nên **self-host n8n** trên **VPS riêng** thay vì dùng phiên bản miễn phí (n8n.cloud).
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** – giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (Đảm bảo tốc độ cao, ổn định)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
| **Lợi Ích** | **Chi Tiết** |
|-------------|-------------|
| **Tiết kiệm thời gian** | Không cần nhập liệu thủ công, chỉ **1 click** là xong. |
| **Chính xác 100%** | Không lo nhầm tên, email hoặc segment. |
| **Tự động hóa hoàn toàn** | Workflow chạy **mỗi khi cần**, không phụ thuộc vào người dùng. |
| **Dễ dàng mở rộng** | Có thể kết nối với **Slack, Email, CRM khác** sau này. |

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi **lên đồ**, các sếp cần chuẩn bị:
✔ **Tài khoản Customer.io** (đã có **API Key**).
✔ **Credentials `customerIoApi`** trong n8n (cấu hình trong **Credentials Manager**).
✔ **Dữ liệu mẫu** (tên khách hàng, email, segment muốn gán).

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/646](https://n8n.io/workflows/646) hoặc copy **JSON dưới đây** vào **n8n Editor**.
- **Cách import**:
  1. Mở **n8n Editor** → **Import Workflow** → **Paste JSON**.
  2. **Active workflow** sau khi import xong.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **3 node chính**, các sếp cần **cấu hình kỹ lưỡng**:

##### **Node 1: `On clicking 'execute'` (Manual Trigger)**
- **Chức năng**: Khởi động workflow khi **bấm nút "Execute"**.
- **Lưu ý**:
  - **Không cần chỉnh sửa gì** nếu chỉ muốn **bấm tay** để chạy.
  - Nếu muốn **tự động hóa**, có thể kết nối với **Webhook** hoặc **Schedule Trigger**.

##### **Node 2 & 3: `CustomerIo` (Tạo Khách Hàng & Gán Segment)**
- **Node `CustomerIo` (Tạo khách hàng mới)**
  - **Credentials**: Chọn `customerIoApi` (đã cấu hình trước).
  - **Parameters cần điền**:
    - `email`: Email của khách hàng (ví dụ: `user@example.com`).
    - `name`: Tên khách hàng (ví dụ: `Nguyễn Văn A`).
    - `properties`: Thông tin thêm (nếu có, ví dụ: `{"phone": "0123456789"}`).

- **Node `CustomerIo1` (Gán Segment)**
  - **Credentials**: Chọn `customerIoApi` (giống node trước).
  - **Parameters cần điền**:
    - `resource`: **`segment`** (đã được set trong workflow).
    - `email`: **Email của khách hàng** (phải trùng với node tạo khách hàng).
    - `segment`: **Tên segment** muốn gán (ví dụ: `new_customers`, `vip_clients`).

⚠️ **Lưu ý quan trọng**:
- **Email phải trùng khớp** giữa node tạo khách hàng và node gán segment.
- **Segment phải tồn tại** trên Customer.io trước khi gán.

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Điền **email**, **name**, và **segment** vào node.
   - **Run workflow** để kiểm tra.
2. **Active workflow** khi đã kiểm tra thành công.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết nối với Slack/Telegram**
   - Sau khi tạo khách hàng thành công, **gửi thông báo** lên Slack/Telegram bằng **node `slack`** hoặc **`telegram`**.
   - **Cách làm**:
     ```json
     {
       "node": "slack",
       "type": "slack",
       "credentials": "slackApi",
       "parameters": {
         "text": "🎉 Khách hàng mới đã được tạo và gán vào segment: {{ $node["CustomerIo1"].json["segment"] }}"
       }
     }
     ```

2. **Lưu Log vào Google Sheets**
   - Dùng **node `googleSheets`** để **ghi lại lịch sử** tạo khách hàng và segment.
   - **Cách làm**:
     ```json
     {
       "node": "googleSheets",
       "type": "googleSheets",
       "credentials": "googleSheetsApi",
       "parameters": {
         "sheetName": "Customer_Log",
         "row": {
           "Email": "{{ $node["CustomerIo"].json["email"] }}",
           "Name": "{{ $node["CustomerIo"].json["name"] }}",
           "Segment": "{{ $node["CustomerIo1"].json["segment"] }}",
           "Time": "{{ $node["CustomerIo"].date }}"
         }
       }
     }
     ```

3. **Tự động hóa định kỳ**
   - Thay vì **bấm tay**, dùng **node `scheduleTrigger`** để chạy workflow **mỗi ngày/lần** (ví dụ: **lấy danh sách khách hàng mới từ CRM** và gán segment tự động).

---
### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc **nhập liệu thủ công** và **gán segment** trên Customer.io. **Chỉ với 1 click**, khách hàng mới được tạo và phân loại chính xác vào nhóm phù hợp.

**Hãy áp dụng ngay!**
👉 **Tải workflow** từ [n8n.io/workflows/646](https://n8n.io/workflows/646) và **cấu hình** theo hướng dẫn trên.
👉 **Nếu cần hỗ trợ**, để lại comment bên dưới hoặc **chat với chúng tôi** trên [Facebook Group n8n Việt Nam](https://www.facebook.com/groups/n8nvietnam).

**🚀 Hành động ngay – Tự động hóa hôm nay, tiết kiệm thời gian mai!**