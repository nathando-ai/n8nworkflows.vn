---
title: "🤖 **Tự Động Hẹn Phỏng Vấn với AI GPT-4o + Google Calendar – Không Cần Code!**"
description: "Workflow tự động hóa hoàn toàn giúp các sếp HR hoặc doanh nghiệp tự động hóa quá trình hẹn phỏng vấn thông qua AI chatbot, kiểm tra lịch Google Calendar và đặt lịch tự động. Giảm thiểu thời gian quản lý lịch đến 90%, tránh xung đột và cải thiện trải nghiệm ứng viên."
slug: "tuy-dong-hoan-thanh-he-nhan-phong-van-ai-gpt-4o-google-calendar"
tags: [n8n, automation, hr, ai, gpt-4o, google-calendar, no-code, chatbot]
keywords: [tự động hóa hẹn phỏng vấn, n8n workflow, ai chatbot, google calendar api, gpt-4o tự động hóa, tự động hóa hr]
---

# 🚀 **Tự Động Hẹn Phỏng Vấn với AI GPT-4o + Google Calendar – Không Cần Code!**

### **Giải pháp hoàn hảo cho các sếp HR và doanh nghiệp**
Hiện nay, việc quản lý lịch phỏng vấn thủ công không chỉ tốn thời gian mà còn dễ gây lỗi như **trùng lịch, quên thông báo, hoặc mất trải nghiệm ứng viên**. Workflow này giúp **tự động hóa toàn bộ quy trình** từ khi ứng viên gửi yêu cầu đến khi lịch được đặt và thông báo tự động – **không cần viết một dòng code nào!**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính riêng tư và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Không cần quản lý lịch thủ công, tự động xử lý hàng trăm yêu cầu đồng thời.
✅ **Tránh xung đột lịch**: AI kiểm tra lịch Google Calendar và chỉ đề xuất thời gian trống.
✅ **Trải nghiệm ứng viên tốt**: Chatbot AI phản hồi nhanh chóng, cá nhân hóa và tự động xác nhận lịch.
✅ **Hoạt động 24/7**: Workflow chạy tự động, không phụ thuộc vào giờ làm việc của nhân viên.
✅ **Cá nhân hóa dễ dàng**: Thay đổi thông điệp, branding hoặc quy trình theo nhu cầu doanh nghiệp.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản OpenAI** với API Key cho mô hình **GPT-4o** (hoặc GPT-4o-mini).
2. **Tài khoản Google** với quyền truy cập vào **Google Calendar**.
3. **Credentials OAuth2 cho Google Calendar API** (cấu hình trong n8n).
4. **Credentials API cho OpenAI** (đã thêm API Key trong n8n).
5. **n8n Self-hosted** (không dùng phiên bản cloud để đảm bảo an toàn dữ liệu).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/3363](https://n8n.io/workflows/3363) hoặc copy toàn bộ JSON từ trang này.
- Mở **n8n Editor** → Nhấn **"Import"** → Dán JSON và nhấn **"Import"**.
- Workflow sẽ xuất hiện với **22 node** đã cấu hình sẵn.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này sử dụng **AI Agent (LangChain)** kết hợp với **Google Calendar**, nên cần chú ý các bước sau:

##### **A. Cấu hình Credentials**
- **Google Calendar OAuth2**:
  - Tạo **project mới** trên [Google Cloud Console](https://console.cloud.google.com/) với tên **"n8n"**.
  - Trong n8n, đi đến **"Credentials"** → **"Add"** → Chọn **"Google Calendar OAuth2 API"**.
  - **Authorize** với tài khoản Google Calendar của bạn (ví dụ: `sop@gmail.com`).
  - Lưu credential với tên dễ nhớ (ví dụ: `googleCalendarOAuth2`).

- **OpenAI API**:
  - Trong n8n, đi đến **"Credentials"** → **"Add"** → Chọn **"OpenAI API"**.
  - Nhập **API Key** từ tài khoản OpenAI và đặt tên (ví dụ: `openAiApi`).

##### **B. Cập nhật thông tin cá nhân hóa**
- **Thay đổi email Google Calendar**:
  - Trong node **"Check My Calendar"** và **"Set Meeting with Google"**, thay thế `rbreen.ynteractive@gmail.com` thành **email Google Calendar của bạn**.
  - Trong node **"Run Get Availability"**, mở **ToolWorkflow JSON** và thay thế email tương tự.

- **Thay đổi tên credential**:
  - Trong node **"Set Meeting with Google"**, thay đổi `googleCalendarOAuth2Api` thành tên credential bạn đã tạo.
  - Trong node **"OpenAI Chat Model2/4"**, thay đổi `openAiApi` thành tên credential OpenAI của bạn.

- **Cập nhật Webhook URL (để ứng viên chat)**:
  - Node **"When chat message received"** có URL webhook công khai. **Chia sẻ URL này** cho ứng viên để họ chat và đặt lịch.
  - **Lưu ý**: Nếu dùng phiên bản cloud, URL sẽ thay đổi khi restart. **Self-hosted** là lựa chọn an toàn nhất.

- **Tùy chỉnh thông điệp AI (Optional)**:
  - Trong node **"Interview Scheduler"**, mở **System Message** để thay đổi **tôn ngữ, câu hỏi hoặc quy tắc** của chatbot.
  - Ví dụ: Thay đổi từ *"Xin chào, tôi là AI hỗ trợ hẹn phỏng vấn"* thành *"Chào mừng đến với [Tên Công Ty], chúng tôi sẵn sàng hỗ trợ!"*.

- **Thay đổi branding (Optional)**:
  - Trong node **"Final Response to User"**, mở **Code Editor** và thay đổi nội dung phản hồi cuối cùng để phù hợp với **logo, màu sắc hoặc thông điệp của doanh nghiệp**.

##### **C. Kích hoạt Workflow ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **"Run"** trên node **"When chat message received"** và nhập một yêu cầu mẫu (ví dụ: *"Hãy hẹn một buổi phỏng vấn vào thứ 3 tuần này"*).
   - Kiểm tra AI có trả lời logic không và lịch có được đặt trên Google Calendar không.

2. **Bật Active**:
   - Sau khi kiểm tra xong, nhấn **"Active"** để workflow chạy tự động.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Slack/Telegram**:
   - Sử dụng node **Slack** hoặc **Telegram Bot** để thông báo lịch mới cho ứng viên và quản trị viên.
   - Ví dụ: Khi lịch được đặt, bot Slack sẽ gửi tin nhắn: *"Lịch phỏng vấn đã được đặt thành công! Thời gian: [Thời gian], Ngày: [Ngày]."*

2. **Lưu log lịch sử**:
   - Thêm node **Airtable** hoặc **Google Sheets** để lưu tất cả lịch phỏng vấn đã đặt, bao gồm thông tin ứng viên, thời gian và trạng thái.

3. **Gửi báo cáo định kỳ**:
   - Sử dụng node **Google Sheets** hoặc **Email** để tự động gửi báo cáo số lượng lịch đã đặt, ứng viên mới và thời gian trống trong tuần.

4. **Cập nhật AI Agent**:
   - Trong node **"Interview Scheduler"**, bạn có thể **tăng cường khả năng xử lý** bằng cách thêm **more tools** (ví dụ: kiểm tra email ứng viên, gửi thông báo qua SMS).

5. **Chặn giờ làm việc**:
   - Trong node **"Split Events into 30 min blocks"**, bạn có thể **tùy chỉnh giờ làm việc** (ví dụ: chỉ cho phép lịch từ 8h-17h EST).

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** để tự động hóa quy trình hẹn phỏng vấn, **giảm thiểu công việc thủ công** và cải thiện trải nghiệm ứng viên. Với **AI GPT-4o** và **Google Calendar**, nó không chỉ tiết kiệm thời gian mà còn **tránh lỗi và tăng hiệu suất**.

**Hãy áp dụng ngay và tự động hóa HR của bạn!**
👉 [Tải workflow từ n8n.io](https://n8n.io/workflows/3363) và bắt đầu **tự động hóa hẹn phỏng vấn** trong vòng 10 phút!

---
**Cần hỗ trợ thêm?** Hãy để lại comment bên dưới hoặc liên hệ với tác giả [Robert Breen](https://n8n.io/workflows/3363) để có hướng dẫn chi tiết hơn! 🚀