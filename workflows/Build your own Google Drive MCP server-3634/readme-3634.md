---
title: "🚀 **Tự Động Hóa MCP Server Trên Google Drive: Tìm Kiếm & Trích Xuất Tệp Như AI - Không Cần Code!**"
description: "Workflow này giúp các sếp xây dựng một **MCP Server trên Google Drive** tự động tìm kiếm, tải xuống và trích xuất nội dung từ các tệp PDF, CSV, hình ảnh, âm thanh - hoàn toàn không cần viết code. Kết nối với AI như Claude để quản lý tệp như một chuyên gia!"
slug: "tay-dong-hoa-mcp-server-google-drive"
tags: [n8n, automation, google-drive, ai-multimodal, model-context-protocol, self-hosted, no-code]
keywords: [n8n workflow google drive, tự động hóa quản lý tệp, MCP server tự động, trích xuất PDF CSV bằng AI, n8n + OpenAI, tự động hóa doanh nghiệp]
---

# 🚀 **Xây Dựng MCP Server Trên Google Drive: Tìm Kiếm & Trích Xuất Tệp Như AI**

### **Giải pháp cho các sếp:**
Hãy tưởng tượng một **AI quản lý tệp Google Drive** của bạn, tự động tìm kiếm, tải xuống và **trích xuất nội dung** từ các tệp PDF, CSV, hình ảnh, âm thanh - **không cần viết một dòng code nào!** Workflow này kết hợp **Model Context Protocol (MCP)** với **n8n** và **OpenAI**, giúp các sếp:
- **Tìm kiếm tệp** trong Google Drive theo yêu cầu (ví dụ: "Tìm báo cáo chi phí tháng trước").
- **Trích xuất nội dung** từ PDF, CSV, hình ảnh (bằng AI), và âm thanh (bằng transcribe).
- **Kết nối với AI** như **Claude** để quản lý tệp như một chuyên gia.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài **n8n trên VPS riêng (Self-hosted)** để đảm bảo tính riêng tư và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian** lên **100%** trong việc tìm kiếm và trích xuất tệp.
✅ **Tính chính xác cao** nhờ AI trích xuất nội dung từ PDF, hình ảnh, âm thanh.
✅ **Quản lý tệp như AI** - chỉ cần nói với **Claude** hoặc **MCP Client** là xong!
✅ **Hoạt động liên tục** 24/7 trên VPS riêng, không phụ thuộc vào máy tính cá nhân.
✅ **Mở rộng dễ dàng** - thêm chức năng xóa, di chuyển tệp, hoặc kết nối với Slack/Telegram.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google Drive** (và **API Key OAuth2** đã cấu hình trong n8n).
2. **Tài khoản OpenAI** (để phân tích hình ảnh và transcribe âm thanh).
3. **MCP Client** (ví dụ: **Claude Desktop** hoặc **Retool**).
4. **n8n Self-hosted** (cài trên VPS để ổn định).

