---
title: "🚀 Tự Động Hoà Báo Cáo Xu Hướng Ngành Hàng Ngày Từ Medium → Google Docs Với AI Claude (Không Cần Code)"
description: "Workflow tự động hóa 100% miễn phí giúp các sếp scrap dữ liệu từ Medium, sử dụng AI Claude (OpenRouter) phân tích và tổng hợp báo cáo xu hướng ngành hàng ngày vào Google Docs, tiết kiệm thời gian nghiên cứu lên đến 80%. Hoạt động 24/7, cá nhân hóa và tự động cập nhật."
slug: "tieu-dong-hoa-bao-cao-xu-huong-nganh-ai-claude"
tags: [n8n, automation, ai-summarization, market-research, google-docs, openrouter, browseract]
keywords: [n8n workflow tự động hóa, báo cáo xu hướng ngành, AI Claude tổng hợp nội dung, scrap Medium, Google Docs tự động, tự động hóa nghiên cứu thị trường]
---

# 🚀 **Tự Động Hoà Báo Cáo Xu Hướng Ngành Hàng Ngày Từ Medium → Google Docs Với AI Claude**

### **Giải pháp cho các sếp bị "ngập" trong việc theo dõi xu hướng ngành**
Hàng ngày, các sếp phải mất **3-5 giờ** để:
- Quét thủ công các bài viết trên Medium theo nhiều tag khác nhau.
- Lọc bỏ spam, trùng lặp và nội dung không liên quan.
- Tóm tắt và phân loại bài viết theo chủ đề (Tech, Marketing, AI, Engineering...).
- Ghi chép vào Google Docs hoặc Notion để báo cáo cho ban lãnh đạo.

