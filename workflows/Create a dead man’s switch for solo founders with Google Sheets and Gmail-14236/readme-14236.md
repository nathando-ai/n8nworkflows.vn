---
title: "🚨 Dead Man’s Switch Tự Động Hóa cho Founder Solo: Bảo Vệ An Toàn 24/7 Với Google Sheets & Gmail"
description: "Workflow tự động hóa an toàn cá nhân cho founder solo, freelancer hoặc doanh nghiệp 1 người. Nếu bạn không check-in trong thời gian quy định, hệ thống sẽ tự động gửi cảnh báo đến người liên lạc khẩn cấp qua email và ghi log chi tiết vào Google Sheets."
slug: "dead-mans-switch-tu-dong-hoa-cho-founder"
tags: [n8n, automation, personal-productivity, google-sheets, gmail, safety-automation, solo-founder]
keywords: [n8n workflow an toàn cá nhân, tự động hóa dead man switch, cảnh báo khẩn cấp tự động, google sheets + gmail, tự động hóa cho founder solo]
---

# 🚨 Dead Man’s Switch Tự Động Hóa: Bảo Vệ An Toàn Cho Founder Solo

## 🔥 Nỗi Đau Của Các Sếp
Làm founder solo hay freelancer, việc quản lý thời gian và an toàn cá nhân thường bị bỏ qua trong bối cảnh công việc căng thẳng. Bạn có bao giờ lo lắng về việc không thể liên lạc được với mình trong trường hợp bất ngờ? Hoặc không biết cách thông báo cho người thân/đối tác khi bị ốm hoặc gặp vấn đề? **Dead Man’s Switch** là giải pháp tự động hóa hoàn hảo để giải quyết vấn đề này.

Với workflow này, các sếp sẽ:
- **Không cần code** để thiết lập hệ thống cảnh báo tự động.
- **Yên tâm** khi biết rằng nếu không check-in trong thời gian quy định, hệ thống sẽ tự động gửi cảnh báo đến người liên lạc khẩn cấp.
- **Ghi log toàn bộ hoạt động** vào Google Sheets để theo dõi và phân tích sau này.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa an toàn cá nhân**: Không cần nhớ check-in thủ công hàng ngày.
- **Cảnh báo cấp độ**: Gửi email nhắc nhở khi quá thời gian quy định, và cảnh báo khẩn cấp nếu không check-in trong thời gian dài.
- **Ghi log toàn bộ hoạt động**: Tất cả cảnh báo và check-in được ghi lại chi tiết trong Google Sheets.
- **Không cần kỹ thuật**: Cài đặt và sử dụng chỉ trong vài phút.
- **Thông báo đa cấp**: Cảnh báo đến người liên lạc khẩn cấp nếu không có phản hồi trong thời gian quy định.
:::

---

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Các sếp cần chuẩn bị:
1. **Tài khoản Google** (để sử dụng Google Sheets và Gmail).
2. **Google Sheets** với hai tab:
   - **CheckIns**: Có các cột: `timestamp`, `source`, `founder_name`, `founder_email`, `emergency_contact_1`, `emergency_contact_2`, `emergency_message`, `threshold_hours`.
   - **AlertLog**: Có các cột: `timestamp`, `status`, `hours_since_checkin`.
3. **Tài khoản Gmail** để gửi cảnh báo và thông báo.
4. **VPS hoặc n8n Cloud** để chạy workflow 24/7.
5. **API Keys và Credentials**:
   - **Google Sheets OAuth2 API Key**.
   - **Gmail OAuth2 Credentials**.
