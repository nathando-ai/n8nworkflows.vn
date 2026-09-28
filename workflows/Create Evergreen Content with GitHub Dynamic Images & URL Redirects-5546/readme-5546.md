---
title: "🌟 Tự Động Hóa Nội Dung Evergreen với Hình Ảnh Động & URL Redirect - Không Cần Code!"
description: "Workflow này tự động tạo và cập nhật nội dung evergreen với hình ảnh động từ GitHub và URL redirect, giúp các sếp tiết kiệm thời gian và duy trì liên lạc với khách hàng lâu dài - ngay cả sau nhiều năm. Hãy tự động hóa quảng cáo, email marketing và tài liệu đăng ký một cách thông minh!"
slug: "tieu-dong-hoa-noi-dung-evergreen-github-url-redirect"
tags: [n8n, automation, social-media, content-marketing, github-integration]
keywords: [n8n workflow tự động hóa, nội dung evergreen, hình ảnh động GitHub, URL redirect tự động, tự động hóa email marketing, tự động hóa quảng cáo]
---

# 🚀 **Tự Động Hóa Nội Dung Evergreen với Hình Ảnh Động & URL Redirect**

### **Giải pháp nào giúp nội dung của các sếp "sống mãi" mà không cần cập nhật thủ công?**
Hãy tưởng tượng một hình ảnh hoặc liên kết trong email, bài đăng mạng xã hội hoặc trang web của bạn **tự động thay đổi nội dung** mà không cần bạn làm gì. Đó chính là **nội dung evergreen tự động hóa** với **hình ảnh động** và **URL redirect** thông minh.

Workflow này **tự động tạo và cập nhật** hình ảnh từ GitHub và URL redirect từ shorten.rest, giúp các sếp:
✅ **Tiết kiệm thời gian** không phải cập nhật thủ công.
✅ **Duy trì liên lạc lâu dài** với khách hàng, ngay cả sau nhiều năm.
✅ **Tăng tương tác** với nội dung quảng cáo, email marketing và tài liệu đăng ký.
✅ **Cập nhật liên tục** hình ảnh và liên kết mà không làm mất tính liên kết ban đầu.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **ổn định 24/7**, các sếp nên cài đặt n8n trên **VPS riêng** (Self-hosted) để tránh giới hạn của phiên bản cloud.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không phải cập nhật thủ công hình ảnh và URL hàng ngày.
- **Nội dung sống động**: Hình ảnh và liên kết tự động thay đổi nội dung mà không làm mất tính liên kết ban đầu.
- **Tương tác cao**: Khách hàng vẫn tương tác với nội dung cũ nhưng với nội dung mới nhất.
- **Duy trì liên lạc lâu dài**: Thích hợp cho email marketing, quảng cáo, tài liệu đăng ký và bài đăng mạng xã hội.
- **Cập nhật tự động**: Hình ảnh được thay đổi hàng giờ, URL được cập nhật hàng ngày.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản shorten.rest** (để tạo URL redirect động).
✔ **Tài khoản GitHub** (để lưu trữ hình ảnh động).
✔ **Tài khoản Gmail** (để gửi email mẫu với hình ảnh động).
✔ **API Key** của shorten.rest và GitHub (để kết nối với n8n).

