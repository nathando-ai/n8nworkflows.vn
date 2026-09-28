---
title: "🚀 Tự Động Hoà Hợp: Tạo Bài Đăng LinkedIn Với Ảnh & Văn Bản AI (Gemini + LinkedIn) - Không Cần Code"
description: "Workflow tự động hóa hoàn toàn giúp các sếp tạo bài đăng LinkedIn chuyên nghiệp với ảnh minh họa độc đáo và văn bản hấp dẫn chỉ bằng 1 cú click, tiết kiệm thời gian lên đến 80% so với cách làm thủ công."
slug: "tay-dong-hoa-tao-bai-dang-linkedin-ai"
tags: [n8n, automation, content-creation, ai-multimodal, linkedin-automation, google-gemini]
keywords: [tự động hóa bài đăng LinkedIn, tạo ảnh AI cho LinkedIn, Gemini API LinkedIn, workflow n8n content marketing, tự động hóa marketing không code]
---

# 🚀 **Tự Động Hoà Hợp: Tạo Bài Đăng LinkedIn Với Ảnh & Văn Bản AI (Gemini + LinkedIn)**

### **🔥 Nỗi Đau Của Các Sếp Trong Content Marketing**
Các sếp thường phải mất **giờ đồng hồ** để:
- Tìm kiếm **quote/đoạn văn** phù hợp cho bài đăng.
- **Tạo ảnh minh họa** chuyên nghiệp (thường phải thuê designer hoặc sử dụng công cụ design phức tạp).
- **Viết văn bản hấp dẫn** mà vẫn giữ được tính chuyên nghiệp.
- **Chia sẻ lên LinkedIn** một cách thủ công, mất thời gian check lại lỗi.

