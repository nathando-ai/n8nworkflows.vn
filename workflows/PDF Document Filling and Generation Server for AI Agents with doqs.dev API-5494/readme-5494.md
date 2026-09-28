---
title: "🚀 **Tự Động Hóa Lập Trang PDF Cho AI Agent Với API doqs.dev – Không Cần Code!**"
description: "Workflow này chuyển đổi API doqs.dev thành giao diện MCP cho AI agent, giúp tự động tạo, chỉnh sửa và điền thông tin vào PDF mà không cần viết một dòng code nào. Giúp các sếp tiết kiệm thời gian lên đến 80% trong việc xử lý tài liệu hàng loạt."
slug: "tieu-dong-hoa-lap-trang-pdf-cho-ai-agent"
tags: [n8n, automation, no-code, ai-agent, doqs.dev, pdf-automation]
keywords: [n8n workflow pdf, tự động hóa tạo PDF, AI agent API, doqs.dev n8n, lập trình không code, tự động hóa văn phòng]
---

# 🚀 **Tự Động Hóa Lập Trang & Điền Thông Tin Vào PDF Cho AI Agent – Không Cần Code!**

### **Nỗi Đau Của Các Sếp**
Hàng ngày, các sếp phải mất **giờ đồng hồ** để:
- Tạo mẫu PDF từ đầu cho các hợp đồng, báo cáo, hoặc đơn hàng.
- Điền thông tin thủ công vào hàng trăm trang PDF hàng tháng.
- Chỉnh sửa và preview trước khi gửi cho khách hàng.
- Quản lý các template PDF một cách rườm rà trên máy tính.

**Kết quả?** Thời gian làm việc bị "chôn vùi" trong công việc lặp đi lặp lại, trong khi AI agent có thể tự động hóa **tất cả** những việc này chỉ với một dòng lệnh!

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[**3 Lợi Ích Cốt Lõi**]
- **Tiết kiệm 80% thời gian** trong việc tạo và điền PDF: AI agent tự động lấy dữ liệu từ chatbot, CRM, hoặc database để điền vào template.
- **Chính xác 100%**: Không còn sai sót do nhập liệu thủ công, tất cả dữ liệu đều được tự động hóa.
- **Hoạt động 24/7**: Workflow chạy liên tục trên VPS, không cần can thiệp của con người.
- **Cá nhân hóa hoàn toàn**: AI agent có thể tạo ra hàng ngàn template PDF khác nhau với nội dung độc quyền cho từng khách hàng.
:::

