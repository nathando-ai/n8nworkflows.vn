---
title: "🚀 Tự Động Chuyển Động Telegram Sang X (Twitter), Threads & LinkedIn Với @Mention – Giảm Thời Gian Tạo Nội Dung Gấp 10 Lần"
description: "Workflow tự động hóa chuyển bài viết từ Telegram sang 3 nền tảng X (Twitter), Threads và LinkedIn chỉ với 1 tin nhắn có @mention. Giúp các sếp tiết kiệm thời gian, tối ưu hóa nội dung và tăng tầm tiếp cận trên mạng xã hội."
slug: "tu-dong-chuyen-dong-telegram-sang-x-threads-linkedin"
tags: [n8n, automation, social-media, no-code, cross-posting]
keywords: [n8n workflow tự động hóa, chuyển bài viết Telegram sang Twitter, tự động hóa LinkedIn, tự động hóa Threads, @mention tự động hóa]
---

# 🚀 **Tự Động Chuyển Động Telegram Sang X (Twitter), Threads & LinkedIn – Không Cần Code!**

### **Nỗi Đau Của Các Sếp Trong Tạo Nội Dung Mạng Xã Hội**
Các sếp thường phải mất **giờ đồng hồ** để sao chép nội dung từ Telegram (hoặc các nguồn khác) và đăng lại trên **X (Twitter), LinkedIn và Threads** một cách thủ công. Điều này không chỉ tốn thời gian mà còn dễ gây **lỗi sai sót** (quên đăng, nội dung không đồng nhất) và **gián đoạn** khi phải làm nhiều việc cùng lúc.

