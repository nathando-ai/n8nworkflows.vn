---
title: "🚀 SEO Domain Audit Tự Động Hóa 360°: Từ Dữ Liệu → Chiến Lược 90 Ngày Với SE Ranking + Claude AI"
description: "Workflow tự động hóa SEO domain audit toàn diện, kết hợp SE Ranking và Claude AI để phân tích kỹ thuật, backlink, từ khóa, AI visibility và đối thủ cạnh tranh, sau đó tự động tổng hợp chiến lược 90 ngày. Giúp các sếp SEO tiết kiệm 10-15 giờ/tháng và đưa ra quyết định dựa trên dữ liệu chính xác."
slug: "seo-domain-audit-tu-dong-hoa-se-ranking-claude-ai"
tags: [n8n, automation, seo, ai-chatbot, se-ranking, anthropic, google-sheets, google-drive]
keywords: [n8n workflow seo, tự động hóa audit seo, se ranking api, claude ai seo, chiến lược seo tự động, domain audit với ai, seo automation no-code]
---

# **🚀 SEO Domain Audit Tự Động Hóa: Từ Dữ Liệu → Chiến Lược 90 Ngày Với SE Ranking + Claude AI**

## **🔍 Nỗi Đau Của Các Sếp SEO Hiện Nay**
Hàng ngày, các sếp SEO phải:
- **Tốn thời gian** để thu thập dữ liệu từ nhiều nguồn (SE Ranking, Ahrefs, Moz...) và so sánh thủ công với đối thủ.
- **Không có chiến lược thống nhất** vì phân tích kỹ thuật, từ khóa, backlink và AI visibility thường được xem riêng rẽ.
- **Phải viết báo cáo** từ đầu, mất nhiều giờ để tổng hợp và trình bày cho khách hàng.
- **Không biết ưu tiên** những công việc nào trong chiến lược SEO 90 ngày vì thiếu phân tích toàn diện.

**Workflow này giải quyết tất cả!** Với **SE Ranking + Claude AI**, bạn chỉ cần nhập domain, hệ thống sẽ tự động:
✅ **Phân tích kỹ thuật** (Core Web Vitals, lỗi crawl, tốc độ trang)
✅ **Tìm kiếm từ khóa cạnh tranh** và cơ hội mới
✅ **Xem xét backlink profile** và anchor text
✅ **Đánh giá AI visibility** trên ChatGPT, Perplexity, Gemini...
✅ **Tự động tổng hợp chiến lược 90 ngày** với ưu tiên rõ ràng

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10-15 giờ/tháng** so với cách làm thủ công.
- **Chiến lược SEO chính xác** dựa trên phân tích AI từ 5 chuyên gia (kỹ thuật, backlink, từ khóa, AI visibility).
- **Báo cáo tự động** được lưu trên Google Drive và Google Sheets, dễ chia sẻ với khách hàng.
- **Theo dõi đối thủ** một cách tự động, không cần update thủ công.
- **Cải thiện AI visibility** bằng cách tối ưu nội dung cho các engine AI mới nổi.
:::

