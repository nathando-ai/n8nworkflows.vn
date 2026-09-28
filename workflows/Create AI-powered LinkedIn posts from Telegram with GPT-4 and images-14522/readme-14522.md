---
title: "🚀 Tự Động Hóa Tạo Bài Đăng LinkedIn AI-Powered Từ Telegram (Với GPT-4 & Hình Ảnh)"
description: "Workflow này giúp các sếp tự động hóa quá trình viết bài LinkedIn chuyên nghiệp chỉ bằng cách trò chuyện trên Telegram, với AI tạo nội dung, hình ảnh và đăng trực tiếp—tất cả từ điện thoại. Tiết kiệm thời gian lên đến 80% so với viết thủ công."
slug: "tieu-dong-hoa-tao-bai-dang-linkedin-ai-telegram"
tags: [n8n, automation, content-creation, ai-chatbot, linkedin-automation, telegram-bot, gpt-4, self-hosted]
keywords: [n8n workflow linkedin, tự động hóa bài đăng linkedin, tạo bài viết ai từ telegram, gpt-4 viết bài, tự động hóa nội dung social media, chatbot linkedin]
---

# 🚀 **Tự Động Hóa Tạo Bài Đăng LinkedIn AI-Powered Từ Telegram (Với GPT-4 & Hình Ảnh)**

## **🔥 Nỗi Đau Của Các Sếp Và Giải Pháp AI**
Các sếp thường phải mất **giờ đồng hồ** để viết bài LinkedIn chuyên nghiệp, nghiên cứu chủ đề, viết lách, tạo hình ảnh và cuối cùng đăng tải. Kết quả là:
✅ **Thời gian quý giá bị "chôn vùi"** trong quá trình viết thủ công.
✅ **Nội dung không nhất quán** vì mỗi bài viết đều khác nhau.
✅ **Khó theo kịp xu hướng** do thiếu thời gian nghiên cứu.
✅ **Hình ảnh không chuyên nghiệp** vì phải tìm kiếm hoặc tạo thủ công.

