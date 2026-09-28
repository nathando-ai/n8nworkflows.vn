---
title: "🚀 Tự Động Hóa Chia Sẻ Bài Viết Mới Từ RSS Feed Sang Slack – Không Cần Code!"
description: "Workflow này tự động phát hiện và chia sẻ bài viết mới từ các nguồn RSS được chọn lọc, gửi trực tiếp vào Slack channel của doanh nghiệp, tiết kiệm thời gian và tránh trùng lặp nội dung. Giúp các sếp cập nhật tin tức ngành hàng hàng ngày một cách hiệu quả."
slug: "tu-dong-hoa-chia-se-bai-viet-rss-slack"
tags: [n8n, automation, no-code, RSS, Slack, GoogleSheets, AI, workflow]
keywords: [n8n workflow RSS Slack, tự động hóa chia sẻ bài viết, RSS feed automation, Slack news digest, tự động hóa nội dung marketing]
---

# 🚀 **Tự Động Hóa Chia Sẻ Bài Viết Mới Từ RSS Feed Sang Slack – Không Cần Code!**

## 🔍 **Nỗi Đau Của Các Sếp**
Hàng ngày, các sếp phải:
- **Quét thủ công** các nguồn tin tức ngành hàng từ RSS feed, blog, hoặc website.
- **Lọc trùng lặp** bài viết đã chia sẻ trước đó.
- **Chia sẻ lại** trên Slack channel, Teams, hoặc email – mất thời gian và dễ bỏ lỡ tin tức mới.
- **Đánh giá chất lượng** bài viết trước khi chia sẻ, để tránh nội dung không phù hợp.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Đọc** các bài viết mới từ RSS feed.
✅ **Lọc bỏ** những bài đã chia sẻ trước đó.
✅ **Gửi** bài viết mới vào Slack channel với định dạng chuyên nghiệp.
✅ **Lưu lịch sử** để tránh trùng lặp trong tương lai.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần quét RSS thủ công hàng ngày.
- **Tránh trùng lặp**: Hệ thống tự động kiểm tra và bỏ bài viết đã chia sẻ.
- **Cập nhật liên tục**: Bài viết mới được gửi tự động vào Slack channel.
- **Dễ dàng mở rộng**: Thêm/loại bỏ nguồn RSS một cách đơn giản.
- **Chất lượng cao**: Chỉ chia sẻ bài viết mới và phù hợp.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets** với 2 tab:
   - **Feeds**: Danh sách các URL RSS (cột `title`, `link`).
   - **Posted Articles**: Lịch sử bài viết đã chia sẻ (cột `title`, `link`, `pubDate`).
2. **OAuth2 credentials** cho:
   - **Google Sheets** (để đọc/thêm dữ liệu).
   - **Slack** (để gửi tin nhắn).
3. **Slack channel** để nhận bài viết mới.
4. **n8n Workflow Editor** (cài đặt trên máy hoặc VPS).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/5333) hoặc copy toàn bộ JSON từ trang này.
- Mở **n8n Editor** → Nhấn **Import** → Dán JSON và nhấn **Import Workflow**.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **7 node**, các sếp cần chú ý cấu hình sau:

##### **A. Node `Trigger Workflow` (Cron)**
- **Chức năng**: Khởi động workflow theo lịch.
- **Cấu hình**:
  - Thời gian mặc định: **7:00 AM hàng ngày** (có thể thay đổi).
  - Ví dụ: `0 7 * * *` (7 giờ sáng hàng ngày).

##### **B. Node `Get Article Feeds` (Google Sheets)**
- **Chức năng**: Đọc danh sách RSS feed từ tab `Feeds`.
- **Cấu hình**:
  - **Credentials**: Chọn OAuth2 Google Sheets đã thiết lập.
  - **Sheet Name**: `Feeds`.
  - **Range**: `A1:B` (cột `title` và `link`).
  - **Output**: Dữ liệu sẽ được truyền sang node tiếp theo.

##### **C. Node `Read Latest Articles from Feeds` (RSS Feed Read)**
- **Chức năng**: Đọc bài viết mới từ các URL RSS.
- **Cấu hình**:
  - **URLs**: Sử dụng dữ liệu từ node `Get Article Feeds` (cột `link`).
  - **Limit**: Thiết lập số lượng bài viết đọc (ví dụ: `10`).

