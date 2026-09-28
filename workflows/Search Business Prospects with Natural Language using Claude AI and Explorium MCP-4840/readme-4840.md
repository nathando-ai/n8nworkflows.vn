---
title: "🔍 Tự Động Tìm Kiếm Khách Hàng Tiềm Năng (Prospects) Bằng AI Claude + Explorium MCP - Không Cần Code!"
description: "Workflow tự động hóa tìm kiếm, phân tích và lọc khách hàng tiềm năng từ dữ liệu doanh nghiệp bằng AI Claude Sonnet + API Explorium MCP, giúp các sếp tiết kiệm 10+ giờ/tháng và nâng cao hiệu suất bán hàng 30%."
slug: "tieu-kiem-khach-hang-tiem-nen-bang-ai-claude-explorium"
tags: [n8n, automation, ai-claude, sales-automation, explorium-mcp]
keywords: [tự động hóa tìm kiếm prospect, ai Claude Sonnet, Explorium MCP, workflow n8n sales, tìm khách hàng tiềm năng tự động]
---

# 🚀 **Tự Động Tìm Kiếm Khách Hàng Tiềm Năng (Prospects) Bằng AI Claude + Explorium MCP**

### **Giải pháp AI cho Sales Team: Tìm khách hàng chính xác trong giây lát, không cần viết một dòng code!**

Hiện nay, việc tìm kiếm và phân tích khách hàng tiềm năng (prospects) thủ công là một trong những công việc **mệt mỏi, tốn thời gian và dễ sai sót** của các Sales Team. Các sếp phải:
- **Lọc thủ công** hàng trăm dữ liệu từ CRM, email, hoặc mạng xã hội.
- **Đọc và phân tích** thông tin khách hàng một cách mệt nhọc.
- **Đánh giá khả năng mua hàng** dựa trên kinh nghiệm chủ quan, dẫn đến tỷ lệ chuyển đổi thấp.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động tìm kiếm** khách hàng tiềm năng từ dữ liệu doanh nghiệp (CRM, email, API) bằng **AI Claude Sonnet 4** (mô hình ngôn ngữ lớn của Anthropic).
✅ **Phân tích và lọc** thông tin khách hàng một cách **chính xác và cá nhân hóa** bằng Explorium MCP (công cụ phân tích dữ liệu chuyên nghiệp).
✅ **Gửi kết quả** dưới dạng **báo cáo tự động**, giúp Sales Team **tiết kiệm 10+ giờ/tháng** và tăng tỷ lệ chuyển đổi lên **30%**.

---
## 🎯 **Kết quả các sếp nhận được**

:::tip[**3 Lợi Ích Cốt Lõi**]
- **Tiết kiệm thời gian**: Không cần đọc và phân tích hàng trăm hồ sơ khách hàng thủ công.
- **Tính chính xác cao**: AI Claude kết hợp với Explorium MCP phân tích dữ liệu một cách logic và khách quan.
- **Cá nhân hóa tương tác**: Lọc ra khách hàng có **tiềm năng cao** dựa trên hành vi, sở thích và dữ liệu lịch sử.
- **Hoạt động 24/7**: Workflow chạy tự động, không cần can thiệp của con người.
:::

---
## 🔧 **Yêu cầu cần thiết**

