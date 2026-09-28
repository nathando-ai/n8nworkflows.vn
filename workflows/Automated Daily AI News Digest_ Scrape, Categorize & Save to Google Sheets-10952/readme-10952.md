---
title: "🤖 **Tự Động Hóa Báo Cáo Tin Tức AI Hàng Ngày: Trích Xuất, Phân Loại & Lưu Trữ Google Sheets**"
description: "Workflow tự động hóa hoàn toàn không cần code để trích xuất, tóm tắt và phân loại tin tức AI từ email hàng ngày, sau đó lưu kết quả vào Google Sheets với định dạng chuyên nghiệp. Giúp các sếp tiết kiệm 10+ giờ/tháng và theo dõi xu hướng AI một cách hệ thống."
slug: "tieu-dong-hoa-bao-cao-tin-tuc-ai-hang-ngay"
tags: [n8n, automation, no-code, ai-summarization, google-sheets, scrapegraphai, openai, gemini]
keywords: [n8n workflow tự động hóa tin tức AI, trích xuất tin tức từ email, phân loại tin tức bằng AI, lưu tin tức vào Google Sheets, tự động hóa báo cáo hàng ngày]
---

# 🚀 **Tự Động Hóa Báo Cáo Tin Tức AI Hàng Ngày: Trích Xuất, Phân Loại & Lưu Trữ Google Sheets**

### **Nỗi Đau Của Các Sếp**
Các sếp trong lĩnh vực **AI, Marketing, hoặc Tech** thường phải mất **10-15 giờ/tuần** để:
- **Lọc và đọc** tin tức từ email hàng ngày (như AlphaSignal, AI Newsletter, hoặc các nguồn khác).
- **Tóm tắt** nội dung dài dòng thành những điểm chính.
- **Phân loại** tin tức theo chủ đề (AI Generative, Robotics, Data Science, etc.).
- **Lưu trữ** kết quả một cách có hệ thống để theo dõi xu hướng.

**Kết quả?** Thời gian quý giá bị "chôn vùi" trong công việc thủ công, còn dữ liệu lại rải rác, khó theo dõi.

---
### **🎯 Giải Pháp: Workflow Tự Động Hóa 100% Không Code**
Workflow này **tự động hóa toàn bộ quy trình** từ trích xuất tin tức đến phân loại và lưu trữ vào **Google Sheets**, giúp các sếp:
✅ **Tiết kiệm 10+ giờ/tháng** chỉ với một workflow.
✅ **Tóm tắt và phân loại tin tức** bằng AI (Gemini + OpenAI).
✅ **Lưu trữ dữ liệu có cấu trúc** để phân tích xu hướng AI.
✅ **Cập nhật liên tục** mà không cần can thiệp thủ công.

---
### **🔧 Yêu Cầu Cần Thiết**
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Gmail** (để lấy email tin tức AI hàng ngày).
2. **API Keys & Credentials**:
   - **Google Gemini API** (để tóm tắt và phân loại tin tức).
   - **OpenAI API** (để hỗ trợ phân loại).
   - **ScrapeGraphAI API** (để trích xuất nội dung từ URL).
   - **Google Sheets OAuth2** (để lưu kết quả).
