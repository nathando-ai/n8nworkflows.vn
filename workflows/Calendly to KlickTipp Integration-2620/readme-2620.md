---
title: "🚀 Tự Động Hóa Tích Hợp Calendly & KlickTipp: Quản Lý Đặt Hẹn & Huỷ Thẻ 100% Không Code"
description: "Workflow này tự động đồng bộ hóa tất cả các sự kiện đặt hẹn, huỷ đặt hẹn từ Calendly sang KlickTipp, giảm thiểu sai sót và tiết kiệm thời gian quản lý khách hàng. Hỗ trợ xử lý khách mời, khách tham dự và trường dữ liệu tùy chỉnh."
slug: "tich-hop-calendly-klicktipp"
tags: [n8n, automation, calendly, klicktipp, no-code, CRM]
keywords: [tự động hóa calendly klicktipp, đồng bộ hóa đặt hẹn, quản lý khách hàng không code, workflow n8n cho doanh nghiệp, tự động hóa CRM]
---

# 🚀 **Tự Động Hóa Tích Hợp Calendly & KlickTipp: Quản Lý Đặt Hẹn & Huỷ Thẻ 100% Không Code**

## **💡 Bạn đang gặp vấn đề gì?**
Quản lý đặt hẹn thủ công trên **Calendly** rồi phải nhập lại vào **KlickTipp** để quản lý khách hàng? Hay phải lo lắng khi khách huỷ đặt hẹn mà không đồng bộ kịp thời? **Workflow này giải quyết tất cả!**

Với **Calendly to KlickTipp Integration**, các sếp có thể:
✅ **Tự động đồng bộ hóa** tất cả sự kiện đặt hẹn, huỷ đặt hẹn từ Calendly sang KlickTipp.
✅ **Xử lý khách mời và khách tham dự** một cách chính xác, không cần nhập thủ công.
✅ **Tự động cập nhật thông tin** như thời gian, địa điểm, và email khách hàng.
✅ **Giảm thiểu sai sót** và tiết kiệm **gần 10 giờ/tuần** cho đội ngũ quản lý.

---
### **🎯 Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần nhập lại dữ liệu từ Calendly sang KlickTipp.
- **Chính xác 100%**: Xử lý tự động các trường hợp đặt hẹn, huỷ đặt hẹn, và thay đổi lịch.
- **Quản lý khách hàng hiệu quả**: Tất cả thông tin khách hàng (khách mời, khách tham dự) được đồng bộ ngay lập tức.
- **Hoạt động 24/7**: Workflow chạy tự động, không cần can thiệp thủ công.
:::

---
### **🔧 Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần:
1. **Tài khoản Calendly** (đã cấu hình API).
2. **Tài khoản KlickTipp** (đã tạo các trường tùy chỉnh cần thiết).
3. **API Key của KlickTipp** (để kết nối với n8n).
4. **Các trường tùy chỉnh trong KlickTipp** (như `Booking Start Time`, `Booking End Time`, `Guest Emails`, `Invitee Email`).
5. **n8n Self-hosted** (để chạy workflow 24/7).
:::

---
### **🚀 Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Bước 1**: Tải file JSON từ [n8n.io/workflows/2620](https://n8n.io/workflows/2620).
- **Bước 2**: Mở **n8n Editor** và chọn **Import Workflow** → Chọn file JSON vừa tải.
- **Bước 3**: Chọn **Active** để kích hoạt workflow.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **18 node**, nhưng các bước quan trọng nhất cần chú ý:

##### **🔹 Node Calendly Trigger (`New Calendly event`)**
- **Cấu hình**:
  - Chọn **credentials** là `calendlyApi`.
  - Chọn **Event Type**: `Booking Created` và `Booking Cancelled`.
  - **Lưu ý**: Nếu muốn thêm sự kiện khác (ví dụ: `Event Rescheduled`), cần thêm vào trong **Credentials**.

