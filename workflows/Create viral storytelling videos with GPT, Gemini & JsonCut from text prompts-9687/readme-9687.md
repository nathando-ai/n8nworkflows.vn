---
title: "🎬 Tự Động Hoàn Thành Video Storytelling Viral Từ Văn Bản Sử Dụng GPT-4, Gemini & JsonCut - Không Cần Code"
description: "Workflow này tự động chuyển đổi văn bản (như chủ đề, setting và phong cách) thành video storytelling chuyên nghiệp với hình ảnh AI, âm thanh và hiệu ứng watermark - hoàn toàn tự động hóa từ đầu đến cuối. Giúp các sếp tiết kiệm thời gian lên đến 80% so với làm thủ công."
slug: "tieu-dong-hoan-thanh-video-storytelling-gpt-gemini-jsoncut"
tags: [n8n, automation, no-code, ai-video-editing, storytelling, openai, google-gemini]
keywords: [n8n workflow video tự động, tạo video storytelling viral, GPT-4 tạo hình ảnh, Gemini AI tạo âm thanh, JsonCut tự động hóa video]
---

# 🚀 **Tạo Video Storytelling Viral Tự Động Từ Văn Bản - Không Cần Code**

### **Giải pháp hoàn hảo cho các sếp cần:**
- **Tạo video storytelling chuyên nghiệp** từ văn bản (chủ đề, setting, phong cách) **một cách tự động**
- **Không cần kỹ năng chỉnh sửa video** hoặc thiết kế hình ảnh
- **Tiết kiệm thời gian lên đến 80%** so với làm thủ công
- **Cung cấp video có chất lượng cao** với hình ảnh AI, âm thanh và hiệu ứng watermark chuyên nghiệp

---

## 🎯 **Kết quả các sếp nhận được**

:::tip[LỢI ÍCH CỐT LÕI]
✅ **Video chuyên nghiệp trong vài phút** thay vì mất nhiều giờ chỉnh sửa
✅ **Hình ảnh và âm thanh AI** phù hợp với chủ đề, không cần tìm kiếm tài liệu
✅ **Tự động lưu kết quả** vào cơ sở dữ liệu NocoDB để quản lý dễ dàng
✅ **Hoạt động 24/7** - không cần can thiệp thủ công
✅ **Tối ưu SEO** - video có thể được chia sẻ trên mạng xã hội hoặc trang web
:::

---

## 🔧 **Yêu cầu cần thiết**

:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
- **Tài khoản API** của các dịch vụ sau:
  - **OpenAI API** (để tạo hình ảnh và âm thanh)
  - **Google Gemini API** (để tạo hình ảnh từ văn bản)
  - **JsonCut API** (để tự động cắt ghép video)
  - **NocoDB API Token** (để lưu kết quả)
