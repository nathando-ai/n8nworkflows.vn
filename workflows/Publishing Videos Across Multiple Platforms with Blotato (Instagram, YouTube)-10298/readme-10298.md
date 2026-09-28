---
title: "🚀 Tự Động Hóa Đăng Video Trên 9 Mạng Xã Hội (Instagram, YouTube, TikTok...) Với Blotato - Không Cần Code!"
description: "Workflow tự động hóa đăng video lên Instagram, YouTube, TikTok, Facebook, LinkedIn, Threads, Twitter, Bluesky và Pinterest chỉ trong 1 lần thiết lập. Tiết kiệm thời gian lên đến 80% cho các sếp marketing, giảm thiểu lỗi nhân sự và tối ưu hóa nội dung trên tất cả các nền tảng."
slug: "tu-dong-hoa-dang-video-blotato"
tags: [n8n, automation, social-media, blotato, google-sheets, self-hosted]
keywords: [n8n workflow video, tự động hóa mạng xã hội, đăng video nhiều nền tảng, blotato api, google sheets tự động hóa]
---

# 🚀 **Tự Động Hóa Đăng Video Trên 9 Mạng Xã Hội Với Blotato - Giải Pháp Marketing 24/7**

### **Nỗi Đau Của Các Sếp Marketing**
Các sếp thường phải mất **giờ đồng hồ** để:
- Chia sẻ video lên **Instagram, YouTube, TikTok, Facebook, LinkedIn, Threads, Twitter, Bluesky và Pinterest** một cách thủ công.
- Lo lắng về **sai sót trong mô tả, thời gian đăng không đồng bộ** giữa các nền tảng.
- **Không thể đăng video tự động** khi đang ngủ hoặc làm việc khác.
- **Không có cách nào để theo dõi trạng thái đã đăng hay chưa** trên Google Sheets.

