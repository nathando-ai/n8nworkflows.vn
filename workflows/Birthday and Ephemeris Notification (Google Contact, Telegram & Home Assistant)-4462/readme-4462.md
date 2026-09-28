---
title: "🎂 Tự Động Chúc Mừng Sinh Nhật & Thánh Lễ Hàng Ngày Với n8n"
description: "Workflow n8n tự động kiểm tra danh bạ Google, đối chiếu với API Nominis để gửi tin nhắn Telegram và điều khiển loa Home Assistant chúc mừng sinh nhật bạn bè, người thân mỗi sáng."
slug: "tu-dong-chuc-mung-sinh-nhat-telegram-home-assistant"
tags: [n8n, automation, no-code, telegram, home-assistant, google-contacts]
keywords: [n8n workflow, tự động hóa sinh nhật, telegram bot, home assistant, google contacts api]
---

# 🎂 Tự Động Chúc Mừng Sinh Nhật & Thánh Lễ Hàng Ngày Với n8n

Các sếp có bao giờ cảm thấy áy náy vì quên chúc mừng sinh nhật bạn bè, đồng nghiệp hay người thân không? Hay đơn giản là muốn có một "trợ lý ảo" tinh tế, mỗi sáng sẽ gửi đến các sếp một tin nhắn chúc mừng sinh nhật cho những ai có ngày sinh nhật trùng hôm nay, kèm theo thông tin về vị Thánh bảo trợ của ngày đó (nếu có)?

Làm việc này thủ công mỗi ngày là một gánh nặng tâm lý và dễ bỏ sót. Workflow **"Birthday and Ephemeris Notification"** này giải quyết triệt để vấn đề đó. Nó hoạt động hoàn toàn tự động, không cần code, kết nối liền mạch giữa **Google Contacts**, **API Nominis** (dữ liệu Thánh lễ), **Telegram** và **Home Assistant**. Mỗi sáng, nó sẽ quét danh bạ, tìm ra người sinh nhật, soạn tin nhắn cá nhân hóa và gửi đi, thậm chí còn có thể phát tiếng chúc mừng qua loa thông minh nhà các sếp.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Không bao giờ quên sinh nhật:** Hệ thống tự động quét danh bạ Google và gửi lời chúc đúng ngày, đúng người.
- **Cá nhân hóa sâu sắc:** Tin nhắn không chỉ là "Chúc mừng sinh nhật" mà còn kèm theo tên Thánh bảo trợ của ngày hôm đó (nếu tên người nhận trùng với tên Thánh), tạo sự tinh tế và ý nghĩa.
- **Đa kênh thông báo:** Gửi tin nhắn qua Telegram và đồng thời điều khiển Home Assistant (ví dụ: phát nhạc chúc mừng qua loa Google Home/Sonos).
- **Hoạt động tự động 100%:** Chạy theo lịch trình (mỗi sáng 7h), không cần can thiệp thủ công, tiết kiệm thời gian quản lý quan hệ.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị các tài khoản và credentials sau:
1.  **Tài khoản Google:** Đã kết nối với n8n (OAuth2) để truy cập **Google Contacts**.
2.  **Tài khoản Telegram:**
    *   Tạo Bot qua @BotFather để lấy **Bot Token**.
    *   Lấy **Chat ID** của kênh hoặc cá nhân nhận tin nhắn.
3.  **Tài khoản Home Assistant:**
    *   Tạo Long-Lived Access Token trong Home Assistant.
    *   Xác định tên thiết bị loa (entity_id) muốn điều khiển (ví dụ: `media_player.google_home_kitchen`).
