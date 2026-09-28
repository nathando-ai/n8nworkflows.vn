---
title: "🚀 Tự Động Thêm Khối Thời Gian Đi Đến Lịch Trình Tự Động Với Google Directions API (N8n)"
description: "Workflow tự động hóa 100% không code giúp các sếp thêm khối thời gian đi lại trước các cuộc hẹn trên Google Calendar, đảm bảo không bao giờ muộn giờ. Sử dụng AI Agent + Google Directions API để tính toán thời gian chính xác và tự động tạo blocker trên lịch."
slug: "tự-dộng-thêm-khối-thời-gian-di-den-lich-trình"
tags: [n8n, automation, google-calendar, google-directions-api, ai-agent, productivity]
keywords: [n8n workflow tự động hóa lịch, tính thời gian đi lại tự động, blocker lịch Google, AI Agent n8n, Google Directions API tự động]
---

# 🚀 **Tự Động Thêm Khối Thời Gian Đi Đến Lịch Trình Trước Cuộc Hẹn (Không Code!)**

### **Nỗi Đau Của Các Sếp:**
Làm việc với lịch trật tự, các sếp thường gặp phải tình trạng **muộn giờ** do không tính toán thời gian đi lại chính xác. Thậm chí, khi có nhiều cuộc hẹn liên tiếp, việc tính toán thời gian chuyển đổi giữa các địa điểm trở nên phức tạp và dễ sai sót. **Workflow này giải quyết vấn đề này bằng cách tự động thêm khối thời gian đi lại vào lịch trước mỗi cuộc hẹn**, đảm bảo các sếp luôn có thời gian dự phòng và không bao giờ bị trễ.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần tính toán thủ công thời gian đi lại hàng ngày.
- **Đảm bảo không muộn giờ**: Khối thời gian được tính toán chính xác từ nhà (hoặc địa điểm trước đó) đến địa điểm cuộc hẹn.
- **Tự động hóa hoàn toàn**: Workflow chạy hàng ngày vào 7h sáng, không cần can thiệp.
- **Cá nhân hóa**: Chỉ áp dụng cho các cuộc hẹn có địa điểm cụ thể (không ảnh hưởng đến lịch trống).
- **Buffer an toàn**: Thêm 10 phút dự phòng để tránh tình trạng kẹt xe hoặc chậm trễ bất ngờ.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Calendar** (đã kết nối OAuth 2.0).
2. **API Key Google Directions API** (mã giảm giá đầu tiên miễn phí: [Đăng ký tại đây](https://developers.google.com/maps/documentation/directions/get-api-key)).
3. **Tài khoản OpenAI** (hoặc thay thế bằng một provider LLM khác như Mistral AI, Perplexity).
4. **Địa chỉ nhà (Home Address)**: Địa điểm xuất phát mặc định để tính toán thời gian đi lại.
5. **Tên khối thời gian (Blocker name)**: Tên hiển thị trên lịch (ví dụ: "Đi đến cuộc hẹn").
6. **Phương thức vận chuyển (Mode)**: Chọn một trong 4 lựa chọn:
   - `transit` (xế dịch vụ công)
   - `driving` (lái xe)
   - `walking` (đi bộ)
   - `bicycling` (đạp xe).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Bước 1**: Tải file JSON từ [n8n.io/workflows/6700](https://n8n.io/workflows/6700).
- **Bước 2**: Trong n8n Editor, nhấn **"Import"** và chọn file JSON.
- **Bước 3**: Chọn **"Create new workflow"** và nhấn **"Import"**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflows này bao gồm **11 node** với logic phức tạp. Các sếp cần chú ý cấu hình các node sau:

##### **A. Cấu Hình Tham Số Mặc Định (Set Defaults)**
- **Node: "Set Defaults"**
  - Điền **Home Address** (địa chỉ nhà hoặc nơi xuất phát mặc định).
  - Đặt **Blocker name** (ví dụ: "Đi đến cuộc hẹn").
  - Chọn **mode** (phương thức vận chuyển).

##### **B. Kết Nối Credentials**
1. **Google Calendar OAuth 2.0**:
   - Tạo credential mới trong n8n với tên `"googleCalendarOAuth2Api"` và kết nối tài khoản Google Calendar.
2. **OpenAI API**:
   - Tạo credential với tên `"openAiApi"` và điền **API Key** từ tài khoản OpenAI.
   - **Lưu ý**: Nếu muốn thay thế bằng một provider khác (ví dụ Mistral), thay đổi trong node `"OpenAI Chat Model"`.
3. **Google Directions API**:
   - Tạo credential **Query Auth** với tên `"key"` và điền **API Key** từ Google.
   - **Hướng dẫn lấy API Key**: [Tại đây](https://g.co/gemini/share/b731be41d4f3).

##### **C. Cấu Hình Node "AI Agent"**
- Node `"AI Agent"` sẽ tự động:
  - Lấy danh sách cuộc hẹn từ Google Calendar.
  - Lọc ra các cuộc hẹn có địa điểm.
  - Tính toán thời gian đi lại từ **Home Address** (hoặc địa điểm trước đó) đến địa điểm cuộc hẹn.
  - Tạo **khối thời gian (blocker)** trước cuộc hẹn với thời gian tính toán + 10 phút buffer.

##### **D. Node "Call Google Directions API"**
- Đảm bảo credential **Query Auth** (`httpQueryAuth`) đã được cấu hình với API Key Google Directions.

##### **E. Node "Schedule Trigger"**
- Workflow sẽ chạy **hàng ngày lúc 7h sáng** (thời gian mặc định). Nếu muốn thay đổi, mở node này và chỉnh sửa **cron expression**.

#### **3. Kích Hoạt ⚡️**
- **Test Run**: Nhấn **"Run"** để kiểm tra workflow với dữ liệu mẫu.
- **Bật Active**: Sau khi kiểm tra thành công, nhấn **"Active"** để workflow chạy tự động hàng ngày.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[TIẾP CẬN HƠN]
1. **Thêm Slack/Telegram Notifications**:
   - Sử dụng node **Slack** hoặc **Telegram Bot** để thông báo khi workflow tạo thành công khối thời gian.
2. **Lưu Log Lịch Sử**:
   - Thêm node **Set** hoặc **File** để lưu lịch sử các khối thời gian đã tạo vào Google Sheets hoặc cơ sở dữ liệu.
3. **Tùy Chỉnh Thời Gian Buffer**:
   - Trong node **"Set Travel_time"**, các sếp có thể tăng giảm buffer (ví dụ: +15 phút thay vì +10 phút).
4. **Áp Dụng Cho Nhiều Địa Chỉ**:
   - Nếu các sếp thường đi lại giữa nhiều địa điểm (ví dụ: nhà → văn phòng → khách hàng), workflow sẽ tự động tính toán thời gian giữa các điểm.
5. **Thay Thế AI Provider**:
   - Nếu OpenAI quá đắt, các sếp có thể thử **Mistral AI** hoặc **Perplexity** bằng cách thay đổi trong node `"lmChatOpenAi"`.
:::

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn **tự động hóa lịch trình**, tránh tình trạng muộn giờ và tiết kiệm thời gian. Với **AI Agent + Google Directions API**, nó không chỉ tính toán thời gian chính xác mà còn **cá nhân hóa** cho từng cuộc hẹn.

**Hành động ngay!**
1. Import workflow vào n8n.
2. Cấu hình credentials và tham số mặc định.
3. Bật **Active** và để workflow làm việc cho bạn hàng ngày.

**🎁 Đăng ký VPS để tự host n8n 24/7:**
👉 [VPS TinoHost (Mã giảm giá: **VPSN8N**)](https://tino.vn/vps-n8n?affid=388)
👉 [VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)

---
**Chúc các sếp tự động hóa cuộc sống hiệu quả hơn!** 🚀