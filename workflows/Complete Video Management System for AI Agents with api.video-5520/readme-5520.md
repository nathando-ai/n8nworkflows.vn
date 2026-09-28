---
title: "🎬 Hệ Thống Quản Lý Video AI Toàn Diện với api.video (Self-Hosted) – Tự Động Hóa 47 API Không Cần Code"
description: "Workflow này chuyển đổi toàn bộ 47 API của api.video thành giao diện MCP (Machine Control Protocol) cho AI Agents, giúp các sếp tự động hóa quản lý video, live streaming, caption, chapter và analytics chỉ với một dòng lệnh. Giúp tiết kiệm thời gian lên đến 80% so với cách làm thủ công."
slug: "he-thong-quan-ly-video-ai-voi-api-video"
tags: [n8n, automation, ai-agent, api.video, self-hosted, no-code, content-creation, rag, machine-control-protocol]
keywords: [n8n workflow api.video, tự động hóa quản lý video, ai agent, MCP server, live streaming automation, video processing automation]
---

# 🚀 **Hệ Thống Quản Lý Video AI Toàn Diện với api.video – Tự Động Hóa 47 API Cho AI Agents**

## **🔥 Tại sao các sếp cần workflow này?**
Hiện nay, quản lý video, live streaming, caption, chapter và analytics vẫn là công việc **mệt mỏi, tốn thời gian và dễ sai sót** khi làm thủ công. Các sếp phải:
- **Tải video lên** và chờ xử lý thủ công (thời gian chờ lên đến 24h).
- **Cập nhật metadata** (caption, chapter) một cách rườm rà.
- **Quản lý live stream** bằng nhiều công cụ khác nhau, dẫn đến **trải nghiệm không đồng bộ**.
- **Tối ưu hóa analytics** bằng cách phân tích dữ liệu thủ công, mất nhiều thời gian.

**Workflow này giải quyết tất cả vấn đề trên bằng cách:**
✅ **Tự động hóa toàn bộ 47 API của api.video** thành giao diện MCP (Machine Control Protocol) cho AI Agents.
✅ **Cho phép AI Agents quản lý video, live stream, caption, chapter và analytics một cách tự động**.
✅ **Giảm thời gian xử lý từ 24h xuống chỉ vài giây** với tự động hóa hoàn toàn.
✅ **Duy trì tính nhất quán** trong quản lý video, tránh sai sót do con người gây ra.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **ổn định 24/7**, các sếp nên **self-host n8n** trên VPS để tránh giới hạn của phiên bản cloud.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (Đảm bảo tốc độ cao cho AI Agents)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian lên đến 80%** so với cách làm thủ công.
- **Tự động hóa quản lý video, live stream, caption và chapter** chỉ với một dòng lệnh.
- **AI Agents có thể tự động xử lý video** (chỉnh sửa metadata, phân tích analytics) mà không cần can thiệp của con người.
- **Hoạt động liên tục 24/7** trên VPS self-hosted.
- **Giảm chi phí** do không cần sử dụng nhiều công cụ khác nhau.
:::

---

