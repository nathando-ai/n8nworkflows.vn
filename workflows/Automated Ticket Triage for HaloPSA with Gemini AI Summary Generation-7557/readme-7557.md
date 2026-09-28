---
title: "🤖 **Tự Động Xử Lý Tickets HaloPSA Với Gemini AI – Tóm Tắt & Ghi Chú Tự Động 100% Không Code**"
description: "Workflow tự động hóa xử lý tickets từ HaloPSA bằng trí tuệ nhân tạo Gemini AI, tự động tạo tóm tắt, hướng dẫn giải quyết và ghi chú HTML cá nhân hóa – tiết kiệm thời gian cho các sếp MSP lên tới 80% trong việc quản lý hỗ trợ kỹ thuật."
slug: "tieu-ly-tickets-halopsa-voi-gemini-ai"
tags: [n8n, automation, no-code, ai-summarization, halopsa, gemini-ai, langchain, msp-automation]
keywords: [tự động hóa tickets halopsa, gemini ai n8n, xử lý hỗ trợ kỹ thuật tự động, tóm tắt ticket bằng ai, langchain n8n, workflow halopsa ai]
---

# 🚀 **Tự Động Xử Lý Tickets HaloPSA Với Gemini AI – Giải Pháp Tiết Kiệm Thời Gian Cho Các Sếp MSP**

### **Nỗi Đau Của Các Sếp MSP Hiện Nay**
Các sếp quản lý dịch vụ hỗ trợ kỹ thuật (MSP) thường phải:
- **Lặp đi lặp lại** việc đọc hàng chục tickets mỗi ngày, mất thời gian lên đến **3-5 giờ/ngày**.
- **Không có tóm tắt nhanh** để hiểu vấn đề một cách chính xác, dẫn đến thời gian phản hồi chậm.
- **Không cá nhân hóa** hướng dẫn giải quyết cho từng khách hàng, khiến trải nghiệm hỗ trợ trở nên lạnh nhạt.
- **Bị mất thông tin quan trọng** khi ghi chú thủ công, gây nhầm lẫn trong quá trình theo dõi.

**Workflow này giải quyết tất cả những vấn đề trên bằng trí tuệ nhân tạo Gemini AI**, tự động:
✅ **Tóm tắt** nội dung ticket thành văn bản ngắn gọn.
✅ **Đề xuất giải pháp** và hướng dẫn giải quyết vấn đề.
✅ **Tạo ghi chú HTML** với logo, màu sắc và thông tin cá nhân hóa.
✅ **Ghi chú tự động** vào HaloPSA, giúp các kỹ thuật viên nhanh chóng hiểu và xử lý ticket.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng thay vì dùng phiên bản cloud.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** – giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ sức mạnh cho workflow AI)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Giảm **80% thời gian** dành cho việc đọc và tóm tắt tickets.
- **Chính xác cao**: Gemini AI hiểu ngữ cảnh và đề xuất giải pháp **phù hợp với từng trường hợp**.
- **Cá nhân hóa**: Ghi chú HTML với **logo công ty, màu sắc và thông tin khách hàng**, làm trải nghiệm hỗ trợ chuyên nghiệp hơn.
- **Hoạt động liên tục**: Workflow chạy **24/7** mà không cần can thiệp thủ công.
- **Tối ưu hóa đội ngũ**: Kỹ thuật viên chỉ cần **xem tóm tắt và hướng dẫn** thay vì đọc toàn bộ ticket.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản HaloPSA** (để lấy **API Token** và **Actions Endpoint**).
✔ **API Key của Google Gemini** (hoặc mô hình LLM khác như OpenAI).
✔ **Webhook URL** trong HaloPSA (sẽ được tạo từ workflow).
✔ **Logo và màu sắc** của công ty (để cá nhân hóa ghi chú HTML).

