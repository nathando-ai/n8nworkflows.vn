---
title: "🍽️ Hệ Thống Đặt Bàn Tự Động Cho Nhà Hàng Với VAPI + PostgreSQL (Không Cần Code)"
description: "Tự động hóa hoàn toàn quá trình nhận gọi đặt bàn, kiểm tra sẵn có bàn ăn và xác nhận đặt chỗ cho nhà hàng, tiết kiệm thời gian nhân viên và giảm thiểu lỗi thủ công. Workflow này kết hợp VAPI (Voice API) với cơ sở dữ liệu PostgreSQL để cung cấp trải nghiệm đặt bàn chuyên nghiệp 24/7."
slug: "he-thong-dat-ban-tu-dong-voi-vapi-postgresql"
tags: [n8n, automation, no-code, restaurant-automation, voice-api, postgres]
keywords: [tự động hóa nhà hàng, đặt bàn tự động, VAPI n8n, PostgreSQL automation, workflow đặt bàn không code]
---

# 🚀 Hệ Thống Đặt Bàn Tự Động Cho Nhà Hàng Với VAPI + PostgreSQL

### 📞 **Giải quyết nỗi đau của các sếp nhà hàng**
Hiện nay, việc quản lý đặt bàn thủ công không chỉ tốn thời gian mà còn dễ gây ra những sai sót như:
- **Thiếu bàn ăn** khi không kiểm tra sẵn có kịp thời.
- **Trùng đặt bàn** dẫn đến mất khách và mất uy tín.
- **Nhân viên phải làm nhiều việc** thay vì tập trung vào dịch vụ khách hàng.
- **Không thể hoạt động 24/7** khi nhân viên nghỉ hoặc nhà hàng đóng cửa.

**Workflow này tự động hóa toàn bộ quy trình** từ nhận gọi đặt bàn (thông qua VAPI) đến kiểm tra sẵn có bàn ăn trong PostgreSQL, đặt chỗ và gửi xác nhận tự động. **Không cần viết một dòng code nào!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động ổn định 24/7, các sếp nên cài n8n trên **VPS riêng** (Self-hosted) để đảm bảo tính riêng tư và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian nhân viên**: Không cần phải ghi chép thủ công hoặc gọi điện xác nhận.
- **Tránh trùng đặt bàn**: Kiểm tra sẵn có bàn ăn trong thời gian thực.
- **Hoạt động 24/7**: Khách hàng có thể đặt bàn bất kỳ lúc nào, ngay cả khi nhà hàng đóng cửa.
- **Tăng trải nghiệm khách hàng**: Xác nhận đặt bàn tự động và nhanh chóng.
- **Giảm thiểu lỗi**: Không cần phải nhớ hoặc ghi nhầm thông tin đặt bàn.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản VAPI** (Voice API) để nhận và gửi gọi điện tự động.
   - **API Key** và **Credentials** của VAPI.
   - **URL Callback** (được tự động tạo khi import workflow).
2. **Cơ sở dữ liệu PostgreSQL** để lưu trữ thông tin bàn ăn và đặt bàn.
   - **Thông tin kết nối PostgreSQL**:
     - Host, Port, Database Name, Username, Password.
   - **Bảng `tables`** (cần tồn tại trước khi chạy workflow):
     ```sql
     CREATE TABLE IF NOT EXISTS tables (
       id SERIAL PRIMARY KEY,
       table_number VARCHAR(10) NOT NULL,
       capacity INT NOT NULL,
       is_booked BOOLEAN DEFAULT FALSE,
       booked_until TIMESTAMP
     );
     ```
   - **Bảng `bookings`** (để lưu lịch sử đặt bàn):
     ```sql
     CREATE TABLE IF NOT EXISTS bookings (
       id SERIAL PRIMARY KEY,
       booking_id VARCHAR(50) NOT NULL,
       table_number VARCHAR(10) NOT NULL,
       customer_name VARCHAR(100) NOT NULL,
       phone_number VARCHAR(20) NOT NULL,
       booking_time TIMESTAMP NOT NULL,
       number_of_people INT NOT NULL,
       status VARCHAR(20) DEFAULT 'pending',
       created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
     );
     ```
3. **Credentials trong n8n**:
   - **PostgreSQL**: Thêm credential mới trong n8n với tên `"postgres"` và điền thông tin kết nối.
   - **VAPI**: Thêm credential mới trong n8n với tên `"vapi"` và điền `API Key`.

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### 1. **Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải file JSON** từ [đây](https://n8n.io/workflows/5466) (nếu link vẫn hoạt động) hoặc sao chép JSON từ canvas.
- Trong **n8n Editor**, nhấn **Import** và chọn file JSON hoặc dán JSON vào ô **Import Workflow**.

#### 2. **Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này bao gồm **2 phần chính**:
- **Kiểm tra sẵn có bàn ăn** (Availability Check Flow).
- **Xử lý đặt bàn** (Booking Flow).

##### **A. Cấu hình Webhook cho VAPI**
Workflow sử dụng **2 Webhook** để nhận gọi từ VAPI:
1. **Trigger: Booking Request (VAPI)** (Path: `027f0f14-93f4-42ff-90a7-715f23316a86`):
   - Đây là Webhook để nhận **yêu cầu đặt bàn** từ khách hàng.
   - Khi import, n8n sẽ tự động tạo URL Webhook. Các sếp cần **cấu hình trong VAPI** để khi gọi điện, VAPI sẽ gửi dữ liệu đến URL này.
   - **Tham số cần điền trong VAPI**:
     - **Endpoint URL**: `https://<tên-domain-n8n>/webhook/027f0f14-93f4-42ff-90a7-715f23316a86`
     - **HTTP Method**: `POST`
     - **Headers**: `Content-Type: application/json`

