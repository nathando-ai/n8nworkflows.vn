---
title: "🛡️ Tự Động Quét URL Tìm Threat An Toàn Với urlscan.io + GPT-4o mini (Không Cần Code)"
description: "Workflow tự động quét URL để phát hiện nguy cơ an ninh mạng, phân tích kết quả bằng AI và gửi báo cáo email chi tiết chỉ trong 30 giây. Giúp các sếp bảo mật, DevOps và team IT nhanh chóng phát hiện lỗ hổng trước khi xảy ra."
slug: "tu-dong-quet-url-tim-threat-an-toan-voi-urlscan-io-gpt-4o-mini"
tags: [n8n, automation, security, ai, urlscan, gmail, no-code]
keywords: [n8n workflow an ninh mạng, tự động hóa quét URL, urlscan.io với n8n, phân tích AI threat, báo cáo email an toàn web]
---

# 🚀 **Tự Động Quét URL Tìm Threat An Toàn Với urlscan.io + GPT-4o mini**

### **Giải pháp cho các sếp:**
Hãy tưởng tượng một tình huống: Một link nghi ngờ được chia sẻ trong nhóm, hoặc một trang web mới được thêm vào danh sách cho phép truy cập. Bạn có thể **tự động quét URL** để phát hiện nguy cơ an ninh mạng như malware, phishing, hoặc nội dung độc hại **trong vòng 30 giây** mà không cần can thiệp thủ công? Với workflow này, **AI và tự động hóa** sẽ làm tất cả cho bạn:
- Quét URL trên **urlscan.io** (dịch vụ quét URL chuyên nghiệp).
- **Phân tích kết quả** bằng GPT-4o mini (OpenAI) để đưa ra đánh giá chi tiết.
- **Gửi báo cáo email tự động** với kết quả, screenshot và link chi tiết.

