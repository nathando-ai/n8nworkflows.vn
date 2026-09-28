---
title: "🚀 Tự Động Hóa Báo Cáo Tech Stack Hàng Tuần Với BuiltWith, GPT-4o & Gmail - Không Cần Code!"
description: "Tự động hóa việc phân tích và tổng hợp stack công nghệ của các website thương mại điện tử hàng tuần, gửi báo cáo tự động qua email với AI GPT-4o. Giúp các sếp tiết kiệm thời gian, nhận được thông tin chính xác và cá nhân hóa cho khách hàng."
slug: "tieu-dong-hoa-bao-cao-tech-stack-hang-tuan"
tags: [n8n, automation, marketing, no-code, ai, builtwith, gmail, google-sheets, openai]
keywords: [tự động hóa n8n, báo cáo tech stack, builtwith api, gpt-4o tự động hóa, tự động hóa email marketing, tự động hóa phân tích website]
---

# 🚀 **Tự Động Hóa Báo Cáo Tech Stack Hàng Tuần Cho Website Thương Mại Điện Tử**

## **Giới Thiệu**
Bạn có bao giờ phải tốn thời gian thủ công phân tích stack công nghệ của các website thương mại điện tử để báo cáo cho khách hàng hoặc đội ngũ kỹ thuật? Hay phải mất nhiều giờ để tra cứu thông tin từ BuiltWith, Google Sheets và tổng hợp lại thành báo cáo dễ đọc?

**Workflow này giải quyết vấn đề đó 100% tự động hóa!** Nó sẽ:
- **Tự động lấy danh sách website** từ Google Sheets hàng tuần.
- **Phân tích stack công nghệ** của mỗi website thông qua API BuiltWith.
- **Tổng hợp thông tin** bằng AI GPT-4o thành báo cáo dễ đọc.
- **Gửi báo cáo tự động** qua email cho bạn hoặc khách hàng.

