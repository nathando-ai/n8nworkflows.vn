---
title: "🚀 Tự Động Hoá Scrape Dữ Liệu Cửa Hàng Local + Gửi Gợi Ý Hợp Tác qua Email (Bright Data + OpenAI)"
description: "Workflow tự động hóa 100% không code giúp các sếp scrape thông tin chi tiết từ Yelp (địa chỉ, đánh giá, dịch vụ, giờ hoạt động...) và tự động gửi email gợi ý hợp tác cá nhân hóa. Tiết kiệm tới 10 giờ/lần so với phương pháp thủ công!"
slug: "tieu-dong-hoa-scrape-yelp-gui-email-gop-y"
tags: [n8n, automation, lead-generation, ai-summarization, bright-data, openai]
keywords: [n8n workflow scrape yelp, tự động hóa scrape dữ liệu, gửi email gợi ý hợp tác, bright data api, openai gpt-4.1-mini, lead generation]
---

# 🚀 **Scrape Dữ Liệu Cửa Hàng Local từ Yelp + Gửi Email Hợp Tác Tự Động (Bright Data + OpenAI)**

## **📌 Nỗi Đau Của Các Sếp**
Bạn có bao giờ phải:
- **Tốn thời gian** để copy-paste thông tin từ Yelp (địa chỉ, số điện thoại, giờ hoạt động, dịch vụ...) vào bảng Excel?
- **Khó tìm kiếm** thông tin chi tiết của các cửa hàng local để xây dựng chiến lược marketing hoặc hợp tác?
- **Bị chậm trễ** khi phải gửi email gợi ý hợp tác một cách thủ công, dẫn đến mất cơ hội?

**Workflow này giải quyết tất cả!** Với công nghệ **scraping AI + OpenAI**, các sếp chỉ cần **nhập URL Yelp của cửa hàng**, hệ thống sẽ tự động:
✅ **Scrape** tất cả thông tin chi tiết (đánh giá, địa chỉ, dịch vụ, giờ hoạt động...)
✅ **Tự động hóa email** gửi gợi ý hợp tác cá nhân hóa
✅ **Tiết kiệm 10+ giờ/lần** so với phương pháp thủ công

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Scrape và gửi email chỉ trong **vài giây** thay vì nhiều giờ.
- **Dữ liệu chính xác**: Thông tin được tự động hóa từ Yelp, không sai sót.
- **Email cá nhân hóa**: Nội dung email được tối ưu bằng AI, tăng tỷ lệ phản hồi.
- **Hoạt động liên tục**: Chạy tự động 24/7 trên VPS, không phụ thuộc vào thời gian làm việc.
- **Tăng cơ hội hợp tác**: Gửi gợi ý đến nhiều cửa hàng local một cách hiệu quả.
:::

---

