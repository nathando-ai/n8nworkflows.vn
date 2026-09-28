---
title: "🚀 Token Estim8r - Sub Workflow để theo dõi sử dụng token và chi phí AI model với JinaAI"
description: "Workflow tự động thu thập dữ liệu thực thi n8n, tính toán token và chi phí dựa trên giá JinaAI, sau đó lưu kết quả vào Google Sheets để bạn có báo cáo chi phí AI thực tế."
slug: "token-estim8r-sub-workflow-track-ai-token-usage-cost-jinaai"
tags: [n8n, automation, no-code, AI, token tracking, cost management, JinaAI, Google Sheets]
keywords: [n8n workflow, tự động hóa, token usage, AI cost tracking, JinaAI pricing, Google Sheets integration]
---

# 🚀 Token Estim8r - Sub Workflow để theo dõi sử dụng token và chi phí AI model với JinaAI

Nhiều đội ngũ phát triển AI thường gặp khó khăn khi phải **theo dõi thủ công** lượng token mà các mô hình tiêu thụ và chi phí liên quan. Quá trình này tốn thời gian, dễ sai sót và không cung cấp cái nhìn tổng thể ngay lập tức. Workflow **Token Estim8r** giải quyết vấn đề bằng cách tự động:

1. Lấy dữ liệu thực thi (execution) từ n8n.  
2. Trích xuất lượng token đầu vào/đầu ra từ các node AI (ví dụ: JinaAI, OpenAI…).  
3. Gọi API giá của JinaAI để lấy đơn giá token hiện tại.  
4. Tính toán chi phí và tóm tắt theo từng mô hình.  
5. Ghi kết quả vào Google Sheets để bạn có báo cáo chi phí thực tế, có thể lọc, biểu đồ hoặc kết hợp với các công cụ BI khác.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm giờ công**: Không cần nhập dữ liệu tay, mọi coisa được tự động hóa.  
- **Chính xác cao**: Tính toán token và chi phí dựa trên giá thực tế từ JinaAI, giảm sai sót.  
- **Theo dõi thực thời**: Dữ liệu được ghi ngay sau mỗi lần thực thi workflow chính.  
- **Dễ mở rộng**: Kết quả lưu trong Google Sheets có thể kết hợp với Data Studio, Power BI hoặc gửi báo cáo qua email/Slack.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n API credentials** (Basic Auth hoặc API Key) để node **n8n Get Execution Data** có thể truy cập vào instance n8n của bạn.  
- **JinaAI API key** (nếu cần gọi endpoint giá) – node **Get AI Pricing** sẽ dùng key này trong header `Authorization: Bearer <JINA_API_KEY>`.  
- **Google Sheets credentials** (OAuth2) để node **Google Sheets** có thể ghi vào bảng tính bạn chỉ định.  
- Một **Google Sheet** đã có ít nhất một worksheet với các cột: `Timestamp`, `Model`, `Input Tokens`, `Output Tokens`, `Total Tokens`, `Cost (USD)`.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Trong n8n Editor, chọn **Import** → **Upload file JSON** (hoặc copy/paste toàn bộ JSON workflow vào ô clipboard) → **Import**.  
- Workflow sẽ xuất hiện với tên **Token Estim8r - Sub Workflow to track AI Model Token Usage and cost with JinaAI**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Cần cấu hình | Hướng dẫn chi tiết |
|------|--------------|--------------------|
| **When clicking ‘Test workflow’** (`manualTrigger`) | Không cần credentials | Dùng để test thủ công. Nhấn **Execute Workflow** để chạy lần đầu. |
| **n8n Get Execution Data** (`n8n`) | **n8n API credentials** | - Chọn credential bạn đã tạo (Basic Auth hoặc API Key). <br> - Đặt **Resource** = `execution`, **Operation** = `list`. <br> - Trong **Filters**, có thể giới hạn thời gian (ví dụ: `status = succeeded` và `startedAfter = {{ $now.setHours($now.getHours()-1) }}`) để chỉ lấy các execution gần đây. |
| **Get AI Usage Data** (`code`) | Không cần credentials | Node này nhận dữ liệu execution từ node trước và trích xuất trường `parameters` chứa `model`, `inputTokens`, `outputTokens` (tùy thuộc vào cách bạn gọi AI). Nếu bạn sử dụng node AI khác, hãy chỉnh sửa hàm JavaScript để lấy đúng trường token. |
| **Set Ai_Run_Data** (`set`) | Không cần credentials | Áp dụng các field cần thiết: `model`, `inputTokens`, `outputTokens`, `timestamp`. Bạn có thể thêm trường `workflowId` nếu muốn phân biệt các workflow cha. |
| **Get AI Pricing** (`httpRequest`) | **JinaAI API key** (nếu endpoint yêu cầu) | - **Method**: `GET`. <br> - **URL**: `https://api.jina.ai/v1/pricing` (hoặc endpoint cụ thể mà bạn sử dụng). <br> - **Headers**: `Authorization: Bearer {{ $env.JINA_API_KEY }}` (hoặc nhập trực tiếp vào trường Header). <br> - **Response Format**: `JSON`. |
| **Get Models Price and Add Summary** (`code`) | Không cần credentials | Nhận hai luồng dữ liệu: token usage (từ Set) và pricing (từ HTTP Request). Hàm JavaScript sẽ: <br> 1. Tìm giá input/output token cho model tương ứng. <br> 2. Tính `cost = (inputTokens * priceIn) + (outputTokens * priceOut)`. <br> 3. Trả về object chứa `model`, `inputTokens`, `outputTokens`, `totalTokens`, `costUSD`, `timestamp`. |
| **Google Sheets** (`googleSheets`) | **Google Sheets OAuth2** | - Chọn credential Google Sheets đã kết nối. <br> - **Operation**: `Append`. <br> - **Spreadsheet ID**: ID của sheet bạn muốn ghi (có thể lấy từ URL). <br> - **Sheet Name**: Tên worksheet (ví dụ: `TokenUsage`). <br> - Các trường sẽ được mapping tự động theo thứ tự bạn thiết lập trong node **Set** hoặc **Code** trước. |
| **When Executed by Another Workflow** (`executeWorkflowTrigger`) | Không cần credentials | Đánh dấu workflow này là **sub‑workflow**. Workflow cha có thể gọi nó bằng node **Execute Workflow** và truyền dữ liệu (nếu cần) qua trường **Workflow Data**. |

