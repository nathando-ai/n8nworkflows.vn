---
title: "🚀 **Monitor Trạng Thái Website Tự Động + Cảnh Báo Email + Trang Status GitHub (Không Cần Code!)**"
description: "Workflow n8n tự động kiểm tra uptime website mỗi 2 phút, gửi email cảnh báo khi server down và cập nhật trang status công khai trên GitHub Pages. Giúp các sếp theo dõi hiệu suất website 24/7 mà không tốn chi phí."
slug: "automated-website-uptime-monitor-email-alerts-github-status-page"
tags: [n8n, devops, tự động hóa, uptime monitoring, github-pages, email-alert, no-code]
keywords: [n8n workflow uptime, tự động hóa kiểm tra website, cảnh báo email khi server down, trang status công khai, gitHub Pages tự động hóa, devops không code]
---

# **🚀 Tự Động Kiểm Tra Website + Cảnh Báo Email + Trang Status GitHub (Không Cần Code!)**

### **Giải pháp hoàn hảo cho các sếp muốn:**
✅ **Biết ngay khi website down** (mỗi 2 phút 1 lần kiểm tra tự động).
✅ **Gửi email cảnh báo chi tiết** (kèm trang alert HTML đẹp mắt).
✅ **Cập nhật trang status công khai** trên GitHub Pages (miễn phí).
✅ **Không cần viết code** – chỉ cần cấu hình n8n là xong!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính riêng tư và ổn định.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## **🎯 Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần phải manual check website hàng giờ.
- **Cảnh báo tức thời**: Nhận email chi tiết khi server down (kèm status code và lỗi).
- **Trang status công khai**: Hiển thị trạng thái website trên GitHub Pages (miễn phí).
- **Tự động hóa hoàn toàn**: Chỉ cần cấu hình 1 lần, workflow chạy tự động mỗi 2 phút.
- **Dễ dàng mở rộng**: Thêm nhiều website khác vào workflow mà không cần code.
:::

---

