---
title: "🚀 Tự Động Hóa Viết Lại Nội Dung Web Với Số Ký Tự Chính Xác Bằng GPT-4.1 + Google Sheets (SEO & AI)"
description: "Workflow này tự động viết lại nội dung web với số ký tự chính xác từng dòng, bảo toàn bố cục trang web và tối ưu SEO. Sử dụng GPT-4.1 để so sánh và ghi log thay đổi vào Google Sheets, giúp các sếp tiết kiệm thời gian và đảm bảo chất lượng nội dung."
slug: "tieu-dong-hoa-viet-lai-noi-dung-web-seo-ai"
tags: [n8n, automation, no-code, ai-content-rewriting, google-sheets, openai-gpt-4]
keywords: [n8n workflow tự động hóa, viết lại nội dung web, GPT-4.1, SEO content, tự động hóa nội dung AI, Google Sheets logging]
---

# 🚀 **Tự Động Hóa Viết Lại Nội Dung Web Với Số Ký Tự Chính Xác (SEO & AI)**

Bạn có bao giờ phải viết lại nội dung web để tối ưu SEO nhưng lại lo lắng về bố cục trang bị phá vỡ? Hay phải kiểm tra từng dòng để đảm bảo số ký tự không thay đổi, gây mất thời gian và công sức? **Workflow này giải quyết tất cả những vấn đề đó!**

Với **n8n + GPT-4.1**, bạn có thể tự động:
✅ **Viết lại nội dung web** một cách chính xác từng ký tự, **bảo toàn bố cục trang** (không thay đổi số ký tự của từng dòng).
✅ **Tối ưu SEO** mà không lo mất tính thẩm mỹ của trang web.
✅ **So sánh và ghi log thay đổi** vào Google Sheets để theo dõi chất lượng và hiệu suất.
✅ **Tiết kiệm thời gian** lên đến **90%** so với cách làm thủ công.

---
### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Bảo toàn bố cục trang web**: Không thay đổi số ký tự của từng dòng, giữ nguyên thiết kế và trải nghiệm người dùng.
- **Tối ưu SEO hiệu quả**: Nội dung được viết lại một cách tự nhiên nhưng vẫn đáp ứng yêu cầu từ khóa và độ dài ký tự.
- **So sánh và kiểm soát chất lượng**: Ghi log tất cả thay đổi vào Google Sheets với chi tiết so sánh ký tự, giúp dễ dàng theo dõi và điều chỉnh.
- **Hoạt động 24/7**: Không cần can thiệp thủ công, workflow chạy tự động sau khi cấu hình xong.
- **Tiết kiệm chi phí**: Giảm thiểu chi phí thuê người viết lại nội dung hoặc sử dụng công cụ AI khác.
:::

---
### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets** (để lưu log so sánh nội dung).
2. **API Key OpenAI** (để sử dụng GPT-4.1 và GPT-4o-mini).
3. **Google Sheets OAuth 2.0 Credentials** (để n8n có quyền ghi dữ liệu vào bảng tính).
4. **URL của Google Sheet** (bảng cần ghi log kết quả).
5. **Mô hình AI đã cấu hình sẵn** (n8n sẽ tự động sử dụng GPT-4.1 và GPT-4o-mini).
:::

