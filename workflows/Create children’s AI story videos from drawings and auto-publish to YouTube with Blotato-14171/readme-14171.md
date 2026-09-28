---
title: "🎨 Tự Động Hoá Tạo Video Truyện AI Từ Vẽ T Tay → Đăng Trực Tiếp YouTube Với Blotato (N8N)"
description: "Workflow n8n tiên tiến giúp các sếp tự động chuyển đổi những bức vẽ tay của trẻ em thành video truyện AI hoàn chỉnh, với nhân vật, cảnh quay và âm thanh tự động sinh thành, sau đó đăng tải lên YouTube chỉ trong vài phút. Giảm thời gian sản xuất từ hàng giờ xuống còn vài giây!"
slug: "tay-dong-hoa-tao-video-truyen-ai-tu-ve-tay-den-youtube"
tags: [n8n, automation, content-creation, ai-multimodal, youtube-automation, blotato, cloudinary, anthropic]
keywords: [n8n workflow tự động hóa, tạo video truyện AI từ vẽ tay, đăng tải tự động YouTube, tự động hóa nội dung trẻ em, AI multimodal, Blotato API, Claude AI, AtlasCloud]
---

# 🚀 **Tự Động Hoá Tạo Video Truyện AI Từ Vẽ Tay → Đăng Trực Tiếp YouTube Với Blotato**

## 📌 **Giải Pháp Cho Những Ai...**
- Mệt mỏi với việc phải viết kịch bản, vẽ nhân vật và chắp bút video truyện cho trẻ em?
- Muốn tạo nội dung sáng tạo nhưng không có thời gian hoặc kỹ năng kỹ thuật?
- Đang tìm cách tối ưu hóa quy trình sản xuất video truyện để tiết kiệm chi phí và thời gian?

Workflow này là **công cụ thần tiên** cho các sếp, nhà giáo dục, hoặc người làm nội dung trẻ em. Chỉ cần **1 bức vẽ tay**, hệ thống sẽ tự động:
✅ **Phân tích** bức vẽ và tạo **nhân vật 3D** với tính cách phù hợp
✅ **Tạo kịch bản** truyện ngắn độc đáo dựa trên hình ảnh
✅ **Sinh cảnh quay** với nhân vật và bối cảnh phù hợp
✅ **Tạo video** với hiệu ứng động ảnh và âm thanh AI
✅ **Đăng tải tự động** lên YouTube với mô tả và thumbnail tự động sinh thành

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tốc độ và tính riêng tư.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ **hàng giờ** viết kịch bản và vẽ nhân vật xuống còn **vài phút**.
- **Chất lượng chuyên nghiệp**: Video với **nhân vật 3D**, **cảnh quay động**, và **âm thanh AI** tự động sinh thành.
- **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công ở bất kỳ bước nào.
- **Tăng cường tương tác**: Nội dung độc đáo, phù hợp với trẻ em, giúp tăng **lượt xem và tương tác** trên YouTube.
- **Tối ưu chi phí**: Không cần thuê nhà thiết kế hoặc biên kịch.
:::

---

