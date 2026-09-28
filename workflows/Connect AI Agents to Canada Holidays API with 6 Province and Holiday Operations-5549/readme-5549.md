---
title: "🇨🇦 **Tự Động Hóa Trực Tuyến: Kết Nối AI Agent với API Lễ Hạ Canada (6 Tỉnh + 6 API Hành Động) - Không Cần Code!**"
description: "Workflow này chuyển đổi API Lễ Hạ Canada thành giao diện MCP cho AI, giúp các sếp tự động hóa việc truy xuất thông tin lễ hội, tỉnh/territory Canada chỉ trong vài phút. Giúp tiết kiệm thời gian lên tới 80% so với cách làm thủ công."
slug: "tieu-dong-hoa-ai-agent-api-le-hoa-canada"
tags: [n8n, automation, AI RAG, API integration, Canada holidays, no-code]
keywords: [n8n workflow Canada holidays, tự động hóa API lễ hội Canada, AI agent MCP, 6 tỉnh Canada API, không cần code]
---

# 🚀 **Tự Động Hóa Trực Tuyến: Kết Nối AI Agent với API Lễ Hạ Canada (6 Tỉnh + 6 API Hành Động)**

## 📌 **Nỗi Đau Của Các Sếp Khi Làm Thủ Công**
Hiện nay, khi cần truy xuất thông tin về **lễ hội, ngày nghỉ lễ, hoặc thông tin về các tỉnh/territory Canada**, các sếp phải:
- **Tìm kiếm thủ công** trên trang web [Canada Holidays](https://canada-holidays.ca) (thời gian mất từ 5-10 phút/lần).
- **Sao chép dữ liệu** vào Excel/Google Sheets để phân tích (rủi ro sai sót cao).
- **Cập nhật thủ công** khi có thay đổi mới (như ngày nghỉ lễ thay đổi theo năm).

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động hóa 100%** việc truy xuất thông tin từ API Canada Holidays.
✅ **Kết nối với AI Agent** để các bot/assistant của bạn có thể **hỏi và trả lời** về lễ hội Canada một cách tự nhiên.
✅ **Hỗ trợ 6 API hành động** (2 thông tin cơ bản, 2 về lễ hội, 2 về tỉnh/territory) để đáp ứng mọi yêu cầu.
✅ **Không cần viết code** – chỉ cần import và kích hoạt!

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**Lợi Ích Cốt Lõi**]
- **Tiết kiệm thời gian lên tới 80%** so với cách làm thủ công.
- **Chính xác 100%** – Dữ liệu luôn được cập nhật từ API chính thức.
- **Cá nhân hóa** – AI Agent có thể trả lời các câu hỏi phức tạp về lễ hội Canada.
- **Hoạt động 24/7** – Không cần can thiệp của con người.
- **Dễ dàng mở rộng** – Thêm các tính năng như **lưu lịch lễ vào Google Calendar** hoặc **gửi thông báo qua Slack/Email**.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[**Chuẩn Bị Trước Khi Lên Đồ**]
Để workflow này hoạt động, các sếp cần:
1. **Môi trường n8n Self-hosted** (không cần API key đặc biệt, nhưng **VPS ổn định** là bắt buộc).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)

