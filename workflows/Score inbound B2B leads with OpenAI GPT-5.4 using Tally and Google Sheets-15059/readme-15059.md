---
title: "🚀 Tự Động Hóa Đánh Giá Lead B2B Tự Động Với OpenAI GPT-5.4, Tally & Google Sheets - Không Cần Code!"
description: "Workflow tự động hóa đánh giá lead B2B thông minh bằng AI GPT-5.4, tích hợp Tally Forms và Google Sheets. Giúp các sếp tiết kiệm thời gian 80% trong quá trình phân tích và đánh giá lead, đồng thời tự động cập nhật dữ liệu vào bảng tính để theo dõi và quản lý hiệu quả."
slug: "tieu-dong-hoa-danh-gia-lead-b2b-voi-openai-gpt-5-4-tally-google-sheets"
tags: [n8n, automation, no-code, lead-generation, ai-summarization, openai, tally-forms, google-sheets]
keywords: [tự động hóa lead b2b, đánh giá lead bằng ai, gpt-5.4 n8n, tally forms n8n, google sheets automation, tự động hóa bán hàng b2b]
---

# 🚀 **Tự Động Hóa Đánh Giá Lead B2B Tự Động Với AI GPT-5.4, Tally & Google Sheets**

### **Giải pháp cho các sếp muốn tự động hóa quá trình đánh giá lead B2B mà không cần viết code**
Hiện nay, việc đánh giá lead B2B thủ công không chỉ tốn thời gian mà còn dễ bị chủ quan và thiếu chính xác. Các sếp phải dành hàng giờ mỗi ngày để:
- Nhập liệu từ form Tally vào Google Sheets.
- Tìm hiểu thông tin công ty từ website, LinkedIn.
- Phân tích kỹ lưỡng để đánh giá lead theo tiêu chí riêng.
- Cập nhật lại bảng tính để theo dõi tiến độ.

