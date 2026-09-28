---
title: "🎬 Tự Động Hóa Sáng Tạo Video AI Viral Từ Telegram Đến Blotato (NanoBanana + VEO3.1)"
description: "Workflow này tự động chuyển đổi ý tưởng video từ tin nhắn Telegram thành video AI viral 8 giây chuẩn 9:16, sau đó tự động đăng tải lên 6 nền tảng xã hội (YouTube, TikTok, LinkedIn, Facebook, Instagram, Twitter) chỉ trong vài giây. Giúp các sếp tiết kiệm thời gian lên tới 80% trong việc tạo nội dung video."
slug: "tieu-dong-hoa-tao-tai-video-ai-viral-telegram-blotato"
tags: [n8n, automation, content-creation, ai-multimodal, nano-banana, veo3-1, blotato, telegram-bot, no-code]
keywords: [n8n workflow video ai, tự động hóa tạo video viral, nano banana 2 pro, veo ai video generator, blotato api, tự động đăng video lên tiktok youtube]
---

# 🚀 **Tự Động Hóa Sáng Tạo Video AI Viral Từ Telegram Đến Blotato (NanoBanana + VEO3.1)**

### **Giải Phóng Tay Sếp Từ Công Việc Tạo Video AI Mệt Mỏi**
Hiện nay, việc tạo nội dung video AI viral để thu hút người dùng trên mạng xã hội là một trong những thách thức lớn nhất của các marketer và content creator. Thường thì, quá trình này bao gồm nhiều bước phức tạp:
- **Tìm ý tưởng** và viết kịch bản.
- **Tạo hình ảnh tham khảo** hoặc chọn hình ảnh từ bên ngoài.
- **Chỉnh sửa và tối ưu hóa** prompt cho AI tạo video.
- **Tải video lên** nhiều nền tảng khác nhau (TikTok, YouTube, Instagram...) một cách thủ công.
- **Đợi và kiểm tra** kết quả trước khi đăng tải.

Với **workflow này**, các sếp chỉ cần **gửi một tin nhắn Telegram** với ý tưởng và hình ảnh tham khảo, hệ thống sẽ tự động:
✅ **Tạo hình ảnh** bằng NanoBanana 2 PRO.
✅ **Tạo video AI viral** 8 giây chuẩn 9:16 bằng VEO3.1.
✅ **Tự động đăng tải** lên **6 nền tảng xã hội** (YouTube, TikTok, LinkedIn, Facebook, Instagram, Twitter) thông qua Blotato.
✅ **Gửi kết quả** về Telegram cho các sếp review.

---

## 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian lên tới 80%** so với phương pháp thủ công.
- **Chất lượng video cao** do AI tối ưu hóa prompt và tạo nội dung theo yêu cầu.
- **Tự động hóa hoàn toàn** – không cần can thiệp của con người.
- **Đăng tải đa nền tảng** một lần, tiết kiệm công sức quản lý.
- **Cá nhân hóa nội dung** dựa trên ý tưởng từ Telegram.
- **Hoạt động 24/7** – không giới hạn số lượng video tạo.
:::

---

