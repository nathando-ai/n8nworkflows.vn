---
title: "🚀 Tự Động Chuyển YouTube Video Sang Shorts & Đăng Trên Tất Cả Mạng Xã Hội - Không Cần Code!"
description: "Workflow này tự động chuyển video YouTube thành Shorts bằng Klap, lên lịch đăng trên Instagram, TikTok, Facebook, Twitter, LinkedIn và nhiều nền tảng khác - tiết kiệm thời gian lên đến 80% cho các sếp Content Creator!"
slug: "tuy-dong-chuyen-youtube-sang-shorts-va-dang-tren-tat-ca-mang-xa-hoi"
tags: [n8n, automation, content-creation, multimodal-ai, klap, social-media, youtube-shorts]
keywords: [n8n workflow youtube shorts, tự động hóa content, đăng video trên nhiều mạng xã hội, klap automation, lịch đăng tự động]
---

# 🚀 **Tự Động Chuyển YouTube Video Sang Shorts & Đăng Trên Tất Cả Mạng Xã Hội - Không Cần Code!**

### **💥 Nỗi Đau Của Các Sếp Content Creator**
Các sếp Content Creator thường phải mất **giờ đồng hồ** để:
- **Chuyển video YouTube thành Shorts** (thời gian, chất lượng, clip phù hợp).
- **Tối ưu lịch đăng** trên Instagram, TikTok, Facebook, Twitter, LinkedIn... (tránh trùng lặp, tối ưu engagement).
- **Quản lý nhiều nền tảng** đồng thời (mất thời gian chuyển đổi giữa các app).

