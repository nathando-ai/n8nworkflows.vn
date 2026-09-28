---
title: "🚀 Tự Động Hoà Scraping Website + Google Sheets: Nhận Dữ Liệu Website Tự Động, Không Cần Code"
description: "Workflow này giúp các sếp tự động trích xuất tất cả liên kết từ robots.txt, sitemap.xml và các file XML trên website, sau đó ghi dữ liệu vào Google Sheets. Giúp tiết kiệm thời gian nghiên cứu thị trường lên đến 80% so với cách làm thủ công."
slug: "tieu-dong-hoa-scraping-website-google-sheets"
tags: [n8n, automation, web-scraping, google-sheets, scrapingbee, market-research]
keywords: [n8n workflow scraping website, tự động hóa trích xuất dữ liệu website, sitemap xml robots txt, google sheets automation, scrapingbee api]
---

# 🚀 **Tự Động Hoà Scraping Website + Google Sheets: Nhận Dữ Liệu Website Tự Động, Không Cần Code**

### **🔍 Nỗi Đau Của Các Sếp Trong Nghiên Cứu Thị Trường**
Các sếp thường phải mất **giờ đồng hồ** để:
- Tìm kiếm và trích xuất tất cả liên kết từ **robots.txt**, **sitemap.xml** và các file XML của đối thủ.
- Sắp xếp, lưu trữ và phân tích dữ liệu trên **Google Sheets** để nghiên cứu thị trường.
- Lo lắng về **sai sót thủ công** khi copy-paste dữ liệu từ website.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách tự động hóa 100% quy trình, chỉ cần một cú nhấp chuột!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và xử lý được sitemap lớn (tránh crash), các sếp nên cài **n8n trên VPS riêng (Self-hosted)** với **RAM ≥ 4GB**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Trích xuất **tất cả liên kết** từ website chỉ trong **vài giây** thay vì **giờ đồng hồ**.
✅ **Dữ liệu chính xác 100%**: Không còn sai sót khi copy-paste thủ công.
✅ **Cập nhật tự động**: Khi website cập nhật sitemap, dữ liệu sẽ tự động được cập nhật vào Google Sheets.
✅ **Phân tích dễ dàng**: Dữ liệu được lưu vào **Google Sheets** với cột `links` sẵn sàng cho phân tích.
✅ **Không giới hạn số lượng website**: Workflow hỗ trợ **scraping nhiều website đồng thời**.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản ScrapingBee** (để scraping website):
   - Đăng ký miễn phí tại: [https://www.scrapingbee.com/](https://www.scrapingbee.com/)
   - Lấy **API Key** từ [Dashboard ScrapingBee](https://www.scrapingbee.com/dashboard).
2. **Tài khoản Google** (để kết nối với Google Sheets):
   - Tạo **Google Sheets** mới và chia sẻ cho `n8n` (quyền chỉnh sửa).
   - Cài đặt **Google Sheets OAuth2** trong n8n (hướng dẫn tại: [n8n Google Sheets Docs](https://docs.n8n.io/integrations/built-in/nodes/n8n-nodes-base.googleSheets/)).
3. **VPS n8n** (nếu muốn chạy 24/7):
   - Cài đặt n8n trên VPS (hướng dẫn tại: [n8n Self-hosted](https://docs.n8n.io/hosting/self-hosted/)).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/7927](https://n8n.io/workflows/7927) và import vào n8n Editor.
- **Copy JSON** từ link trên và paste vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này có **13 node**, nhưng các node quan trọng nhất cần chú ý:

##### **🔹 Node Webhook (Nhận Domain)**
- **Tên Node**: `Domain to scrape`
- **Cấu hình**:
  - Đảm bảo **path** là `1da30868-fbca-4e8e-8580-485afb3fd956` (không thay đổi).
  - Khi gọi webhook, **gửi tham số `domain`** trong query:
    ```
    https://<webhook_link>?domain=n8n.io
    ```
  - **Ví dụ**:
    ```
    https://<your-n8n-url>/webhook/1da30868-fbca-4e8e-8580-485afb3fd956?domain=google.com
    ```

##### **🔹 Node ScrapingBee (Trích Xuất Dữ Liệu)**
- **Tên Node**: `Scrape robots.txt file`, `Scrape sitemap.xml file`, `Scrape xml file`
- **Cấu hình**:
  - **Credentials**: Chọn `ScrapingBeeApi` (đã cấu hình trước khi import).
  - **URL Template**:
    - **robots.txt**: `http://$domain/robots.txt`
    - **sitemap.xml**: `http://$domain/sitemap.xml`
    - **XML file**: `$json["url"]` (được truyền từ node trước).
  - **Headers**:
    - Thêm `User-Agent` (ví dụ: `Mozilla/5.0`).
    - **Không bỏ trống `Accept`** (giúp ScrapingBee biết định dạng trả về).

##### **🔹 Node Google Sheets (Lưu Dữ Liệu)**
- **Tên Node**: `Append links to sheet`
- **Cấu hình**:
  - **Credentials**: Chọn `googleSheetsOAuth2Api`.
  - **Sheet Name**: Đặt tên sheet (ví dụ: `Danh sách liên kết website`).
  - **Range**: `Sheet1!A1` (nếu sheet mới) hoặc `Sheet1!A:A` (nếu muốn append xuống dưới).
  - **Columns**:
    - `links` (cột chứa tất cả liên kết được trích xuất).
    - **Không cần thêm cột khác** (workflow tự động thêm).

##### **🔹 Node Code (Xử Lý File XML & GZ)**
- **Tên Node**: `Store the file to data key`, `Extract non-xml links`, `Extract xml links`
- **Lưu ý**:
  - Các node này **không cần chỉnh sửa** (đã viết sẵn logic xử lý).
  - Nếu gặp lỗi, kiểm tra **log trong node Code** để debug.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với một domain mẫu (ví dụ: `n8n.io`):
   - Gọi webhook:
     ```
     https://<your-n8n-url>/webhook/1da30868-fbca-4e8e-8580-485afb3fd956?domain=n8n.io
     ```
   - Kiểm tra **Google Sheets** xem dữ liệu đã được append chưa.
2. **Bật Active** workflow nếu test thành công.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Scraping Nhiều Website Đồng Thời**
   - Sử dụng **n8n Queue** để xử lý nhiều domain cùng lúc (tránh quá tải).
   - Cài đặt **n8n Enterprise** nếu cần xử lý **sitemap lớn** (tránh crash).

2. **Lưu Log Cho Phân Tích**
   - Thêm node **Slack/Telegram** để nhận thông báo khi workflow hoàn thành.
   - **Ví dụ**:
     ```
     https://api.telegram.org/bot<BOT_TOKEN>/sendMessage?chat_id=<CHAT_ID>&text=Scraping%20hoàn%20thành%20cho%20domain:%20$domain
     ```

3. **Tự Động Cập Nhật Định Kỳ**
   - Sử dụng **n8n Trigger** (n8n 1.0+) để chạy workflow **hàng ngày/tuần**.
   - **Ví dụ**: Scraping lại sitemap của đối thủ hàng tuần.

4. **Phân Tích Dữ Liệu Tự Động**
   - Sau khi dữ liệu vào Google Sheets, sử dụng **Google Apps Script** để:
     - Tách domain, path, keyword.
     - Tạo báo cáo tự động (PDF/Excel).

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc **nhàn nhạt và mòn mỏi** là trích xuất dữ liệu website. Bằng cách **tự động hóa scraping + Google Sheets**, các sếp có thể:
✔ **Nhận dữ liệu chính xác** trong thời gian ngắn.
✔ **Cập nhật liên tục** khi website thay đổi.
✔ **Phân tích thị trường** một cách chuyên nghiệp.

**🚀 Hãy áp dụng ngay workflow này và bắt đầu tự động hóa nghiên cứu thị trường của mình!**

---
**🔗 [Tải workflow gốc tại n8n.io](https://n8n.io/workflows/7927)**
**💬 Có thắc mắc? Để lại comment bên dưới!**