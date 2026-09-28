---
title: "🔍 Tự Động Tìm Kiếm Người Dùng LinkedIn Siêu Nhanh Với TexAU API (N8n)"
description: "Workflow tự động hóa tìm kiếm người dùng LinkedIn từ đầu đến cuối bằng TexAU API, giúp các sếp tiết kiệm thời gian trong tuyển dụng, lead generation và prospecting. Kết quả là danh sách người dùng được cấu trúc với thông tin chi tiết như tên, vị trí, liên kết profile và độ phù hợp."
slug: "tieu-dong-tim-kiem-nguoi-dung-linkedin-texau-api"
tags: [n8n, automation, lead-generation, recruitment, texau-api]
keywords: [tìm kiếm linkedin tự động, lead generation n8n, tuyển dụng tự động hóa, texau api, tự động hóa prospecting]
---

# 🚀 Tự Động Tìm Kiếm Người Dùng LinkedIn Siêu Nhanh Với TexAU API

### 💡 Giải quyết vấn đề gì?
Các sếp đang mất nhiều thời gian quét thủ công LinkedIn để tìm kiếm **nhân sự tiềm năng**, **khách hàng mục tiêu** hoặc **các nhà tuyển dụng phù hợp**? Hay đang phải **lặp đi lặp lại** các từ khóa tìm kiếm mà kết quả không chính xác? **Workflow này sẽ tự động hóa toàn bộ quá trình** bằng TexAU API, giúp bạn nhận được danh sách người dùng được **lọc sàng, cấu trúc và cập nhật liên tục** chỉ với một cú nhấp chuột!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động 24/7 mà không bị gián đoạn, các sếp nên **self-host n8n** trên VPS chuyên dụng:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần quét thủ công LinkedIn, tự động hóa từ tìm kiếm đến xuất kết quả.
- **Dữ liệu chính xác**: Nhận danh sách người dùng được **lọc theo tiêu chí cụ thể** (tên, vị trí, từ khóa, địa điểm).
- **Cấu trúc dữ liệu**: Kết quả bao gồm **tên, tiêu đề, vị trí công việc, liên kết profile LinkedIn** và chỉ số độ phù hợp.
- **Hoạt động liên tục**: Chạy 24/7 trên VPS, không phụ thuộc vào thời gian làm việc của bạn.
- **Dễ dàng tích hợp**: Kết quả có thể **được gửi trực tiếp vào CRM, Slack, hoặc AI agent** để xử lý tiếp.
:::

---

