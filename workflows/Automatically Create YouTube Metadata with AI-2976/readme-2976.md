---
title: "🎬 Tự Động Tạo Metadata YouTube Chuyên Nghiệp Với AI - Giảm Thời Gian Làm Video 90%!"
description: "Workflow này tự động sinh metadata (tiêu đề, mô tả, thẻ) cho video YouTube dựa trên nội dung video và thông tin từ Google Docs, giúp tăng tỷ lệ xem và SEO. Chỉ cần nhập video ID, AI sẽ xử lý toàn bộ - không cần viết tay!"
slug: "tu-dong-tao-metadata-youtube-voi-ai"
tags: [n8n, automation, youtube-seo, ai-chatbot, google-docs, openai]
keywords: [tự động hóa youtube, metadata youtube ai, tăng tỷ lệ xem youtube, seo video youtube, n8n workflow youtube]
---

# 🚀 **Tự Động Tạo Metadata YouTube Chuyên Nghiệp Với AI - Khai Phóng Tiềm Năng Video Của Bạn**

### **💥 Nỗi Đau Của Các Sếp Khi Tạo Metadata YouTube**
Bạn đã bao giờ phải:
- **Viết tiêu đề, mô tả và thẻ** cho hàng chục video mỗi tuần?
- **Lo lắng về SEO** nhưng không biết cách tối ưu?
- **Mất thời gian** tìm từ khóa phù hợp?
- **Đầu tư nhiều công sức** nhưng tỷ lệ xem vẫn thấp?

**Workflow này giải quyết tất cả!** Dựa trên **AI (GPT-4o-mini)** và **Google Docs**, nó tự động sinh metadata **chuyên nghiệp, cá nhân hóa** cho mỗi video của bạn - chỉ với **1 cú nhấp chuột**.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Không cần viết tay metadata cho từng video.
✅ **Tăng tỷ lệ xem**: Metadata được tối ưu SEO, thu hút người xem hiệu quả.
✅ **Cá nhân hóa**: AI phân tích nội dung video để tạo tiêu đề mô tả phù hợp.
✅ **Hoạt động 24/7**: Chỉ cần cài đặt 1 lần, workflow tự động chạy cho tất cả video mới.
✅ **Dễ dàng mở rộng**: Kết hợp với **Slack/Telegram** để thông báo kết quả.
:::

---
### **🔧 Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng, các sếp cần chuẩn bị:
1. **Tài khoản YouTube** (API Key) để cập nhật metadata.
2. **Tài khoản Google Docs** (để lưu trữ thông tin tham khảo về video).
3. **API Key OpenAI** (để sử dụng GPT-4o-mini).
4. **Tài khoản n8n Self-hosted** (để chạy workflow 24/7).
5. **Dữ liệu mẫu** (video ID và thông tin liên quan trong Google Docs).

