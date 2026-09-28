---
title: "🍳 **🚀 Tự Động Hoá Trích Xuất Thông Tin Đồ Ăn Từ Website Bằng AI + Bright Data (Miễn Phí!)**"
description: "Workflow tự động hóa trích xuất dữ liệu chi tiết từ các công thức nấu ăn trên website, chuyển đổi thành định dạng cấu trúc sẵn sàng sử dụng cho AI hoặc hệ thống quản lý. Giúp các sếp tiết kiệm hàng giờ công sức mỗi tuần!"
slug: "tieu-dung-don-an-tu-website-bang-ai-bright-data"
tags: [n8n, automation, ai, bright-data, openai, no-code, structured-data]
keywords: [n8n workflow trích xuất dữ liệu, tự động hóa AI, Bright Data MCP, OpenAI GPT-4o mini, công thức nấu ăn, scraping website]
---

# 🍳 **🚀 Tự Động Hoá Trích Xuất Thông Tin Đồ Ăn Từ Website Bằng AI + Bright Data**

### **🔥 Nỗi Đau Của Các Sếp?**
Hàng ngày, các sếp phải:
- **Tìm kiếm và sao chép** công thức nấu ăn từ nhiều website khác nhau (Food.com, Allrecipes, BBC Good Food...).
- **Chuyển đổi dữ liệu thô** thành định dạng có cấu trúc (ví dụ: JSON) để phân tích hoặc tích hợp vào hệ thống quản lý.
- **Lặp lại công việc thủ công** này hàng tuần, mất thời gian và dễ sai sót.

**Workflow này giải quyết tất cả!** Sử dụng **Bright Data MCP** để lấy dữ liệu từ website và **OpenAI GPT-4o mini** để chuyển đổi thành **dữ liệu cấu trúc hoàn chỉnh**, sẵn sàng sử dụng cho AI hoặc hệ thống của bạn.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### **🎯 Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Trích xuất dữ liệu từ hàng trăm công thức chỉ trong vài phút thay vì hàng giờ.
- **Dữ liệu chính xác**: AI chuyển đổi thông tin thô thành **cấu trúc JSON sạch**, không cần sửa chữa thủ công.
- **Hoạt động liên tục**: Workflow chạy tự động mỗi khi có dữ liệu mới (ví dụ: sau khi cập nhật website).
- **Dữ liệu sẵn sàng tích hợp**: Kết quả có thể dùng cho **chatbot, hệ thống quản lý công thức, hoặc phân tích AI**.
:::

---