### 🔧 Yêu cầu cần thiết
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **API Key của TexAU**:
   - Đăng ký tài khoản tại [TexAU](https://texau.com/) và lấy **API Key** từ dashboard.
   - Nếu chưa có, liên hệ [hỗ trợ TexAU](https://texau.com/contact) để kích hoạt.
2. **Tham số tìm kiếm**:
   - **Tên người dùng** (ví dụ: "Nguyễn Văn A").
   - **Vị trí công việc** (ví dụ: "Chief Technology Officer").
   - **Từ khóa** (ví dụ: "AI", "Blockchain").
   - **Địa điểm** (ví dụ: "Hà Nội", "Việt Nam").
3. **Tài khoản n8n**:
   - Nếu chưa có, tạo tài khoản miễn phí tại [n8n.io](https://n8n.io/) hoặc tự host trên VPS.

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có **2 cách** để import workflow này:
- **Tải file JSON**:
  1. Tải workflow từ [n8n.io/workflows/13670](https://n8n.io/workflows/13670) (ấn nút **Download**).
  2. Trên **n8n Editor**, nhấn **Import** → Chọn file JSON vừa tải.
- **Copy/Paste JSON**:
  1. Trên trang workflow gốc, nhấn **Export** → Copy toàn bộ mã JSON.
  2. Trên n8n Editor, nhấn **Import** → Chọn **Paste JSON** và dán mã.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm **5 node chính**, các sếp cần **cấu hình kỹ lưỡng** như sau:

##### **Node 1: "When Executed by Another Workflow" (executeWorkflowTrigger)**
- **Chức năng**: Khởi động workflow khi được gọi từ bên ngoài (hoặc **manual trigger**).
- **Cấu hình**:
  - Để mặc định (không cần thay đổi gì).

##### **Node 2: "Wait" (wait)**
- **Chức năng**: Đợi TexAU xử lý yêu cầu tìm kiếm (tránh overloading API).
- **Cấu hình**:
  - Thời gian chờ mặc định là **5 giây** (có thể điều chỉnh từ **1-10 giây** tùy vào tải API).
  - **Lưu ý**: Nếu TexAU quá tải, tăng thời gian chờ lên **15-30 giây**.

##### **Node 3: "LinkedIn_People_Search" (httpRequest)**
- **Chức năng**: Gửi yêu cầu tìm kiếm đến TexAU API.
- **Cấu hình BẮT BUỘC**:
  - **Method**: `POST`
  - **URL**: `https://api.texau.com/v1/search/people`
  - **Headers**:
    ```
    Content-Type: application/json
    Authorization: Bearer [API_KEY_CỦA_BẠN]
    ```
  - **Body (JSON)**:
    ```json
    {
      "query": "Nguyễn Văn A",
      "filters": {
        "job_title": "Chief Technology Officer",
        "location": "Hà Nội",
        "keywords": ["AI", "Blockchain"]
      }
    }
    ```
    - **Thay đổi**:
      - `query`: Tên người dùng hoặc từ khóa tìm kiếm.
      - `filters`: Thêm/bỏ các tiêu chí lọc (ví dụ: `location`, `keywords`).

##### **Node 4: "Get Results" (httpRequest)**
- **Chức năng**: Lấy kết quả từ TexAU sau khi xử lý xong.
- **Cấu hình BẮT BUỘC**:
  - **Method**: `GET`
  - **URL**: `https://api.texau.com/v1/search/people/{JOB_ID}`
    - `{JOB_ID}` là **ID của yêu cầu tìm kiếm** (được trả về từ Node 3).
    - **Lưu ý**: Các sếp cần **lấy `JOB_ID` từ response của Node 3** và động điền vào URL này.
  - **Headers**:
    ```
    Authorization: Bearer [API_KEY_CỦA_BẠN]
    ```

##### **Node 5: "People_Search_Results" (httpRequest)**
- **Chức năng**: Hiển thị kết quả cuối cùng (không cần cấu hình thêm, chỉ dùng để **log hoặc xuất dữ liệu**).
- **Cấu hình**:
  - **Method**: `GET` (mặc định).
  - **URL**: Không cần thay đổi (n8n tự động lấy từ Node 4).

#### 3. Kích hoạt ⚡️
1. **Test Run**:
   - Nhấn **Run Workflow** và nhập **tham số tìm kiếm** vào Node 3.
   - Kiểm tra kết quả ở Node 5 (nếu có lỗi, check **API Key** và **URL**).
2. **Bật Active**:
   - Sau khi test thành công, chuyển **Workflow Status** sang **Active**.

---

### ✍️ Mẹo & gợi ý nâng cao
1. **Tích hợp với CRM/Slack**:
   - Sau khi nhận kết quả, các sếp có thể **gửi danh sách người dùng** vào **Slack** (node `slack`) hoặc **CRM** (node `hubspot`, `zapier`).
   - **Ví dụ**: Gửi kết quả vào Slack với format:
     ```json
     {
       "text": "🔍 Kết quả tìm kiếm LinkedIn: {{$node["People_Search_Results"].jsonpath("$.results[0].name")}}",
       "blocks": [
         {
           "type": "section",
           "text": {
             "type": "mrkdwn",
             "text": "*Tên:* {{$node["People_Search_Results"].jsonpath("$.results[0].name")}} \n*Vị trí:* {{$node["People_Search_Results"].jsonpath("$.results[0].job_title")}} \n*Profile:* <{{$node["People_Search_Results"].jsonpath("$.results[0].profile_url")}}|LinkedIn>"
           }
         }
       ]
     }
     ```

2. **Lưu log vào Google Sheets/Notion**:
   - Sử dụng node `googleSheets` hoặc `notion` để **lưu lịch sử tìm kiếm** và **theo dõi lead**.
   - **Ví dụ**:
     ```json
     {
       "sheetName": "LinkedIn Leads",
       "range": "A1",
       "values": [
         [
           "{{$node["People_Search_Results"].jsonpath("$.results[0].name")}}",
           "{{$node["People_Search_Results"].jsonpath("$.results[0].job_title")}}",
           "{{$node["People_Search_Results"].jsonpath("$.results[0].profile_url")}}",
           "{{$node["People_Search_Results"].jsonpath("$.results[0].relevance_score")}}"
         ]
       ]
     }
     ```

3. **Tự động hóa tìm kiếm định kỳ**:
   - Sử dụng **n8n Cron Trigger** để chạy workflow **hàng ngày/tuần** (ví dụ: tìm kiếm các nhà tuyển dụng mới ở Việt Nam).
   - **Cấu hình**:
     - Node **Cron Trigger** (n8n-nodes-base.cron) với biểu thức:
       ```
       0 9 * * *  # Chạy lúc 9h sáng hàng ngày
       ```

4. **Kết hợp với AI (LLM) để phân tích**:
   - Sau khi lấy danh sách, các sếp có thể **gửi dữ liệu vào node LLM** (ví dụ: `openai`, `mistral`) để **tóm tắt thông tin** hoặc **đánh giá độ phù hợp**.
   - **Ví dụ**:
     ```json
     {
       "model": "gpt-3.5-turbo",
       "prompt": "Analyze the following LinkedIn profile: {{$node["People_Search_Results"].jsonpath("$.results[0]")}}. Summarize their skills, experience, and suitability for a CTO role in Vietnam.",
       "temperature": 0.7
     }
     ```

---

### 📌 Kết luận
Workflow này là **giải pháp hoàn hảo** cho các sếp đang cần **tìm kiếm người dùng LinkedIn một cách tự động, chính xác và hiệu quả**. Bằng cách **tích hợp TexAU API với n8n**, bạn không chỉ tiết kiệm **thời gian quét thủ công** mà còn nhận được **dữ liệu được cấu trúc sẵn** để sử dụng trong **tuyển dụng, lead generation hoặc prospecting**.

🚀 **Hành động ngay**:
1. **Tải workflow** và import vào n8n.
2. **Cấu hình API Key** và tham số tìm kiếm.
3. **Bật Active** và bắt đầu tự động hóa!

**Nếu có vấn đề**, các sếp có thể:
- **Trả lời câu hỏi** trong [community n8n](https://community.n8n.io/).
- **Liên hệ TexAU** để hỗ trợ API.

**Chúc các sếp thành công với chiến dịch tìm kiếm mới!** 💼🔍