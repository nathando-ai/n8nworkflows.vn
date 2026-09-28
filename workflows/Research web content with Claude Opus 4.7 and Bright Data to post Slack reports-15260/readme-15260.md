---
title: "🤖 Tự Động Hoàn Thành Nghiên Cứu Web Bằng AI Claude Opus 4.7 + Bright Data & Gửi Báo Cáo Trên Slack (Không Cần Code)"
description: "Workflow tự động hóa nghiên cứu web chuyên nghiệp với AI Claude Opus 4.7 và công cụ Bright Data để lấy dữ liệu từ Google và trang web, tổng hợp báo cáo và gửi trực tiếp lên Slack trong 2-5 phút. Giúp các sếp tiết kiệm thời gian và nhận kết quả chính xác 24/7."
slug: "tieu-dong-hoan-thanh-nghien-cuu-web-bang-ai-claude-opus-4-7-bright-data-slack"
tags: [n8n, automation, ai-rag, market-research, bright-data, anthropic, slack, no-code]
keywords: [n8n workflow nghiên cứu web, tự động hóa nghiên cứu thị trường, Claude Opus 4.7 Bright Data, gửi báo cáo Slack tự động, AI RAG cho doanh nghiệp]
---

# 🚀 **Tự Động Hoàn Thành Nghiên Cứu Web Bằng AI + Bright Data & Gửi Báo Cáo Trên Slack**

