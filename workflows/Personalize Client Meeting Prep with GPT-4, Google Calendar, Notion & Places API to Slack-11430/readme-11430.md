---
title: "🎁 Tự Động Hóa Gợi Ý Quà Tặng & Quán Café Đặc Biệt cho Cuộc Hẹn Khách Hàng với GPT-4, Google Calendar & Notion"
description: "Workflow này tự động tìm kiếm và gợi ý quà tặng cá nhân hóa cùng địa điểm café phù hợp trước mỗi cuộc gặp khách hàng, dựa trên sở thích khách hàng được lưu trong Notion. Giúp các sếp sales và account manager làm ấn tượng với khách hàng chỉ trong vài giây!"
slug: "tieu-dong-hoa-gi-re-qua-tang-cafe-voi-gpt-4-notion-slack"
tags: [n8n, automation, no-code, sales-automation, ai-summarization, google-calendar, notion-api, slack-integration]
keywords: [n8n workflow tự động hóa, gợi ý quà tặng cá nhân hóa, AI GPT-4 cho sales, tự động hóa cuộc họp khách hàng, Notion + Slack + Google Calendar]
---

# 🎁 **Tự Động Hóa Gợi Ý Quà Tặng & Quán Café Đặc Biệt cho Cuộc Hẹn Khách Hàng**

### **🔥 Nỗi Đau Của Các Sếp Sales & Account Manager**
Bạn có bao giờ phải **tìm kiếm quà tặng phù hợp** cho khách hàng trong thời gian ngắn trước một cuộc gặp? Hoặc **không biết chọn quán café nào** để chuẩn bị trước cuộc họp? Thời gian chuẩn bị này không chỉ tốn công sức mà còn **rủi ro chọn sai**, làm mất ấn tượng với khách hàng.

Với **workflow này**, các sếp sẽ:
✅ **Tự động nhận được gợi ý quà tặng & café** dựa trên sở thích khách hàng (được lưu trong Notion).
✅ **Tiết kiệm thời gian** từ 30-60 phút mỗi tuần.
✅ **Làm ấn tượng khách hàng** với những gợi ý cá nhân hóa, phù hợp với sở thích cá nhân.
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không phải tìm kiếm quà tặng và địa điểm café thủ công.
- **Cá nhân hóa hoàn toàn**: Gợi ý dựa trên sở thích khách hàng (được lưu trong Notion).
- **Hoạt động tự động**: Workflow chạy ngay khi có sự kiện mới trong Google Calendar.
- **Gửi thông báo Slack**: Nhận kết quả ngay trên kênh Slack, không phải mở nhiều tab.
- **Đa dạng gợi ý**: Từ quà tặng đến địa điểm café phù hợp với thời gian.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Google Calendar** (để trigger sự kiện).
✔ **Notion Database** với 2 trường:
   - **Tên Công Ty** (Title)
   - **Sở Thích** (Text) – Ví dụ: *"Yêu macaron Pháp"*, *"Thích café yên tĩnh"*.
