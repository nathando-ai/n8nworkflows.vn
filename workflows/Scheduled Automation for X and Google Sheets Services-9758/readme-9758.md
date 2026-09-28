---
title: "🤖 Tự Động Hóa X (Twitter) & Google Sheets: Like & Repost Tweet Theo Lịch Trình - Giúp Các Sếp Tiết Kiệm 100+ Giờ/Năm"
description: "Workflow tự động hóa 100% không code giúp các sếp đọc danh sách tài khoản từ Google Sheets, tìm tweet mới nhất, và tự động like/repost theo lịch trình hàng giờ/hàng ngày - tiết kiệm thời gian, tăng tương tác mà không lo bị spam."
slug: "tu-dong-hoa-x-google-sheets-like-repost-tweet"
tags: [n8n, automation, twitter-bot, google-sheets, no-code, social-media]
keywords: [tự động hóa twitter, like tweet tự động, repost tweet tự động, n8n workflow twitter, tự động hóa mạng xã hội, google sheets api]
---

# 🚀 **Tự Động Hóa X (Twitter) & Google Sheets: Like & Repost Tweet Theo Lịch Trình**

### **Giải pháp cho các sếp muốn:**
- **Tiết kiệm 100+ giờ/năm** để tương tác với khách hàng, đối tác hoặc nội dung quan trọng.
- **Tăng tương tác tự động** mà không cần phải ngồi trước màn hình.
- **Quản lý nhiều tài khoản X (Twitter)** từ một bảng Google Sheets duy nhất.
- **Tránh bị spam hoặc bị chặn** nhờ giới hạn số lượng hành động và kiểm soát API.

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Tự động like/repost tweet mới nhất của khách hàng/đối tác hàng giờ/hàng ngày.
✅ **Tương tác cá nhân hóa**: Tăng độ tương tác với nội dung quan trọng mà không mất thời gian.
✅ **Quản lý tập trung**: Đọc danh sách tài khoản từ Google Sheets, không cần cập nhật thủ công.
✅ **An toàn API**: Giới hạn số lượng hành động để tránh bị chặn hoặc bị spam.
✅ **Hoạt động liên tục**: Chạy 24/7 trên VPS riêng, không phụ thuộc vào thiết bị cá nhân.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
- **Tài khoản X (Twitter) OAuth2**:
  - Đăng ký ứng dụng trên [Twitter Developer Portal](https://developer.twitter.com/) và lấy **API Key + API Secret + Access Token + Access Token Secret**.
  - Cài đặt **Credentials** trong n8n với tên `twitter_credentials` (hoặc tùy chỉnh).
- **Google Sheets OAuth2**:
  - Tạo một Google Sheet chứa danh sách tài khoản (xem cấu trúc dưới đây).
  - Cài đặt **Credentials** trong n8n với tên `google_sheets_credentials`.
- **Bảng Google Sheets**:
  - **Cột bắt buộc**: `account_id` (không có ký tự `@`, ví dụ: `tên_tài_khoản`).
  - **Cột tùy chọn** (nếu muốn mở rộng sau này):
    - `blocked_words`: Danh sách từ bị chặn (ví dụ: "spam", "promo").
    - `last_processed_at`: Thời gian tweet cuối cùng đã xử lý (để tránh trùng lặp).
- **VPS Self-hosted** (khuyến nghị):
  - Để workflow chạy 24/7 ổn định, các sếp nên cài n8n trên VPS riêng.
  - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
  - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Truy cập [n8n.io](https://n8n.io/) và đăng nhập vào workspace của mình.
2. Nhấp vào **"Create"** → **"Import"** và chọn file JSON đã tải xuống từ [link gốc](https://n8n.io/workflows/9758).
   *Hoặc* copy toàn bộ JSON từ [đây](https://n8n.io/workflows/9758) và nhấp **"Import from JSON"** trong Editor.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **6 node chính**, các sếp cần cấu hình kỹ lưỡng như sau:

#### **🔹 Node 1: Schedule Trigger (Lịch trình)**
- **Cài đặt**:
  - **Cadence**: Chọn **hourly** (mỗi giờ) hoặc **daily** (hàng ngày) tùy nhu cầu.
  - **Time**: Đặt thời gian chạy vào giờ không cao điểm (ví dụ: 3h sáng) để tránh bị giới hạn API.
  - **Test run**: Trong giai đoạn thử nghiệm, các sếp có thể nhấp **"Execute Workflow"** thủ công để kiểm tra.

#### **🔹 Node 2: Read accounts from Google Sheets (Đọc danh sách tài khoản)**
- **Cấu hình**:
  - **Credentials**: Chọn `google_sheets_credentials` (đã cài đặt trước).
  - **Document ID**: Thay thế bằng `documentId` của Google Sheet của các sếp (tìm trong URL của sheet: `https://docs.google.com/spreadsheets/d/[DOCUMENT_ID]/edit`).
  - **Sheet Name**: Tên của sheet (ví dụ: `Sheet1`).
  - **Header Row**: Chọn hàng chứa tiêu đề (thường là hàng 1).
  - **Required Columns**:
    - `account_id` (bắt buộc): Tên tài khoản X (không có `@`).
    - `blocked_words` (tùy chọn): Danh sách từ bị chặn (nếu có).
  - **Lưu ý**:
    - Nếu sheet có nhiều hàng, workflow sẽ xử lý từng tài khoản một.
    - Các sếp có thể thêm cột `last_processed_at` để lưu thời gian tweet cuối cùng đã like/repost (mở rộng sau này).

#### **🔹 Node 3: Get latest tweets (Lấy tweet mới nhất)**
- **Cấu hình**:
  - **Credentials**: Chọn `twitter_credentials`.
  - **Query**: Sử dụng cú pháp:
    ```
    from:{{$node["Read accounts from Google Sheets"].json["account_id"]}} -is:retweet -is:reply
    ```
    - `$node["Read accounts from Google Sheets"].json["account_id"]` sẽ tự động lấy giá trị từ cột `account_id` trong Google Sheets.
    - `-is:retweet -is:reply` loại bỏ tweet đã retweet hoặc reply.
  - **Tweet Fields**: Thêm `tweet.fields=created_at` để sắp xếp tweet theo thời gian mới nhất.
  - **Limit**: Giới hạn số tweet lấy về (ví dụ: 5 tweet mới nhất).

#### **🔹 Node 4: Limit (Giới hạn hành động)**
- **Cấu hình**:
  - **Limit**: Đặt số lượng tweet sẽ like/repost (khuyến nghị **1-3 tweet/ngày** để tránh bị spam).
  - **Lưu ý**:
    - Nếu quá nhiều tweet được xử lý cùng một lúc, Twitter có thể chặn tài khoản.
    - Các sếp có thể điều chỉnh giới hạn theo thời gian (ví dụ: 1 tweet/ngày cho tài khoản quan trọng).

#### **🔹 Node 5: Like tweet (Like tweet)**
- **Cấu hình**:
  - **Credentials**: Chọn `twitter_credentials`.
  - **Tweet ID**: Lấy từ node `Get latest tweets`.
  - **Dry-run (tùy chọn)**: Nếu muốn thử trước, các sếp có thể thêm node **Set** để đặt flag `dry_run: true` và sử dụng node **IF** để chỉ chạy like/repost khi `dry_run` là `false`.

#### **🔹 Node 6: Repost tweet (Repost tweet)**
- **Cấu hình**:
  - **Credentials**: Chọn `twitter_credentials`.
  - **Tweet ID**: Lấy từ node `Get latest tweets`.
  - **Lưu ý**:
    - Tránh repost quá nhiều tweet trong một thời gian ngắn.
    - Các sếp có thể thêm **cooldown** (thời gian chờ) giữa các hành động bằng cách sử dụng node **Set** + **Delay**.

---
### **3. Kích hoạt ⚡️**
1. **Test run**:
   - Chạy workflow với **dry-run** (nếu có) để kiểm tra không có lỗi.
   - Kiểm tra log trong node `Get latest tweets` và `Like tweet` để đảm bảo tweet được lấy và like/repost đúng.
2. **Bật Active**:
   - Sau khi kiểm tra thành công, nhấp **"Active"** để workflow chạy tự động theo lịch trình.

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::info[CẬP NHẬT & MỞ RỘNG]
- **Thêm Slack/Telegram Notifications**:
  - Sử dụng node **Slack** hoặc **Telegram Bot** để thông báo khi like/repost thành công/bất thành công.
  - Ví dụ: Gửi tin nhắn `"Đã like/repost tweet của @account_id"` khi workflow hoàn thành.
- **Lưu log vào Google Sheets**:
  - Thêm node **Google Sheets** sau node `Repost tweet` để ghi lại lịch sử hoạt động (tweet ID, thời gian, status).
  - Cấu trúc cột: `tweet_id`, `account_id`, `timestamp`, `status` (success/fail).
- **Phân loại tweet theo từ khóa**:
  - Sử dụng node **Code** hoặc **IF** để lọc tweet chứa từ khóa cụ thể (ví dụ: "sale", "promo") trước khi like/repost.
- **Chỉnh lịch trình theo ngày trong tuần**:
  - Sử dụng node **Schedule Trigger** với lịch trình phức tạp (ví dụ: chỉ chạy từ thứ 2 đến thứ 6).
- **Dry-run mode**:
  - Thêm node **Set** để đặt flag `dry_run: true` và sử dụng node **IF** để chỉ chạy like/repost khi `dry_run` là `false`.
  - Cách này giúp các sếp kiểm tra workflow mà không thực sự like/repost tweet.
:::

---
## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa tương tác trên X (Twitter) mà không cần viết code. Bằng cách kết hợp **Google Sheets** và **n8n**, các sếp có thể:
✔ **Quản lý nhiều tài khoản** từ một nơi duy nhất.
✔ **Tiết kiệm thời gian** để tập trung vào công việc quan trọng hơn.
✔ **Tránh bị spam** nhờ giới hạn hành động và kiểm soát API.

**Hành động ngay!**
1. **Cài đặt n8n trên VPS** (nếu chưa có).
2. **Import workflow** và cấu hình các credentials.
3. **Test run** và bật chế độ **Active**.
4. **Mở rộng** với các tính năng nâng cao như Slack notifications hoặc log vào Google Sheets.

👉 **Bắt đầu tự động hóa ngay hôm nay!** Nếu có thắc mắc, các sếp có thể comment bên dưới hoặc liên hệ với cộng đồng n8n trên [Discord](https://n8n.io/community).