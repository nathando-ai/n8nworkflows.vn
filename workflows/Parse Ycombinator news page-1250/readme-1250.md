---
title: "🚀 Tự Động Hàng Ngày: Parse & Lưu Trữ Tin Tức Y Combinator Vào Google Sheets + Email Cập Nhật (Không Cần Code)"
description: "Workflow tự động hóa lấy tin tức từ trang Y Combinator, trích xuất tiêu đề và liên kết, lưu vào Google Sheets và gửi email thông báo hàng ngày cho các sếp. Giúp tiết kiệm thời gian theo dõi tin tức tech hàng ngày và không bỏ lỡ bất kỳ tin tức mới nào."
slug: "tich-hop-tin-tuc-ycombinator-vao-google-sheets"
tags: [n8n, automation, no-code, google-sheets, email-notification, web-scraping]
keywords: [n8n workflow tự động hóa, parse tin tức Y Combinator, lưu tin tức vào Google Sheets, gửi email tự động hàng ngày, tự động hóa theo dõi tin tức tech]
---

# 🚀 **Tự Động Hàng Ngày: Parse Tin Tức Y Combinator Vào Google Sheets + Email Cập Nhật**

### **Nỗi Đau Của Các Sếp**
Trong thế giới công nghệ phát triển nhanh như hiện nay, các sếp và nhà quản lý thường phải mất nhiều thời gian để theo dõi tin tức mới nhất từ các trang như **Y Combinator** để cập nhật xu hướng mới, công nghệ mới, hoặc các sự kiện quan trọng. Thao tác này không chỉ tốn thời gian mà còn dễ bị bỏ lỡ tin tức quan trọng khi phải làm thủ công hàng ngày.

