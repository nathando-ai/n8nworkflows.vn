---
title: "🚀 Tự động tổng hợp và bắn tin RSS từ nhiều nguồn lên Telegram với n8n"
description: "Hướng dẫn cài đặt workflow n8n tự động đọc tin tức từ nhiều RSS feed khác nhau, lọc tin mới và phân loại gửi thẳng vào các kênh Telegram tương ứng."
slug: "tu-dong-tong-hop-rss-feed-len-telegram-n8n"
tags: [n8n, automation, no-code, rss, telegram, content-curation]
keywords: [n8n workflow, rss to telegram, tự động hóa đọc báo, n8n rss feed, bot telegram tự động]
---

# 🚀 Tự động tổng hợp và bắn tin RSS từ nhiều nguồn lên Telegram với n8n

Việc phải mở hàng chục trang web, blog công nghệ hay các trang tin tức mỗi ngày để cập nhật thông tin thủ công tốn rất nhiều thời gian. Nếu các sếp đang làm mảng quản trị hệ thống, an ninh mạng hay IT và cần theo dõi sát sao tin tức từ nhiều nguồn RSS khác nhau, việc này cực kỳ áp dụng tốn công sức.

Giải pháp là đây! Workflow n8n này sẽ tự động hóa 100% quy trình: gom tin từ nhiều nguồn RSS, thông minh lọc ra các bài viết hoàn toàn mới, sau đó tự động phân loại và gửi thẳng vào các nhóm/channel Telegram tương ứng (IT, Security, M365...) mà không cần các sếp phải động tay.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hoàn toàn 24/7:** Không bỏ lỡ bất kỳ bản tin nóng hay cập nhật quan trọng nào nhờ lịch chạy tự động từ node Cron.
- **Phân loại thông minh:** Tự động chia luồng tin tức (IT, Bảo mật, Microsoft 365...) và bắn thẳng đến đúng channel Telegram chuyên biệt.
- **Chống trùng lặp hiệu quả:** Node lọc thông minh chỉ lấy các bài viết mới xuất bản, tránh làm phiền người dùng bằng tin cũ.
- **Tiết kiệm thời gian:** Thay vì mất hàng giờ lướt web cập nhật tin tức, mọi thứ đã được gom gọn gàng ngay trên ứng dụng Telegram quen thuộc.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt sẵn sàng (Self-hosted hoặc Cloud).
- **Telegram Bot:** Đã tạo Bot qua [@BotFather](https://t.me/BotFather) và lấy Token API.
- **Telegram Chat/Channel ID:** Các nhóm hoặc kênh mà bot đã được thêm vào với quyền gửi tin nhắn.
- **Danh sách nguồn RSS:** Các URL RSS/Atom feed mà các sếp muốn theo dõi (IT, Security, M365...).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Các sếp sao chép mã JSON của workflow hoặc tải file JSON từ nguồn cung cấp.
- Trong giao diện n8n Editor, chọn **Add workflow** -> **Import from File** hoặc dán trực tiếp JSON vào màn hình làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà theo đúng nhu cầu, các sếp cần cấu hình kỹ các node sau:

- **Cron:** Thiết lập lịch chạy tự động (ví dụ: chạy mỗi 30 phút hoặc 1 tiếng một lần quét tin mới).
- **RSS Source & RSS Feed Read:** 
  - Khai báo danh sách các đường dẫn RSS URL tại node **RSS Source** (sử dụng JavaScript code để định nghĩa các nguồn).
  - Cấu hình node **RSS Feed Read** để đọc dữ liệu từ các nguồn đã khai báo.
- **only get new RSS & Clear Function:** Các hàm JavaScript tùy chỉnh giúp lưu trạng thái, so sánh và lọc bỏ các bài viết cũ đã gửi ở các lần chạy trước.
- **IF-1 & IF-2:** Các node điều kiện dùng để phân loại chủ đề bài viết dựa trên từ khóa hoặc nguồn RSS để đẩy vào đúng nhánh xử lý.
- **Telegram_IT, Telegram_Security, Telegram_M365:** 
  - Kết nối với tài khoản Telegram thông qua **Telegram API Credentials** (nhập Bot Token).
  - Điền chính xác `Chat ID` của từng channel/group tương ứng vào phần cấu hình của node.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Test workflow** để chạy thử nghiệm xem dữ liệu từ RSS có đổ về Telegram thành công hay không.
- Nếu mọi thứ hoạt động trơn tru, gạt công tắc sang chế độ **Active** để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh nhận tin:** Các sếp có thể tích hợp thêm node **Slack**, **Discord** hoặc **Zalo ZNS** nếu muốn đồng thời thông báo tin tức đến các nền tảng chat khác trong doanh nghiệp.
- **Lưu trữ lịch sử:** Kết nối thêm node **Google Sheets** hoặc **Notion** để lưu lại toàn bộ các bản tin đã gửi, tạo thành một thư viện kiến thức cá nhân hoặc nội bộ.
- **Tóm tắt bằng AI:** Thêm node **OpenAI (ChatGPT)** hoặc **Anthropic (Claude)** trước bước gửi Telegram để AI tự động tóm tắt ngắn gọn nội dung bài viết thay vì chỉ gửi tiêu đề và link gốc.

### 📌 Kết luận
Workflow "Get data from multiple RSS feeds to Telegram" là một công cụ cực kỳ hữu ích giúp tối ưu hóa thời gian cập nhật thông tin hàng ngày. Chỉ với vài bước cấu hình đơn giản trên n8n, các sếp đã sở hữu ngay một trợ lý AI thông minh tự động đọc báo và gom tin tức về máy. Chúc các sếp cài đặt thành công!