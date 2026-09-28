---
title: "🎮 **Tự Động Thông Báo Trên Discord Khi Game Miễn Phí Epic Games Ra Mới** - Không Cần Code!"
description: "Workflow tự động hóa 24/7 để các sếp và game thủ nhận thông báo tức thời khi các game miễn phí mới trên Epic Games ra mắt, với hình ảnh và trạng thái chính xác. Giúp tiết kiệm thời gian tra cứu và không bỏ lỡ bất kỳ game hot nào!"
slug: "tu-dong-thong-bao-discord-epic-games-free-game"
tags: [n8n, automation, no-code, discord, epic-games, puppeteer]
keywords: [n8n workflow discord, tự động hóa game miễn phí, puppeteer n8n, thông báo game mới, epic games automation]
---

# 🚀 **Tự Động Thông Báo Trên Discord Khi Game Miễn Phí Epic Games Ra Mới**

## **💥 Nỗi Đau Của Các Sếp & Game Thủ**
Bạn có bao giờ phải **quét liên tục trang Epic Games** để tìm game miễn phí mới ra mắt? Hay **bỏ lỡ game hot** vì không kịp tra cứu? Với workflow này, **không cần code**, bạn sẽ được **thông báo tức thời** trên Discord khi có game mới miễn phí, **kèm hình ảnh và trạng thái** (Free Now / Coming Soon), giúp tiết kiệm **tối thiểu 5-10 giờ/tuần** tra cứu thủ công.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
✅ **Tự động hóa 100%**: Không cần can thiệp thủ công, chạy 24/7.
✅ **Thông báo tức thời**: Nhận tin tức game mới ngay khi ra mắt.
✅ **Hình ảnh & trạng thái chi tiết**: Game nào **Free Now**, game nào **Coming Soon** được phân biệt rõ ràng.
✅ **Không bỏ lỡ game hot**: Duy trì danh sách game mới nhất, không phụ thuộc vào email hoặc thông báo push.
✅ **Kết hợp với Discord**: Thông báo ngay trên kênh game của bạn, không cần mở nhiều tab.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ**]
- **Tài khoản Discord**: Để nhận thông báo (cần **Webhook URL** từ kênh Discord).
- **n8n Self-hosted**: Workflow này **không chạy được trên n8n.cloud** do sử dụng **Puppeteer** (bị chặn bởi Cloudflare).
  👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
  👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)**
- **Node `n8n-nodes-puppeteer`**: Cần cài đặt để tránh bị chặn bởi Cloudflare.
- **Thời gian chạy**: Workflow sẽ **lặp lại request** nếu trang Epic Games không trả về kết quả (do Cloudflare).
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/4701) hoặc copy **JSON từ canvas**.
- Mở **n8n Editor** → **Import Workflow** → Dán JSON và nhấn **Import**.

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này **không hoạt động ngay lập tức** do phụ thuộc vào nhiều yếu tố. Dưới đây là **các bước cấu hình chi tiết**:

#### **🔹 Node "Schedule Trigger"**
- **Thiết lập lịch chạy**: Đặt thời gian chạy **mỗi 1-2 giờ** (do Epic Games thường cập nhật game miễn phí vào buổi sáng).
- **Lưu ý**: Nếu chạy quá thường xuyên, có thể bị **Cloudflare chặn** (do nhiều request liên tiếp).

#### **🔹 Node "GET Epic Games Free Games page" (Puppeteer)**
- **Sử dụng Puppeteer**: Node này **truy cập trang Epic Games** và **trích xuất dữ liệu game miễn phí**.
- **Lỗi thường gặp**:
  - **Trang trống**: Do Cloudflare chặn, cần **lặp lại request** (được xử lý trong workflow).
  - **CSS Selector thay đổi**: Nếu Epic Games thay đổi trang, **workflow sẽ thất bại**. Cần **cập nhật lại selector** trong node `Extract offers` và `Extract title and image`.
- **Mẹo**: Nếu bị chặn, **tăng thời gian chờ** (`Wait between requests`) để tránh bị detect.

#### **🔹 Node "Prepare notification" (Code)**
- **Template thông báo Discord**:
  ```plaintext
  ### Epic Games
  New games detected
  ```
  - **Cấu trúc embed**:
    ```
     ______________________
    | GAME 1     [ IMAGE ] |
    | Free Now   [       ] |
    |______________________|
     ```
  - **Lưu ý**: Nếu **không có game mới**, workflow sẽ **không gửi thông báo** (do logic `Only when changed`).

#### **🔹 Node "Notify Discord" (HTTP Request)**
- **Cần Webhook URL từ Discord**:
  1. Mở kênh Discord → **Settings** → **Integrations** → **Webhooks** → **New Webhook**.
  2. Copy **Webhook URL** và dán vào node `Notify Discord` (tham số `Url`).
  3. **Payload**: Sử dụng **JSON template** từ node `Prepare notification`.

#### **🔹 Node "Save Static Data" (Code)**
- **Lưu trữ "hash" của game cũ**: Để so sánh với game mới trong lần chạy tiếp theo.
- **Lưu ý**: Nếu **không lưu được**, workflow sẽ **gửi thông báo cho tất cả game** (không phân biệt mới/đã có).

---

### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Chạy **manual test** với **dữ liệu mẫu** (nếu có).
   - Kiểm tra **Discord** xem có nhận được thông báo không.
2. **Active Workflow**:
   - Sau khi **cấu hình hoàn chỉnh**, bật **Active** và **đặt lịch chạy tự động**.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[**CẬP NHẬT & TỐT HÓA**]
- **Kết hợp với Telegram/Email**: Thay vì chỉ Discord, có thể **gửi thông báo đa kênh** bằng node `email` hoặc `telegram`.
- **Lưu log vào Google Sheets/Notion**: Để **theo dõi lịch sử game** đã thông báo.
- **Báo cáo định kỳ**: Sử dụng node `set` + `scheduleTrigger` để **gửi báo cáo tuần/month** về game miễn phí.
- **Cập nhật selector khi Epic Games thay đổi trang**: Nếu workflow **bị lỗi**, kiểm tra **HTML source** và **cập nhật lại CSS selector** trong node `Extract offers` và `Extract title and image`.
:::

---

## 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp và game thủ khỏi việc **tra cứu thủ công** game miễn phí trên Epic Games. Với **tự động hóa 100%**, bạn sẽ **không bao giờ bỏ lỡ game hot** nữa!

👉 **Bắt đầu ngay**:
1. **Cài đặt n8n trên VPS** (để tránh bị chặn).
2. **Import workflow** và **cấu hình Discord Webhook**.
3. **Bật chạy** và **nhận game miễn phí ngay trên Discord!**

**Chia sẻ workflow này cho bạn bè game thủ** để cùng **tiết kiệm thời gian**! 🎮🚀