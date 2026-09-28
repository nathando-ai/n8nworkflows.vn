---
title: "🚀 Scraper AI Tự Động Lấy Profile Dev từ Stack Overflow & Lưu vào Google Sheets (Không Code)"
description: "Workflow tự động hóa AI-powered để scrape profile developer từ Stack Overflow, tóm tắt thông tin bằng OpenAI, và lưu dữ liệu vào Google Sheets với Bright Data. Giúp doanh nghiệp tìm kiếm và phân tích lead kỹ thuật hiệu quả chỉ với một click."
slug: "scraper-ai-stackoverflow-google-sheets"
tags: [n8n, automation, lead-generation, ai-summarization, bright-data, openai, no-code]
keywords: [scraper stack overflow, tự động hóa lead dev, n8n workflow, scrape profile developer, google sheets automation, ai agent n8n]
---

# 🚀 **Scraper AI Tự Động Lấy Profile Developer từ Stack Overflow & Lưu vào Google Sheets**

## **🔍 Giải quyết vấn đề gì?**
Bạn là một **doanh nghiệp IT, startup, hoặc nhà tuyển dụng** cần tìm kiếm và phân tích **profile developer** từ Stack Overflow để:
- **Tìm kiếm talent** cho dự án mới.
- **Phân tích xu hướng kỹ thuật** trong ngành.
- **Tạo danh sách lead** để liên hệ trực tiếp.
- **Tiết kiệm thời gian** so với việc copy-paste thủ công.

