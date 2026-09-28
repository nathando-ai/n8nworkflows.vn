---
title: "🤖 Tự Động Tạo Video Avatar Nói Chuyển Động Từ Ảnh + Đăng TikTok Miễn Phí (N8N + ElevenLabs + Infinitalk)"
description: "Workflow tự động hóa hoàn toàn không code giúp các sếp tạo video avatar AI nói chuyển động từ 1 ảnh đơn giản và tự động đăng lên TikTok chỉ trong 5 giây. Giảm thời gian content creation 90% và tăng engagement cho brand."
slug: "tay-dong-tao-video-avatar-noi-chuyen-dong-den-tiktok"
tags: [n8n, automation, content-creation, ai-avatar, tiktok-automation, elevenlabs, infinitalk]
keywords: [tạo video avatar ai tiktok, tự động hóa content tiktok, elevenlabs n8n, infinitalk automation, tạo video nói chuyển động từ ảnh, workflow n8n miễn phí]
---

# 🚀 **Tạo Video Avatar Nói Chuyển Động Từ Ảnh + Đăng TikTok Tự Động (Không Code)**

## **Nỗi Đau Của Các Sếp Trong Content Creation TikTok**
Các sếp đang phải:
❌ **Tốn thời gian** để tạo video từ đầu (chụp ảnh, quay video, chỉnh sửa, lồng giọng)
❌ **Khó tạo nội dung cá nhân hóa** với nhiều avatar khác nhau
❌ **Phải quản lý nhiều công cụ** (ElevenLabs, Infinitalk, TikTok Business API)
❌ **Không đảm bảo tính nhất quán** trong chất lượng video

**Workflow này giải quyết tất cả!** Chỉ cần **1 ảnh + 1 đoạn văn bản**, hệ thống sẽ tự động:
✅ **Tạo avatar nói chuyển động** (thông qua ElevenLabs + Infinitalk)
✅ **Tạo tiêu đề hấp dẫn** (bằng AI OpenAI)
✅ **Đăng video lên TikTok** (thông qua Postiz)
✅ **Tối ưu thời gian** (từ 30 phút thành **5 giây**)

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ 30 phút tạo 1 video thành **5 giây** với workflow tự động.
- **Chất lượng chuyên nghiệp**: Avatar nói chuyển động mượt mà, giọng nói tự nhiên (ElevenLabs v3).
- **Tối ưu TikTok**: Video được đăng tự động với tiêu đề AI-optimized (OpenAI).
- **Cá nhân hóa dễ dàng**: Thay đổi ảnh + văn bản → video mới trong giây lát.
- **Hoạt động liên tục**: Workflow chạy 24/7, không cần can thiệp thủ công.
- **Miễn phí (hoặc rẻ)**: Dùng API miễn phí của ElevenLabs + Infinitalk (có giới hạn).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✅ **Tài khoản API**:
- [ElevenLabs](https://elevenlabs.io/) (API Key)
- [Infinitalk](https://infinitalk.ai/) (API Key)
- [OpenAI](https://platform.openai.com/) (API Key)
- [Postiz](https://postiz.com/) (API Key + Channel ID TikTok Business)

✅ **Dữ liệu đầu vào**:
- **Ảnh avatar** (URL hoặc file upload)
- **Văn bản** (nội dung video, tối đa 5 giây)
- **Giọng nói** (tên voice từ ElevenLabs)

✅ **N8n Node bổ sung**:
- Cài đặt **n8n-nodes-postiz** (để đăng video lên TikTok).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có 2 cách:
- **Tải file JSON** từ [n8n.io/workflows/8378](https://n8n.io/workflows/8378) và import vào n8n Editor.
- **Copy JSON** từ link trên và paste vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflows này gồm **18 node**, các sếp cần chú ý cấu hình **các node quan trọng sau**:

##### **A. Cấu Hình API Keys**
| Node | Tham Số Cần Điền | Ghi Chú |
|------|------------------|---------|
| **Create voice** | `httpHeaderAuth` | API Key ElevenLabs |
| **Get status audio** | `httpHeaderAuth` | API Key ElevenLabs |
| **Get Url Audio** | `httpHeaderAuth` | API Key ElevenLabs |
| **Create Video** | `httpHeaderAuth` | API Key Infinitalk |
| **Get status** | `httpHeaderAuth` | API Key Infinitalk |
| **Generate title** | `openAiApi` | API Key OpenAI |
| **Upload Video to Postiz** | `httpHeaderAuth` | API Key Postiz |
| **TikTok** | `postizApi` | API Key Postiz + Channel ID TikTok |

##### **B. Cấu Hình Dữ Liệu Đầu Vào**
1. **Node "Set text input"**:
   - Điền **text** (nội dung video).
   - Điền **voice name** (tên giọng từ ElevenLabs, ví dụ: "Adam").

2. **Node "Set Video Params"**:
   - Điền **image url** (URL ảnh avatar).
   - Điền **prompt** (ví dụ: *"Show a professional man speaking naturally"*).

3. **Node "Generate title" (OpenAI)**:
   - Điền **prompt** (ví dụ: *"Create a catchy TikTok title for a video about [topic]"*).

##### **C. Thời Gian Chờ (Wait Nodes)**
- Workflow có **2 node Wait 60s** để đảm bảo API hoàn thành xử lý.
- **Không xóa** các node này, nếu muốn tăng tốc, giảm thời gian chờ xuống 30s.

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Nhấn **"Test Workflow"** và nhập dữ liệu mẫu (ảnh + văn bản).
  - Kiểm tra **log** để đảm bảo không có lỗi API.
- **Bật Active**:
  - Sau khi test thành công, chuyển workflow sang **Active**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tối ưu API Key**:
   - Sử dụng **API Key miễn phí** của ElevenLabs (có giới hạn 10k credits/tháng).
   - Nếu cần scale, mua **gói Pro** (từ 10$/tháng).

2. **Tự động hóa thêm**:
   - **Gửi thông báo Slack/Telegram** khi video đăng thành công (thêm node **Slack** hoặc **Telegram**).
   - **Lưu log** vào **Google Sheets** để theo dõi hiệu suất (thêm node **Google Sheets**).

3. **Tạo nhiều video cùng lúc**:
   - Sử dụng **node "Set" + Loop** để chạy workflow với nhiều ảnh + văn bản khác nhau.

4. **Optimize TikTok**:
   - Thêm **hashtag** và **caption** tự động bằng OpenAI.
   - Sử dụng **Postiz Schedule** để đăng video vào thời gian tối ưu.

5. **Cải thiện chất lượng video**:
   - Thử **mô hình voice khác** của ElevenLabs (ví dụ: "Elliott" hoặc "Bella").
   - Điều chỉnh **prompt** trong Infinitalk để avatar có biểu cảm rõ ràng hơn.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào **strategy content** thay vì làm thủ công. Với **chỉ 5 giây**, các sếp có thể:
✔ **Tạo video avatar AI** từ 1 ảnh.
✔ **Đăng tự động lên TikTok** với tiêu đề AI-optimized.
✔ **Tối ưu engagement** cho brand.

**Hành động ngay!**
1. **Import workflow** và cấu hình API.
2. **Test với 1 ảnh + văn bản** để xem kết quả.
3. **Bật Active** và bắt đầu tự động hóa content TikTok!

👉 **Cần hỗ trợ?** Liên hệ tác giả Davide qua [LinkedIn](https://linkedin.com/in/davideboizza) hoặc email **info@n3w.it**.

---
**#TikTokAutomation #AIContent #N8NWorkflows #ElevenLabs #Infinitalk**