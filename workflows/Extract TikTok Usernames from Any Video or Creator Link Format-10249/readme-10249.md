---
title: "🚀 Trích xuất Username TikTok tự động từ mọi định dạng Link Video hoặc Creator"
description: "Hướng dẫn xây dựng workflow n8n tự động phân tích, giải mã và trích xuất chính xác username TikTok từ link rút gọn di động hoặc link đầy đủ không cần code."
slug: "trich-xuat-tiktok-username-tu-dong-n8n"
tags: [n8n, automation, no-code, tiktok, api, scraping]
keywords: [n8n workflow, trích xuất username tiktok, tự động hóa tiktok, tiktok link parser, n8n http request]
---

# 🚀 Trích xuất Username TikTok tự động từ mọi định dạng Link Video hoặc Creator

Các sếp có bao giờ gặp khó khăn khi làm các chiến dịch Marketing, nghiên cứu đối thủ hay xây dựng hệ thống tự động hóa liên quan đến TikTok chưa? Việc lấy đúng **Username (handle)** của một tài khoản thông qua đường dẫn chia sẻ (đặc biệt là link rút gọn `vm.tiktok.com` từ điện thoại) cực kỳ rắc rối. Cắt chuỗi thông thường hay bị lỗi do TikTok dùng rất nhiều định dạng link khác nhau.

Workflow n8n này sinh ra để giải quyết triệt để bài toán đó! Nó giúp tự động phân giải các dạng link rút gọn, xử lý chuyển hướng (redirect) và bóc tách chính xác username sạch sẽ (không chứa dấu `@`) để các sếp đưa vào các kịch bản tự động hóa tiếp theo.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Deskt/VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Xử lý mọi định dạng link:** Tự động nhận diện và bóc tách tốt cả link máy tính (`www.tiktok.com`), link app di động lẫn link rút gọn (`vm.tiktok.com`).
- **Chính xác 100%:** Trích xuất đúng chuẩn Username (ví dụ: `creator_xyz`) không kèm theo ký tự `@` hay các tham số rườm rà phía sau.
- **Giao diện tương tác thân thiện:** Tích hợp sẵn Form nhập link và trả kết quả trực tiếp cho người dùng, hoặc dễ dàng tích hợp ngầm vào hệ thống khác.
- **Tiết kiệm hàng giờ đồng hồ:** Thay vì phải click mở từng link thủ công rồi copy paste, hệ thống xử lý hàng loạt chỉ trong vài giây.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một hệ thống **n8n** đang hoạt động (Cloud hoặc Self-hosted).
- Không cần tài khoản API TikTok phức tạp hay cấu hình phức tạp, workflow sử dụng cơ chế HTTP Request thông minh để giải mã link.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy trực tiếp mã JSON từ hệ thống.
- Trong giao diện n8n Editor, chọn **Add workflow** -> Nhấn tổ hợp `Ctrl + V` (hoặc `Cmd + V`) để dán toàn bộ các nodes vào màn hình làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 12 nodes được bố trí logic từ khâu nhận input đến xử lý và trả kết quả:
- **On form submission (`formTrigger`):** Đây là điểm khởi đầu, cung cấp giao diện web form đơn giản để nhập link TikTok. *Nếu các sếp không dùng form mà muốn nhận link từ Webhook, Telegram hoặc Google Sheets, hãy thay thế node này bằng trigger tương ứng và lưu ý gán giá trị link vào biến `TikTok creator/video link:`.*
- **Get final link of TikTok video (`httpRequest`):** Node cốt lõi thực hiện gọi HTTP Request để "đập" vào link rút gọn (`vm.tiktok.com`), theo dõi quá trình chuyển hướng và lấy ra đường dẫn gốc đầy đủ từ `www.tiktok.com`.
- **Extract username of TikTok creator/video link (`set`):** Sử dụng các biểu thức JavaScript/Regex thông minh để lọc lấy phần tài khoản nằm sau ký tự `@`.
- **Các node xử lý lỗi (If invalid TikTok link, Invalid link, Username is null/empty...):** Giúp bắt các trường hợp người dùng nhập link tào lao, link chết hoặc không quét được username để trả về thông báo lịch sự qua form hoàn tất (`Inform the link is invalid`, `Inform an error retrieving the username`).
- **Display the creator's username (`form`):** Trả kết quả username (`{{ $json.username }}`) lên màn hình hoàn tất cho người dùng. *Các sếp có thể thay đổi đoạn này để đẩy thẳng username vào Google Sheets, Database hoặc gửi thông báo về Slack/Telegram.*

#### 3. Kích hoạt ⚡️
- Nhấn nút **Test workflow** và thử nhập một link TikTok bất kỳ (ví dụ link video từ app điện thoại) vào form để kiểm tra kết quả trả về.
- Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để đưa workflow vào trạng thái vận hành tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng lưu trữ:** Thay vì chỉ hiển thị kết quả ra form, các sếp có thể nối thêm node **Google Sheets** hoặc **Airtable** ngay sau node trích xuất thành công để lưu lại danh sách các creator khách hàng quan tâm.
- **Tích hợp Chatbot:** Thay thế form đầu vào và đầu ra bằng **Telegram Trigger** / **Telegram Bot**, cho phép người dùng gửi link qua chat bot và nhận lại username ngay lập tức.
- **Auto-enrichment:** Kết hợp username vừa lấy được với các workflow cào dữ liệu profile TikTok tiếp theo để tự động phân tích lượng followers, lượt thích của đối thủ cạnh tranh.

### 📌 Kết luận
Với workflow n8n này, bài toán xử lý chuỗi link TikTok rườm rà nay đã được giải quyết gọn gàng trong một nốt nhạc. Hãy import ngay vào hệ thống n8n của các sếp và tự động hóa quy trình ngay hôm nay!