> **Lưu ý quan trọng**: Sau khi chỉnh sửa credentials và các trường ID/URL, hãy nhấn **Save** rồi **Execute Workflow** (test) để xác nhận dữ liệu được ghi đúng vào Google Sheets.

#### 3. Kích hoạt ⚡️
- Sau khi test thành công, chuyển toggle **Active** ở góc trên cùng workflow sang **ON** để workflow tự động chạy mỗi khi được gọi (từ workflow cha hoặc từ manual trigger nếu bạn muốn test thường xuyên).  
- Bạn cũng có thể cấu hình **Cron trigger** trong workflow cha để gọi sub‑workflow này mỗi 5‑15 phút, tùy vào tần suất sử dụng AI của bạn.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo Slack/Telegram**: Thêm node **Slack** hoặc **Telegram** sau Google Sheets để gửi tin nhắn cảnh báo khi chi phí vượt ngưỡng bạn định trước.  
- **Lưu log chi tiết**: Thêm node **Set** để lưu toàn bộ payload execution vào một worksheet khác để debug sau này.  
- **Báo cáo tuần tự**: Sử dụng node **Google Sheets** + **Google Docs** (hoặc **Email**) để tạo báo cáo tổng hợp chi phí AI mỗi tuần và gửi tới quản lý dự án.  
- **Đa mô hình**: Nếu bạn dùng nhiều nhà cung cấp (OpenAI, Anthropic, Cohere…), hãy mở rộng node **Get AI Pricing** để gọi nhiều endpoint giá và lưu trữ trong một bảng giá nội bộ.  
- **Xử lý lỗi**: Thêm node **Error Trigger** để bắt lỗi từ bất kỳ node nào và ghi vào sheet `Errors` hoặc gửi cảnh báo qua email.

### 📌 Kết luận
Workflow **Token Estim8r** giúp các sếp tự động hóa quá trình theo dõi token và chi phí AI một cách minh bạch, chính xác và không tốn công sức thủ công. Với chỉ một vài bước cấu hình credentials và Google Sheets, bạn sẽ có ngay một bảng chi phí AI cập nhật thực thời, từ đó dễ dàng tối ưu ngân sách và đưa ra quyết định đầu tư thông minh hơn. Hãy import ngay hôm nay và để n8n làm việc thay bạn!