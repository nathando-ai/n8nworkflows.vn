---
title: "📊 **Tự Động Hóa Báo Cáo Google Analytics Hàng Ngày Với Tóm Tắt AI GPT-4 Mini, Thông Báo WhatsApp & Nhiệm Vụ ClickUp**"
description: "Workflow này tự động thu thập, phân tích và báo cáo dữ liệu Google Analytics hàng ngày, so sánh với ngày hôm trước, tạo tóm tắt thông minh bằng AI, gửi thông báo tức thời qua WhatsApp và email, đồng thời tạo nhiệm vụ trên ClickUp để các sếp marketing và team hoạt động nhanh chóng và chính xác 100% không cần code."
slug: "tieu-dong-hoa-bao-cao-google-analytics-ai-whatsapp-clickup"
tags: [n8n, automation, google-analytics, ai-summarization, marketing-automation, no-code, workflow-tieng-viet]
keywords: [n8n workflow google analytics, tự động hóa báo cáo web, tóm tắt AI GPT-4, thông báo WhatsApp tự động, nhiệm vụ ClickUp tự động, phân tích traffic hàng ngày]
---

# 🚀 **Tự Động Hóa Báo Cáo Google Analytics Hàng Ngày Với AI GPT-4 Mini, Thông Báo WhatsApp & Nhiệm Vụ ClickUp**

### **🔥 Nỗi Đau Của Các Sếp Marketing & Team**
Hàng ngày, các sếp marketing và team phải:
- **Làm thủ công** thu thập báo cáo Google Analytics từ ngày hôm trước và ngày hiện tại.
- **So sánh dữ liệu** để phát hiện xu hướng tăng/giảm traffic, nhưng phải tính toán thủ công phần trăm thay đổi.
- **Tóm tắt báo cáo** bằng cách đọc dữ liệu khô và viết thành văn bản, mất thời gian và dễ sai sót.
- **Gửi thông báo** cho team qua email hoặc WhatsApp, nhưng thường bị quên hoặc trễ.
- **Quên theo dõi lịch sử** traffic, dẫn đến khó phát hiện xu hướng dài hạn.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách tự động hóa toàn bộ quy trình!**

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 3+ giờ/ngày** không phải thu thập và phân tích báo cáo thủ công.
✅ **Dữ liệu chính xác 100%** với tính toán tự động phần trăm thay đổi và xử lý trường hợp traffic thấp.
✅ **Tóm tắt thông minh** bằng AI GPT-4 Mini, giúp các sếp hiểu nhanh xu hướng chính.
✅ **Thông báo tức thời** qua WhatsApp và email, đảm bảo team không bỏ lỡ bất kỳ thay đổi nào.
✅ **Lưu lịch sử traffic** trên Google Sheets, giúp phân tích xu hướng dài hạn.
✅ **Tạo nhiệm vụ tự động** trên ClickUp khi có sự thay đổi đáng kể (tăng/giảm traffic).
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Analytics** (và **API Key OAuth2**) để lấy dữ liệu traffic.
2. **Tài khoản Google Sheets** (và **API Key OAuth2**) để lưu log traffic.
3. **Tài khoản OpenAI** (và **API Key**) để sử dụng GPT-4 Mini tóm tắt báo cáo.
4. **Tài khoản WhatsApp Business API** (cần đăng ký từ Meta) để gửi thông báo.
5. **Tài khoản ClickUp** (và **API Key OAuth2**) để tạo nhiệm vụ tự động.
6. **Tài khoản Email SMTP** (hoặc Gmail) để gửi email thông báo.
7. **Bảng Google Sheets** đã chuẩn bị sẵn với các sheet:
   - `High Traffic Sheet` (lưu traffic tăng).
   - `Less Traffic Sheet` (lưu traffic giảm).
   - `Daily Traffic Sheet` (lưu tất cả dữ liệu hàng ngày).
