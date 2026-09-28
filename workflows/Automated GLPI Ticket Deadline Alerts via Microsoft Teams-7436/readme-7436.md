---
title: "🚀 **Tự Động Cảnh Báo Hạn Chấm Dứt Ticket GLPI Trên Microsoft Teams - Giảm Thiểu Rủi Ro & Tăng Cường Trách Nhiệm**"
description: "Workflow tự động hóa cảnh báo hạn chấm dứt ticket GLPI qua Microsoft Teams, giúp các sếp quản lý hỗ trợ kỹ thuật hiệu quả hơn với thông báo tự động 5 ngày trước hạn, phân công trách nhiệm rõ ràng cho từng kỹ thuật viên. Giảm thiểu rủi ro ticket quá hạn và cải thiện trải nghiệm khách hàng."
slug: "tieu-dong-canh-bao-han-cham-dut-ticket-glpi-tren-microsoft-teams"
tags: [n8n, automation, ticket-management, glpi, microsoft-teams, no-code, workflow-tự-động-hoá]
keywords: [n8n workflow glpi, tự động hóa ticket quản lý, cảnh báo hạn chấm dứt ticket, Microsoft Teams integration, tự động hóa hỗ trợ kỹ thuật, giảm thiểu ticket quá hạn]
---

# 🚀 **Tự Động Cảnh Báo Hạn Chấm Dứt Ticket GLPI Trên Microsoft Teams**

Hãy tưởng tượng một tình huống: **Một ticket hỗ trợ kỹ thuật của khách hàng đang ở trạng thái "chờ xử lý" nhưng đã sắp hết hạn (5 ngày).** Nếu không có cảnh báo kịp thời, ticket sẽ tự động chuyển sang trạng thái "quá hạn", gây mất niềm tin cho khách hàng và làm tăng tải công việc cho đội ngũ kỹ thuật. **Workflow này giải quyết vấn đề này 100% tự động hóa, không cần code!**

Thay vì phải kiểm tra thủ công hàng ngày trên GLPI và gửi thông báo qua Teams, **các sếp chỉ cần cấu hình 1 lần và workflow sẽ tự động:**
✅ **Lấy danh sách ticket sắp hết hạn** (5 ngày trước hạn) từ GLPI.
✅ **Phân công cảnh báo cho kỹ thuật viên phù hợp** (theo ID người dùng trong GLPI).
✅ **Gửi thông báo tự động qua Microsoft Teams** với chi tiết ticket (ID, tiêu đề, hạn chấm dứt).
✅ **Hoạt động 24/7, không cần can thiệp thủ công.**

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm thời gian:** Không cần kiểm tra thủ công hàng ngày trên GLPI.
- **Trách nhiệm rõ ràng:** Mỗi kỹ thuật viên nhận được ticket tương ứng, giảm nhầm lẫn.
- **Cải thiện chất lượng dịch vụ:** Khách hàng không bị bỏ rơi do ticket quá hạn.
- **Dữ liệu chính xác:** Thông báo tự động dựa trên logic thời gian (5 ngày trước hạn).
- **Hoạt động liên tục:** Workflow chạy tự động mỗi ngày, không phụ thuộc vào giờ làm việc.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[**CHUẨN BỊ**]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản GLPI với quyền quản trị ứng dụng (Application Administrator):**
   - URL của server GLPI (ví dụ: `https://your_glpi_server.com`).
   - **App Token** (tạo tại **Administration > Applications > Tokens** trong GLPI).
   - **ID của các kỹ thuật viên** (xem hướng dẫn dưới đây).

2. **Tài khoản Microsoft Teams OAuth2:**
   - Cấu hình OAuth2 cho Microsoft Teams trong n8n (node `microsoftTeams`).
   - **Chat hoặc nhóm Teams** để gửi thông báo (cần quyền gửi tin nhắn).

3. **n8n Self-hosted (không dùng phiên bản miễn phí):**
   - Workflow này **không thể chạy trên phiên bản n8n Cloud** do sử dụng **Schedule Trigger** và **HTTP Request** liên tục.
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/7436) hoặc copy toàn bộ JSON dưới đây vào **n8n Editor**.
- **Cách import:**
  1. Mở n8n Editor → Nhấn **Import Workflow** (icon "↗️").
  2. Chọn file JSON hoặc **paste** toàn bộ mã JSON vào ô `Paste JSON`.
  3. Nhấn **Import**.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
#### **A. Cấu hình "Configuration Variables" (Biến cấu hình)**
- Mở node **"Configuration Variables"** (type: `set`).
- **Cập nhật URL và Token GLPI:**
  ```json
  {
    "glpi_url": "https://your_glpi_server.com",
    "app_token": "Your_App_Token_Here"
  }
  ```
  - **Lấy App Token GLPI:**
    1. Đăng nhập GLPI → **Administration > Applications > Tokens**.
    2. Tạo một token mới và sao chép giá trị.

