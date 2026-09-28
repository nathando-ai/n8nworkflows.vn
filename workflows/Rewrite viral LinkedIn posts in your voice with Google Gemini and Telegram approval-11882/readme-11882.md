---
title: "🚀 Tự Động Hóa Tạo Bài Post Viral LinkedIn Theo Giọng Điệu Cá Nhân Với Google Gemini + Xác Nhận Telegram"
description: "Workflow tự động hóa viết lại bài post LinkedIn thành công viral theo giọng điệu cá nhân của bạn, kết hợp AI Google Gemini và xác nhận thông qua Telegram. Giúp tiết kiệm thời gian, tăng độ tương tác và tự động hóa nội dung LinkedIn 24/7."
slug: "tieu-dong-hoa-tao-bai-post-linkedin-voi-gemini-telegram"
tags: [n8n, automation, no-code, content-creation, ai-multimodal, linkedin-automation, telegram-bot, google-gemini]
keywords: [n8n workflow linkedin, tự động hóa bài post linkedin, google gemini chatbot, viết bài viral linkedin, approval telegram, connectsafely ai]
---

# 🚀 **Tự Động Hóa Tạo Bài Post Viral LinkedIn Theo Giọng Điệu Cá Nhân**

Bạn đã bao giờ cảm thấy mệt mỏi khi phải viết hàng chục bài post LinkedIn mỗi tuần, nhưng lại không chắc chắn liệu nội dung đó có phù hợp với giọng điệu cá nhân hay không? Hay bạn muốn tối ưu hóa thời gian để tập trung vào chiến lược marketing hơn? **Workflow này sẽ giải quyết tất cả những vấn đề đó!**

Với công cụ **n8n**, bạn có thể **tự động hóa toàn bộ quy trình** từ việc **scrape bài post LinkedIn**, **viết lại bằng giọng điệu cá nhân** (thông qua AI Google Gemini), **tạo hình ảnh minh họa**, **xác nhận trước khi đăng** (qua Telegram) đến **đăng bài tự động** trên LinkedIn. **Không cần viết một dòng code nào!**

---
## 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần viết bài từ đầu, chỉ cần gửi URL bài post LinkedIn qua Telegram.
- **Giọng điệu cá nhân hóa**: AI viết lại bài theo phong cách riêng của bạn (cấu hình qua node `Load Your Persona`).
- **Xác nhận trước khi đăng**: Tránh đăng bài không phù hợp nhờ hệ thống **approval/reject** qua Telegram.
- **Tăng tương tác**: Bài post được viết lại với nội dung hấp dẫn hơn, tăng cơ hội virality.
- **Hoạt động 24/7**: Workflow chạy tự động, không cần can thiệp thủ công.
- **Tích hợp hình ảnh**: AI tự động tạo hình ảnh phù hợp cho bài post.
:::

---
## 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị các tài khoản và API sau:

