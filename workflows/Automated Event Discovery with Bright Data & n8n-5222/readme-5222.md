---
title: "🚀 Tự Động Thu Thập Sự Kiện & Webinar với Bright Data + n8n (Không Cần Code)"
description: "Workflow n8n tự động scrape sự kiện/webinar từ Eventbrite và các trang khó nhằn bằng Bright Data Web Unlocker, xử lý HTML thành dữ liệu sạch và lưu vào Google Sheets theo lịch định kỳ."
slug: "tu-dong-thu-thap-su-kien-webinar-bright-data-n8n"
tags: [n8n, automation, no-code, bright-data, google-sheets, web-scraping, ai]
keywords: [n8n workflow, tự động hóa, scrape eventbrite, bright data web unlocker, thu thập sự kiện tự động, lưu google sheets]
---

# 🚀 Tự Động Thu Thập Sự Kiện & Webinar với Bright Data + n8n

Các sếp đang làm marketing, growth, hay vận hành cộng đồng có bao giờ rơi vào cảnh: mỗi tuần phải mở Eventbrite, Meetup, hoặc các trang sự kiện để "lượt" xem có webinar nào mới không? Ngồi copy từng tiêu đề, ngày giờ, link... rồi dán vào Google Sheet cho team? Nghe thì đơn giản nhưng cực kỳ tốn thời gian, dễ sót sự kiện, và gần như không thể scale khi các sếp theo dõi nhiều nguồn cùng lúc.

