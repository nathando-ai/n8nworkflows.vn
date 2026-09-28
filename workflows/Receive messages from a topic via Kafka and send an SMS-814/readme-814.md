---
title: "📢 Tự Động Hóa Nhận Tin Nhắn Kafka → SMS Vô Cần Code - Giảm Thời Gian 90%!"
description: "Workflow n8n tự động nhận tin nhắn từ topic Kafka và gửi SMS ngay lập tức, không cần viết code. Giúp doanh nghiệp xử lý thông báo 24/7 với độ chính xác cao."
slug: "tu-dong-hoa-kafka-sms-voi-n8n"
tags: [n8n, automation, kafka, sms, vonage, no-code]
keywords: [n8n workflow kafka, tự động hóa sms, nhận tin nhắn kafka, vonage api n8n, tự động hóa doanh nghiệp]
---

# 🚀 **Tự Động Hóa Nhận Tin Nhắn Kafka → Gửi SMS Vô Cần Code**

Bạn có bao giờ phải chờ đợi tin nhắn từ hệ thống Kafka để xử lý thủ công? Hay phải ngồi kiểm tra liên tục để không bỏ lỡ thông báo quan trọng? Với **workflow này**, các sếp sẽ **tự động nhận tin nhắn từ Kafka và chuyển ngay thành SMS**, tiết kiệm **90% thời gian** và **tránh bỏ lỡ thông báo** dù ở bất kỳ đâu.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Không cần kiểm tra thủ công, hệ thống hoạt động **24/7** mà không cần can thiệp.
- **Tiết kiệm thời gian**: Giảm **90% công việc lặp lại** trong việc chuyển tiếp thông báo.
- **Độ chính xác cao**: Tin nhắn được chuyển ngay từ Kafka → SMS **không sai sót**.
- **Dễ dàng mở rộng**: Có thể kết nối với nhiều topic Kafka khác hoặc gửi SMS đến nhiều số điện thoại.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
- **Tài khoản Kafka** (để kết nối với topic nhận tin nhắn).
- **API Key Vonage** (để gửi SMS).
- **Số điện thoại nhận SMS** (đã đăng ký với Vonage).

:::note[Lưu ý]
- Nếu chưa có tài khoản Vonage, đăng ký tại [Vonage Developer](https://developer.vonage.com/) (miễn phí cho thử nghiệm).
- Topic Kafka phải **được tạo sẵn** và **cấu hình chủ đề (topic name)** trong workflow.
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể **import** workflow từ file JSON hoặc **copy/paste** JSON vào **n8n Editor**:
1. Mở **n8n Editor** (trang chủ của n8n).
2. Nhấn **"Import"** → **"From JSON"**.
3. Dán JSON từ [link gốc](https://n8n.io/workflows/814) hoặc tải file JSON từ đó.
4. Nhấn **"Import"** để hoàn tất.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này có **4 node chính**, các sếp cần **cấu hình kỹ lưỡng** như sau:

##### **🔹 Node 1: Kafka Trigger (n8n-nodes-base.kafkaTrigger)**
- **Chọn credentials**: Chọn **"kafka"** (nếu chưa có, tạo mới trong **Credentials** của n8n).
- **Topic**: Nhập **tên topic Kafka** bạn muốn theo dõi (ví dụ: `orders`, `alerts`).
- **Group ID**: Nhập một **ID nhóm** (có thể là `n8n-sms-group`).
- **Offset Reset**: Chọn **"earliest"** (để bắt đầu từ tin nhắn cũ nhất).

##### **🔹 Node 2: IF (n8n-nodes-base.if)**
- **Điều kiện mặc định**: Node này **không cần chỉnh sửa** (sử dụng để kiểm tra tin nhắn có tồn tại hay không).
- **Nếu tin nhắn tồn tại**, workflow sẽ chuyển sang **Node Vonage** để gửi SMS.

##### **🔹 Node 3: Vonage (n8n-nodes-base.vonage)**
- **Chọn credentials**: Chọn **"vonageApi"** (nếu chưa có, tạo mới trong **Credentials** của n8n).
- **API Key & Secret Key**: Điền từ tài khoản Vonage của bạn.
- **Số điện thoại gửi (From)**: Nhập số điện thoại **Vonage** (ví dụ: `+1234567890`).
- **Số điện thoại nhận (To)**: Nhập số điện thoại **của khách hàng** (ví dụ: `+84123456789`).
- **Thông điệp (Message)**: Sử dụng **expression** để lấy nội dung tin nhắn từ Kafka:
  ```json
  {{ $json.message }}
  ```
  (Nếu tin nhắn có cấu trúc JSON, có thể lấy trường cụ thể như `{{ $json.data.content }}`).

##### **🔹 Node 4: NoOp (n8n-nodes-base.noOp)**
- **Node này không cần chỉnh sửa**, chỉ dùng để **dừng workflow** sau khi gửi SMS thành công.

#### **3. Kích hoạt ⚡️**
1. **Test run** với dữ liệu mẫu:
   - Nhấn **"Run"** trên node **Kafka Trigger**.
   - Kiểm tra **log** để đảm bảo tin nhắn được chuyển thành SMS.
2. **Bật Active workflow**:
   - Nhấn **"Active"** ở góc trên bên phải để workflow **chạy tự động**.

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁCH NÂNG CAO]
- **Gửi SMS nhiều người**: Sử dụng **expression** để lấy danh sách số điện thoại từ Kafka và gửi SMS cho tất cả.
  ```json
  {{ $json.recipients }}
  ```
- **Lưu log tin nhắn**: Kết nối với **Google Sheets** hoặc **Slack** để ghi lại lịch sử SMS đã gửi.
- **Kết hợp với Telegram**: Thay vì SMS, có thể gửi thông báo qua **Telegram Bot** bằng node `telegram`.
- **Xử lý lỗi**: Thêm node **Set** để lưu tin nhắn thất bại vào **database** hoặc **email admin**.
:::

---

### 📌 **Kết luận**
Workflow này giúp **tự động hóa hoàn toàn** quá trình nhận tin nhắn từ Kafka và chuyển thành SMS, **giúp các sếp tiết kiệm thời gian và tránh bỏ lỡ thông báo quan trọng**. **Hãy áp dụng ngay** và **cải thiện hiệu suất công việc** của doanh nghiệp!

👉 **Bắt đầu tự động hóa ngay** với [n8n Self-hosted](https://n8n.io/) và **cài đặt workflow này** trong vài phút! 🚀