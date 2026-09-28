---
title: "🤖 Tự Động Hoá Cuộc Hỏi Dò Đánh Giá Sản Phẩm Với Telegram, Google Sheets & AI - N8n Workflow Hiệu Quả"
description: "Workflow này tự động hóa cuộc hỏi dò đánh giá sản phẩm thông minh bằng AI, kết hợp Telegram và Google Sheets để thu thập phản hồi chi tiết từ khách hàng. Giúp các sếp tiết kiệm thời gian, nhận được dữ liệu chính xác và cá nhân hóa trải nghiệm."
slug: "tự-dộng-hoá-cuộc-hỏi-dò-đánh-giá-sản-phẩm"
tags: [n8n, automation, ai-powered, google-sheets, telegram-bot, no-code, chatbot-survey]
keywords: [n8n workflow tự động hóa, hỏi dò đánh giá sản phẩm, chatbot AI, Google Sheets tự động, Telegram bot tự động, tự động hóa doanh nghiệp]
---

# 🚀 **Tự Động Hoá Cuộc Hỏi Dò Đánh Giá Sản Phẩm Với Telegram, Google Sheets & AI**

### **Giải Phóng Tay Các Sếp Từ Cuộc Hỏi Dò Thủ Công!**
Hỏi dò đánh giá sản phẩm là một trong những công việc tốn thời gian nhất của các sếp marketing và sản phẩm. Thay vì phải gửi email, gọi điện hoặc chat một cách thủ công, **Workflow này tự động hóa toàn bộ quá trình** bằng cách kết hợp:
- **Telegram Bot** để tương tác với khách hàng một cách tự động và thân thiện.
- **Google Sheets** để lưu trữ và phân tích kết quả một cách dễ dàng.
- **AI Agent (GPT-4o-mini)** để hỏi thêm câu hỏi theo phản hồi của khách hàng, giúp thu thập **đữ liệu sâu sắc hơn** so với các phương pháp truyền thống.