### 🔧 **Yêu cầu cần thiết**
Để workflow này hoạt động, các sếp cần:
✔ **Tài khoản api.video** (đăng ký tại [api.video](https://api.video/)).
✔ **API Key của api.video** (được tạo trong tài khoản).
✔ **n8n self-hosted** (trên VPS hoặc máy chủ riêng).
✔ **AI Agent hỗ trợ MCP** (ví dụ: LangChain, LlamaIndex, hay các agent tự xây dựng).

---
### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/5520).
- **Mở n8n Editor** → **Import Workflow** → Chọn file JSON đã tải.
- **Hoặc copy/paste JSON** từ file vào n8n Editor.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này **không yêu cầu authentication** nhưng **cần cấu hình API Key** cho tất cả các node HTTP Request.

##### **🔹 Cấu hình API Key cho tất cả node HTTP Request**
- Mở từng node **HTTP Request Tool** (ví dụ: `List all videos`, `Create a video`, `Upload a video`...).
- Trong tab **Credentials**, chọn **`api.video`** (nếu đã tạo credential trước đó) hoặc **thêm mới**:
  - **Name**: `api.video`
  - **Type**: `HTTP Request`
  - **URL**: `https://ws.api.video`
  - **Headers**:
    ```
    Authorization: Bearer {API_KEY}
    ```
    (Thay `{API_KEY}` bằng API Key của bạn từ tài khoản api.video).
  - **Method**: `GET` (hoặc `POST`, `PUT`, `DELETE` tùy node).

##### **🔹 Cấu hình MCP Trigger**
- Node **`api.video MCP Server`** (type: `mcpTrigger`) **không cần cấu hình gì** ngoài việc **bật Active**.
- Sau khi bật, **copy URL Webhook** từ node này để **cấu hình cho AI Agent**.

##### **🔹 Chỉnh sửa selective tools (nếu cần)**
Workflow này có **47 node**, nhưng **không nên bật tất cả** (do giới hạn 40 tool của nhiều AI Agent).
- **Mở node `api.video MCP Server`** → Tab **Tools** → **Chọn chỉ các tool cần thiết** (ví dụ: chỉ bật `List all videos`, `Upload a video`, `Create a caption`...).
- **Nhóm các tool liên quan** (ví dụ: nhóm `Videos` và `Captions` lại) để quản lý dễ dàng.

#### **3. Kích hoạt ⚡️**
- **Test Run** với một node đơn giản (ví dụ: `List all videos`) để kiểm tra kết nối.
- **Bật Active** cho workflow và **AI Agent** của bạn.

---

### ✍️ **Mẹo & gợi ý nâng cao**
#### **1. Tối ưu hóa AI Agent**
- **Sử dụng `$fromAI()`** để AI tự động truyền tham số (ví dụ: `title`, `description`, `caption`).
- **Lọc kết quả** bằng cách thêm node **`Set`** sau các node `List` (ví dụ: `List all videos`) để chỉ lấy video mới nhất.

#### **2. Log & Monitoring**
- Thêm node **`Set`** sau mỗi node HTTP Request để **lưu log** vào **Google Sheets** hoặc **Slack**.
- Ví dụ:
  ```json
  {
    "jsonata": "$.data"
  }
  ```
  → Sau đó kết nối với **Google Sheets** hoặc **Slack Webhook**.

#### **3. Tự động hóa báo cáo analytics**
- Sử dụng node **`List video player sessions`** và **`List player session events`** để **tính toán analytics** (ví dụ: thời gian xem, lượt tương tác).
- **Gửi báo cáo tự động** vào **Email** hoặc **Slack** hàng ngày bằng **n8n Scheduler**.

#### **4. Tự động tạo caption & chapter**
- Sử dụng **AI Agent** để **tự động tạo caption** từ video bằng **Whisper** hoặc **Google Speech-to-Text**.
- Sau đó, **upload caption** vào api.video bằng node **`Upload a caption`**.

---

### 📌 **Kết luận**
Workflow này **chuyển đổi api.video thành một hệ thống quản lý video AI toàn diện**, giúp các sếp:
✔ **Tự động hóa toàn bộ quy trình** từ upload video đến quản lý metadata.
✔ **Giảm thời gian xử lý** từ 24h xuống chỉ vài giây.
✔ **Tối ưu hóa analytics** một cách tự động.
✔ **Hoạt động liên tục 24/7** trên VPS self-hosted.

**🚀 Hãy áp dụng ngay để tiết kiệm thời gian và nâng cao hiệu suất quản lý video!**
Nếu cần hỗ trợ thêm, **ping David Ashby trên Discord** ([đây](https://discord.me/cfomodz)) hoặc tham khảo [tài liệu chính thức của n8n](https://docs.n8n.io/integrations/builtin/cluster-nodes/sub-nodes/n8n-nodes-langchain.toolmcp/).

---
**💡 Lưu ý quan trọng:**
- **Không nên bật tất cả 47 tool** (do giới hạn 40 tool của nhiều AI Agent).
- **Nhóm các tool liên quan** để quản lý dễ dàng.
- **Test Run trước khi bật Active** để tránh lỗi.