### **🔧 Yêu cầu cần thiết**
Để workflow hoạt động, các sếp cần:
1. **Tài khoản Bright Data MCP**:
   - [Đăng ký miễn phí tại Bright Data](https://brightdata.com/) và lấy **API Key**.
   - Cài đặt **n8n-node-mcp** (node cộng đồng) để kết nối với Bright Data.
2. **Tài khoản OpenAI**:
   - [Đăng ký tại OpenAI](https://platform.openai.com/) và lấy **API Key**.
3. **URL của website chứa công thức nấu ăn**:
   - Ví dụ: `https://www.allrecipes.com/recipe/23456/chocolate-chip-cookies/`.
4. **URL Webhook (tuỳ chọn)**:
   - Để nhận thông báo khi workflow hoàn thành (ví dụ: Slack, Telegram, hoặc email).

---

### **🚀 Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/4591](https://n8n.io/workflows/4591) và import vào **n8n Editor**.
- **Cách 2**: Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/4591) và dán vào **Create Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này có **17 node** quan trọng, nhưng các sếp chỉ cần chú ý đến các phần sau:

##### **A. Cấu hình Bright Data MCP**
- **Node "List all tools for Bright Data"**:
  - Chọn **credentials**: `mcpClientApi` (đã tạo khi cài đặt node MCP).
  - **Không cần thay đổi** các tham số khác (n8n sẽ lấy danh sách công cụ tự động).

- **Node "Bright Data MCP Client For Recipe Extract"**:
  - **Điền URL công thức nấu ăn** vào **`url`** (ví dụ: `https://www.allrecipes.com/recipe/23456/chocolate-chip-cookies/`).
  - **Chọn operation**: `executeTool` (đã mặc định).

- **Node "Bright Data MCP Client For Recipe Extract Within The Loop"**:
  - **Không cần thay đổi**, workflow sẽ tự động lấy dữ liệu từ trang paginated (nếu có).

##### **B. Cấu hình OpenAI GPT-4o mini**
- **Node "OpenAI Chat Model for Paginated Data Extract"**:
  - **Credentials**: `openAiApi` (API Key OpenAI).
  - **Model**: `gpt-4o-mini` (đã mặc định).
  - **Prompt mặc định** đã tối ưu hóa để trích xuất dữ liệu cấu trúc từ HTML. **Không cần chỉnh sửa** trừ khi muốn thay đổi logic.

- **Node "OpenAI Chat Model for Structured Data Extract"**:
  - **Credentials**: `openAiApi`.
  - **Model**: `gpt-4o-mini`.
  - **Prompt** sẽ tự động chuyển đổi dữ liệu thô thành **JSON cấu trúc** (ví dụ: tên công thức, thành phần, hướng dẫn, thời gian nấu...).

##### **C. Cấu hình Webhook (tuỳ chọn)**
- **Node "Webhook Notification for Data Extract Within the Loop"**:
  - **Điền URL Webhook** của bạn (ví dụ: `https://your-slack-webhook-url.com`).
  - **Thông báo** sẽ gửi khi workflow hoàn thành.

##### **D. Lưu trữ kết quả**
- **Node "Write the structured content to disk"**:
  - **Chọn đường dẫn lưu file** (ví dụ: `/data/recipes/structured_data.json`).
  - Workflow sẽ tự động ghi dữ liệu vào file JSON.

---

#### **3. Kích hoạt ⚡️**
1. **Test run dữ liệu mẫu**:
   - Nhấn **"Test workflow"** và điền **URL công thức nấu ăn** vào node **"Set the Recipe Extract URL"**.
   - Kiểm tra kết quả trong **node "Structured Recipe Data Extract"** (nếu dữ liệu cấu trúc xuất hiện, workflow hoạt động).

2. **Bật Active workflow**:
   - Chuyển trạng thái từ **"Inactive"** sang **"Active"**.
   - Workflow sẽ chạy tự động khi được kích hoạt (ví dụ: qua Webhook hoặc Manual Trigger).

---

### **✍️ Mẹo & gợi ý nâng cao**
1. **Tích hợp với Slack/Telegram**:
   - Sử dụng **node Slack** hoặc **Telegram Bot** để nhận thông báo khi workflow hoàn thành.

2. **Lưu log hoạt động**:
   - Thêm **node "Sticky Note"** để ghi lại lịch sử chạy workflow (ví dụ: ngày giờ, URL công thức, kết quả).

3. **Tự động chạy định kỳ**:
   - Sử dụng **node "Schedule"** (n8n Pro) để chạy workflow hàng ngày/lần tuần.

4. **Xử lý lỗi tự động**:
   - Thêm **node "Error Handling"** (Code node) để xử lý trường hợp website bị thay đổi hoặc API lỗi.

5. **Tối ưu chi phí OpenAI**:
   - Sử dụng **GPT-4o mini** thay vì GPT-4 để tiết kiệm chi phí (đã được cấu hình sẵn).

---

### **📌 Kết luận**
Workflow này **giải phóng thời gian** của các sếp khỏi công việc trích xuất dữ liệu thủ công, đồng thời **tăng cường chính xác** nhờ AI. **Chỉ cần 10 phút cấu hình**, bạn đã có một hệ thống tự động hóa hoàn chỉnh!

**🚀 Hãy áp dụng ngay và tiết kiệm hàng giờ công sức mỗi tuần!**
Nếu có vấn đề, liên hệ tác giả **Ranjan Dailata** qua email: [ranjancse@gmail.com](mailto:ranjancse@gmail.com).

---
**🔹 Lưu ý**: Workflow chỉ hoạt động trên **n8n Self-hosted** vì sử dụng node cộng đồng MCP. Các sếp nên **cài đặt VPS** để tránh giới hạn của n8n Cloud.