## **💡 Giới Thiệu: Giải Pháp Tự Động Hóa Nghiên Cứu Web Cho Doanh Nghiệp**
Các sếp đã bao giờ phải mất **giờ đồng hồ** để tìm kiếm thông tin trên Google, đọc trang web, tổng hợp dữ liệu và viết báo cáo? Hay phải lo lắng về **CAPTCHA, bot detection, hoặc nội dung bị geo-block**? Workflow này sẽ **giải quyết tất cả** bằng cách:
✅ **Tự động hóa toàn bộ quy trình** từ tìm kiếm đến tổng hợp báo cáo.
✅ **Sử dụng AI Claude Opus 4.7** để phân tích và tổng hợp thông tin một cách logic.
✅ **Bright Data Web Unlocker** để lấy dữ liệu từ Google và trang web **không bị chặn**, kể cả trang JavaScript-heavy.
✅ **Gửi báo cáo tự động lên Slack** (hoặc Discord, Email, CRM…) trong **2-5 phút**.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần thủ công tìm kiếm, đọc trang web, tổng hợp dữ liệu.
- **Dữ liệu chính xác & toàn diện**: Bright Data lấy thông tin từ Google và trang web **không bị chặn**, kể cả trang có JavaScript.
- **Báo cáo tự động hóa**: AI tổng hợp và gửi báo cáo lên Slack (hoặc nơi khác) **một cách tự động**.
- **Cá nhân hóa**: Điền mục tiêu nghiên cứu và đối tượng mục tiêu, AI sẽ tự động tìm kiếm và tổng hợp.
- **Hoạt động 24/7**: Workflow chạy liên tục, không cần can thiệp thủ công.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần:
1. **Tài khoản Bright Data** với **Web Unlocker** (trong đó có `web_unlocker_agent`).
   👉 [Đăng ký Bright Data](https://brightdata.com) (Mã giảm giá: **BRIGHTDATA** - giảm 20%).
2. **API Key của Anthropic** (để sử dụng Claude Opus 4.7).
   👉 [Đăng ký API Key Anthropic](https://console.anthropic.com/).
3. **Slack Workspace** và **channel** để gửi báo cáo.
   👉 [Đăng ký Slack](https://slack.com).
4. **n8n Self-hosted** (để workflow chạy 24/7).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (Mã giảm giá: **VPSN8N** - giảm tới 39%).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/15260](https://n8n.io/workflows/15260).
- **Nhấn "Import"** trong n8n Editor.
- **Hoặc copy/paste JSON** vào Editor và nhấn "Create Workflow".

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflows này gồm **5 node chính**, các sếp cần cấu hình như sau:

##### **🔹 Node 1: On Form Submission (formTrigger)**
- **Mục đích**: Hiển thị một **bảng form công khai** để người dùng nhập:
  - **Research goal** (mục tiêu nghiên cứu).
  - **Target audience** (đối tượng mục tiêu).
- **Lưu ý**:
  - Nếu muốn thay đổi trigger, có thể **đổi thành Webhook, Slack Command, hoặc Schedule**.
  - **Không cần thay đổi** nếu muốn giữ nguyên form.

##### **🔹 Node 2: AI Research Agent (agent)**
- **Mục đích**: AI **Claude Opus 4.7** sẽ **lập kế hoạch nghiên cứu**, gọi Bright Data để lấy dữ liệu từ Google và trang web, rồi **tổng hợp báo cáo**.
- **Lưu ý**:
  - **Không cần chỉnh sửa** nếu muốn giữ nguyên hệ thống prompt.
  - Nếu muốn **tùy chỉnh báo cáo**, mở node này và chỉnh sửa **system prompt**.

##### **🔹 Node 3: Anthropic Chat Model (lmChatAnthropic)**
- **Mục đích**: Sử dụng **Claude Opus 4.7** (hoặc mô hình khác như GPT-4, Gemini).
- **Lưu ý**:
  - **Điền API Key Anthropic** vào **Credentials** của node này.
  - Nếu muốn **thay đổi mô hình AI**, chỉnh sửa `model` trong **keyParameters**:
    ```json
    "model": {
      "__rl": true,
      "mode": "list",
      "value": "claude-3-opus-20240229", // Thay đổi mô hình ở đây
      "cachedResultName": "Claude Opus 4.7"
    }
    ```

##### **🔹 Node 4: Bright Data Web Unlocker (brightDataTool)**
- **Mục đích**: **Lấy dữ liệu từ Google và trang web** mà không bị chặn (CAPTCHA, bot detection, geo-block).
- **Lưu ý**:
  - **Đăng ký Bright Data** và **điền API Key** vào **Credentials** của node này.
  - **Chọn `web_unlocker_agent`** trong **Tool Configuration**.
  - **Không cần chỉnh sửa** nếu muốn giữ nguyên cấu hình mặc định.

##### **🔹 Node 5: Send Report to Slack (slack)**
- **Mục đích**: **Gửi báo cáo tự động lên Slack** (hoặc Discord, Email, CRM…).
- **Lưu ý**:
  - **Đăng ký Slack App** và **điền Token** vào **Credentials**.
  - **Chọn channel** trong **Channel** (ví dụ: `#reports`).
  - **Nếu muốn thay đổi output**, có thể đổi thành:
    - **Email** (Gmail, Outlook, SMTP).
    - **Discord / Microsoft Teams / Telegram**.
    - **Notion / Google Docs / Airtable**.
    - **CRM (HubSpot, Salesforce)**.

#### **3. Kích Hoạt ⚡️**
- **Test Run**: Nhấn **"Execute"** và điền dữ liệu mẫu vào form.
- **Bật Active**: Sau khi kiểm tra, **bật workflow** để chạy tự động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁCH THAY ĐỔI TRIGGER]
- **Thay form bằng Webhook**: Sử dụng **n8n-nodes-base.webhook** để nhận dữ liệu từ API.
- **Thay bằng Slack Command**: Sử dụng **n8n-nodes-base.slackCommand**.
- **Thay bằng Schedule**: Sử dụng **n8n-nodes-base.schedule** để chạy hàng ngày/tuần.
- **Thay bằng Chat Trigger**: Sử dụng **n8n-nodes-base.chatTrigger** (Google Assistant, Telegram Bot…).
:::

:::tip[CÁCH TÙY CHỈNH BÁO CÁO]
- Mở node **AI Research Agent** và chỉnh sửa **system prompt** để:
  - **Thay đổi định dạng báo cáo** (Markdown, JSON, HTML).
  - **Thêm/loại nội dung** cần trong báo cáo.
  - **Tùy chỉnh giọng điệu** (chuyên nghiệp, thân thiện, ngắn gọn…).
:::

:::note[CÁCH LƯU LOG & THEO DÕI]
- **Thêm node Sticky Note** (`n8n-nodes-base.stickyNote`) để **lưu log** của mỗi lần chạy.
- **Kết hợp với Google Sheets** (`n8n-nodes-base.googleSheets`) để **lưu báo cáo định kỳ**.
- **Gửi báo cáo qua Email** (`n8n-nodes-base.email`) nếu không muốn dùng Slack.
:::

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** của các sếp khỏi việc nghiên cứu web thủ công, đồng thời **đảm bảo dữ liệu chính xác và toàn diện** nhờ Bright Data và AI Claude Opus 4.7. **Gửi báo cáo tự động lên Slack** (hoặc nơi khác) trong **2-5 phút** là điều hoàn toàn có thể!

👉 **Bắt đầu ngay** bằng cách:
1. **Đăng ký Bright Data** và **Anthropic API Key**.
2. **Import workflow** và **cấu hình credentials**.
3. **Bật workflow** và **nhận báo cáo tự động**!

**Chúc các sếp thành công!** 🚀