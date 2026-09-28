---
title: "🌐 Tự Động Lưu Bookmark Mastodon Sang Raindrop.io - Không Cần Code!"
description: "Workflow này tự động đồng bộ hóa tất cả bookmark mới từ Mastodon sang Raindrop.io, giúp các sếp quản lý nội dung yêu thích một cách hiệu quả, tránh trùng lặp và tiết kiệm thời gian tìm kiếm. Hoạt động 24/7 với lịch trình tự động hoặc kích hoạt thủ công."
slug: "tu-dong-luu-bookmark-mastodon-sang-raindrop"
tags: [n8n, automation, no-code, Mastodon, Raindrop.io, API automation]
keywords: [tự động hóa n8n, đồng bộ bookmark Mastodon, Raindrop.io tự động, lưu trữ nội dung, tự động hóa xã hội mạng]
---

# 🚀 **Tự Động Lưu Bookmark Mastodon Sang Raindrop.io - Không Cần Code!**

### **Giải pháp cho các sếp muốn quản lý nội dung yêu thích một cách thông minh**
Hiện nay, khi các sếp sử dụng Mastodon để lưu trữ các bài viết, link hay nội dung quan trọng, việc tìm kiếm lại trở nên phức tạp khi phải tra cứu trên nhiều trang hoặc máy chủ khác nhau. **Workflow này tự động hóa quá trình đồng bộ hóa tất cả bookmark mới từ Mastodon sang Raindrop.io**, giúp các sếp:
- **Tiết kiệm thời gian** không phải thủ công sao chép link.
- **Tránh trùng lặp** nhờ cơ chế pagination thông minh.
- **Truy cập nội dung từ mọi nơi** thông qua Raindrop.io.
- **Hoạt động liên tục** với lịch trình tự động hoặc kích hoạt thủ công.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính riêng tư và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động đồng bộ hóa** tất cả bookmark mới từ Mastodon sang Raindrop.io **không cần can thiệp**.
- **Không trùng lặp** nhờ lưu trữ `min_id` để chỉ lấy nội dung mới.
- **Truy cập nhanh chóng** từ Raindrop.io trên mọi thiết bị.
- **Hoạt động liên tục** với lịch trình tự động (ví dụ: hàng ngày) hoặc kích hoạt thủ công.
- **Giảm thiểu rủi ro mất dữ liệu** khi chuyển đổi từ Mastodon sang Raindrop.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Token truy cập Mastodon** (có quyền đọc bookmark).
   - **Lấy token**:
     - Truy cập [Mastodon Instance](https://docs.joinmastodon.org/user/account/#access-tokens) của bạn.
     - Tạo một **Access Token** với quyền `read:bookmarks`.
2. **Credentials OAuth2 cho Raindrop.io**:
   - Đăng ký tài khoản [Raindrop.io](https://raindrop.io/) và tạo **OAuth2 Credential** trong n8n.
3. **URL cơ sở của Mastodon**:
   - Ví dụ: `https://mastodon.social` (thay thế bằng máy chủ của bạn).
4. **n8n Workflow Editor**:
   - Các sếp có thể sử dụng phiên bản **n8n Cloud** (miễn phí) hoặc **Self-hosted** (khuyến nghị).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/4800).
- **Nhấn vào "Import"** trong n8n Editor và chọn file JSON đã tải.
- **Hoặc copy toàn bộ JSON** và dán vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Sau khi import, các sếp cần cấu hình **các node quan trọng** như sau:

##### **A. Node `scheduleTrigger` (Kích hoạt theo lịch)**
- **Thiết lập lịch trình**:
  - Ví dụ: `0 0 * * *` (làm việc hàng ngày lúc 00:00).
  - Hoặc kích hoạt **thủ công** bằng node `manualTrigger`.

##### **B. Node `httpRequest` (Lấy bookmark từ Mastodon)**
- **Tham số cần điền**:
  - **Method**: `GET`
  - **URL**: `https://{VOTRE_SERVEUR_MASTODON}/api/v1/bookmarks`
    - Thay `{VOTRE_SERVEUR_MASTODON}` bằng URL của máy chủ Mastodon (ví dụ: `https://mastodon.social`).
  - **Headers**:
    - `Authorization: Bearer {YOUR_MASTODON_ACCESS_TOKEN}`
  - **Query Parameters**:
    - `min_id`: Được tự động cập nhật từ node `code` (không cần điền ban đầu).

##### **C. Node `if` (Kiểm tra có bookmark mới)**
- **Điều kiện**: `$.response && $.response.length > 0`
  - Nếu không có bookmark mới, workflow sẽ **dừng lại** để tránh xử lý không cần thiết.

##### **D. Node `code` (Lấy `min_id` mới nhất)**
- **Mã JavaScript**:
  ```javascript
  // Lấy min_id từ headers của response
  const minId = $input.all()[0].json.headers['link']?.match(/<.*?min_id=([^>]+)>/)?.[1] || '0';
  $node.setVariable('min_id', minId);
  ```
  - **Lưu ý**: Node này tự động lưu `min_id` vào **Workflow Static Data** để tránh lấy lại bookmark cũ.

##### **E. Node `splitOut` (Phân tách bookmark thành các item riêng lẻ)**
- **Tham số**:
  - `Property Path`: `$.response`
  - **Kiểu dữ liệu**: `Array`

##### **F. Node `if` (Lọc bookmark hợp lệ)**
- **Điều kiện**: `$.url && $.title`
  - Loại bỏ bookmark **không có URL hoặc tiêu đề**.

##### **G. Node `raindrop` (Lưu bookmark vào Raindrop.io)**
- **Tham số cần điền**:
  - **Credentials**: Chọn `raindropOAuth2Api` đã cấu hình trước.
  - **Operation**: `create`
  - **Resource**: `bookmark`
  - **Fields**:
    - `url`: `$node["Split Out"].json.url`
    - `title`: `$node["Split Out"].json.title`
    - **Nếu thiếu `card` (nội dung mở rộng)**:
      - Sử dụng node `raindrop` thứ 2 với tham số:
        ```json
        {
          "url": "$node['Split Out'].json.url",
          "title": "$node['Split Out'].json.title",
          "description": "$node['Split Out'].json.description || ''"
        }
        ```

---

#### **3. Kích hoạt ⚡️**
- **Test Run**:
  - Nhấn **Run Workflow** để kiểm tra với dữ liệu mẫu.
  - Kiểm tra **Raindrop.io** để xác nhận bookmark đã được lưu.
- **Bật Active**:
  - Sau khi kiểm tra thành công, **bật Active** để workflow hoạt động tự động.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node `slack` hoặc `telegram` để thông báo khi có bookmark mới được đồng bộ.
2. **Lưu log hoạt động**:
   - Sử dụng node `code` để ghi log vào **Workflow Static Data** hoặc **Google Sheets**.
3. **Báo cáo định kỳ**:
   - Tạo một workflow riêng để gửi **báo cáo tổng hợp** số lượng bookmark mới mỗi tháng qua email.
4. **Tùy chỉnh tiêu đề/miêu tả**:
   - Sử dụng node `code` để **chỉnh sửa tiêu đề** hoặc **thêm tags** cho bookmark trước khi lưu vào Raindrop.

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa việc lưu trữ bookmark từ Mastodon sang Raindrop.io, **giúp tiết kiệm thời gian và tránh mất dữ liệu**. Với **cấu hình đơn giản** và **hoạt động 24/7**, các sếp có thể tập trung vào công việc quan trọng hơn thay vì phải quản lý thủ công.

**🚀 Hãy áp dụng ngay và trải nghiệm sự tiện lợi của tự động hóa!**
Nếu có bất kỳ câu hỏi nào, hãy để lại comment bên dưới. Chúc các sếp thành công! 💪