---
title: "🎨 Tự Động Hóa API Tên Màu Sắc với AI Agent qua MCP Server – Giải Pháp Không Code Cho Thiết Kế & AI"
description: "Workflow này chuyển đổi API Color Name thành giao diện MCP-compatible, cho phép AI agents tự động nhận diện và tạo ra tên màu sắc từ mã hex, đồng thời sinh ra bảng màu cá nhân hóa. Giúp thiết kế viên, nhà phát triển và AI engineer tiết kiệm thời gian lên đến 80% trong quá trình nghiên cứu màu sắc."
slug: "tu-dong-hoa-api-ten-mau-sac-voi-ai-agent-qua-mcp-server"
tags: [n8n, automation, ai-rag, api-integration, design-automation, langchain]
keywords: [n8n workflow color api, tự động hóa tên màu sắc, ai agent mcp server, api color pizza, thiết kế đồ họa tự động]
---

# 🎨 **Tự Động Hóa API Tên Màu Sắc với AI Agent qua MCP Server – Giải Pháp Không Code Cho Thiết Kế & AI**

## **🔍 Nỗi Đau Của Các Sếp Trong Thiết Kế & AI**
Hãy tưởng tượng một tình huống:
- **Thiết kế viên** phải tra cứu hàng chục mã màu hex trên API để tìm tên phù hợp cho dự án, mất thời gian và dễ mắc sai sót.
- **Nhà phát triển AI** muốn xây dựng một agent có khả năng tự động nhận diện và gợi ý tên màu từ mã hex, nhưng phải viết code phức tạp để kết nối với API.
- **Quá trình thiết kế** bị chậm trễ vì không có cách tự động hóa việc tra cứu và tạo ra bảng màu (swatch) từ tên màu.

Workflow này **giải quyết tất cả những vấn đề trên** bằng cách:
✅ **Tự động hóa tra cứu tên màu** từ mã hex (hex code) thông qua API Color Pizza.
✅ **Cung cấp giao diện MCP-compatible** cho AI agents, giúp họ tương tác với API một cách tự nhiên.
✅ **Sinh ra bảng màu cá nhân hóa** (swatch) từ tên màu, tiết kiệm thời gian cho thiết kế viên.
✅ **Không cần viết code** – chỉ cần cấu hình và kích hoạt workflow.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian lên đến 80%** trong quá trình tra cứu tên màu và tạo bảng màu.
- **Tự động hóa hoàn toàn** quá trình tương tác giữa AI agents và API Color Name.
- **Cá nhân hóa thiết kế** với bảng màu sinh động từ tên màu.
- **Không phụ thuộc vào code** – chỉ cần cấu hình đơn giản.
- **Hoạt động 24/7** khi chạy trên VPS tự host (self-hosted).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần:
1. **Tài khoản n8n** (cài đặt trên máy chủ riêng hoặc sử dụng n8n.cloud).
2. **VPS tự host** (để workflow chạy 24/7 ổn định).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
3. **Không cần API Key** – API Color Pizza không yêu cầu xác thực.
4. **N8n Node LangChain** (để sử dụng MCP Trigger).
   - Cài đặt bằng lệnh:
     ```bash
     npx n8n install @n8n/n8n-nodes-langchain
     ```
