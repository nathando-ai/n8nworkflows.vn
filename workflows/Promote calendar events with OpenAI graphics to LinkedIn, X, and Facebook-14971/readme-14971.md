---
title: "🚀 Tự Động Hoá Quảng Báo Sự Kiện Trên LinkedIn, Twitter/X & Facebook Với Hình Ảnh AI – Không Cần Code!"
description: "Workflow này tự động tạo hình ảnh quảng bá sự kiện từ Google Calendar, lên lịch đăng 3 lần trên LinkedIn, Twitter/X và Facebook với caption động dựa trên thời gian, và gửi báo cáo chi tiết qua Telegram. Tiết kiệm 10+ giờ công/tháng cho các sếp marketing!"
slug: "tieu-dong-hoa-quang-bo-su-kien-voi-ai"
tags: [n8n, automation, social-media, ai-multimodal, google-calendar, openai, linkedin, twitter, facebook]
keywords: [n8n workflow tự động hóa quảng bá sự kiện, tạo hình ảnh AI cho sự kiện, lên lịch đăng trên LinkedIn Twitter Facebook, tự động hóa marketing không code, OpenAI chatbot cho caption động]
---

# 🚀 **Tự Động Hoá Quảng Báo Sự Kiện Trên 3 Mạng Xã Hội Với Hình Ảnh AI – Không Cần Code!**

### **Nỗi Đau Của Các Sếp Marketing**
Các sếp thường phải:
✅ **Tạo hình ảnh quảng bá** cho mỗi sự kiện thủ công (thời gian, công sức, chi phí design).
✅ **Lên lịch đăng** trên LinkedIn, Twitter/X và Facebook với caption khác nhau (48h trước, 24h trước, 1h trước).
✅ **Theo dõi và báo cáo** hiệu quả của mỗi bài đăng (Google Sheets + Telegram).
✅ **Lo lắng về thời gian thực** – nếu quên lên lịch, sự kiện đã qua mà chưa quảng bá.

**Workflow này giải quyết tất cả!** Với **AI + Tự Động Hoá**, các sếp chỉ cần **thêm sự kiện vào Google Calendar**, workflow sẽ:
✔ **Tự động tạo hình ảnh quảng bá** với logo, tên sự kiện và ngày giờ.
✔ **Lên lịch đăng 3 lần** trên 3 nền tảng xã hội với caption động (ví dụ: *"Sự kiện này diễn ra vào ngày mai!"*).
✔ **Gửi báo cáo chi tiết** qua Telegram và lưu log vào Google Sheets.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ công/tháng** (không cần thiết kế hình ảnh thủ công).
- **Chuẩn xác 100%** – không quên lên lịch, không sai thời gian.
- **Cá nhân hóa caption** dựa trên thời gian (48h trước, 24h trước, 1h trước).
- **Báo cáo tự động** qua Telegram và Google Sheets (dễ theo dõi hiệu quả).
- **Hoạt động liên tục** – không cần can thiệp thủ công.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Google Calendar OAuth2** (để theo dõi sự kiện).
2. **Mẫu hình ảnh banner** (public URL) để chèn thông tin sự kiện.
3. **UploadToURL** (để lưu hình ảnh tự động tạo).
4. **LinkedIn OAuth2** (đăng bài tự động).
5. **Twitter/X OAuth1** (đăng tweet tự động).
6. **Facebook Graph API** (đăng bài trên Facebook).
7. **Google Sheets** (tên sheet: `EventPostLog`, cột: `EventID, EventName, Platform, ScheduledTime, PostedAt, Status, ImageURL`).
8. **Telegram Bot Token** + **Chat ID** của admin.
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/14971](https://n8n.io/workflows/14971) và import vào n8n Editor.
- **Cách 2:** Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/14971) và paste vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **18 node**, các sếp cần chú ý cấu hình sau:

##### **📅 Google Calendar Trigger**
- **Chọn Calendar** cần theo dõi (ví dụ: "Sự kiện Marketing").
- **Enable "Watch Calendar"** để workflow phát hiện sự kiện mới ngay lập tức.

##### **🖼️ Edit Image Node (Tạo Hình Ảnh)**
- **Điền URL mẫu hình ảnh** (ví dụ: `https://example.com/banner-template.jpg`).
- **Cấu hình text overlay** (tên sự kiện, ngày giờ, địa điểm) trong **Composite Operation**.

##### **⏰ DateTime Node (Lên Lịch Đăng)**
- **Cấu hình 3 thời điểm đăng**:
  - 48h trước sự kiện.
  - 24h trước sự kiện.
  - 1h trước sự kiện.

##### **🤖 OpenAI Node (Tạo Caption Động)**
- **Điền API Key OpenAI** và **Prompt mẫu** (ví dụ: *"Tạo caption động cho sự kiện [NAME] diễn ra vào [TIME]"*).
- **Chọn model** (ví dụ: `gpt-4`).

##### **📊 Google Sheets (Lưu Log)**
- **Chọn sheet** `EventPostLog` và **cột cần update**.
- **Kiểm tra quyền OAuth2** để workflow có thể ghi dữ liệu.

##### **📱 Telegram Notification**
- **Điền Bot Token** và **Chat ID** của admin.
- **Cấu hình template thông báo** (ví dụ: *"Sự kiện [NAME] đã được quảng bá trên 3 nền tảng!"*).

#### **3. Kích Hoạt ⚡️**
- **Test Run** với một sự kiện mẫu (đảm bảo tất cả node hoạt động).
- **Bật Active** workflow sau khi kiểm tra xong.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack** để thông báo khi có sự kiện mới.
2. **Lưu log vào Airtable** thay vì Google Sheets (dễ dàng hơn trong quản lý).
3. **Sử dụng AI để phân tích hiệu quả** (ví dụ: OpenAI phân tích engagement từ dữ liệu Google Sheets).
4. **Tự động gửi email báo cáo** cho team marketing hàng tuần.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp marketing, **tăng hiệu quả quảng bá sự kiện** và **giảm thiểu sai sót**. **Chỉ cần thêm sự kiện vào Google Calendar**, workflow sẽ tự động:
✅ **Tạo hình ảnh quảng bá**.
✅ **Lên lịch đăng trên 3 nền tảng**.
✅ **Gửi báo cáo tự động**.

**Hãy áp dụng ngay và tiết kiệm 10+ giờ công/tháng!** 🚀

---
**🔗 [Tải workflow nguyên bản](https://n8n.io/workflows/14971)**
**💬 Có thắc mắc? Hỏi ngay trong nhóm Telegram n8n Việt Nam!** 👉 [n8n.vn/community](https://t.me/n8nvietnam)