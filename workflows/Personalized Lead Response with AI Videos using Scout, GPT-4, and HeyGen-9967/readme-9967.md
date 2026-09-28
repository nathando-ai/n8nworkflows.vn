---
title: "🚀 Tự Động Hóa Trả Lời Lead Bằng Video Cá Nhân Hóa AI – N8n + GPT-4 + Heygen"
description: "Workflow này giúp các sếp tự động trả lời lead mới bằng video cá nhân hóa + email tự động, tiết kiệm thời gian lên đến 90% so với cách làm thủ công. Hỗ trợ toàn bộ quy trình từ nhận lead đến gửi video + email chỉ trong 2 phút!"
slug: "tieu-dong-hoa-video-lead-ai"
tags: [n8n, automation, ai-video, lead-nurturing, gpt-4, self-hosted]
keywords: [n8n workflow video cá nhân hóa, tự động hóa lead response, AI video outreach, Heygen API với n8n, GPT-4 tự động hóa email]
---

# 🚀 **Tự Động Hóa Trả Lời Lead Bằng Video Cá Nhân Hóa AI – N8n + GPT-4 + Heygen**

## **💡 Giải Pháp Cho Nỗi Đau Của Các Sếp**
Hàng ngày, các sếp phải mất **giờ đồng hồ** để trả lời lead mới bằng email hoặc gọi điện, nhưng lại không thể **cá nhân hóa** đủ để tạo ấn tượng. Kết quả?
- **Tỷ lệ chuyển đổi thấp** vì lead cảm thấy được xử lý như "máy móc".
- **Thời gian phản hồi chậm** khiến lead chuyển sang đối thủ.
- **Khó duy trì sự nhất quán** trong tone voice và thông điệp.

**Workflow này giải quyết tất cả!** Với **AI + Video**, các sếp sẽ:
✅ **Tự động trả lời lead mới** chỉ trong **2 phút** (thay vì 30 phút thủ công).
✅ **Tạo video cá nhân hóa** với giọng nói và hình ảnh giống như chính các sếp.
✅ **Gửi email tự động** chứa video + thông tin lead, tăng **tỷ lệ mở email lên 30%**.
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và **không bị gián đoạn**, các sếp nên **self-host n8n** trên VPS chuyên dụng.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ sức mạnh cho workflow này)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian** so với cách làm thủ công.
- **Tăng tỷ lệ chuyển đổi lead** lên **2-3 lần** nhờ video cá nhân hóa.
- **Duy trì tone voice nhất quán** với AI.
- **Hoạt động tự động 24/7**, không cần can thiệp.
- **Thêm giá trị cho lead** bằng video chuyên nghiệp (không cần quay thủ công).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Heygen** (để tạo video AI) + **API Key**.
✔ **Tài khoản Scout** (CRM cho lead) + **API Key**.
✔ **Tài khoản OpenAI** (GPT-4) + **API Key**.
✔ **Tài khoản Gmail** (để gửi email tự động) + **OAuth2**.
✔ **Link Calendly** (hoặc công cụ booking khác) để thêm vào email.