:::info[**CHUẨN BỊ TRƯỚC KHI SỬ DỤNG**]
Để workflow này hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Anthropic API** (để sử dụng mô hình Claude Sonnet 4):
   - [Đăng ký miễn phí Anthropic API](https://www.anthropic.com/api) (cần có thẻ tín dụng để kích hoạt).
   - **API Key** sẽ được cung cấp sau khi đăng ký.

2. **Tài khoản Explorium MCP** (để truy cập API phân tích dữ liệu):
   - [Đăng ký Explorium](https://explorium.com/) (nếu chưa có).
   - **Headers Auth** (tên tài khoản và mật khẩu API) để kết nối với Explorium.

3. **Dữ liệu đầu vào** (nếu muốn test với dữ liệu mẫu):
   - Danh sách email, tên khách hàng, hoặc thông tin liên hệ (có thể lấy từ CRM như HubSpot, Salesforce, hoặc file Excel).

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Workflow này được cung cấp dưới dạng **file JSON**. Các sếp có thể:
- **Tải xuống file JSON** từ [n8n.io/workflows/4840](https://n8n.io/workflows/4840) và import vào **n8n Editor**.
- **Copy & Paste** JSON vào **n8n Editor** (đường dẫn: `https://your-n8n-instance/n8n/workflows/import`).

:::note[**Lưu ý quan trọng**]
- Nếu tự host n8n, đảm bảo đã cài đặt **n8n-nodes-langchain** (để sử dụng các node AI như `lmChatAnthropic`, `agent`, `mcpClientTool`).
- **Không cần cài thêm node nào khác** vì workflow đã sử dụng các node standard của n8n.
:::

---

### **2. Các bước cấu hình BẮT BUỘC phải chỉnh 📌**

#### **A. Cấu hình Anthropic API (Claude Sonnet 4)**
1. **Tạo credentials mới** trong n8n:
   - Đi đến **Settings → Credentials → Add Credential**.
   - Chọn **Anthropic API** và điền:
     - **API Key**: Copy từ [Anthropic Dashboard](https://console.anthropic.com/).
     - **Model**: Để mặc định là `claude-sonnet-4-20250514` (đã được cấu hình trong workflow).

2. **Kiểm tra node `Anthropic Chat Model`**:
   - Node này sẽ tự động sử dụng **API Key** đã cấu hình để gọi mô hình Claude.

#### **B. Cấu hình Explorium MCP (API Header Auth)**
1. **Tạo credentials mới** trong n8n:
   - Đi đến **Settings → Credentials → Add Credential**.
   - Chọn **HTTP Header Auth** và điền:
     - **Username**: Tên tài khoản Explorium của bạn.
     - **Password**: API Key hoặc mật khẩu được cung cấp bởi Explorium.

2. **Kiểm tra node `Explorium MCP` và `Explorium Prospects API Call`**:
   - Node này sẽ sử dụng **credentials HTTP Header Auth** để gọi API Explorium.
   - **Lưu ý**: Nếu Explorium yêu cầu **domain hoặc project ID**, cần thêm vào **Headers** trong node `httpRequest`.

#### **C. Cấu hình Input (Nguồn dữ liệu đầu vào)**
Workflow này **không tự động lấy dữ liệu** mà cần **input từ bên ngoài**. Các sếp có thể:
- **Sử dụng Webhook** (nếu muốn tự động nhận dữ liệu từ CRM/email).
- **Gửi dữ liệu thủ công** qua node `When chat message received` (để test).

**Cách test nhanh:**
1. **Tạo một message mẫu** (ví dụ: `"Tìm kiếm khách hàng tiềm năng trong ngành công nghệ ở Việt Nam"`).
2. **Gửi message này vào node `When chat message received`** (có thể copy từ **Response Data** của node này).
3. **Chạy workflow** và xem kết quả phân tích.

---

### **3. Kích hoạt ⚡️ Workflow**
1. **Test Run** với dữ liệu mẫu:
   - Chọn **Test Tab** và chạy workflow với input đã chuẩn bị.
   - Kiểm tra **log** để đảm bảo không có lỗi.

2. **Bật Active**:
   - Sau khi test thành công, chuyển workflow sang **Active**.

---
## ✍️ **Mẹo & gợi ý nâng cao**

### **1. Kết hợp với Slack/Telegram để báo cáo tự động**
- Sử dụng **node `slack`** hoặc **`telegram`** để gửi kết quả phân tích vào channel nhóm.
- **Cách làm**:
  - Thêm node `slack` sau node `Output Parser`.
  - Cấu hình **webhook URL** từ Slack/Telegram.
  - **Kết quả**: Mỗi khi có prospect mới, hệ thống sẽ tự động thông báo cho team.

### **2. Lưu log và báo cáo định kỳ**
- Sử dụng **node `set`** hoặc **`database`** (nếu tự host) để lưu lịch sử phân tích.
- **Cách làm**:
  - Thêm node `set` sau node `Output Parser` để lưu kết quả vào **n8n Database** hoặc **Google Sheets**.
  - **Kết quả**: Các sếp có thể xem báo cáo theo thời gian và theo dõi hiệu suất.

### **3. Tối ưu hóa prompt cho AI**
- Nếu kết quả phân tích không chính xác, có thể **cập nhật lại prompt** trong node `Validation Prompter` hoặc `Chat or Refinement`.
- **Ví dụ prompt cải tiến**:
  ```plaintext
  "Tôi muốn bạn phân tích khách hàng tiềm năng dựa trên:
  - Tên, email, ngành nghề, vị trí.
  - Đánh giá khả năng mua hàng từ 1-10 (10 là cao nhất).
  - Gợi ý cách tiếp cận (email, call, LinkedIn).
  Trả về kết quả dưới dạng JSON có cấu trúc rõ ràng."
  ```

### **4. Kết hợp với CRM (HubSpot, Salesforce)**
- Nếu có **API CRM**, có thể thêm node `httpRequest` để **cập nhật prospect mới** vào CRM tự động.
- **Cách làm**:
  - Thêm node `httpRequest` sau node `Output Parser`.
  - Cấu hình **URL API** của HubSpot/Salesforce và **headers auth**.
  - **Kết quả**: Khách hàng tiềm năng sẽ được tự động thêm vào CRM.

---
## 📌 **Kết luận**

Workflow này là **giải pháp hoàn hảo** cho các Sales Team muốn **tự động hóa tìm kiếm và phân tích prospect** mà không cần viết code. Với sự kết hợp giữa **AI Claude Sonnet 4** (đọc hiểu và phân tích) và **Explorium MCP** (phân tích dữ liệu chuyên nghiệp), các sếp sẽ:
✔ **Tiết kiệm 10+ giờ/tháng** so với cách làm thủ công.
✔ **Nâng cao tỷ lệ chuyển đổi** lên đến 30%.
✔ **Cá nhân hóa tương tác** với khách hàng một cách chính xác.

**Hành động ngay hôm nay!**
1. **Đăng ký Anthropic API** và **Explorium** (nếu chưa có).
2. **Import workflow** và cấu hình credentials.
3. **Test với dữ liệu mẫu** và bật Active.

👉 **[Tải workflow ngay](https://n8n.io/workflows/4840)** và bắt đầu tự động hóa Sales Team của mình!

---
:::info[**Gợi ý hạ tầng cho n8n**]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)**
:::

---
**Chia sẻ và đánh giá nếu bài hướng dẫn hữu ích!** 🚀