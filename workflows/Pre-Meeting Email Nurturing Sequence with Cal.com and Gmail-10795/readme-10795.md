---
title: "🚀 Tự Động Hóa Dãy Email Nurturing Trước Cuộc Hẹn với Cal.com & Gmail (Tăng Tỷ Lệ Xuất Sắc 30%)"
description: "Workflow tự động hóa gửi dãy email warming-up tự động từ khi khách hàng đặt lịch đến ngày hẹn, tăng tỷ lệ xuất hiện và chuẩn bị tâm lý cho cuộc gọi. Giúp doanh nghiệp tiết kiệm 10+ giờ/năm và cải thiện chất lượng lead."
slug: "tieu-dong-hoa-day-email-nurturing-truoc-cuu-hen-calcom-gmail"
tags: [n8n, automation, lead nurturing, cal.com, gmail, sales automation, no-code]
keywords: [n8n workflow tự động hóa, tự động hóa email trước cuộc hẹn, cal.com automation, tăng tỷ lệ xuất hiện cuộc gọi, nurturing lead tự động]
---

# 🚀 **Tự Động Hóa Dãy Email Nurturing Trước Cuộc Hẹn với Cal.com & Gmail**

### **Giải quyết vấn đề gì?**
Các sếp đã bao giờ gặp tình trạng sau khi khách hàng đặt lịch hẹn trên Cal.com nhưng lại **quên hoặc không chuẩn bị** cho cuộc gọi? Hay phải **tốn thời gian gửi email thủ công** để nhắc nhở, chuẩn bị tâm lý và tăng tỷ lệ xuất hiện? Workflow này sẽ **tự động hóa toàn bộ quy trình**, giúp bạn:
- **Tăng tỷ lệ xuất hiện cuộc gọi lên 30%** (so với không gửi email).
- **Tiết kiệm 10+ giờ/năm** không phải gửi email thủ công.
- **Chuẩn bị tâm lý khách hàng** trước cuộc gọi, giúp họ hiểu rõ mục đích cuộc trò chuyện.
- **Cá nhân hóa từng email** dựa trên thời gian còn lại trước cuộc hẹn.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tăng tỷ lệ xuất hiện cuộc gọi**: Email nhắc nhở tự động giúp khách hàng không quên hẹn.
✅ **Chuẩn bị tâm lý khách hàng**: Dãy email warming-up giúp họ hiểu rõ mục đích cuộc gọi (bán hàng, tư vấn, hợp tác).
✅ **Tiết kiệm thời gian**: Không phải gửi email thủ công, tự động hóa hoàn toàn.
✅ **Cá nhân hóa từng email**: Nội dung email thay đổi dựa trên thời gian còn lại trước cuộc hẹn.
✅ **Hoạt động 24/7**: Workflow chạy tự động ngay khi khách hàng đặt lịch trên Cal.com.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Cal.com** và **API Key** của Cal.com (để trigger khi khách hàng đặt lịch).
2. **Tài khoản Gmail** (đã kết nối OAuth 2.0) để gửi email tự động.
3. **Dãy email mẫu** (các sếp có thể chỉnh sửa nội dung trong node `Set`).
4. **Thời gian chờ mặc định** (có thể điều chỉnh trong node `Wait`).

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Tải file JSON từ [n8n.io/workflows/10795](https://n8n.io/workflows/10795).
2. Vào **n8n Editor** → Nhấn **"Import"** → Chọn file JSON.
3. **Hoặc** copy toàn bộ JSON và paste vào **"Import from JSON"** trong Editor.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
#### **A. Cấu hình Cal.com Trigger**
- **Node**: `Cal.com Trigger`
- **Thao tác**:
  - Vào **Credentials** → Thêm mới với tên `calApi`.
  - Nhập **API Key** của Cal.com (tìm trong **Settings → API** trên Cal.com).
  - Chọn **Event Type**: `Meeting Created` (hoặc tùy chỉnh theo nhu cầu).

#### **B. Cấu hình Gmail**
- **Node**: `Casual flex`, `Casual press`, `Casual knowledge flex`, `Quick prep`, `Send it`, v.v.
- **Thao tác**:
  - Vào **Credentials** → Thêm mới với tên `gmailOAuth2`.
  - Kết nối tài khoản Gmail (sẽ mở tab mới để xác thực OAuth 2.0).
  - Chọn **From Email**: Địa chỉ Gmail muốn gửi email (ví dụ: `sales@doanhnghiep.com`).

#### **C. Chỉnh sửa nội dung email**
- **Node**: `Quick prep email`, `Quick prep email2`, `Quick prep email (2)`
- **Thao tác**:
  - Mở node `Set` tương ứng → Chỉnh sửa **`emailContent`** để phù hợp với nội dung email của doanh nghiệp.
  - Ví dụ:
    ```json
    {
      "subject": "Chuẩn bị cho cuộc gọi hôm {{ $json["daysRemaining"] }} ngày nữa!",
      "html": "<p>Xin chào {{ $json["prospectName"] }},</p><p>Chúng tôi rất vui khi bạn đã đặt lịch hẹn với chúng tôi vào ngày {{ $json["meetingDate"] }}.</p><p>Để cuộc gọi hiệu quả hơn, hãy chuẩn bị...</p>"
    }
    ```
  - **Tham số động**:
    - `{{ $json["daysRemaining"] }}`: Số ngày còn lại trước cuộc hẹn.
    - `{{ $json["prospectName"] }}`: Tên khách hàng (trích xuất từ Cal.com).
    - `{{ $json["meetingDate"] }}`: Ngày giờ cuộc hẹn.

#### **D. Điều chỉnh thời gian chờ**
- **Node**: `Wait 1 Day`, `Wait another day`, `Wait another day 8+days`, v.v.
- **Thao tác**:
  - Mở node `Wait` → Chỉnh sửa **`time`** (ví dụ: `1d` = 1 ngày, `3d` = 3 ngày).
  - Ví dụ:
    - Email đầu tiên gửi **ngay sau khi đặt lịch**.
    - Email thứ 2 gửi **3 ngày trước cuộc hẹn**.
    - Email cuối gửi **1 ngày trước cuộc hẹn**.

#### **E. Cấu hình logic điều kiện**
- **Node**: `Switch: Days Until Meeting`
- **Thao tác**:
  - Mở node `Switch` → Chỉnh sửa **điều kiện** để phân loại khách hàng:
    - Nếu `daysRemaining <= 3` → Gửi email cuối cùng.
    - Nếu `daysRemaining > 3 && daysRemaining <= 8` → Gửi email trung gian.
    - Nếu `daysRemaining > 8` → Gửi email đầu tiên.

---

### **3. Kích hoạt ⚡️**
1. **Test run** với một cuộc hẹn mẫu:
   - Đặt một cuộc hẹn giả trên Cal.com.
   - Chạy workflow và kiểm tra email đã gửi không.
2. **Bật Active workflow**:
   - Nhấn **"Active"** ở góc trên bên phải của Editor.

---

## ✍️ **Mẹo & gợi ý nâng cao**
1. **Thêm Slack/Telegram Notifications**:
   - Sử dụng node `n8n-nodes-base.slack` hoặc `n8n-nodes-base.telegram` để thông báo khi khách hàng đặt lịch.
   - Ví dụ:
     ```json
     {
       "text": "📅 New meeting booked! 🚀\nName: {{ $json["prospectName"] }}\nDate: {{ $json["meetingDate"] }}"
     }
     ```

2. **Lưu log vào Google Sheets**:
   - Sử dụng node `n8n-nodes-base.googleSheets` để ghi lại lịch sử email đã gửi.
   - Cấu hình:
     - Sheet Name: `Meeting_Nurturing_Log`
     - Columns: `prospectName, meetingDate, emailSentAt, emailContent`

3. **Tùy chỉnh email theo loại cuộc hẹn**:
   - Sử dụng node `If` để phân loại cuộc hẹn (ví dụ: `Sales Call`, `Onboarding`, `Support`).
   - Gửi dãy email khác nhau cho từng loại.

4. **Gửi báo cáo định kỳ**:
   - Sử dụng node `n8n-nodes-base.cron` để gửi báo cáo tổng hợp về tỷ lệ xuất hiện cuộc gọi hàng tuần.

---

## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** để tự động hóa quy trình nurturing lead trước cuộc hẹn, giúp các sếp:
✔ **Tăng tỷ lệ xuất hiện cuộc gọi** lên 30%.
✔ **Tiết kiệm thời gian** không phải gửi email thủ công.
✔ **Chuẩn bị tâm lý khách hàng** trước cuộc gọi.

**Hành động ngay!**
1. Import workflow vào n8n.
2. Cấu hình Cal.com và Gmail.
3. Chỉnh sửa nội dung email phù hợp.
4. **Bật workflow và bắt đầu tự động hóa!**

---
**💡 Lưu ý cuối cùng**: Nếu gặp vấn đề, hãy kiểm tra **log của workflow** và **credentials** đã được cấu hình chính xác. Nếu cần hỗ trợ thêm, các sếp có thể tham khảo [n8n Community](https://community.n8n.io/) hoặc liên hệ với tác giả Maksudur Rahman.