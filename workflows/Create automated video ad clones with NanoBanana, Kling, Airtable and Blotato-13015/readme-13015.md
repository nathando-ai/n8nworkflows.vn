---
title: "🎬 Tự Động Hóa Xưởng Sản Xuất Quảng Cáo Video AI - Từ Video Gốc Đến Post AI Chỉ Với 1 Clic!"
description: "Workflow này tự động phân tích video gốc, tạo các scene, sinh ra hình ảnh, video, nhạc và bài viết AI, cuối cùng xuất bản trên Blotato - hoàn toàn không cần code. Giúp các sếp tiết kiệm 80% thời gian sản xuất quảng cáo video!"
slug: "tieu-dong-hoa-xuong-san-xuat-quang-cao-video-ai"
tags: [n8n, automation, content-creation, multimodal-ai, airtable, blotato, nano-banana, kling, openai, google-gemini]
keywords: [n8n workflow tự động hóa, sản xuất quảng cáo video AI, nano banana kling, tự động hóa content creation, airtable + blotato, tự động hóa marketing]
---

# 🚀 **Xưởng Sản Xuất Quảng Cáo Video AI - Tự Động Hóa 100%**

## **Nỗi Đau Của Các Sếp Trong Sản Xuất Quảng Cáo Video**
Các sếp thường phải mất **từ 2-5 ngày** để sản xuất một quảng cáo video từ đầu đến cuối:
✅ Phân tích video gốc và viết kịch bản
✅ Tạo hình ảnh, video scene theo kịch bản
✅ Ghép video, thêm nhạc và hiệu ứng
✅ Chỉnh sửa và xuất bản trên các nền tảng

**Workflow này giải quyết tất cả bằng AI + tự động hóa!** Chỉ cần **nạp video gốc vào Airtable**, hệ thống sẽ tự động:
✔ **Phân tích video** → Tách scene, phân tích cấu trúc
✔ **Tạo hình ảnh AI** (NanoBanana) → Hình ảnh scene 100% phù hợp
✔ **Sinh video AI** (Kling) → Video scene động và chuyên nghiệp
✔ **Tạo nhạc AI** → Nhạc phù hợp với video
✔ **Ghép video + nhạc** → Video hoàn chỉnh
✔ **Xuất bản tự động** → Đăng lên Blotato (hoặc nền tảng khác)

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** so với cách làm thủ công
- **Chất lượng chuyên nghiệp** với video scene được AI phân tích và tạo
- **Tự động hóa hoàn toàn** - không cần can thiệp thủ công
- **Cá nhân hóa** - mỗi video scene có hình ảnh, video riêng biệt
- **Xuất bản tự động** - đăng lên Blotato chỉ với 1 click
- **Dễ dàng mở rộng** - thêm video mới chỉ cần update Airtable
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
**1. Tài Khoản Cần Thiết:**
- **Airtable** (để lưu trữ video gốc, scene, kết quả)
- **NanoBanana** (tạo hình ảnh AI)
- **Kling** (tạo video AI)
- **Blotato** (xuất bản video)
- **OpenAI API** (ChatGPT 4.1 Mini)
- **Google Gemini API** (phân tích video)

**2. Cấu Trúc Airtable:**
- **Bảng chính:** `Video Projects` với các trường:
  - `Original Video` (link video gốc)
  - `Avatar Image` (ảnh đại diện)
  - `Product Image` (ảnh sản phẩm)
  - `Status` (trạng thái: "Waiting", "In Progress", "Done")
  - `Prompts` (dữ liệu đầu vào cho AI)
  - `Scenes` (danh sách scene đã tạo)
  - `Music File` (link nhạc AI)
  - `Final Video` (link video cuối cùng)
  - `Published Post` (link bài viết trên Blotato)

**3. API Keys:**
- **Airtable API Key** (trong `airtableTokenApi`)
- **OpenAI API Key** (trong `openAiApi`)
- **Google Gemini API Key** (trong `googlePalmApi`)
- **Blotato API Key** (trong `blotatoApi`)
- **NanoBanana/Kling API** (thông qua AtlasCloud)