**Workflow này giải quyết hoàn toàn vấn đề đó!** Chỉ với **một tin nhắn Telegram có @mention**, nội dung của bạn sẽ tự động được chuyển sang **3 nền tảng lớn** trong giây lát, giúp bạn:
✅ **Tiết kiệm thời gian** (không phải copy-paste thủ công)
✅ **Nội dung đồng nhất** (tránh sai sót khi đăng lại)
✅ **Tăng tầm tiếp cận** (đăng trên nhiều nền tảng cùng lúc)
✅ **Hoạt động 24/7** (không cần phải ngồi theo dõi)

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **ổn định 24/7**, các sếp nên **self-host n8n** trên VPS riêng để tránh giới hạn của phiên bản cloud.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** – giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ sức mạnh cho workflow này)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 5-10 giờ/tuần** so với cách làm thủ công.
- **Nội dung đồng nhất** trên tất cả nền tảng (không sai sót).
- **Tăng engagement** vì bài viết được đăng trên **3 nền tảng cùng lúc**.
- **Hoạt động tự động** mà không cần can thiệp.
- **Dễ dàng mở rộng** (thêm Facebook, Instagram, TikTok sau này).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản Telegram Bot** (tạo từ @BotFather và thêm làm admin vào channel).
✔ **Credentials OAuth2 cho X (Twitter)** (tạo từ [Developer Portal](https://developer.twitter.com/)).
✔ **Credentials OAuth2 cho LinkedIn** (tạo từ [LinkedIn Developer](https://www.linkedin.com/developers/)).
✔ **Access Token cho Threads** (theo hướng dẫn [đây](https://www.youtube.com/watch?v=nC1-KZabm6U)).
✔ **Chat ID Telegram** để nhận thông báo thành công/thất bại.

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/13013](https://n8n.io/workflows/13013) và import vào **n8n Editor**.
- **Cách 2:** Copy toàn bộ JSON và **paste** vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **15 node**, nhưng các bước quan trọng nhất cần chú ý:

##### **A. Cấu Hình Credentials (Bắt Buộc)**
| Node | Yêu Cầu Cấu Hình | Ghi Chú |
|------|------------------|---------|
| **Telegram Trigger** | Thiết lập `telegramApi` (API Key từ BotFather) | Đảm bảo bot có quyền admin trong channel. |
| **Create Tweet (X)** | Thiết lập `twitterOAuth2` (Credentials OAuth2 từ Twitter) | Kiểm tra lại **Permissions** trong Developer Portal. |
| **Create a post (LinkedIn)** | Thiết lập `linkedInOAuth2` (Credentials OAuth2 từ LinkedIn) | Chọn **Publisher** trong LinkedIn Developer. |
| **Create Thread** | Thiết lập `httpBearerAuth` (Access Token Threads) | **Lưu ý:** Token chỉ hiệu lực **2 tháng**, cần refresh theo hướng dẫn. |
| **Notifications (Telegram)** | Thiết lập `telegramApi` (Chat ID để nhận thông báo) | Điền **ID chat** của bot hoặc nhóm để nhận phản hồi. |

##### **B. Cấu Hình Switch (Node "Switch")**
- Node này **xác định nền tảng cần đăng** dựa trên **@mention** trong tin nhắn Telegram.
- **Cách hoạt động:**
  - `@x` → Chỉ đăng trên **X (Twitter)**.
  - `@threads` → Chỉ đăng trên **Threads**.
  - `@linkedin` → Chỉ đăng trên **LinkedIn**.
  - `@all` → Đăng trên **tất cả 3 nền tảng**.

##### **C. Lọc Nội Dung (Node "Parse Telegram Message")**
- **Code trong node này** sẽ:
  - **Xóa @mention** (ví dụ: `@x`, `@threads`) khỏi nội dung cuối cùng.
  - **Lọc hashtag** (nếu có) để tránh trùng lặp.
  - **Trả về dữ liệu sạch** cho các node tiếp theo.

##### **D. Thiết Lập Token Threads (Bước Một Lần)**
- Node **"Get Threads Long-Lived Token"** cần **run manual 1 lần** để lấy token mới (hiệu lực **60 ngày**).
- **Hướng dẫn chi tiết:** [Video này](https://www.youtube.com/watch?v=nC1-KZabm6U).

#### **3. Kích Hoạt ⚡️**
- **Test Run:** Gửi tin nhắn mẫu với `@all` để kiểm tra tất cả nền tảng.
- **Bật Active:** Sau khi kiểm tra thành công, **bật workflow** để hoạt động tự động.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Thêm Slack/Telegram Notifications:**
   - Sử dụng **node Slack** hoặc **Telegram** để gửi thông báo khi bài viết đăng thành công.
   - Ví dụ: `"Bài viết đã đăng trên X, Threads và LinkedIn! ID: [ID]"`.
2. **Lưu Log Tất Cả Các Lần Đăng:**
   - Thêm **node StickyNote** hoặc **Google Sheets** để ghi lại lịch sử đăng bài.
   - Dễ dàng **theo dõi hiệu suất** và **tái sử dụng nội dung**.
3. **Tự Động Chỉnh Sửa Nội Dung:**
   - Sử dụng **node Code** để thêm **link, hình ảnh, hoặc hashtag** tự động.
   - Ví dụ: Thêm `#Marketing` vào tất cả bài viết.
4. **Chuyển Động Từ Nhiều Nguồn:**
   - Kết nối với **Facebook, Instagram, TikTok** bằng cách thêm **node HTTP Request** tương ứng.

---
### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào **strategy** thay vì **chuyển động thủ công**. Với **chỉ 1 tin nhắn Telegram**, nội dung của bạn sẽ **đăng trên 3 nền tảng lớn** trong giây lát, giúp **tăng tầm tiếp cận** và **tối ưu hóa hiệu suất**.

**Hãy thử ngay!**
1. **Import workflow** từ [n8n.io/workflows/13013](https://n8n.io/workflows/13013).
2. **Cấu hình credentials** theo hướng dẫn.
3. **Gửi tin nhắn `@all`** và xem kết quả!

**Nếu có vấn đề, hãy comment bên dưới hoặc liên hệ tôi qua Telegram!** 🚀

---
**🔥 BẮT ĐẦU TỰ ĐỘNG HÓA NGAY HÔM NAY!** 🔥