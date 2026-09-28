---
title: "🔍 **Tự Động Học OAuth2 Settings với AI Llama 3.3 & OpenRouter - Không Cần Code!**"
description: "Workflow này tự động trích xuất thông tin OAuth2 (Authorization URI, Token URI, Audience) từ văn bản bằng AI Llama 3.3, kết hợp với OpenRouter, giúp phát triển viên tiết kiệm thời gian và giảm sai sót khi cấu hình API. Kết quả được định dạng JSON chuẩn với hệ thống đánh giá độ tin cậy (confidence score)."
slug: "tieu-dong-hoach-oauth2-settings-ai-llama-3-3"
tags: [n8n, automation, ai, api, oauth2, openrouter, llama-3.3, no-code]
keywords: [n8n workflow oauth2, tự động hóa api, ai trích xuất dữ liệu, llm llama 3.3, cấu hình oauth2 không code, openrouter n8n]
---

# 🚀 **Tự Động Học OAuth2 Settings với AI Llama 3.3 & OpenRouter**

### **Giải pháp cho ai?**
Các sếp phát triển viên, kỹ sư IT hoặc nhà quản trị hệ thống đang phải **tìm kiếm thủ công** thông tin OAuth2 (URL đăng ký, URL lấy token, audience) trong tài liệu API hoặc mã nguồn? Hoặc đang **mất thời gian** vì phải đọc hiểu các tài liệu kỹ thuật phức tạp để cấu hình API?

