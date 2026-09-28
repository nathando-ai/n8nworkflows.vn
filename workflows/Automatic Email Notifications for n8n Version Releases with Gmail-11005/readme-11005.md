---
title: "🚀 **Tự Động Hóa Thông Báo Email Cho Các Phiên Bản Mới n8n (Latest & Beta) - Không Cần Code!**"
description: "Workflow tự động theo dõi phiên bản mới nhất và phiên bản beta của n8n trên npm, gửi email thông báo chi tiết với release notes từ GitHub, giúp các sếp quản lý instance n8n không bỏ lỡ bất kỳ cập nhật nào. Tiết kiệm thời gian và đảm bảo cập nhật kịp thời!"
slug: "tu-dong-hoa-thong-bao-email-cho-phien-ban-moi-n8n"
tags: [n8n, automation, devops, gmail, github, no-code]
keywords: [tự động hóa n8n, thông báo phiên bản mới, email tự động, release notes n8n, quản lý instance n8n]
---

# 🚀 **Tự Động Hóa Thông Báo Email Khi Có Phiên Bản Mới n8n (Latest & Beta)**

### **Giải quyết vấn đề gì?**
Các sếp quản lý instance n8n thường phải **tìm kiếm thủ công** phiên bản mới nhất trên npm hoặc GitHub để cập nhật, dẫn đến:
❌ **Bỏ lỡ phiên bản mới** do không kiểm tra thường xuyên.
❌ **Phải đọc release notes** một cách tẻ nhạt, mất thời gian.
❌ **Không biết phiên bản hiện tại** của instance mình so với phiên bản mới nhất.

