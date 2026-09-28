---
title: "🚀 Tự Động Hóa Quản Lý & Lấy Facebook Access Token 60 Ngày với n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình lấy và gia hạn Facebook User Token, Page Token dài hạn 60 ngày một cách nhanh chóng và bảo mật."
slug: "tu-dong-hoa-lay-va-quan-ly-facebook-token-voi-n8n"
tags: [n8n, automation, facebook-api, marketing, no-code, token-management]
keywords: [n8n workflow, facebook access token, tự động lấy token facebook, facebook graph api, n8n facebook login]
---

# 🚀 Tự Động Hóa Quản Lý & Lấy Facebook Access Token 60 Ngày với n8n

Việc quản lý và gia hạn Facebook Access Token thủ công thường xuyên là "nỗi ám ảnh" của các nhà quảng cáo, marketer và lập trình viên. Token ngắn hạn hết hạn liên tục làm gián đoạn các chiến dịch marketing, bot chăm sóc khách hàng hay hệ thống đăng bài tự động. 

Bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ xịn sò, giúp tự động hóa toàn bộ quá trình lấy **Facebook User Token dài hạn (60 ngày)** thông qua OAuth2 và Webhook chỉ với một vài thao tác cấu hình đơn giản.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và xử lý các OAuth redirect từ Facebook mượt mà, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Chuyển đổi từ Short-Lived Token sang Long-Lived Token (60 ngày) hoàn toàn tự động qua API.
- **Tiết kiệm thời gian:** Không cần thao tác thủ công phức tạp trên Graph API Explorer mỗi khi token hết hạn.
- **Linh hoạt mở rộng:** Dễ dàng kết nối thêm các node lưu trữ token vào Database (Google Sheets, Supabase, Notion) hoặc gửi thông báo về Telegram/Slack.
- **Bảo mật & Chủ động:** Chạy trực tiếp trên hạ tầng riêng của doanh nghiệp, kiểm soát hoàn toàn dữ liệu xác thực.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n (Self-hosted hoặc Cloud) có cấu hình sẵn Tunnel (Ngrok, Cloudflare Tunnel) để Facebook có thể gọi về Webhook.
- Một **Facebook App** được cấu hình chế độ Live/Development tại [Facebook Developers](https://developers.facebook.com/apps/).
- **App ID** và **App Secret** từ ứng dụng Facebook của các sếp.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể lấy mã nguồn JSON của workflow này trực tiếp từ kho lưu trữ GitHub của tác giả L Hung tại: 
`https://github.com/luuhung93/n8n-json` (Workflow ID: `2959`).
Sau đó copy đoạn JSON và Paste trực tiếp vào màn hình n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm các node chính sau đây cần được cấu hình chuẩn xác:
- **Node `Config` (Set):** Điền các thông số cốt lõi của Facebook App bao gồm `app_id`, `app_secret` và `fb_redirect_uri` (URL webhook nhận callback từ Facebook, ví dụ: `https://domain-cua-ban.com/webhook/facebook-login`).
- **Node `Webhook`:** Lắng nghe yêu cầu đăng nhập từ trình duyệt tại đường dẫn `/webhook/facebook-login`.
- **Node `Redirect URL` (Code):** Nơi cấu hình mảng `correctScopes` để yêu cầu các quyền hạn (Permissions) từ Facebook:
  ```javascript
  const correctScopes = [
    'pages_manage_posts', // Quyền quản lý bài đăng trên Page
    'pages_read_engagement', // Quyền đọc tương tác
    // Thêm hoặc bớt các scope tùy theo nhu cầu thực tế của sếp
  ];
  ```
- **Node `Short-Lived Token` & `Long-Lived Token` (HTTP Request):** Tự động trao đổi authorization code lấy token ngắn hạn, sau đó đổi lấy token dài hạn (60 ngày) từ Facebook Graph API.
- **Node `Token` & `Redirect` (Respond to Webhook):** Trả kết quả hiển thị trực tiếp lên màn hình trình duyệt hoặc chuyển hướng người dùng.

*Lưu ý cấu hình trên Facebook App:*
Vào [Facebook App Dashboard](https://developers.facebook.com/apps/) -> Chọn **Facebook Login** -> **Settings**, sau đó thêm `fb_redirect_uri` của các sếp vào mục **Valid OAuth Redirect URIs**.

#### 3. Kích hoạt ⚡️
1. Chuyển trạng thái workflow từ **Inactive** sang **Active** (nút màu xanh ở góc trên bên phải).
2. Truy cập vào đường dẫn Webhook kèm tham số (Ví dụ: `https://domain-cua-ban.com/webhook/facebook-login?type=login`).
3. Hoàn tất các bước đăng nhập và cấp quyền trên giao diện Facebook.
4. Nhận kết quả là **Facebook Access Token** có thời hạn 60 ngày hiển thị ngay trên màn hình.

### ✍️ Mẹo & gợi ý nâng cao
- **Lưu trữ tự động:** Mặc định token sẽ hiển thị trên màn hình. Các sếp có thể nối thêm node **Google Sheets**, **Supabase** hoặc **Notion** ngay sau bước lấy token để tự động lưu lại lịch sử cấp phát.
- **Cảnh báo hết hạn:** Kết hợp node **Schedule Trigger** chạy định kỳ mỗi 50 ngày để kiểm tra trạng thái token hoặc gửi thông báo qua **Telegram/Slack** nhắc nhở gia hạn trước khi token chết.
- **Lấy Page Token:** Sử dụng User Token vừa lấy được để gọi endpoint `https://graph.facebook.com/v21.0/me/accounts?access_token={user-access-token}` nhằm lấy Page Token tự động phục vụ việc đăng bài Page.

### 📌 Kết luận
Workflow **Facebook Token Retrieval & Management** là mảnh ghép hoàn hảo giúp các nhà tự động hóa giải quyết triệt để bài toán token Facebook hết hạn. Hãy áp dụng ngay vào hệ thống của các sếp để tối ưu hóa vận hành và loại bỏ các thao tác thủ công nhàm chán!