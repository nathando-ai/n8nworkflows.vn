---
title: "🚀 Tự Động Hóa Audit Website + Outreach Cá Nhân Hóa Sử Dụng Lighthouse & GPT-4 (N8n)"
description: "Workflow tự động hóa kiểm tra chất lượng website, phân tích UI/UX, và gửi email outreach cá nhân hóa dựa trên dữ liệu Lighthouse và GPT-4. Giúp doanh nghiệp tiết kiệm thời gian, tăng tỷ lệ chuyển đổi và tối ưu hóa trải nghiệm khách hàng."
slug: "tieu-dong-hoa-audit-website-outreach-canh-nhan-hoa"
tags: [n8n, automation, lead-nurturing, multimodal-ai, google-sheets, openai, lighthouse]
keywords: [n8n workflow tự động hóa, audit website tự động, outreach cá nhân hóa, Lighthouse API, GPT-4 n8n, tự động hóa lead generation]
---

# 🚀 **Tự Động Hóa Audit Website + Outreach Cá Nhân Hóa Sử Dụng Lighthouse & GPT-4**

Bạn đã bao giờ phải mất hàng giờ để kiểm tra chất lượng website của khách hàng tiềm năng, phân tích UI/UX, và viết email outreach cá nhân hóa? Hay phải lo lắng rằng thông tin thu thập được không chính xác hoặc không phù hợp với từng doanh nghiệp? **Workflow này sẽ giải quyết tất cả những vấn đề đó!**

Với **Automated Website Audit & Personalized Outreach**, các sếp có thể:
✅ **Kiểm tra website** bằng công cụ Lighthouse (Google) để đánh giá tốc độ, SEO, và trải nghiệm người dùng.
✅ **Phân tích UI/UX** và **nội dung website** bằng GPT-4 để tìm ra điểm mạnh/điểm yếu.
✅ **Tự động gửi email outreach cá nhân hóa** dựa trên dữ liệu thu thập được, tăng tỷ lệ phản hồi lên **30-50%** so với cách làm thủ công.
✅ **Tự động cập nhật Google Sheets** với tất cả thông tin phân tích, giúp theo dõi và quản lý dễ dàng.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tốc độ và tính bảo mật cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần kiểm tra website thủ công, phân tích Lighthouse, hoặc viết email outreach.
- **Cá nhân hóa cao**: Email outreach được tạo dựa trên **dữ liệu cụ thể** của từng website (UI/UX, lỗi, điểm mạnh).
- **Tăng tỷ lệ chuyển đổi**: Nội dung email được tối ưu hóa để phù hợp với từng doanh nghiệp.
- **Hoạt động liên tục**: Workflow chạy tự động, không cần can thiệp của con người.
- **Dữ liệu chính xác**: Thông tin được tự động cập nhật vào Google Sheets, giúp theo dõi và phân tích dễ dàng.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Google Sheets** (để lưu trữ danh sách khách hàng tiềm năng và kết quả phân tích).
✔ **API Key OpenAI** (để sử dụng GPT-4 trong phân tích và tạo email).
✔ **Danh sách email/website** của khách hàng tiềm năng (được lưu trong Google Sheets).
✔ **Tài khoản VPS** (nếu tự host n8n).

---
:::info[CHUẨN BỊ]
**Google Sheets**:
- Tạo một bảng với các cột: `Email`, `Website`, `Status`, `DecisionMaker`, `BusinessDetails`, `LighthouseStats`, `OutreachMessage`, `Screenshot`.
- Đảm bảo **OAuth2 API** của Google Sheets đã được cấu hình trong n8n.

