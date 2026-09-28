---
title: "🤖 **Tự Động Hóa & Phân Loại Tin Nhắn Hỗ Trợ DevOps Với Slack + GPT-5.5 (Miễn Code!)**"
description: "Workflow tự động nhận, phân loại và phân phối tin nhắn hỗ trợ kỹ thuật DevOps từ Slack sang các bộ phận phù hợp bằng trí tuệ nhân tạo (GPT-5.5), tiết kiệm thời gian lên đến 80% cho team IT. Hỗ trợ 7 loại vấn đề phổ biến: sửa lỗi CI/CD, incident, yêu cầu mới hệ thống, và nhiều hơn."
slug: "tieu-dong-hoa-phan-loai-tin-nhan-devops-slack-gpt-5-5"
tags: [n8n, automation, devops, ai-summarization, slack-integration, gpt-5-5, ticket-management]
keywords: [n8n workflow devops, tự động hóa hỗ trợ kỹ thuật, phân loại tin nhắn slack với ai, gpt-5-5 n8n, quản lý ticket devops, slack mcp server, embeddings google gemini]
---

# 🚀 **Tự Động Hóa Phân Loại & Phân Phối Tin Nhắn Hỗ Trợ DevOps Bằng Slack + GPT-5.5**

## **🔥 Nỗi Đau Của Các Sếp DevOps**
Hàng ngày, team DevOps phải:
- **Làm thủ công** theo dõi hàng trăm tin nhắn hỗ trợ trên Slack từ các engineer, client, hoặc team khác.
- **Phân loại và phân phối** yêu cầu kỹ thuật vào các bộ phận phù hợp (CI/CD, Infrastructure, Incident Response...) một cách chậm chạp và dễ sai sót.
- **Mất thời gian** để tổng hợp, trả lời và theo dõi tiến độ, dẫn đến **trải nghiệm người dùng kém** và **giải quyết vấn đề chậm trễ**.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Nhận tin nhắn** từ Slack khi bot được nhắc đến (`@your-oncall-bot`).
✅ **Phân loại tự động** với GPT-5.5 (hoặc OpenAI/Anthropic) vào **7 loại vấn đề** (CI/CD, Infrastructure, Incident, Question, New System, Announcement, Other).
✅ **Trích xuất thông tin chi tiết** (người gửi, nội dung, file đính kèm, độ tin cậy phân loại).
✅ **Phân phối tự động** vào các workflow phụ phù hợp (các sếp có thể **mở rộng** thêm logic riêng).
✅ **Tích hợp với Qdrant** để cải thiện độ chính xác phân loại qua thời gian.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và tối ưu hóa hiệu suất AI, các sếp nên **self-host n8n** trên VPS chuyên dụng:
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đảm bảo tốc độ xử lý nhanh cho AI)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** của team DevOps trong việc phân loại và phân phối ticket.
- **Chính xác cao** với phân loại tự động bằng GPT-5.5 (hoặc Gemini) và hệ thống vector Qdrant.
- **Cá nhân hóa phản hồi**: Trích xuất tên người gửi và thông tin chi tiết từ Slack.
- **Hoạt động liên tục**: Không cần can thiệp thủ công, chạy 24/7 trên VPS.
- **Mở rộng dễ dàng**: Các sếp có thể **thêm logic riêng** vào các nhánh phân phối (CI/CD, Infrastructure, Incident...).
- **Tích hợp AI nâng cao**: Sử dụng **Embeddings Google Gemini** để cải thiện độ chính xác phân loại qua thời gian.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **API Keys**:
   - **OpenAI/GPT-5.5** (hoặc **Anthropic**): Để phân loại tin nhắn.
   - **Google Gemini API Key**: Để tạo **Embeddings** (model `gemini-embedding-2-preview`) và cải thiện hệ thống Qdrant.
   - **Qdrant API Key**: Để lưu trữ và tìm kiếm vector cho phân loại tự động.
   - **Slack OAuth Token**: Để lấy thông tin người dùng (tên, ID).
   - **Slack MCP Bearer Token**: Để tương tác với **Slack MCP Server** (xem [hướng dẫn dưới đây](#slack-mcp-server)).

2. **Dịch vụ bên ngoài**:
   - **Slack App**: Cấu hình **Events API** để gửi tin nhắn đến webhook của n8n.
   - **Qdrant Server**: Để lưu trữ và quản lý vector embeddings.
   - **Slack MCP Server**: [Tải tại đây](https://github.com/korotovsky/slack-mcp-server) (cần cài đặt và cấu hình URL trong workflow).

3. **Tham số cấu hình**:
   - **CHAT_TOKEN**: Giá trị xác thực trong `SetVars` (phải khớp với **Verification Token** trong Slack App).

---
:::note[CHÚ Ý QUAN TRỌNG]
- Workflow **không hoạt động** nếu thiếu **một trong các API Key** hoặc **Slack App** chưa cấu hình.
- **Không có nhánh xử lý cụ thể** trong template (những sếp có thể **thêm logic riêng** vào các nhánh như `modify_infrastructure`, `incident`, `ci_cd_error`...).
:::

---

## 🚀 **Cách Import & Cấu Hình Workflow**

### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/15827](https://n8n.io/workflows/15827) và import vào **n8n Editor**.
- **Copy/paste JSON** từ file vào **Import Workflow** trong n8n.

:::tip[LƯU Ý]
- **Phiên bản n8n**: Workflow **chỉ tương thích với n8n v2.18.2+**.
- **Không xóa node nào** trong workflow, chỉ **cấu hình** các tham số sau.
:::

---

### **2. Các Bước Cấu Hình BẮT BUỘC 📌**

#### **A. Cấu Hình Credentials**
Các sếp cần **thêm hoặc liên kết credentials** trong **n8n Credentials Manager**:
1. **OpenAI/GPT-5.5**:
   - **Tên credentials**: `openAiApi`
   - **API Key**: Điền vào `apiKey` (từ tài khoản OpenAI).
   - **Model**: Chọn `gpt-5.5` (hoặc `gpt-4o` nếu không có).

2. **Google Gemini**:
   - **Tên credentials**: `googlePalmApi`
   - **API Key**: Điền từ [Google Cloud Console](https://console.cloud.google.com/).
   - **Model**: `gemini-embedding-2-preview`.

3. **Qdrant**:
   - **Tên credentials**: `qdrantApi`
   - **URL**: Điền địa chỉ Qdrant (ví dụ: `http://localhost:6333`).
   - **API Key**: Nếu cần.

4. **Slack OAuth**:
   - **Tên credentials**: `slackOAuth2Api`
   - **Token**: Lấy từ **Slack App** (cấu hình sau).

5. **Slack MCP**:
   - **Tên credentials**: `httpBearerAuth`
   - **Bearer Token**: Lấy từ **Slack MCP Server** (cấu hình sau).

---

#### **B. Cấu Hình Node Qua Trình**
Các node **quan trọng nhất** cần chỉnh sửa:

| **Node**               | **Cấu Hình Cần Thiết**                                                                 | **Lưu Ý**                                                                 |
|------------------------|--------------------------------------------------------------------------------------|---------------------------------------------------------------------------|
| **GetSlackMessage**     | `path`: Điền **URL Webhook** của n8n (ví dụ: `https://your-n8n-server/webhook/1234567890`). | URL này **phải khớp** với **Slack App Events Subscriptions**.               |
| **SetVars**            | `CHAT_TOKEN`: Điền **Verification Token** từ Slack App.                              | Giá trị này **phải trùng khớp** với token trong Slack App.                 |
| **Qdrant Vector Store**| `collectionName`: Điền tên **collection** trong Qdrant (ví dụ: `devops_support`).      | Nếu chưa có collection, **tạo mới** trong Qdrant.                          |
| **Slack**              | `url`: Điền **URL của Slack MCP Server** (ví dụ: `http://localhost:3000`).          | Cần cài đặt [Slack MCP Server](https://github.com/korotovsky/slack-mcp-server). |
| **OpenAI Chat Model**  | `model`: Chọn `gpt-5.5` (hoặc `gpt-4o`).                                             | Nếu không có GPT-5.5, có thể dùng `gpt-4-turbo`.                          |

---

#### **C. Cấu Hình Slack App & Webhook**
1. **Tạo Slack App**:
   - Truy cập [Slack API](https://api.slack.com/apps) → **Create New App**.
   - Chọn **Event Subscriptions** → **Enable Events**.
   - **Request URL**: Điền **URL Webhook** của n8n (ví dụ: `https://your-n8n-server/webhook/1234567890`).
   - **Signing Secret**: Lưu lại để dùng trong **n8n** (nếu cần).
   - **Bot Token**: Sử dụng để **xác thực tin nhắn** (điền vào `CHAT_TOKEN` trong `SetVars`).

2. **Subscribe Events**:
   - Chọn **app_mentions** (để nhận tin nhắn khi bot được nhắc đến).
   - Cấu hình **Verification Token** (điền vào `SetVars` trong workflow).

3. **Cài đặt Slack MCP Server**:
   - Tải [Slack MCP Server](https://github.com/korotovsky/slack-mcp-server).
   - Cấu hình `config.json` với:
     ```json
     {
       "slack": {
         "token": "xoxb-your-slack-bot-token"
       },
       "webhook": {
         "url": "http://localhost:3000"
       }
     }
     ```
   - Chạy server và điền **URL** vào node `Slack` trong workflow.

---

### **3. Kích Hoạt Workflow ⚡️**
1. **Test Run**:
   - Gửi tin nhắn trên Slack nhắc đến bot (`@your-oncall-bot`).
   - Kiểm tra **Output** trong n8n để xác nhận:
     ```json
     {
       "message": "Tôi gặp lỗi CI/CD khi deploy...",
       "user_name": "JohnDoe",
       "category": "ci_cd_error",
       "confidence": 0.95,
       "summary": "Lỗi CI/CD khi deploy app vào staging..."
     }
     ```
2. **Bật Active**:
   - Chuyển trạng thái workflow từ **Draft** sang **Active**.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**

### **1. Mở Rộng Logic Phân Phối**
Workflow có **7 nhánh phân loại** (đang trống), các sếp có thể:
- **Thêm node Slack/Email** để tự động trả lời người gửi.
- **Kết nối với Jira/Linear** để tạo ticket tự động.
- **Gửi báo cáo định kỳ** về số lượng ticket theo loại.

**Ví dụ**:
```plaintext
- Nhánh "ci_cd_error" → Gửi tin nhắn Slack cho team CI/CD.
- Nhánh "incident" → Gửi email cho team On-call.
- Nhánh "question" → Trả lời tự động với FAQ.
```

### **2. Cải Thiện Độ Chính Xác Phân Loại**
- **Tăng cường Qdrant**: Lưu trữ **lịch sử tin nhắn** để AI học hỏi và phân loại tốt hơn.
- **Sử dụng Embeddings Gemini**: Cải thiện độ tương đồng giữa tin nhắn và các loại vấn đề.
- **Thêm dữ liệu huấn luyện**: Nếu cần, các sếp có thể **tạo collection mới** trong Qdrant với dữ liệu mẫu.

### **3. Tích Hợp Log & Monitoring**
- **Lưu log** vào **Google Sheets/Notion** để theo dõi tiến độ.
- **Gửi báo cáo hàng tuần** về số lượng ticket, thời gian giải quyết.
- **Kết nối với Datadog/New Relic** để monitor hiệu suất.

### **4. Tự Động Trả Lời Người Gửi**
- Thêm node **Slack/Email** vào các nhánh để trả lời tự động:
  ```plaintext
  - Nếu category = "question" → Trả lời: "Cảm ơn bạn! Chúng tôi sẽ hỗ trợ trong 24h."
  - Nếu category = "incident" → Gửi tin nhắn cho team On-call.
  ```

---

## 📌 **Kết Luận: Áp Dụng Ngay!**
Workflow này **giải phóng team DevOps** khỏi việc phân loại tin nhắn thủ công, **tăng tốc độ phản hồi** và **cải thiện trải nghiệm người dùng**. Với **GPT-5.5 + Qdrant**, độ chính xác phân loại **cao hơn 90%**, và **Slack MCP** đảm bảo tương tác mượt mà.

**Các sếp hãy:**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test với tin nhắn mẫu** trước khi bật hoạt động thực tế.
3. **Mở rộng logic** theo nhu cầu của team.

**🚀 Hãy tự động hóa ngay hôm nay!** Nếu có vấn đề, để lại comment dưới đây hoặc liên hệ với **Sergei Byvshev** (tác giả workflow) qua [GitHub](https://github.com/sergei-byvshev).

---
:::note[CHÚ Ý CUỐI CUNG]
- **Không cần biết code**: Workflow hoàn toàn **no-code**, chỉ cần cấu hình API và Slack.
- **Dễ dàng mở rộng**: Các sếp có thể **thêm logic riêng** vào các nhánh phân phối.
- **Tiết kiệm chi phí**: So với việc thuê người hỗ trợ, **n8n + AI** tiết kiệm **hàng ngàn USD/năm**.
:::

---