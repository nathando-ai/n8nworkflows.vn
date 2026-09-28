---
title: "🚀 Kết nối AI Agents với dữ liệu EPA Clean Air Act qua MCP"
description: "Tự động thu thập, xử lý và cung cấp dữ liệu chất lượng không khí từ EPA bằng AI agents, không cần viết code."
slug: "ket-noi-ai-agents-epa-clean-air-act-mcp"
tags: [n8n, automation, no-code, AI, EPA, data-integration]
keywords: [n8n workflow, tự động hóa, EPA, Clean Air Act, AI agents, MCP integration]
---

# 🚀 Kết nối AI Agents với dữ liệu EPA Clean Air Act qua MCP

Doanh nghiệp, cơ quan môi trường hay nhà nghiên cứu thường phải **làm thủ công** để truy xuất dữ liệu chất lượng không khí từ hệ thống EPA (U.S. Environmental Protection Agency).  
Việc nhập liệu, lọc, chuyển đổi và đưa vào báo cáo tiêu tốn hàng giờ mỗi ngày, đồng thời dễ gây sai sót.  

Workflow **Connect AI Agents to EPA Clean Air Act Data with MCP Integration** giải quyết 100 % nhu cầu này:  
- **Kết nối trực tiếp** tới API của EPA thông qua MCP (Multi‑Channel Platform).  
- **Tự động tải**, **truy vấn**, **phân tích** và **trả về** dữ liệu dưới dạng JSON, GeoJSON, bản đồ hoặc metadata.  
- **Không cần viết một dòng code** – chỉ cấu hình các node trong n8n.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Truy xuất hàng nghìn bản ghi chỉ trong vài giây.  
- **Độ chính xác cao**: Loại bỏ lỗi nhập liệu thủ công.  
- **Cá nhân hoá dữ liệu**: Lọc theo khu vực, loại cơ sở, thời gian, … theo nhu cầu.  
- **Hoạt động liên tục**: Tự động chạy theo lịch hoặc khi có yêu cầu từ AI agents.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản EPA** (API Key) – đăng ký tại https://enviro.epa.gov/.  
- **MCP Server URL** và **Credentials** (username/password hoặc token) để node `mcpTrigger` kết nối.  
- **n8n** đã được cài đặt (Self‑hosted hoặc Cloud).  
- (Tuỳ chọn) **Slack / Telegram** webhook nếu muốn nhận thông báo.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n Editor.  
2. Nhấn **Import** → **Upload JSON** và chọn file workflow (hoặc copy toàn bộ JSON từ trang gốc).  
3. Xác nhận, workflow sẽ xuất hiện với 17 node đã được đặt tên sẵn.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Vai trò | Cấu hình quan trọng |
|------|----------|----------------------|
| **U.S. EPA Enforcement and Compliance History Online (ECHO) - Clean Air Act MCP Server** (`mcpTrigger`) | Kích hoạt workflow khi có yêu cầu từ AI agents. | - **MCP Server URL**: URL của server MCP.<br>- **Credentials**: Chọn hoặc tạo credential chứa `username` & `password` hoặc `Bearer Token`.<br>- **Trigger Event**: Đặt tên event (ví dụ: `fetch_air_quality`). |
| **Download Air Quality Data** (`httpRequestTool`) | Tải file dữ liệu thô (CSV/JSON) từ EPA. | - **Method**: `GET`.<br>- **URL**: `https://api.epa.gov/echo/v1/airquality/download` (ví dụ).<br>- **Headers**: `x-api-key: <EPA_API_KEY>`. |
| **Request Air Quality Data** (`httpRequestTool`) | Gửi yêu cầu chi tiết cho dữ liệu chất lượng không khí. | - **URL**: `https://api.epa.gov/echo/v1/airquality`.<br>- **Query Params**: `state`, `county`, `facilityId` (được truyền từ node trước). |
| **Search Air Quality Facilities** (`httpRequestTool`) | Tìm kiếm các cơ sở (facilities) liên quan. | - **URL**: `https://api.epa.gov/echo/v1/facilities/search`.<br>- **Params**: `searchTerm`, `limit`. |
| **Query Air Quality Facilities** (`httpRequestTool`) | Lấy danh sách chi tiết các facility đã tìm được. | - **URL**: `https://api.epa.gov/echo/v1/facilities`.<br>- **Headers**: API Key. |
| **Get Facility Details** → **Request Facility Details** | Lấy thông tin chi tiết (địa chỉ, loại hoạt động) của một facility cụ thể. | - **URL**: `https://api.epa.gov/echo/v1/facility/{facilityId}`.<br>- **Path Parameter**: `facilityId` từ node trước. |
| **Get Air Quality GeoJSON** → **Request Air Quality GeoJSON** | Trả về dữ liệu địa lý (GeoJSON) để vẽ bản đồ. | - **URL**: `https://api.epa.gov/echo/v1/airquality/geojson`.<br>- **Params**: `bbox`, `date`. |
| **Get Info Clusters Data** → **Request Info Clusters Data** | Nhóm thông tin theo tiêu chí (ví dụ: mức ô nhiễm). | - **URL**: `https://api.epa.gov/echo/v1/airquality/clusters`. |
| **Get Air Quality Map** → **Request Air Quality Map** | Lấy hình ảnh bản đồ tĩnh hoặc URL bản đồ. | - **URL**: `https://api.epa.gov/echo/v1/airquality/map`. |
| **Search by Query ID** → **Query by Query ID** | Kiểm tra trạng thái của một truy vấn đã gửi. | - **URL**: `https://api.epa.gov/echo/v1/query/{queryId}`. |
| **Get Air Quality Metadata** → **Request Air Quality Metadata** | Lấy siêu dữ liệu (định dạng, nguồn) của dataset. | - **URL**: `https://api.epa.gov/echo/v1/airquality/metadata`. |