#### **B. Cập nhật ID của kỹ thuật viên**
- **Lấy ID kỹ thuật viên từ GLPI:**
  1. Đăng nhập GLPI → **Administration > Users**.
  2. Chọn một kỹ thuật viên → **ID sẽ xuất hiện trong URL** (ví dụ: `id=7`).
  3. **Ghi lại ID** cho:
     - **Support Technician 1?** → ID của kỹ thuật viên 1 (ví dụ: `7`).
     - **Support Technician 2?** → ID của kỹ thuật viên 2 (ví dụ: `8`).

- **Cấu hình node `if` (điều kiện):**
  - Mở node **"Support Technician 1?"** → Trong **Expression**, thay thế:
    ```json
    {{ $json["id"] == 7 }}
    ```
    (Thay `7` bằng ID thực tế của kỹ thuật viên 1).
  - Lặp lại cho node **"Support Technician 2?"** với ID tương ứng.

#### **C. Cấu hình Microsoft Teams**
- Mở node **"Send a message to Support Technician 1"** và **"Send a message to Support Technician 2"**.
- **Chọn credentials:** `microsoftTeamsOAuth2Api`.
- **Cấu hình tin nhắn:**
  - **Message content:** Sử dụng template mặc định (có thể tùy chỉnh thêm chi tiết ticket).
  - **Chat/Group:** Chọn **Chat 1:1** với kỹ thuật viên hoặc **Group Channel** chung.

#### **D. Cấu hình "Tickets about to expire" (Lọc ticket sắp hết hạn)**
- Node này sử dụng **Expression** để lọc ticket có hạn chấm dứt trong **5 ngày**.
- **Không cần chỉnh sửa** nếu muốn giữ logic mặc định (5 ngày).
- **Nếu muốn thay đổi ngày cảnh báo:**
  - Mở node **"Tickets about to expire"** → **Expression**:
    ```json
    {{new Date(Date.now() + (X * 24 * 60 * 60 * 1000)).toISOString().split('T')[0]}}
    ```
    (Thay `X` bằng số ngày muốn cảnh báo trước hạn, ví dụ `3` để cảnh báo 3 ngày trước).

#### **E. Kích hoạt Schedule Trigger**
- Node **"Schedule Trigger"** sẽ chạy workflow **hàng ngày** (mặc định là 00:00 UTC).
- **Không cần chỉnh sửa** nếu muốn chạy vào giờ mặc định.
- **Nếu muốn chạy vào giờ khác:**
  - Mở node → **Schedule** → Chọn **Custom** và nhập giờ mong muốn (ví dụ: `09:00` giờ Việt Nam).

---
### **3. Kích hoạt ⚡️ Workflow**
1. **Test Run (kiểm tra thử):**
   - Nhấn **Run Workflow** để kiểm tra logic.
   - Kiểm tra **Microsoft Teams** xem có nhận được tin nhắn mẫu không.
2. **Bật Active:**
   - Sau khi kiểm tra thành công, nhấn **Active** để workflow chạy tự động hàng ngày.

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::info[**TẠO TRẢI NGHIỆM TỐT HƠN**]
1. **Thêm thông tin chi tiết ticket vào tin nhắn Teams:**
   - Mở node `microsoftTeams` → **Message content** → Sử dụng template:
     ```json
     {
       "text": "🚨 **Ticket sắp hết hạn!** 🚨\n\n" +
       "- **ID Ticket:** {{ $json["id"] }}\n" +
       "- **Tiêu đề:** {{ $json["title"] }}\n" +
       "- **Hạn chấm dứt:** {{ $json["deadline"] }}\n" +
       "- **Trạng thái:** {{ $json["status"] }}\n" +
       "- **Người tạo:** {{ $json["user_name"] }}\n\n" +
       "🔗 **Xem chi tiết:** [{{ $json["url"] }}]({{ $json["url"] }})"
     }
     ```
2. **Gửi báo cáo định kỳ cho quản lý:**
   - Thêm node `microsoftTeams` mới để gửi **báo cáo tổng hợp** (ví dụ: số ticket cảnh báo mỗi ngày).
3. **Lưu log vào Google Sheets/Notion:**
   - Thêm node `httpRequest` hoặc `googleSheets` để ghi lại lịch sử cảnh báo.
4. **Kết hợp với Slack (nếu không dùng Teams):**
   - Thay thế node `microsoftTeams` bằng `slackWebhook` và cấu hình Webhook Slack.
5. **Cảnh báo qua email:**
   - Thêm node `email` (ví dụ: `n8n-nodes-base.email`) để gửi email cảnh báo cho kỹ thuật viên.
:::

---
## 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp và kỹ thuật viên khỏi việc kiểm tra thủ công ticket GLPI, đồng thời **cải thiện trách nhiệm và chất lượng dịch vụ** bằng cách cảnh báo kịp thời. **Chỉ cần cấu hình 1 lần và workflow sẽ tự động hoạt động hàng ngày!**

👉 **Bắt đầu tự động hóa ngay hôm nay!**
1. **Cài đặt n8n Self-hosted** (nếu chưa có).
2. **Import workflow** và **cấu hình theo hướng dẫn**.
3. **Bật Active** và **quên đi việc kiểm tra thủ công!**

**Nếu có vấn đề, hãy để lại comment bên dưới hoặc liên hệ với tôi qua [tino.vn](https://tino.vn) để hỗ trợ!** 🚀