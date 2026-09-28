---
title: "🦋 Bluesky New Follower Auto DM – Tự động nhắn tin chào mừng follower mới trên Bluesky"
description: "Workflow tự động kiểm tra follower mới trên Bluesky mỗi 5 phút và gửi tin nhắn DM cá nhân hoá, giúp bạn duy trì sự tương tác mà không cần can thiệp thủ công."
slug: "bluesky-new-follower-auto-dm"
tags: [n8n, automation, no-code, bluesky, social-media, dm-automation, ai-marketing]
keywords: [n8n workflow, tự động hóa bluesky, gửi dm tự động, follower mới, social media automation]
---

# 🦋 Bluesky New Follower Auto DM – Tự động nhắn tin chào mừng follower mới trên Bluesky

Bạn đang quản lý một tài khoản Bluesky và muốn chào mừng mỗi follower mới bằng một tin nhắn DM cá nhân hoá? Thực hiện thủ công tốn thời gian, dễ bỏ lỡ và không thể mở rộng khi lượng follower tăng. Workflow **Bluesky New Follower Auto DM** giải quyết vấn đề này bằng cách tự động:

- Kiểm tra định kỳ (mỗi 5 phút) danh sách follower mới.
- Lọc ra những follower chưa từng được nhắn tin.
- Gửi tin nhắn DM tự động với nội dung bạn tự thiết lập (có thể bao gồm link, mã giảm giá, lời cảm ơn…).

