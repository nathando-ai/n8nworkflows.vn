---
title: "🚀 Tự Động Tweet Thông Báo Mới Mỗi Lần Có Hoạt Động Mới Trên Strava - Không Cần Code!"
description: "Hãy tự động hóa việc tweet thông báo khi có hoạt động mới trên Strava, tiết kiệm thời gian và giữ liên lạc với cộng đồng. Workflow này hoạt động 24/7 mà không cần can thiệp thủ công."
slug: "tweet-hoat-dong-moi-strava"
tags: [n8n, automation, marketing, strava, twitter, no-code]
keywords: [n8n workflow strava, tự động tweet strava, marketing tự động, strava api twitter, tự động hóa thể thao]
---

# 🚀 Tự Động Tweet Thông Báo Mới Mỗi Lần Có Hoạt Động Mới Trên Strava

### 💡 **Giải pháp cho những người yêu thể thao muốn chia sẻ hoạt động của mình một cách tự động**
Bạn đã bao giờ muốn chia sẻ những hoạt động mới nhất trên Strava với cộng đồng mà không phải thủ công tweet mỗi lần? Hay bạn muốn tạo ra một chuỗi thông báo tự động để khuyến khích người dùng theo dõi hoạt động của mình? **Workflow này sẽ giúp bạn tự động tweet mỗi khi có hoạt động mới được tạo trên Strava**, tiết kiệm thời gian và giữ liên lạc với người theo dõi một cách hiệu quả.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động 24/7 mà không gián đoạn, các sếp nên cài n8n trên một **VPS riêng** (Self-hosted) để đảm bảo tính ổn định và bảo mật.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần phải tweet thủ công mỗi khi có hoạt động mới.
- **Tăng tương tác**: Giữ liên lạc với cộng đồng và khuyến khích người dùng tương tác với hoạt động của bạn.
- **Tự động hóa hoàn toàn**: Workflow hoạt động liên tục, ngay cả khi bạn ngủ.
- **Cá nhân hóa thông báo**: Tweet tự động với thông tin chi tiết về hoạt động mới.
:::

---

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow này hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Strava** và **API Key OAuth2** của Strava:
   - Đăng ký tại [Strava Developer Portal](https://www.strava.com/settings/api) để lấy `Client ID` và `Client Secret`.
   - Cấu hình OAuth2 trong n8n với credentials `stravaOAuth2Api`.
2. **Tài khoản Twitter (X)** và **API Key OAuth1**:
   - Đăng ký tại [Twitter Developer Portal](https://developer.twitter.com/) để lấy `Consumer Key`, `Consumer Secret`, `Access Token`, và `Access Token Secret`.
   - Cấu hình OAuth1 trong n8n với credentials `twitterOAuth1Api`.
:::

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- **Tải file JSON** từ [link workflow gốc](https://n8n.io/workflows/745) hoặc sao chép JSON từ trang đó.
- Mở **n8n Editor** và chọn **Import Workflow** (icon "Import" ở góc trên bên phải).
- Chọn file JSON đã tải hoặc dán JSON vào ô nhập liệu và nhấn **Import**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này chỉ có **2 node chính**, nhưng cấu hình chúng là **quan trọng nhất**:

##### **Node 1: Strava Trigger (n8n-nodes-base.stravaTrigger)**
- **Tên node**: Strava Trigger.
- **Credentials**: Chọn `stravaOAuth2Api` (đã cấu hình trước khi import).
- **Lưu ý**:
  - Node này sẽ **lắng nghe và phản hồi** khi có hoạt động mới được tạo trên Strava của bạn.
  - **Không cần cấu hình thêm** vì nó tự động lấy dữ liệu từ Strava thông qua OAuth2.

##### **Node 2: Twitter (n8n-nodes-base.twitter)**
- **Tên node**: Twitter.
- **Credentials**: Chọn `twitterOAuth1Api` (đã cấu hình trước khi import).
- **Lưu ý**:
  - **Action**: Chọn `Post Tweet` để tweet thông báo.
  - **Tham số cần điền**:
    - **Text**: Dùng `{{$node["Strava Trigger"].json["name"]}} đã hoàn thành một hoạt động mới! Chi tiết: [{{$node["Strava Trigger"].json["url"]}}]` để tweet tự động với tên hoạt động và link.
    - **Media (optional)**: Nếu muốn thêm hình ảnh, sử dụng `{{$node["Strava Trigger"].json["athlete"]["profile"]["medium"]}}` (link ảnh profile) hoặc hình ảnh hoạt động từ Strava.

#### 3. Kích hoạt ⚡️
- **Test Run**: Nhấn **Test Run** để kiểm tra workflow với dữ liệu mẫu.
  - Nếu cấu hình đúng, tweet sẽ được gửi tự động khi có hoạt động mới trên Strava.
- **Active Workflow**: Sau khi test thành công, nhấn **Active** để workflow hoạt động liên tục.

---

### ✍️ Mẹo & gợi ý nâng cao
:::tip[CÁC Ý TƯỞNG NÂNG CAO]
1. **Thêm hình ảnh vào tweet**:
   - Sử dụng `{{$node["Strava Trigger"].json["athlete"]["profile"]["medium"]}}` để thêm ảnh profile hoặc ảnh hoạt động từ Strava vào tweet.
2. **Tweet định kỳ**:
   - Nếu muốn tweet **các hoạt động cũ** (không chỉ mới), có thể kết hợp với **Node Schedule** để chạy workflow định kỳ (ví dụ: hàng ngày).
3. **Gửi thông báo Slack/Telegram**:
   - Thêm **Node Slack** hoặc **Node Telegram** sau node Strava Trigger để gửi thông báo ngay khi có hoạt động mới.
4. **Lưu log hoạt động**:
   - Sử dụng **Node Google Sheets** hoặc **Node Airtable** để ghi lại tất cả hoạt động đã tweet để theo dõi.
5. **Tweet cá nhân hóa**:
   - Thêm thông tin chi tiết hơn như **quãng đường, thời gian, loại hoạt động** vào tweet bằng cách sử dụng `{{$node["Strava Trigger"].json["distance"]}}`, `{{$node["Strava Trigger"].json["movingTime"]}}`, `{{$node["Strava Trigger"].json["type"]}}`.
:::

---

### 📌 Kết luận
Workflow này giúp **tự động hóa việc tweet thông báo hoạt động mới trên Strava**, tiết kiệm thời gian và giữ liên lạc với cộng đồng một cách hiệu quả. **Không cần code**, chỉ cần cấu hình OAuth2 và OAuth1 là có thể sử dụng ngay!

**Hãy áp dụng ngay và chia sẻ hoạt động thể thao của mình với cộng đồng một cách tự động hóa!** 🚀💪

---