## **🔧 Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
✔ **Tài khoản n8n** (self-hosted hoặc cloud).
✔ **Tài khoản GitHub** + **Repository** (để lưu trang `index.html`).
✔ **Tài khoản Gmail** (hoặc dịch vụ email khác hỗ trợ n8n, ví dụ: Outlook, Yahoo).
✔ **URL website cần monitor** (ví dụ: `https://app.yourdomain.com/health`).
✔ **GitHub Personal Access Token** (có quyền `repo` để commit file).
✔ **API Key Gmail** (nếu sử dụng Gmail, có thể tạo từ [Google Cloud Console](https://console.cloud.google.com/)).
:::

---

## **🚀 Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/8624](https://n8n.io/workflows/8624).
- **Import vào n8n Editor**:
  - Mở n8n Workflow Editor → Nhấn **Import** → Chọn file JSON vừa tải.
  - Hoặc **copy/paste** JSON từ file vào ô **Import Workflow**.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **10 node** chính, các sếp cần chú ý cấu hình các node sau:

#### **🔹 Node 1: Schedule Trigger (Động cơ lịch)**
- **Cấu hình**:
  - Thời gian chạy mặc định: **2 phút/lần** (có thể thay đổi thành `1m`, `5m`, `1h`, `1d` tùy ý).
  - Ví dụ: `0 */2 * * *` (chạy mỗi 2 phút).

#### **🔹 Node 2: HTTP Request (Kiểm tra website)**
- **Cấu hình**:
  - **URL**: Thay thế `https://app.yourdomain.com/health` thành URL **health check** của website (nên là endpoint trả về status code).
  - **Method**: `GET` (mặc định).
  - **Headers**: Thêm `User-Agent` (ví dụ: `Mozilla/5.0`) để tránh bị chặn.

#### **🔹 Node 3: Switch - status code (Xác định trạng thái)**
- **Cấu hình**:
  - **Condition**:
    - Nếu `statusCode` **bằng 200** → Website **Up**.
    - Nếu `statusCode` **khác 200** (ví dụ: 503, 404, lỗi mạng) → Website **Down**.

#### **🔹 Node 4: Template HTML Code (Tạo trang alert)**
- **Cấu hình**:
  - **Mô tả**: Node này **tạo động HTML** cho trang status (Up/Down).
  - **Nội dung mẫu**:
    ```html
    <!DOCTYPE html>
    <html>
    <head>
        <title>Website Status</title>
        <style>
            body { font-family: Arial; text-align: center; margin-top: 50px; }
            .up { color: green; }
            .down { color: red; }
        </style>
    </head>
    <body>
        <h1>{{ $json["status"] === "Up" ? "✅ Website is UP" : "❌ Website is DOWN" }}</h1>
        <p>Last checked: {{ $json["timestamp"] }}</p>
        {% if $json["status"] === "Down" %}
            <p>Status Code: <strong>{{ $json["statusCode"] }}</strong></p>
            <p>Error: <strong>{{ $json["error"] }}</strong></p>
        {% endif %}
    </body>
    </html>
    ```
  - **Thay đổi**:
    - Thêm logo, màu sắc, hoặc nội dung tùy chỉnh theo branding.
    - Sử dụng biến `{{ $json["status"] }}`, `{{ $json["statusCode"] }}`, `{{ $json["error"] }}` để hiển thị thông tin động.

#### **🔹 Node 5: Gmail (Gửi email cảnh báo)**
- **Cấu hình**:
  - **Credentials**: Thêm tài khoản Gmail (hoặc SMTP khác).
  - **Email To**: Thay thế `example@gmail.com` thành email của mình (hoặc nhóm DL).
  - **Subject**: `🚨 Website Down: {{ $json["statusCode"] }}` (có thể tùy chỉnh).
  - **HTML Content**: Sử dụng nội dung từ **Node 4 (Template HTML)** để hiển thị trang alert.
  - **Example**:
    ```html
    <h2>Website Alert</h2>
    <p>Website <strong>{{ $json["url"] }}</strong> is <strong>{{ $json["status"] }}</strong>.</p>
    <p>Status Code: <strong>{{ $json["statusCode"] }}</strong></p>
    {% if $json["error"] %}<p>Error: <strong>{{ $json["error"] }}</strong></p>{% endif %}
    ```

#### **🔹 Node 6: GitHub (Cập nhật trang status)**
- **Cấu hình**:
  - **Credentials**: Thêm **GitHub Personal Access Token** (có quyền `repo`).
  - **Repository URL**: Thay thế `https://github.com/<OWNER>/<REPO>` thành repo của mình (ví dụ: `https://github.com/linearloop/status`).
  - **Branch**: `main` (hoặc `master`).
  - **File Path**: `index.html` (nên tạo file này trước trong repo).
  - **Content**: Sử dụng nội dung từ **Node 4 (Template HTML)**.
  - **Commit Message**: `Update status page` (có thể tùy chỉnh).

#### **🔹 Node 7: Extract from File (Github) & If (So sánh file)**
- **Cấu hình**:
  - **Node "Extract from existing File (github)"**: Trích xuất nội dung hiện tại của `index.html`.
  - **Node "If - Compare existing HTML file with generated HTML"**:
    - Nếu **nội dung mới ≠ nội dung cũ** → Thực hiện commit cập nhật.
    - Nếu **nội dung giống nhau** → Bỏ qua (không commit).

---

### **3. Kích hoạt ⚡️**
- **Test Run**:
  - Nhấn **Run Workflow** để kiểm tra dữ liệu mẫu.
  - Kiểm tra email và trang GitHub Pages xem có cập nhật không.
- **Bật Active**:
  - Sau khi cấu hình xong, chuyển workflow sang **Active**.

---

## **✍️ Mẹo & gợi ý nâng cao**
:::tip[CÁCH LÀM NÀY ĐỂ TIẾT KIỆM THỜI GIAN]
- **Monitor nhiều website**: Sao chép **HTTP Request + Switch** và thay đổi URL để kiểm tra nhiều trang.
- **Thêm Slack/Telegram**: Sử dụng node **Slack Webhook** hoặc **Telegram Bot** để gửi cảnh báo ngay khi server down.
- **Log lỗi**: Thêm node **Sticky Note** để lưu lịch sử lỗi vào một file CSV.
- **Báo cáo định kỳ**: Sử dụng **Schedule Trigger** khác để gửi báo cáo tổng hợp hàng tuần.
- **Tùy chỉnh email**: Thêm **node Code** trước **Gmail** để động HTML email theo phong cách riêng.
:::

---

## **📌 Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn:
✔ **Biết ngay khi website down** mà không cần manual check.
✔ **Cảnh báo email chi tiết** với trang alert HTML đẹp mắt.
✔ **Cập nhật trang status công khai** trên GitHub Pages (miễn phí).
✔ **Không cần viết code** – chỉ cần cấu hình n8n là xong!

**🚀 Hãy áp dụng ngay và tự động hóa việc monitor website của mình!**
Nếu có thắc mắc, các sếp có thể comment bên dưới hoặc liên hệ với **Linearloop Team** qua [n8n.io](https://n8n.io).

---
**💡 Lưu ý cuối cùng**:
- **GitHub Pages** phải được kích hoạt trong **Settings → Pages** của repo.
- **URL health check** nên trả về **status code** (200/503) để workflow phân tích chính xác.
- **Email Gmail** cần **2FA bị tắt** (n8n không hỗ trợ 2FA). Nếu cần, sử dụng **SMTP khác** như Outlook.