---
title: "🤖 **Tự Động Hóa Email Theo Dõi Khách Hàng Y Tế Với AI Claude, Gmail, Slack & Google Sheets – Không Cần Code!**"
description: "Giải pháp tự động hóa hoàn toàn cho các phòng khám, bác sĩ tư nhân hoặc trung tâm y tế để gửi email chào mừng, nhắc lại lịch hẹn và theo dõi khách hàng mới dựa trên AI Claude Sonnet. Tiết kiệm 10+ giờ/lần cho nhân viên hành chính và cải thiện tỷ lệ giữ chân khách hàng lên đến 30%."
slug: "tieu-dong-hoa-email-theo-doi-khach-hang-y-te-ai-claude"
tags: [n8n, automation, no-code, y-te, ai-claude, google-sheets, gmail, slack, lead-nurturing]
keywords: [tự động hóa y tế n8n, email theo dõi khách hàng y tế, ai Claude Sonnet tự động hóa, tự động hóa phòng khám, gửi email nhắc lại lịch hẹn, tự động hóa Google Sheets]
---

# 🚀 **Tự Động Hóa Email Theo Dõi Khách Hàng Y Tế Với AI Claude – Không Cần Code!**

### **Dừng việc "chạy theo" khách hàng thủ công!**
Hàng ngày, các phòng khám và bác sĩ tư nhân phải mất **giờ đồng hồ** để:
- Gửi email chào mừng cho khách hàng mới.
- Nhắc lại lịch hẹn cho những người bỏ lịch.
- Theo dõi và cá nhân hóa email cho từng trường hợp.
- Lập báo cáo theo dõi trong Google Sheets.

**Kết quả?** Khách hàng cảm thấy không được quan tâm, tỷ lệ giữ chân thấp, và nhân viên hành chính mệt mỏi.