Đây chính là lúc workflow **Automated Event Discovery with Bright Data & n8n** phát huy sức mạnh. Chỉ với **5 nodes**, hệ thống sẽ tự động chạy theo lịch, vượt qua hệ thống chống bot của các trang sự kiện lớn, bóc tách dữ liệu HTML "rối như tơ vò" thành JSON sạch, và ghi thẳng vào Google Sheets — tất cả **100% không cần viết code phức tạp**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm hàng giờ mỗi tuần**: Không còn ngồi copy-paste thủ công từng sự kiện, hệ thống tự chạy theo lịch (ví dụ 8h sáng mỗi ngày).
- **Vượt rào anti-bot dễ dàng**: Bright Data Web Unlocker xử lý CAPTCHA, proxy, và fingerprint trình duyệt — những trang "khó tính" như Eventbrite vẫn scrape ngon lành.
- **Dữ liệu sạch, sẵn sàng dùng**: HTML thô được bóc tách thành JSON có cấu trúc (Title / Date / Link) — dễ filter, sort, hoặc sync sang Google Calendar.
- **Google Sheets làm "nguồn chân lý"**: Cả team cùng xem, cùng lọc, cùng chia sẻ — không cần database riêng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Bright Data** (có credit/API key) — dùng để gọi endpoint `https://api.brightdata.com/request` với Web Unlocker. Đăng ký tại [đây](https://get.brightdata.com/1tndi4600b25).
- **Tài khoản Google** + **Google Sheet** đích đã tạo sẵn (với các cột: `Event Title`, `Date & Time`, `URL`).
- **Credentials Google Sheets OAuth2** đã kết nối trong n8n (`googleSheetsOAuth2Api`).
- **n8n instance** (self-hosted hoặc cloud) đã cài đặt và đăng nhập.
- **URL trang sự kiện mục tiêu** (ví dụ: trang listing Eventbrite theo category/topic mà các sếp quan tâm).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể import theo 1 trong 2 cách:
- **Cách 1 — Từ file JSON**: Tải file `.json` của workflow → mở n8n Editor → menu **⋯ (góc trên phải)** → **Import from File** → chọn file.
- **Cách 2 — Copy/Paste JSON**: Mở n8n Editor → nhấn **Ctrl/Cmd + V** (hoặc **Import from Clipboard**) → dán toàn bộ JSON workflow vào.

Sau khi import, các sếp sẽ thấy 5 nodes được bố trí theo luồng: **Trigger → HTTP Request → HTML Extract → Code → Google Sheets**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

**⏰ Node `Trigger - Weekly Run` (Schedule Trigger)**
- Mặc định workflow chạy theo lịch tuần. Các sếp có thể đổi sang **Daily / Every X hours** tùy nhu cầu.
- Gợi ý: đặt vào khung giờ ít traffic (ví dụ 6–8h sáng) để tránh rate limit từ Bright Data.

**🌐 Node `Scrape event website using bright data` (HTTP Request)**
- **Method**: `POST`
- **URL**: `https://api.brightdata.com/request`
- **Headers**: thêm `Authorization: Bearer <BRIGHT_DATA_API_TOKEN>` (lấy trong dashboard Bright Data).
- **Body (JSON)** cần chỉnh:
  - `zone`: tên zone Web Unlocker của các sếp (ví dụ `web_unlocker1`).
  - `url`: URL trang sự kiện muốn scrape (ví dụ trang listing Eventbrite).
  - `format`: `raw` để nhận HTML thô.
- ⚠️ **Lưu ý**: Nếu chưa có zone Web Unlocker, vào Bright Data dashboard tạo mới trước.

**🧾 Node `Parse HTML - Extract Event Cards` (HTML Extract)**
- **Operation**: `Extract HTML Content`.
- **Source Data**: `JSON` → trỏ tới field chứa HTML trả về từ Bright Data (thường là `data` hoặc `body`).
- **Extraction Values** — cấu hình 3 CSS selectors (theo template Eventbrite, các sếp đổi nếu dùng site khác):
  - `titles` → `.eds-event-card-content__title`
  - `dates` → `.eds-event-card-content__sub-title`
  - `links` → `.eds-event-card-content__action-link[href]` (nhớ bật **Return Array** và **Attribute: href** cho links).
- 💡 Nếu scrape site khác (Meetup, Luma, v.v.), các sếp cần **Inspect Element** trên trang đó để lấy đúng class CSS.

**🧮 Node `Format Event Data` (Code)**
- Node này map song song 3 mảng `titles`, `dates`, `links` thành từng object JSON sạch:
```js
return items[0].json.titles.map((title, i) => {
  return {
    json: {
      title,
      date: items[0].json.dates[i],
      link: items[0].json.links[i]
    }
  };
});
```
- ⚠️ **Kiểm tra**: nếu HTML Extract trả về tên field khác (không phải `titles/dates/links`), phải sửa lại cho khớp.

**📄 Node `Save to Google Sheet` (Google Sheets)**
- **Credential**: chọn `googleSheetsOAuth2Api` đã kết nối.
- **Operation**: `Append`.
- **Document ID**: chọn Google Sheet đích (hoặc dán ID).
- **Sheet Name**: chọn tab muốn ghi (ví dụ `Events`).
- **Columns / Mapping**: map 3 field `title`, `date`, `link` vào đúng cột tương ứng.
- 💡 Bật **Auto-map Input Data** để n8n tự khớp field — nhanh hơn cho người mới.

#### 3. Kích hoạt ⚡️
1. Nhấn **Execute Workflow** để test với dữ liệu mẫu — kiểm tra xem Google Sheet có nhận đúng 3 cột không.
2. Nếu output ổn, gạt công tắc **Active** (góc trên phải) để workflow chạy tự động theo lịch.
3. Theo dõi **Executions** tab trong vài lần chạy đầu để chắc chắn không bị lỗi rate limit hoặc selector sai.

### ✍️ Mẹo & gợi ý nâng cao
- **Gửi thông báo real-time**: Thêm node **Telegram** hoặc **Slack** sau Google Sheets để ping team mỗi khi có sự kiện mới được thêm vào sheet.
- **Lọc sự kiện theo keyword**: Chèn node **IF** hoặc **Filter** trước khi ghi Sheet — chỉ giữ lại sự kiện có tiêu đề chứa từ khóa (ví dụ "AI", "Marketing", "SaaS").
- **Sync sang Google Calendar**: Thay vì chỉ lưu Sheet, thêm node **Google Calendar: Create Event** để tự động đưa sự kiện vào lịch cá nhân/team.
- **Đa nguồn dữ liệu**: Nhân bản nhánh HTTP Request + HTML Extract cho nhiều site (Eventbrite + Meetup + Luma) rồi **Merge** lại trước khi ghi Sheet — biến workflow thành "radar sự kiện" toàn diện.
- **Lưu log & báo cáo định kỳ**: Thêm node **Google Sheets** thứ hai để log số lượng sự kiện mỗi lần chạy, hoặc dùng **Schedule Trigger** hàng tuần để gửi email tổng hợp.

### 📌 Kết luận
Với chỉ 5 nodes, workflow **Automated Event Discovery with Bright Data & n8n** biến việc "săn" sự kiện/webinar thủ công thành một quy trình tự động hoàn toàn — chạy nền 24/7, vượt anti-bot, dữ liệu sạch, và lưu trữ tập trung. Các sếp chỉ cần setup một lần, sau đó ngồi uống cà phê và để hệ thống "cày" thay mình.

👉 Đừng quên đăng ký **Bright Data** qua [link này](https://get.brightdata.com/1tndi4600b25) để ủng hộ tác giả Yaron Been — và cài n8n trên [VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (mã **VPSN8N**) để workflow chạy mượt 24/7 nhé!

:::note[Hỗ trợ từ tác giả]
Có thắc mắc gì trong quá trình setup? Liên hệ trực tiếp tác giả workflow:
- 📧 Email: **Yaron@nofluff.online**
- 🎥 YouTube: [@YaronBeen](https://www.youtube.com/@YaronBeen/videos)
- 💼 LinkedIn: [linkedin.com/in/yaronbeen](https://www.linkedin.com/in/yaronbeen/)
:::