---
title: "🚀 Tự động Boost bài đăng từ tài khoản FediVerse lên Mastodon"
description: "Workflow n8n kéo các status mới của một tài khoản FediVerse và tự động boost lên hồ sơ Mastodon của bạn mỗi ngày."
slug: "boost-bai-dang-fedi-verse-mastodon"
tags: [n8n, automation, no-code, mastodon, fediverse, marketing]
keywords: [n8n workflow, tự động hóa, mastodon boost, fediverse, boost posts]
---

# 🚀 Tự động Boost bài đăng từ tài khoản FediVerse lên Mastodon

Bạn có bao giờ phải mở **threads.net**, sao chép link, rồi mới vào Mastodon để boost mỗi khi có bài mới?  
Công việc này tốn thời gian, dễ sai sót và không thể thực hiện 24/7.  
Workflow này sẽ **tự động**:

1. Lấy các status mới nhất của một tài khoản FediVerse (qua API của threads.net).  
2. Lọc ra chỉ những status được đăng trong ngày hiện tại.  
3. Gửi yêu cầu boost lên Mastodon của bạn.  

Kết quả: **Boost liên tục, không bỏ lỡ** bất kỳ bài nào, hoàn toàn không cần viết code.

:::info[Gợi ý hạ tầng cho n8n]  
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]  
- **Tiết kiệm thời gian**: Không cần mở nhiều tab, thao tác thủ công.  
- **Độ chính xác 100 %**: Chỉ boost những status thực sự mới trong ngày.  
- **Hoạt động liên tục**: Workflow chạy tự động theo lịch, không bỏ lỡ bất kỳ bài nào.  
- **Tăng tương tác**: Nội dung được đưa lên Mastodon nhanh hơn, thu hút nhiều lượt phản hồi.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]  
- **Tài khoản Mastodon** (có quyền boost).  
- **API Token** của Mastodon (được tạo trong Settings → Development → New Application → “Read & write”).  
- **URL API của threads.net** để lấy status (ví dụ: `https://threads.net/api/v1/profile/{username}/posts`).  
- **Tên người dùng FediVerse** (username) mà bạn muốn theo dõi.  
- **n8n** đã được cài đặt và có quyền truy cập internet.  
- (Tùy chọn) **Domain hoặc IP VPS** nếu muốn chạy 24/7.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n Editor.  
2. Nhấn **Import** → **Upload JSON** và chọn file `boost-fedi-verse-mastodon.json` (hoặc copy toàn bộ JSON vào ô **Paste JSON**).  
3. Nhấn **Import** để thêm workflow vào danh sách.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Mô tả | Cấu hình cần chỉnh |
|------|------|--------------------|
| **Schedule Trigger** | Kích hoạt workflow mỗi ngày (hoặc theo tần suất bạn muốn). | - **Cron**: `0 8 * * *` (ví dụ: chạy lúc 08:00 mỗi ngày). |
| **Get statuses from threads.net** | Gửi GET request tới API của threads.net để lấy danh sách status. | - **Method**: `GET` <br> - **URL**: `https://threads.net/api/v1/profile/{{ $json["username"] }}/posts` <br> - **Query Parameters**: `limit=20` (tùy chỉnh). <br> - **Authentication**: nếu API yêu cầu, thêm Header `Authorization: Bearer <API_KEY>`. |
| **Filter today** | Lọc ra các status có ngày tạo bằng ngày hiện tại. | - **Expression**: `{{$json["created_at"] | date:"YYYY-MM-DD"}} === {{$now | date:"YYYY-MM-DD"}}` <br> - Đảm bảo trường `created_at` đúng định dạng ISO. |
| **Boost statuses** | Gửi POST request tới Mastodon để boost mỗi status đã lọc. | - **Credentials**: chọn **httpHeaderAuth** → nhập **Header Name**: `Authorization` và **Header Value**: `Bearer <Mastodon_API_Token>`. <br> - **Method**: `POST` <br> - **URL**: `https://<your-mastodon-instance>/api/v1/statuses/<status_id>/reblog` (sử dụng **Expression**: `https://{{ $json["mastodon_instance"] }}/api/v1/statuses/{{ $json["id"] }}/reblog`). |
| **(Optional) Error handling** | Thêm node **Set** hoặc **IF** để log lỗi nếu boost thất bại. | - Ghi lại `error.message` vào Google Sheet hoặc Slack. |

> **Lưu ý:** Đảm bảo **httpHeaderAuth** được tạo trong **Credentials** → **HTTP Header Auth** và chứa token Mastodon hợp lệ.

#### 3. Kích hoạt ⚡️
1. Nhấn **Execute Workflow** lần đầu để kiểm tra với dữ liệu mẫu.  
2. Kiểm tra log của mỗi node, xác nhận rằng các status được lấy và boost thành công.  
3. Khi mọi thứ ổn, bật **Active** (nút chuyển đổi ở góc trên bên phải). Workflow sẽ tự động chạy theo lịch đã định.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm Slack/Telegram notification**: Sau khi boost xong, gửi tin nhắn thông báo cho nhóm marketing.  
- **Lưu log vào Google Sheets**: Ghi lại ID status, thời gian boost và kết quả (thành công / lỗi).  
- **Boost theo hashtag**: Thêm node **IF** để chỉ boost những status chứa hashtag nhất định.  
- **Đa tài khoản**: Sao chép node **Get statuses** và **Boost** cho nhiều tài khoản FediVerse khác nhau, dùng **SplitInBatches** để xử lý đồng thời.  

### 📌 Kết luận
Với workflow này, các sếp sẽ **không còn phải mất công kiểm tra và boost thủ công** nữa. Chỉ cần một lần cấu hình, hệ thống sẽ tự động đưa nội dung mới từ FediVerse lên Mastodon mỗi ngày, giúp tăng tương tác và duy trì sự hiện diện trên mạng xã hội một cách nhất quán. Hãy triển khai ngay và cảm nhận sức mạnh của tự động hoá!