**Workflow này giải quyết vấn đề đó bằng cách:**
✅ **Tự động lấy tin tức** từ trang Y Combinator hàng ngày.
✅ **Trích xuất tiêu đề và liên kết** của các bài viết mới.
✅ **Lưu dữ liệu vào Google Sheets** để theo dõi và phân tích dễ dàng.
✅ **Gửi email thông báo** cho các sếp khi có tin tức mới, không cần phải kiểm tra thủ công.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần phải truy cập Y Combinator hàng ngày để cập nhật tin tức.
- **Dữ liệu chính xác và cập nhật**: Tin tức được lấy tự động từ trang chính thức, không bị lỗi nhân thủ công.
- **Theo dõi dễ dàng**: Dữ liệu được lưu vào Google Sheets với định dạng rõ ràng, dễ dàng phân tích và chia sẻ.
- **Cập nhật tức thời**: Email thông báo sẽ được gửi ngay khi có tin tức mới, không bỏ lỡ bất kỳ tin tức quan trọng nào.
- **Hoạt động liên tục**: Workflow chạy tự động hàng ngày, không cần can thiệp của con người.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow này, các sếp cần chuẩn bị:
1. **Tài khoản Google** (để sử dụng Google Sheets và gửi email thông qua Gmail).
2. **API Key hoặc Credentials SMTP** (nếu không sử dụng Gmail, cần thiết lập SMTP cho email).
3. **Trang Y Combinator** (URL mặc định là `https://news.ycombinator.com/`).
4. **Google Sheet** đã được tạo sẵn để lưu trữ tin tức (các sếp cần chia sẻ link với quyền chỉnh sửa cho n8n).
5. **Địa chỉ email** để nhận thông báo hàng ngày.
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow này từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Tải file JSON từ [đây](https://n8n.io/workflows/1250) hoặc sao chép JSON từ link trên.
2. Mở **n8n Editor** và chọn **Import Workflow**.
3. Dán JSON vào và nhấn **Import**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Sau khi import, các sếp cần cấu hình các node quan trọng như sau:

##### **a. Node "HTTP Request" (Lấy trang Y Combinator)**
- **Method**: `GET`
- **URL**: `https://news.ycombinator.com/`
- **Headers**: Thêm `User-Agent` để tránh bị chặn (ví dụ: `Mozilla/5.0`).
- **Lưu ý**: Nếu trang Y Combinator thay đổi URL, các sếp cần cập nhật lại ở đây.

##### **b. Node "HTML Extract" (Trích xuất tin tức)**
- **Selector**: Các sếp cần chọn các phần tử HTML chứa tiêu đề và liên kết tin tức.
  - **Tiêu đề**: Thường là `<span class="titleline">` hoặc `<a class="titlelink">`.
  - **Liên kết**: Thường là `<a class="titlelink">` hoặc `<span class="titleline"> a`.
- **Lưu ý**: Nếu trang Y Combinator thay đổi cấu trúc HTML, các sếp cần cập nhật lại selector.

##### **c. Node "list news url" và "list news title" (Tách danh sách)**
- **Các sếp không cần chỉnh sửa gì** ở node này, nó sẽ tự động trích xuất danh sách từ node "HTML Extract".

##### **d. Node "Merge" (Kết hợp dữ liệu)**
- **Các sếp không cần chỉnh sửa gì** ở node này, nó sẽ kết hợp tiêu đề và liên kết thành một danh sách duy nhất.

##### **e. Node "Spreadsheet File" (Lưu vào Google Sheets)**
- **Google Sheet URL**: Các sếp cần chia sẻ link Google Sheet với quyền chỉnh sửa và dán vào node này.
- **Sheet Name**: Chọn tên sheet muốn lưu tin tức (ví dụ: `Tin tức Y Combinator`).
- **Range**: Đặt vào ô `A1` để bắt đầu ghi dữ liệu.
- **Lưu ý**: Các sếp cần đảm bảo Google Sheet đã được tạo sẵn và có cột `Tiêu đề` và `Liên kết`.

##### **f. Node "Send email notification" (Gửi email thông báo)**
- **Credentials**: Chọn `smtp` (nếu sử dụng Gmail, các sếp cần thiết lập SMTP hoặc sử dụng `Gmail` như credentials).
- **From Email**: Địa chỉ email gửi (ví dụ: `sếp@example.com`).
- **To Email**: Địa chỉ email nhận (ví dụ: `sếp@example.com`).
- **Subject**: Thiết lập tiêu đề email (ví dụ: `Cập Nhật Tin Tức Y Combinator Hôm Nay`).
- **HTML Content**: Sử dụng template như sau:
  ```html
  <h2>Danh sách tin tức mới từ Y Combinator</h2>
  <ul>
    {% for item in $json %}
      <li><a href="{{item.url}}">{{item.title}}</a></li>
    {% endfor %}
  </ul>
  ```
- **Lưu ý**:
  - Nếu sử dụng Gmail, các sếp cần bật **Less Secure Apps** hoặc sử dụng **App Password** (nếu đã bật 2FA).
  - Nếu không sử dụng Gmail, các sếp cần thiết lập SMTP khác (ví dụ: SMTP của doanh nghiệp).

##### **g. Node "On clicking 'execute'" (Bật/ Tắt Workflow)**
- **Các sếp không cần chỉnh sửa gì** ở node này, nó chỉ dùng để kích hoạt workflow thủ công (nếu cần).

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**: Các sếp nhấn **Execute** để kiểm tra workflow với dữ liệu mẫu.
2. **Bật Active**: Sau khi kiểm tra thành công, các sếp bật **Active** để workflow chạy tự động hàng ngày.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Thêm Thông Tin Nguồn**:
   - Các sếp có thể thêm cột `Nguồn` vào Google Sheet và tự động trích xuất từ node "HTML Extract" để lưu thông tin chi tiết hơn.

2. **Gửi Email Định Kỳ**:
   - Thay vì gửi email hàng ngày, các sếp có thể sử dụng **n8n Cron Trigger** để chạy workflow vào giờ cụ thể (ví dụ: 8h sáng hàng ngày).

3. **Lưu Log Hoạt Động**:
   - Các sếp có thể thêm node **Log** để ghi lại hoạt động của workflow vào Google Sheets hoặc một file log riêng.

4. **Kết Nối Với Slack/Telegram**:
   - Thay vì chỉ gửi email, các sếp có thể kết nối với **Slack** hoặc **Telegram** để thông báo tin tức mới ngay trên chat.

5. **Lọc Tin Tức Theo Từ Khóa**:
   - Các sếp có thể thêm node **Function** để lọc tin tức chứa từ khóa quan trọng (ví dụ: `AI`, `Blockchain`, `Startup`).

---

### 📌 **Kết Luận**
Workflow này giúp các sếp **tự động hóa việc theo dõi tin tức Y Combinator**, tiết kiệm thời gian và không bỏ lỡ bất kỳ tin tức quan trọng nào. Bằng cách lưu dữ liệu vào Google Sheets và gửi email thông báo, các sếp có thể **quản lý tin tức một cách hiệu quả và chuyên nghiệp**.

**Hãy áp dụng ngay workflow này và bắt đầu tự động hóa công việc hàng ngày của mình!** 🚀

---
**Nếu có bất kỳ câu hỏi hoặc gặp khó khăn trong quá trình setup, các sếp có thể liên hệ với cộng đồng n8n hoặc chia sẻ trên [forum n8n](https://community.n8n.io/) để được hỗ trợ.**