2. **Trigger: Booking Request (VAPI) #2** (Path: `2f7eff83-2e85-45ee-b544-7f889ca3ad07`):
   - Đây là Webhook để **xác nhận đặt bàn thành công** (sẽ được gọi sau khi đặt bàn).
   - Cấu hình tương tự như Webhook đầu tiên.

##### **B. Cấu hình PostgreSQL**
Workflow sử dụng **2 node PostgreSQL**:
1. **Query Table Availability (Postgres)**:
   - **Operation**: `select` (để kiểm tra bàn ăn có sẵn không).
   - **Query SQL**:
     ```sql
     SELECT * FROM tables WHERE table_number = $json["table_number"] AND is_booked = FALSE AND booked_until < NOW();
     ```
   - **Credentials**: Chọn `"postgres"` (đã thêm trước đó).

2. **Upsert Booking in Postgres**:
   - **Operation**: `upsert` (để thêm hoặc cập nhật đặt bàn).
   - **Query SQL**:
     ```sql
     INSERT INTO bookings (booking_id, table_number, customer_name, phone_number, booking_time, number_of_people, status)
     VALUES ($json["booking_id"], $json["table_number"], $json["customer_name"], $json["phone_number"], $json["booking_time"], $json["number_of_people"], 'confirmed')
     ON CONFLICT (booking_id) DO UPDATE
     SET status = 'confirmed', updated_at = NOW();
     ```
   - **Credentials**: Chọn `"postgres"`.

##### **C. Cấu hình Respond to Webhook**
Workflow sử dụng **2 node `respondToWebhook`** để trả lời VAPI:
1. **Respond: Availability Status (VAPI)**:
   - Trả lời về **sẵn có bàn ăn** (có/không).
   - **Tham số trả về**:
     ```json
     {
       "status": "available" || "unavailable",
       "message": "Bàn số X đã sẵn sàng!" || "Xin lỗi, bàn số X đã được đặt."
     }
     ```

2. **Respond: Booking Confirmation (VAPI)**:
   - Trả lời **xác nhận đặt bàn thành công**.
   - **Tham số trả về**:
     ```json
     {
       "status": "confirmed",
       "message": "Đặt bàn thành công! Bàn số X sẽ chờ quý khách từ giờ Y.",
       "booking_id": "ID_dat_bàn"
     }
     ```

---

#### 3. **Kích hoạt ⚡️**
1. **Test Run**:
   - Nhấn **Run Workflow** và gửi một **gọi mô phỏng** từ VAPI để kiểm tra:
     - Dữ liệu đặt bàn có được lưu vào PostgreSQL không?
     - Trả lời từ VAPI có chính xác không?
2. **Bật Active**:
   - Sau khi kiểm tra thành công, nhấn **Active** để workflow hoạt động liên tục.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram** để thông báo đặt bàn mới cho quản lý nhà hàng.
   - Ví dụ: Khi đặt bàn thành công, gửi tin nhắn Slack với thông tin:
     ```
     🚨 **Đặt bàn mới!**
     - Khách hàng: [Tên]
     - Số điện thoại: [Số]
     - Bàn: [Số bàn]
     - Thời gian: [Giờ]
     ```

2. **Lưu log hoạt động**:
   - Thêm node **Sticky Note** hoặc **Google Sheets** để ghi lại lịch sử đặt bàn và trạng thái.
   - Ví dụ:
     ```
     | Booking ID | Table | Customer | Status | Time |
     |------------|-------|----------|--------|------|
     | 12345     | 1     | Lê Văn A | Confirmed | 2024-05-20 18:00 |
     ```

3. **Gửi báo cáo định kỳ**:
   - Sử dụng node **Set** và **Schedule** để gửi báo cáo số lượng đặt bàn hàng ngày/tuần cho quản lý.
   - Ví dụ: Gửi email hoặc Slack với thống kê:
     ```
     📊 **Báo cáo đặt bàn ngày 20/05**
     - Tổng đặt bàn: 15
     - Bàn sẵn có: 8
     - Doanh thu dự kiến: 5.000.000 VNĐ
     ```

4. **Cá nhân hóa thông báo**:
   - Sử dụng **LLM (n8n-nodes-ai.llm)** để tự động tạo tin nhắn thân thiện hơn cho khách hàng:
     ```
     "Chào [Tên khách hàng], cảm ơn quý khách đã đặt bàn tại [Tên nhà hàng]! Chúng tôi rất vui khi phục vụ quý khách tại bàn số [Số bàn] vào lúc [Giờ]."
     ```

---

### 📌 **Kết luận**
Workflow này **giải phóng nhân viên nhà hàng** khỏi công việc lặp đi lặp lại, đồng thời **tăng cường trải nghiệm khách hàng** với quy trình đặt bàn nhanh chóng và chính xác. **Không cần code, không cần kiến thức kỹ thuật sâu**, các sếp chỉ cần cài đặt và cấu hình theo hướng dẫn là có thể vận hành hệ thống ngay từ hôm nay.

**Hành động ngay!**
1. **Cài đặt n8n trên VPS** (để đảm bảo hoạt động 24/7).
2. **Import workflow** và cấu hình PostgreSQL + VAPI.
3. **Test và bật Active** để bắt đầu tự động hóa đặt bàn!

**Nếu có vấn đề**, các sếp có thể tham khảo [hướng dẫn cài đặt n8n trên VPS](https://docs.n8n.io/hosting/self-hosting/) hoặc liên hệ cộng đồng n8n tại [n8n Community](https://community.n8n.io/).

---
🚀 **Chúc các sếp thành công với hệ thống đặt bàn tự động hóa!** 🍽️