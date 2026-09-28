---
title: "🚀 Tự Động Hóa Tạo Báo Cáo PDF Branded Từ Email Nhập Lệch Với Autype & AI Multimodal"
description: "Workflow tự động hóa nhận email có yêu cầu tài liệu, tự động trích xuất nội dung PDF, xử lý bằng AI (OpenRouter + SerpAPI), tạo báo cáo PDF branded với logo, font và styling doanh nghiệp, và gửi tự động qua email. Giảm thời gian xử lý từ 60 phút xuống 5 phút!"
slug: "tieu-dong-hoa-tao-bao-cao-pdf-branded-tu-email"
tags: [n8n, automation, no-code, ai-multimodal, autotype, openrouter, email-automation]
keywords: [n8n workflow pdf branded, tự động hóa báo cáo pdf, ai tạo tài liệu từ email, autype n8n, openrouter chatbot, trích xuất pdf tự động]
---

# 🚀 **Tự Động Hóa Tạo Báo Cáo PDF Branded Từ Email Nhập Lệch Với Autype & AI Multimodal**

### **Giải pháp cho các sếp:**
- **Tiết kiệm 90% thời gian** trong việc xử lý yêu cầu tài liệu từ khách hàng.
- **Chuyển đổi email thành báo cáo chuyên nghiệp** với logo, font và styling doanh nghiệp.
- **Tự động trích xuất nội dung PDF** bằng OCR + AI, không cần can thiệp thủ công.
- **Hoạt động 24/7** trên VPS riêng, không phụ thuộc vào nhân viên.

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian:** Từ 60 phút xử lý 1 yêu cầu xuống chỉ **5 phút** với AI tự động.
- **Chất lượng cao:** Báo cáo PDF được tạo với **logo, font, và styling doanh nghiệp** thống nhất.
- **Tự động hóa hoàn toàn:** Không cần can thiệp thủ công, hoạt động liên tục 24/7.
- **Tích hợp AI đa modal:** Sử dụng **OpenRouter (AI chat)**, **SerpAPI (tìm kiếm web)**, và **Firecrawl (scrape website)** để tạo nội dung chuyên nghiệp.
- **Dễ dàng mở rộng:** Thêm logic AI mới (so sánh tài liệu, tổng hợp, viết lại) mà không cần code.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản n8n Self-hosted** (không dùng n8n.cloud vì cần **n8n-nodes-autype** là node cộng đồng).
2. **API Keys:**
   - **Autype API Key** (trích xuất PDF và tạo PDF branded).
   - **OpenRouter API Key** (hoặc OpenAI/Anthropic) để xử lý AI.
   - **SerpAPI Key** (tìm kiếm web cho AI).
   - **Firecrawl API Key** (scrape website nếu cần).
