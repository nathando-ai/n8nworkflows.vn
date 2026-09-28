---
title: "🎬 Tự Động Hóa MCP Server YouTube: Tải Tự Động Transcript & Tìm Kiếm Video Cho Nghiên Cứu AI (Không Cần Code)"
description: "Workflow này tự động hóa việc tìm kiếm video YouTube và tải transcript (chú thích) bằng APIFY.com, giúp các sếp tiết kiệm thời gian nghiên cứu và tránh giới hạn rate limit của YouTube chính thức. Đặc biệt phù hợp cho AI agent, Claude Desktop hoặc các công cụ MCP khác."
slug: "tay-dong-hoa-mcp-server-youtube"
tags: [n8n, automation, ai-powered, youtube, apify, mcp-server, research-tools]
keywords: [n8n workflow youtube, tự động hóa transcript youtube, mcp server n8n, apify youtube scraper, nghiên cứu video youtube]
---

# 🚀 **Tự Động Hóa MCP Server YouTube: Tải Transcript & Tìm Kiếm Video Cho Nghiên Cứu AI**

### **Giải pháp nào cho các sếp khi phải thủ công:**
- **Tìm kiếm video YouTube** để nghiên cứu chủ đề, phân tích nội dung hoặc chuẩn bị bài giảng?
- **Tải transcript (chú thích)** của video để phân tích chi tiết mà không phải nghe lại?
- **Bị giới hạn rate limit** của YouTube API chính thức, khiến workflow bị gián đoạn?