##### **D. Node `Get Historically Posted Articles from Google Sheet` (Google Sheets)**
- **Chức năng**: Đọc danh sách bài viết đã chia sẻ từ tab `Posted Articles`.
- **Cấu hình**:
  - **Credentials**: OAuth2 Google Sheets.
  - **Sheet Name**: `Posted Articles`.
  - **Range**: `A1:C` (cột `title`, `link`, `pubDate`).

##### **E. Node `Filter Unpublished Articles` (Code)**
- **Chức năng**: Lọc bỏ bài viết đã chia sẻ trước đó.
- **Cấu hình**:
  - **Script** (sử dụng mã JavaScript mặc định trong workflow):
    ```javascript
    // Lọc bỏ bài viết đã có trong lịch sử
    const postedArticles = $input.all().filter(item => item.json);
    const newArticles = $input.all().filter(item => {
      return !postedArticles.some(posted => posted.json.link === item.json.link);
    });
    return newArticles;
    ```
  - **Lưu ý**: Node này **không cần chỉnh sửa** nếu đã import từ file JSON.

##### **F. Node `Post New Articles to Slack Channel` (Slack)**
- **Chức năng**: Gửi bài viết mới vào Slack channel.
- **Cấu hình**:
  - **Credentials**: OAuth2 Slack.
  - **Channel ID**: Nhập ID channel Slack (tham khảo [cách tìm ID channel](https://api.slack.com/reference/channels)).
  - **Message Format**: Sử dụng template mặc định:
    ```
    *New Article Alert!*
    {{ $node["Read Latest Articles from Feeds"].json["title"] }}
    {{ $node["Read Latest Articles from Feeds"].json["link"] }}
    ```

##### **G. Node `Append New Articles to Google Sheet` (Google Sheets)**
- **Chức năng**: Thêm bài viết mới vào tab `Posted Articles`.
- **Cấu hình**:
  - **Credentials**: OAuth2 Google Sheets.
  - **Sheet Name**: `Posted Articles`.
  - **Range**: `A1:C` (thêm dữ liệu vào các cột `title`, `link`, `pubDate`).

---

#### **3. Kích Hoạt ⚡️**
- **Test Run**: Nhấn **Run Workflow** với dữ liệu mẫu để kiểm tra.
- **Bật Active**: Sau khi kiểm tra thành công, nhấn **Active** để workflow chạy tự động theo lịch.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Thêm hình ảnh preview**:
   - Sử dụng node **`webhook`** kết hợp với **`code`** để trích xuất hình ảnh từ bài viết và gửi kèm Slack message.
2. **Lọc bài viết theo từ khóa**:
   - Sử dụng node **`code`** để thêm logic lọc bài viết chứa từ khóa cụ thể (ví dụ: "AI", "Marketing").
3. **Gửi báo cáo định kỳ**:
   - Thêm node **`email`** hoặc **`googleSheets`** để gửi báo cáo tổng hợp bài viết mới hàng tuần.
4. **Tích hợp với Notion/Confluence**:
   - Sử dụng node **`notion`** hoặc **`confluence`** để đồng bộ bài viết mới vào wiki nội bộ.
5. **Cập nhật tự động khi bài viết bị xóa**:
   - Thêm node **`code`** để kiểm tra và xóa bài viết đã chia sẻ nếu nguồn RSS bị xóa.

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa việc chia sẻ tin tức ngành hàng, tiết kiệm thời gian và tránh trùng lặp. **Không cần code**, chỉ cần cấu hình vài bước đơn giản là có thể chạy 24/7 trên VPS.

**Hành động ngay!**
1. **Import workflow** vào n8n của mình.
2. **Cấu hình Google Sheets và Slack**.
3. **Bật Active** và bắt đầu tự động hóa!

**Cần hỗ trợ?** Đăng ký VPS n8n tại [TinoHost](https://tino.vn/vps-n8n?affid=388) với mã giảm giá **VPSN8N** để workflow chạy ổn định! 🚀