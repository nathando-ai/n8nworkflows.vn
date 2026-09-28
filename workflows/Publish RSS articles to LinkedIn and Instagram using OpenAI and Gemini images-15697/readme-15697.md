---
title: "🚀 Tự Động Hóa Bài Viết RSS Sang Bài Đăng LinkedIn & Instagram Với AI (OpenAI + Gemini) - Không Cần Code"
description: "Workflow tự động hóa 100% miễn phí chuyển đổi bài viết từ RSS thành nội dung LinkedIn và Instagram hoàn chỉnh, bao gồm bài viết, hình ảnh AI và hashtags. Giúp các sếp tiết kiệm 10+ giờ/ngày, tăng engagement và tự động hóa nội dung xã hội 24/7."
slug: "tu-dong-hoa-rss-sang-linkedin-instagram-ai"
tags: [n8n, automation, social-media, ai, openai, gemini, no-code]
keywords: [n8n workflow tự động hóa, RSS sang LinkedIn Instagram, AI tạo nội dung xã hội, tự động hóa content marketing, OpenAI Gemini n8n]
---

# 🚀 **Tự Động Hóa Bài Viết RSS Sang LinkedIn & Instagram Với AI (OpenAI + Gemini)**

### **Giải pháp cho các sếp:**
- **Thủ công viết bài LinkedIn/Instagram** mất **10+ giờ/ngày**?
- **Không biết cách tạo hình ảnh đẹp** cho bài đăng?
- **Bài viết không thu hút** vì thiếu cá nhân hóa?
- **Muốn tự động hóa nội dung xã hội** nhưng không biết từ đâu bắt đầu?

