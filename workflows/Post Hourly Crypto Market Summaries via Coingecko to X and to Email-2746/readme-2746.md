---
title: "🚀 Tự Động Hóa Báo Cáo Thị Trường Crypto Giờ Đúng - X (Twitter) + Email Mỗi Giờ"
description: "Workflow tự động hóa lấy dữ liệu Bitcoin từ CoinGecko, tổng hợp và gửi báo cáo thị trường crypto mỗi giờ lên X (Twitter) và email cá nhân - tiết kiệm thời gian theo dõi thị trường 24/7."
slug: "tieu-dong-hoa-bao-cao-thi-truong-crypto-moi-gio"
tags: [n8n, automation, crypto, twitter, email, no-code, finance]
keywords: [n8n workflow crypto, tự động hóa báo cáo thị trường, gửi tin tức crypto mỗi giờ, n8n twitter automation, n8n email automation]
---

# 🚀 **Tự Động Hóa Báo Cáo Thị Trường Crypto Mỗi Giờ: X + Email**

### **Nỗi Đau Của Các Sếp**
Theo dõi thị trường crypto 24/7 là một công việc tốn thời gian và dễ mắc lỗi. Các sếp phải:
- **Lặp đi lặp lại**: Tải dữ liệu từ CoinGecko, tổng hợp thông tin, viết tin tức và chia sẻ trên X (Twitter) hoặc email.
- **Thiếu tính chính xác**: Dữ liệu thủ công dễ bị sai sót, đặc biệt khi thị trường biến động nhanh.
- **Không hoạt động liên tục**: Phải nhớ tự động hóa hoặc mất thời gian theo dõi thủ công.