Kết quả? **Tiết kiệm 80% thời gian**, **giảm sai sót**, và **nâng cao chất lượng phản hồi** nhờ khả năng tương tác tự nhiên của AI.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần phải chat hoặc gọi điện với từng khách hàng.
- **Phản hồi sâu sắc**: AI tự động hỏi thêm câu hỏi theo từng phản hồi, giúp thu thập **đữ liệu chi tiết** hơn.
- **Lưu trữ tự động**: Tất cả kết quả được ghi vào **Google Sheets** một cách tự động.
- **Trải nghiệm cá nhân hóa**: Khách hàng có thể **bắt đầu lại** hoặc **bỏ qua câu hỏi** nếu muốn.
- **Hoạt động liên tục**: Workflow chạy 24/7, không cần can thiệp của con người.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Telegram Bot**:
   - Tạo bot trên [@BotFather](https://t.me/BotFather) và lấy **API Key**.
   - Cài đặt **n8n Telegram Credential** trong n8n Editor.
2. **Google Sheets**:
   - Tạo một bảng Google Sheets với **cột ID** (để theo dõi session) và các **câu hỏi hỏi dò** (dựa vào mẫu [đây](https://docs.google.com/spreadsheets/d/e/2PACX-1vQWcREg75CzbZd8loVI12s-DzSTj3NE_02cOCpAh7umj0urazzYCfzPpYvvh7jqICWZteDTALzBO46i/pubhtml?gid=0&single=true)).
   - Cài đặt **Google Sheets OAuth2 Credential** trong n8n Editor.
3. **Redis (để lưu trạng thái)**:
   - Tạo một instance Redis miễn phí trên [Upstash](https://upstash.com?ref=jimleuk) hoặc tự host.
   - Cài đặt **Redis Credential** trong n8n Editor.
4. **API Key OpenAI (nếu sử dụng GPT-4o-mini)**:
   - Nếu muốn AI hỏi thêm câu hỏi theo phản hồi, cần **API Key OpenAI** (tùy chọn).
   - Cài đặt **OpenAI Credential** trong n8n Editor.
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/3115) và import vào n8n Editor.
- **Copy/Paste JSON** từ file vào n8n Editor (đảm bảo không có lỗi syntax).

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **33 node**, nhưng các sếp chỉ cần chú ý đến các node quan trọng sau:

##### **A. Cấu Hình Telegram Bot**
- **Node "Telegram Trigger"**:
  - Đảm bảo **credentials** là `telegramApi` đã được cài đặt.
  - Thiết lập **chat ID** của bot (có thể lấy từ [@userinfobot](https://t.me/userinfobot)).
- **Node "Send Start", "Send Next Question", "Send Response", "Completed Survey"**:
  - Chỉnh **text template** để phù hợp với brand của các sếp (ví dụ: thay đổi tên sản phẩm, logo...).

##### **B. Cấu Hình Google Sheets**
- **Node "Get Columns1" và "Get Record1"**:
  - Điền **Google Sheets ID** vào `sheetId` (lấy từ URL của bảng Sheets).
  - Chọn **Sheet Name** (trong ví dụ là "Sheet1").
- **Node "Create Record1" và "Create Record2"**:
  - Đảm bảo **credentials** là `googleSheetsOAuth2Api`.
  - Cấu hình **headers** để tránh lỗi CORS (nếu cần).

##### **C. Cấu Hình Redis (Lưu Trạng Thái)**
- **Node "Start Session1", "Get State2", "Get State3", "Increment Index1"**:
  - Đảm bảo **credentials** là `redis` đã được cài đặt.
  - Key Redis mặc định là `survey_state:{userId}` và `survey_index:{userId}`.

##### **D. Cấu Hình AI Agent (Tùy Chọn)**
- **Node "Interview Agent1"**:
  - Nếu muốn AI hỏi thêm câu hỏi, cần **API Key OpenAI** (đặt vào `openAiApi`).
  - Cấu hình **prompt** trong `agent` để phù hợp với sản phẩm của các sếp.
- **Node "Model2" và "Model3"**:
  - Chọn mô hình **gpt-4o-mini** (hoặc mô hình khác nếu có).

##### **E. Cấu Hình Logic Hỏi Dò**
- **Node "Should Follow Up?1" (Text Classifier)**:
  - Cấu hình **rules** để phân loại câu trả lời (ví dụ: nếu câu trả lời dài > 50 ký tự, AI hỏi thêm).
- **Node "Is Survey Continue?" (If Condition)**:
  - Đảm bảo logic kiểm tra **index cuối cùng** của câu hỏi trong Google Sheets.

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Gửi tin nhắn `/start` đến bot Telegram và kiểm tra:
    - Bot có bắt đầu cuộc hỏi dò không?
    - AI có hỏi thêm câu hỏi theo phản hồi không?
    - Dữ liệu có được ghi vào Google Sheets không?
- **Bật Active**:
  - Sau khi test thành công, bật **Active** cho workflow.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram Group**:
   - Thay vì chat 1:1, các sếp có thể chia sẻ link bot vào **Slack/Telegram Group** để nhiều người tham gia cùng lúc.

2. **Gửi Báo Cáo Định Kỳ**:
   - Sử dụng **n8n Schedule Node** để tự động gửi **báo cáo tổng hợp** từ Google Sheets vào email hoặc Slack hàng tuần.

3. **Lưu Log Cuộc Hỏi Dò**:
   - Thêm **n8n-nodes-base.httpRequest** để gửi dữ liệu vào **Google Drive** hoặc **Firebase** để lưu trữ lâu dài.

4. **Cá Nhân Hóa Trải Nghiệm**:
   - Thêm **n8n-nodes-base.telegram** để gửi **cảm ơn** hoặc **quà tặng** (ví dụ: mã giảm giá) cho khách hàng hoàn thành cuộc hỏi dò.

5. **Dịch Workflow Sang WhatsApp**:
   - Thay thế tất cả **Telegram Node** bằng **WhatsApp Node** (n8n có hỗ trợ).

---

### 📌 **Kết Luận**
Workflow này không chỉ **tự động hóa** cuộc hỏi dò đánh giá sản phẩm mà còn **tăng cường trải nghiệm khách hàng** nhờ AI. Các sếp có thể:
✅ **Tiết kiệm thời gian** từ công việc thủ công.
✅ **Thu thập dữ liệu sâu sắc** hơn.
✅ **Phân tích nhanh chóng** trên Google Sheets.
✅ **Cá nhân hóa tương tác** với khách hàng.

**Hãy thử ngay và cải thiện chất lượng sản phẩm của mình!** 🚀

---
**Cần hỗ trợ?**
- **Join Discord n8n**: [https://discord.com/invite/XPKeKXeB7d](https://discord.com/invite/XPKeKXeB7d)
- **Hỏi trên Forum**: [https://community.n8n.io/](https://community.n8n.io/)