👉 **🎁 Đăng ký VPS TinoHost** (chỉ 50k/tháng) để self-host n8n:
[🔗 TinoHost](https://tino.vn/vps-n8n?affid=388) (Mã giảm giá: **VPSN8N**)
:::

---
### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/2976](https://n8n.io/workflows/2976) và import vào **n8n Editor**.
- **Cách 2**: Copy toàn bộ JSON từ link trên và **paste** vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **9 node** chính, các sếp cần cấu hình kỹ các node sau:

##### **🔹 Node "On form submission" (formTrigger)**
- **Mục đích**: Khởi động workflow khi có dữ liệu mới (video ID).
- **Cấu hình**:
  - Chọn **Credentials** là tài khoản n8n của bạn.
  - **Form Fields**:
    - `videoId` (text) → Nhập ID video YouTube (ví dụ: `dQw4w9WgXcQ`).
    - `videoInfo` (text) → Nhập thông tin tham khảo từ Google Docs (ví dụ: "Video về cách tự động hóa YouTube").

##### **🔹 Node "syncbricks information" (googleDocsTool)**
- **Mục đích**: Lấy thông tin tham khảo từ Google Docs.
- **Cấu hình**:
  - **Credentials**: Chọn tài khoản Google Docs.
  - **File ID**: ID của file Google Docs chứa thông tin video (đọc từ URL file).
  - **Sheet Name**: Tên sheet chứa dữ liệu (ví dụ: `VideoInfo`).
  - **Operation**: Chọn `get`.

##### **🔹 Node "OpenAI Chat Model" (lmChatOpenAi)**
- **Mục đích**: Sử dụng AI sinh metadata.
- **Cấu hình**:
  - **Credentials**: Nhập **API Key OpenAI**.
  - **Model**: Chọn `gpt-4o-mini` (mặc định).
  - **Prompt**:
    ```plaintext
    Tôi là một nhà tạo nội dung YouTube. Hãy giúp tôi tạo metadata (tiêu đề, mô tả, thẻ) cho video có ID: {{$node["On form submission"].json["videoId"]}}.
    Thông tin tham khảo từ Google Docs: {{$node["syncbricks information"].json["content"]}}.

    Yêu cầu:
    1. Tiêu đề: Phải hấp dẫn, chứa từ khóa SEO.
    2. Mô tả: 2-3 câu ngắn gọn, bao gồm từ khóa và link liên quan.
    3. Thẻ: 5-10 thẻ phù hợp với nội dung video.
    4. Cấu trúc JSON:
    {
      "title": "Tiêu đề YouTube",
      "description": "Mô tả YouTube",
      "tags": ["thẻ1", "thẻ2", ...]
    }
    ```
  - **Temperature**: 0.7 (để kết quả logic hơn).

##### **🔹 Node "Extract Video ID" (set)**
- **Mục đích**: Trích xuất video ID từ dữ liệu đầu vào.
- **Cấu hình**:
  - **Property**: `videoId` (đảm bảo trùng với field trong form).

##### **🔹 Node "Youtube Meta Generator" (agent)**
- **Mục đích**: Sử dụng AI để sinh metadata.
- **Cấu hình**:
  - **Credentials**: Chọn OpenAI (đã cấu hình ở node trước).
  - **Agent Configuration**:
    - **Tool**: Chọn `lmChatOpenAi`.
    - **Output Parser**: Chọn `outputParserStructured` (để AI trả về JSON).

##### **🔹 Node "YouTube" (youTube)**
- **Mục đích**: Cập nhật metadata lên YouTube.
- **Cấu hình**:
  - **Credentials**: Nhập **API Key YouTube**.
  - **Video ID**: Lấy từ `$node["Extract Video ID"].json["videoId"]`.
  - **Snippet**:
    - `title`: `$node["Youtube Meta Generator"].json["title"]`.
    - `description`: `$node["Youtube Meta Generator"].json["description"]`.
    - `tags`: `$node["Youtube Meta Generator"].json["tags"]`.

##### **🔹 Node "Format Tags" (set)**
- **Mục đích**: Đảm bảo thẻ được định dạng đúng cho YouTube.
- **Cấu hình**:
  - **Property**: `tags` (chuyển thành mảng JSON).

##### **🔹 Node "Output Parser" (outputParserStructured)**
- **Mục đích**: Chuyển kết quả AI thành JSON chuẩn.
- **Cấu hình**:
  - **Schema**:
    ```json
    {
      "title": "string",
      "description": "string",
      "tags": ["string"]
    }
    ```

##### **🔹 Node "Form" (form)**
- **Mục đích**: Hiển thị kết quả cuối cùng.
- **Cấu hình**:
  - **Fields**:
    - `title` (text).
    - `description` (textarea).
    - `tags` (multi-select).

---
#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhập **video ID** và **thông tin tham khảo** vào form.
   - Chạy workflow để kiểm tra kết quả.
2. **Bật Active**:
   - Sau khi kiểm tra thành công, **bật workflow** để tự động chạy khi có dữ liệu mới.

---
### **✍️ Mẹo & Gợi Ý Nâng Cao**
:::info[CÁCH LÀM HƠN]
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram** để thông báo metadata mới.
   - Ví dụ: `{{$node["Youtube Meta Generator"].json["title"]}} đã được tạo thành công!`.

2. **Lưu log vào Google Sheets**:
   - Thêm node **Google Sheets** để ghi lại lịch sử metadata.
   - Dữ liệu: `videoId`, `title`, `date`.

3. **Tối ưu prompt cho AI**:
   - Nếu metadata không phù hợp, cập nhật **prompt** trong node `OpenAI Chat Model` để AI hiểu rõ hơn về nội dung video của bạn.

4. **Sử dụng nhiều mẫu prompt**:
   - Tạo **bộ prompt khác nhau** cho từng loại video (ví dụ: tutorial, review, vlog).
   - Sử dụng node **Set** để chọn prompt phù hợp.

5. **Tự động hóa cho nhiều video**:
   - Sử dụng **webhook** để nhận dữ liệu từ **Google Drive** hoặc **Excel** khi có video mới.
:::

---
### **📌 Kết Luận**
Workflow này **giải phóng thời gian** của các sếp để tập trung vào **nội dung chất lượng** thay vì việc viết metadata. Với **AI + SEO tự động**, video của bạn sẽ **xuất hiện cao hơn trên YouTube**, thu hút nhiều người xem hơn.

**🚀 Hãy thử ngay!**
1. **Import workflow** vào n8n.
2. **Cấu hình API keys** và **Google Docs**.
3. **Nhập video ID** và **chạy thử**.
4. **Bật workflow** để tự động hóa!

**Nếu workflow này hữu ích, hãy ủng hộ tác giả Amjid Ali qua [PayPal](http://paypal.me/pmptraining) để hỗ trợ phát triển thêm các template tự động hóa!**

---
**🔗 Tài liệu tham khảo:**
- [n8n Workflow gốc](https://n8n.io/workflows/2976)
- [Tutorial Google Docs API](https://developers.google.com/docs/api)
- [Tutorial YouTube API](https://developers.google.com/youtube/v3)