**Workflow này giải quyết tất cả!** Chỉ cần **gửi tin nhắn cho bot Telegram** với chủ đề bạn muốn, AI sẽ:
✔ **Viết bài LinkedIn chuyên nghiệp** với GPT-4 (tương đương với một nhà văn chuyên nghiệp).
✔ **Tạo hình ảnh đẹp** bằng DALL-E 3 (không cần kỹ năng thiết kế).
✔ **Xem trước và chỉnh sửa** qua Telegram trước khi đăng.
✔ **Đăng tự động lên LinkedIn** chỉ với một lệnh "approve".

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** so với viết thủ công.
- **Nội dung chuyên nghiệp, cá nhân hóa** cho từng bài viết.
- **Hình ảnh chuyên nghiệp** không cần thiết kế.
- **Hoạt động 24/7** mà không cần can thiệp thủ công.
- **Tối ưu hóa SEO** nhờ AI phân tích chủ đề.
- **Dễ dàng chỉnh sửa** qua Telegram trước khi đăng.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản Telegram Bot**:
   - Tạo bot trên [@BotFather](https://t.me/BotFather) bằng lệnh `/newbot`.
   - Lưu **API Token** của bot (sẽ dùng để kết nối với n8n).
2. **Tài khoản LinkedIn**:
   - Cài đặt **OAuth 2.0** cho LinkedIn (n8n sẽ tự động tạo client ID/secret).
3. **Tài khoản OpenAI (GPT-4 + DALL-E 3)**:
   - Mua **gói API** (từ $20/tháng) và lấy **API Key**.
4. **VPS Self-Hosted n8n** (khuyến nghị):
   - Để workflow hoạt động **24/7** mà không bị gián đoạn.
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).
5. **Thiết bị kết nối Internet** (điện thoại hoặc máy tính để trò chuyện với bot).
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/14522](https://n8n.io/workflows/14522).
- Trong **n8n Editor**, chọn **Import** → Chọn file JSON → Nhấn **Import**.
- **Hoặc** copy toàn bộ JSON từ file và dán vào **Import Workflow** trong n8n.

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này **phức tạp** vì kết hợp **AI, Telegram, LinkedIn và DALL-E 3**. Dưới đây là **các bước cấu hình quan trọng**:

#### **🔹 Cấu Hình Credentials (Tài Khoản)**
| **Node**               | **Credentials Cần Thiết**       | **Lưu Ý** |
|------------------------|----------------------------------|-----------|
| **Telegram Trigger**   | `telegramApi` (API Token bot)    | Điền token bot từ @BotFather. |
| **OpenAI Chat Model**  | `openAiApi` (API Key OpenAI)     | Chọn mô hình **GPT-4** trong `keyParameters`. |
| **Generate AI Image**  | `openAiApi` (API Key OpenAI)     | Đảm bảo tài khoản có đủ **credit DALL-E 3**. |
| **LinkedIn Post**      | `linkedInOAuth2Api`               | Cần **OAuth 2.0** từ LinkedIn Developer. |
| **Daily Cleanup**      | Không cần credentials          | Chỉ cần cấu hình thời gian (mặc định: 2 AM hàng ngày). |

#### **🔹 Cấu Hình Node Quan Trọng**
1. **`LinkedIn Post Generator` (Agent)**
   - **System Message**: Sửa để thay đổi **tôn chỉ viết bài** (ví dụ: chuyên nghiệp, thân thiện, marketing).
   - **Example**:
     ```json
     "systemMessage": "You are an expert LinkedIn content writer. Write engaging, professional posts in Vietnamese about {topic}. Keep it under 500 words."
     ```

2. **`OpenAI Chat Model` (GPT-4)**
   - Đảm bảo **mô hình được chọn là GPT-4** (không phải GPT-3.5).
   - **Temperature**: Đặt từ **0.7-0.9** để tránh nội dung quá ngẫu nhiên.

3. **`Create Image Prompt` (Agent)**
   - **System Message**: Sửa để **tối ưu hóa hình ảnh** cho chủ đề.
   - **Example**:
     ```json
     "systemMessage": "Generate a high-quality image prompt for LinkedIn posts. The image should be professional, visually appealing, and related to {topic}. Use detailed descriptions for DALL-E 3."
     ```

4. **`Switch` Nodes (Route Logic)**
   - **`Check Image Status`** và **`Check Image Approval Result`** cần **định nghĩa rõ ràng** các trường hợp:
     - **Image approved** → Tiến hành đăng bài.
     - **Image rejected** → Gửi thông báo lỗi và dừng quá trình.
     - **User cancel** → Xóa dữ liệu và reset session.

5. **`Daily Cleanup Schedule`**
   - **Thời gian mặc định**: 2 AM hàng ngày.
   - **Thời gian giữ draft**: **48 giờ** (cần chỉnh trong node `Clean Abandoned Drafts`).

#### **🔹 Cấu Hình Telegram Bot**
- **Cài đặt Bot**:
  - Bot phải **được thêm vào nhóm** (nếu muốn sử dụng nhóm).
  - **Cấu hình quyền**: Bot cần quyền **sendMessage** và **sendPhoto**.
- **Commands Cần Test**:
  | **Lệnh**       | **Hành Động**                          |
  |----------------|----------------------------------------|
  | `/start`       | Khởi động bot và hiển thị hướng dẫn. |
  | `Tên chủ đề`  | Ví dụ: "Viết bài về AI trong y tế".    |
  | `approve`      | Xác nhận đăng bài.                    |
  | `approve image`| Xác nhận hình ảnh.                   |
  | `cancel`       | Huỷ và xóa draft.                     |
  | `revise`       | Yêu cầu AI chỉnh sửa bài.             |

---

### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run với Dữ Liệu Mẫu**:
   - Gửi tin nhắn cho bot với **chủ đề mẫu** (ví dụ: "Tác động của AI đến ngành marketing").
   - Kiểm tra:
     - AI có viết bài không?
     - Hình ảnh có được tạo không?
     - Bot có phản hồi xác nhận không?
2. **Bật Active Workflow**:
   - Trong n8n Editor, chuyển **Active** sang **ON**.
   - **Kiểm tra log** để đảm bảo không có lỗi.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**

### **1. Tối Ưu Hóa AI Cho Phù Hợp Với Brand**
- **Chỉnh sửa `systemMessage`** trong node `LinkedIn Post Generator` để phù hợp với **tôn chỉ viết bài** của công ty.
  - **Ví dụ**:
    ```json
    "systemMessage": "You are a content writer for [Tên Công Ty]. Write posts that align with our brand voice: professional, data-driven, and engaging. Always include a call-to-action (CTA)."
    ```

### **2. Tự Động Lưu Log & Báo Cáo**
- **Thêm node `Set`** sau `Create a post` để lưu **thông tin bài đăng** (tiêu đề, ngày đăng, link) vào **Google Sheets** hoặc **Notion**.
- **Example**:
  ```json
  {
    "name": "Save Post Metadata",
    "type": "set",
    "credentials": ["googleSheetsApi"],
    "keyParameters": {
      "sheetName": "LinkedIn_Posts",
      "row": {
        "Title": "={{ $json.output.title }}",
        "Date": "={{ $json.output.date }}",
        "Link": "={{ $json.output.link }}"
      }
    }
  }
  ```

### **3. Kết Nối Với Slack/Telegram Của Công Ty**
- Thay vì chỉ gửi thông báo qua Telegram cá nhân, **cấu hình node `telegram`** để gửi đến **channel Slack** hoặc **nhóm Telegram công ty**.
- **Example**:
  ```json
  {
    "name": "Notify Slack Channel",
    "type": "slack",
    "credentials": ["slackApi"],
    "keyParameters": {
      "channel": "#linkedin-posts",
      "text": "New LinkedIn post approved: {{ $json.output.title }}"
    }
  }
  ```

### **4. Tự Động Xóa Draft Sau Thời Gian**
- **Chỉnh sửa node `Daily Cleanup Schedule`** để **xóa draft sau 24h** thay vì 48h.
- **Example**:
  ```json
  {
    "name": "Daily Cleanup Schedule",
    "type": "scheduleTrigger",
    "keyParameters": {
      "cron": "0 0 * * *", // 00:00 hàng ngày
      "timezone": "Asia/Ho Chi Minh"
    }
  }
  ```

### **5. Thêm Hệ Thống Phân Loại Intent Tự Động**
- **Cải tiến node `AI Intent Classifier`** để **nhận diện chủ đề** từ tin nhắn người dùng.
- **Example**:
  ```json
  {
    "name": "AI Intent Classifier",
    "type": "agent",
    "systemMessage": "Classify user intent into one of these categories: [new_post, image_request, approve, revise, cancel]. Return only the intent as JSON."
  }
  ```

---

## 📌 **Kết Luận: Bắt Đầu Tự Động Hóa Ngay!**

Workflow này **giải phóng thời gian** cho các sếp để tập trung vào **strategy** thay vì viết bài. Với **AI GPT-4 + DALL-E 3**, nội dung và hình ảnh sẽ **luôn chuyên nghiệp**, trong khi **quá trình đăng bài chỉ mất vài giây**.

### **🔥 Bước Đầu Tiên:**
1. **Cài đặt VPS** (nếu chưa có) và **cấu hình n8n**.
2. **Import workflow** và **điền credentials**.
3. **Test với chủ đề mẫu** và **chỉnh sửa system messages** phù hợp.
4. **Bật Active** và **đăng bài đầu tiên**!

**🚀 Hãy thử ngay và xem AI làm việc như thế nào!** Nếu có vấn đề, **hãy comment bên dưới** hoặc liên hệ với cộng đồng n8n để hỗ trợ.

---
**💡 Mẹo cuối:** Nếu muốn **tăng tốc độ**, các sếp có thể **mua gói API OpenAI cao cấp** để giảm thời gian chờ AI xử lý.