:::

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/11786](https://n8n.io/workflows/11786) và import vào n8n Editor.
- **Cách 2:** Copy toàn bộ JSON từ link trên và dán vào **Import Workflow** trong n8n.
- **Cách 3:** Tạo workflow mới và sao chép từng node theo danh sách dưới đây.

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **19 node** với các bước chính sau. Dưới đây là hướng dẫn chi tiết để cấu hình:

#### **🔹 Node 1: Schedule Trigger (Khởi động hàng ngày)**
- **Cấu hình:**
  - Chọn **Cron Expression**: `0 0 * * *` (khởi động lúc 00:00 hàng ngày).
  - **Lưu ý:** Đảm bảo workflow được chạy trên **n8n Self-hosted** (VPS) để hoạt động 24/7.

#### **🔹 Node 2-3: "Today's Report" & "Yesterday's Report" (Lấy dữ liệu Google Analytics)**
- **Cấu hình:**
  - Chọn **Google Analytics OAuth2 Credentials** đã thiết lập trước.
  - **Parameters:**
    - **View ID**: ID View của tài khoản Google Analytics.
    - **Metrics**: Chọn `users`, `sessions`, `pageViews`, `sessionPerPage`.
    - **Dimensions**: Chọn `date`.
    - **Date Range**:
      - **Today's Report**: `TODAY` (ngày hiện tại).
      - **Yesterday's Report**: `YESTERDAY` (ngày hôm qua).
  - **Lưu ý:** Đảm bảo **Google Analytics API** đã được kích hoạt và có quyền truy cập đầy đủ.

#### **🔹 Node 4: Calculator (Tính toán số liệu)**
- **Cấu hình:**
  - Node này tự động tính toán phần trăm thay đổi giữa ngày hôm qua và ngày hôm nay.
  - **Không cần chỉnh sửa** nếu đã import file JSON.

#### **🔹 Node 5: "Combine Today & Yesterday" (Gộp dữ liệu)**
- **Cấu hình:**
  - Node **Merge** này kết hợp dữ liệu từ ngày hôm qua và ngày hôm nay thành một stream duy nhất.
  - **Không cần chỉnh sửa** nếu import file JSON.

#### **🔹 Node 6-9: "Normalize & Convert Types" (Chuyển đổi dữ liệu)**
- **Cấu hình:**
  - Các node **Code** này chuyển đổi dữ liệu từ định dạng G4 của Google Analytics thành định dạng dễ đọc (YYYY-MM-DD) và đảm bảo tất cả các metric là số.
  - **Lưu ý:** Nếu import file JSON, các node này đã được cấu hình sẵn. Nếu tạo mới, cần viết code như sau:
    ```javascript
    // Ví dụ cho node "Normalize & Convert Types":
    return [
      {
        json: {
          date: $input.all()[0].json.date,
          users: parseInt($input.all()[0].json.users),
          sessions: parseInt($input.all()[0].json.sessions),
          pageViews: parseInt($input.all()[0].json.pageViews),
          sessionPerPage: parseFloat($input.all()[0].json.sessionPerPage),
          percentChangeUsers: parseFloat($input.all()[0].json.percentChangeUsers),
          percentChangeSessions: parseFloat($input.all()[0].json.percentChangeSessions),
          percentChangePageViews: parseFloat($input.all()[0].json.percentChangePageViews),
        },
      },
    ];
    ```

#### **🔹 Node 10: "Generate AI Summary" (Tóm tắt bằng GPT-4 Mini)**
- **Cấu hình:**
  - Chọn **OpenAI API Credentials** đã thiết lập.
  - **Parameters:**
    - **Model**: `gpt-4-1106-preview` (hoặc `gpt-4-mini` nếu có).
    - **Prompt**: Cần chỉnh sửa để phù hợp với yêu cầu của team. Ví dụ:
      ```
      Tóm tắt báo cáo traffic của ngày {date} so với ngày {yesterdayDate}:
      - Traffic người dùng: {users} ({percentChangeUsers}% so với ngày hôm qua).
      - Session: {sessions} ({percentChangeSessions}% so với ngày hôm qua).
      - Page Views: {pageViews} ({percentChangePageViews}% so với ngày hôm qua).
      Hãy viết một tóm tắt ngắn gọn (3-4 câu) về xu hướng traffic và đề xuất hành động nếu có.
      ```
  - **Lưu ý:** Đảm bảo **API Key OpenAI** có đủ credit để chạy.

#### **🔹 Node 11: "Format Message for WhatsApp / Email" (Định dạng thông báo)**
- **Cấu hình:**
  - Node **Set** này định dạng lại dữ liệu từ AI thành văn bản phù hợp với WhatsApp và email.
  - **Không cần chỉnh sửa** nếu import file JSON.

#### **🔹 Node 12: "Send message" (Gửi thông báo WhatsApp)**
- **Cấu hình:**
  - Chọn **WhatsApp Credentials** đã thiết lập (API từ Meta).
  - **Parameters:**
    - **Phone Number**: Số điện thoại của team (định dạng quốc tế, ví dụ: `+84123456789`).
    - **Message**: Dữ liệu đã định dạng từ node trước.
  - **Lưu ý:**
    - Cần đăng ký **WhatsApp Business API** từ Meta và kích hoạt cho số điện thoại.
    - Nếu không muốn gửi WhatsApp, có thể bỏ qua node này và chuyển dữ liệu sang email.

#### **🔹 Node 13: "If" (Kiểm tra traffic tăng/giảm)**
- **Cấu hình:**
  - Node **If** này kiểm tra nếu traffic ngày hôm nay **thấp hơn** ngày hôm qua.
  - **Condition:**
    - `{{ $json.percentChangeUsers }} < 0` (nếu phần trăm thay đổi người dùng < 0).
  - **Lưu ý:** Nếu traffic tăng, workflow sẽ bỏ qua nhánh này và chuyển sang nhánh khác.

#### **🔹 Node 14-15: "Send email to dedicated person" & "Send email to marketing team"**
- **Cấu hình:**
  - Chọn **SMTP Credentials** (hoặc Gmail) đã thiết lập.
  - **Parameters:**
    - **To**: Địa chỉ email của người nhận (ví dụ: `team@doanhnghiep.com`).
    - **Subject**: `🚨 Traffic giảm so với ngày hôm qua!` (hoặc tùy chỉnh).
    - **Body**: Nội dung từ node "Format Message for WhatsApp / Email".
  - **Lưu ý:**
    - Nếu traffic tăng, workflow sẽ gửi email khác với nội dung khen ngợi.
    - Có thể chỉnh sửa nội dung email theo yêu cầu.

#### **🔹 Node 16-18: "Add log to High Traffic Sheet" & "Add log to Less Traffic"**
- **Cấu hình:**
  - Chọn **Google Sheets Credentials** đã thiết lập.
  - **Parameters:**
    - **Sheet Name**:
      - `High Traffic Sheet` (nếu traffic tăng).
      - `Less Traffic Sheet` (nếu traffic giảm).
    - **Row**: Dữ liệu từ node trước (date, users, sessions, percentChange,...).
  - **Lưu ý:** Đảm bảo các sheet đã được tạo sẵn trong Google Sheets.

#### **🔹 Node 19: "Create a task" (Tạo nhiệm vụ ClickUp)**
- **Cấu hình:**
  - Chọn **ClickUp OAuth2 Credentials** đã thiết lập.
  - **Parameters:**
    - **Space ID**: ID của Space trong ClickUp.
    - **List ID**: ID của List (ví dụ: "Traffic Alerts").
    - **Task Name**: `📉 Traffic giảm! Kiểm tra nguyên nhân` (hoặc tùy chỉnh).
    - **Description**: Nội dung từ node "Format Message for WhatsApp / Email".
    - **Assignee**: ID của thành viên cần xử lý (nếu có).
  - **Lưu ý:** Node này chỉ chạy khi traffic giảm. Nếu traffic tăng, có thể bỏ qua hoặc tạo nhiệm vụ khác.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram Bot** để gửi thông báo tức thời cho team.
   - Ví dụ: Sử dụng node `n8n-nodes-base.slack` hoặc `n8n-nodes-base.telegram`.

2. **Lưu log chi tiết hơn**:
   - Thêm node **Google Sheets** để lưu tất cả dữ liệu chi tiết (không chỉ traffic tăng/giảm) vào một sheet riêng.

3. **Gửi báo cáo định kỳ**:
   - Sử dụng node **Schedule Trigger** khác để gửi báo cáo tuần/monthly qua email hoặc WhatsApp.

4. **Tùy chỉnh AI Prompt**:
   - Chỉnh sửa prompt của GPT-4 Mini để phù hợp với ngành nghề cụ thể (ví dụ: e-commerce, blogging, SaaS).

5. **Xử lý lỗi tự động**:
   - Thêm node **Code** để kiểm tra lỗi và gửi email thông báo khi có vấn đề (ví dụ: API Google Analytics không hoạt động).
   - Ví dụ:
     ```javascript
     if ($input.all()[0].json.error) {
       return [
         {
           json: {
             error: $input.all()[0].json.error.message,
             timestamp: new Date().toISOString(),
           },
         },
       ];
     }
     ```

6. **Tích hợp với Google Data Studio**:
   - Sau khi lưu log vào Google Sheets, có thể kết nối với **Google Data Studio** để tạo dashboard tự động.

---
### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp marketing và team khỏi việc thu thập, phân tích và báo cáo dữ liệu Google Analytics thủ công. Với **AI tóm tắt thông minh**, **thông báo tức thời** và **nhiệm vụ tự động**, các sếp có thể:
✅ **Quản lý traffic hiệu quả** hơn.
✅ **Phát hiện xu hướng sớm** và phản ứng kịp thời.
✅ **Tiết kiệm thời gian** để tập trung vào chiến lược marketing.

**🚀 Hãy tự động hóa ngay hôm nay!**
- **Nếu chưa có VPS**, đăng ký ngay [VPS TinoHost](https://tino.vn/vps-n8n?affid=388) với mã giảm giá **VPSN8N** (giảm tới 39%) hoặc [VPS Xeon 4GB chỉ