3. **Google Sheet mẫu** (đã được cung cấp [ở đây](https://docs.google.com/spreadsheets/d/15VKWMbd2cOb74uwYncfXkwLZam-dXD5sBiAttVpKIQw/edit?usp=sharing)).

---
### **🚀 Cách Import & Cấu Hình Workflow**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/10952](https://n8n.io/workflows/10952) hoặc copy/paste JSON vào **n8n Editor**.
- **Nhấn "Import"** và chọn **Self-hosted n8n** (nếu dùng VPS).

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

#### **2. Các Bước Cấu Hình BẮT BUỘC**
Workflow gồm **11 node**, nhưng các bước quan trọng nhất như sau:

##### **📌 Bước 1: Lấy Email & Chuyển Sang Markdown**
- **Node "Get email"** (Gmail):
  - Chọn **credentials**: `gmailOAuth2` (đã cấu hình trước).
  - Cấu hình:
    - **Sender**: Địa chỉ email của tin tức AI (ví dụ: `alphasignal@email.com`).
    - **Label**: Nếu email có nhãn, chọn vào đó.
    - **Limit**: 1 email (để lấy tin tức mới nhất).

- **Node "Convert HTML to MD"**:
  - Chuyển nội dung HTML của email sang **Markdown** (dễ xử lý cho AI).

##### **📌 Bước 2: Trích Xuất Bài Viết & Tạo JSON**
- **Node "Scrape"** (ScrapeGraphAI):
  - Chọn **credentials**: `scrapegraphAIApi` (API key từ [ScrapeGraphAI](https://dashboard.scrapegraphai.com/)).
  - **Input**: Dữ liệu Markdown từ bước trước.
  - **Output**: JSON chứa danh sách bài viết với URL, tiêu đề, nội dung.

- **Node "Scrape Agent"** (Agent):
  - Sử dụng **Gemini AI** để trích xuất và tóm tắt bài viết.
  - **Input**: JSON từ node "Scrape".
  - **Output**: JSON đã được **tóm tắt và chuẩn hóa**.

##### **📌 Bước 3: Phân Loại & Lưu Trữ**
- **Node "Categorization Chain"** (OpenAI):
  - Phân loại bài viết theo **chủ đề AI** (Generative AI, Robotics, Data Science, etc.).
  - **Input**: JSON từ node "Scrape Agent".
  - **Output**: JSON thêm cột `category`.

- **Node "Short url"** (HTTP Request):
  - Chuyển URL dài thành **URL ngắn** (ví dụ: `bit.ly/...`).
  - **Input**: URL từ JSON.
  - **Output**: URL ngắn.

- **Node "Add article to sheet"** (Google Sheets):
  - **Credentials**: `googleSheetsOAuth2Api`.
  - **Sheet ID**: `15VKWMbd2cOb74uwYncfXkwLZam-dXD5sBiAttVpKIQw` (hoặc clone sheet mẫu).
  - **Operation**: `append` (thêm dữ liệu mới vào sheet).
  - **Data**: Tiêu đề, tóm tắt, chủ đề, URL ngắn.

---
#### **3. Kích Hoạt Workflow ⚡️**
- **Test Run**:
  - Nhấn **"Run Workflow"** với dữ liệu mẫu (email tin tức AI).
  - Kiểm tra kết quả trong **Google Sheets**.
- **Bật Active**:
  - Sau khi kiểm tra thành công, **bật workflow** để chạy tự động hàng ngày.

---
### **✍️ Mẹo & Gợi Ý Nâng Cao**
1. **Tự động hóa gửi báo cáo hàng tuần**:
   - Sử dụng **node Email** (Gmail) để gửi **tóm tắt báo cáo** cho team hàng tuần.
2. **Lưu log hoạt động**:
   - Thêm **node StickyNote** để ghi lại lỗi hoặc thông tin debug.
3. **Kết hợp với Slack/Telegram**:
   - Sử dụng **node Webhook** để thông báo khi có tin tức mới.
4. **Tùy chỉnh chủ đề phân loại**:
   - Cập nhật **prompt** trong node "Categorization Chain" để phù hợp với nhu cầu cụ thể.

---
### **📌 Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào **strategy và phân tích** thay vì công việc thủ công. Với **AI tóm tắt và phân loại**, dữ liệu trở nên **chuyên nghiệp, có hệ thống và dễ theo dõi**.

**🚀 Hành động ngay!**
1. **Import workflow** vào n8n của mình.
2. **Cấu hình credentials** theo hướng dẫn.
3. **Bật workflow** và bắt đầu tự động hóa báo cáo AI hàng ngày!

---
**💡 Cần hỗ trợ thêm?**
- **Tạo issue** trên [n8n Community](https://community.n8n.io/).
- **Liên hệ tác giả**: [Davide Boizza](https://linkedin.com/in/davideboizza) (info@n3w.it).