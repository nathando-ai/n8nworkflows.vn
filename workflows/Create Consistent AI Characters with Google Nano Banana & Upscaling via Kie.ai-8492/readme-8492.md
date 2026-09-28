---
title: "🎨 Tự Động Hóa Tạo Nhân Vật AI Đa Dạng & Nâng Cao Chất Lượng Hình Ảnh với Google Nano Banana & Kie.ai (N8N)"
description: "Workflow tự động hóa 100% không code giúp các sếp tạo nhân vật AI độc đáo, tự động hóa quá trình viết story, sinh hình ảnh và nâng cấp chất lượng hình ảnh lên 4K/8K chỉ với 1 cú nhấp chuột. Giảm thời gian làm việc xuống 90% so với thủ công!"
slug: "tự-dộng-hoa-tao-nhan-vat-ai-google-nano-banana-kie-ai"
tags: [n8n, automation, ai-character-generation, upscaling, google-nanobanana, kie-ai, google-sheets, google-drive]
keywords: [n8n workflow tự động hóa nhân vật AI, tạo nhân vật AI với Google Nano Banana, nâng cấp hình ảnh AI lên 4K/8K, tự động hóa viết story và sinh hình, n8n AI automation, workflow AI không code]
---

# 🚀 **Tự Động Hóa Tạo Nhân Vật AI Đa Dạng & Nâng Cao Chất Lượng Hình Ảnh với Google Nano Banana & Kie.ai**