4.  **API Nominis:** Workflow sử dụng API công khai của Nominis (Catholic Ephemeris) để lấy dữ liệu Thánh lễ. Các sếp không cần API key riêng cho phần này, chỉ cần đảm bảo n8n có quyền truy cập HTTP Request.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ link gốc [n8n.io/workflows/4462](https://n8n.io/workflows/4462) hoặc copy toàn bộ JSON code.
*   Mở n8n Editor.
*   Chọn **Import from URL** hoặc **Import from File**.
*   Dán JSON vào và nhấn **Import**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình lại các node sau để workflow chạy đúng với dữ liệu của mình:

*   **Node "Everyday at 7am" (Schedule Trigger):**
    *   Mặc định chạy lúc 7:00 sáng. Các sếp có thể chỉnh giờ theo múi giờ địa phương hoặc thời điểm mong muốn (ví dụ: 8:00 sáng để mọi người đã thức dậy).

*   **Node "Google Contacts":**
    *   Chọn **Credentials** đã kết nối với tài khoản Google của các sếp.
    *   Đảm bảo quyền truy cập vào danh bạ (Contacts).

*   **Node "Sent Telegram Message" (Telegram):**
    *   Chọn **Credentials** chứa Bot Token của Telegram.
    *   Ở trường **Chat ID**, điền ID của kênh hoặc cá nhân mà các sếp muốn nhận tin nhắn.
    *   *Lưu ý:* Nếu gửi cho nhiều người, các sếp có thể cần thêm logic để lặp qua danh sách Chat ID, nhưng workflow gốc thường thiết kế để gửi cho một kênh chung hoặc một cá nhân quản lý.

*   **Node "Send to Google Home Speaker" (Home Assistant):**
    *   Chọn **Credentials** chứa Long-Lived Access Token của Home Assistant.
    *   Ở phần **Service**, chọn `media_player` và **Service Data** là `play_media` hoặc `announce`.
    *   Điền **Entity ID** của loa thông minh (ví dụ: `media_player.living_room_speaker`).
    *   *Tùy chọn:* Có thể thay đổi nội dung phát (ví dụ: phát một bài hát chúc mừng sinh nhật cụ thể thay vì chỉ thông báo).

*   **Node "Check if any firstname match a Saints of the day" (Code):**
    *   Node này xử lý logic đối chiếu tên trong danh bạ với danh sách Thánh của ngày hôm nay từ API Nominis.
    *   Các sếp **không cần** sửa code này trừ khi muốn thay đổi logic đối chiếu (ví dụ: chỉ đối chiếu với một số tên cụ thể, hoặc thêm tên tiếng Việt).
    *   *Mẹo:* Nếu các sếp muốn hỗ trợ tên tiếng Việt, cần sửa phần code trong node này để thêm mapping tên tiếng Việt sang tên Thánh (ví dụ: "An" -> "Anne", "Minh" -> "Minh" nếu có Thánh Minh, v.v.).

*   **Node "Compose Message" & "Birthday celebration message":**
    *   Đây là các node Set dùng để soạn nội dung tin nhắn.
    *   Các sếp có thể chỉnh sửa văn bản trong các node này để thay đổi giọng văn, thêm emoji, hoặc thay đổi cách xưng hô (ví dụ: từ "Bạn" sang "Anh/Chị").
    *   Đảm bảo các biến `{{ $json.firstName }}` và `{{ $json.saintName }}` được giữ nguyên để workflow điền dữ liệu động.

#### 3. Kích hoạt ⚡️
1.  **Test Run:** Nhấn nút **Execute Workflow** để chạy thử. Kiểm tra xem có tin nhắn nào được gửi qua Telegram không (nếu hôm nay không có sinh nhật, workflow có thể không gửi gì hoặc gửi thông báo "Không có sinh nhật hôm nay" tùy cấu hình).
2.  **Kiểm tra Home Assistant:** Nếu có sinh nhật, kiểm tra xem loa Home Assistant có phát tiếng không.
3.  **Bật Active:** Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để workflow chạy tự động theo lịch trình.

### ✍️ Mẹo & gợi ý nâng cao
*   **Tích hợp thêm Email:** Thêm một node **Gmail** hoặc **SMTP** để gửi email chúc mừng song song với Telegram, đảm bảo không bỏ lỡ ai đó không dùng Telegram.
*   **Cá nhân hóa theo nhóm:** Tạo các danh sách riêng trong Google Contacts (ví dụ: "Gia đình", "Bạn bè thân", "Đồng nghiệp") và tạo các luồng xử lý khác nhau với giọng văn khác nhau cho từng nhóm.
*   **Lưu log lịch sử:** Thêm một node **Google Sheets** hoặc **Airtable** để lưu lại lịch sử các lần chúc mừng, giúp các sếp theo dõi và tránh gửi trùng lặp nếu có lỗi.
*   **Tùy biến Thánh lễ:** Nếu các sếp không quan tâm đến yếu tố Công giáo, có thể bỏ qua phần API Nominis và chỉ giữ lại phần chúc mừng sinh nhật thông thường. Hoặc thay bằng API dự báo thời tiết để gửi lời chúc kèm theo thời tiết hôm nay.

### 📌 Kết luận
Workflow **"Birthday and Ephemeris Notification"** là một ví dụ tuyệt vời về cách n8n có thể biến những tác vụ nhỏ nhưng quan trọng trong cuộc sống thành những quy trình tự động hóa tinh tế. Với sự kết hợp giữa dữ liệu danh bạ, API bên thứ ba và các nền tảng thông báo phổ biến, các sếp có thể duy trì mối quan hệ tốt đẹp với bạn bè, người thân mà không tốn chút công sức nào. Hãy import và tùy chỉnh ngay hôm nay để trải nghiệm sự khác biệt!