**Lưu ý chung**  
- Tất cả các node `httpRequestTool` cần **Header** `x-api-key` chứa **EPA API Key**.  
- Đảm bảo **định dạng JSON** trả về được truyền đúng sang node tiếp theo (sử dụng `Set` hoặc `Function` nếu cần).  
- Kiểm tra **các trường bắt buộc** (ví dụ: `facilityId`, `queryId`) đã được map từ output của node trước.  

#### 3. Kích hoạt ⚡️
1. Chạy **Test** từng node với dữ liệu mẫu (có thể dùng `Execute Node` để xem response).  
2. Khi mọi thứ ổn, bật **Active** ở góc trên bên phải.  
3. Đặt **Schedule** (nếu muốn tự động chạy mỗi ngày) hoặc để **Trigger** `mcpTrigger` chờ lệnh từ AI agents.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo Slack/Telegram**: Thêm node `Slack` hoặc `Telegram` sau node `Get Air Quality Map` để gửi link bản đồ cho nhóm.  
- **Lưu trữ lịch sử**: Kết nối `Google Sheets` hoặc `PostgreSQL` để ghi lại mỗi lần truy vấn, giúp phân tích xu hướng thời gian.  
- **Báo cáo định kỳ**: Dùng node `Cron` + `HTML to PDF` + `Email` để gửi báo cáo chất lượng không khí hàng tuần cho các bên liên quan.  
- **Kết hợp LLM**: Sử dụng node `ChatGPT` (hoặc `LangChain`) để tóm tắt dữ liệu, đưa ra khuyến nghị giảm phát thải dựa trên kết quả.

### 📌 Kết luận
Với workflow này, các sếp có thể **tự động hoá toàn bộ quy trình** lấy, xử lý và truyền dữ liệu EPA Clean Air Act cho AI agents, giảm thiểu công sức thủ công và tăng độ tin cậy. Hãy **import ngay**, **cấu hình API Key** và **bật chạy** – dữ liệu sạch sẽ luôn trong tầm tay! 🚀