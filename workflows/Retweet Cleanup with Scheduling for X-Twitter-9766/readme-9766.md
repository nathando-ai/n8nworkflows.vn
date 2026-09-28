---
title: "🧹 **Tự Động Xóa Retweet Trên X (Twitter) Với Lịch Trình Hóa – Giúp Profile Luôn Sạch Đẹp & Hiệu Quả**"
description: "Workflow tự động hóa xóa retweet cũ trên X (Twitter) theo lịch trình hàng ngày, giúp quản lý nội dung, duy trì hình ảnh thương hiệu và tiết kiệm thời gian cho các sếp marketing. Hoạt động 24/7, tuân thủ giới hạn API, và có thể kết nối với Slack để báo cáo."
slug: "tieu-dong-xoa-retweet-x-twitter-voi-lich-trinh-hoa"
tags: [n8n, automation, social-media, x-twitter, no-code]
keywords: [tự động hóa xóa retweet twitter, workflow n8n twitter, tự động hóa xóa retweet hàng ngày, quản lý nội dung x, tự động hóa marketing social media]
---

# 🚀 **Tự Động Xóa Retweet Trên X (Twitter) – Giải Pháp Tối Ưu Cho Quản Lý Nội Dung Hàng Ngày**

### **Nỗi Đau Của Các Sếp Marketing & Quản Lý Mạng Xã Hội**
Làm thế nào để giữ cho **profile X (Twitter) của bạn luôn sạch sẽ, chuyên nghiệp và tập trung vào nội dung chính?** Retweets cũ, quảng cáo tạm thời, hoặc nội dung không phù hợp có thể làm **làm mất uy tín thương hiệu**, **giảm độ tương tác** và **làm phức tạp việc quản lý nội dung**.

Với **Retweet Cleanup Workflow**, các sếp có thể:
✅ **Xóa tự động retweets cũ** sau mỗi chiến dịch hoặc theo lịch trình định kỳ.
✅ **Duy trì feed X sạch sẽ**, tập trung vào nội dung mới và có giá trị.
✅ **Tiết kiệm thời gian** bằng cách loại bỏ công việc thủ công hàng ngày.
✅ **Tuân thủ giới hạn API** của X (Twitter) với cơ chế batching và delay an toàn.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**Lợi Ích Cốt Lõi**]
- **Profile X luôn chuyên nghiệp**: Loại bỏ retweets cũ, quảng cáo tạm thời, hoặc nội dung không phù hợp.
- **Tiết kiệm thời gian**: Không cần phải kiểm tra và xóa retweets thủ công hàng ngày.
- **Tự động hóa hoàn toàn**: Hoạt động 24/7 theo lịch trình, không cần can thiệp.
- **An toàn với API**: Tuân thủ giới hạn gọi API của X (Twitter) bằng cách chia nhỏ batch và thêm delay.
- **Kết nối với Slack/Email**: Nhận báo cáo và cảnh báo lỗi nếu có.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[**Chuẩn Bị Trước Khi Bắt Đầu**]
Để workflow này hoạt động, các sếp cần:
1. **Tài khoản X (Twitter) với API Access**:
   - Tạo một **X Developer App** và cấp quyền:
     - `Read: Tweets` (đọc tweet của bạn)
     - `Write: Tweets` (xóa retweet của bạn)
   - [Hướng dẫn tạo OAuth2 cho X API](https://developer.twitter.com/en/docs/authentication/oauth-2-0/user-access-token)
   - **Lưu ý**: **Không bao giờ** đặt token API trực tiếp trong node, mà sử dụng **Credentials** trong n8n.

2. **n8n Self-hosted (khuyến nghị)**:
   - Để workflow chạy 24/7 ổn định, các sếp nên cài đặt n8n trên **VPS riêng** (Self-hosted).
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)

