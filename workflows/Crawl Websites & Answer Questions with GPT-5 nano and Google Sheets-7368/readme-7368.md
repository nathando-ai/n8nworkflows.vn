---
title: "🤖 Tự Động Hoàn Hảo: Crawl Website + Trả Lời Câu Hỏi Với GPT-5 Nano & Google Sheets (Không Code)"
description: "Workflow tự động hóa hoàn toàn để thu thập thông tin từ website (sitemap, nội dung, liên kết), lưu vào Google Sheets, và trả lời câu hỏi người dùng như một 'công cụ AI của website' với GPT-5 Nano. Giúp tiết kiệm 80% thời gian nghiên cứu thị trường và hỗ trợ chatbot 24/7."
slug: "tieu-dong-hoan-hao-crawl-website-gpt-5-google-sheets"
tags: [n8n, automation, market-research, multimodal-ai, google-sheets, openai, gpt-5-nano, no-code]
keywords: [n8n workflow crawl website, tự động hóa nghiên cứu thị trường, chatbot AI website, GPT-5 nano tự động hóa, Google Sheets + AI, không cần code]
---

# 🚀 **Crawl Website + Trả Lời Câu Hỏi Với AI: Giải Pháp Tự Động Hóa 100% Cho Nghiên Cứu Thị Trường**

### **Nỗi Đau Của Các Sếp**
Bạn có bao giờ phải:
- **Tốn hàng giờ** để crawl website, phân tích nội dung, và tổng hợp thông tin?
- **Không thể trả lời nhanh** khi khách hàng hỏi về sản phẩm/đường dẫn trên website?
- **Lặp lại công việc** vì không có cơ sở dữ liệu thống nhất về website?

