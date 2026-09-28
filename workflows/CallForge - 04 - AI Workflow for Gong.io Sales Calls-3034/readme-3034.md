---
title: "🤖 **Tự Động Hóa Phân Tích Cuộc Gọi Sales với AI: AI Workflow cho Gong.io trên n8n**"
description: "Tự động hóa phân tích cuộc gọi bán hàng từ Gong.io, trích xuất thông tin quan trọng, lưu trữ trên Notion và báo cáo tiến trình trên Slack - giải pháp không cần code cho đội ngũ Sales & Marketing."
slug: "tieu-dong-hoa-phan-tich-cuoc-noi-gong-io-voi-ai-n8n"
tags: [n8n, automation, sales, ai, gong.io, notion, slack, no-code]
keywords: [tự động hóa gong.io, phân tích cuộc gọi sales, ai workflow n8n, lưu trữ thông tin trên notion, báo cáo tiến trình slack, tự động hóa không code]
---

# 🚀 **Tự Động Hóa Phân Tích Cuộc Gọi Sales với AI: AI Workflow cho Gong.io trên n8n**

### **Giải pháp cho các sếp Sales & Marketing:**
Bạn đã từng phải mất **giờ đồng hồ** để thủ công ghi chép lại những điểm quan trọng từ cuộc gọi bán hàng? Hay phải tra cứu lại thông tin từ hàng trăm cuộc gọi để báo cáo cho lãnh đạo? **CallForge** - workflow này sẽ **tự động hóa toàn bộ quá trình**, trích xuất thông tin từ cuộc gọi trên **Gong.io**, lưu trữ trên **Notion** và báo cáo tiến trình trên **Slack** - **không cần viết một dòng code nào!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính riêng tư và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian:** Không còn phải nghe lại cuộc gọi nhiều lần để ghi chép.
✅ **Dữ liệu chính xác:** AI tự động trích xuất thông tin quan trọng như **tên khách hàng, nhu cầu, đối thủ cạnh tranh, cơ hội bán hàng**.
✅ **Lưu trữ hệ thống:** Thông tin được lưu trên **Notion** với cấu trúc logic, dễ dàng chia sẻ cho các bộ phận khác (Marketing, Product, CS).
✅ **Báo cáo tự động:** Tiến trình xử lý được cập nhật **thực thời trên Slack**, giúp đội ngũ theo dõi hiệu quả.
✅ **Khả năng mở rộng:** Dễ dàng kết nối với **LLM (AI Chatbot)** để phân tích sâu hơn.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Gong.io** (để lấy dữ liệu cuộc gọi).
✔ **API Key Notion** (để tạo và cập nhật database).
✔ **Webhook Slack** (để gửi thông báo tiến trình).
✔ **Workflow con (Subworkflow) cho AI Processing** (nếu muốn sử dụng AI phân tích sâu).
✔ **Credentials cho n8n** (cấu hình trong n8n Dashboard):
   - `notionApi` (Notion API Key)
   - `slackApi` (Slack Token)

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/3034](https://n8n.io/workflows/3034) và import vào **n8n Editor**.
- **Cách 2:** Copy toàn bộ JSON từ [đây](https://uploads.n8n.io/templates/callforgeshadow.json) và paste vào **n8n Editor** → **Import Workflow**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **18 node**, nhưng các bước quan trọng nhất cần chú ý:

##### **A. Cấu hình Notion Database**
- **Node:** `Create Notion DB Page`
  - **Tham số cần điền:**
    - `Database ID` (lấy từ Notion → Database Settings → Copy ID).
    - `Properties` (cấu trúc dữ liệu, ví dụ: `Call ID`, `Customer Name`, `Key Insights`).
  - **Lưu ý:** Nếu Notion bị **rate limiting**, workflow sẽ tự động **bỏ qua cuộc gọi đó** và tiếp tục với cuộc gọi tiếp theo.

##### **B. Kết nối Slack cho báo cáo tiến trình**
- **Node:** `Post Slack Receipt`, `Update Slack Progress`, `Post Completed Calls Message`
  - **Tham số cần điền:**
    - `Channel ID` (lấy từ Slack → Settings → Customize Slack → Copy Channel ID).
    - `Message Format` (có thể tùy chỉnh để phù hợp với đội ngũ).
  - **Lưu ý:** Slack sẽ hiển thị **tiến trình xử lý** và thông báo khi hoàn thành.

##### **C. Cấu hình AI Subworkflow (nếu sử dụng)**
- **Node:** `AI Team Processor` (là một **Execute Workflow** dẫn đến workflow con)
  - **Lưu ý:** Nếu muốn **tăng cường phân tích AI**, các sếp cần tạo một **workflow con** riêng để xử lý dữ liệu cuộc gọi bằng **LLM** (ví dụ: sử dụng `n8n-nodes-ai`).
  - **Ví dụ prompt AI:**
    ```json
    "Analyze this sales call and extract:
    1. Customer name and company
    2. Main pain points
    3. Competitor mentions
    4. Next steps for the sales team"
    ```

##### **D. Xử lý lỗi & Rate Limiting**
- **Node:** `Only Process New Calls` (so sánh dữ liệu cũ mới)
  - **Lưu ý:** Workflow sẽ **bỏ qua cuộc gọi đã xử lý** để tránh trùng lặp.
- **Node:** `Loop to next call` (noOp)
  - **Lưu ý:** Nếu một cuộc gọi bị lỗi, workflow sẽ **tiếp tục với cuộc gọi tiếp theo** thay vì dừng lại.

#### **3. Kích hoạt ⚡️**
- **Test Run:** Chọn **1-2 cuộc gọi mẫu** để kiểm tra.
- **Bật Active:** Sau khi kiểm tra thành công, **bật workflow** để chạy tự động.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết nối với AI Chatbot (LLM)**
   - Thêm node `n8n-nodes-ai` để **phân tích sâu hơn** cuộc gọi (ví dụ: trích xuất cảm xúc khách hàng, đề xuất chiến lược bán hàng).
   - **Ví dụ:** Sử dụng **Mistral AI** hoặc **Gemini** để phân tích văn bản.

2. **Lưu log xử lý**
   - Thêm node `n8n-nodes-base.stickyNote` để ghi lại **lịch sử lỗi** và **thông tin debug**.

3. **Gửi báo cáo định kỳ**
   - Sử dụng **n8n Schedule Node** để **gửi báo cáo hàng tuần** về tiến độ xử lý cuộc gọi.

4. **Tích hợp với CRM khác**
   - Nếu sử dụng **HubSpot, Salesforce**, có thể **tích hợp thêm node API** để cập nhật thông tin từ cuộc gọi vào CRM.

---

### 📌 **Kết luận**
**CallForge** là **giải pháp hoàn hảo** cho các sếp Sales & Marketing muốn **tự động hóa phân tích cuộc gọi**, **tiết kiệm thời gian** và **cải thiện hiệu quả bán hàng**. Với **n8n**, bạn không cần viết code mà vẫn có thể xây dựng một **hệ thống AI mạnh mẽ** để xử lý dữ liệu.

**Hãy thử ngay!**
1. Import workflow.
2. Cấu hình Notion & Slack.
3. Bật workflow và **để AI làm việc cho bạn!**

🚀 **Nếu có thắc mắc, hãy để lại comment bên dưới!** 👇