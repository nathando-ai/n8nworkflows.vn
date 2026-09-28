---
title: "🌟 Tự Động Hóa API NPR Station Finder với MCP Server - Giải Pháp AI Cho Doanh Nghiệp"
description: "Workflow này chuyển đổi API NPR Station Finder thành giao diện MCP, giúp AI agent tìm kiếm thông tin đài phát thanh NPR một cách tự động hóa hoàn toàn. Giúp tiết kiệm thời gian tìm kiếm thủ công và tích hợp dễ dàng với các hệ thống AI hiện đại."
slug: "tu-dong-hoa-api-npr-station-finder-mcp-server"
tags: [n8n, automation, ai-agent, api-integration, mcp-server]
keywords: [n8n workflow npr station finder, tự động hóa tìm kiếm đài phát thanh, api npr mcp, ai agent integration, tự động hóa no-code]
---

# 🚀 **Tự Động Hóa API NPR Station Finder với MCP Server - Giải Pháp AI Cho Doanh Nghiệp**

### **Nỗi Đau Của Các Sếp**
Hiện nay, khi cần tìm kiếm thông tin về các đài phát thanh thành viên của NPR (National Public Radio), các sếp thường phải:
- **Tìm kiếm thủ công** trên trang web NPR Station Finder.
- **Sao chép và dán** thông tin vào các hệ thống nội bộ hoặc báo cáo.
- **Chờ đợi phản hồi từ AI** khi cần tích hợp thông tin này vào các agent tự động.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động hóa hoàn toàn** việc lấy dữ liệu từ API NPR.
✅ **Tích hợp với AI Agent** thông qua MCP (Machine Conversation Protocol), giúp AI tìm kiếm và trả về thông tin một cách tự động.
✅ **Giảm thiểu thời gian** từ giờ đến phút khi cần thông tin về đài phát thanh.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian** khi không cần tìm kiếm thủ công trên trang web NPR.
- **Tích hợp AI Agent** một cách dễ dàng, giúp tự động hóa các công việc liên quan đến thông tin đài phát thanh.
- **Cập nhật dữ liệu tự động** khi AI agent yêu cầu thông tin mới.
- **Giảm thiểu lỗi** do con người trong việc sao chép và xử lý dữ liệu.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow này hoạt động, các sếp cần:
1. **Tài khoản n8n** (cài đặt trên VPS hoặc sử dụng phiên bản cloud).
2. **Thiết lập OAuth2 Credentials** (để xác thực với API NPR).
3. **AI Agent** (nếu muốn tích hợp với MCP, ví dụ như LangChain, LlamaIndex, hay các agent tự động hóa khác).
4. **URL Webhook** từ MCP Trigger để AI Agent gọi API.
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Bước 1:** Tải workflow từ [n8n.io/workflows/5654](https://n8n.io/workflows/5654).
- **Bước 2:** Nhấn **Import** trong n8n Editor và chọn file JSON đã tải.
- **Bước 3:** Chọn **Import Workflow** để thêm vào n8n của bạn.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này bao gồm **3 node chính**, và các sếp cần chú ý đến các bước sau:

##### **a. MCP Trigger (Node 1)**
- **Tên Node:** `NPR Station Finder Service MCP Server`
- **Cấu hình:**
  - **Path:** `npr-station-finder-service-mcp` (không cần thay đổi).
  - **Mục đích:** Đây là **điểm đầu vào** cho AI Agent gọi API. Khi AI Agent gửi yêu cầu, nó sẽ được chuyển đến node này.

##### **b. Get Stations 1 & Get Station 1 (Node 2 & 3)**
- **Tên Node:** `Get Stations 1` và `Get Station 1`
- **Cấu hình:**
  - **Credentials:** Sử dụng `httpHeaderAuth` (đã được thiết lập sẵn trong workflow).
  - **URL API:** `https://station.api.npr.org` (được tự động gọi trong node).
  - **Tham số:**
    - **Get Stations 1:** Lấy danh sách tất cả các đài phát thanh.
    - **Get Station 1:** Lấy thông tin chi tiết về một đài phát thanh cụ thể (nếu có ID).
  - **AI Expressions:** Workflow sử dụng `$fromAI()` để tự động lấy tham số từ yêu cầu của AI Agent.

##### **c. Thiết Lập OAuth2 Credentials**
- **Bước 1:** Trong n8n, đi đến **Credentials** > **Add Credential** > **HTTP Header Auth**.
- **Bước 2:** Điền thông tin:
  - **Name:** `npr-api-auth` (hoặc tên tùy ý).
  - **Username:** (Nếu API yêu cầu, có thể để trống hoặc sử dụng token).
  - **Password:** (Nếu cần, có thể là API Key hoặc token từ NPR).
- **Bước 3:** Gán credential này cho **Get Stations 1** và **Get Station 1**.

#### **3. Kích Hoạt ⚡️**
- **Bước 1:** Chạy **Test Run** với dữ liệu mẫu (nếu có).
- **Bước 2:** Nhấn **Active** để bật workflow.
- **Bước 3:** **Copy URL Webhook** từ MCP Trigger để AI Agent gọi API.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tích Hợp với Slack/Telegram**
   - Thêm node **Slack** hoặc **Telegram** để thông báo kết quả tìm kiếm cho team.
   - Ví dụ: Khi AI Agent tìm được đài phát thanh, gửi thông báo đến Slack với thông tin chi tiết.

2. **Lưu Log & Báo Cáo**
   - Thêm node **Google Sheets** hoặc **Airtable** để lưu lịch sử tìm kiếm.
   - Sẽ giúp các sếp theo dõi và phân tích dữ liệu lâu dài.

3. **Tùy Chỉnh API Endpoint**
   - Nếu cần thêm hoặc thay đổi tham số trong API, mở node **Get Stations 1** hoặc **Get Station 1** và chỉnh sửa **Method** (GET/POST) và **Headers**.

4. **Sử Dụng AI Agent Tích Hợp**
   - Nếu đang sử dụng **LangChain** hoặc **LlamaIndex**, chỉ cần gán **MCP URL** từ workflow này vào cấu hình của AI Agent.

---
### 📌 **Kết Luận**
Workflow **NPR Station Finder Service MCP Server** là giải pháp **tự động hóa hoàn toàn** để giúp AI Agent tìm kiếm và trả về thông tin về đài phát thanh NPR một cách nhanh chóng và chính xác. **Không cần code**, chỉ cần import và cấu hình OAuth2 là có thể tích hợp ngay vào hệ thống AI của doanh nghiệp.

**Hành động ngay hôm nay:**
1. **Import workflow** vào n8n của bạn.
2. **Thiết lập OAuth2** và kích hoạt.
3. **Tích hợp với AI Agent** để tự động hóa công việc!

Nếu có bất kỳ vấn đề nào, các sếp có thể liên hệ với tác giả **David Ashby** trên [Discord](https://discord.me/cfomodz) để hỗ trợ thêm! 🚀