---
---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/13015](https://n8n.io/workflows/13015) hoặc copy/paste JSON vào **n8n Editor**.
- **Nhấn "Import"** và chọn **Self-hosted** (nếu dùng VPS).

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **5 bước chính**, mỗi bước có các node quan trọng cần cấu hình:

##### **📌 Bước 1: Tạo Prompt (Setup Workflow)**
- **Node "Setup Workflow"** → Điền **cấu trúc prompt** cho AI (ví dụ: mô tả video gốc, yêu cầu scene, phong cách hình ảnh).
- **Node "Generate Creative Assets JSON"** → Sử dụng **Agent AI** để tạo JSON cấu trúc scene.

##### **📌 Bước 2: Tạo Hình Ảnh AI (NanoBanana)**
- **Node "OpenAI Chat Model"** → Điền **prompt chi tiết** cho hình ảnh (ví dụ: "Tạo hình ảnh scene 1 của video quảng cáo, phong cách cinematic").
- **Node "Generate Image POST"** → Gửi request đến **NanoBanana** (thông qua AtlasCloud) để tạo hình ảnh.
- **Node "Wait 3 Minutes"** → NanoBanana cần thời gian xử lý.
- **Node "Update Record with Image"** → Cập nhật hình ảnh vào Airtable.

##### **📌 Bước 3: Tạo Video AI (Kling)**
- **Node "Analyze video"** → Sử dụng **Google Gemini** để phân tích video gốc.
- **Node "Generate Video POST"** → Gửi request đến **Kling** (thông qua AtlasCloud) để tạo video scene.
- **Node "Wait 5 Minutes"** → Kling cần thời gian xử lý.
- **Node "Update Record with Video"** → Cập nhật video vào Airtable.

##### **📌 Bước 4: Ghép Video & Tạo Nhạc**
- **Node "Merge All Videos"** → Ghép tất cả video scene thành 1 video hoàn chỉnh.
- **Node "Create audio"** → Tạo nhạc AI (thông qua API nhạc).
- **Node "Merge audio and video"** → Ghép nhạc vào video cuối cùng.

##### **📌 Bước 5: Xuất Bản Tự Động (Blotato)**
- **Node "Upload media"** → Upload video lên Blotato.
- **Node "Create post"** → Tạo bài viết và đăng video.
- **Node "Update Status"** → Cập nhật trạng thái "Done" trong Airtable.

---
#### **3. Kích Hoạt ⚡️**
- **Test Run:** Chọn **Manual Trigger** và chạy với **1 video mẫu** để kiểm tra.
- **Bật Active:** Sau khi kiểm tra thành công, **bật workflow** và **cấu hình Schedule Trigger** để chạy tự động hàng ngày.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tối ưu hóa Airtable:**
   - Sắp xếp bảng theo **trạng thái** ("Waiting", "In Progress", "Done") để dễ theo dõi.
   - Thêm **trường "Error Log"** để ghi lỗi nếu workflow bị lỗi.

2. **Kết hợp với Slack/Telegram:**
   - Thêm **node Slack/Telegram** để thông báo khi workflow hoàn thành.

3. **Lưu Log & Monitoring:**
   - Sử dụng **node Set** để lưu log vào Airtable hoặc Google Sheets.

4. **Tùy chỉnh Prompt:**
   - Đối với **OpenAI/Gemini**, thử nghiệm các **prompt khác nhau** để tối ưu hóa kết quả.

5. **Dùng VPS để chạy 24/7:**
   - Cài **n8n trên VPS** để workflow chạy tự động mà không cần mở máy.

---
### 📌 **Kết Luận**
Workflow này là **công cụ hoàn hảo** cho các sếp muốn **tự động hóa sản xuất quảng cáo video** mà không cần code. Từ **phân tích video** đến **xuất bản AI**, tất cả đều được tự động hóa chỉ với **1 click**.

**Hãy thử ngay và tiết kiệm 80% thời gian sản xuất quảng cáo!** 🚀

---
**🔗 [Tải workflow gốc](https://n8n.io/workflows/13015)**
**📖 [Hướng dẫn chi tiết Notion](https://automatisation.notion.site/Clone-Video-Ads-Factory-using-NanoBanana-Kling-and-Publish-with-Blotato-2f03d6550fd980a78193e996cca37600?source=copy_link)**
**🎁 [Đăng ký VPS n8n](https://tino.vn/vps-n8n?affid=388) với mã giảm giá **VPSN8N**!**