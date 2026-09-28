---
title: "🚀 Tìm Sở Thích Ẩn Trên Facebook Ngay Qua Telegram Bằng n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động tìm kiếm các sở thích ẩn (hidden interests) của Facebook qua chatbot Telegram và trả về file Excel tiện lợi."
slug: "tim-so-thich-an-facebook-qua-telegram-voi-n8n"
tags: [n8n, automation, no-code, facebook-ads, telegram, marketing]
keywords: [n8n workflow, facebook hidden interests, facebook graph api, telegram bot n8n, tự động hóa marketing, tìm sở thích facebook ads]
---

# 🚀 Tìm Sở Thích Ẩn Trên Facebook Ngay Qua Telegram Bằng n8n

Các sếp chạy quảng cáo Facebook chắc chắn đều biết rằng việc tìm kiếm các sở thích (interests) tiềm năng và ẩn (hidden interests) là chìa khóa để tối ưu chi phí và bứt phá doanh số. Tuy nhiên, việc tra cứu thủ công trên Ads Manager hoặc các công cụ ngoài vừa tốn thời gian, vừa giới hạn số lượng. 

Giải pháp là đây! Workflow n8n này sẽ giúp các sếp tạo ngay một con **Telegram Bot**. Chỉ cần nhắn từ khóa vào bot, hệ thống sẽ tự động gọi **Facebook Graph API** để khai thác toàn bộ các sở thích liên quan (bao cả sở thích ẩn), tổng hợp lại thành file Excel gọn gàng và gửi ngược lại cho các sếp ngay trên Telegram. Tất cả tự động 100%, không cần code phức tạp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và sẵn sàng nhận yêu cầu từ Telegram bất cứ lúc nào, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không cần mở trình quản lý quảng cáo hay các tool phức tạp, tra cứu trực tiếp qua chat Telegram nhanh như chớp.
- **Khai thác sở thích ẩn:** Tận dụng Facebook Graph API để tìm ra những tệp khách hàng ngách mà đối thủ chưa biết tới.
- **Báo cáo trực quan:** Tự động đóng gói dữ liệu thành file spreadsheet và gửi trực tiếp về Telegram để các sếp dễ dàng phân tích, lọc tệp.
- **Hoạt động 24/7:** Bot luôn sẵn sàng phục vụ bất cứ lúc nào các sếp cần lên camp quảng cáo.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt sẵn n8n (Self-hosted hoặc Cloud).
- **Telegram Bot:** Tạo một bot miễn phí thông qua `@BotFather` trên Telegram để lấy **Telegram API Token**.
- **Facebook Developer Account:** Cần cấu hình ứng dụng trên Facebook Developers và lấy API Key/Access Token để kết nối với **Facebook Graph API**. (Xem hướng dẫn chi tiết tại [Facebook API Setup Docs](https://developers.facebook.com/docs/commerce-platform/setup/api-setup/)).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow (hoặc tải file JSON từ n8n template) và dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, hệ thống sẽ hiển thị 10 nodes. Các sếp cần tập trung cấu hình các điểm mấu chốt sau:

- **Get interest name (`telegramTrigger`):** 
  - Kết nối với tài khoản Telegram của các sếp bằng **Telegram API Credentials**.
  - Node này đóng vai trò lắng nghe tin nhắn chứa từ khóa sở thích mà các sếp gửi vào bot.
- **Check message contents & Extract message (`if` & `code`):** 
  - Các node này làm nhiệm vụ lọc và bóc tách nội dung tin nhắn để đảm bảo bot chỉ xử lý các từ khóa hợp lệ.
- **Connect to Graph API (`facebookGraphApi`):** 
  - Sử dụng **Facebook Graph API Credentials** để xác thực. Các sếp cần điền Access Token đã lấy từ tài khoản Facebook Developer để hệ thống có quyền truy vấn dữ liệu sở thích.
- **Split Interests into a Table & Get variables (`code`):** 
  - Các node xử lý bằng mã JavaScript có sẵn giúp định dạng, lọc và chuyển đổi dữ liệu thô từ Facebook thành dạng bảng (table) sạch sẽ.
- **Create a Spreadsheet (`spreadsheetFile`):** 
  - Thiết lập thao tác chuyển đổi dữ liệu thành file (`toFile`) để chuẩn bị gửi đi.
- **Send the Spreadsheet file (`telegram`):** 
  - Sử dụng lại **Telegram API Credentials** để gửi file tài liệu (`sendDocument`) ngược lại khung chat Telegram cho các sếp.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** và gửi thử một từ khóa (ví dụ: `Digital Marketing`) vào bot Telegram của các sếp để test xem hệ thống phản hồi file có chuẩn chỉnh không.
- Nếu mọi thứ mượt mà, hãy gạt công tắc sang **Active** để bật bot chạy 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng lưu trữ:** Thay vì chỉ nhận file qua Telegram, các sếp có thể nối thêm node Google Sheets để lưu trữ toàn bộ lịch sử tìm kiếm sở thích vào một bảng tính chung của team marketing.
- **Thông báo nhóm:** Thêm node Telegram phụ để gửi thông báo vào nhóm chat chung của team mỗi khi có thành viên tra cứu sở thích mới, giúp team cùng cập nhật ý tưởng content/ads.
- **Xử lý đa ngôn ngữ:** Tinh chỉnh các node code bên trong để bot có khả năng tự động dịch từ khóa tiếng Việt sang tiếng Anh trước khi gọi Facebook Graph API nhằm trả về kết quả phong phú hơn.

### 📌 Kết luận
Workflow **Find Facebook Hidden Interests via Telegram** là một trợ lý đắc lực giúp các nhà quảng cáo tối ưu hóa quy trình nghiên cứu thị trường và tìm kiếm tệp khách hàng ngách. Hãy cài đặt ngay hôm nay để biến chiếc điện thoại của các sếp thành một trung tâm điều khiển chiến dịch quảng cáo thông minh!