---
title: "🎥 Tự Động Hóa Sáng Tạo & Phát Hành Video AI Từ Telegram → VEED + Blotato (Không Cần Code)"
description: "Workflow tự động hóa hoàn chỉnh giúp các sếp tạo video AI từ Telegram, chỉnh sửa trên VEED, và phát hành đồng thời lên 9 nền tảng xã hội (TikTok, YouTube, Instagram...) chỉ với một cú nhấp chuột. Tiết kiệm thời gian 80% so với cách làm thủ công!"
slug: "tieu-dong-hoa-tao-phat-hanh-video-ai-telegram-veed-blotato"
tags: [n8n, automation, ai-video, content-creation, veed, blotato, telegram-bot, no-code]
keywords: [n8n workflow video ai, tự động hóa video marketing, tạo video ai từ telegram, veed n8n, blotato n8n, phát hành video lên 9 nền tảng]
---

# 🚀 **Tự Động Hóa Sáng Tạo & Phát Hành Video AI Từ Telegram → VEED + Blotato**

### **Giải pháp hoàn hảo cho các sếp marketing, content creator và doanh nghiệp muốn:**
- **Tạo video AI nói chuyện tự động** từ yêu cầu của khách hàng trên Telegram.
- **Chỉnh sửa và xuất bản video** trên VEED (dùng bởi 75% Fortune 500).
- **Phát hành đồng thời lên 9 nền tảng xã hội** (TikTok, YouTube, Instagram, LinkedIn...) chỉ với một cú nhấp chuột.
- **Tiết kiệm thời gian** lên đến 80% so với cách làm thủ công.

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[**LỢI ÍCH CỐT LÕI**]
✅ **Tạo video AI nhanh chóng** chỉ bằng cách chat với bot Telegram.
✅ **Chỉnh sửa và xuất bản tự động** trên VEED (không cần kỹ thuật).
✅ **Phát hành đồng thời lên 9 nền tảng** (TikTok, YouTube, Instagram, LinkedIn, Facebook, X, Threads, Bluesky, Pinterest).
✅ **Cá nhân hóa nội dung** theo yêu cầu của khách hàng.
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.
✅ **Giảm chi phí** so với việc thuê nhân viên chỉnh sửa video.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI BẮT ĐẦU**]
Để workflow này hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Telegram Bot** (đăng ký trên [@BotFather](https://t.me/BotFather)).
2. **API Key OpenAI** (để AI tạo nội dung video).
3. **Credentials VEED MCP** (OAuth2) để tạo video AI.
4. **Tài khoản Blotato** (đăng ký [tại đây](https://blotato.com) - cần gói trả phí).
5. **API Key Blotato** (cần cài đặt [n8n-nodes-blotato](https://github.com/blotato/n8n-nodes-blotato)).
6. **Các tài khoản mạng xã hội** (TikTok, YouTube, Instagram, LinkedIn, Facebook, X, Threads, Bluesky, Pinterest) để phát hành.
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/14290](https://n8n.io/workflows/14290) hoặc copy/paste JSON vào **n8n Editor**.
- **Cài đặt node Blotato** (nếu chưa có):
  ```bash
  npm install @blotato/n8n-nodes-blotato
  ```
- **Khởi động workflow** và bật chế độ **Active**.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **24 node** và hoạt động theo **các bước sau**:

#### **📌 Bước 1: Telegram Trigger (📩)**
- **Cấu hình**:
  - Chọn **Bot Token** từ Telegram Bot (đã đăng ký trên @BotFather).
  - Chọn **Chat ID** của bot (có thể lấy từ [@userinfobot](https://t.me/userinfobot)).
  - **Lưu ý**: Bot phải được **approve** để gửi tin nhắn.

#### **📌 Bước 2: AI Video Agent (🤖)**
- **Cấu hình**:
  - **Model OpenAI**: Chọn `gpt-5-nano` (hoặc model khác nếu muốn).
  - **Credentials OpenAI**: Điền **API Key** từ tài khoản OpenAI.
  - **Memory Buffer**: Bật để lưu lịch sử chat (tối đa 5 tin nhắn trước).

#### **📌 Bước 3: VEED MCP Tools (🎬)**
- **Cấu hình**:
  - **Credentials VEED**: Điền **Client ID** và **Client Secret** từ VEED MCP.
  - **Tools sử dụng**:
    - `list_characters` (lấy danh sách nhân vật AI).
    - `list_voices` (lấy danh sách giọng nói).
    - `confirm_fabric_video` (xác nhận trước khi tạo video).
    - `create_fabric_video` (tạo video AI).
    - `get_generation_status` (kiểm tra tiến độ tạo video).

#### **📌 Bước 4: Xác nhận & Phát hành (✅)**
- **Nếu video được tạo thành công**:
  - Bot sẽ gửi **URL video** và hỏi **"Publish to social media?"**.
  - Nếu **Approve**, video sẽ được **upload lên Blotato** và **phát hành lên 9 nền tảng**.
  - Nếu **Reject**, video sẽ **bị bỏ qua** và bot sẽ thông báo.

#### **📌 Bước 5: Blotato Setup (📤)**
- **Cấu hình API Key Blotato**:
  - Đăng ký [tại đây](https://blotato.com) và lấy **API Key** từ **Settings > API**.
  - **Cài đặt node Blotato** trong n8n:
    ```bash
    npm install @blotato/n8n-nodes-blotato
    ```
- **Cấu hình các nền tảng**:
  - Mỗi nền tảng (TikTok, YouTube, Instagram...) cần **accountId** (lấy từ Blotato Dashboard).
  - **Cấu hình thêm**:
    - **YouTube**: Điền **title** và **privacy** (public/private).
    - **Facebook**: Điền **Page ID**.
    - **Pinterest**: Điền **Board ID**.

---
### **3. Kích hoạt ⚡️**
- **Test run** với một tin nhắn mẫu:
  ```
  "Tạo một video AI giới thiệu sản phẩm của công ty tôi, nhân vật là một người đàn ông trẻ, giọng nói tiếng Việt."
  ```
- **Bật Active workflow** và bắt đầu sử dụng!

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::tip[**CÁCH LÀM NÂNG CAO**]
1. **Tự động gửi báo cáo** sau khi phát hành video lên Telegram/Email.
2. **Kết hợp với Slack/Telegram** để thông báo khi video sẵn sàng.
3. **Lưu log hoạt động** để theo dõi hiệu suất.
4. **Tùy chỉnh caption** bằng cách chỉnh sửa node **Set Caption**.
5. **Bật/dừng tự động** phát hành lên các nền tảng không cần thiết (ví dụ: Pinterest nếu không dùng).
:::

---
## 📌 **Kết luận**
Workflow này **giải phóng thời gian** của các sếp để tập trung vào chiến lược marketing thay vì làm thủ công. **Chỉ cần chat với bot Telegram**, AI sẽ tự động tạo video, chỉnh sửa trên VEED, và phát hành lên **9 nền tảng xã hội** chỉ trong vài giây!

**👉 Bắt đầu ngay bằng cách import workflow và cấu hình theo hướng dẫn trên!**

---
:::info[**Gợi ý hạ tầng cho n8n**]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**🚀 Hãy tự động hóa công việc sáng tạo video của mình ngay hôm nay!** 🚀