**Workflow này tự động hóa toàn bộ quy trình:**
✅ **Scrape** profile từ Stack Overflow (không cần viết code).
✅ **Tóm tắt & phân tích** thông tin bằng **AI (OpenAI GPT-4o-mini)**.
✅ **Lưu dữ liệu** vào **Google Sheets** để theo dõi và phân tích.
✅ **Hoạt động 24/7** khi cài trên **VPS tự host**.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần copy-paste thủ công, AI tự scrape và tóm tắt.
- **Dữ liệu chính xác**: AI phân tích và lưu thông tin **cấu trúc** (tên, vị trí, tags, reputation...).
- **Tự động hóa hoàn toàn**: Chỉ cần **click 1 nút** để bắt đầu, không cần lập trình.
- **Dễ mở rộng**: Có thể kết nối với **Slack/Telegram** để báo cáo kết quả hoặc **CRM** để quản lý lead.
- **Hoạt động liên tục**: Khi cài trên VPS, workflow chạy **24/7** mà không cần can thiệp.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản Bright Data MCP** (để scrape Stack Overflow):
   - [Đăng ký Bright Data](https://get.brightdata.com/1tndi4600b25) (mã giới thiệu để hỗ trợ tạo nội dung miễn phí).
   - **API Key** của Bright Data MCP (tham số `mcpClientApi` trong n8n).
2. **Tài khoản Google Sheets** (để lưu dữ liệu):
   - **File Google Sheets** đã tạo sẵn (cấu trúc 1 sheet với các cột: `Name`, `Location`, `Profile URL`, `Tags`, `Reputation`).
   - **OAuth 2.0 API Key** của Google Sheets (tham số `googleSheetsOAuth2Api`).
3. **Tài khoản OpenAI** (để AI tóm tắt dữ liệu):
   - **API Key** của OpenAI (tham số `openAiApi`).
4. **n8n Self-hosted** (để chạy workflow 24/7):
   - Cài đặt trên **VPS** (khuyến nghị sử dụng VPS từ TinoHost hoặc BNIX).
:::

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/5944](https://n8n.io/workflows/5944).
2. **Click "Import"** trong n8n Editor.
3. **Chọn file JSON** đã tải và **import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Tải workflow** từ link trên và **copy toàn bộ JSON**.
2. Trong n8n Editor, **click "Import"** → **Paste JSON** và **import**.

---
### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **11 node**, các sếp cần **cấu hình chính xác** các node sau:

#### **🔹 Node 1: Start Scraping (Manual Trigger)**
- **Không cần chỉnh**, chỉ cần **click "Execute"** khi muốn chạy.

#### **🔹 Node 2: Input Setup (Set)**
- **Điền các tham số tùy chỉnh** (nếu cần):
  - **Forum target**: Chọn `Stack Overflow` (mặc định).
  - **Filters**: Vị trí (`location`), tags (`tags`), số lượng profile (`limit`).
  - **Example**:
    ```json
    {
      "forum": "stackoverflow",
      "filters": {
        "location": "Vietnam",
        "tags": ["javascript", "nodejs"],
        "limit": 10
      }
    }
    ```

#### **🔹 Node 3: AI Agent: Generate Scraper Instructions (Agent)**
- **Không cần chỉnh**, AI sẽ tự động **tạo instruction** cho Bright Data scrape.
- **Prompt mặc định** đã được tối ưu cho Stack Overflow.

#### **🔹 Node 4: MCP Client to Scrape as HTML (Bright Data MCP)**
- **Chọn credentials**:
  - `mcpClientApi` → **Paste API Key** từ Bright Data.
- **Key Parameters**:
  - `operation`: `executeTool` (không cần chỉnh).
  - **URL Example**:
    ```json
    "url": "https://stackoverflow.com/users?tab=Activity&filter=All"
    ```

#### **🔹 Node 5: Conversation Memory (Memory Buffer Window)**
- **Không cần chỉnh**, AI sẽ **giữ context** giữa các bước.

#### **🔹 Node 6: Format Data for Google Sheets (Code)**
- **Mở node Code** và **chỉnh script** nếu cần:
  ```javascript
  // Script mặc định (không cần chỉnh trừ khi muốn thêm/bỏ trường)
  return [
    {
      Name: item.name,
      Location: item.location,
      ProfileURL: item.profileUrl,
      Tags: item.tags.join(", "),
      Reputation: item.reputation
    }
  ];
  ```

#### **🔹 Node 7: Save Leads to Google Sheet (Google Sheets)**
- **Chọn credentials**:
  - `googleSheetsOAuth2Api` → **Paste OAuth Key** từ Google Sheets.
- **Key Parameters**:
  - `operation`: `append` (lưu dữ liệu mới vào sheet).
  - **Sheet Name**: Điền tên sheet (ví dụ: `StackOverflow_Leads`).
  - **Range**: `Sheet1!A1` (đảm bảo sheet có cột `Name`, `Location`, `ProfileURL`, `Tags`, `Reputation`).

#### **🔹 Node 8-11: OpenAI & Output Parser (AI Tóm Tắt)**
- **Không cần chỉnh**, AI sẽ tự động:
  1. **Tóm tắt profile** (Node `lmChatOpenAi`).
  2. **Chuyển dữ liệu thành JSON cấu trúc** (Node `outputParserStructured`).

---
### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Click **Execute** và kiểm tra **Google Sheets** xem dữ liệu đã lưu chưa.
2. **Bật Active**:
   - Đặt workflow ở **mode Active** để chạy tự động khi có trigger.

---

## ✍️ **Mẹo & gợi ý nâng cao**
### **1. Kết nối với Slack/Telegram để báo cáo kết quả**
- **Thêm node Slack/Telegram Webhook** sau `Save Leads to Google Sheet`.
- **Gửi thông báo** khi scrape hoàn tất:
  ```json
  {
    "text": `🚀 Scrape hoàn tất! Đã lấy ${data.length} profile developer từ Stack Overflow.`
  }
  ```

### **2. Lưu log vào Google Drive**
- **Thêm node Google Drive** để lưu **log scrape** (thời gian, số lượng profile, lỗi nếu có).

### **3. Tự động scrape định kỳ (Schedule Trigger)**
- **Thay thế Manual Trigger** bằng **Schedule Trigger** (n8n Pro) để chạy hàng ngày/tuần.

### **4. Kết nối với CRM (HubSpot, Salesforce)**
- **Thêm node HubSpot/Salesforce** sau `Save Leads to Google Sheet` để tự động **tạo lead** trong CRM.

### **5. Tối ưu AI với Prompt riêng**
- **Mở node `AI Agent`** và chỉnh **prompt** để AI:
  - **Lọc profile** theo tiêu chí cụ thể (ví dụ: chỉ lấy dev có `reputation > 1000`).
  - **Trích xuất thông tin chi tiết** (ví dụ: liên kết LinkedIn, GitHub).

---
## 📌 **Kết luận**
Workflow này **giải phóng bạn khỏi việc copy-paste thủ công** và **tự động hóa toàn bộ quy trình tìm kiếm lead developer** từ Stack Overflow. **Chỉ cần 1 click**, AI sẽ:
✔ **Scrape** profile.
✔ **Tóm tắt & phân tích** thông tin.
✔ **Lưu vào Google Sheets** để theo dõi.

**Hành động ngay!**
1. **Cài n8n trên VPS** (khuyến nghị TinoHost/BNIX).
2. **Import workflow** và **cấu hình API Key**.
3. **Click "Execute"** và **xem dữ liệu tự động lưu vào Google Sheets**.

**🚀 Hãy bắt đầu tự động hóa ngay hôm nay!** Nếu gặp vấn đề, liên hệ [Yaron Been](https://www.linkedin.com/in/yaronbeen/) qua LinkedIn hoặc YouTube của anh ta để hỗ trợ.

---
**🎁 Bonus**: Nếu sử dụng **Bright Data** qua link này, bạn sẽ hỗ trợ tạo nội dung miễn phí cho cộng đồng n8n!
👉 [Đăng ký Bright Data](https://get.brightdata.com/1tndi4600b25)