:::note[Lưu ý quan trọng]
- **Không cần code** - workflow đã sẵn sàng import và chạy ngay.
- **Không cần kiến thức kỹ thuật sâu** - chỉ cần biết cách cấu hình OAuth2 và API Key.
:::

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow này:
#### **Cách 1: Import từ file JSON**
1. Tải workflow từ [đây](https://n8n.io/workflows/3634) (nút **Export Workflow**).
2. Trên **n8n Editor**, nhấn **Import Workflow** và chọn file JSON tải xuống.
3. Chọn **Create New Workflow** và nhấn **Import**.

#### **Cách 2: Copy/Paste JSON**
1. Tải workflow từ [đây](https://n8n.io/workflows/3634) và chọn **Export Workflow**.
2. Copy toàn bộ JSON từ file.
3. Trên **n8n Editor**, nhấn **Import Workflow** → **Paste JSON** và nhấn **Import**.

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Sau khi import, các sếp **phải cấu hình** các node quan trọng sau:

#### **🔹 Node 1: "When Executed by Another Workflow" (executeWorkflowTrigger)**
- **Không cần chỉnh** - node này dùng để kích hoạt workflow từ MCP Client.

#### **🔹 Node 2: "Google Drive MCP Server" (mcpTrigger)**
- **Cấu hình `path`** (đã mặc định là `a289c719-fb71-4b08-97c6-79d12645dc7e`).
- **BẮT BUỘC** sau khi chạy thử, **bật Authentication** để an toàn (trước khi đi sản xuất).

#### **🔹 Node 3: "Search Files from Gdrive" (googleDriveTool)**
- **Chọn Credentials**: `googleDriveOAuth2Api` (đã cấu hình sẵn).
- **Cấu hình `resource`**: Đặt thành `fileFolder` (để tìm kiếm cả tệp và thư mục).
- **Lọc theo folder**: Nếu muốn chỉ tìm kiếm trong một thư mục cụ thể, thêm điều kiện trong **Google Drive API Search Query**:
  ```json
  "mimeType != 'application/vnd.google-apps.folder'" && "parents contains 'FOLDER_ID'"
  ```

#### **🔹 Node 4-5: "FileType" & "Operation" (switch)**
- **Không cần chỉnh** - node này phân loại tệp theo **kiểu file** (PDF, CSV, hình ảnh, âm thanh) và **hành động** (tải xuống, trích xuất).

#### **🔹 Node 6-7: "Extract from PDF" & "Extract from CSV" (extractFromFile)**
- **Không cần chỉnh** - node này tự động trích xuất nội dung từ tệp.

#### **🔹 Node 8-9: "Get PDF Response" & "Get CSV Response" (set)**
- **Không cần chỉnh** - node này chuẩn bị dữ liệu cho MCP Client.

#### **🔹 Node 10: "Analyse Image" (openAi)**
- **Chọn Credentials**: `openAiApi` (đã cấu hình sẵn).
- **Cấu hình `operation`**: Đặt thành `analyze`.
- **Prompt mặc định**: AI sẽ mô tả nội dung hình ảnh (ví dụ: "Hình này mô tả một báo cáo tài chính").
- **Nếu muốn thay đổi prompt**, chỉnh ở **keyParameters**:
  ```json
  "prompt": "Mô tả chi tiết nội dung của hình này và trích xuất thông tin quan trọng."
  ```

#### **🔹 Node 11: "Transcribe Audio" (openAi)**
- **Chọn Credentials**: `openAiApi` (đã cấu hình sẵn).
- **Cấu hình `operation`**: Đặt thành `transcribe`.
- **Prompt mặc định**: AI sẽ chuyển âm thanh thành văn bản.
- **Nếu muốn thay đổi ngôn ngữ**, thêm vào **keyParameters**:
  ```json
  "language": "vi" // hoặc "en", "fr", etc.
  ```

#### **🔹 Node 12: "Read File From GDrive" (toolWorkflow)**
- **Không cần chỉnh** - node này gọi workflow con để tải tệp từ Google Drive.

#### **🔹 Node 13: "Download File1" (googleDrive)**
- **Chọn Credentials**: `googleDriveOAuth2Api` (đã cấu hình sẵn).
- **Không cần chỉnh** - node này tải tệp xuống trước khi trích xuất.

---

### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **Run Workflow** và kiểm tra kết quả.
   - Nếu gặp lỗi, kiểm tra **log** và **credentials** (OAuth2, API Key).
2. **Bật Active**:
   - Sau khi test thành công, nhấn **Active** để workflow chạy tự động khi MCP Client gọi.

---

## ✍️ **Mẹo & gợi ý nâng cao**
### **1. Kết nối với Slack/Telegram để báo cáo kết quả**
- Thêm **node Slack Webhook** sau node `Get PDF Response` để gửi thông báo khi trích xuất thành công.
- Ví dụ:
  ```json
  {
    "operation": "sendMessage",
    "resource": "text",
    "text": "📄 File PDF đã được trích xuất thành công! Nội dung: {{ $json["content"] }}"
  }
  ```

### **2. Lưu log hoạt động vào Google Sheets**
- Thêm **node Google Sheets** sau node `Analyse Image` để ghi lại lịch sử phân tích hình ảnh.
- Cấu hình:
  - **Sheet Name**: `Log_AI_Analysis`
  - **Columns**: `Timestamp, FileName, AI_Response`

### **3. Tự động gửi báo cáo định kỳ**
- Sử dụng **node Schedule** (n8n Pro) để chạy workflow hàng ngày và gửi báo cáo qua email.
- Ví dụ:
  - **Schedule**: `0 0 * * *` (lúc 00:00 hàng ngày).
  - **Node Email**: Gửi báo cáo từ Google Sheets qua Gmail.

### **4. Mở rộng chức năng quản lý tệp**
- **Xóa tệp**: Thêm node `googleDrive` với `operation: delete`.
- **Di chuyển tệp**: Thêm node `googleDrive` với `operation: move`.
- **Tạo thư mục mới**: Thêm node `googleDrive` với `operation: createFolder`.

---

## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn **tự động hóa quản lý tệp Google Drive** một cách **không cần code**, kết hợp với **AI** để phân tích và trích xuất thông tin. **Chỉ cần kết nối với MCP Client như Claude**, các sếp có thể **tìm kiếm, trích xuất và quản lý tệp như một chuyên gia**!

:::success[**Hành động ngay hôm nay!**]
1. **Cài n8n trên VPS** (để ổn định 24/7).
2. **Import workflow** và cấu hình **Google Drive OAuth2 + OpenAI API**.
3. **Kết nối với Claude Desktop** và thử nghiệm:
   - *"Tìm báo cáo chi phí tháng trước."*
   - *"Mô tả nội dung hình ảnh trong folder 'Contracts'."*
4. **Bật Active** và bắt đầu tự động hóa!

**Nếu có vấn đề**, để lại comment bên dưới hoặc liên hệ tác giả:
📩 **Email**: [hello@jimle.uk](mailto:hello@jimle.uk)
🔗 **LinkedIn**: [Jim Leuk](https://www.linkedin.com/in/jimleuk/)
🐦 **Twitter**: [@jimle_uk](https://x.com/jimle_uk)

**Chúc các sếp thành công!** 🚀