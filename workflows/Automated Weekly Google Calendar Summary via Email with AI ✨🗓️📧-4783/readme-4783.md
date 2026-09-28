---
title: "🚀 Tự Động Hoá Báo Cáo Tuần Google Calendar Với AI - Nhận Email Tóm Tắt Hàng Tuần Mỗi Ngày 🗓️✨"
description: "Workflow tự động hóa hoàn toàn không cần code giúp các sếp tiết kiệm 5+ giờ/tháng bằng cách tự động tổng hợp và gửi email tóm tắt lịch trình tuần tới từ Google Calendar với AI Gemini, bao gồm sự kiện quan trọng, thời gian, và nhận xét tuần. Giúp quản lý thời gian hiệu quả hơn 30%!"
slug: "tieu-dong-hoa-bao-cao-tuan-google-calendar-voi-ai"
tags: [n8n, automation, no-code, ai-gemini, google-calendar, email-automation]
keywords: [tự động hóa google calendar, email tóm tắt tuần, ai gemini n8n, tự động hóa lịch trình, báo cáo tuần tự động]
---

# 🚀 **Tự Động Hoá Báo Cáo Tuần Google Calendar Với AI - Nhận Email Tóm Tắt Hàng Tuần Mỗi Ngày**

### **🔥 Nỗi Đau Của Các Sếp Hiện Nay**
Các sếp và nhân viên văn phòng thường phải mất **5-10 giờ/tháng** để thủ công:
- **Tìm kiếm và tổng hợp** các sự kiện trong Google Calendar hàng tuần.
- **Lọc bỏ thông tin không cần thiết** (link, metadata) để tập trung vào nội dung quan trọng.
- **Tạo email tóm tắt** với định dạng chuyên nghiệp, nhấn mạnh sự kiện cấp thiết.
- **Gửi email định kỳ** cho đồng nghiệp hoặc bản thân để theo dõi lịch trình.

**Kết quả?** Thời gian quý giá bị "chôn vùi" trong công việc lặp lại, trong khi AI và tự động hóa có thể **giải phóng 100% công việc này** chỉ trong vài phút!

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm 5-10 giờ/tháng** bằng cách loại bỏ công việc thủ công.
- **Nhận email tóm tắt chuyên nghiệp** hàng tuần, với sự kiện được **nhấn mạnh, phân loại và tổng hợp** bởi AI Gemini.
- **Cập nhật thời gian thực** (không cần cập nhật thủ công).
- **Tùy chỉnh hoàn toàn** nội dung, định dạng, và cách AI phân tích sự kiện.
- **Hoạt động 24/7** mà không cần can thiệp của con người.
:::

---
### **🔧 Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI SỬ DỤNG**]
Để workflow này hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Google Calendar** (để lấy dữ liệu sự kiện).
2. **API Key Google Gemini (PaLM API)** (để sử dụng AI tổng hợp).
3. **Tài khoản SMTP** (để gửi email tự động):
   - Dịch vụ SMTP phổ biến: **Gmail (SMTP), SendGrid, Mailgun, hoặc SMTP của nhà cung cấp hosting**.
4. **Thông tin cá nhân hóa**:
   - **Ngôn ngữ (locale)**: Ví dụ: `en-AU` (Anh Úc), `vi-VN` (Tiếng Việt).
   - **Múi giờ (timezone)**: Ví dụ: `Asia/Ho_Chi_Minh` (Hà Nội), `Europe/London` (London).
   - **Tên và thành phố**: Ví dụ: `users-name: "Lê Minh Thắng"`, `users-home-city: "Hà Nội"`.
:::

---
### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/4783](https://n8n.io/workflows/4783) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ link trên và dán vào **Import Workflow** trong n8n.

:::note[**Lưu ý quan trọng**]
- **Không sao chép/paste trực tiếp từ trang web** (do có ký tự đặc biệt gây lỗi). **Sử dụng file JSON** hoặc **copy từ tab "JSON"** trong n8n Editor.
- **Không xóa node nào** trong workflow (trừ khi biết rõ tác dụng của nó).
:::

