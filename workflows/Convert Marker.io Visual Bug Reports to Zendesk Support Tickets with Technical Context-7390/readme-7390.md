---
title: "🚀 Tự Động Hóa Báo Cáo Lỗi Hình Ảnh Marker.io Sang Zendesk Với Bối Cảnh Kỹ Thuật Chi Tiết"
description: "Giải pháp tự động hóa 100% không code chuyển đổi tất cả báo cáo lỗi từ Marker.io sang Zendesk thành ticket hỗ trợ với đầy đủ thông tin kỹ thuật, giúp đội ngũ kỹ thuật và hỗ trợ làm việc hiệu quả hơn. Tiết kiệm thời gian lên đến 80% trong quá trình xử lý lỗi."
slug: "tieu-dong-hoa-marker-io-sang-zendesk"
tags: [n8n, automation, ticket-management, no-code, zendesk-integration, marker-io]
keywords: [tự động hóa marker io zendesk, chuyển đổi báo cáo lỗi hình ảnh sang ticket, n8n workflow zendesk, tích hợp marker io với zendesk, tự động hóa hỗ trợ kỹ thuật]
---

# 🚀 **Tự Động Hóa Báo Cáo Lỗi Marker.io Sang Zendesk Với Bối Cảnh Kỹ Thuật Chi Tiết**

### **Giải pháp cho đội ngũ kỹ thuật và hỗ trợ tránh mất thời gian chuyển đổi dữ liệu thủ công**
Hiện nay, khi khách hàng hoặc đồng nghiệp báo cáo lỗi trên website thông qua **Marker.io** (công cụ ghi lại lỗi hình ảnh phổ biến), thông tin này thường tồn tại ở dạng riêng biệt, không được tích hợp với hệ thống **Zendesk** của bạn. Điều này khiến:
- Đội ngũ kỹ thuật phải **tìm kiếm thủ công** thông tin lỗi trong Marker.io và chuyển sang Zendesk.
- Đội ngũ hỗ trợ **không có bối cảnh kỹ thuật** để xử lý nhanh chóng.
- **Thời gian phản hồi chậm** do quá trình chuyển đổi dữ liệu tốn nhiều thời gian.

**Workflow này tự động hóa toàn bộ quá trình**, chuyển đổi **mỗi báo cáo lỗi từ Marker.io thành ticket Zendesk** với đầy đủ:
✅ **Thông tin kỹ thuật** (browser, OS, console logs, network logs)
✅ **Hình ảnh và ghi chú** từ Marker.io
✅ **Link trực tiếp** đến báo cáo lỗi
✅ **Danh sách tag tự động** cho quản lý dễ dàng

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng để đảm bảo tính ổn định và bảo mật cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đảm bảo tốc độ cao cho workflow)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian lên đến 80%** trong quá trình chuyển đổi dữ liệu từ Marker.io sang Zendesk.
- **Tăng tốc độ xử lý lỗi** nhờ có **bối cảnh kỹ thuật đầy đủ** trong ticket Zendesk.
- **Giảm sai sót** do tự động hóa thay vì nhập thủ công.
- **Quản lý dễ dàng** với **tag tự động** và **thông tin chi tiết** trong comment nội bộ.
- **Tích hợp hoàn hảo** giữa công cụ ghi lỗi (Marker.io) và hệ thống hỗ trợ (Zendesk).
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản Marker.io** (đã cấu hình **Webhook** cho sự kiện "Issue Created").
✔ **Tài khoản Zendesk** với quyền **API access**.
✔ **Zendesk API Token** (có quyền tạo user, ticket và comment).
✔ **Subdomain Zendesk** (ví dụ: `yourcompany.zendesk.com`).
✔ **N8n self-hosted** (khuyến nghị để tránh giới hạn free tier).

