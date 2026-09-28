---
title: "🎥 Tự Động Hóa Trả Lời Lead Inbound Bằng Video Cá Nhân Hóa AI (Heygen + GPT-4) - Không Cần Code"
description: "Workflow này tự động tạo video cá nhân hóa từ thông tin lead, gửi kèm email tự động hóa với GPT-4 và Heygen AI - giúp tăng tỷ lệ chuyển đổi lên 300% chỉ trong vài giây sau khi lead gửi form."
slug: "tieu-dong-hoa-video-canh-bao-lead-inbound"
tags: [n8n, automation, no-code, ai-video, lead-nurturing, gpt-4, heygen, sales-automation]
keywords: [n8n workflow video cá nhân hóa, tự động hóa lead inbound, AI video marketing, Heygen API n8n, GPT-4 tự động email, tự động hóa bán hàng không code]
---

# 🚀 **Tự Động Hóa Trả Lời Lead Inbound Bằng Video Cá Nhân Hóa AI (Heygen + GPT-4)**

### **🔥 Nỗi Đau Của Các Sếp Khi Làm Thủ Công**
Hàng ngày, các sếp phải:
- **Chờ đợi** lead gửi form và sau đó **tự tay** viết email, tạo video giới thiệu, và gửi đi (thời gian trung bình: 30-60 phút/lead).
- **Không thể cá nhân hóa** vì thiếu thời gian và công cụ tự động hóa.
- **Mất cơ hội** khi lead đã chuyển sang đối thủ trong khi chờ đợi phản hồi.
- **Không đo lường được hiệu quả** của video và email vì không có hệ thống tự động hóa.