---
### **🔧 Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI BẮT ĐẦU**]
Để workflow này hoạt động, các sếp cần:
1. **Tài khoản doqs.dev**:
   - Đăng ký tại [doqs.dev](https://doqs.dev/) và lấy **API Key** (x-api-key).
   - **Lưu ý**: API Key này sẽ được sử dụng để xác thực với API của doqs.dev.
2. **n8n Self-hosted** (không dùng phiên bản cloud):
   - Để workflow hoạt động 24/7, các sếp nên cài n8n trên **VPS riêng**.
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).
3. **AI Agent hỗ trợ MCP**:
   - Workflow này sử dụng giao diện **MCP (Multi-Tool Control Protocol)**, nên các sếp cần một AI agent hỗ trợ MCP (ví dụ: LangChain, AutoGen, hay các agent tùy chỉnh).
   - Nếu chưa có, các sếp có thể sử dụng [LangChain](https://www.langchain.com/) để kết nối với workflow này.
4. **Dữ liệu mẫu (nếu test)**:
   - Một số mẫu PDF hoặc template để test điền thông tin tự động.

---
### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Bước 1**: Tải workflow từ [n8n.io/workflows/5494](https://n8n.io/workflows/5494) hoặc copy JSON từ link này.
- **Bước 2**: Mở **n8n Editor** và chọn **"Import"** → Dán JSON hoặc tải file `.json`.
- **Bước 3**: Workflow sẽ tự động tạo **15 node** như trong danh sách dưới đây.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **15 node**, nhưng **các node quan trọng nhất** cần cấu hình kỹ là:

##### **🔹 Node MCP Trigger (doqs.dev | PDF filling MCP Server)**
- **Chức năng**: Là **điểm kết nối** giữa AI agent và API doqs.dev.
- **Cấu hình**:
  - **Path**: Đặt thành `doqs.dev-|-pdf-filling-mcp` (không thay đổi).
  - **Credentials**: Chọn **API Key** (type: `API Key in header`, key name: `x-api-key`).
    - Điền **API Key** từ doqs.dev vào đây.
  - **Webhook URL**: Sau khi activate, copy URL này để kết nối với AI agent.

##### **🔹 Các Node HTTP Request (API doqs.dev)**
Tất cả **14 node HTTP Request** đều gọi API của doqs.dev. Các sếp cần:
- **Thiết lập credentials**:
  - Chọn **API Key** (type: `API Key in header`, key name: `x-api-key`).
  - Điền **API Key** từ doqs.dev vào tất cả các node này.
- **URL API**:
  - Tất cả các node đều gọi đến `https://api.doqs.dev/v1`.
  - **Không cần thay đổi URL**, chỉ cần đảm bảo API Key đúng.

##### **🔹 Node "Fill" (Điền Thông Tin Vào PDF)**
- **Chức năng**: Điền dữ liệu vào template PDF từ AI agent.
- **Cấu hình**:
  - **Method**: POST.
  - **Headers**:
    - `Content-Type: application/json`.
    - `x-api-key: [API Key của bạn]`.
  - **Body**:
    ```json
    {
      "template_id": "$fromAI('template_id')",
      "data": "$fromAI('data')"
    }
    ```
    - `$fromAI()` là **placeholder** để AI agent truyền dữ liệu vào.
    - Ví dụ: Nếu AI agent trả về:
      ```json
      {
        "template_id": "abc123",
        "data": { "name": "John Doe", "email": "john@example.com" }
      }
      ```
      Thì node này sẽ tự động điền vào template PDF.

##### **🔹 Node "Generate Pdf" (Tạo PDF Mới)**
- **Chức năng**: Tạo một template PDF mới từ đầu.
- **Cấu hình**:
  - **Method**: POST.
  - **Headers**: Như trên.
  - **Body**:
    ```json
    {
      "name": "$fromAI('name')",
      "file": "$fromAI('file')"
    }
    ```
    - `$fromAI('file')` là **file binary** của template PDF (nếu AI agent tải file từ URL).

---
#### **3. Kích Hoạt ⚡️ Workflow**
- **Bước 1**: **Test Run** với dữ liệu mẫu:
  - Gửi một request từ AI agent (ví dụ: LangChain) với payload:
    ```json
    {
      "operation": "fill",
      "template_id": "abc123",
      "data": { "name": "John Doe", "email": "john@example.com" }
    }
    ```
  - Kiểm tra **Output** của node "Fill" để xem PDF có được tạo thành công không.
- **Bước 2**: **Activate Workflow**:
  - Bật **Active** trên n8n Editor.
  - Copy **Webhook URL** từ node MCP Trigger để kết nối với AI agent.

---
### **✍️ Mẹo & Gợi Ý Nâng Cao**
:::info[**CÁCH SỬ DỤNG HIỆU QUẢ NHẤT**]
1. **Kết nối với AI Agent**:
   - Sử dụng **LangChain** hoặc **AutoGen** để gọi API MCP của workflow này.
   - Ví dụ với LangChain:
     ```python
     from langchain.agents import create_tool_calling_agent
     from langchain.tools import Tool

     tools = [
         Tool(
             name="doqs_pdf_filler",
             description="Fill and generate PDFs using doqs.dev API",
             func=lambda x: requests.post(
                 "https://your-n8n-instance/webhook/doqs.dev-|-pdf-filling-mcp",
                 json=x
             )
         )
     ]
     ```
2. **Lưu Log & Monitoring**:
   - Thêm **node "Set"** hoặc **"Sticky Note"** để lưu log hoạt động.
   - Ví dụ: Lưu ID của template PDF đã tạo thành công vào **Google Sheets** hoặc **Slack**.
3. **Tự Động Gửi PDF**:
   - Sau khi tạo PDF, sử dụng **node "HTTP Request"** để gửi PDF về email hoặc Slack.
   - Ví dụ:
     ```json
     {
       "method": "POST",
       "url": "https://api.slack.com/webhook/your-webhook-url",
       "body": {
         "text": "PDF đã tạo thành công: {{ $node["Fill"].json["file_url"] }}"
       }
     }
     ```
4. **Tạo Template Tự Động**:
   - Sử dụng **node "Create Template"** để tạo template mới từ file PDF đã upload.
   - AI agent có thể tự động tạo template từ các file mẫu đã có sẵn.
5. **Xử Lý Lỗi**:
   - Thêm **node "If"** để kiểm tra lỗi từ API doqs.dev.
   - Ví dụ:
     ```json
     {
       "condition": "{{ $node["Fill"].json.error }}",
       "then": [
         {
           "node": "Slack Notify",
           "operation": "post",
           "body": {
             "text": "Lỗi khi điền PDF: {{ $node["Fill"].json.error }}"
           }
         }
       ]
     }
     ```
:::

---
### **📌 Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa **tất cả quá trình tạo, chỉnh sửa và điền PDF** mà không cần viết một dòng code nào. Với **AI agent**, các sếp có thể:
✅ **Tạo hàng ngàn template PDF khác nhau** chỉ trong vài giây.
✅ **Điền dữ liệu tự động** từ chatbot, CRM, hoặc database.
✅ **Hoạt động 24/7** trên VPS, không cần can thiệp của con người.

**Hành động ngay hôm nay!**
1. **Cài đặt n8n trên VPS** (sử dụng mã giảm giá **VPSN8N**).
2. **Import workflow** và cấu hình API Key.
3. **Kết nối với AI agent** (LangChain, AutoGen...) và bắt đầu tự động hóa!

---
**💬 Cần hỗ trợ?**
- Trực tiếp liên hệ với tác giả **David Ashby** trên [Discord](https://discord.me/cfomodz).
- Đọc tài liệu chi tiết tại [n8n MCP Documentation](https://docs.n8n.io/integrations/builtin/cluster-nodes/sub-nodes/n8n-nodes-langchain.toolmcp/).