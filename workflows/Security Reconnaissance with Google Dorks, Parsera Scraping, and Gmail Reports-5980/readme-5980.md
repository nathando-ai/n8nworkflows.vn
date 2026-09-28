---
title: "🔍 **Tự Động Hoàn Thành Báo Cáo An Toàn Mạng với Google Dorks, Scraping Parsera & Gmail (Không Cần Code!)**"
description: "Workflow tự động hóa tìm kiếm thông tin nhạy cảm trên web bằng Google Dorks, scrape dữ liệu từ Parsera, và gửi báo cáo định kỳ qua Gmail. Giúp các sếp SecOps tiết kiệm 80% thời gian phân tích thủ công."
slug: "tieu-dong-hoan-thanh-bao-cao-an-toan-mang-google-dorks-parsera-gmail"
tags: [n8n, automation, secops, google-dorks, scraping, gmail-automation]
keywords: [n8n workflow secops, tự động hóa tìm kiếm an toàn mạng, google dorks automation, scrape website tự động, báo cáo an toàn mạng qua email]
---

# 🚀 **Tự Động Hoàn Thành Báo Cáo An Toàn Mạng với Google Dorks, Scraping & Gmail**

### **Nỗi Đau Của Các Sếp SecOps**
Hàng ngày, các sếp phải:
- **Tìm kiếm thủ công** thông tin nhạy cảm trên web bằng Google Dorks (tốn thời gian và dễ bỏ lỡ).
- **Scrape dữ liệu** từ nhiều trang web khác nhau để phân tích (rủi ro vi phạm pháp luật nếu không đúng cách).
- **Tập hợp và gửi báo cáo** qua email định kỳ (lặp đi lặp lại, dễ sai sót).

**Workflow này giải quyết tất cả!** Sử dụng **Google Dorks**, **scraping tự động với Parsera**, và **gửi báo cáo qua Gmail** một cách hoàn toàn tự động, **không cần viết một dòng code nào**.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**Lợi Ích Cốt Lõi**]
✅ **Tiết kiệm 80% thời gian** phân tích thủ công.
✅ **Tìm kiếm chính xác** thông tin nhạy cảm trên web bằng Google Dorks.
✅ **Scrape dữ liệu an toàn** với Parsera (không cần viết script).
✅ **Báo cáo tự động** qua Gmail, không cần nhớ gửi.
✅ **Cập nhật liên tục** khi có dữ liệu mới (không giới hạn thời gian làm việc).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[**Chuẩn Bị Trước Khi Lên Đồ**]
- **Tài khoản Google** (để sử dụng Gmail và Google Dorks).
- **Tài khoản Parsera** (để scrape dữ liệu):
  - Tạo **1 agent mới** tên **"Google"** (hướng dẫn chi tiết bên dưới).
  - API Key của Parsera (mua tại [Parsera](https://www.parsera.io/)).
- **Gmail OAuth2** (để gửi báo cáo tự động).
- **URL website** cần scrape (ví dụ: `https://example.com`).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/5980](https://n8n.io/workflows/5980).
- **Mở n8n Editor** → **Import Workflow** → Chọn file JSON đã tải.
- **Hoặc copy/paste** JSON từ file vào Editor.

#### **2. Cấu Hình Cần Thiết (BẮT BUỘC Chỉnh!)**
##### **🔹 Node 1: Form Input (Đầu vào)**
- **Không cần chỉnh** (sử dụng mặc định để nhập URL).

##### **🔹 Node 2: Split Dorks One-by-One (Chia nhỏ Dorks)**
- **Không cần chỉnh** (auto split từ input).

##### **🔹 Node 3: Dorks Template Search (Tạo liên kết Google Dorks)**
- **Không cần chỉnh** (sử dụng template mặc định).

##### **🔹 Node 4: Scrape with agent (Parsera Scraping)**
:::warning[**LƯU Ý QUAN TRỌNG**]
- **Tạo agent "Google" trên Parsera**:
  1. Đăng nhập [Parsera Dashboard](https://www.parsera.io/).
  2. Tạo **1 agent mới** → Tên: **"Google"**.
  3. Nhập URL mẫu: `https://google.com`.
  4. Lưu agent và lấy **API Key** của nó.
- **Cấu hình node**:
  - **Credentials**: Chọn `aiScraperApi` (đã tạo trước).
  - **Agent Name**: Nhập `"google"` (phải trùng với tên agent trên Parsera).
  - **URL Input**: Điền vào `{{ $node["Form Input"].json["url"] }}` (auto lấy từ Form Input).
:::

##### **🔹 Node 5: Clean Output (Làm sạch dữ liệu)**
- **Không cần chỉnh** (auto xử lý dữ liệu raw).

##### **🔹 Node 6: Generate HTML (Tạo báo cáo HTML)**
- **Không cần chỉnh** (auto chuyển dữ liệu thành HTML).

##### **🔹 Node 7: Send a message (Gửi qua Gmail)**
:::info[**Cấu Hình Gmail**]
1. **Double click** vào node này.
2. **Chọn credentials**: `gmailOAuth2` (đã cấu hình OAuth2).
3. **Điền địa chỉ email nhận**:
   - `{{ $node["Form Input"].json["email"] }}` (auto lấy từ Form Input).
   - **Hoặc** nhập email cố định (ví dụ: `team@company.com`).
4. **Chủ đề email**: `{{ $node["Form Input"].json["subject"] }}` (auto lấy từ Form Input).
5. **Nội dung email**: Chọn `HTML` (để hiển thị báo cáo đẹp).
:::

#### **3. Kích Hoạt Workflow ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhập **URL website** cần scrape (ví dụ: `https://example.com`).
   - Nhập **email nhận báo cáo**.
   - Chạy **Test Execution** để kiểm tra.
2. **Bật Active** nếu test thành công.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[**Cách Sử Dụng Hiệu Quả**]
- **Tự động hóa định kỳ**:
  - Sử dụng **n8n Trigger (HTTP/Schedule)** thay vì Form Input để chạy hàng ngày.
  - Ví dụ: Chạy workflow vào **8h sáng** để gửi báo cáo hàng ngày.
- **Lưu log scrape**:
  - Thêm node **Google Sheets** để lưu dữ liệu scrape vào bảng tính.
- **Kết hợp với Slack/Telegram**:
  - Thêm node **Slack Webhook** để thông báo khi có dữ liệu mới.
- **Tăng cường an toàn**:
  - Sử dụng **IP Proxy** trong Parsera để tránh bị chặn.
  - **Xóa dữ liệu nhạy cảm** trước khi gửi qua email (sử dụng node **Code** thêm logic).
:::

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp SecOps khỏi công việc lặp đi lặp lại, đồng thời **cung cấp báo cáo chính xác và tự động hóa hoàn toàn**. **Không cần viết code**, chỉ cần **cấu hình vài bước** là có thể sử dụng ngay!

**👉 Bắt đầu tự động hóa ngay hôm nay!**
1. **Cài n8n Self-hosted** trên VPS (để workflow chạy 24/7).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Chạy test** và **bật Active** để bắt đầu!

---
:::success[**Gợi Ý Hạ Tầng**]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**🚀 Hãy tự động hóa ngay và tập trung vào công việc quan trọng hơn!** 🚀