### **1. Telegram Bot**
- Tạo bot qua [@BotFather](https://t.me/BotFather) và lấy **API Token**.
- Cài đặt bot vào Telegram và **lấy Telegram ID** của chính mình (để node `🔒 Security Check` hoạt động).
- **Cài đặt bot vào nhóm** (nếu muốn quản lý nhiều người).

### **2. Google Gemini API**
- **Đăng ký API Key** tại [Google AI Studio](https://aistudio.google.com/).
- Chọn **Gemini Pro** hoặc **Gemini 1.5** (phù hợp với node `lmChatGoogleGemini` và `googleGemini`).

### **3. LinkedIn OAuth**
- Tạo **OAuth App** tại [LinkedIn Developer Portal](https://www.linkedin.com/developers/).
- Lấy **Client ID** và **Client Secret** để đăng nhập và đăng bài tự động.

### **4. ConnectSafely.ai (Node Custom)**
- **Đăng ký tài khoản** tại [ConnectSafely.ai](https://connectsafely.ai/).
- Lấy **API Key** để scrape bài post LinkedIn.

### **5. Tài khoản LinkedIn cá nhân**
- Đăng nhập LinkedIn với tài khoản muốn đăng bài tự động.

### **6. Giọng điệu cá nhân (Persona)**
- Chuẩn bị **một đoạn văn bản ngắn** (5-10 câu) mô tả phong cách viết của bạn (ví dụ: chuyên nghiệp, thân thiện, hài hước...). Đây sẽ được sử dụng trong node `👤 Load Your Persona`.

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. Tải workflow từ [n8n.io/workflows/11882](https://n8n.io/workflows/11882) (chọn **Export as JSON**).
2. Trên **n8n Editor**, nhấn **Import** và chọn file JSON vừa tải.
3. Chọn **Self-hosted** (nếu tự host) hoặc **n8n.cloud** (nếu dùng miễn phí).

#### **Phương pháp 2: Copy/Paste JSON**
1. Copy toàn bộ mã JSON từ [n8n.io/workflows/11882](https://n8n.io/workflows/11882).
2. Trên **n8n Editor**, nhấn **Import** → **Paste JSON**.

---
### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**

#### **🔍 Node `🔍 Extract Post URL` (Code)**
- **Mục đích**: Trích xuất URL bài post từ Telegram message.
- **Lưu ý**:
  - Node này sử dụng **regex** để tìm URL trong message. Nếu Telegram message có định dạng khác, cần chỉnh sửa regex.
  - **Kiểm tra**: Gửi một URL bài post qua Telegram và đảm bảo node trích xuất đúng.

#### **👤 Node `👤 Load Your Persona` (Code)**
- **Mục đích**: Tải giọng điệu cá nhân (Persona) để AI viết lại bài post theo phong cách của bạn.
- **Cách cấu hình**:
  ```javascript
  // Thay thế nội dung này bằng đoạn văn bản mô tả phong cách viết của bạn
  const persona = {
    tone: "Chuyên nghiệp nhưng thân thiện, giọng điệu gần gũi với khách hàng",
    style: "Sử dụng câu hỏi để kích thích tương tác, kết hợp dữ liệu thực tế",
    examples: [
      "Ví dụ: 'Hãy tưởng tượng nếu bạn có thể tự động hóa 80% công việc hàng ngày...'",
      "Cách kết thúc: 'Bạn có thử nghiệm chưa? Hãy chia sẻ ý kiến dưới đây!'"
    ]
  };
  $node.set("persona", persona);
  ```
- **Lưu ý**:
  - **Đảm bảo đoạn văn bản ngắn gọn** (AI sẽ sử dụng nó để viết lại bài post).
  - Nếu không cấu hình, AI sẽ viết theo phong cách mặc định (có thể không phù hợp).

#### **🤖 Node `Google Gemini Chat Model` (lmChatGoogleGemini)**
- **Mục đích**: Viết lại bài post theo giọng điệu cá nhân.
- **Cấu hình cần thiết**:
  - **API Key**: Điền **Google Gemini API Key** (từ Google AI Studio).
  - **Prompt mẫu**:
    ```json
    {
      "role": "user",
      "content": "Viết lại bài post này theo phong cách cá nhân của tôi. Bài post gốc: {{ $json.originalPost }}. Giọng điệu: {{ $json.persona.tone }}. Kết thúc bằng một câu hỏi để kích thích tương tác."
    }
    ```
  - **Lưu ý**:
    - **Kiểm tra kết quả**: Gửi một bài post mẫu qua Telegram và xem AI viết như thế nào. Nếu không phù hợp, chỉnh sửa **prompt** hoặc **persona**.

#### **🎨 Node `Generate an image` (googleGemini)**
- **Mục đích**: Tạo hình ảnh minh họa cho bài post.
- **Cấu hình cần thiết**:
  - **Prompt**: Sử dụng nội dung từ node `📝 Create Image Prompt` (được tự động tạo từ bài post).
  - **Lưu ý**:
    - Nếu hình ảnh không phù hợp, chỉnh sửa **prompt** trong node `📝 Create Image Prompt`.
    - **Kiểm tra**: Hình ảnh phải rõ nét và liên quan đến nội dung bài post.

#### **🔒 Node `🔒 Security Check` (If)**
- **Mục đích**: Chỉ cho phép người dùng đã được xác thực (Telegram ID) sử dụng bot.
- **Cấu hình**:
  - Điền **Telegram ID của bạn** vào trường `{{ $json.telegramId }}`.
  - **Lưu ý**:
    - Lấy Telegram ID bằng cách gửi tin nhắn cho bot và kiểm tra URL: `https://t.me/<botname>?start=<your_id>`.
    - Nếu không cấu hình, **người dùng khác** có thể gửi URL bài post.

#### **📢 Node `Send Message and Wait for Approval` (Telegram)**
- **Mục đích**: Gửi preview bài post và hình ảnh cho xác nhận.
- **Cấu hình**:
  - **Chat ID**: Điền **Telegram ID của bạn** (hoặc nhóm).
  - **Lưu ý**:
    - Nếu không cấu hình, bot sẽ gửi tin nhắn đến chat mặc định (có thể không đúng).

#### **📤 Node `Create LinkedIn Post` (linkedIn)**
- **Mục đích**: Đăng bài tự động lên LinkedIn.
- **Cấu hình cần thiết**:
  - **OAuth Credentials**: Điền **Client ID** và **Client Secret** từ LinkedIn Developer Portal.
  - **Lưu ý**:
    - **Kiểm tra quyền**: Đảm bảo tài khoản LinkedIn đã cấp quyền cho app.
    - **Rate limit**: LinkedIn có giới hạn đăng bài (thường 8 bài/ngày). Nếu quá giới hạn, workflow sẽ lỗi.

---
### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run**:
   - Gửi một URL bài post LinkedIn qua Telegram bot.
   - Kiểm tra:
     - AI có viết lại bài post không?
     - Hình ảnh có phù hợp không?
     - Bot có gửi preview và chờ xác nhận không?
2. **Bật Active**:
   - Sau khi kiểm tra thành công, chuyển workflow từ **Inactive** sang **Active**.

---
## ✍️ **Mẹo & Gợi Ý Nâng Cao**

### **1. Tích Hợp Slack Thay Vì Telegram**
- Thay node `telegramTrigger` và `telegram` bằng `slackTrigger` và `slack`.
- **Lợi ích**: Dễ dàng hơn trong môi trường doanh nghiệp sử dụng Slack.

### **2. Lưu Log Tất Cả Các Bài Post**
- Thêm node **Google Sheets** hoặc **Notion** sau node `Create LinkedIn Post` để lưu lịch sử bài post.
- **Cách làm**:
  - Sử dụng node `set` để lưu dữ liệu bài post (tiêu đề, nội dung, ngày đăng).
  - Kết nối với Google Sheets qua API.

### **3. Gửi Báo Cáo Định Kỳ**
- Sử dụng **n8n Scheduler** để chạy workflow hàng tuần và gửi báo cáo thống kê (số bài post, tương tác, engagement rate) qua Email hoặc Telegram.
- **Cách làm**:
  - Tạo một workflow mới với node `setDateTime` + `googleSheets` + `email`.

### **4. Tự Động Chọn Bài Post Viral Nhất**
- Thêm node **Google Analytics** hoặc **LinkedIn API** để theo dõi engagement rate.
- Sử dụng node `if` để chỉ đăng bài có engagement cao nhất.

### **5. Cập Nhật Giọng Điệu Cá Nhân (Persona) Mỗi Tháng**
- Tạo một **Google Form** để cập nhật lại phong cách viết của bạn.
- Sử dụng node `googleForm` để tự động cập nhật `👤 Load Your Persona`.

---
## 📌 **Kết Luận**
Workflow này không chỉ **giúp bạn tiết kiệm thời gian** khi viết bài post LinkedIn mà còn **tăng cơ hội virality** nhờ giọng điệu cá nhân hóa và hình ảnh chuyên nghiệp. **Không cần là nhà phát triển**, bạn cũng có thể tự động hóa toàn bộ quy trình chỉ với **n8n** và một chút cấu hình.

**Bắt đầu ngay!**
1. **Import workflow** vào n8n của bạn.
2. **Cấu hình các API và credentials** theo hướng dẫn.
3. **Test với một bài post mẫu** và điều chỉnh nếu cần.
4. **Bật workflow** và bắt đầu tự động hóa nội dung LinkedIn!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

**Chúc các sếp thành công với chiến lược LinkedIn tự động hóa!** 🚀