**Workflow này giải quyết tất cả!** Nó tự động lấy dữ liệu Bitcoin từ CoinGecko, tổng hợp thông tin và gửi báo cáo mỗi giờ lên **X (Twitter)** và **email** của bạn - **không cần code, hoạt động 24/7**.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần theo dõi thủ công mỗi giờ.
- **Tin tức chính xác**: Dữ liệu tự động cập nhật từ CoinGecko.
- **Cá nhân hóa**: Chia sẻ trên X (Twitter) và email cùng lúc.
- **Hoạt động liên tục**: Báo cáo tự động gửi mỗi giờ, kể cả khi bạn ngủ.
- **Dễ dàng mở rộng**: Thêm các coin khác hoặc thay đổi nội dung tin tức.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản CoinGecko API**:
   - Đăng ký API key tại [CoinGecko](https://www.coingecko.com/en/api) (miễn phí).
   - Thêm API key vào **Credentials** của n8n (n8n-nodes-base.httpRequest).

2. **Tài khoản X (Twitter)**:
   - Tạo **OAuth 2.0 Token** từ [Developer Portal Twitter](https://developer.twitter.com/) và thêm vào **Credentials** của n8n (n8n-nodes-base.twitter).

3. **Tài khoản Gmail**:
   - Kích hoạt **Less Secure Apps** (nếu cần) hoặc sử dụng **App Password** nếu tài khoản có bảo mật mạnh.
   - Thêm thông tin tài khoản vào **Credentials** của n8n (n8n-nodes-base.gmail).

4. **VPS cho n8n (khuyến nghị)**:
   - Để workflow chạy 24/7 ổn định, các sếp nên **self-host n8n** trên VPS.
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Truy cập [n8n.io](https://n8n.io/) và đăng nhập vào workspace.
2. Nhấp vào **"Import"** và chọn file JSON (hoặc copy/paste JSON từ [link gốc](https://n8n.io/workflows/2746)).
3. Chọn **"Import"** để tạo workflow.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow gồm **5 node chính**, các sếp cần cấu hình như sau:

##### **A. Crypto Hourly Trigger (n8n-nodes-base.scheduleTrigger)**
- **Thiết lập lịch chạy**: Cài đặt **1 giờ/lần** (ví dụ: 9:00 AM UTC).
- **Lưu ý**: Đảm bảo thời gian chạy phù hợp với múi giờ của bạn.

##### **B. Fetch Bitcoin Data (n8n-nodes-base.httpRequest)**
- **URL**: `https://api.coingecko.com/api/v3/simple/price?ids=bitcoin&vs_currencies=usd`
- **Headers**:
  - `Accept`: `application/json`
  - `Authorization`: `Bearer {API_KEY_COINGECKO}` (điền API key từ Credentials).
- **Lưu ý**: Nếu API key không đúng, node sẽ trả về lỗi 401.

##### **C. Format Crypto Message (n8n-nodes-base.code)**
- **Mã JavaScript**: Workflow đã cung cấp sẵn logic để format tin tức (ví dụ: giá Bitcoin, biến động 24h).
- **Lưu ý**:
  - Nếu muốn thay đổi nội dung tin tức, chỉnh sửa mã trong node này.
  - Dữ liệu đầu vào từ node `Fetch Bitcoin Data` sẽ tự động được format.

##### **D. Post Crypto Update on X (n8n-nodes-base.twitter)**
- **Credentials**: Chọn tài khoản Twitter đã cấu hình trước.
- **Tham số**:
  - **Status**: `{json["price"]["bitcoin"]["usd"]} USD (24h: {json["price"]["bitcoin"]["usd"] * (1 + json["price_change_percentage_24h"]["bitcoin"]["usd"] / 100)} USD)`.
  - **Lưu ý**: Đảm bảo OAuth token còn hiệu lực.

##### **E. Send Crypto Update Email (n8n-nodes-base.gmail)**
- **Credentials**: Chọn tài khoản Gmail đã cấu hình.
- **Tham số**:
  - **To**: Địa chỉ email của bạn.
  - **Subject**: `Báo cáo Bitcoin - {current_date}`.
  - **Body**: Nội dung tin tức đã format từ node `Format Crypto Message`.
- **Lưu ý**:
  - Nếu Gmail yêu cầu xác thực 2FA, sử dụng **App Password**.
  - Kiểm tra **SPAM** nếu email không đến.

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhấp vào **"Run Workflow"** để kiểm tra dữ liệu mẫu.
   - Kiểm tra **X (Twitter)** và **email** xem có nhận được tin tức không.
2. **Bật Active**:
   - Sau khi test thành công, chuyển trạng thái workflow sang **"Active"**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Thêm các coin khác**:
   - Thay đổi URL trong node `Fetch Bitcoin Data` để lấy dữ liệu Ethereum, Solana, etc.
   - Ví dụ: `https://api.coingecko.com/api/v3/simple/price?ids=bitcoin,ethereum,solana&vs_currencies=usd`.

2. **Gửi báo cáo định kỳ**:
   - Thay đổi lịch chạy trong `Crypto Hourly Trigger` thành **ngày** (ví dụ: mỗi thứ 2, 4, 6).

3. **Lưu log vào StickyNote**:
   - Thêm node `n8n-nodes-base.stickyNote` để lưu lịch sử báo cáo.

4. **Kết hợp với Telegram**:
   - Thêm node `n8n-nodes-base.telegram` để gửi tin tức lên Telegram cùng lúc.

5. **Tự động hóa báo cáo cho đội nhóm**:
   - Thay đổi node `Send Crypto Update Email` để gửi cho nhiều người nhận.
:::

---

### 📌 **Kết Luận**
Workflow này giúp các sếp **tự động hóa hoàn toàn** việc theo dõi và chia sẻ báo cáo thị trường crypto mỗi giờ - **không cần code, không cần nhớ làm thủ công**. Bằng cách kết hợp **CoinGecko API**, **X (Twitter)** và **email**, nó mang lại **tính chính xác, tiết kiệm thời gian** và **hoạt động liên tục**.

**Hãy áp dụng ngay và bắt đầu theo dõi thị trường crypto một cách thông minh!** 🚀

---
:::tip[LƯU Ý CUỐI CUNG]
- Nếu gặp lỗi, kiểm tra **Credentials** của các node (Twitter, Gmail, CoinGecko).
- Để workflow chạy ổn định, **self-host n8n** trên VPS (không phụ thuộc vào phiên bản miễn phí).
- Mở rộng workflow bằng cách thêm các coin hoặc dịch vụ khác (Telegram, Slack...).
:::