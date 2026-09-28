---
title: "🚀 Tự Động Hoàn Hảo: Scrape Website Batch từ Google Sheets → Google Docs với Firecrawl (Không Cần Code)"
description: "Workflow tự động hóa 100% miễn phí giúp các sếp scrape nội dung từ hàng trăm trang web, chuyển đổi thành Google Docs có cấu trúc (Markdown), và tự động cập nhật tiến độ. Giúp tiết kiệm 10+ giờ/tháng cho công việc nghiên cứu thị trường, xây dựng knowledge base AI, hoặc phân tích đối thủ."
slug: "tieu-dong-hoan-hao-scrape-website-batch"
tags: [n8n, automation, no-code, document-extraction, multimodal-ai, google-sheets, google-drive, firecrawl, ai-chatbot]
keywords: [n8n workflow scrape website, tự động hóa scrape content, google sheets google docs automation, firecrawl n8n, xây dựng knowledge base AI, phân tích đối thủ cạnh tranh]
---

# 🚀 **Scrape Website Batch: Từ Google Sheets → Google Docs Tự Động (Không Cần Code)**

### **Nỗi Đau Của Các Sếp**
Các sếp đang phải **tốn thời gian vô cùng** để:
- **Thủ công scrape** nội dung từ hàng trăm trang web (E-commerce, FAQ, Blog, hoặc trang đối thủ).
- **Chuyển đổi** nội dung thô thành định dạng có cấu trúc (Markdown/Google Docs) để sử dụng cho **AI Chatbot**, **Knowledge Base**, hoặc **Phân tích SEO**.
- **Cập nhật thủ công** tiến độ trong Google Sheets, dẫn đến **sai sót** và **tốn thời gian**.

**Workflow này giải quyết tất cả!** Với **9 node đơn giản**, nó tự động:
✅ **Scrape** nội dung từ URL trong Google Sheets.
✅ **Chuyển đổi** thành **Google Docs có cấu trúc** (Markdown).
✅ **Tự động cập nhật** trạng thái trong Sheets (OK/Đã xử lý).
✅ **Tiết kiệm 10+ giờ/tháng** cho công việc nghiên cứu, xây dựng AI, hoặc phân tích đối thủ.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài **n8n trên VPS riêng (Self-hosted)** để tránh giới hạn của phiên bản miễn phí.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tháng** cho việc scrape và chuyển đổi nội dung.
- **Nội dung có cấu trúc** (Markdown) dễ dàng **đào tạo AI Chatbot** (Rasa, Dialogflow, LlamaIndex).
- **Tự động cập nhật tiến độ** trong Google Sheets → **không cần kiểm tra thủ công**.
- **Lưu trữ sạch sẽ** trong Google Drive với **tên file tự động** (từ URL).
- **Phân tích đối thủ** nhanh chóng bằng cách so sánh nội dung scraped.
:::

---