**Workflow này tự động giải quyết tất cả!** Nó sẽ:
✅ **Theo dõi phiên bản mới nhất và beta** của n8n trên npm.
✅ **Lọc bỏ phiên bản cũ** để tránh thông báo trùng lặp.
✅ **Lấy release notes từ GitHub** và chuyển đổi sang định dạng HTML đẹp.
✅ **Gửi email thông báo chi tiết** với:
   - Tên phiên bản mới.
   - Link tải phiên bản.
   - Phiên bản hiện tại của instance (nếu cấu hình).
   - Nội dung release notes (được format đẹp).

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy 24/7 ổn định, các sếp nên **self-host n8n** trên VPS riêng:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần kiểm tra phiên bản thủ công hàng ngày.
- **Cập nhật kịp thời**: Nhận thông báo ngay khi có phiên bản mới (bao gồm cả beta).
- **So sánh phiên bản**: Biết ngay phiên bản hiện tại của instance mình so với phiên bản mới nhất.
- **Release notes dễ đọc**: Nội dung được chuyển đổi từ Markdown sang HTML, format đẹp trong email.
- **Tự động hóa hoàn toàn**: Chỉ cần cấu hình 1 lần, workflow chạy tự động hàng giờ.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Gmail** (để gửi email thông báo).
   - **Bật OAuth 2.0** trong [cài đặt Gmail](https://myaccount.google.com/lesssecureapps).
   - **Tạo OAuth 2.0 Client ID** trong [Google Cloud Console](https://console.cloud.google.com/).
2. **URL của instance n8n** (tùy chọn, để so sánh phiên bản hiện tại).
   - Ví dụ: `https://n8n.tinohost.vn`.
3. **Email nhận thông báo** (điền trong node Gmail).

---
:::note[LƯU Ý QUAN TRỌNG]
- Workflow **không cần API key** nào ngoài OAuth 2.0 của Gmail.
- Nếu không muốn so sánh phiên bản instance, có thể bỏ qua node `Get Instance Version`.
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có 2 cách:
- **Tải file JSON** từ [n8n.io/workflows/11005](https://n8n.io/workflows/11005) và import vào n8n Editor.
- **Copy JSON** từ link trên và paste vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **15 node**, các sếp cần chú ý cấu hình sau:

##### **A. Cấu hình Gmail (Node "Send Email")**
1. **Tạo OAuth 2.0 Credential**:
   - Trong n8n, đi đến **Credentials** → **Add** → Chọn **Gmail OAuth 2.0**.
   - Điền:
     - **Client ID** và **Client Secret** từ Google Cloud Console.
     - **Refresh Token** (lấy từ [Google OAuth Playground](https://developers.google.com/oauthplayground/) sau khi authorize).
   - **Tên credential**: `gmailOAuth2` (phải trùng với workflow gốc).

2. **Cấu hình node "Send Email"**:
   - **Credentials**: Chọn `gmailOAuth2`.
   - **To**: Điền email nhận thông báo (ví dụ: `admin@doanhnghiep.com`).
   - **Subject**: Có thể thay đổi (ví dụ: `"🆕 Cập nhật phiên bản n8n mới: v{{ $json["version"] }}"`).
   - **HTML Body**: Sử dụng template mặc định (đã format từ Markdown).

##### **B. Cấu hình URL instance n8n (Node "Get Instance Version")**
- **URL**: Điền URL của instance n8n (ví dụ: `https://n8n.tinohost.vn`).
- **Headers**:
  - `Authorization`: `Bearer <API_KEY>` (nếu instance có API key).
  - **Lưu ý**: Nếu không muốn so sánh phiên bản, có thể **xóa node này** và **xóa node "n8n URL & Version References"**.

##### **C. Cấu hình lịch chạy (Node "Schedule Trigger")**
- Mặc định là **1 giờ/lần** (có thể thay đổi):
  - **Cron**: `0 * * * *` (chạy mỗi giờ).
  - **Timezone**: Chọn timezone phù hợp (ví dụ: `Asia/Ho_Chi_Minh`).

##### **D. Các node khác (không cần chỉnh)**
- **Get Latest n8n Release** & **Get Beta n8n Release**: Lấy phiên bản từ npm.
- **RemoveDuplicates**: Lọc bỏ phiên bản cũ.
- **Merge Releases**: Ghép phiên bản mới nhất và beta.
- **Get GitHub Release Notes**: Lấy nội dung release notes.
- **Convert Notes To HTML**: Chuyển Markdown → HTML.

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Chọn **Run Workflow** và kiểm tra email có nhận được không.
   - Nếu có lỗi, kiểm tra:
     - **Credentials Gmail** có đúng không?
     - **URL instance n8n** có đúng không?
     - **Lịch trình** có hoạt động không?

2. **Bật Active**:
   - Sau khi test thành công, chuyển **Active** sang `ON`.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Thêm kênh thông báo khác**:
   - Kết nối với **Slack** hoặc **Telegram** bằng node `webhook` để gửi thông báo song song.
   - Ví dụ: Sau node `Send Email`, thêm node `Slack Webhook` để gửi tin nhắn.

2. **Tự động cập nhật instance**:
   - Sử dụng node `httpRequest` gọi API của instance n8n để **cập nhật tự động** khi có phiên bản mới.
   - Cần thêm logic kiểm tra phiên bản hiện tại vs phiên bản mới.

3. **Lọc phiên bản cụ thể**:
   - Thay đổi **npm registry URL** trong node `Get Latest n8n Release` nếu muốn theo dõi phiên bản khác (ví dụ: `https://registry.npmjs.org/n8n-beta`).

4. **Lưu log cho quản lý**:
   - Thêm node `stickyNote` hoặc `database` để lưu lịch sử phiên bản đã nhận thông báo.

5. **Thay đổi lịch chạy**:
   - Nếu muốn kiểm tra **2 lần/ngày**, thay đổi cron thành `0 8,20 * * *` (8h và 20h).

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp quản lý instance n8n muốn:
✔ **Không bỏ lỡ phiên bản mới** (bao gồm cả beta).
✔ **Tiết kiệm thời gian** so với kiểm tra thủ công.
✔ **Nhận thông báo chi tiết** với release notes format đẹp.

**Hành động ngay!**
1. Import workflow vào n8n của mình.
2. Cấu hình Gmail và URL instance (nếu có).
3. Bật **Active** và chờ email thông báo phiên bản mới!

**Nếu có vấn đề**, các sếp có thể tham khảo [forum n8n](https://community.n8n.io/) hoặc liên hệ tác giả [Mohamed Anan](https://link.anan.dev/Linkedin).

---
**💡 Mẹo cuối**: Nếu muốn **cập nhật tự động**, các sếp có thể mở rộng workflow bằng node `httpRequest` gọi API của instance n8n để thực hiện update khi có phiên bản mới!