---
:::note[CHUẨN BỊ N8N]
- N8n **self-hosted** (không dùng cloud để tránh giới hạn API).
- Cài đặt **n8n-nodes-langchain** (để sử dụng AI Agent).
- Cài đặt **n8n-nodes-base** (Gmail, HTTP, Wait...).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có **2 cách**:
- **Tải file JSON** từ [n8n.io/workflows/9967](https://n8n.io/workflows/9967) và import vào **n8n Editor**.
- **Copy JSON** từ link trên và **paste** vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này có **12 node**, nhưng các sếp **phải cấu hình kỹ** các node sau:

##### **🔹 Node "Selfie Video Prompt Agent" (Agent LangChain)**
- **Mục đích**: Tạo script video cá nhân hóa cho lead.
- **Cấu hình**:
  - Điền **OpenAI API Key** vào `openAiApi` (từ credentials).
  - **Chỉnh Prompt** để phù hợp với **brand tone** của các sếp:
    ```json
    "systemMessage": "Bạn là một chuyên gia bán hàng AI. Viết một đoạn script video ngắn (15-20 giây) để chào lead {name}, giới thiệu về {company} và mời họ đặt lịch meeting qua {calendly_link}. Tone phải thân thiện và chuyên nghiệp."
    ```

##### **🔹 Node "Get Avatars" & "Generate Video" (Heygen API)**
- **Mục đích**: Tạo video từ script bằng AI.
- **Cấu hình**:
  - Thêm **Heygen API Key** vào `httpHeaderAuth` (credentials).
  - Chọn **avatar** và **voice style** phù hợp (ví dụ: avatar giống các sếp).
  - **Lưu ý**: Heygen có giới hạn API, nên các sếp nên **check status** ở node `Wait1` để tránh lỗi.

##### **🔹 Node "Send Email & Video" (Gmail)**
- **Mục đích**: Gửi email tự động chứa video + thông tin lead.
- **Cấu hình**:
  - Kết nối **Gmail OAuth2** (credentials).
  - **Chỉnh template email** để phù hợp:
    ```html
    <p>Hi {name},</p>
    <p>Tôi là {your_name} từ {company}. Đây là video chào mừng bạn:</p>
    <iframe width="560" height="315" src="{video_url}" frameborder="0"></iframe>
    <p>Đặt lịch meeting qua <a href="{calendly_link}">đây</a>!</p>
    ```

##### **🔹 Node "OpenAI Chat Model1" (GPT-4)**
- **Mục đích**: Tạo email HTML tự động.
- **Cấu hình**:
  - Chọn **model: gpt-4.1-mini** (rẻ hơn GPT-4).
  - **Prompt mẫu**:
    ```json
    "prompt": "Tạo một email HTML cá nhân hóa cho lead {name}, chứa video {video_url}, thông tin {company}, và link booking {calendly_link}. Tone phải thân thiện và chuyên nghiệp."
    ```

#### **3. Kích Hoạt ⚡️**
- **Test Run** với **dữ liệu mẫu** (ví dụ: tên lead = "Anh Minh", email = "minh@example.com").
- **Bật Active** workflow sau khi kiểm tra thành công.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Thêm Slack/Telegram Notification**
   - Sử dụng node **Slack Webhook** để thông báo khi video hoàn tất.
   ```json
   "webhookUrl": "https://hooks.slack.com/services/..."
   ```

2. **Lưu Log Tất Cả Video**
   - Sử dụng **Google Sheets** hoặc **Airtable** để lưu lịch sử video đã tạo.
   - Node **Google Sheets** + **HTTP Request** để ghi dữ liệu.

3. **Tự Động Xóa Video Sau 7 Ngày**
   - Thêm node **Wait** + **HTTP Request (Heygen API)** để xóa video cũ.
   ```json
   "method": "DELETE",
   "url": "https://api.heygen.com/videos/{video_id}"
   ```

4. **Tăng Cường Cá Nhân Hóa**
   - Sử dụng **Scout API** để lấy thông tin lead (ví dụ: ngành nghề, sở thích) và đưa vào script.
   ```json
   "prompt": "Bạn là {name}, từ {company}. Tôi thấy bạn quan tâm đến {interest}. Đây là video chào mừng..."
   ```

---
### 📌 **Kết Luận**
Workflow này **không chỉ tự động hóa trả lời lead**, mà còn **tăng giá trị cho lead** bằng video cá nhân hóa AI. Các sếp sẽ:
✔ **Tiết kiệm thời gian** để tập trung vào chiến lược.
✔ **Tăng tỷ lệ chuyển đổi** nhờ video chuyên nghiệp.
✔ **Hoạt động 24/7** mà không cần can thiệp.

**🚀 Hãy import ngay và thử nghiệm!** Nếu có vấn đề, các sếp có thể **comment bên dưới** hoặc liên hệ với tác giả [Drew Fabrikant](https://n8n.io/workflows/9967) để hỗ trợ.

---
**💬 Câu hỏi thường gặp:**
- **Cần bao nhiêu tiền để chạy workflow này?**
  - Heygen: ~$0.50/video (gói free có giới hạn).
  - OpenAI: ~$0.001/1K tokens (gói free có giới hạn).
  - Gmail: Miễn phí (nếu không quá 500 email/ngày).
- **Làm sao nếu Heygen API lỗi?**
  - Kiểm tra node `Wait1` và **retry** sau 5-10 giây.
- **Có thể thay thế Heygen bằng AI khác không?**
  - Có, nhưng Heygen có **chất lượng video tốt nhất** hiện nay. Các sếp có thể thử **Synthesia** hoặc **Pictory**.