Không cần viết một dòng code nào cả!

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng. Đây là giải pháp tối ưu cho các doanh nghiệp có nhu cầu tự động hóa liên tục và bảo mật cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần quét thủ công mỗi URL, AI làm việc 24/7.
- **Phát hiện nguy cơ nhanh chóng**: Nhận báo cáo chi tiết về malware, phishing, hoặc nội dung độc hại.
- **Báo cáo tự động**: Email bao gồm **link kết quả, screenshot và JSON chi tiết** từ urlscan.io.
- **Tích hợp AI**: GPT-4o mini phân tích và tổng hợp kết quả một cách **cá nhân hóa và chuyên nghiệp**.
- **Bảo mật cao**: Không lưu trữ API key trong mã nguồn, sử dụng **n8n Credentials**.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản urlscan.io**:
   - [Đăng ký miễn phí](https://urlscan.io/) và lấy **API Key**.
2. **Tài khoản OpenAI** (để sử dụng GPT-4o mini):
   - [Đăng ký OpenAI](https://platform.openai.com/) và lấy **API Key**.
3. **Tài khoản Gmail** (để gửi báo cáo):
   - Cần **OAuth2** để n8n có thể gửi email tự động.
4. **Địa chỉ email nhận báo cáo** (điền trong node Gmail).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/7159](https://n8n.io/workflows/7159) và import vào **n8n Editor**.
- **Cách 2**: Copy toàn bộ JSON từ link trên và **paste vào n8n Editor** (tab "Import").

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này bao gồm **5 node chính**, các sếp cần cấu hình kỹ lưỡng như sau:

##### **🔹 Node 1: Webhook (Nhận URL từ bên ngoài)**
- **Path**: `/urlscan` (không thay đổi).
- **HTTP Method**: POST (đã mặc định).
- **Test Webhook**:
  - Gửi request POST đến URL của bạn (ví dụ: `https://domain.com/webhook/urlscan`) với body:
    ```json
    { "url": "https://example.com" }
    ```
  - Để test nhanh, sử dụng tool như **Postman** hoặc **cURL**:
    ```bash
    curl -X POST https://domain.com/webhook/urlscan \
    -H "Content-Type: application/json" \
    -d '{"url": "https://example.com"}'
    ```

##### **🔹 Node 2: Perform a scan (urlscan.io)**
- **Credentials**: Chọn `urlScanIoApi` (đã tạo trước khi import).
- **Lưu ý**:
  - Không cần thay đổi tham số nào, chỉ đảm bảo **API Key** đã được cài đặt đúng trong n8n Credentials.

##### **🔹 Node 3: Wait (Đợi kết quả quét)**
- **Thời gian mặc định**: 30 giây (đủ để urlscan.io tạo screenshot).
- **Nếu screenshot chưa ready**:
  - Mở node **StickyNote** (nếu có) để theo dõi log.
  - **Tăng thời gian wait** (ví dụ: 60s) trong trường hợp URL phức tạp.

##### **🔹 Node 4: Message a model (GPT-4o mini)**
- **Credentials**: Chọn `openAiApi` (đã tạo từ API Key OpenAI).
- **Prompt mặc định**:
  ```plaintext
  Analyze the URL scan results from urlscan.io and provide a summary of potential security threats. Include:
  1. Malware or phishing indicators.
  2. Suspicious domains or IPs.
  3. Any unusual behavior detected.
  4. Recommendations for action.
  ```
- **Lưu ý**:
  - Nếu muốn **cá nhân hóa prompt**, mở node này và chỉnh sửa trong tab "Code".

##### **🔹 Node 5: Send a message (Gmail)**
- **Credentials**: Chọn `gmailOAuth2` (đã cài đặt OAuth2).
- **Địa chỉ email nhận (To)**: Điền vào trường `To` trong node này.
- **Tiêu đề email mặc định**:
  ```plaintext
  URL Scan Results: [URL]
  ```
- **Nội dung email**:
  - Bao gồm **link kết quả urlscan.io**, **screenshot** và **JSON chi tiết**.
  - Nếu muốn **thêm logo hoặc footer**, mở node này và chỉnh sửa trong tab "Code".

---

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Gửi một URL mẫu (ví dụ: `https://example.com`) qua Webhook.
   - Kiểm tra **email nhận** để xem kết quả.
2. **Bật Active**:
   - Chuyển trạng thái workflow từ **Inactive** sang **Active**.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tích hợp với Slack/Telegram**:
   - Thay thế node Gmail bằng **Slack Webhook** hoặc **Telegram Bot** để thông báo kết quả ngay lập tức.
2. **Lưu log vào Google Sheets**:
   - Sử dụng node **Google Sheets** để ghi lại lịch sử quét URL và kết quả.
3. **Báo cáo định kỳ**:
   - Tạo một workflow riêng để **tổng hợp báo cáo hàng tuần** từ các kết quả quét.
4. **Cập nhật API Key**:
   - Nếu API Key của OpenAI hoặc urlscan.io hết hạn, **cập nhật trong Credentials** mà không cần thay đổi workflow.

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp cần **tự động hóa quét URL an ninh** mà không cần viết code. Với sự kết hợp giữa **urlscan.io** (quét URL chuyên nghiệp) và **GPT-4o mini** (phân tích AI), bạn sẽ nhận được **báo cáo chi tiết và cá nhân hóa** chỉ trong vài giây.

**Hành động ngay!**
1. Import workflow vào n8n của mình.
2. Cấu hình **API Key** và **email nhận**.
3. **Test với một URL** và bắt đầu tự động hóa bảo mật!

🔗 [Xem workflow gốc](https://n8n.io/workflows/7159) | 📌 [Cài đặt n8n Self-hosted](https://n8n.io/docs/hosting/self-hosted)

---
**Chia sẻ và đóng góp**: Nếu các sếp có ý tưởng cải tiến, hãy comment bên dưới hoặc liên hệ với tác giả [Calistus Christian](https://www.linkedin.com/in/calistuschristian/) để được hỗ trợ!