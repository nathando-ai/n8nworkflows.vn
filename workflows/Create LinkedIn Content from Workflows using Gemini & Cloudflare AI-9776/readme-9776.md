---
title: "🚀 Tự Động Hóa Tạo Nội Dung LinkedIn Từ Workflow n8n Với Gemini & AI Cloudflare"
description: "Workflow này tự động chuyển đổi workflow n8n của bạn thành bài viết LinkedIn chuyên nghiệp kèm ảnh minh họa AI, tiết kiệm thời gian lên đến 90% so với cách viết thủ công. Hỗ trợ tự động hóa nội dung marketing 24/7."
slug: "tay-dong-hoa-tao-noi-dung-linkedin-tu-workflow-n8n"
tags: [n8n, automation, no-code, linkedin-automation, ai-content-creation, cloudflare-ai]
keywords: [tự động hóa linkedin, tạo bài viết linkedin tự động, gemini ai, cloudflare ai, n8n workflow linkedin]
---

# 🚀 **Tự Động Hóa Tạo Nội Dung LinkedIn Từ Workflow n8n Với Gemini & AI Cloudflare**

### **Giải pháp AI hoàn toàn tự động hóa nội dung LinkedIn cho các sếp kỹ thuật**
Bạn đã từng phải **vất vả viết bài LinkedIn** để giới thiệu workflow n8n của mình? Hay phải **tìm kiếm ảnh phù hợp** để minh họa? Hay **lo lắng về chất lượng nội dung** không chuyên nghiệp? Workflow này sẽ **giải quyết tất cả những vấn đề đó** bằng cách tự động:
✅ **Tạo bài viết LinkedIn** từ JSON của workflow n8n
✅ **Sinh ảnh minh họa** bằng AI Cloudflare (đảm bảo chất lượng 1M+ pixel)
✅ **Tự động đăng lên LinkedIn** chỉ với một cú nhấp chuột
✅ **Lưu lịch sử** trên Google Sheets để theo dõi hiệu suất

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính riêng tư và tốc độ tối ưu.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian lên đến 90%** so với viết bài thủ công.
- **Nội dung chuyên nghiệp** với hình ảnh AI chất lượng cao (1M+ pixel).
- **Tự động hóa hoàn toàn** – không cần viết code hoặc thiết kế.
- **Lưu trữ lịch sử** trên Google Sheets để phân tích hiệu suất.
- **Tích hợp Telegram** để kiểm soát và phản hồi dễ dàng.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản n8n Self-hosted** (đã cài đặt và chạy ổn định).
2. **API Keys & Credentials**:
   - **Google Gemini API** (để tạo nội dung và mô tả ảnh).
   - **Cloudflare API** (để sinh ảnh AI).
   - **LinkedIn OAuth2 API** (đăng bài tự động).
   - **Google Sheets OAuth2 API** (lưu lịch sử bài viết).
   - **Telegram Bot Token** (2 bot riêng biệt):
     - **Bot A**: Nhận JSON workflow → Trả về bài viết + ảnh AI.
     - **Bot B**: Nhận ảnh + nội dung → Đăng lên LinkedIn.