## 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Telegram** (để nhận và gửi tin nhắn tự động).
2. **API Key Telegram Bot** (tạo bot trên [@BotFather](https://t.me/BotFather)).
3. **Tài khoản Blotato Pro** ([Đăng ký Blotato](https://blotato.com/?ref=firas)) và **API Key** (tìm ở `Settings > API > Generate API Key`).
4. **NanoBanana 2 PRO** ([Tải tại đây](https://nanobanana.ai/)) và **API Key** (nếu cần).
5. **VEO3.1** ([Tải tại đây](https://veo.ai/)) và **API Key** (nếu cần).
6. **n8n Self-hosted** (không dùng phiên bản miễn phí trên cloud).
7. **Node Blotato** (phải **bật "Verified Community Nodes"** trong cài đặt admin n8n).
8. **Node LangChain** (để sử dụng AI Agent và OpenAI).
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/11204).
- Mở **n8n Editor** → Nhấn **Import** → Chọn file JSON → **Load**.

:::note[LƯU Ý]
- **Không dùng phiên bản n8n cloud** (do yêu cầu API Key và node Blotato).
- **Cài đặt n8n trên VPS** để workflow hoạt động 24/7.
:::

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**

#### **A. Cấu Hình Telegram Trigger**
- **Node:** `Telegram Trigger: Receive Video Idea`
- **Cần thiết:**
  - **Credentials:** `telegramApi` (điền `token` từ bot Telegram).
  - **Webhook URL:** Cấu hình trong Telegram Bot (đường dẫn n8n + `/telegramTrigger/your-bot-token`).

#### **B. Cấu Hình OpenAI (NanoBanana & VEO3.1)**
- **Node:** `OpenAI Chat Model`, `LLM: OpenAI Chat`, `OpenAI Vision: Analyze Reference Image`
- **Cần thiết:**
  - **Credentials:** `openAiApi` (điền `apiKey` từ tài khoản OpenAI).
  - **Model:** `gpt-4.1-mini` (đã cấu hình sẵn).

#### **C. Cấu Hình NanoBanana 2 PRO**
- **Node:** `NanoBanana: Create Image`
- **Cần thiết:**
  - **URL API:** `https://api.nanobanana.ai/v1/generate` (hoặc URL riêng nếu dùng phiên bản Pro).
  - **Headers:** Điền `Authorization: Bearer YOUR_API_KEY`.

#### **D. Cấu Hình VEO3.1**
- **Node:** `Veo Generation`
- **Cần thiết:**
  - **URL API:** `https://api.veo.ai/v1/generate` (hoặc URL riêng).
  - **Headers:** Điền `Authorization: Bearer YOUR_API_KEY`.

#### **E. Cấu Hình Blotato**
- **Node:** `Upload Video to BLOTATO` và các node `Youtube`, `Tiktok`, `Linkedin`, `Facebook`, `Instagram`, `Twitter (X)`
- **Cần thiết:**
  - **Credentials:** `blotatoApi` (điền `apiKey` từ Blotato).
  - **Resource:** `media` (đã cấu hình sẵn).

#### **F. Cấu Hình AI Agent & Structured Output Parser**
- **Node:** `AI Agent: Generate Video Script`, `Structured Output Parser`
- **Cần thiết:**
  - **Master Prompt:** Điền vào `Set Master Prompt` (có thể tùy chỉnh để phù hợp với nội dung của các sếp).
  - **ToolThink:** Đảm bảo node `toolThink` hoạt động để AI suy nghĩ logic.

---

### **3. Kích Hoạt ⚡️**
- **Test Run:** Chọn **Run Workflow** và gửi tin nhắn Telegram với **ý tưởng video + hình ảnh tham khảo**.
- **Bật Active:** Sau khi kiểm tra thành công, chuyển trạng thái workflow sang **Active**.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[TIẾP CẬN HƠN]
1. **Tùy Chỉnh Master Prompt** để AI tạo video phù hợp với phong cách của các sếp.
2. **Lưu Log** bằng node `stickyNote` để theo dõi quá trình tạo video.
3. **Gửi Báo Cáo Định Kỳ** (ví dụ: hàng tuần) về số lượng video tạo và lượt view.
4. **Kết Hợp Slack** thay vì Telegram để quản lý công việc nhóm.
5. **Tối Ưu Hình Ảnh Tham Khảo** bằng cách sử dụng **DALL·E 3** hoặc **MidJourney** trước khi gửi cho NanoBanana.
6. **Sử Dụng VEO Pro** để tạo video dài hơn (trên 8 giây).
:::

---

## 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn **tự động hóa toàn bộ quá trình tạo và đăng tải video AI viral** mà không cần kiến thức code. Với chỉ **một tin nhắn Telegram**, hệ thống sẽ tự động:
✔ **Tạo hình ảnh** bằng NanoBanana.
✔ **Tạo video** bằng VEO3.1.
✔ **Đăng tải lên 6 nền tảng** thông qua Blotato.
✔ **Gửi kết quả** về Telegram.

**Hành động ngay!**
- **Cài đặt n8n trên VPS** (để workflow hoạt động 24/7).
- **Import workflow** và cấu hình theo hướng dẫn.
- **Gửi tin nhắn Telegram** và xem AI làm việc!

👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)**.

---
**Chúc các sếp thành công với việc tự động hóa sáng tạo nội dung video AI!** 🚀