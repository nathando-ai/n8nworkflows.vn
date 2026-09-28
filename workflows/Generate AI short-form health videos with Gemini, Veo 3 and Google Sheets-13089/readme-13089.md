---
title: "🎥 Tự Động Hóa Sáng Tạo Video Health AI Viral với Gemini, Veo 3 & Google Sheets (N8n)"
description: "Workflow tự động hóa hoàn toàn từ việc thu thập ý tưởng viral health đến tạo video AI ngắn, xuất bản tự động trên Facebook - tiết kiệm 100h/năm cho các sếp Content Creator."
slug: "tieu-dong-hoa-tao-video-health-ai-veo3-gemini"
tags: [n8n, automation, content-creation, ai-video, google-sheets, veo3, gemini-ai, facebook-automation]
keywords: [n8n workflow video ai, tự động hóa video health, gemini api n8n, veo3 api tự động, tạo video viral tự động, google sheets + ai video]
---

# 🚀 **Tự Động Hóa Sáng Tạo Video Health AI Viral - Từ Ý Tưởng Đến Xuất Bản Tự Động**

### **Nỗi Đau Của Các Sếp Content Creator Health**
Các sếp đang mất **100+ giờ/năm** để:
✅ **Thu thập ý tưởng viral** từ nhiều nguồn khác nhau (Reddit, TikTok, Facebook Groups).
✅ **Tạo script** phù hợp với xu hướng, nhưng thường mất nhiều thời gian và không đảm bảo chất lượng.
✅ **Chỉnh sửa video** thủ công, dẫn đến hiệu suất thấp và khó mở rộng.
✅ **Xuất bản trên nhiều nền tảng** mà không có hệ thống theo dõi hiệu quả.

**Workflow này giải quyết tất cả!** Với **AI Gemini + Veo 3 + Google Sheets**, các sếp có thể:
✔ **Tự động thu thập** ý tưởng viral từ internet.
✔ **Tạo script video** tối ưu hóa cho engagement.
✔ **Tạo video AI** trong vài phút thay vì nhiều giờ.
✔ **Xuất bản tự động** lên Facebook (hoặc Instagram) mà không cần can thiệp thủ công.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài **n8n trên VPS riêng (Self-hosted)** để tránh giới hạn của phiên bản miễn phí.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đảm bảo tốc độ cao cho AI)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100+ giờ/năm** cho việc thu thập, tạo script và chỉnh sửa video.
- **Video AI chất lượng cao** với script được tối ưu hóa bởi Gemini AI.
- **Xuất bản tự động** lên Facebook/Instagram mà không cần can thiệp.
- **Dữ liệu theo dõi toàn diện** trên Google Sheets (từ ý tưởng đến hiệu quả xuất bản).
- **Mở rộng dễ dàng** với nhiều ý tưởng viral mới mỗi tuần.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✅ **Tài khoản Google Sheets** (để lưu trữ ý tưởng và kết quả).
✅ **API Key Google Gemini** (để phân tích và tạo script).
✅ **API Key Veo 3** (để tạo video AI).
✅ **Tài khoản Blotato** (để xuất bản tự động lên Facebook/Instagram).
✅ **Tài khoản Apify** (để thu thập dữ liệu viral từ internet).

🔹 **Lưu ý:** Các sếp có thể sử dụng **Veo 3 của GeminigenAi** hoặc **Kie.ai** (đã được hỗ trợ trong workflow).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/13089](https://n8n.io/workflows/13089) và import vào **n8n Editor**.
- **Cách 2:** Copy toàn bộ JSON và dán vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **22 node**, các sếp cần chú ý cấu hình các node quan trọng sau:

##### **🔹 Node "Scrape Viral Health Content (Apify)"**
- **Tham số cần thiết:**
  - **Apify OAuth2 API Key** (đăng ký tại [Apify](https://apify.com/)).
  - **Actor ID** (sử dụng actor thu thập dữ liệu viral health, ví dụ: `apify/reddit-scraper`).
  - **URL hoặc query** để lấy dữ liệu (ví dụ: `r/health` trên Reddit).

##### **🔹 Node "Analyze Viral Potential & Hook" (Google Gemini)**
- **Tham số cần thiết:**
  - **Google Palm API Key** (đăng ký tại [Google AI Studio](https://aistudio.google/)).
  - **Prompt tối ưu hóa** (các sếp có thể chỉnh sửa trong node `toolThink` để phù hợp với nội dung health).

##### **🔹 Node "Create AI Video (Veo 3 API)"**
- **Tham số cần thiết:**
  - **API Key Veo 3** (đăng ký tại [GeminigenAi](https://geminigen.ai/) hoặc [Kie.ai](https://kie.ai)).
  - **Script input** (tự động lấy từ node `Generate AI Video Script`).
  - **Thời gian render** (thường là **5-15 phút** tùy video).

##### **🔹 Node "Publish Video to Facebook" (Blotato)**
- **Tham số cần thiết:**
  - **Blotato API Key** (đăng ký tại [Blotato](https://blotato.com/)).
  - **Tài khoản Facebook Business Manager** (để xuất bản tự động).

##### **🔹 Node "Update Status & Results in Sheet"**
- **Tham số cần thiết:**
  - **Google Sheets OAuth2 API Key** (đăng ký trong n8n).
  - **Sheet Name** (các sếp phải tạo một sheet mới với cấu trúc như trong workflow).

#### **3. Kích Hoạt ⚡️**
- **Test Run:** Chạy thử với **1-2 ý tưởng viral** để kiểm tra kết quả.
- **Bật Active:** Sau khi kiểm tra thành công, bật **Active** để workflow chạy tự động theo lịch.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tối ưu hóa prompt cho Gemini:**
   - Chỉnh sửa node `Reasoning / Prompt Logic` để AI phân tích **xu hướng cụ thể** (ví dụ: "Video về dinh dưỡng cho người giảm cân").
   - Ví dụ prompt nâng cao:
     ```plaintext
     Analyze this viral health idea: "[ý tưởng]". Provide:
     1. Top 3 hooks to grab attention in the first 3 seconds.
     2. Script structure (intro, main points, call-to-action).
     3. Keywords for SEO in video description.
     ```

2. **Lưu log và báo cáo:**
   - Thêm node **Google Sheets** để lưu **thống kê hiệu quả** (like, share, view count) sau khi xuất bản.
   - Sử dụng **n8n Dashboard** để theo dõi workflow.

3. **Xuất bản trên nhiều nền tảng:**
   - Thêm node **Instagram API** (nếu cần) bằng cách sử dụng **Blotato** hoặc **n8n-nodes-instagram**.

4. **Tự động chia sẻ video:**
   - Kết hợp với **Slack/Telegram** để thông báo khi video hoàn thành (sử dụng node **webhook**).

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp Content Creator Health để tập trung vào **strategy và sáng tạo**, trong khi AI và tự động hóa làm tất cả công việc thủ công.

**Hành động ngay:**
1. **Cài đặt n8n trên VPS** (để workflow chạy 24/7).
2. **Import workflow** và cấu hình các API key.
3. **Chạy thử** với 1-2 ý tưởng viral.
4. **Bật tự động** và theo dõi kết quả!

🚀 **Các sếp sẵn sàng tự động hóa content của mình chưa?** Nếu có vấn đề, hãy để lại comment dưới đây! 👇