## 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản Bright Data MCP** (để scrape Yelp):
   - [Đăng ký Bright Data](https://get.brightdata.com/1tndi4600b25) (mã giới thiệu: **1tndi4600b25**)
   - **API Key** từ Dashboard Bright Data MCP
✔ **Tài khoản Gmail** (để gửi email hợp tác):
   - **OAuth 2.0 Credentials** (cài đặt trong n8n)
✔ **API Key OpenAI** (để sử dụng GPT-4.1-mini):
   - [Đăng ký OpenAI](https://platform.openai.com/account/api-keys) và lấy API Key

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
```bash
# Cách 1: Import từ file JSON
1. Tải file workflow từ [n8n.io/workflows/5971](https://n8n.io/workflows/5971)
2. Trên trang n8n Editor, nhấn **Import** và chọn file JSON
3. Chọn **Create Workflow**

# Cách 2: Copy/Paste JSON
1. Copy toàn bộ JSON từ [n8n.io/workflows/5971](https://n8n.io/workflows/5971)
2. Trên n8n Editor, nhấn **Import** → **Paste JSON**
```

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow gồm **3 phần chính**, các sếp cần cấu hình kỹ các node sau:

#### **🔹 PHẦN 1: Trigger & Nhập URL Yelp**
- **Node: `⚡ Trigger: Manual Execution`**
  - **Lưu ý**: Chỉnh **Manual Trigger** để kích hoạt workflow khi cần.
- **Node: `📝 Set Yelp Business URL`**
  - **Cách sử dụng**:
    - Nhập **URL Yelp** của cửa hàng (ví dụ: `https://www.yelp.com/biz/dr-william-kimbrough-md`)
    - **Không cần chỉnh gì khác**, chỉ cần nhập URL và nhấn **Execute**.

#### **🔹 PHẦN 2: Scrape Dữ Liệu với AI Agent**
- **Node: `🤖 Agent: Scrape Yelp Business Info`**
  - **Cấu hình Bright Data MCP**:
    - Đi đến **Credentials** → **mcpClientApi**
    - Nhập **API Key** từ Bright Data MCP (đã lấy từ [đây](https://get.brightdata.com/1tndi4600b25))
  - **Node con: `🌐 Bright Data MCP Client`**
    - **Operation**: Đảm bảo chọn **`executeTool`**
    - **Tool**: Chọn **`scrape_as_markdown`** (đã cấu hình sẵn trong workflow)
  - **Node con: `📝 Parse Scraped Data into JSON`**
    - **Không cần chỉnh**, AI tự động hóa việc chuyển đổi dữ liệu thành JSON.

#### **🔹 PHẦN 3: Gửi Email Hợp Tác Tự Động**
- **Node: `📧 Send Partnership Proposal to Business Email`**
  - **Cấu hình Gmail**:
    - Đi đến **Credentials** → **gmailOAuth2**
    - Cài đặt **OAuth 2.0** cho tài khoản Gmail (theo hướng dẫn [n8n Gmail Setup](https://docs.n8n.io/integrations/builtins/nodes/n8n-nodes-base.gmail.html))
  - **Cấu hình email**:
    - **Subject**: Ví dụ: *"Gợi ý Hợp Tác Tăng Doanh Thu cho [Tên Cửa Hàng]"* (có thể chỉnh trong **Node `lmChatOpenAi`**)
    - **Nội dung email**: AI tự động hóa bằng **GPT-4.1-mini** (không cần chỉnh, trừ khi muốn thay đổi template).

---
### **3. Kích Hoạt ⚡️**
- **Test Run**:
  1. Nhập **URL Yelp** của một cửa hàng (ví dụ: `https://www.yelp.com/biz/cafe-xanh-ho-chi-minh`)
  2. Nhấn **Execute** và kiểm tra:
     - Dữ liệu scrape có đầy đủ không? (Địa chỉ, số điện thoại, giờ hoạt động...)
     - Email có gửi thành công không?
- **Bật Active**:
  - Sau khi test thành công, chuyển **Status** từ **Draft** sang **Active**.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
### **🔹 1. Tự Động Hoá Scrape Nhiều Cửa Hàng**
- **Sử dụng Webhook** thay vì Manual Trigger:
  - Cài đặt **Node `webhook`** để nhận danh sách URL từ Excel/Google Sheets.
  - Ví dụ: Nhập danh sách URL vào **Google Sheets**, sau đó **n8n Webhook** sẽ tự động scrape và gửi email cho từng cửa hàng.

### **🔹 2. Lưu Log Dữ Liệu**
- **Thêm Node `stickyNote`** để lưu dữ liệu scrape vào **Google Sheets** hoặc **Notion**.
- **Cách làm**:
  1. Thêm **Node `n8n-nodes-base.stickyNote`** sau **`Parse Scraped Data into JSON`**.
  2. Cấu hình **Google Sheets API** và lưu dữ liệu vào bảng mới.

### **🔹 3. Tối Ưu Email Bằng AI**
- **Chỉnh Prompt cho OpenAI**:
  - Trong **Node `lmChatOpenAi`**, thay đổi **Prompt** để email phù hợp với ngành nghề cụ thể:
    ```json
    "prompt": "Tạo email gợi ý hợp tác cho cửa hàng [Tên Cửa Hàng] trong ngành [Ngành Nghề]. Nội dung phải bao gồm:
    1. Giới thiệu về dịch vụ của tôi
    2. Lợi ích hợp tác cụ thể
    3. Call-to-action rõ ràng (ví dụ: 'Hãy liên hệ qua email này để thảo luận chi tiết')"
    ```

### **🔹 4. Gửi Email qua Slack/Telegram**
- **Thêm Node `slack`** hoặc **`telegram`** để thông báo khi email gửi thành công:
  - Ví dụ: Khi email gửi xong, hệ thống tự động thông báo trên **Slack Channel** hoặc **Telegram Bot**.

---

## 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn:
✔ **Tự động hóa scrape dữ liệu** từ Yelp một cách nhanh chóng.
✔ **Gửi email hợp tác** một cách cá nhân hóa, tăng tỷ lệ phản hồi.
✔ **Tiết kiệm thời gian** và tập trung vào chiến lược kinh doanh.

**Hành động ngay!**
1. **Cài đặt n8n trên VPS** (để workflow chạy 24/7).
2. **Import workflow** và cấu hình **Bright Data + Gmail + OpenAI**.
3. **Nhập URL Yelp** của cửa hàng đầu tiên và **nhấn Execute**!

**🚀 Cùng tự động hóa công việc của mình ngay hôm nay!** 🚀

---
:::note[Lưu Ý Quan Trọng]
- **Bright Data MCP** có giới hạn scrape (check **Free Tier** của Bright Data).
- **OpenAI API** có giới hạn request/month (đăng ký **Plus Plan** nếu cần scrape nhiều).
- **Gmail OAuth** cần **2FA bật** để tránh bị block.
:::

---
**🔗 Tài Liệu Tham Khảo:**
- [Bright Data MCP Documentation](https://docs.brightdata.com/docs/mcp-client)
- [n8n Gmail Setup Guide](https://docs.n8n.io/integrations/builtins/nodes/n8n-nodes-base.gmail.html)
- [OpenAI API Reference](https://platform.openai.com/docs/api-reference)