### **Giải pháp hoàn hảo cho các sếp viết truyện, game dev, content creator và nhà thiết kế muốn:**
- **Tạo nhân vật AI độc đáo** với tính cách, ngoại hình và câu chuyện riêng biệt chỉ bằng một lệnh.
- **Sinh hình ảnh AI chất lượng cao** từ mô tả văn bản (text-to-image) với Google Nano Banana.
- **Nâng cấp hình ảnh lên 4K/8K** bằng công nghệ upscaling tiên tiến của Kie.ai.
- **Tự động hóa toàn bộ quy trình** từ viết story đến xuất file, **không cần code** và hoạt động 24/7.
- **Lưu trữ và quản lý** tất cả nhân vật và hình ảnh trong Google Drive & Google Sheets, dễ dàng theo dõi tiến trình.

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian lên đến 90%** so với viết story và sinh hình thủ công.
✅ **Nhân vật AI cá nhân hóa** với tính cách, lối nói và câu chuyện riêng biệt.
✅ **Hình ảnh chất lượng cao** (4K/8K) phù hợp cho game, truyện tranh, hoặc nội dung marketing.
✅ **Quản lý dễ dàng** với Google Sheets theo dõi trạng thái của mỗi nhân vật.
✅ **Hoạt động tự động** mà không cần can thiệp thủ công.
✅ **Mở rộng dễ dàng** để tích hợp với Slack, Telegram hoặc gửi báo cáo định kỳ.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google** (để kết nối với Google Drive & Google Sheets).
2. **API Key OpenAI** (để sử dụng mô hình GPT-4.1-mini trong Story Creator Agent).
3. **Tài khoản Kie.ai** (để upscale hình ảnh lên 4K/8K).
4. **Tài khoản Google Nano Banana** (để sinh hình ảnh từ mô tả văn bản).
5. **Bảng Google Sheets** để lưu trạng thái của các nhân vật và hình ảnh.
6. **Google Drive** để lưu trữ hình ảnh và tổ chức theo folder.
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Bước 1:** Tải workflow từ [đây](https://n8n.io/workflows/8492) (hoặc copy JSON từ trang này).
- **Bước 2:** Mở **n8n Editor** và nhấn **"Import"** → Dán JSON hoặc tải file JSON.
- **Bước 3:** Chọn **"Create Workflow"** và đặt tên (ví dụ: **"AI Character Creator"**).

---
### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **4 phần chính**: **Tạo Folder & File**, **Viết Story**, **Sinh Hình Ảnh**, và **Nâng Cao Chất Lượng Hình Ảnh**. Dưới đây là hướng dẫn chi tiết để cấu hình:

#### **📌 Phần 1: Cấu hình Google Drive & Google Sheets**
1. **Thiết lập OAuth2 cho Google Drive & Sheets**:
   - Trong **n8n**, đi đến **"Credentials"** → **"Add"** → Chọn **"Google Drive OAuth2"** và **"Google Sheets OAuth2"**.
   - Theo hướng dẫn để kết nối tài khoản Google.
   - **Lưu ý:** Các sếp cần cấp quyền **"Drive API"** và **"Sheets API"** cho ứng dụng n8n.

2. **Tạo Bảng Google Sheets**:
   - Tạo một bảng mới với **cột**: `TaskId`, `Story`, `ImageUrl`, `Status`, `UpscaledImageUrl`.
   - **Lưu ý:** Cột `TaskId` sẽ được tự động sinh ra để theo dõi tiến trình.

3. **Tạo Folder trong Google Drive**:
   - Workflow sẽ tự động tạo một folder mới để lưu trữ hình ảnh.
   - **Lưu ý:** Đặt tên folder theo định dạng: `"AI_Characters_[Date]"` (ví dụ: `"AI_Characters_2024-05-20"`).

---
#### **📌 Phần 2: Cấu hình OpenAI & Kie.ai**
1. **Thiết lập API Key OpenAI**:
   - Trong **"Credentials"**, thêm **"OpenAI API"** và dán **API Key** từ tài khoản OpenAI.
   - **Model mặc định**: `gpt-4.1-mini` (được sử dụng trong **Story Creator Agent**).

2. **Thiết lập API Key Kie.ai**:
   - Trong node **"Upscale Image"**, thêm **API Key** của Kie.ai (nếu không có, đăng ký tại [Kie.ai](https://kie.ai/)).
   - **Lưu ý:** Node này sẽ gọi API của Kie.ai để nâng cấp hình ảnh.

---
#### **📌 Phần 3: Cấu hình Google Nano Banana**
1. **Thiết lập API Key Nano Banana**:
   - Trong node **"Create Image"**, thêm **API Key** của Google Nano Banana (nếu không có, đăng ký tại [Nano Banana](https://nanobanana.com/)).
   - **Lưu ý:** Node này sẽ sinh hình ảnh từ mô tả văn bản (story) được tạo bởi AI.

---
#### **📌 Phần 4: Cấu hình các Node quan trọng**
| **Node**               | **Cấu hình cần chú ý**                                                                 | **Ghi chú**                                                                 |
|------------------------|---------------------------------------------------------------------------------------|-----------------------------------------------------------------------------|
| **Manual Trigger**     | Nhấn **"Execute workflow"** để bắt đầu.                                             | Đây là nút khởi động thủ công.                                            |
| **Story Creator Agent**| Sử dụng mô hình **GPT-4.1-mini** để tạo story dựa trên input từ người dùng.          | Các sếp có thể chỉnh sửa **prompt** trong node này để điều chỉnh tính cách nhân vật. |
| **OpenAI Chat Model**  | Đảm bảo **API Key OpenAI** được điền chính xác.                                     | Nếu gặp lỗi, kiểm tra lại **credentials**.                                |
| **Upscale Image**      | Chọn **API Key Kie.ai** và đảm bảo **input** là URL hình ảnh từ Nano Banana.        | Node này sẽ gọi API Kie.ai để nâng cấp hình ảnh.                          |
| **Google Sheets**      | Chọn **credentials** là **"googleSheetsOAuth2Api"** và chỉ định **Sheet Name**.         | Workflow sẽ cập nhật trạng thái (`Status`) của mỗi nhân vật.               |
| **Google Drive**       | Chọn **credentials** là **"googleDriveOAuth2Api"** và chỉ định **folder** để lưu hình ảnh. | Hình ảnh sẽ được upload vào folder tự động tạo.                          |

---
### **3. Kích hoạt ⚡️**
1. **Test Run với dữ liệu mẫu**:
   - Nhấn **"Execute workflow"** và nhập **input** như:
     ```json
     {
       "characterName": "DragonSlayer",
       "characterDescription": "A brave knight with a golden sword and a dragon tattoo on his arm. He fights against dark magic.",
       "storyPrompt": "Write a short fantasy story about this knight and his journey to defeat the evil sorcerer."
     }
     ```
   - Workflow sẽ:
     - Tạo **story** bằng AI.
     - Sinh **hình ảnh** từ mô tả.
     - **Nâng cấp** hình ảnh lên 4K/8K.
     - **Upload** vào Google Drive.
     - **Cập nhật** trạng thái trong Google Sheets.

2. **Bật Active workflow**:
   - Sau khi test thành công, chuyển **Active** sang **"ON"**.

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Tích hợp với Slack/Telegram**:
   - Sử dụng node **Slack** hoặc **Telegram Bot** để thông báo kết quả khi workflow hoàn thành.
   - Ví dụ: Gửi tin nhắn như: *"✅ Nhân vật **DragonSlayer** đã được tạo thành công! Hình ảnh đã được nâng cấp và lưu tại: [Link]."*

2. **Lưu log hoạt động**:
   - Sử dụng node **Set** hoặc **Code** để lưu **log** của workflow vào Google Sheets hoặc một file JSON.
   - Có thể thêm cột `Log` vào bảng Google Sheets để theo dõi lỗi hoặc tiến trình.

3. **Tự động hóa gửi báo cáo định kỳ**:
   - Sử dụng **n8n Scheduler** để chạy workflow hàng ngày và gửi báo cáo tổng hợp về số lượng nhân vật tạo ra.
   - Ví dụ: Gửi email hoặc Slack notification hàng tuần với thống kê.

4. **Chỉnh sửa prompt cho Story Creator**:
   - Mở node **Story Creator Agent** và chỉnh sửa **prompt** để tạo story phù hợp với thể loại (fantasy, sci-fi, romance...).
   - Ví dụ:
     ```json
     "prompt": "Tạo một câu chuyện ngắn về nhân vật {characterName} với phong cách {style}. Nhân vật phải có tính cách {characterDescription}. Kết thúc câu chuyện với một câu nói động viên."
     ```

5. **Sử dụng biến môi trường (Environment Variables)**:
   - Để bảo mật, các sếp có thể lưu **API Key** trong **Environment Variables** thay vì trong credentials.
   - Hướng dẫn: Trong **n8n**, đi đến **"Settings"** → **"Environment Variables"** và thêm:
     ```json
     {
       "OPENAI_API_KEY": "sk-...",
       "KIE_AI_API_KEY": "abc123...",
       "NANO_BANANA_API_KEY": "xyz789..."
     }
     ```
   - Sau đó, trong các node, thay vì chọn **credentials**, các sếp chỉ cần điền tên biến môi trường (ví dụ: `{{$env.OPENAI_API_KEY}}`).

---
## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa quá trình tạo nhân vật AI, viết story và nâng cấp hình ảnh **không cần code**. Với **Google Nano Banana** và **Kie.ai**, các sếp có thể tạo ra **nhân vật độc đáo** với hình ảnh chất lượng cao, tiết kiệm thời gian và công sức so với cách làm thủ công.

:::success[💡 **Áp dụng ngay hôm nay!**]
- **Import workflow** và bắt đầu tạo nhân vật AI của riêng mình.
- **Chỉnh sửa prompt** để phù hợp với thể loại nội dung của các sếp.
- **Tích hợp với Slack/Telegram** để theo dõi tiến trình thực thời.
- **Mở rộng** workflow để tự động hóa thêm các tác vụ khác như gửi email báo cáo hoặc lưu log.

**Nếu gặp khó khăn**, các sếp có thể liên hệ với tác giả **Muhammad Farooq Iqbal** qua:
📧 **Email**: [mfarooqiqbal143@gmail.com](mailto:mfarooqiqbal143@gmail.com)
📱 **Phone**: +923036991118
💼 **LinkedIn**: [Connect here](https://linkedin.com/in/muhammadfarooqiqbal)
🌐 **Portfolio**: [View his work](https://mfarooqone.github.io/n8n/)

**Chúc các sếp thành công với tự động hóa AI!** 🚀
:::

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::