## 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
### **1. Tài Khoản & API Keys**
| Dịch vụ               | Mô tả                                                                 | Link Đăng Ký                                                                 |
|-----------------------|-------------------------------------------------------------------------|------------------------------------------------------------------------------|
| **Blotato**           | Đăng tải video lên YouTube/TikTok tự động.                              | [blotato.com](https://blotato.com/?ref=firas)                                |
| **AtlasCloud (Kling)**| Tạo video động ảnh từ kịch bản.                                        | [atlascloud.ai](https://www.atlascloud.ai?ref=8QKPJE)                       |
| **Anthropic (Claude)**| AI viết kịch bản và tạo prompt cho nhân vật.                          | [anthropic.com](https://www.anthropic.com/)                                 |
| **ElevenLabs**        | Tạo âm thanh AI cho video.                                              | [elevenlabs.io](https://elevenlabs.io/)                                      |
| **Shotstack**         | Ghép video và hiệu ứng cuối cùng.                                      | [shotstack.com](https://www.shotstack.com/)                                  |
| **Nano Banana**       | Tạo hình ảnh nhân vật từ mô tả.                                        | [nanobanana.ai](https://nanobanana.ai/)                                      |
| **Cloudinary**        | Lưu trữ và quản lý file hình ảnh/video.                                | [cloudinary.com](https://cloudinary.com/)                                    |
| **Google Gemini**      | Phân tích hình ảnh và tạo mô tả nhân vật.                              | [gemini.google.com](https://gemini.google.com/)                              |

### **2. Cấu Hình N8N**
- **N8N phiên bản mới nhất** (để hỗ trợ các node mới như `chainLlm`, `outputParserStructured`).
- **3 Workflow riêng biệt** (Part 1, Part 2, Part 3) cần được **import và kết nối** qua webhook.

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Workflow này được chia thành **3 phần**, các sếp cần import từng phần vào **3 workflow riêng biệt** trong n8n:
1. **Part 1**: Từ vẽ tay → Nhân vật & Kịch bản
2. **Part 2**: Từ nhân vật → Cảnh quay
3. **Part 3**: Từ cảnh quay → Video hoàn chỉnh → Đăng YouTube

**Cách import**:
- Tải file JSON từ [liên kết gốc](https://n8n.io/workflows/14171) hoặc copy/paste JSON vào **n8n Editor**.
- Chọn **Import Workflow** và chọn file JSON tương ứng với từng phần.

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
#### **A. Cấu Hình Credentials**
Các sếp cần **đăng ký và cấu hình** các API keys trong n8n:
- **Blotato API**: Thêm vào `blotatoApi` với `Client ID` và `Client Secret`.
- **Cloudinary API**: Thêm vào `cloudinaryApi` với `API Key` và `API Secret`.
- **Anthropic API**: Thêm vào `anthropicApi` với `API Key`.
- **Google Gemini API**: Thêm vào `googlePalmApi` với `API Key`.

#### **B. Cấu Hình Webhook**
- **Part 1** sử dụng webhook với `path: 87f99887-37fa-432a-ba5b-fd8043373e64`.
- **Part 2** và **Part 3** sử dụng webhook khác (`abbcaa45-a01a-4e75-bcac-e2734a9bb489`).
- **Kết nối giữa các phần**:
  - Sau khi **Part 1** hoàn thành, nó sẽ gọi **Part 2** qua webhook.
  - Sau khi **Part 2** hoàn thành, nó sẽ gọi **Part 3** qua webhook.

#### **C. Cấu Hình Form Trigger (Bước Khởi Động)**
- Tạo một **form trigger** trong **Part 1** với trường upload file để người dùng **nộp bức vẽ tay**.
- Ví dụ:
  ```json
  {
    "name": "On form submission",
    "type": "formTrigger",
    "credentials": [],
    "keyParameters": {
      "fields": [
        {
          "name": "drawing",
          "type": "file",
          "label": "Upload your child's drawing"
        }
      ]
    }
  }
  ```

#### **D. Cấu Hình Node Quan Trọng**
| Node                          | Cần Chỉnh Gì?                                                                 | Ví Dụ Tham Khảo                                                                 |
|-------------------------------|--------------------------------------------------------------------------------|----------------------------------------------------------------------------------|
| **Google Gemini (Analyze)**   | Điền `googlePalmApi` và chọn `operation: analyze`.                            | `resource: image`, `image: $node["Extract from File"].json()`                   |
| **Anthropic Chat Model**      | Chọn model `claude-sonnet-4-5-20250929`.                                      | `prompt: $json["Build Story Context"].json()`                                   |
| **Cloudinary Upload**         | Điền `cloudinaryApi` và chọn `operation: uploadFile`.                          | `file: $node["Scene Image to File"].json()`                                     |
| **AtlasCloud Generate Video** | Điền URL video từ **Part 2** và cấu hình prompt.                             | `payload: $json["Build Kling Payloads"].json()`                                |
| **Blotato (YouTube)**        | Chọn `blotatoApi` và cấu hình tiêu đề, mô tả, thumbnail tự động.           | `title: "AI Story Video from Drawing"`, `description: $json["Generate Story"].json()` |

#### **E. Cấu Hình Node `chainLlm`**
- Các node này sử dụng **Anthropic Claude** để tạo kịch bản và prompt.
- Ví dụ:
  ```json
  {
    "name": "Generate Story",
    "type": "chainLlm",
    "credentials": ["anthropicApi"],
    "keyParameters": {
      "model": "claude-sonnet-4-5-20250929",
      "prompt": "$json['Build Story Context'].story_prompt"
    }
  }
  ```

---

### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Nộp một **bức vẽ tay mẫu** (ví dụ: một con vật hoặc nhân vật hư cấu).
   - Theo dõi quá trình trong **n8n Dashboard** để kiểm tra lỗi.
2. **Bật Active**:
   - Sau khi kiểm tra thành công, **bật Active** cho 3 workflow.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
### **1. Tối Ưu Hóa Cho Trẻ Em**
- **Thêm trường nhập tên nhân vật** trong form trigger để tạo **câu chuyện cá nhân hóa**.
- **Sử dụng template kịch bản** cho các chủ đề phổ biến (ví dụ: "Câu chuyện về một chú mèo đi du lịch").

### **2. Tích Hợp Slack/Telegram**
- Thêm node **Slack/Telegram** để thông báo kết quả khi video hoàn thành:
  ```json
  {
    "name": "Notify on Completion",
    "type": "httpRequest",
    "keyParameters": {
      "method": "POST",
      "url": "https://api.telegram.org/bot<BOT_TOKEN>/sendMessage",
      "body": {
        "chat_id": "<CHAT_ID>",
        "text": "Video đã hoàn thành! Link: $json['Youtube'].json()"
      }
    }
  }
  ```

### **3. Lưu Log & Báo Cáo**
- Thêm node **Google Sheets** để lưu **log hoạt động** và **thống kê**:
  ```json
  {
    "name": "Log to Google Sheets",
    "type": "googleSheets",
    "credentials": ["googleSheetsApi"],
    "keyParameters": {
      "sheetName": "Video_Logs",
      "data": {
        "Drawing": "$node['On form submission'].json()['drawing']",
        "Video_URL": "$json['Youtube'].json()['url']",
        "Status": "Success"
      }
    }
  }
  ```

### **4. Tự Động Chia Sẻ trên Mạng Xã Hội**
- Sau khi đăng YouTube, tự động chia sẻ lên **Facebook/Instagram** bằng API:
  ```json
  {
    "name": "Share on Facebook",
    "type": "httpRequest",
    "keyParameters": {
      "method": "POST",
      "url": "https://graph.facebook.com/v18.0/me/feed",
      "body": {
        "access_token": "<FACEBOOK_ACCESS_TOKEN>",
        "message": "Xem video truyện AI mới từ bức vẽ tay của trẻ: $json['Youtube'].json()['url']"
      }
    }
  }
  ```

---

## 📌 **Kết Luận**
Workflow này không chỉ **giảm thiểu thời gian** mà còn **mở ra thế giới mới** cho nội dung sáng tạo với trẻ em. Các sếp có thể:
✔ **Tạo video truyện nhanh chóng** từ những bức vẽ tay đơn giản.
✔ **Tăng cường tương tác** với khán giả trẻ thông qua nội dung cá nhân hóa.
✔ **Tự động hóa toàn bộ quy trình** từ vẽ tay đến đăng tải YouTube.

**Hãy bắt đầu ngay hôm nay!**
1. **Import 3 workflow** và cấu hình API.
2. **Test với một bức vẽ mẫu**.
3. **Bật hoạt động và bắt đầu tạo nội dung AI!**

---
**🚀 Cần hỗ trợ thêm?** Liên hệ với **Dr. Firas** (tác giả workflow) qua [liên kết](https://n8n.io/workflows/14171) để truy cập **khóa học chi tiết** về tự động hóa với n8n!