---
### **🔧 Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần:
1. **n8n Self-hosted** (không dùng phiên bản cloud để đảm bảo bảo mật và hoạt động 24/7).
2. **API Key SE Ranking**:
   - Đăng ký tại [SE Ranking](https://online.seranking.com/admin.api.dashboard.html) và lấy token API.
3. **API Key Anthropic (Claude)**:
   - Đăng ký tại [Anthropic](https://www.anthropic.com/) và lấy API key.
4. **Tài khoản Google Drive & Google Sheets** (để lưu báo cáo).
5. **Node SE Ranking cho n8n** (phiên bản 1.3.5+):
   - Cài đặt từ npm: `npm install @seranking/n8n-nodes-seranking@latest`.
:::

---
### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/13373](https://n8n.io/workflows/13373) hoặc copy/paste JSON vào **n8n Editor**.
- **Nhấn "Import"** và chọn **Self-hosted instance**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **27 node**, nhưng có **5 node quan trọng nhất** cần cấu hình cẩn thận:

##### **A. Cấu Hình Credentials (API Keys)**
- **SE Ranking API**:
  - Trong **Credentials Manager** của n8n, tạo mới credential với tên `seRankingApi`.
  - Điền **API Token** từ SE Ranking vào trường `apiToken`.
- **Anthropic (Claude)**:
  - Tạo credential mới với tên `anthropicApi`.
  - Điền **API Key** từ Anthropic vào trường `apiKey`.
- **Google Drive & Sheets**:
  - Tạo credential OAuth2 với tên `googleDriveOAuth2Api` và `googleSheetsOAuth2Api`.
  - Chọn quyền **Drive** và **Sheets** tương ứng.

##### **B. Cấu Hình Node "Domain Input Form"**
- **Thêm trường tùy chọn** (nếu cần):
  - Mở node `Domain Input Form` → **Edit** → **Fields**.
  - Thêm trường `businessDescription` và `targetMarket` để cung cấp thêm bối cảnh cho AI.

##### **C. Cấu Hình Node "Claude Sonnet & Opus"**
- **Model Claude**:
  - Node `Claude Sonnet` và `Claude Opus` đã được cấu hình sẵn với phiên bản mới nhất.
  - **Không cần chỉnh** trừ khi muốn thay đổi model (ví dụ: `claude-3-opus-20240229`).
- **Prompt Optimization**:
  - Nếu muốn **tối ưu hóa prompt** cho AI, mở node `Format Data for AI Agents` (type `code`) và chỉnh sửa logic để truyền dữ liệu rõ ràng hơn.

##### **D. Cấu Hình Node "Save to Google Sheets"**
- **Chọn Sheet và Range**:
  - Trong node `Save to Google Sheets`, chọn:
    - **Google Sheets ID** (từ liên kết share của sheet).
    - **Sheet Name** (ví dụ: `SEO_Audit_Results`).
    - **Range** (ví dụ: `A1` để ghi từ ô A1).

##### **E. Kích Hoạt Workflow**
- **Test Run**:
  - Nhập một domain mẫu (ví dụ: `example.com`).
  - Chạy workflow và kiểm tra **Google Drive** để xem báo cáo tự động được tạo.
- **Bật Active**:
  - Sau khi kiểm tra thành công, **bật workflow** để hoạt động liên tục.

---
### **✍️ Mẹo & Gợi Ý Nâng Cao**
:::note[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Thêm Notifications Slack/Telegram**:
   - Sau node `Save report to Google Drive`, thêm node **Slack Webhook** hoặc **Telegram Bot** để thông báo khi báo cáo hoàn tất.
   - **Cách làm**:
     ```json
     {
       "nodeType": "n8n-nodes-base.slack",
       "name": "Notify Slack",
       "options": {
         "webhookUrl": "https://hooks.slack.com/services/...",
         "message": "🚀 SEO Audit hoàn tất! Kết quả đã lưu tại: {{ $node["Save report to Google Drive"].json["fileLink"] }}"
       }
     }
     ```
2. **Lưu Log Lịch Sử Audit**:
   - Thêm node **Google Sheets** sau `Save report to Google Drive` để ghi lại lịch sử domain đã audit.
   - **Cấu hình**:
     - Sheet mới: `SEO_Audit_History`
     - Cột: `Domain`, `Date`, `Status`, `Report Link`.
3. **Tự Động Update Báo Cáo Định Kỳ**:
   - Sử dụng **n8n Trigger (Schedule)** để chạy workflow hàng tháng tự động.
   - **Cách làm**:
     - Tạo một **Schedule Node** với thời gian chạy (ví dụ: ngày đầu tháng).
     - Kết nối với node `Domain Input Form` để nhập domain cũ.
4. **Thay Thế Claude bằng GPT-4o (OpenAI)**:
   - Nếu muốn giảm chi phí, thay thế node `lmChatAnthropic` bằng `n8n-nodes-base.llmChatOpenAI`.
   - **Cấu hình**:
     - Tạo credential `openaiApi` với API Key OpenAI.
     - Thay đổi model từ `claude-sonnet` sang `gpt-4o`.
5. **Tích Hợp với Notion**:
   - Thay vì Google Drive, lưu báo cáo vào **Notion Database** bằng node `n8n-nodes-base.notion`.
   - **Ưu điểm**: Dễ dàng chia sẻ và theo dõi trong Notion.
:::

---
### **📌 Kết Luận**
Workflow này không chỉ **tự động hóa audit SEO** mà còn **tự động tổng hợp chiến lược** từ dữ liệu thực tế, giúp các sếp:
✔ **Tiết kiệm thời gian** lên đến 80% so với cách làm thủ công.
✔ **Nhận báo cáo chuyên nghiệp** chỉ trong vài phút.
✔ **Cập nhật liên tục** về đối thủ và xu hướng AI search.

**Hành động ngay!**
1. **Cài đặt n8n Self-hosted** trên VPS (👉 [TinoHost](https://tino.vn/vps-n8n?affid=388) với mã giảm **VPSN8N**).
2. **Import workflow** và cấu hình API keys.
3. **Nhập domain đầu tiên** và xem kết quả magi!

**💡 Lưu ý**: Nếu gặp khó khăn trong quá trình setup, các sếp có thể tham khảo [hướng dẫn chi tiết của SE Ranking](https://online.seranking.com/blog/seo-audit/) hoặc liên hệ hỗ trợ n8n tại [n8n Community](https://community.n8n.io/).

---
**🚀 Chúc các sếp thành công với chiến lược SEO tự động hóa!** 🚀