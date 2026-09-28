---
title: "🚀 **Tự Động Hóa Kiểm Tra Trạng Thái Website Hàng Giờ Với Thông Báo Slack Tự Động** – Giảm Thiểu Downtime Cho Doanh Nghiệp"
description: "Workflow tự động hóa kiểm tra trạng thái website hàng giờ và gửi thông báo Slack ngay khi website down, giúp các sếp phát hiện và khắc phục sự cố nhanh chóng, tối ưu hóa thời gian và giảm thiểu mất mát doanh thu."
slug: "tieu-dong-hoa-kiem-tra-trang-thai-website-hang-gio"
tags: [n8n, automation, DevOps, uptime-monitor, slack-notification]
keywords: [n8n workflow uptime, tự động hóa kiểm tra website, alert slack khi website down, tự động hóa DevOps, n8n cron job]
---

# 🚀 **Tự Động Hóa Kiểm Tra Trạng Thái Website Hàng Giờ Với Thông Báo Slack Tự Động**

### **Giải Pháp Cho Nỗi Đau "Website Down" – Mất Doanh Thu Và Thời Gian**
Các sếp đã bao giờ phải ngồi chờ website của mình bị down, mất hàng giờ để phát hiện và khắc phục sự cố? Hay phải chịu thiệt hại từ mất doanh thu do downtime không được phát hiện kịp thời? **Workflow này sẽ tự động hóa toàn bộ quy trình**, giúp bạn:
- **Kiểm tra trạng thái website hàng giờ** (không cần can thiệp thủ công).
- **Nhận thông báo Slack ngay lập tức** khi website down.
- **Tiết kiệm thời gian** và giảm thiểu rủi ro mất doanh thu.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Phát hiện sự cố nhanh chóng** – Kiểm tra tự động hàng giờ, không bỏ lỡ bất kỳ downtime nào.
✅ **Thông báo tức thời** – Nhận cảnh báo Slack ngay khi website down, giúp phản ứng nhanh chóng.
✅ **Tự động hóa hoàn toàn** – Không cần can thiệp thủ công, hoạt động 24/7 mà không tốn thời gian.
✅ **Giảm thiểu mất mát** – Tránh mất doanh thu do downtime không được phát hiện kịp thời.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
- **Tài khoản Slack** (để nhận thông báo).
- **API Key Slack** (để kết nối với Slack).
- **URL website** cần được monitor (ví dụ: `https://tênwebsite.com`).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Truy cập [n8n.io](https://n8n.io/) và đăng nhập vào tài khoản.
2. Vào **Workflow** → **Import Workflow**.
3. Chọn file JSON hoặc paste JSON từ [đây](https://n8n.io/workflows/6467) (hoặc copy từ link trên).
4. Nhấn **Import**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này bao gồm **4 node chính**, các sếp cần cấu hình như sau:

##### **Node 1: Schedule Monitor (Every Hour)**
- **Loại node:** `n8n-nodes-base.cron`
- **Cấu hình:**
  - **Schedule:** `0 * * * *` (chạy hàng giờ).
  - **Time Zone:** Chọn múi giờ phù hợp (ví dụ: `Asia/Ho_Chi_Minh`).
  - **Active:** Đánh dấu ✅.

##### **Node 2: Check Website HTTP Status**
- **Loại node:** `n8n-nodes-base.httpRequest`
- **Cấu hình:**
  - **Method:** `GET`.
  - **URL:** Điền **URL website** cần monitor (ví dụ: `https://tênwebsite.com`).
  - **Response Format:** Chọn `JSON`.
  - **Credentials:** Không cần (nếu website không yêu cầu auth).

##### **Node 3: If Website is Down**
- **Loại node:** `n8n-nodes-base.if`
- **Cấu hình:**
  - **Condition:** `{{ $json["statusCode"] }} != 200` (nếu statusCode khác 200, website down).
  - **True Branch:** Kết nối với **Node 4 (Send a message)**.

##### **Node 4: Send a Message (Slack Alert)**
- **Loại node:** `n8n-nodes-base.slack`
- **Cấu hình:**
  - **Credentials:** Chọn hoặc tạo **Slack API Token** (tạo từ [API Slack](https://api.slack.com/apps)).
  - **Channel:** Chọn **#channel** muốn nhận thông báo (ví dụ: `#alerts`).
  - **Message:** Điền nội dung cảnh báo (ví dụ: `🚨 Website DOWN! URL: {{ $input["url"] }}`).
  - **Attachments:** Có thể thêm thông tin chi tiết như `{{ $json["statusCode"] }}`.

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Chạy workflow và kiểm tra nếu website down, Slack sẽ gửi thông báo.
2. **Bật Active workflow**:
   - Đánh dấu **Active** ở góc trên bên phải.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::note[CÁC Ý TƯỞNG MỞ RỘNG]
- **Kết hợp với Email Alert:** Thêm node `n8n-nodes-base.email` để gửi email cảnh báo cho team.
- **Lưu Log Downtime:** Sử dụng node `n8n-nodes-base.googleSheets` để ghi lại lịch sử downtime.
- **Monitor Nhiều Website:** Sử dụng **Sticky Note** (`n8n-nodes-base.stickyNote`) để lưu danh sách URL cần monitor.
- **Thông Báo Telegram:** Thêm node `n8n-nodes-base.telegram` để nhận cảnh báo trên Telegram.
:::

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa kiểm tra uptime website và nhận thông báo tức thời khi có sự cố. **Không cần code, không tốn thời gian**, chỉ cần cấu hình và chạy 24/7.

👉 **Hãy áp dụng ngay và bảo vệ doanh nghiệp của mình khỏi downtime!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::