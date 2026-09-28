---
title: "🌍 Tự Động Hóa Dự Báo Thời Tiết Du Lịch Từ Google Calendar Sang Telegram - Không Cần Code"
description: "Workflow tự động hóa thông minh giúp các sếp nhận dự báo thời tiết chính xác cho chuyến đi ngay khi lịch trình được cập nhật trên Google Calendar, giảm thiểu rủi ro và tối ưu hóa kế hoạch du lịch. Hỗ trợ cảnh báo thời tiết khẩn cấp qua Telegram 24/7."
slug: "tự-dộng-hoa-du-báo-thời-tiết-du-lịch"
tags: [n8n, automation, google-calendar, telegram-bot, thời-tiết, du-lịch, no-code]
keywords: [tự động hóa n8n, dự báo thời tiết du lịch, cảnh báo thời tiết telegram, tự động hóa google calendar, workflow n8n du lịch]
---

# 🌍 **Tự Động Hóa Dự Báo Thời Tiết Du Lịch Từ Google Calendar Sang Telegram**

### **Giải pháp nào cho các sếp khi:**
- **Làm thủ công:** Phải nhớ check thời tiết cho từng chuyến đi, lo lắng về thời tiết bất ngờ làm thay đổi kế hoạch.
- **Sử dụng app thông thường:** Không có cảnh báo thời tiết cá nhân hóa cho chuyến đi cụ thể, thiếu thông tin chi tiết về thời gian và địa điểm.
- **Cần tính chuyên nghiệp:** Muốn tự động hóa cảnh báo thời tiết cho đội ngũ nhân viên đi công tác hoặc gia đình đi du lịch, nhưng không biết cách code.

**Workflow này sẽ giúp các sếp:**
✅ **Nhận dự báo thời tiết chính xác** cho chuyến đi ngay khi lịch trình được cập nhật trên Google Calendar.
✅ **Cảnh báo thời tiết khẩn cấp** (bão, mưa lớn, lốc xoáy...) qua Telegram **1 ngày trước chuyến đi** để có thời gian chuẩn bị.
✅ **Tiết kiệm thời gian** lên đến **50%** so với cách làm thủ công.
✅ **Hoạt động liên tục 24/7** mà không cần can thiệp của con người.

---

## 🎯 **Kết quả các sếp nhận được**

:::tip[LỢI ÍCH CỐT LÕI]
- **Thông tin thời tiết chính xác và cá nhân hóa:** Dự báo thời tiết **chỉ dành cho chuyến đi** của bạn, với thông tin chi tiết về nhiệt độ, mưa, gió, và cảnh báo khẩn cấp.
- **Cảnh báo kịp thời:** Nhận thông báo **1 ngày trước chuyến đi** để có thời gian điều chỉnh kế hoạch.
- **Tự động hóa hoàn toàn:** Không cần nhớ check thời tiết, hệ thống làm tất cả cho bạn.
- **Hỗ trợ đa kênh:** Có thể dễ dàng thay thế Telegram bằng Email, Slack, WhatsApp hoặc SMS.
- **Tiết kiệm chi phí:** Sử dụng **Visual Crossing API miễn phí** (1000 yêu cầu/ngày) và không cần đầu tư phần mềm.
:::

---

## 🔧 **Yêu cầu cần thiết**

:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Calendar** và **API Key** của Google Calendar (đăng ký tại [Google Cloud Console](https://console.cloud.google.com/)).
2. **Tài khoản Telegram** và **Chat ID** của bot Telegram (cách lấy Chat ID: gửi tin nhắn cho bot và copy ID từ link `https://t.me/YOURBOTNAME?start=ID`).
3. **API Key của Visual Crossing** (miễn phí, đăng ký tại [Visual Crossing](https://www.visualcrossing.com/)).
4. **Workflow n8n** đã cài đặt trên máy chủ riêng (Self-hosted) hoặc sử dụng n8n Cloud (miễn phí cho các dự án nhỏ).
:::

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải file JSON** từ [đây](https://n8n.io/workflows/10481) (hoặc sử dụng link gốc).
- Mở **n8n Editor** và chọn **Import Workflow** → Chọn file JSON hoặc dán JSON vào ô nhập.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **A. Cấu hình Google Calendar Trigger**
- **Node:** `Event created` và `Event updated` (cả hai đều cần cấu hình).
- **Thao tác:**
  - Chọn **Google Calendar** trong danh sách credentials.
  - Chọn **Calendar** muốn theo dõi (ví dụ: "Du lịch" hoặc "Công tác").
  - **Lưu ý:** Workflow sẽ **lọc các sự kiện** có từ khóa như "trip", "flight", "vacation" trong tiêu đề hoặc mô tả.

#### **B. Cấu hình Telegram Bot**
- **Node:** `Send Forecast`.
- **Thao tác:**
  - Chọn **Telegram** trong danh sách credentials.
  - Điền **Chat ID** của bot Telegram (cách lấy: gửi tin nhắn cho bot và copy ID từ link `https://t.me/YOURBOTNAME?start=ID`).
  - **Lưu ý:** Nếu chưa có bot Telegram, tạo bot tại [@BotFather](https://t.me/BotFather) và lấy **API Token**.

#### **C. Cấu hình API Key của Visual Crossing**
- **Node:** `Build interrogation URL` và `Get Destination Weather Forecast`.
- **Thao tác:**
  - Trong node `Build interrogation URL`, thêm **API Key** vào biến `VISUAL_CROSSING_API_KEY` (đăng ký miễn phí tại [Visual Crossing](https://www.visualcrossing.com/)).
  - **Lưu ý:** Workflow sử dụng **1000 yêu cầu miễn phí/ngày**, đủ cho hầu hết các chuyến đi cá nhân.

#### **D. Cấu hình Node `If` (Lọc chuyến đi)**
- **Node:** `If1`.
- **Thao tác:**
  - Đảm bảo **điều kiện lọc** trong node `If` là đúng (các sếp có thể chỉnh sửa code trong node `Identify trips` để thêm/bỏ từ khóa lọc).

#### **E. Cấu hình Node `Wait` (Chờ 1 ngày trước chuyến đi)**
- **Node:** `Wait`.
- **Thao tác:**
  - Workflow sẽ **tạm dừng** và **lấy lại dự báo thời tiết mới** **1 ngày trước chuyến đi** để đảm bảo thông tin chính xác nhất.

---

### **3. Kích hoạt ⚡️**
- **Test Run:** Chạy workflow với **dữ liệu mẫu** (tạo một sự kiện du lịch trên Google Calendar để kiểm tra).
- **Bật Active:** Sau khi kiểm tra thành công, **bật Active workflow** để nó hoạt động tự động.

---

## ✍️ **Mẹo & gợi ý nâng cao**

### **1. Thay thế Telegram bằng các kênh khác**
Các sếp có thể dễ dàng **thay thế node Telegram** bằng:
- **Email:** Sử dụng node `n8n-nodes-base.email`.
- **Slack:** Sử dụng node `n8n-nodes-base.slack`.
- **WhatsApp:** Sử dụng node `n8n-nodes-base.whatsapp`.
- **SMS:** Sử dụng node `n8n-nodes-base.twilio`.

**Cách thực hiện:**
- Xóa node `Send Forecast` (Telegram).
- Thêm node mới tương ứng với kênh thông báo mong muốn.
- Cấu hình credentials và nội dung thông báo tương ứng.

### **2. Lưu log để theo dõi lịch sử**
- Thêm **node `StickyNote`** để lưu thông tin dự báo thời tiết và lịch sử cảnh báo.
- **Cách thực hiện:**
  - Thêm node `StickyNote` vào workflow.
  - Cấu hình để lưu **tiêu đề sự kiện**, **dự báo thời tiết**, và **thời gian cảnh báo**.

### **3. Gửi báo cáo định kỳ**
- Sử dụng **node `n8n-nodes-base.schedule`** để gửi báo cáo tổng hợp thời tiết cho các chuyến đi trong tháng.
- **Cách thực hiện:**
  - Thêm node `Schedule` với thời gian chạy hàng tuần/tháng.
  - Sử dụng node `Code` để tổng hợp dữ liệu từ `StickyNote` và gửi qua Telegram/Email.

### **4. Cải thiện logic lọc chuyến đi**
- Trong node `Identify trips`, các sếp có thể **chỉnh sửa code** để thêm/bỏ từ khóa lọc (ví dụ: thêm "conference", "meeting" để lọc các chuyến đi công tác).
- **Mẫu code tham khảo:**
  ```javascript
  // Kiểm tra tiêu đề và mô tả sự kiện
  const isTrip = event.summary.toLowerCase().includes('trip') ||
                 event.summary.toLowerCase().includes('flight') ||
                 event.description.toLowerCase().includes('vacation');

  if (isTrip) {
    return { json: { ...event } };
  } else {
    return { json: null };
  }
  ```

---

## 📌 **Kết luận**

Workflow **Tự Động Hóa Dự Báo Thời Tiết Du Lịch** là giải pháp **tự động hóa hoàn toàn** giúp các sếp:
✔ **Nhận dự báo thời tiết chính xác** cho chuyến đi ngay khi lịch trình được cập nhật.
✔ **Cảnh báo thời tiết khẩn cấp** qua Telegram **1 ngày trước chuyến đi**.
✔ **Tiết kiệm thời gian và giảm thiểu rủi ro** khi đi du lịch hoặc công tác.

**Hành động ngay hôm nay:**
1. **Cài đặt n8n trên VPS** (Self-hosted) để workflow hoạt động 24/7.
2. **Import workflow** và cấu hình theo hướng dẫn trên.
3. **Bật Active workflow** và bắt đầu tự động hóa cuộc sống du lịch của mình!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::