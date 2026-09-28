---
title: "🌅 Tự Động Hóa Briefing Sáng Hôm Nay: Lịch Google, Thời Tiết & Tin Tức Trên Slack (N8N)"
description: "Giải pháp tự động hóa hoàn toàn không code giúp các sếp nhận được briefing sáng hôm nay với lịch Google, thời tiết Tokyo và tin tức nóng hổi trên Slack chỉ trong 10 giây. Tiết kiệm thời gian, tăng năng suất và bắt đầu ngày làm việc với thông tin đầy đủ."
slug: "tieu-dong-hoa-briefing-sang-hom-google-calendar-thoi-tiet-tin-tuc-slack"
tags: [n8n, automation, no-code, google-calendar, slack-integration, weather-api]
keywords: [n8n workflow tự động hóa, briefing sáng hôm nay, lịch Google tự động, thời tiết Tokyo API, tin tức RSS Slack, tự động hóa Slack]
---

# 🌅 Briefing Sáng Hôm Nay: Lịch, Thời Tiết & Tin Tức Trên Slack (N8N)

### **Giải pháp cho các sếp bận rộn muốn bắt đầu ngày làm việc với thông tin đầy đủ chỉ trong 10 giây**

Chúng ta đã từng phải mở nhiều tab trên trình duyệt để kiểm tra lịch Google, thời tiết và tin tức mới nhất trước khi bắt đầu một ngày làm việc. **Công việc này mất thời gian và dễ bị bỏ quên** khi cuộc sống và công việc ngày càng bận rộn. Với **workflow tự động hóa này**, các sếp sẽ nhận được một **briefing sáng hôm nay** được tổng hợp từ:
- **Lịch Google** (tất cả sự kiện trong ngày)
- **Thời tiết Tokyo** (mặc định, có thể thay đổi thành bất kỳ thành phố nào)
- **Tin tức nóng hổi** (top 3 tin tức từ Google News RSS)

Tất cả thông tin sẽ được **gửi trực tiếp lên Slack** mỗi sáng lúc 7h, giúp các sếp **bắt đầu ngày làm việc với thông tin đầy đủ mà không cần mở một tab nào**.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần mở nhiều tab để kiểm tra lịch, thời tiết và tin tức.
- **Thông tin đầy đủ**: Nhận tất cả thông tin cần thiết trong một tin nhắn Slack duy nhất.
- **Tự động hóa hoàn toàn**: Không cần nhớ hoặc thiết lập lại mỗi ngày.
- **Cá nhân hóa**: Dễ dàng thay đổi thành phố, nguồn tin tức hoặc thời gian gửi.
- **Hoạt động liên tục**: Workflow chạy tự động hàng ngày, ngay cả khi các sếp không ở máy.
:::

---

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Google Calendar** (để lấy lịch sự kiện).
2. **Tài khoản Slack** (để gửi briefing).
3. **API Key hoặc OAuth2** cho Google Calendar (cấu hình trong Credentials của n8n).
4. **Không cần API Key cho thời tiết và tin tức** (workflow sử dụng nguồn mở: `wttr.in` và RSS Google News).