:::

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào n8n Editor:
1. Tải file JSON từ [n8n.io/workflows/14236](https://n8n.io/workflows/14236).
2. Mở n8n Editor và chọn **Import Workflow** từ menu.
3. Chọn file JSON đã tải và nhấn **Import**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình các node quan trọng như sau:

##### **a. Cấu hình Google Sheets**
- **Node "Read Check-in Log"**:
  - Điền **Google Sheets URL** vào trường `Sheet URL`.
  - Chọn **tab "CheckIns"** trong `Sheet Name`.
  - Chọn `credentials`: `googleSheetsOAuth2Api`.

- **Node "Record Check-in"**:
  - Điền **Google Sheets URL** vào trường `Sheet URL`.
  - Chọn **tab "CheckIns"** trong `Sheet Name`.
  - Chọn `credentials`: `googleSheetsOAuth2Api`.
  - Đảm bảo `operation` là `append`.

- **Node "Log Alert to Sheet"**:
  - Điền **Google Sheets URL** vào trường `Sheet URL`.
  - Chọn **tab "AlertLog"** trong `Sheet Name`.
  - Chọn `credentials`: `googleSheetsOAuth2Api`.
  - Đảm bảo `operation` là `append`.

##### **b. Cấu hình Gmail**
- **Node "Send Reminder to Founder"**:
  - Chọn `credentials`: `gmailOAuth2`.
  - Điền địa chỉ email của founder vào trường `To`.
  - Tùy chỉnh nội dung email trong `Subject` và `Body`.

- **Node "Alert Emergency Contact 1" và "Alert Emergency Contact 2"**:
  - Chọn `credentials`: `gmailOAuth2`.
  - Điền địa chỉ email của người liên lạc khẩn cấp vào trường `To`.
  - Tùy chỉnh nội dung email trong `Subject` và `Body`.

##### **c. Cấu hình Webhook**
- **Node "Check-in Webhook"**:
  - Đảm bảo `path` là `dead-mans-switch-checkin`.
  - Sau khi import, copy URL webhook từ node này và **bookmark** nó để check-in hàng ngày.

##### **d. Cấu hình Schedule Trigger**
- **Node "Daily Check (9 AM)"**:
  - Đảm bảo `schedule` được thiết lập để chạy hàng ngày lúc 9 AM.

##### **e. Cấu hình Code Node**
- **Node "Calculate Hours Since Last Check-in"**:
  - Các sếp không cần chỉnh sửa mã nguồn, nhưng có thể kiểm tra lại logic tính toán thời gian nếu cần.

##### **f. Cấu hình Sticky Note**
- **Node "StickyNote"**:
  - Các sếp có thể sử dụng sticky note để ghi chú các thông tin quan trọng như địa chỉ email của người liên lạc khẩn cấp hoặc thông điệp khẩn cấp.

#### 3. Kích hoạt ⚡️
1. **Test Run**:
   - Chạy workflow với dữ liệu mẫu để kiểm tra tính năng.
   - Đảm bảo các email cảnh báo và ghi log vào Google Sheets hoạt động chính xác.

2. **Bật Active Workflow**:
   - Sau khi kiểm tra xong, chuyển trạng thái workflow từ `Inactive` sang `Active`.

---

### ✍️ Mẹo & gợi ý nâng cao
:::tip[Mẹo nâng cao]
1. **Thêm thông báo qua Slack/Telegram**:
   - Sử dụng node **Slack** hoặc **Telegram Bot** để gửi cảnh báo đến nhóm chat hoặc cá nhân.

2. **Tự động gửi báo cáo định kỳ**:
   - Sử dụng node **Schedule Trigger** để gửi báo cáo tổng hợp về check-in và cảnh báo hàng tuần qua email.

3. **Tăng cường tính bảo mật**:
   - Sử dụng **Google Sheets API** với quyền hạn tối thiểu để giảm thiểu rủi ro.

4. **Tùy chỉnh thông điệp cảnh báo**:
   - Thay đổi nội dung email trong các node Gmail để phù hợp với tình huống cụ thể (ví dụ: thông báo khẩn cấp, nhắc nhở nhẹ nhàng).

5. **Lưu log chi tiết hơn**:
   - Thêm các cột như `location` hoặc `device` vào tab **CheckIns** để ghi lại thông tin check-in chi tiết hơn.
:::

---

### 📌 Kết luận
Dead Man’s Switch là giải pháp tự động hóa an toàn cá nhân hoàn hảo cho founder solo, freelancer hoặc doanh nghiệp 1 người. Với workflow này, các sếp không chỉ tiết kiệm thời gian mà còn yên tâm về an toàn cá nhân. **Hãy áp dụng ngay và bảo vệ bản thân mình trong mọi tình huống!**

👉 [Tải workflow ngay tại đây](https://n8n.io/workflows/14236) và bắt đầu tự động hóa an toàn cá nhân của mình!

---