**Workflow này giải quyết tất cả!** Với **AI Gemini** (Google) và **n8n**, các sếp chỉ cần **gửi một quote**, hệ thống sẽ tự động:
✅ **Tạo ảnh minh họa** độc đáo, chuyên nghiệp.
✅ **Viết văn bản caption** hấp dẫn, cá nhân hóa.
✅ **Đăng bài lên LinkedIn** một cách tự động.

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ **30 phút/bài đăng** xuống **5 giây** (chỉ cần click submit).
- **Nội dung chuyên nghiệp**: Ảnh và văn bản được tạo bởi **AI Gemini**, đảm bảo tính sáng tạo và chuyên nghiệp.
- **Hoạt động 24/7**: Workflow chạy tự động, không cần can thiệp thủ công.
- **Tăng engagement**: Văn bản và ảnh được tối ưu hóa để thu hút người đọc.
- **Dễ dàng chia sẻ**: Kết quả được trả về website để các sếp **chỉnh sửa và đăng** một cách dễ dàng.
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản LinkedIn** (đã cấp quyền API).
2. **API Key Google Gemini** (tạo tại [AI Studio Google](https://aistudio.google.com/)).
3. **Website HTML** (cung cấp bởi tác giả, link tải ở phần dưới).
4. **n8n Self-hosted** (không dùng phiên bản miễn phí để đảm bảo hoạt động 24/7).
:::

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/13112](https://n8n.io/workflows/13112) hoặc copy toàn bộ JSON từ link trên.
- Mở **n8n Editor** → **Import Workflow** → Dán JSON và nhấn **Import**.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **11 node**, các sếp cần chú ý cấu hình sau:

##### **A. Cấu Hình Webhook (Lấy Dữ Liệu Từ Website)**
- **Node: "Webhook - Receive Form"**
  - **Path**: `Linkedin-update` (không thay đổi).
  - **HTTP Method**: `POST` (không thay đổi).
- **Node: "Webhook-LinkedIn-post"**
  - **Path**: `d01e0a95-5a60-4c9f-9f4e-3e6ef694f402` (không thay đổi).
  - **HTTP Method**: `POST` (không thay đổi).

##### **B. Cấu Hình API Keys**
- **Google Gemini**:
  - Tạo **credentials** mới trong n8n với tên `googlePalmApi`.
  - Điền **API Key** từ [AI Studio Google](https://aistudio.google.com/).
- **LinkedIn**:
  - Tạo **credentials** mới với tên `linkedInOAuth2Api`.
  - Cấu hình **OAuth 2.0** theo hướng dẫn của [LinkedIn Developer](https://developer.linkedin.com/).

##### **C. Cấu Hình Prompt AI (Tạo Ảnh & Văn Bản)**
- **Node: "Generate post image"**
  - **Prompt mặc định**:
    ```
    Create a modern, minimal but visually fuller illustration inspired by this quote "{{ $json.body.quote }}".
    Generate a unique background color for every output, using rich but professional tones that are not overly bright.
    Design a concept-driven scene that clearly symbolizes the core message of the quote.
    ```
  - **Không thay đổi** nếu muốn kết quả nhất quán.

- **Node: "Generate post caption"**
  - **Agent AI** sẽ tự động xử lý, không cần cấu hình thêm.

##### **D. Cấu Hình Website HTML**
- **Tải file HTML** từ [đây](https://drive.google.com/file/d/1JvViq-oNAdZosNOr7S5PfrxgbYcpK1Te/view).
- **Thay đổi 2 Webhook URL** trong file HTML:
  - Thay `YOUR_WEBHOOK_URL_1` bằng URL của **Webhook - Receive Form** (của n8n).
  - Thay `YOUR_WEBHOOK_URL_2` bằng URL của **Webhook-LinkedIn-post** (của n8n).
- **Host website** lên một domain hoặc sử dụng **Vercel/Netlify** để dễ dàng chia sẻ.

##### **E. Cấu Hình Node "Create Linkedin post"**
- **Credentials**: Chọn `linkedInOAuth2Api` (đã cấu hình trước).
- **Không cần thay đổi** các tham số khác.

#### **3. Kích Hoạt Workflow ⚡️**
- **Test Run**:
  - Gửi một **quote mẫu** qua website HTML.
  - Kiểm tra **output** từ node **"Combine the branches"** để đảm bảo ảnh và văn bản được tạo đúng.
- **Bật Active**:
  - Sau khi test thành công, **bật workflow** và **đăng bài lên LinkedIn** một cách tự động.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[TIẾP CẬN HƠN]
1. **Tích Hợp Slack/Telegram**:
   - Sử dụng **node Slack** hoặc **Telegram Bot** để thông báo khi bài đăng được tạo thành công.
   - Cấu hình trong node **"Respond to Webhook"** để gửi tin nhắn tự động.

2. **Lưu Log & Báo Cáo**:
   - Sử dụng **node StickyNote** để lưu lịch sử bài đăng.
   - Tạo **báo cáo tuần/month** về số lượng bài đăng và engagement.

3. **Tùy Chỉnh Prompt AI**:
   - Nếu muốn **ảnh/van bản khác biệt**, chỉnh sửa prompt trong node **"Generate post image"** và **"Generate post caption"**.
   - Ví dụ: Thêm yêu cầu **"phù hợp với ngành [ngành nghề]"** vào prompt.

4. **Tự Động Chia Sẻ Đến Nhóm**:
   - Sử dụng **node LinkedIn Groups** để chia sẻ bài đăng vào nhóm chuyên môn.
---
### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn **tự động hóa content marketing** trên LinkedIn mà **không cần viết code**. Với **AI Gemini** và **n8n**, các sếp có thể:
✔ **Tiết kiệm thời gian** lên đến **80%** so với cách làm thủ công.
✔ **Tăng chất lượng nội dung** với ảnh và văn bản được tạo bởi AI.
✔ **Hoạt động 24/7** mà không cần can thiệp.

**👉 Hãy thử ngay!**
1. **Tải file HTML** và **cấu hình webhook**.
2. **Import workflow** và **cấu hình API**.
3. **Gửi quote** và **xem kết quả AI tạo ra!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::