---
:::info[CHUẨN BỊ]
- **shorten.rest API Key**: Tạo tại [shorten.rest](https://shorten.rest/).
- **GitHub OAuth Token**: Tạo tại [GitHub Developer Settings](https://github.com/settings/tokens).
- **Gmail OAuth Token**: Cấu hình tại [Google Cloud Console](https://console.cloud.google.com/).
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Truy cập [n8n.io/workflows/5546](https://n8n.io/workflows/5546) và nhấn **Export**.
2. Mở file JSON và copy toàn bộ nội dung.
3. Trong n8n Editor, nhấn **Import** và dán JSON vào.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này bao gồm **12 node** quan trọng, các sếp cần cấu hình như sau:

##### **A. Cấu hình Credentials**
- **shorten.rest API Key**:
  - Đi đến **Credentials** trong n8n → Tạo mới → Chọn **HTTP Header Auth**.
  - Điền **API Key** từ shorten.rest vào **Header Value** (dạng `Bearer YOUR_API_KEY`).

- **GitHub OAuth Token**:
  - Đi đến **Credentials** → Tạo mới → Chọn **GitHub OAuth2 API**.
  - Chọn **Personal Access Token** và điền **Token** từ GitHub.

- **Gmail OAuth Token**:
  - Đi đến **Credentials** → Tạo mới → Chọn **Gmail OAuth2**.
  - Chọn **Gmail Account** và điền **Client ID** và **Client Secret** từ Google Cloud Console.

##### **B. Cấu hình Node Quan Trọng**
1. **`Create new URL redirection` (HTTP Request)**
   - Thay đổi **URL** thành `https://shorten.rest/api/v1/shorten` (hoặc URL của shorten.rest).
   - Điền **Header** với `Authorization: Bearer YOUR_API_KEY`.

2. **`Update URL redirection` (HTTP Request)**
   - Thay đổi **URL** thành `https://shorten.rest/api/v1/shorten` (hoặc URL của shorten.rest).
   - Điền **Header** với `Authorization: Bearer YOUR_API_KEY`.

3. **`Create Image` (Edit Image)**
   - Chọn **Operation** là `multiStep`.
   - Điền **URL** của hình ảnh động (ví dụ: `https://raw.githubusercontent.com/ed-parsadanyan/public-tests/main/n8n-examples/dynamic-images/dynamic_img.png`).

4. **`Update GitHub file` (GitHub)**
   - Chọn **Repository** và **Branch** trong GitHub.
   - Điền **Path** của file hình ảnh (ví dụ: `n8n-examples/dynamic-images/dynamic_img.png`).

5. **`Form with dynamic image` (Form Trigger)**
   - Thêm **HTML Custom Element** với mã:
     ```html
     <div class="html">
       <img src="{{ $json.download_url }}" style="max-width: 100%; height: auto; display: block; margin-bottom: 8px;" />
     </div>
     ```

6. **`Send a message` (Gmail)**
   - Chọn **Gmail Account** và điền **Subject** và **HTML Body** với nội dung:
     ```html
     <h2>Dynamic image</h2>
     <a href="{{ $json.redirect_url }}" target="_blank">
       <img src="{{ $json.download_url }}" style="max-width: 100%; height: auto; display: block; margin-bottom: 8px;" />
     </a>
     ```

##### **C. Cấu hình Schedule Trigger**
- **`Schedule Trigger`** (cập nhật URL hàng ngày):
  - Thiết lập **Cron Expression** là `0 0 * * *` (lúc 00:00 hàng ngày).
- **`Schedule Trigger1`** (cập nhật hình ảnh hàng giờ):
  - Thiết lập **Cron Expression** là `0 * * * *` (lúc 00 phút hàng giờ).

#### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **Execute Workflow** và kiểm tra kết quả.
2. **Bật Active Workflow**:
   - Đảm bảo tất cả **Schedule Trigger** được kích hoạt.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram** để thông báo khi hình ảnh hoặc URL được cập nhật.

2. **Lưu log hoạt động**:
   - Thêm node **Sticky Note** để ghi lại lịch sử cập nhật.

3. **Gửi báo cáo định kỳ**:
   - Sử dụng node **Schedule Trigger** kết hợp với **Gmail** để gửi báo cáo tổng hợp hàng tuần.

4. **Tùy chỉnh hình ảnh động**:
   - Thay đổi **URL hình ảnh** trong node **Edit Image** để sử dụng hình ảnh từ nguồn khác (ví dụ: Canva, Unsplash).

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn **tự động hóa nội dung evergreen** mà không cần code. Bằng cách kết hợp **GitHub, shorten.rest và n8n**, các sếp có thể:
✔ **Tiết kiệm thời gian** không phải cập nhật thủ công.
✔ **Duy trì tương tác** với khách hàng lâu dài.
✔ **Tăng hiệu quả marketing** với hình ảnh và liên kết động.

**Hãy áp dụng ngay và làm cho nội dung của bạn "sống mãi"!** 🚀

---
**🔗 [Xem workflow gốc](https://n8n.io/workflows/5546)** | **📌 [Cài đặt n8n Self-hosted](https://docs.n8n.io/)**