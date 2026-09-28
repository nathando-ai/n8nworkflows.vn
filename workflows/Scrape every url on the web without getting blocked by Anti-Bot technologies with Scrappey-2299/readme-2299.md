---
title: "🤖 Scrape Tất Cả Trang Web Miễn Lo Lại Anti-Bot - Sử Dụng Scrappey + n8n (Không Cần Code)"
description: "Tự động hóa việc scrape toàn bộ URL trên web mà không bị chặn bởi các công nghệ chống bot như Cloudflare, hCaptcha, hoặc reCAPTCHA. Workflow này hoạt động 24/7, tiết kiệm thời gian và đảm bảo dữ liệu chính xác."
slug: "scrape-website-voi-scrappey-tren-n8n"
tags: [n8n, web-scraping, tự động hóa, anti-bot, Scrappey, no-code, API]
keywords: [scrape website tự động, n8n workflow scrape, scrape không bị chặn, Scrappey API, tự động hóa scrape, công cụ scrape web]
---

# 🚀 Scrape Tất Cả Trang Web Miễn Lo Lại Anti-Bot - Sử Dụng Scrappey + n8n

### 🔍 **Nỗi Đau Của Các Sếp**
Bạn đã bao giờ phải mất hàng giờ để scrape dữ liệu từ các trang web mà không thể tránh khỏi việc bị chặn bởi **Cloudflare, hCaptcha, reCAPTCHA** hay các công nghệ chống bot hiện đại? Hoặc bạn phải viết code phức tạp để bypass các hệ thống bảo mật này? **Workflow này giải quyết vấn đề đó 100% không cần code!**

Dùng **Scrappey** (API scrape chuyên nghiệp) kết hợp với **n8n**, bạn có thể:
✅ **Scrape toàn bộ URL** mà không bị chặn.
✅ **Hoạt động tự động 24/7** mà không cần can thiệp thủ công.
✅ **Lấy dữ liệu chính xác** từ các trang web phức tạp (Amazon, Facebook, LinkedIn, blog cá nhân...).
✅ **Tiết kiệm thời gian** lên đến **90%** so với cách làm thủ công.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa scrape** mà không bị chặn bởi bất kỳ hệ thống chống bot nào.
- **Lấy dữ liệu liên tục** từ nhiều trang web khác nhau.
- **Không cần viết code** – chỉ cần cấu hình và chạy.
- **Dữ liệu sạch, chính xác** và có thể lưu trữ hoặc xử lý tiếp theo.
- **Hoạt động 24/7** mà không tốn thời gian giám sát.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Scrappey** (đăng ký tại [Scrappey](https://scrappey.com/?ref=n8n)).
2. **API Key của Scrappey** (mã này sẽ được sử dụng trong workflow).
3. **Danh sách URL** (hoặc một URL mẫu để test).

---
:::info[CHUẨN BỊ]
- **Scrappey API Key**: Lấy từ [Scrappey Dashboard](https://scrappey.com/dashboard) sau khi đăng ký.
- **URL để scrape**: Ví dụ: `https://n8n.io` (hoặc thay thế bằng danh sách URL của bạn).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Bước 1**: Tải file JSON của workflow từ [n8n.io/workflows/2299](https://n8n.io/workflows/2299).
- **Bước 2**: Mở **n8n Editor** và chọn **Import Workflow** (từ menu bên trái).
- **Bước 3**: Chọn file JSON đã tải và nhấn **Import**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **3 node chính**, các sếp cần chú ý cấu hình như sau:

##### **Node 1: Schedule Trigger (Động cơ kích hoạt lịch)**
- **Chức năng**: Chạy workflow theo lịch (ví dụ: hàng ngày, hàng giờ).
- **Cấu hình**:
  - Chọn **Cron expression** phù hợp (ví dụ: `0 0 * * *` để chạy hàng ngày lúc 00:00).
  - **Không cần thay đổi gì** nếu muốn chạy theo lịch mặc định.

##### **Node 2: Test Data (Dữ liệu mẫu)**
- **Chức năng**: Cung cấp URL mẫu để scrape.
- **Cấu hình**:
  - **Thay đổi giá trị** trong `url` từ `https://n8n.io` thành **URL của bạn**.
  - Ví dụ:
    ```json
    {
      "url": "https://example.com"
    }
    ```
  - **Lưu ý**: Nếu muốn scrape nhiều URL, các sếp có thể **lưu trữ danh sách URL trong một file JSON** và sử dụng **node `set`** để truyền danh sách đó vào.

##### **Node 3: Scrape Website with Scrappey (Scrape bằng Scrappey API)**
- **Chức năng**: Gửi yêu cầu scrape đến Scrappey và lấy kết quả.
- **Cấu hình**:
  - **Thay thế `YOUR_API_KEY`** trong header `Authorization` bằng **API Key của bạn**:
    ```json
    {
      "Authorization": "Bearer YOUR_API_KEY"
    }
    ```
  - **Thay đổi URL** trong `url` (nếu không sử dụng node `Test Data`).
  - **Thêm tham số tùy chọn** (nếu cần):
    - `headers`: Thêm header tùy chỉnh (nếu trang web yêu cầu).
    - `proxy`: Sử dụng proxy nếu cần (Scrappey hỗ trợ proxy tự động).
    - `userAgent`: Thay đổi user agent để tránh bị detect.

- **API Endpoint của Scrappey**:
  Scrappey cung cấp API để scrape. Các sếp có thể tham khảo [đây](https://scrappey.com/docs/api) để biết thêm chi tiết về các tham số hỗ trợ.

#### **3. Kích Hoạt ⚡️**
- **Bước 1**: **Test Run** với dữ liệu mẫu để kiểm tra workflow hoạt động.
- **Bước 2**: Nếu kết quả đúng, **bật Active workflow** để chạy tự động.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Scrape nhiều trang web cùng lúc**:
   - Sử dụng **node `set`** để truyền danh sách URL từ một file JSON (ví dụ: `urls.json`).
   - Cấu hình node `httpRequest` để loop qua từng URL trong danh sách.

2. **Lưu kết quả scrape vào Google Sheets/Database**:
   - Thêm **node `googleSheets`** sau node `httpRequest` để lưu dữ liệu vào bảng tính.
   - Hoặc sử dụng **node `database`** (n8n Database) để lưu trữ dữ liệu.

3. **Gửi báo cáo scrape qua Email/Slack**:
   - Thêm **node `email`** hoặc **node `slack`** để thông báo kết quả scrape.
   - Ví dụ: Gửi email báo cáo hàng ngày với dữ liệu mới scrape được.

4. **Sử dụng proxy để tránh bị chặn**:
   - Scrappey tự động quản lý proxy, nhưng các sếp có thể cấu hình proxy riêng trong header `proxy`.

5. **Lọc và xử lý dữ liệu**:
   - Sử dụng **node `function`** để xử lý dữ liệu trước khi lưu hoặc gửi.

---
### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp cần scrape dữ liệu từ web mà **không bị chặn bởi bot detection**, **không cần viết code** và **hoạt động tự động 24/7**.

**Hãy áp dụng ngay và tiết kiệm thời gian, tăng hiệu suất scrape!**
👉 [Tải workflow này](https://n8n.io/workflows/2299) và **cài đặt trên VPS** để bắt đầu scrape ngay!

---
**Cần hỗ trợ?** Hãy để lại bình luận hoặc liên hệ với tác giả [Bela](https://n8n.io/workflows/2299) để được tư vấn chi tiết!