---
### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### 1. **Import Workflow 📥**
- **Bước 1**: Tải workflow từ [n8n.io/workflows/13268](https://n8n.io/workflows/13268) (chọn **Export as JSON**).
- **Bước 2**: Mở **n8n Editor** và nhấn **Import** → Dán JSON vào hoặc tải file JSON đã tải xuống.
- **Bước 3**: Chọn **Create Workflow** để lưu vào dự án của bạn.

#### 2. **Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **11 node** quan trọng, các sếp cần chú ý cấu hình như sau:

##### **A. Cấu hình Google Sheets**
- **Node**: *Log Comparison to Google Sheets*
  - **Tham số cần điền**:
    - **Google Sheets URL**: Điền vào trường `sheetUrl` (ví dụ: `https://docs.google.com/spreadsheets/d/EXAMPLE_SHEET_ID/edit`).
    - **Sheet Name**: Tên của bảng tính trong Google Sheets (ví dụ: `Comparison_Log`).
    - **Range**: Điền `A1` (n8n sẽ tự động append dữ liệu từ dòng này).
  - **Credentials**: Chọn `googleSheetsOAuth2Api` (đã cấu hình trước khi import).

##### **B. Cấu hình OpenAI API**
- **Node**: *OpenAI GPT-4.1 Rewriting Model* và *OpenAI GPT-4.1 Comparison Model*
  - **Tham số cần điền**:
    - **Model**: Đã mặc định là `gpt-4.1` (không cần thay đổi).
    - **Credentials**: Chọn `openAiApi` (đã cấu hình trước khi import).
  - **Lưu ý**:
    - Đảm bảo **API Key OpenAI** đã được thêm vào **Credentials** của n8n (nếu chưa, thêm tại **Settings → Credentials → Add Credential → OpenAI API**).

##### **C. Cấu hình Form Trigger**
- **Node**: *Submit Content Rewriting Request*
  - **Tham số cần điền**:
    - **Form Fields**: Thêm các trường như:
      - `url` (để người dùng nhập URL cần viết lại).
      - `characterCount` (nếu cần chỉ định số ký tự cụ thể).
    - **Credentials**: Không cần (sử dụng mặc định).

##### **D. Cấu hình Agent & Output Parser**
- **Node**: *Rewrite Content with Exact Character Count* và *Compare Original vs Rewritten Content*
  - **Tham số mặc định**: Đã cấu hình sẵn, **không cần thay đổi** trừ khi cần tùy chỉnh logic AI.
  - **Lưu ý**:
    - Agent sẽ tự động xử lý yêu cầu viết lại nội dung với số ký tự chính xác.
    - Parser sẽ chuyển đổi kết quả so sánh thành định dạng JSON.

##### **E. Cấu hình SplitOut & Logging**
- **Node**: *Split Comparison into Individual Rows* và *Log Comparison to Google Sheets*
  - **Tham số mặc định**: Đã cấu hình sẵn, **chỉ cần đảm bảo Google Sheets URL và Sheet Name đúng**.
  - **Lưu ý**:
    - N8n sẽ tự động chia kết quả so sánh thành các dòng riêng biệt và ghi vào Google Sheets.

---
#### 3. **Kích hoạt ⚡️**
- **Bước 1**: Nhấn **Test Run** với một URL mẫu (ví dụ: `https://example.com`).
- **Bước 2**: Kiểm tra kết quả trong **Google Sheets** để đảm bảo dữ liệu ghi đúng.
- **Bước 3**: Nếu test thành công, nhấn **Active** để workflow chạy tự động khi có yêu cầu.

---
### ✍️ **Mẹo & gợi ý nâng cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Gửi thông báo Slack/Telegram khi hoàn thành**:
   - Thêm **node Slack/Telegram Webhook** sau node *Log Comparison to Google Sheets* để thông báo kết quả.
   - **Cách làm**:
     - Tạo một **webhook** từ Slack/Telegram.
     - Thêm node **HTTP Request** với payload:
       ```json
       {
         "text": "✅ Content rewritten successfully! Check Google Sheets for details."
       }
       ```
     - Gửi payload đến URL webhook của Slack/Telegram.

2. **Lưu log vào cơ sở dữ liệu (Database)**:
   - Thay thế node *googleSheets* bằng **node MySQL/PostgreSQL** để lưu kết quả vào cơ sở dữ liệu.
   - **Cách làm**:
     - Cài đặt **n8n-node-db** (nếu chưa có).
     - Thêm node **MySQL/PostgreSQL** và cấu hình kết nối.

3. **Tự động viết lại nội dung định kỳ**:
   - Sử dụng **node Schedule** để chạy workflow hàng tuần/tháng.
   - **Cách làm**:
     - Thêm node **Schedule** trước node *Submit Content Rewriting Request*.
     - Chọn thời gian chạy (ví dụ: **0 0 * * 0** để chạy hàng tuần).

4. **Tùy chỉnh mô hình AI**:
   - Nếu muốn thay đổi mô hình từ GPT-4.1 sang GPT-4o, chỉnh sửa trong node *lmChatOpenAi*:
     ```json
     "model": {
       "__rl": true,
       "mode": "list",
       "value": "gpt-4o",
       "cachedResultName": "gpt-4o"
     }
     ```
     - **Lưu ý**: Đảm bảo mô hình mới có trong danh sách hỗ trợ của OpenAI.

5. **Xây dựng dashboard theo dõi**:
   - Sử dụng **Google Data Studio** hoặc **Power BI** để tạo dashboard từ dữ liệu trong Google Sheets.
   - **Cách làm**:
     - Kết nối Google Sheets với Data Studio.
     - Tạo biểu đồ theo dõi số lượng nội dung được viết lại, thời gian xử lý, và tỷ lệ thay đổi ký tự.
:::

---
### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp cần tự động hóa việc viết lại nội dung web **với số ký tự chính xác**, tối ưu SEO mà không mất thời gian kiểm tra thủ công. **Bằng cách sử dụng n8n + GPT-4.1 + Google Sheets**, bạn không chỉ tiết kiệm thời gian mà còn **đảm bảo chất lượng và nhất quán** cho tất cả nội dung trên trang web.

👉 **Hãy thử ngay và tự động hóa quy trình viết lại nội dung của mình!**
👉 **Nếu cần hỗ trợ**, để lại comment hoặc liên hệ với cộng đồng n8n tại [n8n.io/community](https://n8n.io/community).

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::