**Workflow này giải quyết tất cả!** Với **32 node tự động hóa**, các sếp chỉ cần **gửi URL YouTube qua Telegram**, hệ thống sẽ:
✅ **Tự động chuyển video thành Shorts** (bằng Klap).
✅ **Lên lịch đăng** trên **10+ nền tảng** (Instagram, TikTok, Facebook, Twitter, LinkedIn, Bluesky, Pinterest...).
✅ **Tối ưu thời gian đăng** dựa trên lịch từ Google Sheets.
✅ **Gửi báo cáo** về Telegram khi hoàn thành.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** so với làm thủ công.
- **Chất lượng Shorts đồng nhất** (bằng AI Klap).
- **Lịch đăng tự động** trên tất cả mạng xã hội.
- **Không lo quên đăng** (hệ thống tự kiểm tra và đăng).
- **Báo cáo chi tiết** qua Telegram (biết được tiến độ).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Các sếp cần chuẩn bị:
1. **Tài khoản Klap** (dùng để chuyển video thành Shorts).
   - [Đăng ký Klap](https://klap.ai/) (mã giảm giá: **N8N20** - giảm 20% phí đầu tiên).
2. **Tài khoản Telegram** (để nhận URL YouTube và báo cáo).
3. **Google Sheets OAuth2 API** (để lưu lịch đăng và log hoạt động).
   - [Cài đặt OAuth2](https://developers.google.com/sheets/api/quickstart/python) (sử dụng Python hoặc Node.js).
4. **Tài khoản Blotato** (để upload video trước khi đăng).
   - [Đăng ký Blotato](https://blotato.com/) (mã giảm giá: **N8N10** - giảm 10% phí).
5. **API Keys cho các nền tảng xã hội** (nếu cần):
   - Instagram, TikTok, Facebook, Twitter, LinkedIn (một số nền tảng yêu cầu OAuth).
6. **VPS n8n Self-hosted** (để workflow chạy 24/7).
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow:
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/5608) và import vào **n8n Editor**.
- **Copy JSON** từ link trên và **paste** vào **Create New Workflow** trong n8n.

:::note[LƯU Ý]
- **Không chỉnh sửa cấu trúc** của workflow (sẽ làm hỏng logic).
- **Sử dụng phiên bản n8n mới nhất** (n8n 1.x hoặc 2.x).
:::

---

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này **phức tạp** vì liên quan đến **10+ nền tảng xã hội**, nên các sếp **phải cấu hình cẩn thận** các node sau:

##### **🔹 Node 1: Trigger (Nhận YouTube URL qua Telegram)**
- **Cấu hình Telegram Trigger**:
  - Đăng nhập tài khoản Telegram với **API Key** (mã `API_ID` và `API_HASH`).
  - Chọn **chatbot** hoặc **group** để nhận URL.
  - **Lưu ý**: Dùng **/start** để test trigger.

##### **🔹 Node 2: Extract YouTube URL & Số Clip Shorts**
- **Node Code** này **trích xuất URL** và **tính số clip Shorts** từ video.
- **Không cần chỉnh sửa** (n8n tự động xử lý).

##### **🔹 Node 3-12: Chuyển Video Sang Shorts (Klap)**
- **Cấu hình API Klap**:
  - Đăng nhập tài khoản Klap và lấy **API Key** từ **Settings > API**.
  - Điền vào **Headers** của node `Send Video to Klap for Shorts Generation`:
    ```json
    {
      "Authorization": "Bearer YOUR_KLAP_API_KEY"
    }
    ```
- **Node "Check Shorts Generation Status"** sẽ **kiểm tra tiến độ** mỗi 30 giây (có thể điều chỉnh thời gian chờ).

##### **🔹 Node 13-16: Lấy Clip Shorts & URL Cuối Cùng**
- **Node "Export HD Short from Klap"** sẽ **tải video Shorts** về.
- **Node "Fetch Final Shorts URLs"** sẽ **lấy link** để đăng trên mạng xã hội.

##### **🔹 Node 17-25: Lên Lịch Đăng (Google Sheets)**
- **Cấu hình Google Sheets**:
  - Tạo **1 bảng Google Sheets** với **2 sheet**:
    1. **`Schedule`** (để lưu lịch đăng: `PostsPerDay`, `HoursBetweenPosts`).
    2. **`Logs`** (để lưu log hoạt động).
  - **Chia sẻ bảng** với **n8n** và lấy **OAuth2 API Key**.
  - **Node "Load Publishing Schedule"** sẽ **đọc lịch đăng** từ sheet `Schedule`.
  - **Node "Log Shorts & Schedule Info"** sẽ **ghi log** vào sheet `Logs`.

##### **🔹 Node 26-32: Đăng Trên Mạng Xã Hội (Blotato)**
- **Cấu hình Blotato**:
  - Đăng nhập tài khoản Blotato và lấy **API Key**.
  - **Node "Upload Video to Blotato"** sẽ **upload video** trước khi đăng.
  - **Các node `INSTAGRAM`, `TIKTOK`, `FACEBOOK`, `TWITTER`, `LINKEDIN`...** sẽ **gửi video** đến từng nền tảng.
  - **Lưu ý**:
    - Một số nền tảng (như Instagram) **yêu cầu OAuth2**.
    - **Blotato** hỗ trợ **upload tự động** cho hầu hết nền tảng.

---

#### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run** với **1 video mẫu** để kiểm tra:
   - Klap có chuyển thành Shorts không?
   - Lịch đăng có đúng không?
   - Đăng trên mạng xã hội thành công không?
2. **Bật Active** khi mọi thứ hoạt động ổn.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Kết hợp với Telegram Bot** để **nhận phản hồi** từ người dùng.
2. **Lưu log hoạt động** vào **Google Drive** thay vì Google Sheets.
3. **Gửi báo cáo hàng tuần** về **email** (sử dụng node `n8n-nodes-base.email`).
4. **Tối ưu thời gian chờ** (nếu Klap chậm, tăng thời gian chờ trong node `Wait`).
5. **Sử dụng AI ChatGPT** để **tạo caption tự động** cho Shorts (nếu cần).
6. **Tích hợp với Notion** để **lưu danh sách video** đã đăng.
:::

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp Content Creator, **tự động hóa toàn bộ quy trình** từ YouTube đến Shorts và đăng trên **tất cả mạng xã hội** một cách **chính xác và hiệu quả**.

**🚀 Hành động ngay!**
1. **Chuẩn bị tài khoản** (Klap, Telegram, Google Sheets, Blotato).
2. **Import workflow** và **cấu hình API**.
3. **Test với 1 video** và **bật Active**.

**Nếu gặp vấn đề**, các sếp có thể liên hệ với **Dr. Firas** (tác giả workflow) qua [website](https://www.drfiras.com/) để hỗ trợ!

---
**🎁 Bonus**: Các sếp có thể **tăng cường workflow** bằng cách thêm **node AI** (như **n8n-nodes-ai.llm**) để **tự động tạo caption** hoặc **chỉnh sửa video** bằng AI.