**Workflow này tự động hóa toàn bộ quá trình đó chỉ trong vài giây!** Dựa trên AI GPT-5.4, nó sẽ:
✅ **Tự động thu thập** thông tin từ form Tally (tên công ty, website, LinkedIn, tiêu chí đánh giá).
✅ **Lấy dữ liệu** từ trang chủ của công ty và phân tích nội dung bằng AI.
✅ **Đánh giá lead** từ 1-10 điểm và gán nhãn (A-D) cùng lý do và hành động khuyến nghị.
✅ **Cập nhật tự động** vào Google Sheets để các sếp theo dõi và quản lý dễ dàng.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần nhập liệu thủ công, tự động hóa từ form đến bảng tính.
- **Đánh giá chính xác**: AI GPT-5.4 phân tích thông tin chi tiết từ website và LinkedIn.
- **Cá nhân hóa**: Đánh giá lead theo tiêu chí riêng của doanh nghiệp.
- **Hoạt động liên tục**: Workflow chạy 24/7, không cần can thiệp của con người.
- **Dữ liệu sẵn sàng**: Tất cả thông tin được lưu vào Google Sheets, dễ dàng theo dõi và phân tích.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Tally Forms**:
   - Tạo một form với các trường sau:
     - **Company Name** (Tên công ty)
     - **LinkedIn URL** (Đường dẫn LinkedIn)
     - **Company Website URL** (Đường dẫn website)
     - **Scoring Criteria** (Tiêu chí đánh giá, ví dụ: "Sử dụng công nghệ AI", "Độ lớn công ty", "Ngành nghề phù hợp")
     - **Additional Notes** (Ghi chú thêm, nếu có).
   - **API Key Tally**: Tạo tại [Tally Developer Portal](https://tally.so/developer) và lưu vào n8n dưới **Credentials > tallyApi**.

2. **OpenAI API Key**:
   - Tạo tại [OpenAI Platform](https://platform.openai.com/) và lưu vào n8n dưới **Credentials > openAiApi**.

3. **Google Sheets**:
   - Tạo một bảng mới với tab tên **exactly "leads"** (không dấu, không khoảng trắng).
   - Cột đầu tiên là **timestamp** (thời gian), sau đó là các cột sau (đảm bảo tên cột **không dấu**, **lowercase**):
     ```
     timestamp | company | website_url | linkedin_url | criteria | company_summary | tech_stack | score | grade | reasoning | recommended_action
     ```
   - **Share Google Sheet** với n8n bằng cách cấp quyền **Editor** cho email liên kết với tài khoản OAuth2 của n8n.

4. **n8n Self-hosted**:
   - Cài đặt n8n trên VPS (khuyến nghị sử dụng [TinoHost](https://tino.vn/vps-n8n?affid=388) hoặc [BNIX](https://my.bnix.one/aff.php?aff=172)) để workflow chạy liên tục.
   - Cài đặt **n8n-nodes-tallyforms** và **@n8n/n8n-nodes-langchain** (để sử dụng AI GPT-5.4).
     ```bash
     n8n install @n8n/nodes-tallyforms
     n8n install @n8n/nodes-langchain
     ```

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể tải workflow từ [n8n.io/workflows/15059](https://n8n.io/workflows/15059) và import vào n8n Editor theo cách sau:
- **Tải file JSON**: Nhấn **Export** trên trang workflow, tải xuống file `.json`.
- **Import vào n8n**:
  1. Mở **n8n Editor** (http://localhost:5678).
  2. Nhấn **Import** ở góc trên bên phải.
  3. Chọn file JSON vừa tải và nhấn **Import**.

**Hoặc copy/paste JSON**:
1. Mở **n8n Editor**.
2. Nhấn **Create Workflow** > **Import Workflow**.
3. Chọn **Paste JSON** và dán toàn bộ mã JSON từ [trang workflow](https://n8n.io/workflows/15059) vào ô **JSON**.

---

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Sau khi import, các sếp cần cấu hình các node quan trọng như sau:

##### **A. Tally Trigger**
- **Node**: `Tally Trigger`
- **Cấu hình**:
  - Chọn **Credentials**: `tallyApi` (đã lưu trước đó).
  - Chọn **Form ID**: Lấy từ URL của form Tally (ví dụ: `https://tally.so/r/abc123` → `abc123`).
  - **Webhook URL**: Để mặc định (n8n sẽ tự động tạo).

##### **B. OpenAI GPT-5.4 (3 node)**
- **Node**: `GPT-5.4 Model`, `GPT-5.4 Model 2`, `GPT-5.4 Model 3`
- **Cấu hình chung**:
  - **Credentials**: `openAiApi` (API Key đã lưu).
  - **Model**: Đảm bảo chọn `gpt-5.4` (hoặc `gpt-4` nếu không có).
  - **Prompt**: Các node này sử dụng **Agent** để tự động xây dựng prompt, **không cần chỉnh sửa** (nếu muốn tối ưu, các sếp có thể chỉnh sửa trong node `Set` trước khi gửi vào AI).

##### **C. Google Sheets**
- **Node**: `Append Lead to Sheet`
- **Cấu hình**:
  - **Credentials**: Chọn **Google Sheets OAuth2** (đã cấu hình trước).
  - **Spreadsheet ID**: Lấy từ URL của Google Sheet (ví dụ: `https://docs.google.com/spreadsheets/d/abc123/edit` → `abc123`).
  - **Sheet Name**: Đảm bảo là **`leads`** (không dấu, không khoảng trắng).
  - **Operation**: Để mặc định là `append` (thêm dữ liệu vào cuối bảng).

##### **D. Các node `Set` (Map Lead Fields, Map Website Analysis, Build Sheet Row)**
- **Node**: `Map Lead Fields`, `Map Website Analysis`, `Build Sheet Row`
- **Cấu hình**:
  - Các node này **không cần chỉnh sửa** nếu các sếp đã tạo form Tally và Google Sheet theo yêu cầu.
  - Nếu muốn thay đổi cột trong Google Sheet, các sếp cần chỉnh sửa **key** trong node `Build Sheet Row` để phù hợp với tên cột mới.

##### **E. Fetch Company Homepage & Strip HTML**
- **Node**: `Fetch Company Homepage` (HTTP Request) và `Strip HTML to Plain Text` (Code)
- **Cấu hình**:
  - **HTTP Request**:
    - **Method**: `GET`.
    - **URL**: `{{$json["website_url"]}}` (đường dẫn website từ form Tally).
    - **Headers**: Thêm `User-Agent: Mozilla/5.0` để tránh bị chặn.
  - **Code Node**:
    - Mã JavaScript mặc định sẽ **xóa tất cả HTML** và giữ lại văn bản thuần túy. **Không cần chỉnh sửa** nếu không muốn thay đổi logic.

---

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Nhấn **Run Workflow** và chọn **Test Execution**.
   - Điền dữ liệu mẫu vào form Tally (ví dụ: tên công ty "TechCorp", website `https://techcorp.com`, LinkedIn `https://linkedin.com/company/techcorp`).
   - Kiểm tra kết quả trong Google Sheet sau khi workflow hoàn tất.

2. **Bật Active**:
   - Sau khi test thành công, chuyển trạng thái workflow từ **Draft** sang **Active**.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tích hợp Slack/Telegram để báo cáo kết quả**:
   - Thêm node **Slack** hoặc **Telegram Bot** sau node `Append Lead to Sheet` để thông báo khi lead mới được đánh giá.
   - Ví dụ:
     ```json
     {
       "nodeType": "n8n-nodes-base.slack",
       "name": "Notify Slack",
       "credentials": {
         "slackApi": "slack-api-key"
       },
       "options": {
         "channel": "#leads",
         "message": "🚀 Lead mới được đánh giá: {{ $json["company"] }} (Điểm: {{ $json["score"] }}, Nhận xét: {{ $json["reasoning"] }})"
       }
     }
     ```

2. **Lưu log vào Google Drive**:
   - Thêm node **Google Drive** để lưu file log của workflow (ví dụ: file CSV hoặc JSON) cho việc theo dõi lâu dài.

3. **Tự động gửi báo cáo hàng tuần**:
   - Sử dụng **n8n Scheduler** để chạy workflow định kỳ (ví dụ: mỗi thứ 7) và gửi báo cáo tổng hợp qua email hoặc Slack.

4. **Cập nhật tiêu chí đánh giá động**:
   - Nếu tiêu chí đánh giá thay đổi, các sếp có thể chỉnh sửa form Tally và **không cần chỉnh sửa workflow** (do AI tự động lấy dữ liệu từ form).

5. **Optimize AI Prompt**:
   - Nếu muốn AI trả về kết quả chi tiết hơn, các sếp có thể chỉnh sửa **prompt** trong node `Set` trước khi gửi vào AI. Ví dụ:
     ```json
     {
       "json": {
         "prompt": "Tôi là một chuyên gia đánh giá lead B2B. Hãy phân tích chi tiết về công ty {{ $json["company"] }} dựa trên nội dung trang chủ: {{ $json["website_content"] }}. Đánh giá theo tiêu chí sau: {{ $json["criteria"] }}. Cung cấp điểm từ 1-10, nhãn A-D, lý do và hành động khuyến nghị."
       }
     }
     ```

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa quá trình đánh giá lead B2B mà không cần viết code. Bằng cách tích hợp **Tally Forms, AI GPT-5.4 và Google Sheets**, nó giúp:
✔ **Tiết kiệm thời gian** lên đến 80% trong việc phân tích lead.
✔ **Đảm bảo chính xác** với phân tích AI từ website và LinkedIn.
✔ **Cập nhật tự động** dữ liệu vào bảng tính để theo dõi dễ dàng.

**Hành động ngay hôm nay!**
1. Chuẩn bị tài khoản và credentials theo hướng dẫn.
2. Import workflow và cấu hình các node.
3. Test và bật workflow để tự động hóa quá trình đánh giá lead của doanh nghiệp.

**Nếu có vấn đề, các sếp có thể liên hệ với tác giả Yaron Been qua [LinkedIn](https://www.linkedin.com/in/yaronbeen/) hoặc [YouTube](https://www.youtube.com/@YaronBeen/videos) để hỗ trợ thêm!**

---
**Chúc các sếp thành công với việc tự động hóa lead B2B!** 🚀