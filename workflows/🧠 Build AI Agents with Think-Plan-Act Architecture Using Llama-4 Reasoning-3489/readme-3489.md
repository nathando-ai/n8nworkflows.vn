---
title: "🧠 Xây dựng AI Agent Think-Plan-Act với Llama-4 Reasoning trên n8n"
description: "Workflow tự động hóa quy trình suy nghĩ, lập kế hoạch và thực thi bằng kiến trúc Think-Plan-Act, sử dụng Llama-4 qua OpenRouter để tạo ra agents thông minh mà không cần viết code."
slug: "xay-dung-ai-agent-think-plan-act-llama4"
tags: [n8n, automation, no-code, AI, Llama-4, OpenRouter, Think-Plan-Act, Agent]
keywords: [n8n workflow, tự động hóa AI, Think-Plan-Act, Llama-4 reasoning, OpenRouter agent, n8n agent node]
---

# 🧠 Xây dựng AI Agent Think-Plan-Act với Llama-4 Reasoning trên n8n

Bạn từng cảm thấy mệt mỏi khi phải viết hàng chục dòng code chỉ để xây dựng một agent AI có thể **suy nghĩ → lập kế hoạch → thực thi**? Với workflow này, bạn chỉ cần kéo thả, cấu hình credentials và webhook – n8n sẽ xử lý toàn bộ luồng suy luận bằng mô hình **Llama-4** (truy cập qua OpenRouter) và trả về kết quả có cấu trúc sẵn sàng để tích hợp vào bất kỳ hệ thống nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hoá suy luận đa bước**: Think → Plan → Act mà không cần viết một dòng code AI.
- **Kết quả có cấu trúc JSON** nhờ Structured Output Parser, dễ dàng truyền cho các hệ thống downstream (API, database, Slack…).
- **Tái sử dụng linh hoạt**: Các agent Think và Act có thể được gọi riêng qua webhook `start-thinking` hoặc `get-weather` để tích hợp vào các use case khác.
- **Chi phí thấp**: Chỉ trả phí cho token sử dụng trên OpenRouter, không cần triển khai mô hình riêng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản OpenRouter** và **API Key** (để truy cập mô hình Llama-4).
- **Credentials n8n** loại **OpenRouter Chat Model** (tên credential tùy bạn, ví dụ: `openrouter_llama4`).
- (Tùy chọn) **Webhook client** (curl, Postman, hoặc bất kỳ hệ thống nào) để gọi hai webhook:
  - `start-thinking` – khởi động chuỗi Think‑Plan‑Act.
  - `get-weather` – ví dụ minh họa gọi agent với dữ liệu thời tiết (có thể thay bằng bất kỳ payload nào).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Trong n8n Editor, nhấn **Import** → **From File** (hoặc dán JSON trực tiếp).
2. Chọn file JSON của workflow này → **Import**.
3. Workflow sẽ xuất hiện với tên **🧠 Build AI Agents with Think-Plan-Act Architecture Using Llama-4 Reasoning**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Loại | Cần cấu hình | Hướng dẫn chi tiết |
|------|------|--------------|--------------------|
| **OpenRouter Chat Model** (các bản 1‑7) | `lmChatOpenRouter` | **Credential** + **Model** | Mở node → Credentials → chọn credential OpenRouter bạn đã tạo → Trong trường **Model**, nhập `meta-llama/llama-4-scout` (hoặc bất kỳ biến thể Llama-4 nào bạn có quyền truy cập). |
| **Think** / **Act** / **Think1** / **Act1** | `agent` | **Agent Type** + **Tools** | Đảm bảo trường **Agent Type** được đặt thành `Structured` (để làm việc với Structured Output Parser). Trong **Tools**, bạn có thể để trống nếu chỉ muốn agent suy luận; nếu muốn gọi các công cụ bên ngoài (ví dụ: API thời tiết), thêm node **HTTP Request** như tool và chọn nó ở đây. |
| **Config** & **Config1** | `code` | **JavaScript** (tùy chọn) | Các node này chứa mã mẫu để thiết lập biến môi trường (ví dụ: `maxTokens`, `temperature`). Bạn có thể chỉnh sửa để phù hợp với use case: double‑click node → thay đổi giá trị trong `return { ... }`. |
| **start-thinking** | `webhook` | **Path** | Mở node → trong **Webhook Path**, điền một đường dẫn dễ nhớ, ví dụ: `/ai/think-plan-act`. Lưu lại và n8n sẽ cung cấp URL đầy đủ (ví dụ: `https://<your-n8n-domain>/webhook/ai/think-plan-act`). |
| **get-weather** | `webhook` | **Path** | Tương tự, đặt path như `/ai/get-weather` để test nhanh với payload thời tiết. |
| **Structured Output Parser** (các bản 1‑3) | `outputParserStructured` | **Schema** | Định dạng JSON mà agent sẽ trả về. Mặc định workflow đã có schema mẫu (ví dụ: `{ thinking: string, plan: string[], action: string }`). Bạn có thể chỉnh sửa schema để phù hợp với output mong muốn. |
| **Thinking output parser** & **Task Output Parser** (các bản 1‑2) | `outputParserAutofixing` | **Prompt** (tùy chọn) | Nodes này giúp tự sửa lỗi JSON nếu agent trả về chuỗi không hợp lệ. Bạn thường không cần chỉnh sửa trừ khi muốn thay đổi hướng dẫn sửa lỗi. |
| **Sticky Note** & **No Operation** | `stickyNote` / `noOp` | Chỉ ghi chú | Không cần thay đổi; chúng chỉ dùng để giải thích luồng trong editor. |