---
:::note[Lưu ý quan trọng]
- Workflow mặc định lấy **thời tiết Tokyo** và **tin tức từ Google News RSS**. Các sếp có thể thay đổi thành bất kỳ thành phố hoặc nguồn tin tức khác.
- Để thay đổi thành phố, cần chỉnh sửa URL trong node `Get Weather Forecast` (ví dụ: `https://wttr.in/Paris`).
- Để thay đổi nguồn tin tức, cần chỉnh sửa `rssUrl` trong node `Get Top News from RSS`.
:::

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Tải file JSON từ [link gốc](https://n8n.io/workflows/9819).
2. Trong n8n Editor, nhấn **Import Workflow** và chọn file JSON.
3. Hoặc copy toàn bộ JSON và dán vào **Import Workflow** trong menu.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình các node quan trọng sau:

##### **A. Cấu hình Google Calendar**
1. Trong node **"Get Today's Calendar Events"**:
   - Chọn **credentials** là `googleCalendarOAuth2Api`.
   - Đảm bảo đã **cấu hình OAuth2** trong Credentials của n8n (nếu chưa, tham khảo [hướng dẫn OAuth2](https://docs.n8n.io/integrations/credentials/google-calendar/)).

##### **B. Cấu hình Slack**
1. Trong node **"Post to Slack"**:
   - Chọn **credentials** là `slackWebhook` (hoặc `slackOAuth2` nếu sử dụng OAuth2).
   - Đảm bảo đã **cấu hình Webhook URL** trong Credentials của Slack (tham khảo [hướng dẫn Slack](https://docs.n8n.io/integrations/credentials/slack/)).
   - Chọn **channel** (ví dụ: `#general` hoặc `#briefing`).

##### **C. Cấu hình thời tiết và tin tức**
1. Trong node **"Get Weather Forecast"** (HTTP Request):
   - URL mặc định: `https://wttr.in/Tokyo?format=%C+%t`.
   - Các sếp có thể thay đổi thành phố (ví dụ: `https://wttr.in/Hà Nội?format=%C+%t`).
   - **Không cần API Key** vì `wttr.in` là dịch vụ mở.

2. Trong node **"Get Top News from RSS"** (RSS Feed Read):
   - URL mặc định: `https://news.google.com/rss/search?q=world&hl=en-US&gl=US&ceid=US:en`.
   - Các sếp có thể thay đổi chủ đề tin tức (ví dụ: `https://news.google.com/rss/search?q=technology&hl=en-US`).

##### **D. Cấu hình thời gian gửi**
1. Trong node **"Daily Morning Trigger"** (Schedule Trigger):
   - Thời gian mặc định: **7:00 AM** (UTC).
   - Các sếp có thể thay đổi theo giờ địa phương (ví dụ: `7:00 AM +07` cho Việt Nam).

#### 3. Kích hoạt ⚡️
1. **Test Run**:
   - Nhấn **Run Workflow** để kiểm tra nếu tất cả dữ liệu được lấy và gửi thành công.
   - Kiểm tra Slack để xem briefing có hiển thị đúng không.

2. **Bật Active**:
   - Sau khi test thành công, chuyển trạng thái workflow sang **Active**.

---

### ✍️ Mẹo & gợi ý nâng cao
:::tip[CÁCH THAY ĐỔI THÀNH PHỐ THỜI TIẾT]
- Thay đổi URL trong node `Get Weather Forecast`:
  - Ví dụ: `https://wttr.in/Hà Nội?format=%C+%t` (thay Tokyo thành Hà Nội).
  - Các mã thành phố khác: [Danh sách mã thành phố](https://en.wikipedia.org/wiki/List_of_country_codes_by_ISO_3166).
:::

:::tip[CÁCH THAY ĐỔI NỢI TIN TỨC]
- Thay đổi `rssUrl` trong node `Get Top News from RSS`:
  - Ví dụ: `https://news.google.com/rss/search?q=technology&hl=en-US` (tin tức công nghệ).
  - Các chủ đề khác: `finance`, `sports`, `entertainment`.
:::

:::tip[CÁCH LƯU LOG HOẠT ĐỘNG]
- Thêm node **Sticky Note** để lưu log:
  - Sử dụng node `Workflow Configuration` để lưu thông tin debug.
  - Ví dụ: Lưu ngày giờ chạy và kết quả.
:::

:::tip[CÁCH GỬI BÁO CÁO ĐỊNH KỲ]
- Thêm node **Email** (n8n-nodes-base.email) để gửi briefing qua email:
  - Cấu hình SMTP và địa chỉ email trong Credentials.
  - Thêm node này sau node `Format Briefing Message`.
:::

---

### 📌 Kết luận
**Briefing sáng hôm nay** là một trong những **workflow tự động hóa hiệu quả nhất** để giúp các sếp bắt đầu ngày làm việc với thông tin đầy đủ. Với **chỉ 10 giây mỗi sáng**, các sếp sẽ không bao giờ bỏ lỡ lịch, thời tiết hoặc tin tức quan trọng.

**Hãy áp dụng ngay workflow này và bắt đầu ngày làm việc hiệu quả hơn!**
👉 [Tải workflow từ n8n.io](https://n8n.io/workflows/9819)
👉 [Cài đặt n8n trên VPS](https://docs.n8n.io/hosting/installation/) (nếu chưa có).

---
**Chia sẻ và phản hồi:**
Nếu các sếp có bất kỳ câu hỏi hoặc ý kiến, hãy để lại comment bên dưới. Chúng tôi sẽ hỗ trợ miễn phí! 🚀