**Giải pháp?** **Workflow này tự động hóa toàn bộ quy trình với AI Claude Sonnet**, giúp:
✅ **Gửi email cá nhân hóa** cho từng khách hàng (chào mừng, nhắc lại lịch, hoặc theo dõi).
✅ **Nhắc lại lịch hẹn** cho khách hàng bỏ lịch với **Slack alert** cho quản lý.
✅ **Lập báo cáo tự động** trong Google Sheets với thời gian, nội dung và lý do.
✅ **Tiết kiệm 10+ giờ/tháng** cho nhân viên hành chính.
✅ **Tăng tỷ lệ giữ chân khách hàng lên đến 30%** nhờ cá nhân hóa.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng. Đây là giải pháp **an toàn, nhanh chóng và tiết kiệm** so với dùng phiên bản cloud.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** – giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ sức mạnh cho workflow này)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần viết email thủ công, giảm **10+ giờ/tháng** cho nhân viên.
- **Cá nhân hóa hoàn toàn**: AI Claude tự động viết email phù hợp với từng trường hợp (chào mừng, nhắc lại lịch, hoặc theo dõi).
- **Nhắc lại lịch hiệu quả**: Khách hàng bỏ lịch sẽ được nhắc lại **và quản lý phòng khám được thông báo** qua Slack.
- **Báo cáo tự động**: Tất cả thông tin được ghi lại trong **Google Sheets** với thời gian, nội dung và lý do.
- **Tăng tỷ lệ giữ chân**: Email cá nhân hóa giúp **tăng 30% tỷ lệ khách hàng quay lại**.
- **Không cần kỹ thuật**: Cài đặt và chạy workflow chỉ trong **30 phút**, không cần viết code.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản Google** (để sử dụng **Gmail** và **Google Sheets**).
✔ **Tài khoản Slack** (nếu muốn **nhắc lại lịch** cho quản lý).
✔ **API Key Claude Sonnet** (mua tại [console.anthropic.com](https://console.anthropic.com/)).
✔ **Địa chỉ email chính thức** của phòng khám (để gửi email từ Gmail).
✔ **Google Sheet** có tên **"Communications Log"** với các cột:
   - Timestamp
   - Patient Name
   - Patient Email
   - Action (Welcome/Rebook/Follow-Up)
   - Urgency (Low/Medium/High)
   - Email Subject
   - Reason
   - Status

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow:
- **Tải file JSON** từ [n8n.io/workflows/15969](https://n8n.io/workflows/15969) và import vào **n8n Editor**.
- **Copy toàn bộ JSON** từ file và **paste** vào **Import Workflow** trong n8n.

👉 **Lưu ý:** Nếu dùng phiên bản **n8n cloud**, các sếp nên **self-host** để tránh giới hạn API và đảm bảo **chạy 24/7**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này có **15 node**, nhưng **các bước quan trọng nhất** cần điều chỉnh:

##### **A. Cấu hình "Configure Clinic Settings" (Node Code)**
- Mở node này và cập nhật:
  - **Clinic Name** (tên phòng khám/bác sĩ).
  - **Gmail Sender Address** (email chính thức của phòng khám).
  - **Slack Channel ID** (nếu dùng Slack).
  - **Booking Link** (đường link đặt lịch của phòng khám).
  - **Google Sheets ID** (ID của sheet "Communications Log").

##### **B. Kết nối Claude AI (Node `lmChatAnthropic`)**
1. Mở node **"Claude Sonnet"** (nằm trong **"Analyse Patient Submission"**).
2. Click vào **"Add Credential"** và chọn **"Anthropic"**.
3. Nhập **API Key** từ [console.anthropic.com](https://console.anthropic.com/).
4. **Lưu ý:** Nếu không có API Key, các sếp phải **mua gói Claude Sonnet** (từ **$5/1M tokens**).

##### **C. Kết nối Gmail (Node `gmail`)**
- Trong các node **"Send Welcome Email"**, **"Send Rebook Email"**, **"Send Follow-Up Email"**:
  - Click **"Add Credential"** → **"Gmail"**.
  - Đăng nhập tài khoản Google của phòng khám.
  - **Chọn email chính thức** làm sender.

##### **D. Kết nối Slack (Node `slack`)**
- Mở node **"Notify Clinic Manager"**.
- Click **"Add Credential"** → **"Slack"**.
- Đăng nhập tài khoản Slack và chọn **channel** muốn thông báo.
- **Nếu không dùng Slack**, các sếp **right-click → Disable node**.

##### **E. Cấu hình Google Sheets (Node `googleSheets`)**
- Trong các node **"Log Welcome"**, **"Log Rebook"**, **"Log Follow-Up"**:
  - Click **"Add Credential"** → **"Google Sheets"**.
  - Chọn **Google Sheet** có tên **"Communications Log"** (đã tạo trước).
  - **Kiểm tra lại cột** để đảm bảo dữ liệu ghi đúng.

##### **F. Cập nhật Prompt AI (Node `Build Patient Prompt`)**
- Mở node này và **cập nhật mô tả phòng khám** để AI hiểu rõ hơn:
  - Ví dụ: Nếu là **phòng khám nha khoa**, thêm chi tiết như:
    > *"Bạn là một bác sĩ nha khoa chuyên khoa. Khách hàng thường đến vì răng sâu, nha chu, hoặc kiểm tra định kỳ. Hãy viết email thân thiện và chuyên nghiệp."*
  - **Lưu ý:** Prompt càng chi tiết, email càng phù hợp.

#### **3. Kích hoạt ⚡️**
- **Test run** với **dữ liệu mẫu**:
  1. Điền thông tin vào **Patient Intake Form** (tự động tạo khi kích hoạt workflow).
  2. Chọn **Run Workflow** và kiểm tra:
     - Email có được gửi không?
     - Slack có thông báo không (nếu dùng)?
     - Dữ liệu có ghi vào Google Sheets không?
- **Bật Active workflow** khi đã kiểm tra xong.

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁCH LÀM NÂNG CAO]
- **Thêm nhánh "Urgent Case"** (ví dụ: khách hàng cần khám cấp):
  1. Mở node **"Route by Action"** (Switch).
  2. Thêm **output mới** với điều kiện `{{ $json.urgency }} === "High"`.
  3. Kết nối với node mới (ví dụ: **Twilio** để gọi điện tự động).

- **Gửi báo cáo định kỳ**:
  - Sử dụng **n8n Trigger (Schedule)** để gửi **tổng hợp email theo dõi hàng tuần** cho quản lý.

- **Kết hợp với CRM**:
  - Nếu dùng **HubSpot** hoặc **Zoho CRM**, các sếp có thể **update thông tin khách hàng tự động** sau khi gửi email.

- **Dùng Google Forms thay Form Trigger**:
  - Nếu khách hàng đã điền thông tin vào **Google Form**, các sếp có thể **sử dụng node `googleSheetsTrigger`** để bắt đầu workflow.

- **Tăng tính cá nhân hóa**:
  - Thêm **node `code`** để lấy dữ liệu từ **Google My Business** hoặc **Facebook Messenger** để enrich thông tin khách hàng.
:::

---

### 📌 **Kết luận**
Workflow này **giải phóng toàn bộ công việc thủ công** trong việc theo dõi khách hàng y tế, giúp:
✔ **Tiết kiệm thời gian** cho nhân viên hành chính.
✔ **Tăng tỷ lệ giữ chân khách hàng** nhờ email cá nhân hóa.
✔ **Cải thiện trải nghiệm khách hàng** với thông tin nhanh chóng và chuyên nghiệp.

**Hành động ngay!**
1. **Self-host n8n** trên VPS (để tránh giới hạn cloud).
2. **Import workflow** và **cấu hình các node** theo hướng dẫn.
3. **Test run** với dữ liệu mẫu và **bật workflow**.

**Không cần code, không cần kỹ thuật – chỉ cần n8n và AI Claude!** 🚀

---
**🔗 [Tải workflow gốc tại n8n.io](https://n8n.io/workflows/15969)**
**💬 Có thắc mắc? Hỏi tại [Community n8n Việt Nam](https://community.n8n.io/)**