3. **Tham số cấu hình cơ bản**:
   - **Tên tài khoản X (Twitter)**: Ví dụ `yourhandle` (không cần `@`).
   - **Số lượng tweet lấy**: Từ 10 đến 100 (mặc định 50).
   - **Thời gian chờ giữa batch**: Để tránh bị chặn API (mặc định 1 phút).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/9766](https://n8n.io/workflows/9766) hoặc copy/paste JSON vào **n8n Editor**.
- **Cách import**:
  1. Mở **n8n Editor** → Nhấn **Import** → Chọn file JSON.
  2. Hoặc **Copy JSON** → Nhấn **Import** → Dán vào ô JSON.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **12 node**, nhưng các bước quan trọng nhất cần chú ý:

##### **🔹 Node 1: TRIGGER | Schedule (09:00 server time)**
- **Mục đích**: Khởi động workflow hàng ngày lúc 9h (theo giờ máy chủ).
- **Cách chỉnh**:
  - Nhấn vào node → Tab **Settings** → Chỉnh **Schedule** theo nhu cầu (ví dụ: `0 0 9 * * ?` cho 9h sáng hàng ngày).
  - **Lưu ý**: Để test, có thể chạy **manual run** một lần trước khi bật **Active**.

##### **🔹 Node 2: CONFIG | User Variables (Set Fields)**
- **Mục đích**: Cấu hình các tham số chính như `target_username`, `max_results`, `batch_delay_minutes`.
- **Cách chỉnh**:
  ```json
  {
    "target_username": "yourhandle",  // Thay bằng tên tài khoản X của bạn (không có @)
    "max_results": 50,                // Số tweet lấy (tối đa 100)
    "batch_delay_minutes": 1         // Thời gian chờ giữa batch (để tránh bị chặn API)
  }
  ```
  - **Lưu ý**: **Không chỉnh sửa trực tiếp trong node**, mà sử dụng **Credentials** để tránh lộ token.

##### **🔹 Node 3 & 4: FETCH | Get user ID by username & FETCH | Latest tweets**
- **Mục đích**: Lấy ID tài khoản và danh sách tweet gần đây.
- **Cách chỉnh**:
  - Trong **HTTP Request nodes**, chọn **Credentials** (OAuth2) đã tạo trước đó.
  - **Không điền token API trực tiếp** vào node, mà sử dụng **Credentials** để an toàn.
  - **Endpoint**:
    - `GET /2/users/by/username/{username}` → Lấy ID tài khoản.
    - `GET /2/users/{id}/tweets?tweet.fields=created_at,referenced_tweets` → Lấy tweet gần đây.

##### **🔹 Node 5: SPLIT | One item per tweet**
- **Mục đích**: Chia danh sách tweet thành các item riêng lẻ để xử lý.
- **Lưu ý**: Nếu API trả về cấu trúc khác, cần chỉnh `fieldToSplitOut` phù hợp.

##### **🔹 Node 6: IF | Is retweet?**
- **Mục đích**: Lọc chỉ giữ retweet (`referenced_tweets.type = "retweeted"`).
- **Cách chỉnh**:
  - **Condition**: `$json.referenced_tweets ? $json.referenced_tweets[0].type : ''` **equals** `retweeted`.
  - **Lưu ý**: Nếu muốn lọc **reply/quote**, chỉnh condition tương ứng.

##### **🔹 Node 7 & 8: LOOP | Split in batches & WAIT | Delay between API calls**
- **Mục đích**: Chia tweet thành batch nhỏ và thêm delay để tránh bị chặn API.
- **Cách chỉnh**:
  - **Split in batches**: Chỉnh số lượng tweet trong mỗi batch (ví dụ: 10 tweet/lần).
  - **WAIT**: Sử dụng `batch_delay_minutes` từ CONFIG (mặc định 1 phút).

##### **🔹 Node 9: SEND | Unretweet (delete retweet)**
- **Mục đích**: Xóa retweet của bạn (không ảnh hưởng đến tweet gốc).
- **Cách chỉnh**:
  - Chọn **Twitter Credential** (OAuth2) đã cấu hình.
  - **Operation**: `delete`.
  - **Input**: `$json.id` (ID của tweet cần xóa).
  - **Lưu ý**:
    - Nếu tweet **không phải retweet**, API sẽ trả về lỗi 404.
    - Nếu không có quyền `Write: Tweets`, API trả về lỗi 403.

##### **🔹 Node 10 & 11: NOTIFY | Slack (optional) & ON ERROR | Capture**
- **Mục đích**:
  - **Slack**: Gửi thông báo khi xóa retweet thành công (tùy chọn).
  - **Error Trigger**: Nhận lỗi và lưu vào **Dead Letter Queue (DLQ)** để debug.
- **Cách chỉnh**:
  - **Slack**: Chọn **Webhook URL** hoặc **Credentials Slack**.
  - **Error Trigger**: Kết nối với **Google Sheets/Email/Slack** để log lỗi.

##### **🔹 Node 12: DLQ | Format error (Set)**
- **Mục đích**: Định dạng lỗi để lưu vào nơi nào đó (ví dụ: Google Sheets).
- **Cách chỉnh**:
  - Kết nối với **Google Sheets** hoặc **Email** để lưu log lỗi.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Chạy **manual run** để kiểm tra workflow với dữ liệu mẫu.
   - Kiểm tra **log** để đảm bảo không có lỗi.
2. **Bật Active**:
   - Sau khi test thành công, nhấn **Active** để workflow chạy tự động theo lịch trình.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[**Cách Tối Ưu Hiệu Quả**]
1. **Kết nối với Slack/Email**:
   - Thêm **Slack Webhook** hoặc **Email Node** để nhận báo cáo sau mỗi lần xóa retweet.
   - Ví dụ: `"Đã xóa {count} retweet thành công vào {date}"`.

2. **Lưu Log vào Google Sheets**:
   - Kết nối **Error Trigger** với **Google Sheets** để theo dõi lỗi và hoạt động của workflow.

3. **Chỉnh lịch trình theo nhu cầu**:
   - Nếu muốn xóa retweet **mỗi ngày lúc 8h sáng**, chỉnh **Schedule Trigger** thành `0 0 8 * * ?`.
   - Nếu muốn xóa **một lần sau chiến dịch**, chỉnh lịch trình tạm thời.

4. **Lọc retweet theo từ khóa**:
   - Thêm **ENRICH Node** trước **IF Node** để lọc retweet chứa từ khóa cụ thể (ví dụ: `#promo`).

5. **Tăng `max_results` cho kết quả chi tiết**:
   - Nếu muốn xóa **tất cả retweet** (tối đa 100), chỉnh `max_results: 100`.

6. **Thêm delay dài hơn trong giờ cao điểm**:
   - Nếu API bị chặn, tăng `batch_delay_minutes` lên 2-3 phút.
:::

---

### 📌 **Kết Luận**
Workflow **Retweet Cleanup with Scheduling** là **giải pháp hoàn hảo** để các sếp:
✔ **Tự động hóa việc xóa retweet cũ** trên X (Twitter) theo lịch trình.
✔ **Duy trì profile sạch sẽ, chuyên nghiệp** và tập trung vào nội dung mới.
✔ **Tiết kiệm thời gian** bằng cách loại bỏ công việc thủ công hàng ngày.
✔ **Tuân thủ giới hạn API** của X (Twitter) với cơ chế batching và delay an toàn.

**Hãy áp dụng ngay workflow này và làm cho profile X của bạn luôn **sạch sẽ, hiệu quả và chuyên nghiệp!** 🚀**

---
**🔗 [Tải workflow nguyên bản](https://n8n.io/workflows/9766) | [Hướng dẫn tạo OAuth2 cho X API](https://developer.twitter.com/en/docs/authentication/oauth-2-0/user-access-token)**