**Workflow này giải quyết tất cả bằng:**
✅ **Tự động tạo video cá nhân hóa** từ thông tin lead trong giây lát.
✅ **Gửi email kèm video** ngay lập tức (không cần chờ đợi).
✅ **Tăng tỷ lệ chuyển đổi** lên **300%** so với phương pháp truyền thống.
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **ổn định 24/7** và **không bị gián đoạn**, các sếp nên **self-host n8n** trên VPS chuyên dụng:
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đảm bảo tốc độ cao cho Heygen + GPT-4)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ **60 phút/lead** xuống **5 giây/lead**.
- **Cá nhân hóa hoàn toàn**: Video và email được **tự động điều chỉnh** dựa trên thông tin lead (tên, ngành nghề, vấn đề gặp phải).
- **Tăng tỷ lệ phản hồi**: Lead **gần gấp 3x** hơn khi nhận được video cá nhân hóa so với email thường.
- **Hoạt động liên tục**: Không cần can thiệp của con người, **24/7**.
- **Dễ dàng mở rộng**: Thêm **Slack/Telegram báo cáo**, **lưu log**, hoặc **gửi báo cáo định kỳ** cho team.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Heygen API**:
   - Đăng ký tại [Heygen](https://heygen.com/) và lấy **API Key**.
   - Thiết lập **credential** trong n8n với loại `httpHeaderAuth` (Header Name: `Authorization`, Value: `Bearer {API_KEY}`).

2. **Tài khoản OpenAI (GPT-4)**:
   - Đăng ký tại [OpenAI](https://platform.openai.com/) và lấy **API Key**.
   - Thiết lập **credential** trong n8n với loại `openAi`.

3. **Tài khoản Gmail (OAuth2)**:
   - Cần **một email Gmail** để gửi email tự động.
   - Thiết lập **credential OAuth2** trong n8n (chọn `gmail`).

4. **Form Submission**:
   - Một **form trên website** (có thể là Google Form, Typeform, hoặc form tùy chỉnh) để lead nhập thông tin (tên, email, website, vấn đề gặp phải).

5. **Link Calendly (nếu có)**:
   - Nếu muốn thêm **CTA đặt lịch hẹn**, cập nhật link Calendly vào **prompt của AI Agent** và **email template**.

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow này:
- **Tải file JSON** từ [n8n.io/workflows/6404](https://n8n.io/workflows/6404) và import vào **n8n Editor**.
- **Copy toàn bộ JSON** từ link trên và **paste** vào **Import Workflow** trong n8n.

:::note[Lưu ý]
- **Không copy/paste trực tiếp từ trang web** (do có ký tự đặc biệt gây lỗi).
- **Kiểm tra lại** các **credential** sau khi import (Heygen, OpenAI, Gmail).
:::

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **10 node** quan trọng, các sếp cần **cấu hình kỹ** các node sau:

##### **🔹 Node 1: "On form submission" (formTrigger)**
- **Chọn loại trigger**: `Form Submission` (n8n-nodes-base.formTrigger).
- **Cấu hình**:
  - **Form URL**: Địa chỉ form lead gửi (ví dụ: `https://formsubmit.co/your-email`).
  - **Fields cần bắt**: `name`, `email`, `website`, `pain-point` (vấn đề lead gặp phải).
  - **Test**: Gửi một form mẫu để kiểm tra dữ liệu có truyền vào workflow không.

##### **🔹 Node 2: "HeyGen Post" (httpRequest)**
- **Thiết lập credential**: Sử dụng **Heygen API Key** (đã thiết lập trước).
- **URL**: `https://api.heygen.com/v1/videos`
- **Headers**:
  ```json
  {
    "Authorization": "Bearer {HEYGEN_API_KEY}",
    "Content-Type": "application/json"
  }
  ```
- **Body (JSON)**:
  ```json
  {
    "script": "{{ $node["Selfie Video Prompt Agent"].json.output.script }}",
    "avatar": "your-avatar-id",  // Thay bằng ID avatar của bạn trên Heygen
    "voice": "your-voice-id",     // Thay bằng ID voice của bạn
    "language": "en-US"
  }
  ```
  - **Lưu ý**: `$node["Selfie Video Prompt Agent"].json.output.script` là **script video** được tạo bởi AI Agent.

##### **🔹 Node 3: "Wait" & "Wait1" (wait)**
- **Thời gian chờ**: Heygen có thể mất **5-30 giây** để tạo video.
  - **Cài đặt**: `5000` (5 giây) hoặc `30000` (30 giây) tùy thuộc vào tốc độ Heygen.
  - **Lưu ý**: Nếu video chưa hoàn thành, workflow sẽ **chờ lại** cho đến khi trạng thái thành công.

##### **🔹 Node 4: "Selfie Video Prompt Agent" (agent)**
- **Cấu hình LangChain Agent**:
  - **System Message (Prompt)**:
    ```plaintext
    You are a professional video script writer for lead nurturing. Your task is to create a short, engaging video script (under 30 seconds) based on the lead's information.

    Format:
    1. Greet the lead by name.
    2. Mention their website/industry.
    3. Reference their pain point (e.g., "I see you're struggling with [pain point]...").
    4. Briefly introduce your brand/service.
    5. End with a call-to-action (e.g., "Let's schedule a quick call to discuss how we can help!").

    Example:
    "Hi [Name], thanks for reaching out! I noticed you're at [Website], and it looks like you're dealing with [Pain Point]. At [Your Company], we specialize in helping businesses like yours [solve problem]. Let's hop on a quick call to explore how we can make this easier for you. Book a slot here: [Calendly Link]."
    ```
  - **Input Variables**: `$json.name`, `$json.email`, `$json.website`, `$json.pain-point`.
  - **Test**: Gửi một **dữ liệu mẫu** (ví dụ: `{"name": "John", "email": "john@example.com", "website": "john.com", "pain-point": "tối ưu hóa SEO"}`) để kiểm tra script.

##### **🔹 Node 5: "OpenAI Chat Model1" (lmChatOpenAi)**
- **Model**: `gpt-4.1-mini` (đã thiết lập sẵn).
- **Prompt**:
  ```plaintext
  Write a professional and engaging email outreach for a lead. The email should include:
  1. A personalized greeting using the lead's name.
  2. A brief introduction about their pain point (from the video script).
  3. A call-to-action to book a call using the provided Calendly link.
  4. An embedded video thumbnail (use HTML for the video embed code).
  5. Keep the tone friendly but professional.

  Example:
  <html>
    <body>
      <h2>Hi [Name],</h2>
      <p>Thanks for reaching out! I noticed you're dealing with [Pain Point] at [Website].</p>
      <p>Here's a quick video I created for you:</p>
      <iframe width="560" height="315" src="[VIDEO_URL]" frameborder="0" allowfullscreen></iframe>
      <p>Let's discuss how we can help! <a href="[CALENDLY_LINK]">Book a call here</a>.</p>
      <p>Best regards,<br>[Your Name]</p>
    </body>
  </html>
  ```
  - **Input Variables**: `$json.name`, `$json.email`, `$json.pain-point`, `$json.video_url`, `$json.video_thumbnail`.

##### **🔹 Node 6: "Get Video" (httpRequest)**
- **URL**: `https://api.heygen.com/v1/videos/{video_id}` (truyền động từ node "HeyGen Post").
- **Headers**: Giống như node "HeyGen Post".
- **Lấy dữ liệu**: Video URL và thumbnail khi video hoàn thành.

##### **🔹 Node 7: "OpenAI" (openAi)**
- **Sử dụng** để **tối ưu hóa email** (nếu cần) hoặc **tạo thêm nội dung** (không bắt buộc).

##### **🔹 Node 8: "Send Email & Video" (gmail)**
- **Cấu hình**:
  - **To**: `$json.email` (email lead).
  - **Subject**: `"Video Personalized for You - [Your Company]"`.
  - **HTML Body**: Dữ liệu từ node "OpenAI Chat Model1".
  - **Test**: Gửi email mẫu để kiểm tra **định dạng và video có hiển thị** không.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Gửi **dữ liệu mẫu** qua form và kiểm tra:
     - Video có tạo thành công không?
     - Email có gửi được không?
     - Video có hiển thị trong email không?

2. **Bật Active**:
   - Sau khi **test thành công**, chuyển workflow sang **Active**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Thêm Slack/Telegram Báo Cáo**:
   - Sử dụng **node `slack`** hoặc **`telegram`** để thông báo khi workflow hoàn thành.
   - Ví dụ: `"🎥 Video cá nhân hóa đã gửi cho lead: {{ $json.name }}"`.

2. **Lưu Log & Analytics**:
   - Sử dụng **node `stickyNote`** hoặc **Google Sheets** để lưu lịch sử lead và tỷ lệ chuyển đổi.
   - Cập nhật **thống kê** như: `Tỷ lệ mở email`, `Tỷ lệ click video`, `Tỷ lệ đặt lịch hẹn`.

3. **Tối Ưu Hóa Prompt**:
   - Nếu tỷ lệ chuyển đổi thấp, **cập nhật lại prompt** trong **LangChain Agent** để:
     - **Động viên lead** hơn (ví dụ: "Chúng tôi đã giúp hơn 500 doanh nghiệp giải quyết vấn đề này!").
     - **Thêm chứng minh xã hội** (ví dụ: "Hàng ngàn khách hàng tin tưởng chúng tôi...").

4. **Gửi Báo Cáo Định Kỳ**:
   - Sử dụng **node `setInterval`** (n8n) để gửi **báo cáo tuần/month** cho team:
     - Số lead được xử lý.
     - Tỷ lệ chuyển đổi.
     - Video/email nào hiệu quả nhất.

5. **Tích Hợp CRM (HubSpot/Salesforce)**:
   - Sử dụng **node `hubspot`** hoặc **`salesforce`** để cập nhật thông tin lead vào CRM tự động.
:::

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** của các sếp để tập trung vào **strategy** hơn là **chăm sóc lead thủ công**. Với **AI + Heygen + GPT-4**, mỗi lead đều nhận được **trải nghiệm cá nhân hóa cao cấp**, tăng **tỷ lệ chuyển đổi lên 300%** và **tạo ấn tượng mạnh mẽ** ngay từ lần tiếp xúc đầu tiên.

**🚀 Hành động ngay hôm nay:**
1. **Import workflow** và **cấu hình credential**.
2. **Test với dữ liệu mẫu** trước khi chuyển sang live.
3. **Bật Active** và **theo dõi kết quả**!

**Nếu có vấn đề**, các sếp có thể tham khảo:
- [Tutorial chi tiết của Automate With Marc](https://www.youtube.com/@Automatewithmarc)
- [Diễn đàn hỗ trợ n8n](https://community.n8n.io/)

**Chúc các sếp thành công!** 💪🚀