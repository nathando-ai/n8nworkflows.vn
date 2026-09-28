---
title: "🚀 Tự Động Hóa Gửi Email & SMS Kết Quả Thí Sinh + Thông Báo Cho Người Giới Thiệu Với Airtable (N8N)"
description: "Workflow này tự động gửi email/SMS kết quả tham dự khóa học/thông tin cho thí sinh và thông báo cho người giới thiệu khi có sự kiện mới trong Airtable, tiết kiệm 10+ giờ công/năm cho các sếp quản lý tuyển sinh."
slug: "tieu-dong-hoa-gui-email-sms-ket-qua-thi-sinh-airtable"
tags: [n8n, automation, lead-nurturing, airtable, sendinblue, sms-automation]
keywords: [n8n workflow tự động hóa tuyển sinh, gửi email/SMS kết quả khóa học, thông báo người giới thiệu, Airtable + n8n, tự động hóa tuyển sinh không code]
---

# 🚀 **Tự Động Hóa Gửi Email & SMS Kết Quả Thí Sinh + Thông Báo Người Giới Thiệu Với Airtable**

### **Giải pháp hoàn hảo cho các sếp quản lý tuyển sinh, đào tạo, hoặc SaaS**
Hãy tưởng tượng một tình huống: Sau khi tổ chức khóa học hoặc buổi thông tin, các sếp phải **gửi email/SMS kết quả tham dự cho từng thí sinh**, đồng thời **thông báo cho người giới thiệu** khi họ hoàn thành hoặc bỏ cuộc. Nếu làm thủ công, việc này sẽ tốn **10+ giờ/năm** cho mỗi sếp, dễ gây lỗi và mất thời gian phản hồi. **Workflow này tự động hóa toàn bộ quy trình**, đảm bảo thông tin chính xác, cá nhân hóa và hoạt động liên tục 24/7.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động ổn định và không bị gián đoạn, các sếp nên **self-host n8n trên VPS** thay vì dùng phiên bản miễn phí (có giới hạn).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (phù hợp cho n8n + Airtable + Sendinblue)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Không cần gửi email/SMS thủ công sau mỗi khóa học.
✅ **Chính xác 100%**: Không bị quên hoặc sai thông tin do con người.
✅ **Cá nhân hóa**: Gửi nội dung khác nhau cho từng trường hợp (đã tham dự, bỏ cuộc, hoàn thành khóa học).
✅ **Thông báo tự động cho người giới thiệu**: Khi thí sinh hoàn thành hoặc bỏ cuộc, hệ thống tự động gửi thông báo cho người giới thiệu.
✅ **Hoạt động liên tục**: Không phụ thuộc vào giờ làm việc của nhân viên.
✅ **Dễ dàng mở rộng**: Thêm các thông báo mới hoặc tích hợp với Slack/Telegram mà không cần viết code.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Airtable**:
   - Một bảng dữ liệu chứa thông tin thí sinh (cần có các trường:
     - `Info Event Outcome` (đã tham dự/không tham dự)
     - `Course Outcome` (đã hoàn thành/đã bỏ cuộc)
     - Các trường `sent` (checkbox) để theo dõi trạng thái đã gửi email/SMS chưa.
   - **Cần thiết**: Các trường timestamp (`Info Outcome Updated At`, `Course Outcome Updated At`) để workflow được kích hoạt tự động.
   - **Mã API Airtable** (`airtableTokenApi`) để kết nối.

2. **Tài khoản Sendinblue (Brevo)**:
   - API Key (`sendInBlueApi`) để gửi email.
   - Danh sách email đã được cấu hình (nếu chưa có, cần tạo mới).

3. **Dịch vụ SMS (nếu muốn gửi SMS)**:
   - Nếu sử dụng `httpRequest` để gửi SMS (ví dụ: Twilio, MessageBird), cần cấu hình API Key và số điện thoại gửi.

4. **Thông tin cá nhân hóa**:
   - Danh sách người giới thiệu (email/điện thoại) trong Airtable.
   - Nội dung email/SMS mẫu (có thể chỉnh sửa trong nodes `sendInBlue` và `httpRequest`).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Tải file JSON từ [đây](https://n8n.io/workflows/13062) (hoặc copy toàn bộ JSON từ link trên).
2. Trong n8n Editor, nhấn **Import** và dán JSON vào.
3. Chọn **Create Workflow** và đặt tên (ví dụ: **"Automate Candidate Outcomes"**).

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này được thiết kế để **truyền thông tin từ Airtable** và **gửi email/SMS tự động**. Dưới đây là các bước cấu hình **quan trọng nhất**:

##### **A. Cấu hình Airtable**
1. **Kết nối Airtable**:
   - Trong node `Airtable Trigger`, chọn `airtableTokenApi` (đã cấu hình trước khi import).
   - Chọn bảng dữ liệu chứa thông tin thí sinh.
   - Cấu hình **trigger** cho hai trường:
     - `Info Outcome Updated At` (khi trạng thái buổi thông tin được cập nhật).
     - `Course Outcome Updated At` (khi trạng thái khóa học được cập nhật).

2. **Kiểm tra các trường trong Airtable**:
   - Các trường `sent` (checkbox) phải tồn tại và được đặt tên chính xác (ví dụ: `sentInfoEmail`, `sentCourseEmail`).
   - Các trường `eventType` (`info` hoặc `course`) phải được sử dụng để phân loại hành động.

##### **B. Cấu hình Email & SMS**
1. **Email (Sendinblue)**:
   - Trong các node `sendInBlue` (ví dụ: `Attended email`, `Did Not Attended email`), chọn `sendInBlueApi`.
   - **Chỉnh sửa nội dung email**:
     - Mở node `Attended email` và chỉnh sửa **template email** trong tab `Configuration`.
     - Sử dụng **dynamic content** để hiển thị tên thí sinh, ngày khóa học, và thông tin liên quan.
     - Ví dụ:
       ```html
       <p>Chào {{$json["firstName"]}},</p>
       <p>Chúng tôi rất vui khi biết bạn đã tham dự buổi thông tin về khóa học "{{$json["courseName"]}}" thành công!</p>
       ```
   - Lặp lại cho các node email khác (`Course outcome email`, `Brevo Email — Referrer Info Outcome`, `Did Not Attended email`).

2. **SMS (nếu sử dụng)**:
   - Trong node `Attended sms1` và `Did Not Attended sms`, cấu hình `httpRequest` để gửi SMS.
   - Cần thay đổi **URL API** và **headers** phù hợp với dịch vụ SMS của bạn (ví dụ: Twilio).
   - Ví dụ cấu hình Twilio:
     ```json
     {
       "method": "POST",
       "url": "https://api.twilio.com/2010-04-01/Accounts/{{TWILIO_ACCOUNT_SID}}/Messages.json",
       "headers": {
         "Authorization": "Basic {{TWILIO_API_KEY}}",
         "Content-Type": "application/x-www-form-urlencoded"
       },
       "body": {
         "To": "{{$json["phone"]}}",
         "From": "{{$json["twilioPhone"]}}",
         "Body": "Chào {{$json["firstName"]}}, bạn đã tham dự buổi thông tin thành công!"
       }
     }
     ```

##### **C. Cấu hình Logic & Switch**
1. **Node `Code — Normalize + Decide Action`**:
   - Đây là **cốt lõi logic** của workflow, quyết định hành động nào sẽ được thực hiện.
   - Các sếp **không cần chỉnh sửa mã** (nếu không muốn), nhưng có thể mở node này để hiểu logic:
     ```javascript
     // Dữ liệu đầu vào từ Airtable
     const data = $input.all();

     // Xác định loại sự kiện (info hoặc course)
     const eventType = data[0].fields.eventType;

     // Xác định trạng thái (attended, no-show, completed, withdrawn)
     const outcome = data[0].fields.outcome;

     // Xác định hành động cần thực hiện
     let action = "";
     if (eventType === "info") {
       if (outcome === "attended") action = "sendInfoAttended";
       else if (outcome === "no-show") action = "sendInfoNoShow";
     } else if (eventType === "course") {
       if (outcome === "completed") action = "sendCourseCompleted";
       else if (outcome === "withdrawn") action = "sendCourseWithdrawn";
     }

     // Trả về dữ liệu để Switch node xử lý
     return {
       json: {
         action: action,
         ...data[0].fields
       }
     };
     ```
   - **Không chỉnh sửa** nếu không hiểu code, để tránh lỗi.

2. **Node `Switch — Route Action`**:
   - Node này **chuyển hướng** đến các hành động cụ thể (gửi email/SMS) dựa trên kết quả từ Code node.
   - Các sếp **không cần chỉnh sửa** node này, nhưng có thể kiểm tra các branch:
     - `sendInfoAttended` → Gửi email/SMS cho thí sinh đã tham dự buổi thông tin.
     - `sendInfoNoShow` → Gửi email cho thí sinh không tham dự.
     - `sendCourseCompleted` → Gửi email cho thí sinh hoàn thành khóa học.
     - `sendCourseWithdrawn` → Gửi email cho thí sinh bỏ cuộc.

##### **D. Cập nhật Airtable sau khi gửi**
1. Các node `Airtable — Commit Post-Info Attended Sent`, `Airtable — Commit Referrer Notified`, v.v.:
   - **Cập nhật trạng thái `sent`** trong Airtable để tránh gửi lại email/SMS.
   - Ví dụ: Khi gửi email thành công, node này sẽ cập nhật trường `sentInfoEmail` thành `true`.
   - **Không cần chỉnh sửa** nếu cấu hình Airtable đúng.

---

#### **3. Kích hoạt ⚡️**
1. **Test run với dữ liệu mẫu**:
   - Trong Airtable, **cập nhật một bản ghi** (ví dụ: thay đổi `Info Outcome Updated At`).
   - Workflow sẽ tự động kích hoạt và gửi email/SMS.
   - Kiểm tra **log** trong n8n để xác nhận workflow hoạt động.

2. **Bật Active workflow**:
   - Sau khi test thành công, chuyển workflow từ **Draft** sang **Active**.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Thêm thông báo Slack/Telegram**:
   - Sử dụng node `n8n-nodes-base.slack` hoặc `n8n-nodes-base.telegram` để gửi thông báo khi có sự kiện mới.
   - Ví dụ: Khi thí sinh hoàn thành khóa học, gửi tin nhắn Slack cho team quản lý.

2. **Lưu log hoạt động**:
   - Thêm node `n8n-nodes-base.set` hoặc `n8n-nodes-base.airtable` để lưu lịch sử hoạt động vào Airtable.
   - Có thể tạo một bảng `Logs` để theo dõi tất cả các email/SMS đã gửi.

3. **Tích hợp với CRM**:
   - Nếu sử dụng HubSpot, Salesforce hoặc CRM khác, có thể thêm node `n8n-nodes-base.httpRequest` để cập nhật thông tin thí sinh vào CRM.

4. **Tự động gửi báo cáo định kỳ**:
   - Sử dụng **n8n Cron Trigger** để gửi báo cáo tổng hợp (ví dụ: số lượng thí sinh đã tham dự, hoàn thành khóa học) cho quản lý hàng tuần.

5. **Chỉnh sửa nội dung email/SMS**:
   - Mở các node `sendInBlue` và `httpRequest` để tùy chỉnh nội dung phù hợp với brand của doanh nghiệp.

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp quản lý tuyển sinh, đào tạo, hoặc SaaS khỏi công việc thủ công gửi email/SMS và thông báo cho người giới thiệu. **Với chỉ vài bước cấu hình**, các sếp có thể tự động hóa toàn bộ quy trình, **tăng cường trải nghiệm của thí sinh** và **cải thiện hiệu quả hoạt động**.

🚀 **Hành động ngay hôm nay**:
1. Import workflow vào n8n.
2. Cấu hình Airtable và Sendinblue.
3. Test với một bản ghi mẫu.
4. Bật workflow và **nhận kết quả ngay lập tức**!

**Nếu có vấn đề**, hãy để lại comment hoặc liên hệ với tác giả [Jasurbek](https://n8n.io/workflows/13062) để hỗ trợ. **Chúc các sếp thành công!** 💪