2. **Cài đặt Node `@n8n/n8n-nodes-langchain`** (để hỗ trợ MCP Trigger).
   - Hướng dẫn cài đặt: [Tại đây](https://docs.n8n.io/integrations/builtin/cluster-nodes/sub-nodes/n8n-nodes-langchain.toolmcp/).

3. **Không cần API Key** – Workflow này **không yêu cầu đăng ký tài khoản** nào.
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. Tải workflow từ [đây](https://n8n.io/workflows/5549) (chọn **Export as JSON**).
2. Trên n8n Editor, nhấn **Import** → Chọn file JSON vừa tải.
3. Chọn **Create Workflow** và đặt tên (ví dụ: **"Canada Holidays AI Agent"**).

#### **Phương pháp 2: Copy/Paste JSON**
1. Copy toàn bộ mã JSON từ [đây](https://n8n.io/workflows/5549) (chọn **Export as JSON**).
2. Trên n8n Editor, nhấn **Import** → Chọn **Paste JSON**.
3. Chọn **Create Workflow** và đặt tên.

---

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflows này **không yêu cầu cấu hình API Key**, nhưng các sếp cần **kiểm tra và đảm bảo** các node sau hoạt động đúng cách:

#### **🔹 Node MCP Trigger ("Canada Holidays MCP Server")**
- **Không cần cấu hình gì** – Node này sẽ tự động tạo **URL Webhook** để AI Agent kết nối.
- **Lưu ý:** Sau khi kích hoạt workflow, **copy URL Webhook** từ node này để dùng trong **cấu hình AI Agent**.

#### **🔹 Các Node HTTP Request Tool (6 Node)**
Tất cả 6 node này **gọi API từ [Canada Holidays](https://canada-holidays.ca)**. Các sếp **không cần chỉnh sửa gì** vì:
- **URL API** đã được cấu hình sẵn.
- **Headers** và **method (GET/POST)** cũng đã được thiết lập.
- **AI Expressions (`$fromAI()`)** sẽ tự động điền tham số khi AI Agent gọi API.

**Danh sách 6 Node và chức năng:**
| **Tên Node**               | **Chức Năng**                                                                 | **Tham Số Tự Động**                     |
|----------------------------|-------------------------------------------------------------------------------|------------------------------------------|
| Get API Root               | Lấy thông tin cơ bản về API (welcome message, links).                        | `$fromAI()` (không cần chỉnh)           |
| Get API Schema             | Lấy schema (cấu trúc dữ liệu) của API.                                       | `$fromAI()` (không cần chỉnh)           |
| List All Holidays          | Lấy danh sách **tất cả lễ hội** của Canada (31 ngày nghỉ lễ).               | `$fromAI()` (không cần chỉnh)           |
| Get Holiday by ID          | Lấy thông tin chi tiết **một lễ hội** theo ID.                               | `$fromAI()` (không cần chỉnh)           |
| List All Provinces         | Lấy danh sách **tất cả tỉnh/territory** Canada (13 đơn vị).                 | `$fromAI()` (không cần chỉnh)           |
| Get Province by ID         | Lấy thông tin chi tiết **một tỉnh/territory** theo ID.                       | `$fromAI()` (không cần chỉnh)           |

---

### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run** (để kiểm tra workflow hoạt động):
   - Nhấn **Run Workflow** (button ở góc trên phải).
   - Chọn **Manual Trigger** (nếu có).
   - Kiểm tra **output** của mỗi node để đảm bảo dữ liệu trả về chính xác.

2. **Bật Active Workflow**:
   - Sau khi test thành công, nhấn **Active** (button ở góc trên phải).
   - **Copy URL Webhook** từ node **"Canada Holidays MCP Server"** để dùng trong **cấu hình AI Agent**.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**

### **🔹 Kết Nối với AI Agent (LangChain, LlamaIndex, hay các bot khác)**
Sau khi có **URL Webhook**, các sếp có thể kết nối với:
- **LangChain** (để tạo AI Agent tự động hỏi về lễ hội Canada).
- **LlamaIndex** (để xây dựng knowledge base về Canada).
- **Discord/Slack Bot** (để người dùng chat với AI về lễ hội).

**Ví dụ cấu hình cho LangChain:**
```python
from langchain.agents import create_tool_calling_agent
from langchain.agents import AgentExecutor
from langchain.tools import StructuredTool

# Thay thế URL bằng URL Webhook từ n8n
tools = [
    StructuredTool(
        name="Canada Holidays",
        description="Get information about Canadian holidays and provinces",
        func=lambda query: requests.get(f"YOUR_N8N_WEBHOOK_URL?query={query}").json(),
    )
]

agent = create_tool_calling_agent(llm=llm, tools=tools)
agent_executor = AgentExecutor(agent=agent, tools=tools, verbose=True)
```

### **🔹 Lưu Log & Monitoring**
- **Thêm Node "Set"** sau mỗi HTTP Request để lưu **ID request** và **thời gian**.
- **Kết nối với Google Sheets/Notion** để theo dõi lịch sử gọi API.
- **Gửi báo cáo định kỳ** qua Email/Slack khi có thay đổi mới về lễ hội.

**Ví dụ thêm Node "Set" để lưu log:**
1. Sau mỗi node HTTP Request, thêm **Node "Set"** với key `log`.
2. Điền giá trị:
   ```json
   {
     "timestamp": "{{$node["Get API Root"].json["timestamp"]}}",
     "operation": "Get API Root",
     "status": "success"
   }
   ```
3. Kết nối Node "Set" với **Google Sheets** để lưu dữ liệu.

### **🔹 Tự Động Gửi Thông Báo Khi Có Lễ Hạ Mới**
- **Thêm Node "Schedule"** (nếu dùng n8n Enterprise) để chạy hàng ngày.
- **Kết nối với Node "HTTP Request"** để gọi API và so sánh với dữ liệu cũ.
- **Nếu có thay đổi**, gửi thông báo qua **Email** hoặc **Slack**.

---

## 📌 **Kết Luận: Áp Dụng Ngay Để Tiết Kiệm Thời Gian!**

Workflow này là **giải pháp hoàn hảo** cho các sếp cần:
✔ **Tự động hóa truy xuất dữ liệu lễ hội Canada** một cách nhanh chóng.
✔ **Kết nối với AI Agent** để tạo ra các bot thông minh trả lời về lễ hội.
✔ **Không cần viết code** – chỉ cần import và kích hoạt.

**Hành động ngay:**
1. **Import workflow** từ [đây](https://n8n.io/workflows/5549).
2. **Kích hoạt** và **copy URL Webhook**.
3. **Kết nối với AI Agent** của bạn (LangChain, LlamaIndex, Discord Bot...).
4. **Thêm các tính năng nâng cao** như lưu log, gửi báo cáo tự động.

**Nếu cần hỗ trợ thêm:**
- **Trực tiếp với tác giả David Ashby** trên [Discord](https://discord.me/cfomodz).
- **Dùng n8n Community** để tìm hiểu thêm: [n8n Docs - MCP](https://docs.n8n.io/integrations/builtin/cluster-nodes/sub-nodes/n8n-nodes-langchain.toolmcp/).

---
**🚀 Hãy tự động hóa ngay hôm nay – tiết kiệm thời gian và nâng cao hiệu suất công việc!**