Workflow này **tự động chuyển đổi bài viết từ RSS** (như TechCrunch, Forbes, hoặc blog cá nhân) thành **bài đăng LinkedIn + Instagram hoàn chỉnh**, bao gồm:
✅ **Bài viết LinkedIn** (cá nhân hóa, thu hút)
✅ **Caption Instagram** (hấp dẫn, có hashtags)
✅ **Hình ảnh AI** (tạo bởi Gemini, phù hợp với nội dung)
✅ **Tự động đăng** lên 2 nền tảng trong **1 workflow**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài **n8n trên VPS riêng (Self-hosted)** để tránh giới hạn của phiên bản miễn phí.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ sức mạnh cho workflow này)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/ngày** viết bài và tạo hình ảnh.
- **Nội dung cá nhân hóa** theo phong cách riêng của doanh nghiệp.
- **Hình ảnh AI chuyên nghiệp** thay vì sử dụng hình ảnh stock.
- **Tự động đăng** lên LinkedIn và Instagram **không cần can thiệp**.
- **Tăng engagement** với bài viết được tối ưu cho mỗi nền tảng.
- **Hoạt động 24/7** mà không cần người quản lý.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản RSS Feed** (cần URL RSS của nguồn bài viết, ví dụ: `https://feeds.feedburner.com/TechCrunch`).
2. **API Key OpenAI** (để sử dụng GPT-4o-mini tạo nội dung).
   - **Lấy API Key tại:** [https://platform.openai.com/api-keys](https://platform.openai.com/api-keys)
3. **API Key Google Gemini** (để tạo hình ảnh AI).
   - **Lấy API Key tại:** [https://makersuite.google.com/app](https://makersuite.google.com/app)
4. **Tài khoản LinkedIn** (để đăng bài).
   - **Cấu hình OAuth 2.0** trong n8n (hướng dẫn sau).
5. **Tài khoản Instagram Business** (để đăng hình ảnh).
   - **Cần API Instagram** (sử dụng node `@mookielianhd/n8n-nodes-instagram`).
6. **UploadToURL API** (để lưu trữ hình ảnh AI và tạo URL công khai).
   - **Lựa chọn miễn phí:** [ImgBB](https://imgbb.com/) hoặc [Cloudinary](https://cloudinary.com/).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/15697](https://n8n.io/workflows/15697).
- **Nhấn "Import"** trong n8n Editor và chọn file JSON.
- **Hoặc copy/paste** JSON vào **Import Workflow** trong giao diện.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **9 node**, các sếp cần cấu hình **cẩn thận** các phần sau:

##### **🔹 Node 1: Watch RSS Feed for New Articles**
- **Tham số cần thiết:**
  - **RSS URL:** Điền URL RSS của nguồn bài viết (ví dụ: `https://feeds.feedburner.com/TechCrunch`).
  - **Interval (phút):** Thiết lập **60 phút** để kiểm tra mới bài (thường xuyên hơn sẽ tăng load).
  - **Credentials:** Không cần (sử dụng mặc định).

##### **🔹 Node 2: Extract Article Data**
- **Cấu hình mặc định** đã đủ, không cần thay đổi.
- **Output:** Trích xuất `article_title`, `article_link`, `article_description`, `published_date`.

##### **🔹 Node 3: Generate Social Media Content (OpenAI)**
- **Credentials:** Chọn `openAiApi` (đã cấu hình trước).
- **Model:** Đặt `gpt-4o-mini` (mặc định).
- **Prompt AI:**
  ```json
  {
    "instruction": "Tạo nội dung xã hội cho bài viết RSS sau:\n\nTitle: {{ $json.article_title }}\nDescription: {{ $json.article_description }}\nLink: {{ $json.article_link }}\n\nYêu cầu:\n1. **Content Angle:** Góc nhìn chính của bài viết (1-2 câu).\n2. **LinkedIn Post:** Bài đăng LinkedIn (5-7 câu, có câu hỏi hoặc call-to-action).\n3. **Instagram Caption:** Caption hấp dẫn (không quá 220 ký tự).\n4. **Instagram Image Prompt:** Mô tả hình ảnh AI (phù hợp với nội dung).\n5. **Hashtags:** 5-7 hashtag liên quan.\n\nTrả về JSON có cấu trúc rõ ràng!"
  ```
- **Lưu ý:** Nếu OpenAI trả về JSON không đúng định dạng, **Node 4 (Parse AI JSON Output)** sẽ sửa lỗi.

##### **🔹 Node 4: Parse AI JSON Output (Code)**
- **Mã JavaScript:**
  ```javascript
  // Chuyển đổi JSON text thành đối tượng JSON
  const jsonText = $input.all()[0].json.text;
  try {
    const parsedJson = JSON.parse(jsonText);
    return {
      json: parsedJson,
      // Trả về các trường cần thiết
      content_angle: parsedJson.content_angle,
      linkedin_post: parsedJson.linkedin_post,
      instagram_caption: parsedJson.instagram_caption,
      instagram_image_prompt: parsedJson.instagram_image_prompt,
      hashtags: parsedJson.hashtags
    };
  } catch (error) {
    return {
      error: "JSON không hợp lệ. Vui lòng kiểm tra prompt OpenAI!"
    };
  }
  ```
- **Lưu ý:** Nếu OpenAI trả về JSON không đúng, **node này sẽ báo lỗi** và workflow dừng lại.

##### **🔹 Node 5: Generate an Image (Google Gemini)**
- **Credentials:** Chọn `googlePalmApi` (đã cấu hình).
- **Resource:** Đặt `image`.
- **Prompt:** Sử dụng `{{ $json.instagram_image_prompt }}` (được tạo bởi OpenAI).
- **Lưu ý:**
  - Nếu Gemini trả về lỗi, **kiểm tra API Key** hoặc **cập nhật prompt** để rõ ràng hơn.
  - Thời gian tạo hình ảnh có thể **lên đến 30 giây**, nên **không nên đặt interval quá ngắn** trong Node 1.

##### **🔹 Node 6: Upload a File (UploadToURL)**
- **Credentials:** Chọn `uploadToUrlApi` (cấu hình với ImgBB/Cloudinary).
- **URL:** Điền URL API của dịch vụ lưu trữ hình ảnh (ví dụ: `https://api.imgbb.com/1/upload`).
- **Headers:**
  ```json
  {
    "Authorization": "Bearer YOUR_API_KEY"
  }
  ```
- **Lưu ý:**
  - Nếu hình ảnh quá lớn, **cần resize** trước khi upload.
  - **URL trả về** sẽ được sử dụng cho Instagram.

##### **🔹 Node 7: Publish LinkedIn Post**
- **Credentials:** Chọn `linkedInOAuth2Api` (cấu hình OAuth 2.0).
- **Tham số cần thiết:**
  - **Content:** `{{ $json.linkedin_post }}`.
  - **Image URL:** `{{ $json.image_url }}` (trả về từ Node 6).
- **Lưu ý:**
  - **Kiểm tra quyền OAuth** (n8n cần quyền đăng bài).
  - Nếu LinkedIn yêu cầu **captcha**, **cần cấu hình thêm** trong `linkedInOAuth2Api`.

##### **🔹 Node 8: Publish Instagram Post**
- **Credentials:** Chọn `instagramApi` (cấu hình với `@mookielianhd/n8n-nodes-instagram`).
- **Tham số cần thiết:**
  - **Image URL:** `{{ $json.image_url }}`.
  - **Caption:** `{{ $json.instagram_caption }}`.
  - **Hashtags:** `{{ $json.hashtags }}`.
- **Lưu ý:**
  - **Instagram Business Account** phải được **kích hoạt API**.
  - Nếu gặp lỗi, **kiểm tra tài khoản** có bị hạn chế không.

---

#### **3. Kích hoạt ⚡️**
1. **Test Run** với một bài viết mẫu:
   - Chọn **Node 1 (Watch RSS Feed)** và **nhấn "Execute"** để kiểm tra.
   - Kiểm tra **các node liên quan** (OpenAI, Gemini, LinkedIn, Instagram) có hoạt động không.
2. **Bật Active workflow** sau khi test thành công.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tăng tính cá nhân hóa:**
   - **Thêm Node Code** trước OpenAI để **đính kèm logo doanh nghiệp** vào prompt:
     ```javascript
     const customPrompt = `Tạo nội dung cho bài viết ${$json.article_title} của ${$input.all()[0].json.company_name}.`;
     return { json: { instruction: customPrompt } };
     ```
2. **Lưu log hoạt động:**
   - **Thêm Node Google Sheets** sau Node 8 để **ghi lại lịch sử đăng bài**.
3. **Gửi báo cáo định kỳ:**
   - **Sử dụng Node Email** (SendGrid/Mailgun) để **gửi báo cáo tuần/Tháng** về số bài đăng.
4. **Tối ưu hình ảnh:**
   - **Thêm Node Image Resize** (n8n-nodes-image) trước UploadToURL để **giảm kích thước** hình ảnh.
5. **Kết hợp với Slack/Telegram:**
   - **Thêm Node Webhook** để **gửi thông báo** khi bài đăng thành công.

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào **strategy marketing** thay vì viết bài và tạo hình ảnh. Với **AI + tự động hóa**, nội dung xã hội của doanh nghiệp sẽ **ngày càng chuyên nghiệp và thu hút hơn**.

**🚀 Hành động ngay:**
1. **Cài đặt n8n trên VPS** (để workflow hoạt động 24/7).
2. **Cấu hình các API Key** (OpenAI, Gemini, LinkedIn, Instagram).
3. **Import workflow** và **test với bài viết mẫu**.
4. **Bật Active** và **nhận nội dung xã hội tự động hóa!**

---
**💡 Cần hỗ trợ?**
- **Trên n8n Community:** [https://community.n8n.io/](https://community.n8n.io/)
- **Tạo issue trên GitHub:** [https://github.com/n8n-io/n8n/issues](https://github.com/n8n-io/n8n/issues)
- **Chat với tôi (AI Automation Specialist)** để **cấu hình chi tiết!** 😊