3. **Google Sheet** (để lưu trữ lịch sử bài viết).
4. **Workflow n8n JSON** (cần chuyển đổi thành bài viết).
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/9776](https://n8n.io/workflows/9776) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ [đây](link-json) và paste vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
##### **A. Cấu hình Telegram Bot**
- **Bot A (Generator)**:
  - Thiết lập **Telegram Trigger** để nhận file JSON.
  - Cấu hình **Telegram Node** để gửi lại bài viết + ảnh AI.
- **Bot B (Publisher)**:
  - Thiết lập **Telegram Trigger** để nhận ảnh + nội dung.
  - Cấu hình **Telegram Node** để phản hồi và kích hoạt đăng bài.

##### **B. Cấu hình Google Gemini**
- Trong node **"Gemini: Generate Post & Image Prompt"**:
  - Chọn **credentials**: `googlePalmApi`.
  - Điền **Prompt mẫu** (nếu cần tùy chỉnh):
    ```json
    "Tôi có một workflow n8n với JSON sau: {json}. Viết một bài viết LinkedIn chuyên nghiệp (tiếng Việt) về workflow này, bao gồm tiêu đề hấp dẫn, mô tả chi tiết và một mô tả ảnh AI phù hợp. Bài viết phải ngắn gọn (150-200 từ) và chuyên nghiệp."
    ```

##### **C. Cấu hình Cloudflare AI**
- Trong node **"Cloudflare: Get Account ID"** và **"Cloudflare: Generate Image"**:
  - Thêm **Cloudflare Account ID** vào URL:
    ```
    https://api.cloudflare.com/client/v4/accounts/{ACCOUNT_ID}/images/v1
    ```
  - Thiết lập **Headers**:
    ```json
    {
      "Authorization": "Bearer {API_KEY}",
      "Content-Type": "application/json"
    }
    ```
  - Trong node **"Set Image Generation Parameters"**, điền:
    ```json
    {
      "width": 1200,
      "height": 630,
      "format": "png",
      "model": "ai-image-1"
    }
    ```

##### **D. Cấu hình LinkedIn**
- Trong node **"Publish Post to LinkedIn"**:
  - Chọn **credentials**: `linkedInOAuth2Api`.
  - Đảm bảo **OAuth2 API** đã được cấp quyền **post** cho tài khoản LinkedIn.

##### **E. Cấu hình Google Sheets**
- Trong node **"Log Content to Google Sheet"**:
  - Điền **Google Sheet ID** (tìm trong URL của sheet).
  - Chọn **Sheet Name** (ví dụ: "LinkedIn Posts").
  - Cấu hình **Headers** để append dữ liệu:
    ```json
    {
      "range": "Sheet1!A1",
      "values": [
        [new Date().toISOString(), json.json.postContent, json.json.imageUrl]
      ]
    }
    ```

#### **3. Kích hoạt ⚡️**
- **Test Run**:
  - Gửi một **file JSON workflow** đến **Bot A** (Telegram).
  - Kiểm tra kết quả:
    - Bot A trả về **bài viết + ảnh AI**.
    - Chuyển ảnh + nội dung đến **Bot B**.
    - Bot B sẽ **đăng bài lên LinkedIn** khi nhận phản hồi.
- **Bật Active**: Sau khi test thành công, bật workflow.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tùy chỉnh Prompt Gemini**:
   - Thay đổi prompt để phù hợp với **ngôn ngữ mục tiêu** (Việt Nam, Anh, Nhật...).
   - Ví dụ:
     ```json
     "Viết bài viết LinkedIn về workflow này dành cho {ngành nghề cụ thể}, với phong cách {chuyên nghiệp/giản đơn/hài hước}."
     ```

2. **Lưu log chi tiết**:
   - Thêm node **StickyNote** để ghi chú lỗi hoặc cập nhật.
   - Ví dụ:
     ```json
     {
      "text": "Bài viết đã đăng thành công: {{$node["Parse Gemini Output"].json.postContent}}",
      "color": "#4CAF50"
     }
     ```

3. **Tích hợp Slack/Email báo cáo**:
   - Thêm node **Slack** hoặc **Email** để thông báo khi bài viết được đăng.
   - Cấu hình:
     ```json
     {
      "text": "🚀 Bài viết mới đã đăng lên LinkedIn!\nTiêu đề: {{$node["Parse Gemini Output"].json.postTitle}}\nLink: {{$node["Publish Post to LinkedIn"].json.url}}"
     }
     ```

4. **Sử dụng AI khác (LLM)**:
   - Thay thế Gemini bằng **Mistral AI** hoặc **Anthropic Claude** nếu có API.

---

### 📌 **Kết luận**
Workflow này là **công cụ AI hoàn hảo** để các sếp **tự động hóa nội dung LinkedIn** mà không cần viết code. Bằng cách kết hợp **Gemini (tạo nội dung)**, **Cloudflare AI (sinh ảnh)**, và **Telegram (quản lý)**, bạn có thể:
✔ **Tiết kiệm thời gian** lên đến 90% so với cách viết thủ công.
✔ **Tăng cường sự hiện diện** trên LinkedIn với nội dung chuyên nghiệp.
✔ **Tự động hóa hoàn toàn** – chỉ cần nhấp chuột là xong!

**Hãy thử ngay và biến workflow n8n của bạn thành bài viết LinkedIn hấp dẫn nhất!** 🚀

---
:::note[Liên hệ hỗ trợ]
Có vấn đề hoặc cần tùy chỉnh? Liên hệ với tác giả:
- **Email**: anirudh.n.aeran@gmail.com
- **LinkedIn**: [@anirudh-narayan](https://www.linkedin.com/in/anirudh-narayan-a/)
:::

---
**Happy automating!** 🤖✨