3. **SMTP Credentials** (để gửi email trả lời tự động).
4. **Tài khoản Email IMAP** (để workflow theo dõi email nhập lệch).
5. **Node cộng đồng `n8n-nodes-autype`** (cài đặt trên n8n self-hosted).
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/14184](https://n8n.io/workflows/14184) hoặc copy/paste JSON vào **n8n Editor**.
- **Cách import:**
  1. Mở **n8n Editor** trên VPS.
  2. Nhấn **Import** → Chọn file JSON hoặc dán JSON vào ô **Import Workflow**.
  3. Chọn **Import** để lưu workflow.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **21 node**, nhưng các bước quan trọng cần chú ý:

#### **A. Cấu hình Email IMAP (Node: "New Email Received")**
- **Thiết lập IMAP:**
  - Điền **Host, Port, Username, Password** của tài khoản email (ví dụ: Gmail, Outlook).
  - **Inbox Name:** Đặt tên folder email cần theo dõi (ví dụ: "Inbox").
  - **Search Query:** `FROM:"client@example.com"` (để chỉ theo dõi email từ khách hàng).
- **Lưu ý:**
  - Nếu dùng Gmail, **bật "Less Secure Apps"** hoặc tạo **App Password** (nếu 2FA bật).
  - **Không** dùng tài khoản Gmail cá nhân (rủi ro bị block).

#### **B. Cấu hình Autype API (Node: "Upload PDF to Autype" & "Render Branded PDF")**
- **Tạo credential Autype:**
  1. Trong **Credentials** → **Add Credential** → Chọn **Autype API**.
  2. Điền **API Key** từ [Autype Dashboard](https://autype.com/).
- **Node "Autype Lens OCR":**
  - Sử dụng **HTTP Request** với **Header Auth** (không phải node Autype chính thức).
  - **Header Name:** `X-API-Key`
  - **Header Value:** API Key của Autype.
  - **Endpoint:** `https://api.autype.com/v1/ocr` (cần kiểm tra trên [Autype Docs](https://docs.autype.com/)).

#### **C. Cấu hình AI (OpenRouter, SerpAPI, Firecrawl)**
- **OpenRouter (Node: "OpenRouter Chat Model")**
  - Tạo credential **OpenRouter API** trong **Credentials** → **Add Credential** → **OpenRouter API**.
  - **Model:** `z-ai/glm-5` (hoặc model khác từ [OpenRouter](https://openrouter.ai/)).
- **SerpAPI (Node: "SerpAPI")**
  - Tạo credential **SerpAPI** với API Key từ [SerpAPI](https://serpapi.com/).
- **Firecrawl (Node: "/scrape in Firecrawl")**
  - Tạo credential **Firecrawl API** với API Key từ [Firecrawl](https://firecrawl.io/).

#### **D. Cấu hình SMTP (Node: "Send Report via Email")**
- **Thiết lập SMTP:**
  - **Host:** `smtp.gmail.com` (nếu dùng Gmail) hoặc `smtp.yourdomain.com`.
  - **Port:** `587` (cho TLS) hoặc `465` (cho SSL).
  - **Username/Password:** Tài khoản email gửi (nếu dùng Gmail, **bật "Less Secure Apps"**).
  - **From Email:** Địa chỉ email gửi (ví dụ: `no-reply@yourcompany.com`).

#### **E. Cấu hình Branding (Node: "Set Company Config")**
- **Điền thông tin branding:**
  - **Logo URL:** Link đến logo PNG/JPG của doanh nghiệp.
  - **Font:** Chọn font (ví dụ: `Arial`, `Roboto`).
  - **Colors:** Màu nền, text (ví dụ: `#0066cc`).
  - **Header/Footer:** Thêm thông tin như tên công ty, trang số.

---
### **3. Kích hoạt ⚡️**
1. **Test Run với email mẫu:**
   - Gửi email mẫu có **yêu cầu tài liệu** và **đính kèm PDF** vào inbox theo dõi.
   - Chạy **Test Run** trong n8n Editor để kiểm tra workflow.
2. **Bật Active:**
   - Sau khi test thành công, **bật Active** để workflow hoạt động tự động.

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::info[MỞ RỘNG THÊM TÍNH NĂNG]
- **Thêm Slack/Telegram Notifications:**
  - Sử dụng node **Slack Webhook** hoặc **Telegram Bot** để thông báo khi workflow hoàn thành.
- **Lưu Log vào Google Sheets/Notion:**
  - Sử dụng node **Google Sheets** hoặc **Notion API** để ghi lại lịch sử yêu cầu.
- **Tự động gửi báo cáo định kỳ:**
  - Sử dụng **n8n Schedule Node** để gửi báo cáo tổng hợp hàng tuần/tháng.
- **Cải thiện AI với Prompt Engineering:**
  - Tùy chỉnh **prompt** trong node **AI Document Assistant** để AI trả lời chính xác hơn.
- **Dùng AI để so sánh tài liệu:**
  - Thêm logic so sánh PDF bằng **LangChain Agent** để AI báo cáo sự khác biệt.
:::

---
## 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc thủ công, **tự động hóa hoàn toàn** quá trình tạo báo cáo PDF branded từ email nhập lệch. Với **AI Multimodal** (OpenRouter + SerpAPI + Firecrawl), báo cáo không chỉ được tạo nhanh mà còn **chuyên nghiệp, cá nhân hóa và có branding doanh nghiệp**.

**🚀 Hành động ngay:**
1. **Cài n8n Self-hosted** trên VPS (đăng ký [VPS TinoHost](https://tino.vn/vps-n8n?affid=388) với mã giảm **VPSN8N**).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Test với email mẫu** và bật **Active** để tự động hóa!

**💡 Lưu ý:** Workflow này **không hoạt động trên n8n.cloud** vì cần node cộng đồng `n8n-nodes-autype`. Các sếp cần **self-hosted** để sử dụng đầy đủ tính năng.

---