Nhờ n8n, toàn bộ quy trình chạy 100% trên nền tảng tự động hoá không cần viết một dòng code nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần đăng nhập thủ công mỗi ngày để kiểm tra follower mới.
- **Tương tác ngay lập tức**: Follower mới nhận được tin nhắn chào mừng trong vòng vài phút sau khi theo dõi.
- **Cá nhân hoá nội dung**: Bạn có thể chỉnh sửa tin nhắn DM bất kỳ lúc nào để phù hợp với chiến dịch marketing.
- **Hoạt động liên tục**: Cron trigger đảm bảo workflow chạy nền mà không cần can thiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Bluesky**: Username và password ( hoặc App Specific Password nếu bạn bật 2FA ).
- **API Token Bluesky** (nếu sử dụng xác thực qua token) – có thể lấy từ trang thiết lập tài khoản Bluesky.
- **n8n phiên bản >= 1.0** (để hỗ trợ nodes HTTP Request, Code, Filter…).
- (Tùy chọn) **Credentials HTTP Basic Auth** hoặc **Header Auth** để lưu trữ thông tin đăng nhập Bluesky an toàn trong n8n.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Sao chép toàn bộ JSON workflow từ nguồn gốc (link: https://n8n.io/workflows/4713).
2. Trong n8n Editor, nhấn **Import** → **Upload file** hoặc **Paste JSON**.
3. Nhấn **Import** để workflow xuất hiện trong danh sách của bạn.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, bạn cần cấu hình các node sau để workflow hoạt động đúng với tài khoản Bluesky của mình:

| Node | Loại | Cấu hình cần thiết |
|------|------|--------------------|
| **Setup** | Set | Định nghĩa các biến môi trường: <br>• `BSKY_USERNAME` (tên đăng nhập Bluesky) <br>• `BSKY_PASSWORD` (mật khẩu hoặc App Specific Password) <br>• `DM_MESSAGE` (nội dung tin nhắn DM bạn muốn gửi) |
| **Create Session** | HTTP Request | Method: `POST` <br>URL: `https://bsky.social/xrpc/com.atproto.server.createSession` <br>Auth: **None** (sẽ gửi username/password trong body) <br>Body (JSON): `{ "identifier": "{{ $json[\"BSKY_USERNAME\"] }}", "password": "{{ $json[\"BSKY_PASSWORD\"] }}" }` <br>Sau khi chạy, node sẽ trả về `accessJwt` – lưu lại để dùng trong các request sau. |
| **Get Follow Notifications** | HTTP Request | Method: `GET` <br>URL: `https://bsky.social/xrpc/app.bsky.feed.getFollowers?actor={{ $json[\"BSKY_USERNAME\"] }}&limit=100` <br>Headers: `Authorization: Bearer {{ $json[\"accessJwt\"] }}` <br>Lấy danh sách follower hiện tại. |
| **Filter New Follows** | Code | JavaScript để so sánh danh sách follower hiện tại với danh sách đã lưu (có thể lưu trong workflow static data hoặc trong một bảng SQLite/Postgres nếu bạn muốn lưu lâu dài). <br>Lọc ra những follower mới (ID chưa từng xuất hiện). |
| **Initiate Convo with Follower** | HTTP Request | Method: `POST` <br>URL: `https://bsky.social/xrpc/app.bsky.convo.createConversation` <br>Headers: `Authorization: Bearer {{ $json[\"accessJwt\"] }}` <br>Body: `{ "users": [ "{{ $json[\"followerDid\"] }}" ] }` <br>Tạo cuộc trò chuyện (DM) với follower mới. |
| **Send DM** | HTTP Request | Method: `POST` <br>URL: `https://bsky.social/xrpc/app.bsky.convo.sendMessage` <br>Headers: `Authorization: Bearer {{ $json[\"accessJwt\"] }}` <br>Body: `{ "conversationId": "{{ $json[\"conversationId\"] }}", "message": "{{ $json[\"DM_MESSAGE\"] }}" }` <br>Gửi tin nhắn DM đã thiết lập trong node **Setup**. |
| **Filter** | Filter | Đảm bảo chỉ tiếp tục khi cả hai bước trên (tạo conversation và gửi message) đều trả về status 200. Nếu bất kỳ bước nào thất bại, workflow sẽ dừng và bạn có thể kiểm tra log để debug. |

> **Lưu ý quan trọng**:  
> - Thay đổi `DM_MESSAGE` trong node **Setup** để phù hợp với thương hiệu hoặc chiến dịch của bạn (có thể bao gồm link landing page, mã giảm giá, lời cảm ơn…).  
> - Nếu bạn muốn lưu trữ danh sách follower đã được nhắn tin để không gửi lại, hãy thêm một node **Set** hoặc **SQLite** sau node **Filter New Follows** để ghi lại ID follower đã xử lý.  
> - Đảm bảo credentials (username/password) được lưu trữ dưới dạng **Credentials** trong n8n (type: **HTTP Basic Auth** hoặc **Custom Credential**) để tránh lộ thông tin nhạy cảm trong workflow.

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong, nhấn **Test Workflow** để chạy một lần với dữ liệu mẫu (n8n sẽ sử dụng dữ liệu từ node **Setup**).  
2. Kiểm tra tab **Execution Logs** để xác nhận mỗi node trả về status 200 và bạn đã nhận được tin nhắn DM trên Bluesky (có thể dùng tài khoản test để kiểm tra).  
3. Nếu mọi thứ ổn, bật toggle **Active** ở góc trên bên phải workflow.  
4. Workflow sẽ chạy tự động theo cron (mặc định mỗi 5 phút) và thực hiện quy trình trên nền tảng mà không cần can thiệp.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo Slack/Telegram**: Thêm node **Slack** hoặc **Telegram** sau node **Send DM** để gửi thông báo khi có follower mới được nhắn tin – giúp bạn theo dõi hoạt động trong thời gian thực.  
- **Ghi log vào Google Sheets**: Lưu lại thời gian, username follower và nội dung DM đã gửi vào một sheet để báo cáo hàng tuần.  
- **A/B test nội dung DM**: Tạo hai biến `DM_MESSAGE_A` và `DM_MESSAGE_B` trong node **Setup**, dùng node **IF** để ngẫu nhiên chọn một trong hai và đo lường tỷ lệ phản hồi (nếu bạn có cách tracking).  
- **Tích hợp với CRM**: Sau khi gửi DM, gọi API tới CRM (HubSpot, Pipedrive…) để tạo lead mới từ follower vừa tương tác.  
- **Giới hạn tốc độ**: Nếu bạn có lượng follower lớn, thêm node **Delay** (ví dụ: 1 giây) giữa mỗi lần gửi DM để tránh bị Bluesky giới hạn tốc độ (rate limit).

### 📌 Kết luận
Workflow **Bluesky New Follower Auto DM** giúp bạn tự động hoá quá trình chào mừng và tương tác với follower mới trên Bluesky mà không tốn công sức thủ công. Với chỉ một vài bước cấu hình, bạn sẽ duy trì sự hiện diện tích cực, tăng cơ hội chuyển đổi và tập trung vào những chiến lược marketing quan trọng hơn.

🚀 **Hãy import ngay hôm nay và để n8n làm việc thay bạn!**