---
### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/7390](https://n8n.io/workflows/7390) hoặc sao chép mã JSON từ trang này.
- Mở **n8n Editor** → Nhấn **"Import"** → Dán mã JSON và nhấn **"Import"**.
- Workflow sẽ tự động xuất hiện với **5 node** chính.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này bao gồm **5 node chính**, các sếp cần cấu hình kỹ lưỡng như sau:

##### **🔹 Node 1: Webhook (Nhận dữ liệu từ Marker.io)**
- **Tên node:** `Webhook`
- **Cấu hình:**
  - **Path:** `a1bfef52-25c9-4a7d-916f-87c0ca195305` (không thay đổi).
  - **HTTP Method:** `POST` (không thay đổi).
  - **Sau khi lưu**, copy **URL Webhook** (ví dụ: `https://your-n8n-server/webhook/a1bfef52-25c9-4a7d-916f-87c0ca195305`).
  - **Đăng ký Webhook trên Marker.io:**
    - Mở **Workspace Settings → Webhooks → Create Webhook**.
    - Nhập URL Webhook vừa copy.
    - Chọn **Event:** `Issue Created`.
    - Lưu và kích hoạt.

##### **🔹 Node 2: Format Marker.io Data (Xử lý dữ liệu đầu vào)**
- **Tên node:** `Format Marker.io Data` (là node **Code**).
- **Lưu ý:**
  - Node này **không cần chỉnh sửa** nếu các sếp đã import workflow chính xác từ file JSON.
  - Nếu cần **tùy chỉnh**, các sếp có thể mở node này và chỉnh sửa logic **JavaScript** để extra dữ liệu từ payload Marker.io.

##### **🔹 Node 3: Create/Update User (Tạo/Update người dùng Zendesk)**
- **Tên node:** `Create/Update User`
- **Cấu hình:**
  - **Method:** `POST` (tạo mới) hoặc `PUT` (cập nhật).
  - **URL:** `https://[REPLACE_SUBDOMAIN].zendesk.com/api/v2/users.json`
  - **Headers:**
    - `Content-Type: application/json`
    - `Authorization: Bearer [ZENDESK_API_TOKEN]`
  - **Body (JSON):**
    ```json
    {
      "user": {
        "name": "{{ $node["Webhook"].json["reporter"]["name"] }}",
        "email": "{{ $node["Webhook"].json["reporter"]["email"] }}",
        "tags": ["marker-io-reporter"]
      }
    }
    ```
  - **Lưu ý:**
    - Thay thế `[REPLACE_SUBDOMAIN]` bằng subdomain Zendesk của bạn.
    - Đảm bảo **Zendesk API Token** có quyền **create/update users**.

##### **🔹 Node 4: Create Ticket (Tạo ticket Zendesk)**
- **Tên node:** `Create Ticket`
- **Cấu hình:**
  - **Method:** `POST`
  - **URL:** `https://[REPLACE_SUBDOMAIN].zendesk.com/api/v2/tickets.json`
  - **Headers:**
    - `Content-Type: application/json`
    - `Authorization: Bearer [ZENDESK_API_TOKEN]`
  - **Body (JSON):**
    ```json
    {
      "ticket": {
        "subject": "{{ $node["Format Marker.io Data"].json["title"] }}",
        "comment": {
          "body": "{{ $node["Format Marker.io Data"].json["description"] }}",
          "public": false
        },
        "requester_id": "{{ $node["Create/Update User"].json["id"] }}",
        "tags": ["marker-io-bug", "needs-triage"]
      }
    }
    ```
  - **Lưu ý:**
    - **Thay thế `requester_id`** bằng ID người dùng từ node `Create/Update User`.
    - **Thêm tag tự động** (`marker-io-bug`, `needs-triage`) để quản lý dễ dàng.