Workflow này **giải quyết tất cả** bằng cách:
✅ **Crawl tự động** tất cả trang từ sitemap (không cần viết code).
✅ **Trích xuất thông tin chi tiết** (ngôn ngữ, cấu trúc tiêu đề, liên kết nội bộ/ngoại bộ, tóm tắt).
✅ **Lưu vào Google Sheets** để truy xuất nhanh.
✅ **Trả lời câu hỏi người dùng** như một "AI của website" (ví dụ: *"Trang X có nội dung gì?"*, *"Có liên kết nào liên quan?"*).

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và **không bị gián đoạn**, các sếp nên **self-host n8n** trên VPS chuyên dụng:
👉 **[Đăng ký VPS TinoHost (Mã giảm giá: VPSN8N - 39%)](https://tino.vn/vps-n8n?affid=388)**
👉 **[VPS Xeon 4GB chỉ 50k/tháng (BNIX)](https://my.bnix.one/aff.php?aff=172)** (tối ưu cho AI + crawl)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** so với cách làm thủ công.
- **Cập nhật tự động** khi website thay đổi (không cần can thiệp).
- **Trả lời chính xác** mọi câu hỏi về website (ví dụ: *"Trang 'Dịch vụ' có nội dung gì?"*).
- **Hoạt động liên tục** 24/7, không phụ thuộc vào nhân viên.
- **Dữ liệu sạch** (không CSS/JS, chỉ nội dung thực sự).
- **Kết hợp với Slack/Telegram** để thông báo kết quả crawl.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets**:
   - **File mẫu**: [Liên kết Google Sheets](https://docs.google.com/spreadsheets/d/112qqkm4omdSzDT2jI17IQAxYvGjKuGlYxj6XytDA5L8/edit?usp=sharing) (copy và tạo bản sao).
   - **Quản trị viên** phải chia sẻ quyền **Editor** cho n8n.
2. **API Key OpenAI**:
   - **Tạo tại [OpenAI](https://platform.openai.com/account/api-keys)** và thêm vào **Credentials** của n8n (mã: `openAiApi`).
   - **Model yêu cầu**: `gpt-5-nano` (miễn phí) hoặc `gpt-4o` (đối với chọn sitemap).
3. **Webhook Basic Auth** (để nhận câu hỏi từ người dùng):
   - Tạo **một URL webhook** trong n8n (node `Chat web`) và bảo mật bằng **Basic Auth**.
   - **Gợi ý**: Sử dụng **ngrok** để expose webhook nếu self-host.

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/7368](https://n8n.io/workflows/7368) (ấn **Export**).
- **Cách import**:
  - Mở **n8n Editor** → **Import** → Dán JSON hoặc kéo thả file.
  - **Không cần chỉnh sửa** nếu đã có tất cả credentials.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflows này có **2 nhánh chính** (A và B), phụ thuộc vào trạng thái của Google Sheets. Các sếp cần chú ý:

##### **A. Cấu Hình Credentials (Bắt Buộc)**
| Node | Tham Số Cần Chỉnh | Ghi Chú |
|------|-------------------|---------|
| **Chat web** | `httpBasicAuth` | Điền **Username/Password** để bảo mật webhook. |
| **OpenAI Chat Model** | `openAiApi` | Chọn **API Key** đã tạo trước. |
| **Google Sheets** | `googleSheetsOAuth2Api` | Chọn **OAuth2 Credential** đã kết nối với Google Sheets. |
| **AI Agent** | **System Prompt** | Không cần chỉnh (đã tối ưu sẵn). |
| **Message a model (GPT-4o)** | **Model** | Chọn `gpt-4o` (nếu có) hoặc `gpt-5-nano`. |

##### **B. Cấu Hình Cụ Thể Cho Mỗi Nhánh**
###### **Nhánh A: Agent Mode (Trả Lời Câu Hỏi)**
- **Khi người dùng gửi URL đã crawl trước đó** (cột `Data schema = true`):
  - **AI Agent** sẽ sử dụng **bộ nhớ ngắn hạn** (50 tin nhắn) để trả lời liên tục.
  - **Cấu hình `HTTP Request2`**:
    - Đảm bảo **User-Agent** được chọn ngẫu nhiên (node `UA Rotativo1`) để tránh bị chặn.
    - **Headers** phải có `Accept-Language`, `Accept-Encoding`, `Referer`.

###### **Nhánh B: Crawl Website (Lần Đầu)**
- **Khi URL mới hoặc chưa crawl**:
  1. **AI Agent1** kiểm tra URL hợp lệ (trả về JSON `{ "URL": "...", "URL_bool": true/false }`).
  2. **Req robots.txt**:
     - **URL**: `{{ AI Agent1.output.URL }}/robots.txt`.
     - **Headers**: Phải có `User-Agent`, `Accept`, `Referer`.
  3. **extract sitemap url**:
     - **Code Node**: Sử dụng regex để trích xuất dòng `Sitemap:` trong `robots.txt`.
  4. **Maping Sitemap**:
     - **URL**: `{{ sitemapUrl }}` (đã trích xuất).
     - **Headers**: Giống như trên.

##### **C. Cấu Hình Google Sheets**
- **Sheet phải có cột**:
  - `Lang`, `H1 and hierarchy`, `External URLs`, `Internal URLs`, `Summary Content`, `Data schema`.
- **Node `Append row`**:
  - **Mappings**:
    - `Lang`: `$json.data.language`.
    - `H1 and hierarchy`: `$json.data.headings`.
    - `External URLs`: `$json.data.external_links`.
    - `Internal URLs`: `$json.data.internal_links`.
    - `Summary Content`: `$json.data.summary`.
    - `Data schema`: `true` (để chuyển sang Agent Mode).

##### **D. Cấu Hình Model GPT**
- **Node `OpenAI Chat Model`**:
  - **Model**: `gpt-5-nano` (miễn phí) hoặc `gpt-4o` (nếu có).
  - **Temperature**: Đặt **0.7** (để tránh trả lời quá ngẫu nhiên).
- **Node `Message a model` (chọn sitemap)**:
  - **System Prompt**: *"Tôi sẽ cho bạn 3 URL đầu tiên từ sitemap index. Hãy chọn và trả về JSON với URL của sitemap 'pages' dựa vào flags `scan_pages` và `scan_posts`."*

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Gửi **URL mẫu** (ví dụ: `https://example.com`) qua webhook.
   - Kiểm tra **Google Sheets** có dữ liệu crawl không.
2. **Bật Active**:
   - Đánh dấu workflow thành **Active** trong n8n Dashboard.
   - **Monitor Logs** để đảm bảo không có lỗi.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết Nối Với Slack/Telegram**:
   - Sử dụng **node `slack`** hoặc **`telegram`** để thông báo khi crawl hoàn tất.
   - Ví dụ: *"Crawl website [URL] thành công! Có [X] trang."*
2. **Lưu Log Crawl**:
   - Thêm **node `set`** trước `Append row` để ghi **thời gian crawl**, **status**, và **lỗi** (nếu có).
3. **Tự Động Crawl Định Kỳ**:
   - Sử dụng **node `setInterval`** (Custom Node) để crawl lại website sau **1 tuần/1 tháng**.
4. **Cải Thiện Trích Xuất Nội Dung**:
   - Thêm **node `code`** để **lọc bỏ CSS/JS** trước khi gửi cho GPT.
   - Ví dụ: Sử dụng regex `/<script|<style>.*?<\/script|<\/style>/g` để loại bỏ.
5. **Kết Hợp Với Notion**:
   - Thay vì Google Sheets, sử dụng **Notion API** để lưu dữ liệu (node `notion`).

---

### 📌 **Kết Luận**
Workflow này **không chỉ crawl website mà còn biến website thành một AI trả lời tự động**, giúp các sếp:
✔ **Tiết kiệm thời gian** cho công việc nghiên cứu thị trường.
✔ **Cập nhật dữ liệu** liên tục mà không cần can thiệp.
✔ **Trả lời khách hàng** nhanh chóng và chính xác.

**Hành động ngay**:
1. **Import workflow** và cấu hình credentials.
2. **Test với 1-2 website** để đảm bảo hoạt động.
3. **Kết nối với Slack/Telegram** để theo dõi kết quả.

👉 **[Tải workflow ngay](https://n8n.io/workflows/7368)** và **bắt đầu tự động hóa**!

---
**Chia sẻ ý kiến**:
Các sếp có thể **mở rộng workflow** thêm gì? Ví dụ: crawl nhiều website cùng lúc, thêm phân tích sentiment, hoặc kết nối với CRM? **Để lại comment bên dưới!** 🚀