---

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Dưới đây là **danh sách các node cần cấu hình chi tiết**:

##### **📌 Node `locale` (Set) – Cấu Hình Thông Tin Cá Nhân**
- **Yêu cầu bắt buộc**:
  - `users-locale`: Chọn ngôn ngữ phù hợp (ví dụ: `vi-VN`).
  - `users-timezone`: Chọn múi giờ (ví dụ: `Asia/Ho_Chi_Minh`).
  - `users-name`: Tên của bạn (sẽ xuất hiện trong email).
  - `users-home-city`: Thành phố bạn thường ở (để AI cung cấp bối cảnh).
- **Ví dụ**:
  ```json
  {
    "users-locale": "vi-VN",
    "users-timezone": "Asia/Ho_Chi_Minh",
    "users-name": "Lê Minh Thắng",
    "users-home-city": "Hà Nội"
  }
  ```

##### **📌 Node `weekly_schedule` (Schedule Trigger) – Lịch Trình Tự Động**
- **Mặc định**: Chạy **mỗi tuần vào 12:00 PM** (giờ UTC).
- **Cách thay đổi**:
  - Vào **Settings** của node → **Rule**.
  - Chọn **Interval**: `Weekly`.
  - Chọn **Day**: `Monday` (hoặc ngày khác).
  - Chọn **Time**: `12:00 PM` (hoặc giờ phù hợp).
  - **Lưu ý**: Nếu muốn chạy **ngày khác** (ví dụ: thứ 2), chỉnh theo yêu cầu.

##### **📌 Node `get_next_weeks_events` (Google Calendar) – Lấy Dữ Liệu Sự Kiện**
- **Yêu cầu bắt buộc**:
  1. **Thiết lập OAuth2 cho Google Calendar**:
     - Vào **Credentials** → **Add** → Chọn `googleCalendarOAuth2Api`.
     - Theo hướng dẫn để kết nối tài khoản Google Calendar.
  2. **Thay đổi `calendar` ID**:
     - Mặc định là `c_4d9...group.calendar.google.com` (là một calendar mẫu).
     - **Cách tìm ID của calendar cá nhân**:
       - Mở Google Calendar → Nhấn **⚙️ Settings** → **Calendar settings**.
       - Chọn calendar muốn lấy dữ liệu → **Calendar address** (đây là ID cần thay).
     - **Ví dụ**:
       ```json
       "calendar": "lmtang@gmail.com"  // Thay bằng ID của bạn
       ```