Workflow này **tự động hóa toàn bộ quá trình** bằng cách sử dụng **AI Llama 3.3 (70B)** kết hợp với **OpenRouter**, trích xuất thông tin OAuth2 từ văn bản đầu vào và **định dạng thành JSON chuẩn** với hệ thống đánh giá độ tin cậy (confidence score). Kết quả sẽ được truyền tiếp cho các workflow khác để tự động hóa quy trình cấu hình API hoàn toàn.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần đọc tài liệu API phức tạp để tìm OAuth2 settings.
- **Độ chính xác cao**: AI Llama 3.3 phân tích và trích xuất thông tin với **confidence score** (0 < x ≤ 1), giúp các sếp đánh giá độ tin cậy của kết quả.
- **Hoạt động liên tục**: Workflow có thể được kích hoạt từ các sự kiện khác (ví dụ: khi có yêu cầu mới từ Slack/Email).
- **Dữ liệu chuẩn hóa**: Kết quả được định dạng JSON, dễ dàng tích hợp vào các hệ thống khác (CRM, database, hoặc workflow tiếp theo).
- **Tùy chỉnh linh hoạt**: Có thể thay đổi prompt AI hoặc schema JSON để phù hợp với yêu cầu cụ thể của dự án.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản OpenRouter API**:
   - API Key từ [OpenRouter](https://openrouter.ai/) (đăng ký miễn phí).
   - Model được sử dụng: `latitudegames/wayfarer-large-70b-llama-3.3` (miễn phí trong giới hạn).
2. **Workflow gọi trigger**:
   - Workflow này được thiết kế để **bị kích hoạt bởi workflow khác** (ví dụ: khi có yêu cầu mới từ Slack, Email, hoặc form).
  . **Dữ liệu đầu vào**:
   - Văn bản chứa thông tin OAuth2 (ví dụ: tài liệu API, mã nguồn, hoặc văn bản tự động trích xuất từ trang web).
   - Ví dụ văn bản đầu vào:
     ```
     Service Name: GitHub
     Authorization URI: https://github.com/login/oauth/authorize
     Token URI: https://github.com/login/oauth/access_token
     Audience: api.github.com
     Details: Standard OAuth2 flow with PKCE support
     Confidence: 0.98
     ```

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Truy cập [n8n.io](https://n8n.io/) và đăng nhập vào workspace.
2. Nhấn **"Create"** → **"Import Workflow"**.
3. Chọn file JSON hoặc paste JSON từ [link gốc](https://n8n.io/workflows/3279).
4. Nhấn **"Import"** để hoàn tất.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này bao gồm **5 node chính**, các sếp cần cấu hình như sau:

##### **A. Node "When Executed by Another Workflow" (Trigger)**
- **Chức năng**: Workflow này **không tự động chạy**, mà được kích hoạt bởi workflow khác.
- **Cách cấu hình**:
  - Đảm bảo workflow gọi trigger đã được **bật (Active)** và truyền dữ liệu đầu vào (JSON) vào node này.
  - Ví dụ: Nếu gọi từ Slack, dữ liệu sẽ được truyền dưới dạng `{"text": "Tìm OAuth2 settings cho API GitHub"}`.

##### **B. Node "OpenRouter Chat Model" (AI Llama 3.3)**
- **Chức năng**: Sử dụng AI Llama 3.3 để phân tích văn bản và trích xuất OAuth2 settings.
- **Cấu hình bắt buộc**:
  1. **Credentials**:
     - Chọn `openRouterApi` (đã cấu hình trước trong n8n).
     - Đảm bảo API Key đã được thêm vào **Credentials Manager** của n8n.
  2. **Key Parameters**:
     - **Model**: Đặt thành `latitudegames/wayfarer-large-70b-llama-3.3` (không thay đổi).
     - **Prompt**: Workflow đã tự động cấu hình prompt để trích xuất:
       ```
       Tìm kiếm và trích xuất thông tin OAuth2 từ văn bản sau:
       - Authorization URI
       - Token URI
       - Audience
       - Service Name (nếu có)
       - Chi tiết bổ sung (nếu có)
       Đánh giá độ tin cậy (confidence score) từ 0 đến 1 cho mỗi trường.
       ```
     - **Input Data**: Chọn `JSON` từ node trigger.

##### **C. Node "Structured Output Parser"**
- **Chức năng**: Định dạng output của AI thành JSON chuẩn.
- **Cấu hình**:
  - Schema JSON mặc định đã được thiết lập trong workflow. Các sếp **không cần chỉnh sửa** trừ khi yêu cầu khác.
  - Ví dụ output:
    ```json
    {
      "service_name": "GitHub",
      "audience": "api.github.com",
      "authorization_uri": "https://github.com/login/oauth/authorize",
      "token_uri": "https://github.com/login/oauth/access_token",
      "details": "Standard OAuth2 flow with PKCE support",
      "confidence": 0.98
    }
    ```

##### **D. Node "Conform JSON" (Code Node)**
- **Chức năng**: Xử lý lỗi định dạng hoặc điều chỉnh output nếu AI trả về định dạng không chuẩn.
- **Cấu hình**:
  - Mặc định, node này đã được cấu hình để **chuyển đổi văn bản thô của AI thành JSON** theo schema.
  - **Mã nguồn**:
    ```javascript
    const items = $input.all();
    const originalText = items[0].json.output.text;
    const lines = originalText.split('\n');
    const service_name = lines[0].split(': ')[1];
    const audience = lines[1].split(': ')[1];
    const authorization_uri = lines[2].split(': ')[1];
    const token_uri = lines[3].split(': ')[1];
    const details = lines[4].split(': ')[1];
    const confidence = parseFloat(lines[5].split(': ')[1]);
    return [
      {
        json: {
          output: {
            service_name,
            audience,
            authorization_uri,
            token_uri,
            details,
            confidence
          }
        }
      }
    ];
    ```
  - **Lưu ý**:
    - Nếu văn bản đầu vào của AI **khác với định dạng trên**, các sếp cần **cập nhật mã trong Code Node** để phù hợp.
    - Ví dụ: Nếu AI trả về định dạng JSON trực tiếp, có thể bỏ qua node này.

##### **E. Node "LLM Bus" & "Structured Output Parser"**
- **Chức năng**: Quản lý luồng dữ liệu giữa AI và parser.
- **Không cần chỉnh sửa** (đã cấu hình sẵn).

---

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Nhấn **"Run"** trên node trigger để gửi dữ liệu mẫu (ví dụ: văn bản OAuth2 của GitHub).
   - Kiểm tra output ở node cuối cùng (JSON) để đảm bảo kết quả chính xác.
2. **Bật Active**:
   - Sau khi test thành công, nhấn **"Active"** trên workflow để chạy liên tục.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tích hợp với Slack/Telegram**:
   - Sử dụng node **Slack/Telegram Webhook** để gửi yêu cầu trích xuất OAuth2 từ chat.
   - Ví dụ: Khi người dùng gửi tin nhắn `"Tìm OAuth2 cho API [Tên API]"` → Workflow tự động trả về kết quả.

2. **Lưu log kết quả**:
   - Sử dụng node **Google Sheets** hoặc **Notion** để lưu lịch sử trích xuất OAuth2.
   - Cấu hình node **Set** để truyền dữ liệu JSON vào sheet.

3. **Gửi báo cáo định kỳ**:
   - Sử dụng node **Schedule** để chạy workflow hàng ngày và gửi báo cáo OAuth2 mới nhất qua Email (n8n-node-email).

4. **Tùy chỉnh prompt AI**:
   - Nếu cần trích xuất thông tin khác (ví dụ: OAuth2 settings cho API cụ thể), cập nhật prompt trong node **OpenRouter Chat Model**:
     ```plaintext
     Tìm kiếm và trích xuất thông tin OAuth2 cho API [Tên API] từ văn bản sau:
     - Client ID
     - Client Secret (nếu có)
     - Scopes
     - Redirect URI
     ```

5. **Sử dụng với API khác**:
   - Workflow này không chỉ dành cho OAuth2, mà có thể **tùy chỉnh** để trích xuất thông tin khác từ văn bản (ví dụ: cấu hình JWT, API keys).

---

### 📌 **Kết luận**
Workflow **OAuth2 Settings Finder** là giải pháp **tự động hóa hoàn toàn** để các sếp phát triển viên và kỹ sư IT **không cần đọc tài liệu API phức tạp** mà vẫn có thể **nhanh chóng và chính xác** lấy được thông tin OAuth2 cần thiết.

👉 **Áp dụng ngay** để tiết kiệm thời gian và giảm thiểu sai sót trong quá trình cấu hình API!

---
**Gợi ý tiếp theo**:
- [Tự động hóa OAuth2 với Slack](link-workflow-slack)
- [Tích hợp OAuth2 vào CRM](link-workflow-crm)