> **Lưu ý quan trọng**: Sau khi thay đổi credential hoặc model ở bất kỳ node OpenRouter Chat Model nào, hãy **copy** cùng cấu hình đó sang tất cả các node OpenRouter Chat Model còn lại để đảm bảo đồng nhất (hoặc sử dụng tính năng **Expressions** để tham chiếu credential chung nếu bạn muốn quản lý tập trung).

#### 3. Kích hoạt ⚡️
1. Chọn nút **Execute Workflow** → **Trigger Node** → chọn **start-thinking** (hoặc **get-weather**) để chạy test.
2. Trong panel **Input**, gửi một payload JSON đơn giản, ví dụ:
   ```json
   {
     "question": "Hãy lập kế hoạch du lịch 3 ngày tại Đà Nẵng cho gia đình 4 người."
   }
   ```
3. Kiểm tra output ở node **Structured Output Parser3** (hoặc node cuối cùng tùy vào luồng bạn kích hoạt). Bạn sẽ thấy một đối tượng JSON có trường `thinking`, `plan` (mảng) và `action`.
4. Nếu test thành công, quay lại workflow editor và bật toggle **Active** ở góc trên bên phải để workflow bắt đầu lắng nghe webhook 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo kết quả qua Slack/Telegram**: Thêm node **Slack** hoặc **Telegram** sau Structured Output Parser để gửi thông báo tự động khi agent hoàn thành nhiệm vụ.
- **Lưu log vào Google Sheets**: Kết nối node **Google Sheets** để ghi lại mỗi lần agent suy nghĩ, kế hoạch và hành động – hữu ích cho việc audit và cải thiện prompt.
- **Kích hoạt theo lịch**: Thay vì webhook, thay node **start-thinking** bằng node **Cron** để chạy agent tự động mỗi giờ (ví dụ: tạo báo cáo thị trường hàng ngày).
- **Chain nhiều agent**: Sao chép luồng Think‑Plan‑Act và nối chúng thành một pipeline đa bước (ví dụ: agent đầu ra của luồng đầu vào làm input cho luồng thứ hai).
- **Tối ưu chi phí**: Trong node OpenRouter Chat Model, giảm `temperature` xuống 0.2‑0.3 và giới hạn `maxTokens` để giảm lượng token sử dụng mà vẫn giữ chất lượng suy luận.

### 📌 Kết luận
Workflow **Think‑Plan‑Act** với Llama-4 trên n8n mang lại cách tiếp cận **no-code** mạnh mẽ để xây dựng các agent AI có thể suy luận, lập kế hoạch và thực thi tự động. Bạn chỉ cần cấu hình credential OpenRouter, thiết lập webhook và (tùy chọn) tweak một few code nodes – sau đó, hệ thống sẽ hoạt động liên tục, trả về kết quả có cấu trúc sẵn sàng để tích hợp vào bất kỳ ứng dụng nào.

🚀 **Hãy import ngay, kích hoạt webhook và trải nghiệm sức mạnh của AI reasoning mà không cần viết một dòng code!**