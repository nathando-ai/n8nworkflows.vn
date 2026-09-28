---
title: "🌟 **Tự Động Hóa Lời Khích Lực Hàng Ngày qua Email & Telegram - Dành Cho Người Bận Rộn**"
description: "Workflow tự động gửi lời khích lệ ngẫu nhiên hàng ngày vào 7h sáng qua Email (bắt buộc) và Telegram (tùy chọn), giúp các sếp bắt đầu ngày mới với tinh thần tích cực, tiết kiệm thời gian và không cần code."
slug: "tieu-dong-hoa-loi-khich-luc-hang-ngay-email-telegram"
tags: [n8n, automation, personal-productivity, telegram-bot, email-automation, no-code]
keywords: [tự động hóa n8n, lời khích lệ hàng ngày, Telegram Bot, Email tự động, productivity, workflow n8n]
---

# **🌞 Tự Động Hóa Lời Khích Lực Hàng Ngày qua Email & Telegram**

### **🔥 Nỗi Đau Của Các Sếp Hiện Nay**
Các sếp có biết rằng **90% thời gian đầu ngày** của bạn có thể bị "cướp đi" bởi việc tìm kiếm động lực, kiểm tra email, hoặc mất tập trung? Đặc biệt với những người **bận rộn, là người chăm sóc gia đình, hoặc nhà sáng tạo**, việc bắt đầu ngày mới với một **lời khích lệ cá nhân hóa** có thể thay đổi toàn bộ tâm thế của bạn.

Thay vì phải **ghi nhớ, tự viết, hoặc tìm kiếm lời khích lệ** hàng ngày, **hãy để n8n tự động hóa nó**! Workflow này sẽ:
✅ **Gửi 1 lời khích lệ ngẫu nhiên** vào **7h sáng** (hoặc thời gian bạn chọn) qua **Email** (bắt buộc) và **Telegram** (tùy chọn).
✅ **Không cần code**, chỉ cần cấu hình vài bước đơn giản.
✅ **Tiết kiệm thời gian** và giúp bạn **bắt đầu ngày với tinh thần tích cực**.
✅ **Cá nhân hóa hoàn toàn** – bạn có thể thay đổi danh sách lời khích lệ, thời gian, hoặc kênh thông báo.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để tránh giới hạn của phiên bản miễn phí.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần phải tự tìm kiếm hoặc viết lời khích lệ hàng ngày.
- **Tinh thần tích cực**: Bắt đầu ngày với một **lời động viên cá nhân hóa**, giúp giảm stress và tăng động lực.
- **Hoạt động tự động**: Workflow chạy **mỗi ngày tự động** (không cần can thiệp thủ công).
- **Dễ dàng cá nhân hóa**: Thay đổi danh sách lời khích lệ, thời gian, hoặc kênh thông báo theo ý muốn.
- **An toàn & bảo mật**: **Không lưu mật khẩu** trong nodes – tất cả cấu hình đều được quản lý trong **Set: Configuration**.
:::

---

### **🔧 Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản Email** (để gửi lời khích lệ) với **SMTP credentials** (tên miền, username, password, port).
✔ **Bot Telegram** (tùy chọn) – nếu muốn nhận thông báo trên Telegram.
✔ **Danh sách lời khích lệ** (các sếp có thể tự thêm vào trong **Set: Configuration**).

---
:::info[CHUẨN BỊ]
**Nếu chưa có SMTP credentials:**
- Dùng **Gmail SMTP** (cần kích hoạt "Mật khẩu ứng dụng" nếu 2FA bật).
- Hoặc dùng **SMTP của nhà cung cấp email** (như Zoho, Outlook, Mailgun...).