- **Tài khoản Google Drive** (để tải xuống hình ảnh và âm thanh mẫu)
- **Mã API Header Auth** (nếu sử dụng JsonCut hoặc dịch vụ khác yêu cầu)
:::

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Bước 1:** Tải file JSON từ [link gốc](https://n8n.io/workflows/9687) hoặc copy toàn bộ mã JSON từ đây.
- **Bước 2:** Mở **n8n Editor** và nhấn **"Import"** → Dán hoặc tải file JSON.
- **Bước 3:** Chọn **"Create new workflow"** và nhấn **"Import"**.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **🔹 Cấu hình API Keys & Credentials**
Workflow sử dụng nhiều API, các sếp cần **điền chính xác** các thông tin sau:

| **Node**                     | **Tham số cần điền**               | **Lưu ý**                                                                 |
|------------------------------|------------------------------------|---------------------------------------------------------------------------|
| **Generate content and Image Prompt** | `openAiApi` (API Key OpenAI)       | Điền API Key từ tài khoản OpenAI (mã `sk-...`)                          |
| **Generate an image**        | `googlePalmApi` (API Key Gemini)   | Điền API Key từ tài khoản Google Cloud (mã `AIza...`)                   |
| **Create JsonCut Job**       | `httpHeaderAuth` (Mã API JsonCut)  | Đăng ký tại [JsonCut](https://jsoncut.com/) và lấy mã API Header Auth    |
| **Save Video in NocoDB**     | `nocoDbApiToken`                   | Tạo token API từ NocoDB và điền vào credentials                          |

#### **🔹 Cấu hình Form Trigger (Bắt đầu workflow)**
- Node **"On form submission"** sẽ **khởi động workflow** khi có dữ liệu đầu vào.
- Các sếp cần **cấu hình form** với **3 trường dữ liệu** sau (đối ứng với ví dụ trong workflow):
  1. **General Video Theme** (Ví dụ: *"Overcoming struggles / personal growth"*)
  2. **Video Setting** (Ví dụ: *"Introspective, deep thinking, sunrise or twilight moments"*)
  3. **Background Image Style** (Ví dụ: *"Watercolor painting with muted colors, low light"*)

#### **🔹 Cấu hình JsonCut (Tự động cắt ghép video)**
- Workflow sử dụng **JsonCut API** để tự động ghép hình ảnh, âm thanh và logo thành video cuối cùng.
- Nếu không muốn sử dụng JsonCut, các sếp có thể **thay thế bằng JsonCut Community Node** (liên kết trong ghi chú của workflow).

#### **🔹 Cấu hình OpenAI & Gemini**
- **OpenAI (DALL·E 3 & TTS)** sẽ tạo **hình ảnh và âm thanh** từ văn bản.
- **Gemini (Google AI)** sẽ **tạo hình ảnh** với phong cách được chỉ định.
- Các sếp cần **đảm bảo tài khoản có đủ credit** để tránh lỗi API.

#### **🔹 Lưu ý về hình ảnh và âm thanh**
- Workflow sẽ **tải xuống hình ảnh mẫu** từ Google Drive (đã được cấu hình trong node `Download Image`).
- **Âm nhạc nền** sẽ được tải từ danh sách âm nhạc mẫu (node `Get List of background Audio`).

---

### **3. Kích hoạt ⚡️**
- **Bước 1:** Nhấn **"Test Run"** với dữ liệu mẫu (ví dụ trong phần **Example Form Input**).
- **Bước 2:** Kiểm tra **log** để đảm bảo workflow chạy đúng.
- **Bước 3:** Nhấn **"Active"** để workflow hoạt động liên tục.

---

## ✍️ **Mẹo & gợi ý nâng cao**

### **🔹 Tối ưu hóa chất lượng video**
- **Chọn âm nhạc phù hợp** với chủ đề (ví dụ: âm nhạc yên tĩnh cho video introspective).
- **Thử nghiệm các phong cách hình ảnh** (ví dụ: watercolor, pixel art, 3D) để tìm phong cách phù hợp nhất.

### **🔹 Tích hợp với Slack/Telegram**
- Thêm node **Slack/Telegram Webhook** sau node `Save Video in NocoDB` để **báo cáo kết quả** ngay khi video hoàn thành.

### **🔹 Lưu log hoạt động**
- Sử dụng node **Sticky Note** hoặc **Google Sheets** để **lưu lịch sử chạy workflow**, giúp theo dõi hiệu suất.

### **🔹 Tạo báo cáo định kỳ**
- Sử dụng **n8n Scheduler** để **chạy workflow hàng tuần/month** với các chủ đề mới, tự động tạo video cho nội dung mới.

---

## 📌 **Kết luận**

Workflow này là **giải pháp hoàn hảo** cho các sếp muốn **tạo video storytelling chuyên nghiệp mà không cần kỹ năng chỉnh sửa**. Với sự kết hợp của **GPT-4, Gemini AI và JsonCut**, video sẽ được tự động tạo ra từ văn bản, với **hình ảnh, âm thanh và hiệu ứng watermark** chuyên nghiệp.

**🚀 Hãy áp dụng ngay và tiết kiệm thời gian cho công việc sáng tạo!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**💡 Lưu ý:** Nếu gặp lỗi, hãy kiểm tra **log của node `Error Stop`** và **cập nhật lại API Key** nếu cần.