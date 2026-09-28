---
title: "🎨 Tự Động Lấy Ảnh Embeddable từ Getty Images Miễn Phí - Không Cần Code!"
description: "Workflow n8n tự động tìm kiếm, phân tích và lấy mã iframe embeddable từ Getty Images để sử dụng trong bài viết, blog hoặc trang web. Giúp tiết kiệm thời gian lên tới 90% so với cách thủ công."
slug: "tu-dong-lay-anh-embeddable-getty-images"
tags: [n8n, automation, marketing, no-code, getty-images]
keywords: [n8n workflow getty images, tự động hóa lấy ảnh, embeddable image, tự động hóa marketing, n8n tự động lấy ảnh miễn phí]
---

# 🎨 **Tự Động Lấy Ảnh Embeddable từ Getty Images - Giải Pháp Tiết Kiệm Thời Gian cho Các Sếp Marketing**

### **Nỗi Đau Thực Tế Của Các Sếp**
Làm việc với nội dung marketing, các sếp thường phải mất **từ 30-60 phút** để tìm kiếm, tải xuống và embed một ảnh chất lượng cao từ Getty Images. Quá trình này bao gồm:
- **Tìm kiếm thủ công** trên trang Getty Images với từ khóa phù hợp.
- **Phân tích trang kết quả** để chọn ảnh phù hợp.
- **Tải mã iframe embeddable** từ trang chi tiết ảnh (nếu có).
- **Sao chép mã** và embed vào bài viết hoặc trang web.

Với **n8n**, các sếp có thể **tự động hóa toàn bộ quy trình này chỉ trong vài giây**, không cần viết một dòng code nào!

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian lên tới 90%** so với cách làm thủ công.
- **Chất lượng ảnh cao** từ Getty Images (miễn phí cho mục đích thương mại).
- **Tự động hóa liên tục** (24/7) khi kết nối với các hệ thống CMS hoặc blog.
- **Mã embeddable chính xác** không cần sao chép tay.
- **Dễ dàng mở rộng** cho nhiều từ khóa hoặc dự án khác.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow này hoạt động, các sếp cần:
1. **Tài khoản Getty Images** (đăng ký miễn phí tại [gettyimages.com](https://www.gettyimages.com/)).
2. **API Key hoặc Credentials** (nếu Getty Images yêu cầu).
3. **n8n Self-hosted** (để chạy workflow 24/7).
   :::info[Gợi ý hạ tầng cho n8n]
   Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
   :::
4. **Dữ liệu đầu vào** (từ khóa tìm kiếm ảnh).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Tải file JSON từ [link gốc](https://n8n.io/workflows/2795).
2. Mở **n8n Editor** và chọn **"Import"** → Chọn file JSON.
3. Hoặc copy toàn bộ JSON và paste vào **"Import Workflow"** trong n8n.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này bao gồm **13 node** với các bước sau:

##### **A. Cấu Hình Node "Getty Images Editorial Search" (httpRequest)**
- **Method:** `GET`
- **URL:** `https://www.gettyimages.com/vi/vi/search?phrase={input_keyword}&sort=popular`
  - Thay `{input_keyword}` bằng **node "Replaceable input"** (node `set` có tên này).
- **Headers:**
  ```json
  {
    "Accept": "text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8",
    "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36"
  }
  ```
- **Lưu ý:** Nếu Getty Images yêu cầu **cookie hoặc session**, các sếp cần thêm vào headers.

##### **B. Cấu Hình Node "Parse results page for first image" (html)**
- **Selector:** `$('div.result-item img').attr('src')` (lấy URL ảnh đầu tiên).
- **Lưu ý:** Nếu trang Getty Images thay đổi CSS, các sếp cần **inspect element** và cập nhật selector.

##### **C. Cấu Hình Node "Extract the Getty image_id from url" (set)**
- **Expression:**
  ```json
  {
    "image_id": "{{$json.url.split('/').slice(-1)[0]}}"
  }
  ```
  - Trích xuất `image_id` từ URL ảnh để lấy chi tiết.

##### **D. Cấu Hình Node "Request Getty Images Embed code" (httpRequest)**
- **Method:** `GET`
- **URL:** `https://www.gettyimages.com/vi/vi/embed/{image_id}`
  - Thay `{image_id}` bằng giá trị từ node trước.
- **Headers:** Giống như node "Getty Images Editorial Search".

##### **E. Cấu Hình Node "Get Embeddable iframeSnippet" (set)**
- **Expression:**
  ```json
  {
    "iframeSnippet": "{{$json}}"
  }
  ```
  - Lấy toàn bộ mã iframe từ response.

##### **F. Node "Raise error when no results" (stopAndError)**
- **Expression:**
  ```json
  {{!$json.url}}
  ```
  - Nếu không tìm thấy URL ảnh, workflow sẽ dừng và báo lỗi.

#### **3. Kích Hoạt ⚡️**
1. **Test Run:**
   - Điền **từ khóa tìm kiếm** vào node `manualTrigger` (ví dụ: "business meeting").
   - Chạy workflow và kiểm tra kết quả.
2. **Bật Active:**
   - Sau khi test thành công, chuyển workflow sang **Active**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[CÁCH SỬ DỤNG HIỆU QUẢ]
1. **Kết Nối với CMS/WordPress:**
   - Sử dụng node **WordPress API** để tự động embed ảnh vào bài viết.
2. **Lưu Log Lịch Sử:**
   - Thêm node **Google Sheets** hoặc **Airtable** để ghi lại lịch sử tìm kiếm.
3. **Tự Động Hoạt Động Theo Lịch:**
   - Sử dụng **n8n Scheduler** để chạy workflow định kỳ (ví dụ: mỗi sáng).
4. **Tích Hợp với Slack/Telegram:**
   - Gửi kết quả tìm kiếm vào kênh Slack/Telegram bằng node **Slack Webhook**.
5. **Tối Ưu Từ Khóa:**
   - Sử dụng **LLM (n8n-nodes-base.llm)** để tự động đề xuất từ khóa phù hợp.
:::

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp marketing để tập trung vào nội dung chất lượng cao hơn. Bằng cách tự động hóa việc lấy ảnh embeddable từ Getty Images, các sếp không chỉ **tiết kiệm thời gian** mà còn **nâng cao hiệu suất công việc** một cách đáng kể.

**Hãy áp dụng ngay và bắt đầu tự động hóa từ hôm nay!** 🚀

---
**🔗 [Tải Workflow JSON](https://n8n.io/workflows/2795)**
**📌 [Cài n8n Self-hosted](https://docs.n8n.io/)**
**💬 [Hỏi đáp với Ludwig](https://www.linkedin.com/in/ludwiggerdes/)**