**Nếu muốn dùng Telegram:**
- Tạo **Bot Telegram** tại [@BotFather](https://t.me/BotFather) và lấy **API Token**.
- Thêm **Chat ID** của bạn (có thể lấy bằng cách gửi tin nhắn cho bot và check URL).
:::

---

### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow bằng **2 cách**:
- **Tải file JSON** từ [n8n.io/workflows/7421](https://n8n.io/workflows/7421) và import vào **n8n Editor**.
- **Copy JSON** từ trang trên và **paste** vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Sau khi import, các sếp cần **cấu hình các node quan trọng** như sau:

##### **A. Cấu Hình Cron (Định thời gian)**
- Node: **"Cron: Trigger Daily at 7 AM"**
- **Lưu ý**: Thời gian mặc định là **7h sáng**, nhưng các sếp có thể thay đổi thành bất kỳ thời gian nào (ví dụ: `0 7 * * *` cho 7h sáng hàng ngày).
- **Test**: Để debug, các sếp có thể thay đổi thành `* * * * *` (mỗi phút) để kiểm tra workflow trước khi bật chế độ tự động.

##### **B. Cấu Hình Email (Bắt Buộc)**
- Node: **"Email: Send Affirmation"**
- **Yêu cầu**:
  - Đã thêm **SMTP credentials** trong **Credentials Manager** của n8n.
  - Trong **Set: Configuration**, điền:
    - **Email recipient** (địa chỉ email của bạn).
    - **Subject** (tiêu đề email, ví dụ: "Lời Khích Lực Hàng Ngày").
    - **Body template** (nội dung email, có thể sử dụng biến `$json["affirmation"]` để hiển thị lời khích lệ).

##### **C. Cấu Hình Telegram (Tùy Chọn)**
- Node: **"Telegram: Send Affirmation"**
- **Yêu cầu**:
  - Đã thêm **Telegram Bot Token** và **Chat ID** trong **Credentials Manager**.
  - Trong **Set: Configuration**, điền:
    - **Telegram chat ID** (nếu để trống, node này sẽ bị bỏ qua).
  - **Lưu ý**: Nếu không muốn dùng Telegram, các sếp có thể **xóa node này** hoặc **tắt điều kiện IF** sau.

##### **D. Cấu Hình Lời Khích Lực Ngẫu Nhiên**
- Node: **"Code: Pick Random Affirmation"**
- Các sếp cần chỉnh sửa **danh sách affirmations** trong **Set: Configuration**:
  ```json
  {
    "affirmations": [
      "Hôm nay tôi sẽ làm việc hiệu quả và tự tin!",
      "Tôi tin vào khả năng của mình và sẽ đạt được mục tiêu!",
      "Mỗi ngày là cơ hội mới để học hỏi và phát triển.",
      "Tôi yêu cuộc sống và cảm ơn mọi thứ đã xảy ra.",
      "Hãy nhẹ nhàng với bản thân, bạn đã làm tốt!"
    ]
  }
  ```
- **Lưu ý**: Các sếp có thể **thêm/bớt** lời khích lệ tùy ý.

##### **E. Điều Kiện IF (Telegram Enabled?)**
- Node: **"IF: Telegram Enabled?"**
- Nếu muốn **bật/tắt Telegram**, các sếp chỉ cần:
  - **Điền Chat ID** vào **Set: Configuration** → Telegram sẽ được kích hoạt.
  - **Để Chat ID trống** → Telegram sẽ bị bỏ qua.

#### **3. Kích Hoạt ⚡️**
- **Test Run**: Chuyển **Cron** thành `* * * * *` (mỗi phút) và **run workflow** để kiểm tra.
- **Bật Active**: Sau khi kiểm tra thành công, **đổi lại thời gian Cron** và **bật Active workflow**.

---

### **✍️ Mẹo & Gợi Ý Nâng Cao**
Các sếp có thể **tối ưu hóa workflow** thêm bằng cách:
1. **Thêm Notion/Google Sheets để lưu lịch sử**:
   - Sử dụng **Node Notion** hoặc **Google Sheets** để ghi lại **lời khích lệ đã gửi** và **ngày tháng**.
   - Cách làm: Thêm **Node Notion API** sau **Email/Telegram** và ghi dữ liệu vào bảng.

2. **Kết hợp với Slack/Teams**:
   - Thay vì Telegram, các sếp có thể **gửi thông báo qua Slack** bằng **Node Slack Webhook**.

3. **Thay đổi danh sách lời khích lệ tự động**:
   - Sử dụng **Node HTTP Request** để lấy **lời khích lệ từ API** (ví dụ: API của [Affirmations API](https://affirmations-api.herokuapp.com/)).

4. **Gửi báo cáo tuần/Tháng**:
   - Thêm **Node Set** sau **Cron** để đếm số lần gửi và **gửi báo cáo định kỳ** qua Email.

5. **Sử dụng AI để tạo lời khích lệ**:
   - Thêm **Node LLM** (như Mistral AI) để **tự động sinh lời khích lệ** dựa trên tình trạng tâm lý (nếu có API kết nối).

---

### **📌 Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn **bắt đầu ngày với động lực**, **tiết kiệm thời gian**, và **không cần code**. Với chỉ **vài bước cấu hình**, bạn đã có một **công cụ tự động hóa cá nhân hóa**, giúp bạn **tích cực hơn** mỗi ngày.

**Hãy thử ngay!** Import workflow, cấu hình theo hướng dẫn, và **nhận lời khích lệ hàng ngày** mà không cần lo lắng.

---
**💡 Mẹo cuối**: Nếu các sếp muốn **mở rộng**, có thể kết hợp với **n8n Code Node** để **tính toán thống kê** (ví dụ: số ngày liên tiếp nhận lời khích lệ) và **gửi báo cáo tự động**.

**Chúc các sếp thành công!** 🚀