Không cần viết một dòng code nào cả!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần thủ công phân tích mỗi website.
- **Tính chính xác cao**: Dữ liệu lấy từ API BuiltWith và AI GPT-4o.
- **Báo cáo cá nhân hóa**: AI tổng hợp thông tin thành văn bản dễ đọc.
- **Hoạt động liên tục**: Workflow chạy tự động hàng tuần, không cần can thiệp.
- **Dễ mở rộng**: Thêm website mới chỉ cần cập nhật Google Sheets.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets** với một bảng chứa danh sách website (cột `Domain`).
2. **API Key BuiltWith** (miễn phí, đăng ký tại [BuiltWith](https://builtwith.com/)).
3. **Tài khoản OpenAI** với API Key (đăng ký tại [OpenAI](https://platform.openai.com/)).
4. **Tài khoản Gmail** để gửi báo cáo tự động.
5. **Tài khoản n8n** (cài đặt trên VPS hoặc dùng phiên bản cloud miễn phí).
:::

---

## 🚀 **Cách Import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Truy cập [n8n.io](https://n8n.io/) và đăng nhập.
2. Nhấn **"Import"** và chọn file JSON hoặc dán JSON vào ô `Paste JSON`.
3. Nhấn **"Import"** để hoàn tất.

---
### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **7 node chính**, các sếp cần chú ý cấu hình như sau:

#### **📅 Node 1: Weekly Trigger (Thời gian kích hoạt hàng tuần)**
- **Tên Node**: `Weekly Trigger`
- **Cấu hình**:
  - Chọn **Schedule Trigger**.
  - Đặt thời gian chạy hàng tuần (ví dụ: **Mỗi thứ Hai lúc 9h sáng**).
  - Lưu ý: Nếu muốn chạy khác, chỉnh `cron` trong node này (ví dụ: `0 9 * * 1` cho thứ Hai lúc 9h).

#### **🗂️ Node 2: Fetch Domain List (Lấy danh sách website từ Google Sheets)**
- **Tên Node**: `Fetch Domain List`
- **Cấu hình**:
  - Chọn **Google Sheets**.
  - Đăng nhập tài khoản OAuth2 của Google Sheets.
  - Chọn **Sheet Name** và **Range** (ví dụ: `Sheet1!A2:A100`).
  - **Lưu ý**: Cột `A` phải chứa tên domain (ví dụ: `nike.com`, `asos.com`).

#### **🌐 Node 3: Get Tech Stack (BuiltWith API) (Lấy stack công nghệ từ API)**
- **Tên Node**: `Get Tech Stack (BuiltWith API)`
- **Cấu hình**:
  - Chọn **HTTP Request**.
  - Điền **URL**: `https://api.builtwith.com/api/v3/website/{domain}`
  - Thay `{domain}` bằng `$json["domain"]` (để lấy domain từ node trước).
  - Thêm **Headers**:
    ```
    Authorization: Bearer YOUR_BUILTWITH_API_KEY
    ```
  - **Lưu ý**: Thay `YOUR_BUILTWITH_API_KEY` bằng API Key của BuiltWith.

#### **🧮 Node 4: Extract Tech Stack Info (Trích xuất thông tin stack)**
- **Tên Node**: `Extract Tech Stack Info` (Node Code)
- **Cấu hình**:
  - Sử dụng **JavaScript** để xử lý JSON trả về từ BuiltWith.
  - Dưới đây là mã mẫu để trích xuất stack công nghệ:
    ```javascript
    // Lấy danh sách stack từ BuiltWith
    const techStack = $input.all().map(item => {
      const data = JSON.parse(item.json);
      return {
        domain: item.json.domain,
        stack: data.technologies || []
      };
    });

    // Trích xuất stack quan trọng (ecommerce, analytics, payment)
    const filteredStack = techStack.map(item => {
      const ecommerce = item.stack.filter(t => t.category === "Ecommerce");
      const analytics = item.stack.filter(t => t.category === "Analytics");
      const payment = item.stack.filter(t => t.category === "Payment");
      return {
        domain: item.domain,
        ecommerce: ecommerce.map(t => t.name),
        analytics: analytics.map(t => t.name),
        payment: payment.map(t => t.name)
      };
    });

    return filteredStack;
    ```
  - **Lưu ý**: Các sếp có thể điều chỉnh logic để lấy thông tin cần thiết.

#### **🤖 Node 5: Generate Stack Summary (AI) (Tổng hợp báo cáo bằng GPT-4o)**
- **Tên Node**: `Generate Stack Summary (AI)`
- **Cấu hình**:
  - Chọn **LangChain Agent** (n8n-nodes-langchain.agent).
  - Đăng nhập **OpenAI API Key** (credentials: `openAiApi`).
  - Đặt **Model**: `gpt-4o-mini`.
  - **Prompt mẫu** (có thể chỉnh sửa):
    ```
    Analyze the tech stack of {domain} and summarize the key technologies used.
    Focus on ecommerce platforms, analytics tools, and payment gateways.
    Format the response as a clear bullet list.
    ```
  - **Lưu ý**: Nếu muốn thay đổi cách AI tổng hợp, chỉnh sửa prompt.

#### **📧 Node 6: Send Summary Email (Gửi báo cáo qua email)**
- **Tên Node**: `Send Summary Email`
- **Cấu hình**:
  - Chọn **Gmail**.
  - Đăng nhập tài khoản OAuth2 của Gmail.
  - Điền **Subject**: `Báo cáo Tech Stack Hàng Tuần - {date}`.
  - **Body Email** (HTML):
    ```html
    <h2>Báo cáo Tech Stack Hàng Tuần</h2>
    <p>Xin chào,</p>
    <p>Dưới đây là tổng hợp stack công nghệ của các website:</p>
    <ul>
      {% for item in $json %}
        <li><strong>{{ item.domain }}</strong></li>
        <p><strong>Ecommerce:</strong> {{ item.ecommerce | join(", ") }}</p>
        <p><strong>Analytics:</strong> {{ item.analytics | join(", ") }}</p>
        <p><strong>Payment:</strong> {{ item.payment | join(", ") }}</p>
      {% endfor %}
    </ul>
    <p>Trân trọng,</p>
    <p>Automation Team</p>
    ```
  - **Recipients**: Điền email của bạn hoặc khách hàng (ví dụ: `sếp@example.com`).
  - **Lưu ý**: Nếu muốn gửi cho nhiều người, chia email bằng dấu phẩy.

---
### **3. Kích hoạt ⚡️**
1. **Test Run**: Nhấn **"Run Workflow"** để kiểm tra dữ liệu mẫu.
2. **Active Workflow**: Sau khi kiểm tra thành công, bật **Active** để workflow chạy tự động hàng tuần.

---

## ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁCH LÀM NGOÀI]
1. **Thêm Slack/Telegram Notifications**:
   - Sử dụng node **Slack** hoặc **Telegram Bot** để gửi thông báo khi workflow hoàn thành.
   - Ví dụ: `"Báo cáo Tech Stack đã được gửi qua email!"`.

2. **Lưu Log vào Google Sheets**:
   - Thêm node **Google Sheets** sau node **Send Email** để ghi lại lịch sử báo cáo.
   - Cột mới: `Date`, `Status`, `Email Sent To`.

3. **Tự động gửi báo cáo định kỳ**:
   - Nếu muốn gửi báo cáo hàng tháng thay vì hàng tuần, chỉnh **Schedule Trigger** thành `0 9 1 * *` (mỗi tháng ngày 1 lúc 9h).

4. **Tích hợp với Notion/Confluence**:
   - Thay vì gửi email, có thể gửi báo cáo vào **Notion** hoặc **Confluence** bằng node **Notion API**.

5. **Tự động cập nhật website mới**:
   - Thêm một cột `Status` vào Google Sheets để đánh dấu website đã được phân tích.
   - Sử dụng node **Code** để lọc chỉ lấy website mới hoặc chưa phân tích.
:::

---

## 📌 **Kết luận**
Workflow này giúp các sếp **tự động hóa hoàn toàn** việc phân tích và báo cáo stack công nghệ của website thương mại điện tử. Không cần viết code, không cần thủ công, và báo cáo được gửi tự động hàng tuần!

**Hãy áp dụng ngay và tiết kiệm thời gian cho công việc phân tích kỹ thuật!** 🚀

---
**Cần hỗ trợ?**
- Liên hệ tác giả: [Yaron Been](https://www.linkedin.com/in/yaronbeen/)
- Xem thêm tutorial: [Youtube - Yaron Been](https://www.youtube.com/@YaronBeen/videos)