## 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản Google** (Google Sheets + Google Drive).
✔ **API Key Firecrawl** (đăng ký tại [Firecrawl](https://firecrawl.io/)).
✔ **Google Sheets mẫu** (cần có **cột URL** và **tab "Page to doc"**).
✔ **Google Drive folder** để lưu kết quả (mặc định: **"Contenu scrapé"**).

---
:::info[CHUẨN BỊ]
**Bước 1: Chuẩn bị Google Sheets**
- Tạo một **Google Sheet mới** và sao chép **tab "Page to doc"** từ [template mẫu](https://docs.google.com/spreadsheets/d/1ry3xvQ9UqM2Rf9C4-AoJdg1lfB9inh_5/edit).
- Điền **URL** vào cột **A** (cột đầu tiên).
- **Cột B** sẽ tự động cập nhật trạng thái (**OK** khi scrape thành công).

**Bước 2: Cấu hình API & Credentials**
Trong **n8n Editor**, thêm **3 credentials**:
1. **Firecrawl API** (điền `API Key` từ Firecrawl).
2. **Google Sheets OAuth2** (đăng nhập Google và cấp quyền).
3. **Google Drive OAuth2** (đăng nhập Google và cấp quyền).
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/7384).
- Trong **n8n Editor**, nhấn **Import** → Chọn file JSON.
- **Hoặc** copy toàn bộ JSON và **paste** vào **Import Workflow** (tab bên trái).

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
#### **A. Cấu Hình Node "Get URL" (Lấy URL từ Google Sheets)**
- **Credentials**: Chọn `googleSheetsOAuth2Api` (đã cấu hình trước).
- **Sheet Name**: Đặt thành **"Page to doc"** (hoặc tên tab của các sếp).
- **Range**: Đặt thành `"Page to doc!A:B"` (cột A: URL, cột B: Trạng thái).

#### **B. Cấu Hình Node "Row not empty" (Lọc bỏ dòng trống)**
- **Filter Query**: Đặt thành:
  ```json
  { "URL": { "operator": "isNotEmpty" } }
  ```
  (Lọc bỏ dòng không có URL).

#### **C. Cấu Hình Node "Scraping" (Firecrawl)**
- **Credentials**: Chọn `firecrawlApi`.
- **URL**: Sử dụng **`$node["Get URL"].json[].URL`** (đường dẫn từ node trước).
- **Operation**: Đặt thành **"scrape"**.
- **Optional**: Thêm **`waitTime: 5000`** (chờ 5 giây để tránh bị block).

#### **D. Cấu Hình Node "Create file markdown scraping" (Tạo Google Docs)**
- **Credentials**: Chọn `googleDriveOAuth2Api`.
- **Folder ID**: Đặt thành **ID folder của các sếp** (mặc định: `1ry3xvQ9UqM2Rf9C4-AoJdg1lfB9inh_5`).
- **File Name**: Sử dụng **`$node["Scraping"].json[].url`** (tên file tự động từ URL).
- **Content**: Sử dụng **`$node["Scraping"].json[].content`** (nội dung Markdown).

#### **E. Cấu Hình Node "Scraped : OK" (Cập nhật trạng thái)**
- **Credentials**: Chọn `googleSheetsOAuth2Api`.
- **Sheet Name**: **"Page to doc"**.
- **Range**: `"Page to doc!B2:B"` (cập nhật cột trạng thái).
- **Update Values**: Đặt thành **"OK"** (trạng thái đã scrape thành công).

---
### **3. Kích Hoạt ⚡️**
- **Test Run**: Nhấn **Run Workflow** với **1-2 URL mẫu** để kiểm tra.
- **Bật Active**: Sau khi kiểm tra thành công, **bật Active** để chạy tự động.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram**
   - Thêm node **Slack/Telegram Webhook** để **báo cáo tiến độ** khi scrape xong.
   - Ví dụ: `"Scrape hoàn tất: [URL](link)"`.

2. **Lưu Log Scrape**
   - Thêm node **Google Sheets** mới để **lưu chi tiết lỗi** (nếu scrape thất bại).
   - Cột: `URL`, `Status`, `Error`, `Timestamp`.

3. **Gửi Báo Cáo Định Kỳ**
   - Sử dụng **n8n Cron Trigger** để **gửi email báo cáo** hàng tuần.
   - Nội dung: **"Danh sách URL đã scrape: [Link Google Drive]"**.

4. **Tối Ưu Hiệu Suất**
   - Nếu scrape nhiều URL, **tăng `waitTime`** (ví dụ: 10 giây) để tránh bị block.
   - **Sử dụng Firecrawl Pro** (nếu có budget) để tăng tốc độ scrape.

---

## 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào **strategy** thay vì công việc thủ công. **Dùng ngay để:**
✔ **Xây dựng Knowledge Base AI** từ nội dung web.
✔ **Phân tích đối thủ** nhanh chóng.
✔ **Tự động hóa nghiên cứu thị trường**.

**Bắt đầu ngay!** Import workflow, cấu hình credentials, và **chạy tự động** trong vài phút.

---
**💡 Cần hỗ trợ?** Đăng ký **VPS n8n** từ [TinoHost](https://tino.vn/vps-n8n?affid=388) để workflow **chạy 24/7** mà không bị giới hạn!