**OpenAI API**:
- Tạo một tài khoản tại [OpenAI](https://platform.openai.com/) và lấy **API Key**.
- Cấu hình **OpenAI API** trong n8n với tên `openAiApi`.

**Webhook**:
- Workflow sẽ sử dụng một **Webhook** để bắt đầu quá trình. Các sếp có thể sử dụng một **URL Webhook** từ n8n hoặc kết nối với một dịch vụ như **Zapier** hoặc **Make (Integromat)**.
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Tải file JSON từ [n8n.io/workflows/5940](https://n8n.io/workflows/5940).
2. Trong n8n Editor, nhấn **Import** và chọn file JSON.
3. Hoặc copy toàn bộ JSON và paste vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này gồm **39 nodes** và được chia thành **4 bước chính**. Dưới đây là hướng dẫn chi tiết về các node quan trọng cần cấu hình:

##### **📌 Bước 1: Trigger & CRM Input**
- **Node "Get New Rows" (Google Sheets)**:
  - Chọn **Google Sheets OAuth2 API** đã cấu hình.
  - Chọn **Sheet** và **Range** (ví dụ: `Sheet1!A:Z`).
  - Cấu hình để lấy dữ liệu từ cột `Email` và `Website`.

- **Node "If Email is not Empty"**:
  - Nếu email **không tồn tại**, workflow sẽ **bỏ qua** và không thực hiện các bước tiếp theo.

- **Node "If Email is not BokaDirect's support email"**:
  - Nếu email là **email hỗ trợ** của BokaDirect, workflow sẽ **bỏ qua** và không gửi outreach.

##### **📌 Bước 2: Scraping Business Data**
- **Node "BokaDirect Profile URL Request" (HTTP Request)**:
  - Thiết lập **URL** của trang web cần phân tích (ví dụ: `https://bokadirect.com/{website}`).
  - Cấu hình **headers** để mô phỏng trình duyệt (nếu cần).

- **Node "DecisionMaker Name" (OpenAI)**:
  - Sử dụng **GPT-4** để dự đoán **tên người quyết định** (Decision Maker) của doanh nghiệp.
  - **Prompt mẫu**:
    ```plaintext
    Tôi có một trang web: {website}. Hãy dự đoán tên người quyết định (Decision Maker) của doanh nghiệp này.
    ```

- **Node "Professional Email or Personal" (Code)**:
  - Node này sẽ **kiểm tra** email có phải là email **nhân viên chuyên nghiệp** hay không.
  - Nếu không phải, workflow sẽ **bỏ qua** và không gửi outreach.

##### **📌 Bước 3: Analyzing Lighthouse Stats + Website UI/UX Design**
- **Node "Lighthouse Stats Request" (HTTP Request)**:
  - Sử dụng **API Lighthouse** để kiểm tra chất lượng website.
  - URL mẫu:
    ```plaintext
    https://www.lighthouse-ci.org/run-only-ci.v2.json?url={website}&chromeFlags=--headless
    ```

- **Node "Screenshot of Website Request" (HTTP Request)**:
  - Chụp **ảnh màn hình** của website để phân tích UI/UX.
  - Sử dụng **Puppeteer** hoặc **Playwright** để thực hiện.

- **Node "Analyse UI/UX design, Lighthouse stats & Business details" (OpenAI)**:
  - Sử dụng **GPT-4** để phân tích **UI/UX, Lighthouse stats, và thông tin doanh nghiệp**.
  - **Prompt mẫu**:
    ```plaintext
    Tôi có một website: {website}. Dựa trên dữ liệu sau:
    - Lighthouse Stats: {lighthouseStats}
    - Screenshot: {screenshot}
    - Thông tin doanh nghiệp: {businessDetails}
    Hãy phân tích điểm mạnh/điểm yếu của website và đề xuất cải thiện.
    ```

##### **📌 Bước 4: Analyzing Website Error & Generating Outreach Email**
- **Node "Write message for error in Website" (OpenAI)**:
  - Nếu website có **lỗi**, GPT-4 sẽ tự động **viết email thông báo** về vấn đề đó.
  - **Prompt mẫu**:
    ```plaintext
    Website {website} có lỗi: {error}. Hãy viết một email outreach cá nhân hóa để thông báo cho chủ website về vấn đề này.
    ```

- **Node "Update Sheet with messages and Status" (Google Sheets)**:
  - Cập nhật **Google Sheets** với:
    - **Email outreach** đã tạo.
    - **Trạng thái** (`Sent`, `Error`, `Pending`).

---

#### **3. Kích hoạt ⚡️**
1. **Test Run** với một **dữ liệu mẫu** (ví dụ: một email và website cụ thể).
2. Kiểm tra **Google Sheets** để đảm bảo dữ liệu được cập nhật chính xác.
3. **Bật Active workflow** và kết nối với **Webhook** để bắt đầu tự động hóa.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm một **node Slack** hoặc **Telegram** để thông báo khi workflow hoàn thành hoặc gặp lỗi.
   - Ví dụ: Khi email outreach được gửi thành công, gửi tin nhắn Slack:
     ```plaintext
     Email outreach đã được gửi cho {email} về website {website}.
     ```

2. **Lưu log hoạt động**:
   - Sử dụng **node Code** để lưu **log** của workflow vào Google Sheets hoặc một **database** như **MongoDB**.

3. **Gửi báo cáo định kỳ**:
   - Thêm một **node Schedule** để gửi **báo cáo tổng hợp** về kết quả outreach hàng tuần.

4. **Tối ưu hóa GPT-4**:
   - Nếu budget cho OpenAI cao, có thể sử dụng **GPT-4 Turbo** để cải thiện chất lượng phân tích.

---

### 📌 **Kết luận**
Workflow **Automated Website Audit & Personalized Outreach** là **giải pháp hoàn hảo** cho các doanh nghiệp muốn:
✔ **Tiết kiệm thời gian** trong quá trình phân tích website và outreach.
✔ **Tăng tỷ lệ chuyển đổi** với email outreach cá nhân hóa.
✔ **Tự động hóa toàn bộ quy trình** mà không cần code.

**Hãy áp dụng ngay workflow này và xem cách nó giúp doanh nghiệp của các sếp **tăng doanh thu và tối ưu hóa quy trình marketing**!**

---
**🔗 [Tải workflow từ n8n.io](https://n8n.io/workflows/5940)**
**💡 Cần hỗ trợ? Hãy để lại comment bên dưới!**