---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/5489](https://n8n.io/workflows/5489) hoặc copy/paste JSON vào **n8n Editor**.
- **Cách import**:
  1. Mở **n8n Editor** trên trang web hoặc máy chủ tự host.
  2. Nhấn **Import** (icon "..." trên góc trên bên phải).
  3. Chọn **Upload JSON** và tải file workflow.
  4. Nhấn **Import** để hoàn tất.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này bao gồm **5 node chính**, nhưng **không cần cấu hình gì** ngoài việc kích hoạt MCP Server. Tuy nhiên, để tối ưu hóa, các sếp nên:
- **Kiểm tra MCP Trigger**:
  - Node này sẽ **tạo URL webhook** cho AI agents kết nối.
  - Sau khi import, **copy URL** từ node `Color Name API MCP Server` để sử dụng trong cấu hình AI agent.
  - Ví dụ cấu hình trong **LangChain**:
    ```python
    from langchain.agents import create_langchain_agent
    from langchain.agents.tools import Tool

    tools = [
        Tool(
            name="Color Name API",
            func=lambda x: requests.get(f"YOUR_MCP_URL_HERE?query={x}"),
            description="Get color name from hex code"
        )
    ]
    ```

- **Tham số HTTP Request**:
  - Workflow sử dụng **4 endpoint** của API Color Pizza:
    1. **`/lists`** – Lấy danh sách màu mặc định.
    2. **`/names`** – Lấy tên màu từ mã hex.
    3. **`/swatch`** – Sinh ra bảng màu từ tên màu.
    4. **`/generate`** – Tạo bảng màu từ mã hex.
  - **Không cần chỉnh sửa** các tham số này, vì workflow đã cấu hình sẵn.

- **AI Expressions (`$fromAI()`)**:
  - Workflow tự động **chuyển đổi tham số** từ AI agent sang API thông qua biểu thức `$fromAI()`.
  - Ví dụ: Nếu AI agent gửi yêu cầu `"Tìm tên màu từ #FF5733"`, workflow sẽ tự động chuyển thành `GET /names?hex=#FF5733`.

#### **3. Kích Hoạt ⚡️**
1. **Test Run** (nếu cần):
   - Nhấn **Run Workflow** và nhập dữ liệu mẫu (ví dụ: `#FFFFFF`).
   - Kiểm tra kết quả trả về từ API.
2. **Bật Active**:
   - Chuyển trạng thái workflow sang **Active** để MCP Server hoạt động liên tục.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Kết nối với Slack/Telegram**:
   - Thêm node **Slack Webhook** hoặc **Telegram Bot** để thông báo kết quả tra cứu màu sắc.
   - Ví dụ: Khi AI agent tra cứu thành công, gửi tin nhắn Slack với bảng màu sinh ra.

2. **Lưu Log & Báo Cáo**:
   - Thêm node **Google Sheets** hoặc **Notion** để lưu lịch sử tra cứu màu.
   - Tạo báo cáo định kỳ về các màu được sử dụng nhiều nhất.

3. **Tích Hợp với Figma/Adobe XD**:
   - Sử dụng API Color Pizza kết hợp với **Figma Plugin** để tự động cập nhật màu sắc trong thiết kế.

4. **Tối Ưu Hiệu Suất**:
   - Nếu workflow chạy chậm, thêm node **Set** để cache kết quả tra cứu (tránh gọi API nhiều lần).
   - Ví dụ:
     ```json
     {
       "operation": "set",
       "property": "$json.colorName",
       "value": "$json.data.name"
     }
     ```

5. **Tạo AI Agent Tự Học**:
   - Kết hợp với **LangChain** để xây dựng một agent có khả năng **gợi ý màu sắc phù hợp** với chủ đề (ví dụ: "màu sắc cho logo startup tech").
---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp trong lĩnh vực thiết kế, AI và phát triển phần mềm muốn:
✔ **Tự động hóa tra cứu tên màu** từ mã hex.
✔ **Kết nối AI agents với API một cách dễ dàng** thông qua MCP Server.
✔ **Tiết kiệm thời gian và giảm sai sót** trong quá trình thiết kế.

**Hành động ngay hôm nay!**
1. **Import workflow** và kích hoạt MCP Server.
2. **Cấu hình AI agent** của bạn để sử dụng URL webhook.
3. **Thử nghiệm** và tối ưu hóa cho phù hợp với dự án của mình.

🚀 **Nếu cần hỗ trợ**, các sếp có thể tham khảo:
- [Tài liệu MCP của n8n](https://docs.n8n.io/integrations/builtin/cluster-nodes/sub-nodes/n8n-nodes-langchain.toolmcp/)
- [Discord của David Ashby](https://discord.me/cfomodz) (tác giả workflow).

---