Workflow này **tự động hóa toàn bộ quy trình** bằng cách kết hợp **n8n + APIFY.com**, giúp các sếp:
✅ **Tìm kiếm video** theo từ khóa (10 kết quả đầu tiên).
✅ **Tải transcript** của video (chú thích tự động).
✅ **Monitor sử dụng API** để tránh vượt quá giới hạn.
✅ **Kết nối với AI agent** (Claude, n8n AI) để nghiên cứu tự động.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy 24/7 ổn định, các sếp nên **self-host n8n** trên VPS. APIFY.com cung cấp **tier miễn phí $5/month** đủ cho việc thử nghiệm.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không phải thủ công tìm kiếm và tải transcript.
- **Nghiên cứu sâu**: Phân tích nội dung video chi tiết từ transcript.
- **Không bị giới hạn**: APIFY.com không áp dụng rate limit như YouTube chính thức.
- **Hoạt động liên tục**: Workflow tự động hóa, hoạt động 24/7.
- **Kết nối với AI**: Sử dụng với Claude Desktop, n8n AI hoặc các công cụ MCP khác.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần:
1. **Tài khoản APIFY.com** (tiers miễn phí $5/month đủ dùng):
   - [Đăng ký với mã giảm 20%](https://www.apify.com?fpr=414q6) (mã: **20JIMLEUK**).
   - **Cần 2 Actor** của [YouTube Scraper](https://apify.com/streamers/youtube-scraper?fpr=414q6):
     - `youtube-search` (tìm kiếm video).
     - `youtube-transcript` (tải transcript).
2. **MCP Client hoặc AI Agent**:
   - [Claude Desktop](https://claude.ai/download) (để kết nối với MCP Server).
   - Hoặc **n8n AI Agent** (nếu tự động hóa trong n8n).
3. **VPS cho n8n** (nếu self-host):
   - [TinoHost](https://tino.vn/vps-n8n?affid=388) (mã giảm **VPSN8N**).
   - [BNIX](https://my.bnix.one/aff.php?aff=172) (VPS Xeon 4GB chỉ 50k/tháng).
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/3637](https://n8n.io/workflows/3637).
- **Cách import**:
  - Mở **n8n Editor** → Nhấn **Import** → Chọn file JSON.
  - **Hoặc** copy toàn bộ JSON vào **Import Workflow** (tab bên trái).

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này **không cần cấu hình API key YouTube** (tránh rate limit), nhưng cần **cấu hình APIFY.com** và **MCP Server Trigger**. Dưới đây là các bước chi tiết:

##### **A. Cấu hình APIFY.com**
1. **Tạo API Token**:
   - Trên [APIFY Dashboard](https://api.apify.com/tokens), tạo **1 token mới**.
   - Chọn **Scope**: `apify-api`.
   - **Lưu token này** (sẽ dùng trong **HTTP Request** của n8n).

2. **Cấu hình HTTP Request cho APIFY**:
   - **Node**: `Apify Youtube Search`, `Apify Youtube Transcripts`, `Get Usage Metrics`.
   - **Tham số cần điền**:
     - **Headers**:
       ```
       Authorization: Bearer <API_TOKEN_APIFY>
       ```
     - **URL**:
       - **Search**: `https://api.apify.com/v2/actors/streamers%2Fyoutube-scraper/runs`
       - **Transcript**: `https://api.apify.com/v2/actors/streamers%2Fyoutube-transcript/runs`
       - **Usage**: `https://api.apify.com/v2/actors/streamers%2Fyoutube-scraper/usage`
     - **Body (Request Payload)**:
       ```json
       {
         "input": {
           "searchQuery": "{{$node["Youtube Search"].jsonpath("$.searchQuery")}}",
           "limit": 10
         }
       }
       ```
       *(Đối với `Apify Youtube Transcripts`, thay `searchQuery` bằng `videoUrl` từ kết quả tìm kiếm.)*

##### **B. Cấu hình MCP Server Trigger**
1. **Tạo MCP Server Trigger**:
   - **Node**: `Apify Youtube MCP Server` (type: `mcpTrigger`).
   - **Cấu hình**:
     - **Path**: `b975bb25-be7c-49fb-8cd2-8e135d91ed4e` (đã cung cấp).
     - **Require Credentials**: **BẮT BUỘC** chọn **Yes** (tránh lộ workflow cho người dùng không hợp lệ).
     - **Credentials**:
       - Tạo **1 credential mới** (ví dụ: `apify-token`) và điền **API Token APIFY** vào.

2. **Kết nối với MCP Client**:
   - **Claude Desktop**:
     - Mở **Settings** → **MCP Servers** → Thêm server mới.
     - Điền:
       - **URL**: `http://<IP_VPS>:5678/mcp` (nếu self-host).
       - **Credentials**: `apify-token` (nếu yêu cầu).
   - **n8n AI Agent**:
     - Cấu hình **MCP Client** trong **n8n AI** với cùng URL và credentials.

##### **C. Test Workflow**
1. **Run Test**:
   - Nhấn **Execute Workflow** (button play).
   - Gửi **query mẫu** (ví dụ: `"what is MCP?"`) vào **MCP Trigger**.
   - Kiểm tra kết quả trong **Tool Workflows**:
     - `Youtube Search`: Kết quả tìm kiếm video.
     - `Youtube Transcripts`: Transcript của video đầu tiên.
     - `Usage Report`: Sử dụng APIFY.

2. **Bật Active**:
   - Sau khi test thành công, chuyển **Active** sang **On**.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết nối với Slack/Telegram**:
   - Thêm **node `n8n-nodes-base.slack`** để báo cáo kết quả tìm kiếm tự động.
   - Ví dụ: Khi workflow hoàn thành, gửi tin nhắn Slack với link video và transcript.

2. **Lưu log sử dụng API**:
   - Thêm **node `n8n-nodes-base.if`** để kiểm tra giới hạn APIFY.
   - Nếu gần hết giới hạn, gửi **email cảnh báo** (sử dụng `n8n-nodes-base.email`).

3. **Tăng số lượng video/tải nhiều transcript**:
   - Thay đổi `limit` trong **HTTP Request** của `Apify Youtube Search` (mặc định là 10).
   - Sử dụng **loop** (`n8n-nodes-base.foreach`) để tải transcript cho nhiều video.

4. **Tích hợp với Google Sheets**:
   - Lưu kết quả tìm kiếm vào **Google Sheets** để theo dõi lịch sử nghiên cứu.
   - Sử dụng **node `n8n-nodes-base.googleSheets`**.

5. **Cập nhật tự động**:
   - Sử dụng **node `n8n-nodes-base.schedule`** để chạy workflow định kỳ (ví dụ: hàng tuần).

---

### 📌 **Kết luận**
Workflow này **giải phóng tay chân các sếp** khỏi việc thủ công tìm kiếm và tải transcript YouTube, đồng thời **tránh bị giới hạn rate limit** của YouTube API. **Kết nối với AI agent** (Claude, n8n AI) giúp tự động hóa nghiên cứu sâu, tiết kiệm thời gian và tăng hiệu suất công việc.

**Bắt đầu ngay!**
1. **Import workflow** từ [n8n.io/workflows/3637](https://n8n.io/workflows/3637).
2. **Cấu hình APIFY.com** và **MCP Trigger**.
3. **Test với query**: `"how can I use MCP in n8n?"`.
4. **Bật Active** và kết nối với **Claude Desktop** hoặc **n8n AI**.

👉 **Hỏi đáp & hỗ trợ**: Liên hệ [Jim Leuk](mailto:hello@jimle.uk) nếu cần tư vấn chi tiết!