✔ **Google Places API Key** (để tìm kiếm địa điểm gần đó).
✔ **OpenAI API Key** (để sử dụng GPT-4 gợi ý).
✔ **Slack Workspace** (để gửi thông báo kết quả).
✔ **Tài khoản OAuth2** cho:
   - Google Calendar
   - Slack
   - Notion
   - OpenAI
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/11430](https://n8n.io/workflows/11430) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ link trên và paste vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflows này có **9 node chính**, các sếp cần chú ý cấu hình các node sau:

##### **🔹 Node "Google Calendar Trigger" (n8n-nodes-base.googleCalendarTrigger)**
- **Cấu hình**:
  - Chọn **credentials**: `googleCalendarOAuth2Api`.
  - **Event Type**: Chọn **"Event Created"** hoặc **"Event Updated"**.
  - **Filter Events**: Chỉ lọc sự kiện chứa từ khóa:
    - `visit`, `meeting`, `client`, `dinner`, `greeting` (có thể tùy chỉnh theo phong cách đặt tên của các sếp).
  - **Output Format**: Chọn `json`.

##### **🔹 Node "Extract Company Name" (n8n-nodes-base.code)**
- **Mã JavaScript**:
  ```javascript
  // Lấy tên công ty từ tiêu đề sự kiện (ví dụ: "Meeting with ABC Corp")
  const eventTitle = $input.all()[0].event.title;
  const companyName = eventTitle.split("with ")[1]?.split(" ")[0]; // Giả sử định dạng tiêu đề là "Meeting with [Company]"
  return { json: { companyName } };
  ```
  - **Lưu ý**: Các sếp cần **điều chỉnh regex** phù hợp với cách đặt tên sự kiện trong Google Calendar của mình.

##### **🔹 Node "Get Customer Preferences from Notion" (n8n-nodes-base.notion)**
- **Cấu hình**:
  - **Credentials**: `notionApi`.
  - **Database Name**: Tên cơ sở dữ liệu Notion chứa thông tin khách hàng.
  - **Filter**: Lọc theo trường `Company Name` bằng tên công ty được trích xuất từ node trước.
  - **Output**: Chọn `json`.

##### **🔹 Node "AI Gift Recommendation" (n8n-nodes-langchain.openAi)**
- **Cấu hình**:
  - **Credentials**: `openAiApi`.
  - **Model**: Chọn `gpt-4` (hoặc `gpt-3.5-turbo` nếu không có API key GPT-4).
  - **Prompt**:
    ```plaintext
    Bạn là một chuyên gia gợi ý quà tặng và địa điểm café. Dựa trên thông tin sau:
    - Tên công ty: {{ $json.companyName }}
    - Sở thích của khách hàng: {{ $json.preferences }}

    Hãy gợi ý:
    1. Một cửa hàng quà tặng phù hợp (ví dụ: "Patisserie Sadaharu AOKI" với lý do "khách hàng yêu macaron Pháp").
    2. Một quán café yên tĩnh, gần địa điểm cuộc họp (nếu có địa chỉ trong sự kiện).
    Đảm bảo gợi ý có lý do rõ ràng và phù hợp với sở thích của khách hàng.
    ```
  - **Temperature**: 0.7 (để kết quả sáng tạo nhưng không quá ngẫu nhiên).

##### **🔹 Node "Send Slack Notification" (n8n-nodes-base.slack)**
- **Cấu hình**:
  - **Credentials**: `slackOAuth2Api`.
  - **Channel ID**: Điền ID kênh Slack muốn gửi thông báo (có thể tìm bằng cách mở kênh > URL > phần `C=...`).
  - **Message Format**:
    ```json
    {
      "blocks": [
        {
          "type": "section",
          "text": {
            "type": "mrkdwn",
            "text": "*🎁 Gợi ý quà tặng & café cho cuộc họp với {{ $json.companyName }}*"
          }
        },
        {
          "type": "section",
          "text": {
            "type": "mrkdwn",
            "text": "💡 *Quà tặng:* {{ $json.aiRecommendation.giftShop }}"
          }
        },
        {
          "type": "section",
          "text": {
            "type": "mrkdwn",
            "text": "📍 *Lý do:* {{ $json.aiRecommendation.giftReason }}"
          }
        },
        {
          "type": "section",
          "text": {
            "type": "mrkdwn",
            "text": "☕ *Café gợi ý:* {{ $json.aiRecommendation.cafe }}"
          }
        }
      ]
    }
    ```
  - **Lưu ý**: Các sếp cần **điều chỉnh template** phù hợp với kết quả từ GPT-4.

##### **🔹 Node "Workflow Configuration" (n8n-nodes-base.set)**
- **Tham số cần điền**:
  - `googlePlacesApiKey`: API key của Google Places (mua tại [Google Cloud Console](https://console.cloud.google.com/)).
  - `searchRadius`: Bán kính tìm kiếm (mét, mặc định 1000m).
  - `minRating`: Đánh giá tối thiểu cho địa điểm (mặc định 4.5).

---

#### **3. Kích Hoạt ⚡️**
- **Test Run**: Chạy thử với một sự kiện mẫu trong Google Calendar để kiểm tra kết quả.
- **Bật Active**: Sau khi kiểm tra thành công, bật **Active** để workflow chạy tự động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Zoom/Teams**:
   - Sử dụng node **Zoom API** để lấy địa chỉ cuộc họp và tự động gợi ý café gần đó.

2. **Lưu Log Kết Quả**:
   - Thêm node **Google Sheets** hoặc **Notion** để lưu lịch sử gợi ý, giúp theo dõi hiệu quả.

3. **Gửi Báo Cáo Định Kỳ**:
   - Sử dụng **n8n Scheduler** để gửi báo cáo tổng hợp gợi ý hàng tuần qua email (node **Send Email**).

4. **Tùy Chỉnh Từ Khóa**:
   - Nếu các sếp đặt tên sự kiện theo cách riêng (ví dụ: "Customer Visit"), hãy **cập nhật từ khóa** trong node `Filter Client Visit Events`.

5. **Sử Dụng API Key Miễn Phí**:
   - Nếu không có API key GPT-4, có thể thử **Mistral AI** (miễn phí) hoặc **Claude** (Anthropic) với node `@n8n/nodes-langchain.mistral`.

---

### 📌 **Kết Luận**
Workflows này **giải phóng thời gian** cho các sếp sales và account manager, giúp họ **chuẩn bị cuộc họp một cách chuyên nghiệp và cá nhân hóa** chỉ trong vài giây. **Không cần code**, chỉ cần cấu hình và chạy!

**🚀 Hãy import ngay và thử nghiệm với một khách hàng đầu tiên!** Nếu có vấn đề, các sếp có thể **đăng câu hỏi trên [n8n Community](https://community.n8n.io/)** hoặc liên hệ với tôi để hỗ trợ.

---
**💡 Chúc các sếp thành công với chiến dịch sales mới!** 🚀