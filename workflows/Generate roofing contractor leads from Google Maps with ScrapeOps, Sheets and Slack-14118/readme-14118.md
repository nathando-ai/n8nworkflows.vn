---
title: "🚀 Tự động quét Lead nhà thầu lợp mái từ Google Maps với ScrapeOps, Google Sheets và Slack"
description: "Hướng dẫn chi tiết cách xây dựng workflow n8n tự động tìm kiếm, cào dữ liệu nhà thầu lợp mái từ Google Maps, lọc trùng lặp và gửi thông báo qua Slack, Gmail."
slug: "tu-dong-quet-lead-nha-thau-lop-mai-google-maps-n8n"
tags: [n8n, automation, lead-generation, google-maps, scrapeops, google-sheets, slack]
keywords: [n8n workflow, cào dữ liệu google maps, scrapeops n8n, tìm kiếm lead tự động, nhà thầu lợp mái]
---

# 🚀 Tự động quét Lead nhà thầu lợp mái từ Google Maps với ScrapeOps, Google Sheets và Slack

Việc tìm kiếm khách hàng tiềm năng (lead generation) trong ngành xây dựng hoặc dịch vụ sửa chữa như thợ lợp mái (roofing contractors) theo phương pháp thủ công cực kỳ tốn thời gian. Các sếp phải mò mẫm trên Google Maps, copy từng số điện thoại, địa chỉ, website và kiểm tra xem đã gọi hay chưa.

Quá trình thủ công này không chỉ chậm chạp mà còn dễ gây sót đơn. Workflow n8n này sinh ra để giải quyết triệt để bài toán đó: **Tự động hóa 100% quy trình tìm kiếm, cào dữ liệu chiều sâu, chống trùng lặp và bắn thông báo ngay lập tức!**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và không lo bị gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Chỉ cần nhập tên thành phố qua một Form, hệ thống tự động lo phần còn lại.
- **Dữ liệu chất lượng cao:** Khai thác sâu tên doanh nghiệp, số điện thoại, website, đánh giá (rating), số lượng review và địa chỉ từ Google Maps nhờ ScrapeOps.
- **Chống trùng lặp thông minh:** Tự động đối chiếu với Google Sheets hiện có để chỉ lưu những lead mới hoàn toàn.
- **Thông báo đa kênh:** Nhận ngay báo cáo chi tiết qua Email (Gmail) và tin nhắn tức thời qua Slack.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản ScrapeOps:** Đăng ký key miễn phí tại [ScrapeOps API Key](https://scrapeops.io/app/register/n8n).
- **Google Sheets:** Chuẩn bị sẵn một file Google Sheet chứa dữ liệu lead cũ (xem template mẫu bên dưới).
- **Tài khoản Gmail & Slack workspace** để cấu hình phần gửi thông báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tạo một workflow mới trên n8n, sau đó copy toàn bộ mã JSON của workflow này và dán trực tiếp vào giao diện n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các node sau trước khi kích hoạt:

- **Form: Enter City to Search (`formTrigger`):** Node này tạo một giao diện Web Form đơn giản để nhập tên thành phố cần quét. Sau khi kích hoạt, n8n sẽ cung cấp một URL công khai để các sếp truy cập điền form.
- **Set Google Maps Configuration (`set`):** Cấu hình từ khóa tìm kiếm (mặc định là "roofing contractor") và các tham số vị trí theo thành phố được nhập từ Form. *Mẹo nhỏ: Các sếp hoàn toàn có thể đổi keyword thành "plumber", "electrician" hay "HVAC contractor" tùy nhu cầu.*
- **ScrapeOps: Search Google Maps & Fetch Business Details (`@scrapeops/n8n-nodes-scrapeops.ScrapeOps`):** Cần điền ScrapeOps API Key vào phần Credentials. Node này đóng vai trò cào danh sách và đi sâu vào từng chi tiết doanh nghiệp mà không sợ bị Google chặn IP.
- **Read Previous Entries from Sheet & Save New Leads to Sheet (`googleSheets`):** Kết nối tài khoản Google Sheets của các sếp qua OAuth2. Trỏ đúng đến file Google Sheet lưu trữ lead (Các sếp có thể tham khảo [Google Sheet template mẫu tại đây](https://docs.google.com/spreadsheets/d/16oOK5vqHRua4e0tSaywCjwVA0tXQN61Tl2PkfQ487pU/edit?gid=0#gid=0)).
- **Send Gmail Alert (`gmail`) & Send Slack Alert (`slack`):** Thêm credentials tương ứng để hệ thống gửi email và tin nhắn thông báo khi có lead mới.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và test thử bằng cách mở Form URL, điền tên một thành phố bất kỳ.
- Kiểm tra xem dữ liệu đã được cào về, lọc trùng và đẩy lên Google Sheets/Slack chưa.
- Nếu mọi thứ chạy mượt mà, gạt công tắc sang **Active** để hệ thống sẵn sàng hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Thay thế Form Trigger:** Nếu không muốn nhập thủ công qua Form, các sếp có thể thay thế bằng *Schedule Trigger* để hệ thống tự động quét các thành phố định kỳ hàng tuần/hàng tháng.
- **Mở rộng kênh thông báo:** Thay vì chỉ dùng Gmail và Slack, các sếp có thể nối thêm node Telegram (`telegram`) để bắn tin nhắn về điện thoại cá nhân nhanh chóng hơn.
- **Lưu log lỗi:** Thêm một nhánh xử lý lỗi (Error Trigger) để nếu ScrapeOps gặp sự cố quá tải, hệ thống sẽ gửi thông báo khẩn về Slack cho các sếp.

### 📌 Kết luận
Workflow này là một "vũ khí" cực mạnh cho các đội ngũ sales và marketing mảng dịch vụ địa phương (local services). Chỉ với vài bước cài đặt đơn giản trên n8n, các sếp đã có thể tự động hóa toàn bộ phễu khai thác khách hàng tiềm năng mà không tốn một đồng chi phí nhân sự cào tay nào. Triển khai ngay thôi các sếp ơi!