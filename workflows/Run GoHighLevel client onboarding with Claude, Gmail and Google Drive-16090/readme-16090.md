---
title: "🚀 Tự Động Hóa Onboarding Khách Hàng GoHighLevel Với AI Claude, Gmail & Google Drive - Giảm 90% Công Việc Thủ Công"
description: "Workflow này tự động hóa toàn bộ quy trình onboarding khách hàng khi một giao dịch được đánh dấu 'Won' trên GoHighLevel, từ tạo kế hoạch cá nhân hóa cho khách hàng đến lập lịch cuộc gọi và gửi email chào mừng - chỉ trong 60 giây. Giúp các sếp tiết kiệm thời gian, giảm sai sót và nâng cao trải nghiệm khách hàng."
slug: "tieu-dong-hoa-onboarding-ghl-ai-claude-gmail-google-drive"
tags: [n8n, automation, crm, ai-chatbot, gohighlevel, google-drive, gmail, slack, google-sheets]
keywords: [tự động hóa onboarding, n8n workflow, ai claude sonnet, gohighlevel automation, tự động hóa crm, google drive api, gmail automation]
---

# 🚀 **Tự Động Hóa Onboarding Khách Hàng GoHighLevel Với AI Claude, Gmail & Google Drive**

### **Giải pháp hoàn hảo cho các sếp muốn loại bỏ công việc thủ công trong onboarding khách hàng**

Hãy tưởng tượng một tình huống: Một khách hàng mới vừa ký hợp đồng với doanh nghiệp của các sếp. Thay vì phải viết email chào mừng, lập kế hoạch onboarding, tạo nhiệm vụ trong GoHighLevel và lập lịch cuộc gọi một cách thủ công, **tất cả những việc này sẽ tự động hoàn thành chỉ trong 60 giây** khi một giao dịch được đánh dấu "Won" trên GoHighLevel.

