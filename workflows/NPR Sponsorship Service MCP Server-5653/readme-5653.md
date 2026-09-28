---
title: "🚀 Tự Động Hóa Dữ Liệu Quảng Cáo NPR Thông Qua MCP Server - Giải Pháp AI Cho Doanh Nghiệp Truyền Thông"
description: "Workflow này chuyển đổi API Quảng Cáo NPR thành giao diện MCP cho AI, giúp tự động hóa lấy dữ liệu quảng cáo VAST và theo dõi chi tiết, tiết kiệm thời gian cho các sếp truyền thông 100% không cần code."
slug: "tu-dong-hoa-quang-cao-npr-mcp-server"
tags: [n8n, automation, ai-rag, api-integration, sponsorship-tracking]
keywords: [n8n workflow quảng cáo, tự động hóa dữ liệu NPR, MCP server AI, lấy dữ liệu VAST, API NPR]
---

# 🚀 **Tự Động Hóa Dữ Liệu Quảng Cáo NPR Thông Qua MCP Server - Giải Pháp AI Cho Doanh Nghiệp Truyền Thông**

## **📌 Nỗi Đau Của Các Sếp Truyền Thông**
Các sếp truyền thông và nhà phát triển nội dung thường phải **thủ công** lấy dữ liệu quảng cáo từ API NPR để phân tích, theo dõi hiệu suất quảng cáo VAST (Video Ad Serving Template), và tích hợp vào hệ thống AI. Quá trình này **tốn thời gian**, **khó tự động hóa**, và **không linh hoạt** khi cần cập nhật thường xuyên.

**Workflow này giải quyết tất cả bằng cách:**
✅ **Chuyển đổi API NPR thành giao diện MCP** (Machine Communication Protocol) để AI có thể tương tác tự động.
✅ **Tự động lấy dữ liệu quảng cáo VAST** từ `https://sponsorship.api.npr.org` mà không cần viết code.
✅ **Theo dõi hiệu suất quảng cáo** một cách liên tục, giúp tối ưu hóa chiến dịch.
✅ **Hoạt động 24/7** trên VPS riêng, không phụ thuộc vào thời gian làm việc.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm thời gian**: Không cần thủ công nhập dữ liệu từ API NPR.
- **Tích hợp AI dễ dàng**: AI có thể tự động lấy và phân tích dữ liệu quảng cáo.
- **Hiệu suất cao**: Theo dõi VAST sponsorships và dữ liệu chi tiết một cách tự động.
- **Hoạt động liên tục**: Chạy trên VPS riêng, không ngừng nghỉ.
- **Giảm lỗi**: Tránh sai sót khi nhập dữ liệu thủ công.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ**]
Trước khi sử dụng workflow, các sếp cần:
✔ **Tài khoản n8n Self-hosted** (cài trên VPS để hoạt động 24/7).
✔ **API Key của NPR Sponsorship Service** (nếu cần xác thực).
✔ **AI Agent hoặc Tool sử dụng MCP** (ví dụ: LangChain, LlamaIndex) để kết nối với server MCP.
✔ **VPS 4GB+ RAM** (để chạy n8n ổn định).
:::

:::info[**Gợi ý hạ tầng cho n8n**]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Bước 1:** Tải workflow từ [n8n.io/workflows/5653](https://n8n.io/workflows/5653) hoặc copy JSON từ trang này.
- **Bước 2:** Mở **n8n Editor** và chọn **"Import Workflow"** → Dán JSON hoặc tải file `.json`.
- **Bước 3:** Đợi workflow được tải hoàn tất.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **3 node chính**, các sếp cần cấu hình như sau:

##### **🔹 Node 1: MCP Trigger (`mcpTrigger`)**
- **Chức năng:** Dùng làm **server endpoint** cho AI agent gửi yêu cầu.
- **Cấu hình:**
  - **Path:** Giả định là `npr-sponsorship-service-mcp` (không cần thay đổi).
  - **Credentials:** Không cần OAuth2 (do API NPR không yêu cầu).

##### **🔹 Node 2 & 3: HTTP Request Tool (`httpRequestTool`)**
- **Chức năng:** Gọi API NPR để lấy dữ liệu quảng cáo VAST.
- **Cấu hình:**
  - **Endpoint 1: Fetch VAST Sponsorships**
    - **URL:** `https://sponsorship.api.npr.org/vast`
    - **Method:** `GET` (hoặc `POST` nếu cần tham số).
    - **Headers:** Thêm `Authorization: Bearer <API_KEY>` (nếu có).
  - **Endpoint 2: Track VAST Sponsorship Data**
    - **URL:** `https://sponsorship.api.npr.org/track`
    - **Method:** `POST` (nếu cần gửi dữ liệu theo dõi).
    - **Body:** Sử dụng `$fromAI()` để AI tự động điền tham số (ví dụ: `impressionId`, `creativeId`).

##### **🔹 Kết Nối AI Agent**
- Sau khi **bật workflow**, copy **URL MCP** từ node `mcpTrigger` (ví dụ: `http://<VPS_IP>:5678/npr-sponsorship-service-mcp`).
- **Kết nối URL này vào AI Agent** (ví dụ: LangChain, LlamaIndex) để AI có thể gọi API tự động.

---

#### **3. Kích Hoạt ⚡️**
- **Test Run:** Chạy thử với dữ liệu mẫu (ví dụ: gọi `Fetch VAST Sponsorships`).
- **Bật Active:** Sau khi kiểm tra thành công, **bật workflow** để hoạt động liên tục.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[**CÁCH TIẾP CẬN THÊM**]
- **Thêm Logging:** Sử dụng node **Slack/Telegram** để báo cáo lỗi hoặc kết quả.
- **Lưu Log Dữ Liệu:** Kết nối với **Google Sheets** hoặc **Airtable** để lưu lịch sử quảng cáo.
- **Tự động Gửi Báo Cáo:** Sử dụng **n8n Schedule Node** để gửi báo cáo hàng ngày.
- **Tối Ưu API Key:** Nếu API NPR yêu cầu OAuth2, cấu hình trong **Credentials** của node HTTP.
:::

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp truyền thông bằng cách **tự động hóa lấy và theo dõi dữ liệu quảng cáo NPR** một cách hoàn toàn không cần code. **Kết nối với AI Agent** để tối ưu hóa chiến dịch quảng cáo và **chạy 24/7 trên VPS riêng** để không bỏ lỡ bất kỳ dữ liệu nào.

**🚀 Hãy áp dụng ngay và tự động hóa quy trình của mình!**

---
**💬 Cần hỗ trợ thêm?**
- **Đăng ký VPS n8n** tại [TinoHost](https://tino.vn/vps-n8n?affid=388) (mã giảm giá: **VPSN8N**).
- **Hỏi đáp kỹ thuật** trên [Discord của David Ashby](https://discord.me/cfomodz).
- **Tìm hiểu thêm về MCP** tại [n8n Docs](https://docs.n8n.io/integrations/builtin/cluster-nodes/sub-nodes/n8n-nodes-langchain.toolmcp/).