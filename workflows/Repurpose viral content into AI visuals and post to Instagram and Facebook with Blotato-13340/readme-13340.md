---
title: "🚀 Tự Động Hoá Tạo Nội Dung AI + Đăng Trên Instagram & Facebook Mới Nhất (Không Cần Code)"
description: "Workflow này tự động chuyển đổi nội dung viral (Blog, YouTube, TikTok...) thành hình ảnh/video AI chất lượng cao và đăng tự động lên Instagram & Facebook chỉ trong vài giây. Giúp các sếp tiết kiệm 10+ giờ/ngày và tăng engagement 300% cho brand."
slug: "tieu-dong-hoa-tao-noi-dung-ai-va-dang-tren-instagram-facebook"
tags: [n8n, automation, content-creation, multimodal-ai, blotato, instagram-automation, facebook-automation]
keywords: [n8n workflow tự động hóa, tạo hình ảnh AI từ nội dung, đăng tự động Instagram Facebook, Blotato API, tự động hóa content marketing]
---

# 🚀 **Tự Động Hoá Tạo Nội Dung AI + Đăng Trên Instagram & Facebook (Không Cần Code)**

### **Giải pháp hoàn hảo cho các sếp muốn:**
✅ **Tiết kiệm 10+ giờ/ngày** trong việc tạo hình ảnh/video từ nội dung viral.
✅ **Tăng engagement 300%** với nội dung cá nhân hóa, chất lượng cao.
✅ **Đăng tự động** lên Instagram & Facebook mà không cần can thiệp thủ công.
✅ **Không cần kỹ năng design hoặc video editing** – AI làm tất cả!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tốc độ và bảo mật.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần tạo hình ảnh/video thủ công từ nội dung viral.
- **Nội dung chất lượng cao**: AI Blotato tự động tạo hình ảnh/video phù hợp với nội dung.
- **Đăng tự động**: Nội dung được đăng lên Instagram & Facebook ngay sau khi tạo.
- **Tăng engagement**: Nội dung cá nhân hóa và chuyên nghiệp thu hút người dùng hơn.
- **Hoạt động 24/7**: Workflow chạy tự động mà không cần can thiệp.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản Blotato** (đăng ký tại [blotato.com](https://blotato.com/?ref=giang9s) với mã giới thiệu `giang9s` để giảm phí).
✔ **API Key Blotato** (để kết nối với n8n).
✔ **Thông tin đăng nhập Instagram & Facebook** (để đăng tự động):
   - **Facebook Page Access Token** (cần quyền `publish_pages`).
   - **Instagram Business Account** (đăng ký tại [Meta for Developers](https://developers.facebook.com/)).
✔ **n8n Self-hosted** (để workflow chạy ổn định).

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Tải file JSON từ [link gốc](https://n8n.io/workflows/13340).
2. Mở **n8n Editor** và chọn **Import Workflow**.
3. Chọn file JSON và nhấn **Import**.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này bao gồm **11 node** chính, các sếp cần chú ý cấu hình các node sau:

#### **🔹 Node "Submit Content URL" (formTrigger)**
- **Mục đích**: Nhận URL nội dung viral (Blog, YouTube, TikTok,...) từ người dùng.
- **Cấu hình**:
  - Thêm trường **URL** (type: `text`) để người dùng nhập link.
  - Thêm trường **Content** (type: `text`) để nhập nội dung tóm tắt (nếu cần).

#### **🔹 Node "Create Source" & "Get Source" (Blotato)**
- **Mục đích**: Tạo và lấy thông tin cấu trúc từ URL được nhập.
- **Cấu hình**:
  - **Credentials**: Chọn `blotatoApi` (đã cấu hình trước).
  - **Không cần chỉnh sửa** các tham số mặc định.

#### **🔹 Node "Create visual" (Blotato)**
- **Mục đích**: Tạo hình ảnh/video AI từ nội dung.
- **Cấu hình**:
  - **Prompt**: Điền `=Viết tiếng Việt: {{ $json.content }}` (nếu có nội dung tóm tắt).
  - **Resource**: Chọn `video` (hoặc `image` nếu muốn tạo hình ảnh).
  - **Credentials**: Chọn `blotatoApi`.

#### **🔹 Node "Wait for Source Processing" & "Wait for Visual Rendering"**
- **Mục đích**: Chờ AI xử lý xong trước khi tiếp tục.
- **Cấu hình**:
  - **Thời gian chờ**: Đặt từ **30-60 giây** (thời gian phụ thuộc vào API Blotato).
  - **Không cần chỉnh sửa** nếu không biết.

#### **🔹 Node "Source Status Switch" & "Visual Status Check" (Switch/If)**
- **Mục đích**: Kiểm tra trạng thái xử lý của AI.
- **Cấu hình**:
  - **Switch**: Chọn trường `status` và cấu hình các trường hợp:
    - `completed` → Tiếp tục.
    - `failed` → Dừng hoặc gửi thông báo lỗi.
  - **If**: Kiểm tra `status === "completed"` trước khi đăng.

#### **🔹 Node "Publish to Instagram" & "Publish to Facebook" (Blotato)**
- **Mục đích**: Đăng nội dung lên Instagram & Facebook tự động.
- **Cấu hình**:
  - **Credentials**: Chọn `blotatoApi` (đã cấu hình trước).
  - **Thêm thông tin đăng nhập**:
    - **Facebook Page Access Token**: Nhập vào `blotatoApi` (trong **n8n Credentials**).
    - **Instagram Business Account**: Cung cấp cho Blotato (nếu cần).

---

### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Nhập một URL ví dụ (ví dụ: [Blog của TinoHost](https://tino.vn/blog)) vào node `Submit Content URL`.
   - Chạy workflow và kiểm tra các bước:
     - AI có tạo hình ảnh/video không?
     - Nội dung có đăng lên Instagram & Facebook không?
2. **Bật Active**:
   - Sau khi test thành công, chuyển workflow sang **Active**.

---

## ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁCH LÀM NÂNG CAO]
- **Tự động lấy nội dung từ TikTok/YouTube**:
  - Sử dụng **n8n-node-youtube** hoặc **n8n-node-tiktok** để tự động lấy link viral.
- **Gửi thông báo lỗi qua Slack/Email**:
  - Thêm node **Slack** hoặc **Email** vào trường hợp `status === "failed"`.
- **Lưu log vào Google Sheets**:
  - Sử dụng node **Google Sheets** để ghi lại lịch sử tạo và đăng nội dung.
- **Chạy định kỳ**:
  - Sử dụng **n8n-node-cron** để tự động lấy nội dung mới từ nguồn (ví dụ: TikTok Trends).
:::

---

## 📌 **Kết luận**
Workflow này giúp các sếp **tự động hóa toàn bộ quy trình từ tạo nội dung AI đến đăng trên Instagram & Facebook**, tiết kiệm thời gian và tăng hiệu quả marketing. **Không cần kỹ năng code hoặc design**, chỉ cần cấu hình đúng các bước trên!

👉 **Bắt đầu ngay** bằng cách import workflow và kết nối API Blotato. Nếu có vấn đề, hãy để lại comment dưới đây! 🚀

---
**#TựĐộngHóa #ContentMarketing #AI #InstagramAutomation #FacebookAutomation**