Workflow này không chỉ tiết kiệm thời gian mà còn **cung cấp trải nghiệm cá nhân hóa cao nhất** cho khách hàng, đồng thời giúp đội ngũ của các sếp **không bao giờ quên một nhiệm vụ nào** trong quá trình onboarding. Dưới đây là hướng dẫn chi tiết để các sếp triển khai workflow này và tự động hóa toàn bộ quy trình onboarding một cách chuyên nghiệp.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động 24/7 mà không gặp lỗi, các sếp nên cài đặt n8n trên **VPS riêng** (Self-hosted) để đảm bảo tính ổn định và bảo mật cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Onboarding một khách hàng chỉ mất **60 giây** thay vì 1-2 giờ thủ công.
- **Cá nhân hóa hoàn toàn**: Email chào mừng và kế hoạch onboarding được tạo dựa trên **loại dịch vụ, giá trị giao dịch và ghi chú đặc biệt** của khách hàng.
- **Không quên nhiệm vụ**: Tất cả **6 nhiệm vụ onboarding** được tự động tạo trong GoHighLevel với ngày hạn chặt chẽ.
- **Lập lịch tự động**: Cuộc gọi kickoff được lập lịch **2 ngày làm việc sau** khi khách hàng được onboarding.
- **Đội ngũ được thông báo kịp thời**: Slack alert giúp toàn bộ đội ngũ **biết ngay khi có khách hàng mới** và biết những nhiệm vụ cần làm.
- **Dữ liệu được theo dõi**: Tất cả thông tin onboarding được **ghi chép vào Google Sheets** để theo dõi và báo cáo.
- **Khách hàng được quản lý chuyên nghiệp**: Mỗi khách hàng sẽ có **thư mục riêng trên Google Drive** chứa tất cả tài liệu liên quan.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi triển khai workflow, các sếp cần chuẩn bị:
1. **Tài khoản GoHighLevel** (để kích hoạt webhook khi giao dịch được đánh dấu "Won").
2. **API Key của GoHighLevel** (để tạo nhiệm vụ và cập nhật thông tin khách hàng).
3. **Tài khoản Gmail** (để gửi email chào mừng tự động).
4. **Tài khoản Google Drive** (để tạo thư mục cho mỗi khách hàng).
5. **Tài khoản Google Calendar** (để lập lịch cuộc gọi kickoff).
6. **Tài khoản Slack** (tùy chọn, để thông báo cho đội ngũ).
7. **Tài khoản Google Sheets** (để ghi chép log onboarding).
8. **Anthropic API Key** (để sử dụng Claude Sonnet AI).
9. **Thông tin cấu hình cơ bản**:
   - Tên công ty.
   - ID Location của GoHighLevel.
   - Tên và ID người quản lý tài khoản.
   - ID kênh Slack (nếu sử dụng).
   - ID thư mục cha trên Google Drive.
   - Link đặt lịch (nếu có).
   - ID sheet log onboarding.

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Mở **n8n Editor** trên trang web hoặc máy chủ self-hosted.
2. Nhấp vào **"Import"** và chọn file JSON đã tải xuống từ [link gốc](https://n8n.io/workflows/16090).
   **Hoặc** copy toàn bộ JSON từ [đây](https://n8n.io/workflows/16090) và paste vào **"Import from JSON"** trong n8n Editor.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **13 node** quan trọng, các sếp cần cấu hình kỹ lưỡng như sau:

##### **A. Node "Receive GHL Won Deal" (Webhook)**
- **Cấu hình webhook trên GoHighLevel**:
  - Đi đến **Settings → Integrations → Webhooks** trên GoHighLevel.
  - Tạo một webhook mới với **Trigger: Opportunity Stage Changed**.
  - Chọn **Stage: Won** (hoặc tùy chỉnh theo yêu cầu).
  - Dán **URL từ node Webhook** trong n8n vào trường **Webhook URL** của GoHighLevel.
  - **Kích hoạt webhook** trước khi kích hoạt workflow.

##### **B. Node "Configure Settings" (Code)**
- Mở node này và cập nhật các thông tin sau:
  ```json
  {
    "agencyName": "Tên Công Ty Của Các Sếp",
    "ghlApiKey": "API_KEY_GHL",
    "ghlLocationId": "LOCATION_ID_GHL",
    "accountManagerName": "Tên Người Quản Lý",
    "accountManagerId": "ID_NGƯỜI_QUẢN_LÝ",
    "slackChannelId": "CHANNEL_ID_SLACK", // Nếu không dùng Slack, để trống
    "googleCalendarId": "CALENDAR_ID_GOOGLE",
    "googleDriveParentFolderId": "PARENT_FOLDER_ID_DRIVE",
    "bookingLink": "LINK_DẶT_LỊCH", // Nếu có
    "logSheetId": "SHEET_ID_LOG_ONBOARDING"
  }
  ```
  - Các sếp cần **trích xuất `ghlLocationId`, `accountManagerId`** từ GoHighLevel và **`googleDriveParentFolderId`** từ Google Drive.

##### **C. Node "Generate Onboarding Plan" (ChainLlm + Claude Sonnet)**
- **Cấu hình Claude Sonnet**:
  1. Mở node **"Claude Sonnet"** bên trong **"Generate Onboarding Plan"**.
  2. Tạo **một credential mới** cho Anthropic bằng cách:
     - Đăng nhập vào [console.anthropic.com](https://console.anthropic.com/).
     - Tạo **API Key** và copy vào n8n.
  3. **Cập nhật Prompt** trong node **"Generate Onboarding Plan"** để phù hợp với dịch vụ của các sếp. Ví dụ:
     ```json
     "prompt": "Tôi là một chuyên gia onboarding cho công ty {{agencyName}}. Khách hàng mới đã mua dịch vụ {{serviceType}} với giá trị giao dịch {{dealValue}}. Ghi chú của khách hàng là: {{dealNotes}}.
     Hãy tạo:
     1. Một email chào mừng cá nhân hóa, giới thiệu dịch vụ và kế hoạch onboarding.
     2. Một danh sách 6 nhiệm vụ onboarding cụ thể cho dịch vụ này, với ngày hạn phù hợp trong 30 ngày đầu tiên.
     3. Một tóm tắt ngắn gọn cho Slack, bao gồm tên khách hàng, dịch vụ, giá trị giao dịch và 3 nhiệm vụ đầu tiên.
     Đảm bảo nội dung chuyên nghiệp, thân thiện và rõ ràng."
     ```

##### **D. Node "Create Task in GHL" (HTTP Request)**
- Node này sẽ tự động tạo **6 nhiệm vụ** trong GoHighLevel dựa trên kế hoạch từ Claude.
- **Không cần chỉnh sửa** nếu các sếp đã cấu hình GoHighLevel API Key chính xác.

##### **E. Node "Create Client Folder" (Google Drive)**
- Node này sẽ tạo **thư mục mới** trên Google Drive cho mỗi khách hàng.
- **Không cần chỉnh sửa** nếu đã cấu hình Google Drive credential.

##### **F. Node "Send Welcome Email" (Gmail)**
- **Cấu hình Gmail**:
  - Đăng nhập vào tài khoản Gmail và cho phép n8n truy cập.
  - Đảm bảo **email từ Gmail** được cấu hình với **tên người gửi** và **địa chỉ email** phù hợp.

##### **G. Node "Schedule Kickoff Call" (Google Calendar)**
- **Cấu hình Google Calendar**:
  - Đăng nhập vào tài khoản Google và cho phép n8n truy cập.
  - Node này sẽ tự động lập lịch cuộc gọi **2 ngày làm việc sau** khi khách hàng được onboarding.

##### **H. Node "Notify Team - New Client" (Slack)**
- **Cấu hình Slack** (tùy chọn):
  - Nếu không muốn sử dụng Slack, các sếp có thể **tắt node này** bằng cách nhấp chuột phải → **Disable**.
  - Nếu sử dụng, đăng nhập vào Slack và chọn **kênh phù hợp**.

##### **I. Node "Log Onboarding" (Google Sheets)**
- **Cấu hình Google Sheets**:
  - Tạo một **sheet mới** với tên **"Onboarding Log"** và các cột sau:
    | Timestamp | Client Name | Client Email | Company | Service | Deal Value | Tasks Created | Drive Link | Kickoff Date | Status |
  - Đăng nhập vào Google Sheets và cho phép n8n truy cập.

---

#### **3. Kích hoạt ⚡️**
1. **Test run với dữ liệu mẫu**:
   - Tạo một **giao dịch mẫu** trên GoHighLevel và đánh dấu nó là **"Won"**.
   - Kiểm tra email chào mừng, nhiệm vụ trong GoHighLevel, và thông báo Slack (nếu có).
2. **Bật Active workflow**:
   - Sau khi kiểm tra thành công, các sếp có thể **bật workflow** để nó hoạt động 24/7.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tùy chỉnh Prompt cho Claude**:
   - Nếu các sếp có **nhiều loại dịch vụ khác nhau**, hãy **cập nhật Prompt** để Claude tạo kế hoạch phù hợp với từng dịch vụ.
   - Ví dụ: Nếu có dịch vụ "Website Design", "SEO", "Marketing Digital", hãy liệt kê rõ trong Prompt để Claude hiểu rõ hơn.

2. **Thêm báo cáo định kỳ**:
   - Sử dụng **Google Sheets** để tạo **báo cáo tổng hợp** về số lượng khách hàng onboarding, tỷ lệ hoàn thành nhiệm vụ, và thời gian trung bình onboarding.

3. **Kết hợp với Zapier/Integromat**:
   - Nếu cần **thông báo thêm** (ví dụ: gửi tin nhắn qua Telegram), các sếp có thể kết nối với **Zapier** hoặc **Integromat** từ node Slack.

4. **Lưu log chi tiết**:
   - Các sếp có thể **thêm node Log** để ghi lại **tất cả hoạt động** của workflow vào Google Sheets hoặc một cơ sở dữ liệu khác.

5. **Tạo kế hoạch 30-60-90 ngày cho khách hàng VIP**:
   - Đối với khách hàng có **giá trị giao dịch cao**, các sếp có thể **thêm một node Claude thứ hai** để tạo kế hoạch dài hạn (30-60-90 ngày).

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** để các sếp **tự động hóa toàn bộ quy trình onboarding** trên GoHighLevel, từ tạo kế hoạch cá nhân hóa cho khách hàng đến lập lịch cuộc gọi và gửi email chào mừng. **Không cần viết code, không cần thủ công** - chỉ cần **cấu hình và kích hoạt**, workflow sẽ hoạt động tự động 24/7.

**Hành động ngay hôm nay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test với một giao dịch mẫu** để đảm bảo mọi thứ hoạt động.
3. **Bật workflow** và **giải phóng thời gian** cho đội ngũ của các sếp!

**🚀 Cùng tự động hóa onboarding và nâng cao hiệu suất kinh doanh ngay bây giờ!**