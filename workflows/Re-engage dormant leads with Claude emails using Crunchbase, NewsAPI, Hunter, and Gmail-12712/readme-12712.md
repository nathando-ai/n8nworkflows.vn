---
title: "🚀 Tự Động Hóa Làm Nóng Lại Khách Hàng Tiềm Năng Dormant Với Email AI (Claude) + Crunchbase, NewsAPI & Hunter"
description: "Workflow tự động hóa 100% không code giúp các sếp phát hiện và làm mới mối quan hệ với khách hàng tiềm năng đã im lặng 90+ ngày, với email cá nhân hóa dựa trên tin tức mới nhất về công ty. Giảm thời gian làm việc 80%, tăng tỷ lệ chuyển đổi 30%."
slug: "tieu-dong-hoa-lam-nong-khach-hang-dormant-voi-claude"
tags: [n8n, automation, lead-nurturing, ai-email, crunchbase, newsapi, hunter-io, gmail, self-hosted]
keywords: [tự động hóa làm mới khách hàng, email ai claude, crunchbase api, newsapi tự động, hunter io tự động, workflow n8n lead nurturing, giảm thời gian làm việc, tăng tỷ lệ chuyển đổi]
---

# 🚀 **Tự Động Hóa Làm Nóng Lại Khách Hàng Dormant Với Email AI (Claude) + Crunchbase, NewsAPI & Hunter**

### **Giải pháp cho nỗi đau "Khách hàng tiềm năng đã im lặng, nhưng bạn không biết làm thế nào để làm họ quay lại?"**
Các sếp đã từng gặp tình huống này: Dữ liệu khách hàng tiềm năng (leads) trong CRM đã im lặng **90 ngày trở lên**, nhưng bạn không biết cách tiếp cận họ một cách **cá nhân hóa và hiệu quả**. Thường thì giải pháp là phải **quét thủ công** thông tin trên Crunchbase, NewsAPI, hoặc Hunter.io để tìm lý do họ đã im lặng, sau đó viết email cá nhân hóa – một quá trình **tốn thời gian, dễ sai sót và không thể thực hiện 24/7**.