##### **📌 Node `Google Gemini` (lmChatGoogleGemini) – Kết Nối API AI**
- **Yêu cầu bắt buộc**:
  1. **Thiết lập API Key Google Gemini**:
     - Vào **Credentials** → **Add** → Chọn `googlePalmApi`.
     - Nhập **API Key** từ [Google AI Studio](https://aistudio.google.com/).
  2. **Chọn model**:
     - Mặc định: `models/gemini-2.5-flash-preview-05-20` (model miễn phí).
     - **Không cần thay đổi** trừ khi muốn sử dụng model khác.

##### **📌 Node `send_email` (EmailSend) – Gửi Email Tóm Tắt**
- **Yêu cầu bắt buộc**:
  1. **Thiết lập SMTP**:
     - Vào **Credentials** → **Add** → Chọn `smtp`.
     - Nhập thông tin SMTP (host, port, username, password).
     - **Dịch vụ SMTP phổ biến**:
       - **Gmail**: `smtp.gmail.com`, Port `465` (SSL).
       - **SendGrid**: `smtp.sendgrid.net`, Port `587` (TLS).
  2. **Cấu hình email**:
     - `fromEmail`: Email gửi (ví dụ: `lmtang@gmail.com`).
     - `toEmail`: Email nhận (ví dụ: `lmtang@gmail.com` hoặc `team@doanhnghiep.com`).
     - **Ví dụ**:
       ```json
       {
         "fromEmail": "lmtang@gmail.com",
         "toEmail": "lmtang@gmail.com",
         "subject": "Tóm tắt lịch trình tuần tới - {{ $node["date_time"].json["users-current-day"] }}"
       }
       ```

##### **📌 Node `event_summary_agent` (AI Agent) – Cấu Hình Prompt AI**
- **Không cần thay đổi** trừ khi muốn **tùy chỉnh cách AI tổng hợp**:
  - **Greeting**: Thay đổi lời chào (ví dụ: từ "Chào buổi sáng" thành "Xin chào").
  - **Phân loại sự kiện**: Thêm từ khóa như `urgent`, `deadline` để AI nhấn mạnh.
  - **Weekly Insight**: Yêu cầu AI đưa ra **nhận xét tuần** (ví dụ: "Tuần này có nhiều cuộc họp, nên ưu tiên hoàn thành dự án X").

---
#### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run** (kiểm tra trước khi chạy thực tế):
   - Nhấn **Run Workflow** và chọn **Test Execution**.
   - Kiểm tra **email mẫu** có được gửi không.
2. **Bật Active**:
   - Sau khi kiểm tra thành công, chuyển **Active** sang `true`.

---
### **✍️ Mẹo & Gợi Ý Nâng Cao**
:::tip[**CÁCH TIẾP CẬN HƠN**]
1. **Gửi email cho nhiều người**:
   - Thay `toEmail` thành danh sách email (ví dụ: `"lmtang@gmail.com, team@doanhnghiep.com"`).
2. **Lưu log sự kiện**:
   - Thêm node **Google Sheets** hoặc **Slack** để ghi lại lịch sử email đã gửi.
3. **Tùy chỉnh subject email**:
   - Thay đổi `subject` trong node `send_email` để hiển thị ngày cụ thể (ví dụ: `"Tóm tắt tuần từ {{ $node["date_time"].json["users-start-date"] }}"`).
4. **Sử dụng AI Gemini Pro**:
   - Nếu muốn chất lượng cao hơn, thay model thành `models/gemini-1.5-pro-001` (có chi phí).
5. **Kết hợp với Slack/Telegram**:
   - Thay node `send_email` bằng **Slack Webhook** hoặc **Telegram Bot** để thông báo tức thì.
:::

---
### **📌 Kết Luận**
Workflow này **giải phóng bạn khỏi công việc lặp lại** hàng tuần, giúp bạn **tập trung vào những việc quan trọng** hơn. Với **AI Gemini**, email tóm tắt không chỉ đơn giản là danh sách sự kiện, mà còn là **báo cáo chuyên nghiệp, cá nhân hóa và đầy thông tin**.

**🚀 Hành động ngay hôm nay!**
1. **Import workflow** vào n8n của bạn.
2. **Cấu hình các node bắt buộc** (Google Calendar, SMTP, AI Key).
3. **Chạy test** và **bật tự động hóa** để nhận email tóm tắt hàng tuần!

---
:::info[**Gợi ý hạ tầng cho n8n**]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**💡 Câu hỏi thường gặp:**
- **AI Gemini có miễn phí không?**
  → Model `gemini-2.5-flash-preview-05-20` miễn phí, nhưng có giới hạn request/tháng.
- **Email có bị đánh vào spam không?**
  → Nếu SMTP cấu hình đúng, email sẽ được gửi bình thường. Nếu bị spam, kiểm tra **SPF/DKIM** của SMTP.
- **Có thể chạy workflow hàng ngày không?**
  → Có, chỉ cần thay đổi **schedule** từ `Weekly` sang `Daily`.

**🔗 Tài liệu tham khảo:**
- [Cách lấy ID Google Calendar](https://support.google.com/calendar/answer/37100)
- [Cách thiết lập SMTP Gmail](https://support.google.com/mail/answer/7126229)
- [Google AI Studio](https://aistudio.google.com/)