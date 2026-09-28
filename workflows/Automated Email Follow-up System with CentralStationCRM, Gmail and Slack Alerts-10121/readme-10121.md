---
title: "🚀 Hệ Thống Theo Dõi Email Tự Động với CentralStationCRM, Gmail & Thông Báo Slack - Tiết Kiệm 100% Thời Gian Theo Dõi Lead"
description: "Workflow tự động hóa gửi email nhắc nhở, theo dõi phản hồi và cảnh báo trên Slack cho các lead có tag 'Outreach' trong CentralStationCRM. Giúp các sếp tự động hóa quy trình nurturing lead mà không cần code."
slug: "he-thong-theo-doi-email-tu-dong-centralstationcrm-gmail-slack"
tags: [n8n, automation, no-code, CRM, lead-nurturing, gmail, slack, centralstationcrm]
keywords: [tự động hóa email, CRM tự động, theo dõi lead, n8n workflow, gửi email tự động, cảnh báo Slack, CentralStationCRM API]
---

# 🚀 **Hệ Thống Theo Dõi Email Tự Động với CentralStationCRM, Gmail & Thông Báo Slack**

### **Giải pháp cho các sếp muốn tự động hóa quy trình nurturing lead mà không cần code**
Hãy tưởng tượng một tình huống: Các sếp đã gửi email cho lead nhưng không biết họ đã trả lời chưa? Hoặc phải mất nhiều thời gian theo dõi từng lead một cách thủ công? **Workflow này sẽ giải quyết tất cả những vấn đề đó** bằng cách tự động:
- Gửi email nhắc nhở cho lead có tag **"Outreach"** trong CentralStationCRM.
- Theo dõi phản hồi trong vòng **7 ngày**.
- Cảnh báo ngay trên Slack nếu lead đã trả lời.
- **Không cần can thiệp thủ công**, tiết kiệm **gần 10 giờ/tuần** cho các sếp.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Không cần theo dõi từng lead một cách thủ công.
✅ **Tăng hiệu quả chuyển đổi**: Email nhắc nhở được gửi tự động, tăng cơ hội lead phản hồi.
✅ **Cảnh báo tức thời**: Nhận thông báo trên Slack khi lead trả lời, không bỏ lỡ bất kỳ cơ hội nào.
✅ **Hoạt động liên tục**: Workflow chạy tự động hàng ngày vào **17:00** (thời gian có thể điều chỉnh).
✅ **Tránh trùng lặp**: Hệ thống loại bỏ email trùng lặp để tránh làm phiền lead.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản CentralStationCRM** (CRM dành cho đội ngũ nhỏ).
✔ **API Key của CentralStationCRM** (xem hướng dẫn dưới đây).
✔ **Tài khoản Gmail** (để gửi email tự động).
✔ **Tài khoản Slack** (để nhận cảnh báo).
✔ **n8n Workflow Editor** (cài đặt trên máy hoặc VPS).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Truy cập [n8n.io](https://n8n.io/) và đăng nhập vào Editor.
2. Nhấn **"Import"** và chọn file JSON (hoặc copy/paste JSON từ [link gốc](https://n8n.io/workflows/10121)).
3. Chọn **"Import"** để tải workflow vào.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này có **14 node** và cần cấu hình kỹ lưỡng để hoạt động hiệu quả. Dưới đây là hướng dẫn chi tiết:

##### **A. Cấu hình CentralStationCRM API Key**
1. **Tạo API Key trong CentralStationCRM**:
   - Đăng nhập vào [CentralStationCRM](https://centralstationcrm.de).
   - Nhấn vào **bánh răng (⚙️) ở góc trên phải** → **"Settings"**.
   - Chọn **"API Keys"** → **"Create API Key"**.
   - Nhập **mô tả** (ví dụ: *"n8n Automation"*) và lưu.
   - **Lưu API Key này vì nó sẽ không được hiển thị lại!**

2. **Thêm Credentials trong n8n**:
   - Trong **n8n Editor**, nhấn **"Credentials"** (góc trên phải).
   - Chọn **"Add"** → **"Add new credential"**.
   - Chọn **"Header Auth"** (loại xác thực).
   - Nhập:
     - **Name**: `X-apikey` (không đổi).
     - **Value**: Dán **API Key** vừa tạo.
   - Nhấn **"Save"**.

##### **B. Cấu hình Gmail**
1. **Kết nối Gmail với n8n**:
   - Trong **n8n Editor**, nhấn **"Credentials"** → **"Add"** → **"Add new credential"**.
   - Chọn **"Gmail"** → **"Connect with Google"**.
   - Đăng nhập tài khoản Gmail và cấp quyền cho n8n.
   - **Lưu tài khoản này** để sử dụng trong các node Gmail sau.

2. **Cấu hình các node Gmail**:
   - Trong workflow, các node Gmail có tên:
     - `get last 7 days`
     - `get last 7 days again`
     - `Send a message`
     - `send another message`
   - **Chọn credentials Gmail** tương ứng trong mỗi node.

##### **C. Cấu hình Slack**
1. **Kết nối Slack với n8n**:
   - Trong **n8n Editor**, nhấn **"Credentials"** → **"Add"** → **"Add new credential"**.
   - Chọn **"Slack"** → **"Connect with Slack"**.
   - Đăng nhập tài khoản Slack và cấp quyền.
   - **Lưu credentials này**.

2. **Cấu hình các node Slack**:
   - Trong workflow, có **2 node Slack**:
     - `alert user` (cảnh báo khi lead chưa trả lời).
     - `alert user1` (cảnh báo khi lead đã trả lời).
   - **Chọn credentials Slack** trong mỗi node.
   - **Cấu hình thông báo**:
     - Trong trường **"User (By Username)"**, nhập `@SlackUsername` (ví dụ: `@team-lead`).
     - **Tùy chỉnh nội dung thông báo** trong trường **"Message"** (ví dụ: *"Lead đã trả lời email!"*).

##### **D. Cấu hình Cron Trigger**
- Node **"Cron: weekday 17:00"** sẽ kích hoạt workflow **mỗi thứ 2 đến thứ 6 lúc 17:00**.
- **Không cần chỉnh sửa** nếu muốn giữ thời gian mặc định.

##### **E. Loại bỏ email trùng lặp**
- Workflow sử dụng **2 node Remove Duplicates** để tránh gửi email trùng lặp cho cùng một lead.
- **Không cần chỉnh sửa** node này.

---

#### **3. Kích hoạt ⚡️ Workflow**
1. **Test Run (kiểm tra trước khi chạy thực tế)**:
   - Nhấn **"Run"** trên workflow.
   - **Không dùng dữ liệu thực tế** để test (để tránh gửi email thật cho lead).
   - **Lưu ý**: Nếu muốn test nhanh, các sếp có thể **xóa node Wait 7 days** (nhấn vào icon thùng rác trên đường nối) và **reconnect lại sau khi test xong**.

2. **Bật Active Workflow**:
   - Sau khi kiểm tra thành công, nhấn **"Active"** để workflow chạy tự động hàng ngày.

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁC Ý TƯỞNG NÂNG CAO]
🔹 **Thêm thông báo trên Telegram**: Kết nối với Telegram Bot để nhận cảnh báo ngoài Slack.
🔹 **Lưu log hoạt động**: Sử dụng node **StickyNote** để ghi lại lịch sử email đã gửi.
🔹 **Gửi báo cáo định kỳ**: Tạo một workflow riêng để tổng hợp thống kê lead đã phản hồi.
🔹 **Tùy chỉnh email**: Sử dụng **n8n-nodes-base.llm** (nếu có) để tự động hóa nội dung email dựa trên phản hồi.
🔹 **Kết hợp với Zapier/Make**: Nếu cần tích hợp thêm dịch vụ khác (ví dụ: Mailchimp, HubSpot).
:::

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa quy trình nurturing lead mà không cần code. Bằng cách kết hợp **CentralStationCRM, Gmail và Slack**, các sếp sẽ:
✔ **Tiết kiệm thời gian** theo dõi lead.
✔ **Tăng cơ hội chuyển đổi** với email nhắc nhở tự động.
✔ **Nhận cảnh báo tức thời** khi lead phản hồi.

**Hãy import workflow ngay hôm nay và bắt đầu tự động hóa công việc của mình!** 🚀
Nếu có bất kỳ câu hỏi nào, các sếp có thể tham khảo [hướng dẫn chi tiết của CentralStationCRM](https://centralstationcrm.de/) hoặc liên hệ hỗ trợ n8n tại [n8n.io](https://n8n.io/).

---
**Chúc các sếp thành công với tự động hóa!** 💪