##### **🔹 Node 5: Add Internal Comment (Thêm comment nội bộ)**
- **Tên node:** `Add Internal Comment`
- **Cấu hình:**
  - **Method:** `POST`
  - **URL:** `https://[REPLACE_SUBDOMAIN].zendesk.com/api/v2/tickets/{{ $node["Create Ticket"].json["id"] }}/comments.json`
  - **Headers:**
    - `Content-Type: application/json`
    - `Authorization: Bearer [ZENDESK_API_TOKEN]`
  - **Body (JSON):**
    ```json
    {
      "comment": {
        "body": "**Marker.io Issue Details:**\n\n- **Marker ID:** {{ $node["Format Marker.io Data"].json["marker_id"] }}\n- **Priority:** {{ $node["Format Marker.io Data"].json["priority"] }}\n- **Browser:** {{ $node["Format Marker.io Data"].json["browser"] }}\n- **OS:** {{ $node["Format Marker.io Data"].json["os"] }}\n- **URL:** {{ $node["Format Marker.io Data"].json["url"] }}\n\n**Technical Context:**\n{{ $node["Format Marker.io Data"].json["technical_context"] }}\n\n**Marker.io Issue Link:** [View on Marker.io]({{ $node["Format Marker.io Data"].json["marker_url"] }})",
        "public": false
      }
    }
    ```
  - **Lưu ý:**
    - **Thay thế `ticket_id`** bằng ID ticket từ node `Create Ticket`.
    - **Thêm thông tin kỹ thuật chi tiết** (browser, OS, console logs, network logs) vào comment nội bộ.

---

#### **3. Kích hoạt ⚡️**
- **Test run dữ liệu mẫu:**
  - Tạo **một báo cáo lỗi mẫu** trên Marker.io.
  - Kiểm tra **Zendesk** xem ticket có xuất hiện không.
  - Đảm bảo **comment nội bộ** chứa đầy đủ thông tin kỹ thuật.
- **Bật Active workflow:**
  - Nhấn **"Active"** trên workflow để kích hoạt tự động hóa.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tích hợp Slack/Telegram thông báo:**
   - Sử dụng **node Slack/Telegram** để gửi thông báo khi có ticket mới.
   - Ví dụ: `Ticket mới từ Marker.io: #{{ $node["Create Ticket"].json["subject"] }} (ID: {{ $node["Create Ticket"].json["id"] }})`.

2. **Lưu log hoạt động:**
   - Sử dụng **node StickyNote** hoặc **Google Sheets** để ghi lại lịch sử hoạt động của workflow.
   - Ví dụ: Lưu **Marker ID**, **Zendesk Ticket ID**, **Thời gian xử lý**.

3. **Gửi báo cáo định kỳ:**
   - Sử dụng **node Schedule** (n8n Pro) để gửi **báo cáo tổng hợp** về số lượng ticket mới, lỗi phổ biến hàng tuần.

4. **Tùy chỉnh tag và priority:**
   - Thay đổi **tag tự động** (`marker-io-bug`, `needs-triage`) phù hợp với quy trình của công ty.
   - Cập nhật **priority mapping** (ví dụ: `High` → `urgent`, `Low` → `standard`).

5. **Xử lý lỗi tự động:**
   - Sử dụng **node Set** để kiểm tra lỗi và gửi **thông báo Slack** khi workflow gặp vấn đề.

---

### 📌 **Kết luận**
Workflow này **giải phóng đội ngũ kỹ thuật và hỗ trợ** khỏi công việc **nhập liệu thủ công**, đồng thời **tăng cường bối cảnh kỹ thuật** trong Zendesk. **Kết quả:**
✅ **Tiết kiệm thời gian** lên đến **80%**.
✅ **Tăng tốc độ xử lý lỗi** nhờ thông tin đầy đủ.
✅ **Giảm sai sót** do tự động hóa.
✅ **Quản lý dễ dàng** với tag tự động.

**Hãy áp dụng ngay workflow này và nâng cao hiệu quả làm việc của đội ngũ!** 🚀

---
**🔗 [Tải workflow nguyên bản](https://n8n.io/workflows/7390)**
**💬 Cần hỗ trợ? Hãy để lại bình luận bên dưới!**