**Workflow này giải quyết tất cả!** Với **n8n + Blotato**, các sếp chỉ cần **cài đặt 1 lần**, sau đó video sẽ tự động đăng lên **9 nền tảng** theo lịch trình, đồng thời cập nhật trạng thái trên Google Sheets.

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian lên đến 80%** so với cách đăng thủ công.
✅ **Đăng video đồng thời trên 9 nền tảng** chỉ với 1 lần upload.
✅ **Cập nhật tự động trạng thái** trên Google Sheets (đã đăng hay chưa).
✅ **Lịch trình tự động** (đăng video vào giờ vàng theo yêu cầu).
✅ **Không cần code**, chỉ cần **cấu hình 1 lần** là hoạt động 24/7.
✅ **Giảm thiểu lỗi nhân sự** (không còn quên đăng video hoặc sai mô tả).
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản Blotato** (đăng ký tại [blotato.com](https://my.blotato.com/))
✔ **API Key của Blotato** (lấy từ **Settings > API**)
✔ **Google Sheets** với 2 cột:
   - **URL VIDEO** (đường dẫn video từ Blotato)
   - **ReadyToPost** (ghi "Ready" nếu video sẵn sàng đăng)
✔ **Tài khoản các nền tảng xã hội** (Instagram, YouTube, TikTok, Facebook, LinkedIn, Threads, Twitter, Bluesky, Pinterest) và **ID của từng tài khoản** (lấy từ Blotato Settings).
✔ **VPS Self-hosted n8n** (để workflow chạy 24/7).
:::

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể **download file JSON** từ [n8n.io/workflows/10298](https://n8n.io/workflows/10298) và import vào **n8n Editor** hoặc **copy/paste JSON** từ file vào.

:::note[LƯU Ý]
- **Không sử dụng phiên bản n8n Cloud** (do cần tự động hóa 24/7, nên **self-hosted** là lựa chọn tối ưu).
- **Không quên bật "Active"** sau khi import.
:::

#### **2. Các Bước Cấu Hình BẮT BUỘC**
##### **A. Thiết Lập Blotato API Key**
- **Cách 1 (Khuyến nghị):** Sử dụng **Data Table** để quản lý API Key (để dễ thay đổi sau này).
  - Tạo **Data Table** mới với 2 cột:
    - **Service** (ghi "Blotato")
    - **Token** (ghi API Key từ Blotato)
  - Tham chiếu API Key trong tất cả các node **HTTP Request** bằng cú pháp:
    ```json
    {{ $('get blotato key').item.json.token }}
    ```
- **Cách 2 (Nếu không dùng Data Table):**
  - Điền **API Key** vào tất cả các node **HTTP Request** (nhưng **không khuyến nghị** vì khó quản lý).

##### **B. Cấu Hình Google Sheets**
- Tạo **Google Sheet** mới với 2 cột:
  - **URL VIDEO** (đường dẫn video từ Blotato)
  - **ReadyToPost** (ghi "Ready" nếu video sẵn sàng đăng)
- **Cấu hình node "Get my video"** (Google Sheets):
  - Chọn **Google Sheets OAuth2 API** (đã cấu hình trước).
  - Chọn **Sheet Name** và **Range** (ví dụ: `Sheet1!A:B`).

##### **C. Thêm ID Tài Khoản Blotato**
- Trong node **"Assign Social Media IDs"**, thay thế **ID của các sếp** bằng ID từ **Blotato Settings** (mỗi nền tảng có 1 ID riêng).
- Ví dụ:
  ```json
  {
    "INSTAGRAM": "123456789",
    "YOUTUBE": "987654321",
    "TIKTOK": "555555555",
    ...
  }
  ```

##### **D. Cấu Hình Lịch Trình (Schedule Trigger)**
- Đặt **thời gian chạy** (ví dụ: **8h sáng hàng ngày**).
- **Lưu ý:** Nếu muốn **đăng video ngay khi có mới**, thay thế **Schedule Trigger** bằng **Webhook** hoặc **Form Trigger**.

##### **E. Kích Hoạt Sub-Workflow (Nếu Sử Dụng)**
- Nếu muốn **đăng video từ ngoài workflow chính**, cần **cấu hình sub-workflow** `"[SUB] Video to Social"`:
  - Thay thế **Blotato Key** bằng Data Table (nếu đã cấu hình).
  - **Test sub-workflow** bằng cách gọi từ **Test Workflow** (có sẵn trong file).

---
#### **3. Kích Hoạt ⚡️**
- **Run Test** với 1 video mẫu để kiểm tra.
- **Bật "Active"** để workflow chạy tự động.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[CÁC Ý TƯỞNG MỞ RỘNG]
🔹 **Gửi thông báo Slack/Telegram khi đăng thành công:**
   - Thêm node **Slack/Telegram** sau node **"Social Posts Completed"** để thông báo kết quả.

🔹 **Lưu log hoạt động:**
   - Sử dụng **Google Sheets** hoặc **Airtable** để ghi lại lịch sử đăng video.

🔹 **Tự động tạo mô tả bằng AI:**
   - Kết hợp với **LLM (n8n-node-ai)** để tự động sinh mô tả video.

🔹 **Đăng video theo ngày tháng (ví dụ: ngày sinh nhật khách hàng):**
   - Sử dụng **Schedule Trigger** kết hợp với **Google Calendar API** để đăng video vào ngày đặc biệt.

🔹 **Tự động chia sẻ video cho nhóm nội bộ:**
   - Thêm node **WhatsApp/Telegram** để thông báo cho team khi video được đăng.
:::

---
### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp marketing, giúp **đăng video tự động trên 9 nền tảng** chỉ với **1 lần cài đặt**. Không cần code, không cần lo lắng về **sai sót hoặc quên đăng**, và **tối ưu hóa nội dung** trên tất cả các kênh.

**Hãy áp dụng ngay và tiết kiệm thời gian cho công việc quan trọng hơn!** 🚀

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**Bạn có thắc mắc gì?** Hãy để lại comment bên dưới, các sếp sẽ hỗ trợ miễn phí! 😊