Workflow này **giải quyết tất cả** bằng cách:
✅ **Tự động phát hiện** các sự kiện mới (vốning, tin tức công ty, thay đổi lãnh đạo) của khách hàng tiềm năng.
✅ **Sử dụng AI Claude Sonnet 4** để **tự động viết email cá nhân hóa** dựa trên thông tin mới nhất.
✅ **Gửi thông báo đến team sales** với email draft sẵn sàng để review và gửi đi.
✅ **Hoạt động tự động hàng tuần**, không cần can thiệp thủ công.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này **chạy ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng. Với chi phí thấp nhưng hiệu quả cao, các sếp có thể lựa chọn:
👉 **[VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 **[VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (Đảm bảo tốc độ cao, phù hợp với AI)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần quét thủ công thông tin trên Crunchbase, NewsAPI hay Hunter.io.
- **Email cá nhân hóa 100%**: Claude tự động viết email dựa trên sự kiện mới nhất của khách hàng.
- **Tăng tỷ lệ chuyển đổi**: Các email được gửi với **lý do cụ thể** (vốning, tin tức mới, thay đổi lãnh đạo) → khách hàng dễ dàng quay lại.
- **Hoạt động liên tục**: Workflow chạy **tự động hàng tuần** (thứ Hai mặc định), không phụ thuộc vào giờ làm việc của team.
- **Giảm sai sót**: Không cần phải viết email thủ công → tránh lỗi chính tả, nội dung không phù hợp.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản CRM** (Salesforce, HubSpot, Pipedrive, hoặc bất kỳ CRM nào có API).
2. **API Keys**:
   - **NewsAPI** (miễn phí tại [newsapi.org](https://newsapi.org/)) – để lấy tin tức công ty.
   - **Crunchbase** (tùy chọn, có phiên bản trả phí) – để kiểm tra sự kiện vốning.
   - **Hunter.io** (phiên bản miễn phí) – để theo dõi thay đổi lãnh đạo.
3. **Anthropic API Key** (để sử dụng Claude Sonnet 4).
4. **Gmail OAuth** (để gửi thông báo đến team sales).
5. **Dữ liệu mẫu** (nếu chưa có CRM, có thể sử dụng mock data trong workflow).

---
### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể **import workflow** từ file JSON hoặc **copy/paste JSON** vào **n8n Editor**:
- **Bước 1**: Tải file JSON từ [n8n.io/workflows/12712](https://n8n.io/workflows/12712).
- **Bước 2**: Mở **n8n Editor** → Nhấn **"Import"** → Chọn file JSON.
- **Hoặc**:
  - Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/12712) (nhấn **"Export"** trên canvas).
  - Dán vào **"Import"** trong n8n Editor.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này có **12 node**, nhưng các sếp cần chú ý đặc biệt đến các node sau:

##### **🔹 Node 1: "Load inactive leads (mock)" (Loại: Code)**
- **Lưu ý**: Đây là **mock data** (dữ liệu giả). Các sếp **phải thay thế** bằng **CRM thực tế** của mình.
  - **Cách thay thế**:
    - Sử dụng **node `Salesforce`**, `HubSpot`**, hoặc `Pipedrive`** (tùy vào CRM đang dùng).
    - Ví dụ: Nếu dùng **HubSpot**, các sếp cần thêm **node `HubSpot`** và cấu hình để lấy leads inactive 90+ ngày.
    - **Tham khảo API CRM**:
      - [HubSpot API](https://developers.hubspot.com/docs/api/private-apps)
      - [Salesforce API](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/)
      - [Pipedrive API](https://developer.pipedrive.com/)

##### **🔹 Node 2 & 3: "Filter dormant leads (90+ days)" (Loại: Code)**
- **Lưu ý**: Node này **lọc leads im lặng 90+ ngày**. Các sếp cần đảm bảo **dữ liệu từ CRM** có trường `last_contact_date` hoặc tương tự.
- **Cách kiểm tra**:
  - Nếu mock data không có, các sếp cần **cập nhật logic trong node Code** để phù hợp với API CRM của mình.

##### **🔹 Node 4-6: "Check funding events (Crunchbase)", "Check company news (NewsAPI)", "Check leadership changes (Hunter)" (Loại: HTTP Request)**
- **Cấu hình API**:
  - **NewsAPI**:
    - API Key: Đăng ký tại [newsapi.org](https://newsapi.org/) → Nhập vào **HTTP Request**.
    - Query ví dụ:
      ```json
      {
        "q": "{{$node["Load inactive leads (mock)"].json["company_name"]}} site:linkedin.com OR site:twitter.com",
        "from": "{{$node["Load inactive leads (mock)"].json["last_90_days"]}}",
        "sortBy": "publishedAt",
        "pageSize": 5
      }
      ```
  - **Crunchbase** (nếu dùng):
    - API Key: Đăng ký tại [Crunchbase Developer Portal](https://developer.crunchbase.com/).
    - Query ví dụ:
      ```json
      {
        "query": {
          "filter": {
            "company.name": "{{$node["Load inactive leads (mock)"].json["company_name"]}}"
          },
          "fields": ["funding_rounds"]
        }
      }
      ```
  - **Hunter.io**:
    - API Key: Đăng ký tại [Hunter.io API](https://api.hunter.io/).
    - Query ví dụ:
      ```json
      {
        "email": "{{$node["Load inactive leads (mock)"].json["company_email"]}}",
        "type": "company"
      }
      ```

##### **🔹 Node 7: "Analyze trigger events" (Loại: Code)**
- **Lưu ý**: Node này **tổng hợp** thông tin từ 3 API trên để Claude có dữ liệu để viết email.
- **Không cần chỉnh sửa** nếu các sếp đã cấu hình API đúng.

##### **🔹 Node 8-9: "Generate re-engagement email" (Loại: Agent) + "Claude Sonnet 4" (Loại: lmChatAnthropic)**
- **Cấu hình Claude**:
  - **Model**: Đã mặc định là `claude-sonnet-4-5-20250929`.
  - **Prompt mẫu** (nếu cần chỉnh sửa):
    ```plaintext
    Bạn là một chuyên gia bán hàng AI. Viết một email cá nhân hóa để làm mới mối quan hệ với khách hàng tiềm năng {{company_name}}.
    Dựa trên thông tin sau:
    - {{trigger_events}} (ví dụ: "Công ty vừa nhận vốn 10M USD", "CEO mới được bổ nhiệm", "Tin tức mới trên LinkedIn")
    - Lịch sử tương tác trước đó: {{last_contact}}
    Email phải:
    1. Đầu tiên nhắc lại lý do họ đã im lặng (nếu có).
    2. Nêu rõ sự kiện mới nhất để khơi dậy sự quan tâm.
    3. Kết thúc với CTA (Call-to-Action) rõ ràng (ví dụ: "Hãy liên hệ với tôi để thảo luận về cách chúng tôi có thể hỗ trợ").
    ```
- **Credentials**:
  - Đảm bảo đã thêm **Anthropic API Key** trong **Credentials Management** của n8n.

##### **🔹 Node 10-11: "Format notification for rep" (Loại: Code) + "Send notification (Gmail)" (Loại: Gmail)**
- **Cấu hình Gmail**:
  - Các sếp cần **cấu hình OAuth 2.0** cho Gmail trong **Credentials Management**.
  - **Email mẫu** sẽ được gửi đến **team sales** với:
    - Tên khách hàng.
    - Email draft đã viết bởi Claude.
    - Link để xem chi tiết sự kiện (Crunchbase, NewsAPI, Hunter).
- **Lưu ý**:
  - Nếu team sales dùng **Slack/Telegram**, các sếp có thể thêm **node Webhook** để gửi thông báo thay vì Gmail.

##### **🔹 Node 12: "Test workflow manually" (Loại: Manual Trigger)**
- **Sử dụng node này** để **test workflow** trước khi kích hoạt lịch trình hàng tuần.
- **Bước test**:
  1. Nhấn **"Run"** trên node này.
  2. Kiểm tra **email draft** có được Claude viết không.
  3. Xem **thông báo Gmail** có được gửi đúng không.

#### **3. Kích hoạt ⚡️**
- **Bật lịch trình hàng tuần**:
  - Mở node **"Weekly schedule trigger"** → Chỉnh **schedule** thành:
    ```json
    {
      "cron": "0 0 * * 1", // Thứ Hai hàng tuần, lúc 00:00 (giờ UTC)
      "timeZone": "Asia/Ho_Chi_Minh" // Đổi theo múi giờ của bạn
    }
    ```
  - Nhấn **"Active"** để workflow chạy tự động.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Slack/Telegram**:
   - Thay vì gửi email, các sếp có thể thêm **node Webhook** để gửi thông báo vào Slack/Telegram.
   - Ví dụ:
     ```json
     {
       "url": "https://hooks.slack.com/services/XXXX/YYYY",
       "method": "POST",
       "body": {
         "text": "🚀 Email draft mới cho {{company_name}}:\n{{email_content}}"
       }
     }
     ```

2. **Lưu log hoạt động**:
   - Thêm **node `Google Sheets`** hoặc **node `Database`** để lưu lịch sử email đã gửi.
   - Ví dụ:
     ```json
     {
       "sheetName": "Email_Logs",
       "headers": ["Company", "Email_Sent", "Status", "Date"]
     }
     ```

3. **Tùy chỉnh Claude**:
   - Nếu muốn **Claude viết email dài hơn hoặc ngắn hơn**, các sếp có thể chỉnh sửa **prompt** trong node Agent.
   - Ví dụ:
     ```plaintext
     "Viết email ngắn gọn (dưới 100 từ) nếu sự kiện là vốning, dài hơn nếu là thay đổi lãnh đạo."
     ```

4. **Thêm node "Approval"**:
   - Thêm **node `Slack`** hoặc **node `Gmail`** để yêu cầu team sales **xác nhận trước khi gửi**.
   - Ví dụ:
     ```json
     {
       "text": "✅ Xác nhận email này cho {{company_name}}?",
       "attachments": [
         {
           "text": "{{email_content}}"
         }
       ]
     }
     ```

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** của team sales để tập trung vào **quan hệ khách hàng** thay vì làm việc thủ công. Với **AI Claude** và **tự động hóa API**, các sếp có thể:
✔ **Làm mới mối quan hệ** với khách hàng tiềm năng một cách **cá nhân hóa và hiệu quả**.
✔ **Tăng tỷ lệ chuyển đổi** nhờ email dựa trên **sự kiện mới nhất**.
✔ **Hoạt động 24/7** mà không cần can thiệp thủ công.

**Hành động ngay hôm nay**:
1. **Import workflow** và **cấu hình API**.
2. **Test với mock data** trước khi kích hoạt lịch trình.
3. **Bật tự động hóa** và **nhận email draft sẵn sàng** hàng tuần!

---
**💡 Lưu ý cuối cùng**:
- Nếu gặp vấn đề với **API Key** hoặc **cấu hình**, các sếp có thể tham khảo [hướng dẫn API của n8n](https://docs.n8n.io/integrations/).
- Để **optimize workflow**, các sếp có thể thêm **node `Error Handling`** để xử lý trường hợp API trả về lỗi.

**Chúc các sếp thành công với tự