##### **🔹 Node KlickTipp Subscribe (`Subscribe invitee booking in KlickTipp`, `Subscribe guest booking in KlickTipp`, ...)**
- **Cấu hình**:
  - **Credentials**: Chọn `klickTippApi`.
  - **Operation**: `subscribe` (để thêm hoặc cập nhật subscriber).
  - **Resource**: `subscriber`.
  - **Lưu ý**:
    - Cần **tạo trước các trường tùy chỉnh** trong KlickTipp (ví dụ: `Booking Start Time`, `Guest Emails`).
    - **Mapping dữ liệu**:
      - `Invitee Email` → `Email` (trường email của khách mời).
      - `Guest Emails` → `Custom Field` (nếu có).
      - `Booking Start Time` → `Start Time` (định dạng UNIX timestamp).

##### **🔹 Node Split Out (`Split Out guest bookings`, `Split Out guest cancellations`)**
- **Cấu hình**:
  - Chọn **JSON Path** để tách dữ liệu khách tham dự (ví dụ: `$.guests`).
  - **Lưu ý**: Nếu không có khách tham dự, node này sẽ bỏ qua.

##### **🔹 Node If (`Guests booking check`, `Guests cancellation check`, `Rescheduling check`)**
- **Cấu hình**:
  - **Condition**: Kiểm tra xem có khách tham dự không (`$.guests.length > 0`).
  - **Lưu ý**:
    - Nếu **không có khách tham dự**, workflow sẽ chuyển sang node `No guest email addresses found`.
    - Nếu **có khách tham dự**, sẽ xử lý thêm thông tin của họ.

##### **🔹 Node Set (`Convert data for KlickTipp`, `List guests for booking`, `List guests for cancellation`)**
- **Cấu hình**:
  - **Transform dữ liệu** để phù hợp với API KlickTipp.
  - **Ví dụ**:
    - Chuyển đổi `DateTime` thành **UNIX timestamp**.
    - Tách `Guest Emails` thành danh sách riêng biệt.

##### **🔹 Node NoOp (`Invitee did not add guests to the booking`, `Event was rescheduled`, `No guest email addresses found`)**
- **Cấu hình**:
  - Đây là **node placeholder** để xử lý trường hợp đặc biệt.
  - **Lưu ý**: Nếu muốn log hoặc gửi thông báo, có thể thay thế bằng **Slack/Email Node**.

---
#### **3. Kích hoạt ⚡️**
- **Bước 1**: **Test Run** với một sự kiện mẫu từ Calendly.
- **Bước 2**: Kiểm tra **KlickTipp** để xác nhận dữ liệu đã đồng bộ chính xác.
- **Bước 3**: Chuyển workflow sang **Active** để chạy 24/7.

---
### **✍️ Mẹo & gợi ý nâng cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Gửi thông báo Slack/Email khi có sự kiện mới**:
   - Thêm **Slack Node** hoặc **Email Node** sau node `New Calendly event` để thông báo cho đội ngũ.

2. **Lưu log hoạt động**:
   - Sử dụng **Google Sheets Node** để ghi lại tất cả sự kiện đặt hẹn, huỷ đặt hẹn và cập nhật.

3. **Tự động gửi email chào mừng**:
   - Kết hợp với **SendGrid Node** để gửi email chào mừng cho khách hàng mới.

4. **Xử lý trường hợp đặc biệt**:
   - Nếu có khách hàng thường xuyên huỷ đặt hẹn, có thể thêm **Logic Node** để gửi email nhắc nhở.

5. **Tích hợp với CRM khác**:
   - Nếu cần, có thể mở rộng để đồng bộ dữ liệu sang **HubSpot** hoặc **Zoho CRM**.
:::

---
### **📌 Kết luận**
Workflow **Calendly to KlickTipp Integration** là **giải pháp hoàn hảo** để tự động hóa quản lý đặt hẹn, giảm thiểu sai sót và tiết kiệm thời gian cho các sếp. **Không cần code**, chỉ cần cấu hình đúng các node và **chạy 24/7** mà không tốn chi phí thêm.

**👉 Bắt đầu ngay hôm nay!**
1. **Cài đặt n8n Self-hosted** trên VPS (để chạy ổn định).
2. **Import workflow** và cấu hình các node theo hướng dẫn.
3. **Test và kích hoạt** để tự động hóa quản lý đặt hẹn!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::