---
:::note[Lưu ý quan trọng]
- **Không cần kiến thức code** – workflow đã sẵn sàng, chỉ cần cấu hình một số tham số.
- **Không cần cài đặt thêm** – chỉ cần **import JSON** và điền thông tin API.
- **Hoạt động với nhiều mô hình AI** (Gemini, OpenAI, Mistral...) – chỉ cần thay đổi node LLM.
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các bước đơn giản:
1. **Tải file JSON** từ [n8n.io/workflows/7557](https://n8n.io/workflows/7557).
2. **Mở n8n Editor** (trang chủ của n8n) và nhấn **"Import"** → Chọn file JSON.
3. **Hoặc copy/paste** toàn bộ JSON vào **Import Workflow** (nút ở góc phải).

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflows này có **10 node**, nhưng chỉ **5 node quan trọng** cần cấu hình kỹ:

##### **🔗 Webhook (HaloPSA → n8n)**
- **Phương thức**: **POST** (không thay đổi).
- **Path**: Thay đổi thành **một đường dẫn duy nhất** (ví dụ: `halopsa-new-ticket-ai`).
  ```yaml
  path: "halopsa-new-ticket-ai"
  ```
- **Cách lấy URL Production**:
  1. Sau khi import, **copy toàn bộ URL** từ node Webhook.
  2. **Dán vào HaloPSA**:
     - Trên HaloPSA → **Settings** → **Webhooks** → **Add New Webhook**.
     - **Payload Type**: `JSON`.
     - **URL**: Dán URL từ n8n.
     - **Trigger**: Chọn **"New Ticket"** (hoặc tùy chọn khác).
     - **Save**.

##### **🛡️ Guard (Lọc Ticket theo Team - Tùy Chọn)**
- **Nếu không muốn xử lý tất cả tickets**, cấu hình node này để **bỏ qua** team nào đó.
  ```javascript
  // Ví dụ: Bỏ qua team "Sales" (ID=6)
  if (json.teamId === "6" || json.teamName === "sales") {
    return { json: null }; // Skip ticket
  }
  ```
- **Nếu không cần lọc**, **xóa node này**.

##### **🤖 AI Agent (Gemini / LLM)**
- **Kết nối với node Google Gemini**:
  1. **Thêm node `Google Gemini Chat Model`** (nếu chưa có).
  2. **Kết nối** node `AI Agent` → **Language Model** → Chọn node Gemini.
  3. **Cấu hình API Key**:
     - Trên node **Google Gemini Chat Model**, điền **API Key** từ [Google AI Studio](https://makersuite.google.com/).
     - **Không cần thay đổi gì khác**.

##### **📄 Parse AI JSON (Chuyển JSON thành dữ liệu sử dụng)**
- **Không cần chỉnh sửa** – node này tự động **xóa dấu ```json``` và phân tích output** của AI thành:
  - `summary` (tóm tắt)
  - `next_step` (hướng dẫn tiếp theo)
  - `troubleshooting` (HTML)
  - `ticket_id`

##### **🌐 HTTP → HaloPSA (Gửi Ghi Chú Về Ticket)**
- **Thay đổi URL và Header**:
  ```yaml
  url: "https://TEN_DOMAIN_HALOPSA.api/actions"
  headers:
    Authorization: "Bearer API_TOKEN_HALOPSA"
  ```
  - **Lấy API Token**:
    - Trên HaloPSA → **Settings** → **API Keys** → **Create New Key**.
    - Chọn **Actions API** → **Copy Token**.
  - **Lấy Actions Endpoint**:
    - Trên HaloPSA → **Settings** → **API** → **Actions Endpoint** (thường là `https://tenhalo.api/actions`).

##### **🎨 Build AI HTML Note (Cá Nhân Hóa Ghi Chú)**
- **Thay đổi logo, màu sắc và footer** để phù hợp với brand của công ty:
  ```javascript
  // Ví dụ: Thay đổi màu nền và logo
  const noteHtml = `
    <div style="background-color: #f0f0f0; padding: 15px; border-radius: 5px;">
      <img src="https://logo-cong-ty.com/logo.png" width="100" style="margin-bottom: 10px;">
      <h3>Tóm tắt ticket #${ticketId}</h3>
      <p>${summary}</p>
      <h4>Hướng dẫn giải quyết:</h4>
      <div>${troubleshooting}</div>
      <footer style="margin-top: 20px; color: #666;">Công ty TNHH ABC - Hotline: 0123456789</footer>
    </div>
  `;
  ```

---

#### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run** với một ticket mẫu:
   - Gửi một ticket test từ HaloPSA → n8n.
   - Kiểm tra **output** của node `Parse AI JSON` và `Build AI HTML Note`.
2. **Bật Active**:
   - Nhấn **Active** trên canvas.
   - Kiểm tra **Logs** để đảm bảo không có lỗi.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack Webhook** sau node `Build AI HTML Note` để **báo cáo tự động** khi có ticket mới.
   - Cấu hình:
     ```yaml
     url: "https://hooks.slack.com/services/XXX"
     payload:
       text: "Ticket mới #{{$node["Extract Ticket"].json.id}}: {{ $node["Extract Ticket"].json.summary }}"
     ```

2. **Lưu Log Tickets**:
   - Thêm node **Google Sheets** hoặc **Notion** để **lưu lịch sử** tất cả tickets đã xử lý.
   - Cấu hình:
     ```yaml
     url: "https://sheets.googleapis.com/v4/spreadsheets/XXX/values/A1:B1?valueInputOption=RAW"
     headers:
       Authorization: "Bearer API_KEY_GOOGLE_SHEETS"
     payload:
       values: [
         ["Ticket ID", "{{ $node["Extract Ticket"].json.id }}"],
         ["Summary", "{{ $node["Extract Ticket"].json.summary }}"],
         ["AI Summary", "{{ $node["Parse AI JSON"].json.summary }}"]
       ]
     ```

3. **Gửi Báo Cáo Định Kỳ**:
   - Sử dụng **n8n Cron Trigger** để **tổng hợp báo cáo** hàng tuần/month về:
     - Số ticket mới.
     - Thời gian trung bình giải quyết.
     - Top vấn đề thường gặp.

4. **Thay Đổi Mô Hình AI**:
   - Nếu không muốn dùng **Gemini**, có thể **thay thế bằng OpenAI** hoặc **Mistral**:
     - Thêm node **`lmChatOpenAI`** hoặc **`lmChatMistral`**.
     - Kết nối với node **AI Agent** thay vì Gemini.

5. **Tự Động Phân Loại Ticket**:
   - Sử dụng **node Code** sau `Build AI Prompt` để **phân loại ticket** (Critical, Normal, Low) và gửi đến **team phù hợp**:
     ```javascript
     if (json.summary.includes("không mở máy")) {
       return { json: { team: "hardware" } };
     } else if (json.summary.includes("mạng chậm")) {
       return { json: { team: "network" } };
     }
     ```

---

### 📌 **Kết Luận**
Workflow **Automated Ticket Triage for HaloPSA** là **giải pháp hoàn hảo** cho các sếp MSP muốn:
✔ **Tiết kiệm thời gian** trong việc xử lý tickets.
✔ **Cải thiện chất lượng hỗ trợ** với tóm tắt và hướng dẫn từ AI.
✔ **Cá nhân hóa trải nghiệm** khách hàng với ghi chú HTML chuyên nghiệp.

**Hành động ngay hôm nay**:
1. **Import workflow** vào n8n của mình.
2. **Cấu hình API Key** và **URL HaloPSA**.
3. **Test với một ticket** và **bật Active** để tự động hóa toàn bộ quy trình!

**Nếu có vấn đề**, các sếp có thể:
- **Trả lời comment** dưới bài viết này.
- **Gửi tin nhắn** cho tôi trên [Facebook](https://facebook.com/robikorb) hoặc [LinkedIn](https://linkedin.com/in/robikorb).

**Chúc các sếp thành công với tự động hóa!** 🚀