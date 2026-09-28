---
title: "🎵 Tự Động Hoàn Thành Gói Âm & Dàn Văn Bản TikTok Cho Video AI Sản Phẩm Với Wouldliker (N8N)"
description: "Workflow này tự động chuyển đổi mô tả sản phẩm/clip ngắn thành gói âm nhạc TikTok + dàn văn bản hoàn chỉnh, giúp các sếp tiết kiệm 80% thời gian soạn thảo nội dung AI. Kết quả: Âm nhạc phù hợp, caption hấp dẫn, hashtag tối ưu - tất cả chỉ với 1 cú nhấp chuột."
slug: "tieu-dong-hoan-thanh-goi-am-tiktok-voi-wouldliker"
tags: [n8n, automation, content-creation, multimodal-ai, tiktok-marketing]
keywords: [n8n workflow tiktok, tự động hóa content ai, gói âm nhạc tiktok tự động, caption tiktok tự động, wouldliker api n8n]
---

# 🚀 **Tự Động Hoàn Thành Gói Âm & Dàn Văn Bản TikTok Cho Video AI Sản Phẩm**

### **Nỗi Đau Của Các Sếp Trong Content AI**
Các sếp đang phải mất **giờ đồng hồ** để:
❌ Tìm kiếm âm nhạc TikTok phù hợp với sản phẩm
❌ Soạn thảo caption, hashtag, và dàn văn bản hấp dẫn
❌ Lo lắng về xu hướng âm nhạc mới nhất
❌ Phải update liên tục khi AI tạo ra video mới

**Workflow này giải quyết tất cả!** Chỉ cần **gửi mô tả sản phẩm**, n8n sẽ tự động:
🎶 **Lựa chọn âm nhạc TikTok** phù hợp với nội dung
📝 **Tạo caption, hashtag, và dàn văn bản** chuyên nghiệp
🔄 **Cập nhật liên tục** khi có âm nhạc mới phù hợp

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **24/7** và không bị gián đoạn, các sếp nên **self-host** n8n trên VPS chuyên dụng:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 [VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đảm bảo tốc độ cao)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 80% thời gian** soạn thảo content AI
✅ **Âm nhạc TikTok mới nhất** tự động cập nhật
✅ **Caption & hashtag tối ưu** tăng engagement
✅ **Hoạt động liên tục** (không cần can thiệp thủ công)
✅ **Kết nối với CMS/Slack/Notion** để tự động xuất bản
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
- **Tài khoản Wouldliker** (miễn phí, không cần API key)
- **Mô tả sản phẩm/clip ngắn** (gửi qua Webhook)
- **Thông tin bổ sung** (platform, content_type, language, is_aigc)
- **Kết nối với công cụ xuất bản** (Slack, Notion, Airtable, Shopify...)
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Bước 1:** Tải file JSON từ [n8n.io/workflows/15829](https://n8n.io/workflows/15829)
- **Bước 2:** Vào **n8n Editor** → **Import Workflow** → Chọn file JSON
- **Bước 3:** Nhấn **Import** và chờ workflow tải xong

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này **không cần API key**, nhưng cần **cấu hình Webhook** để nhận dữ liệu:

##### **A. Webhook: "product brief in"**
- **Tên Node:** `Webhook: product brief in`
- **Cấu hình:**
  - **Path:** `wouldliker-product-video` (không thay đổi)
  - **HTTP Method:** `POST` (không thay đổi)
  - **Credentials:** Chọn **None** (không cần xác thực)

##### **B. Gửi Dữ liệu Test**
- **Bước 1:** Nhấn **Execute Workflow** (icon play) để kích hoạt Webhook
- **Bước 2:** Gửi **POST request** đến URL Webhook với payload mẫu:
  ```json
  {
    "description": "Video quảng cáo sản phẩm AI tạo hình 3D cho doanh nghiệp",
    "platform": "tiktok",
    "content_type": "product_video",
    "language": "vi",
    "is_aigc": true
  }
  ```
- **Kết quả:** Workflow sẽ trả về **gói âm nhạc + dàn văn bản** tự động.

##### **C. Kết Nối Với Công Cụ Xuất Bản**
- **Node cuối:** `Shape final output` trả về **dữ liệu flat** (JSON) như:
  ```json
  {
    "tiktok_sound_url": "https://www.tiktok.com/music/...",
    "tiktok_music_id": "123456789",
    "video_brief": "Mô tả video chi tiết...",
    "captions": ["Caption 1", "Caption 2"],
    "hashtags": ["#AIGC", "#TikTokMarketing"],
    "boundary_copy": "Lời giới thiệu đầu video..."
  }
  ```
- **Kết nối với:**
  - **Slack/Telegram:** Gửi thông báo tự động
  - **Notion/Airtable:** Lưu dữ liệu vào bảng
  - **Shopify:** Cập nhật mô tả sản phẩm
  - **CMS (WordPress, Ghost...):** Xuất bản tự động

#### **3. Kích Hoạt ⚡️**
- **Bật Active:** Đặt switch **Active** ở góc trên bên phải thành **ON**
- **Test lại:** Gửi 1-2 request test để đảm bảo workflow hoạt động ổn định

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tích Hợp với AI Video Generator**
   - Sau khi nhận **tiktok_sound_url**, các sếp có thể **gắn âm nhạc vào video AI** (Runway ML, Pika Labs...) và xuất bản tự động.

2. **Lưu Log & Báo Cáo**
   - Kết nối với **Google Sheets** hoặc **Airtable** để lưu lịch sử gợi ý âm nhạc và caption.

3. **Tự Động Xuất Bản trên TikTok**
   - Sử dụng **TikTok API** (nếu có) để **tự động upload video** với âm nhạc và caption đã chuẩn bị.

4. **Cập Nhật Thường Xuyên**
   - **Schedule Workflow** (n8n Pro) để **check âm nhạc mới** hàng ngày và cập nhật cho các video mới.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp từ việc **tìm kiếm âm nhạc + soạn thảo caption thủ công**, thay vào đó **AI và n8n làm tất cả** chỉ với **1 cú nhấp chuột**.

**Hành động ngay:**
1. **Import workflow** và test với mô tả sản phẩm của mình
2. **Kết nối với Slack/Notion** để nhận thông báo tự động
3. **Tích hợp với AI Video Generator** để xuất bản nhanh chóng

**🚀 CÓ THỂ LÀM ĐƯỢC HƠN ĐÓ!** Các sếp có thể mở rộng workflow này để **tự động hóa toàn bộ pipeline content AI** từ mô tả đến xuất bản.

---
**Chia sẻ ý kiến hoặc câu hỏi về workflow này trong [community n8n Việt Nam](https://discord.gg/n8n)!** 🚀