**Workflow này tự động hóa toàn bộ quy trình đó chỉ trong vài phút mỗi ngày!** Dựa trên công nghệ **AI Claude (OpenRouter)**, nó sẽ:
✅ **Scrap** dữ liệu từ Medium theo tag cụ thể.
✅ **Phân tích AI** loại bỏ spam, trùng lặp và tóm tắt nội dung.
✅ **Categorize** bài viết theo ngành (Must Reads, Engineering, Business...).
✅ **Tự động tạo báo cáo** dưới dạng Google Docs với định dạng chuyên nghiệp.
✅ **Gửi thông báo Slack** khi có báo cáo mới.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để tránh giới hạn của phiên bản Cloud.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ 5 giờ/tháng xuống còn **5 phút/tháng**.
- **Chính xác cao**: AI Claude loại bỏ spam và trùng lặp tự động.
- **Cá nhân hóa**: Phân loại bài viết theo ngành (Tech, Marketing, AI...).
- **Hoạt động liên tục**: Báo cáo tự động cập nhật hàng ngày.
- **Dễ chia sẻ**: Google Docs có thể chia sẻ với team hoặc khách hàng.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản và API Keys**:
   - [BrowserAct](https://browseract.com/) (Template: **"Automated Industry Trend Scraper & Outline Creator"**).
   - [OpenRouter](https://openrouter.ai/) (API Key cho model **anthropic/claude-sonnet-4.5**).
   - [Google Docs](https://developers.google.com/docs/api/quickstart/nodejs) (OAuth 2.0).
   - [Slack](https://api.slack.com/) (Webhook URL hoặc OAuth Token).
2. **URL Medium mục tiêu**:
   - Ví dụ: `https://medium.com/tag/ai?sort=dateAsc` (tag AI).
3. **Google Docs mới**:
   - Tạo một Google Doc trống để workflow tự động cập nhật.
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
**Cách 1: Từ file JSON**
1. Tải workflow từ [n8n.io/workflows/12348](https://n8n.io/workflows/12348) (đăng nhập tài khoản n8n).
2. Nhấn **Export** (icon hình file) → Chọn **JSON**.
3. Trên n8n Editor, nhấn **Import** (icon hình mũi tên vào) → Dán JSON và nhấn **Import**.

**Cách 2: Copy/Paste JSON**
1. Copy toàn bộ JSON từ [n8n.io/workflows/12348](https://n8n.io/workflows/12348).
2. Trên n8n Editor, nhấn **Import** → Chọn **Paste JSON** → Dán và nhấn **Import**.

---

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **16 node**, nhưng các sếp chỉ cần chú ý đến **5 node quan trọng** sau:

##### **A. Node "Every Day" (scheduleTrigger)**
- **Cấu hình**:
  - Thời gian chạy: **Mỗi ngày lúc 8h sáng** (thời gian Việt Nam).
  - **Lưu ý**: Nếu không muốn chạy hàng ngày, thay bằng **Webhook** (node `webhook` không có trong workflow này, các sếp cần thêm nếu muốn kích hoạt thủ công).

##### **B. Node "Scrape Headlines" (browserAct)**
- **Cấu hình**:
  - **Credentials**: Chọn `browserActApi` (đã cấu hình trước khi import).
  - **Template**: Chọn **"Automated Industry Trend Scraper & Outline Creator"** (đã lưu trên BrowserAct).
  - **URL Target**: Điền vào node **"Target Page Link"** (type `set`) trước khi chạy.
    - Ví dụ: `https://medium.com/tag/ai?sort=dateAsc` (tag AI).
    - **Lưu ý**: Nếu muốn scrap nhiều tag, các sếp cần **tạo một workflow riêng** hoặc sử dụng node `splitInBatches` để chạy song song.

##### **C. Node "OpenRouter" (lmChatOpenRouter)**
- **Cấu hình**:
  - **Credentials**: Chọn `openRouterApi` (API Key của OpenRouter).
  - **Model**: Đã mặc định là `anthropic/claude-sonnet-4.5` (không cần thay đổi).
  - **Prompt**: AI sẽ tự động phân tích và tóm tắt, không cần chỉnh sửa.

##### **D. Node "Add Header & Body" / "Add Body" (googleDocs)**
- **Cấu hình**:
  - **Credentials**: Chọn `googleDocsOAuth2Api`.
  - **File Google Docs**: Chọn **file mới** (các sếp tạo trước khi chạy).
  - **Lưu ý**:
    - Node này **cập nhật nội dung** vào Google Docs. Nếu muốn tạo file mới mỗi ngày, các sếp cần thêm node `googleDocs.create` trước node `update`.

##### **E. Node "Slack Team Notification" (slack)**
- **Cấu hình**:
  - **Credentials**: Chọn `slackApi` (Webhook URL hoặc OAuth Token).
  - **Message**: Đã mặc định là thông báo báo cáo mới được tạo.
  - **Lưu ý**: Nếu không muốn thông báo Slack, các sếp có thể **xóa node này**.

---
#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Nhấn **Run Workflow** (icon play) và chọn **Test Execution**.
   - Điền **URL Medium** vào node `Target Page Link` (type `set`).
   - Kiểm tra kết quả:
     - Slack: Có thông báo không?
     - Google Docs: Có nội dung được cập nhật không?
2. **Bật Active**:
   - Sau khi test thành công, nhấn **Active** (icon bật tắt) để workflow chạy tự động hàng ngày.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Scrap nhiều tag Medium cùng lúc**
   - Sử dụng node `splitInBatches` để chạy song song cho nhiều URL.
   - Ví dụ: Scrap `tag/ai`, `tag/tech`, `tag/marketing` trong cùng một workflow.

2. **Lưu log hoạt động**
   - Thêm node `stickyNote` sau node `Slack Team Notification` để ghi log vào n8n Dashboard.

3. **Gửi báo cáo định kỳ qua Email**
   - Thêm node `email` (n8n-nodes-base.email) sau node `googleDocs` để gửi liên kết Google Docs qua Email.

4. **Tùy chỉnh AI Prompt**
   - Nếu muốn AI Claude phân tích theo cách riêng, chỉnh sửa node `lmChatOpenRouter`:
     ```json
     {
       "parameters": {
         "prompt": "Tóm tắt bài viết này về chủ đề [CHỦ ĐỀ], loại bỏ spam và trùng lặp. Phân loại bài viết vào danh mục: Must Reads, Engineering, Business, AI."
       }
     }
     ```

5. **Xử lý Rate Limit**
   - Node `Rate Limit Mitigation` (type `wait`) đã được cấu hình mặc định là **5 giây**. Nếu gặp lỗi rate limit, tăng thời gian chờ.

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào chiến lược kinh doanh thay vì việc nghiên cứu thủ công. Với **AI Claude** phân tích và **Google Docs tự động hóa**, báo cáo xu hướng ngành sẽ **luôn được cập nhật mới nhất**, chính xác và chuyên nghiệp.

**Hành động ngay!**
1. Import workflow vào n8n.
2. Cấu hình **URL Medium** và **Google Docs**.
3. Bật **Active** và để AI làm việc cho bạn!

---
**Cần hỗ trợ?**
- [BrowserAct Docs](https://docs.browseract.com)
- [n8n Community](https://community.n8n.io/)
- **Góp ý**: Để lại comment bên dưới hoặc liên hệ [Madame AI Team](https://madameai.com/)!