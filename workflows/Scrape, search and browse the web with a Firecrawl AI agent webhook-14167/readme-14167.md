---
title: "🤖 **Tự Động Hoá Nghiên Cứu Web Tốc Độ AI: Scrape & Search với Firecrawl + n8n (Không Cần Code!)""
description: "Workflow tự động hóa nghiên cứu thị trường, phân tích đối thủ và thu thập dữ liệu web bằng AI + Firecrawl, trả về kết quả cấu trúc JSON chính xác chỉ trong vài giây. Giúp các sếp tiết kiệm hàng giờ công sức so sánh thủ công."
slug: "tieu-dong-hoa-nghien-cuu-web-firecrawl-n8n"
tags: [n8n, automation, market-research, ai-rag, firecrawl, no-code, ai-agent]
keywords: [n8n workflow scrape web, tự động hóa nghiên cứu thị trường, firecrawl n8n, ai agent webhook, dữ liệu web tự động, phân tích đối thủ không code]
---

# 🚀 **Tự Động Hoá Nghiên Cứu Web Tốc Độ AI: Scrape & Search với Firecrawl + n8n**

Hãy tưởng tượng một tình huống: Các sếp cần **so sánh sản phẩm của đối thủ**, **tìm kiếm thông tin thị trường mới** hoặc **thu thập dữ liệu từ hàng ngàn trang web** để ra quyết định kinh doanh. Thời gian làm thủ công? **Hàng giờ**, thậm chí **hàng ngày**! Kết quả lại **không chính xác**, **không cấu trúc** và **khó so sánh**.

**Workflow này giải quyết tất cả!** Dùng **AI + Firecrawl + n8n**, các sếp chỉ cần **gửi một yêu cầu bằng văn bản** (natural language), hệ thống sẽ:
✅ **Tự động scrape** thông tin từ web
✅ **Tìm kiếm sâu** trên Google, Bing, và các nguồn khác
✅ **Tự động hóa browser** để lấy dữ liệu động (login, scroll, interact)
✅ **Trả về kết quả cấu trúc JSON** (không cần xử lý thêm)
✅ **Hoạt động 24/7** mà không cần can thiệp của con người

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và **không bị gián đoạn**, các sếp nên **self-host n8n** trên VPS riêng. Đây là giải pháp **an toàn, nhanh chóng và tiết kiệm chi phí** so với hosting cloud.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ sức mạnh cho workflow này)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Thay vì mất **3-5 giờ** để scrape thủ công, workflow hoàn thành trong **vài giây**.
- **Dữ liệu chính xác & cấu trúc**: Không còn lo **lỗi copy-paste** hay **dữ liệu rác**, kết quả luôn **sạch sẽ và dễ phân tích**.
- **Tự động hóa 24/7**: Hoạt động **một cách độc lập**, không cần can thiệp của con người.
- **Phân tích đối thủ & thị trường**: So sánh **giá cả, tính năng, đánh giá** của đối thủ chỉ với **một cú nhấp chuột**.
- **Kết hợp với Slack/Telegram**: Nhận **báo cáo tự động** mỗi khi có dữ liệu mới.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Firecrawl**:
   - Đăng ký tại **[firecrawl.dev](https://www.firecrawl.dev)** và lấy **API Key**.
   - Cài đặt **n8n-node-firecrawl** (nếu chưa có) từ **[n8n Community](https://flows.n8n.io/)**.

2. **API Key cho OpenRouter (hoặc LLM khác)**:
   - Đăng ký tại **[OpenRouter](https://openrouter.ai/)** và lấy **API Key**.
   - Chọn **mô hình AI** (được workflow sử dụng mặc định là **Claude Sonnet** và **Claude Haiku** của Anthropic).

3. **N8n Self-Hosted**:
   - Cài đặt n8n trên **VPS** (không dùng phiên bản cloud để tránh giới hạn).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ **[n8n.io/workflows/14167](https://n8n.io/workflows/14167)**.
- **Mở n8n Editor** → **Import Workflow** → Chọn file JSON đã tải.
- **Hoặc copy/paste** JSON từ file vào **Import Workflow**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này **không hoạt động ngay lập tức** vì cần cấu hình **credentials** và **tham số**. Dưới đây là **các bước chi tiết**:

##### **A. Cấu hình Firecrawl API**
- **Tất cả các node Firecrawl** (trong danh sách trên) **cần sử dụng credential `firecrawlApi`**.
- **Cách thiết lập**:
  1. Vào **Credentials** (phía trên bên trái n8n Editor).
  2. Nhấn **+ Add** → Chọn **Firecrawl API**.
  3. Điền:
     - **API Key**: Copy từ tài khoản Firecrawl.
     - **Base URL**: `https://api.firecrawl.dev/v1` (mặc định).
  4. Lưu và **lặp lại cho tất cả các node Firecrawl** (nếu workflow có nhiều credential).

##### **B. Cấu hình OpenRouter API**
- **3 node LLM** (`Primary Chat Model`, `Fallback Chat Model`, `Parser Chat Model`) **cần credential `openRouterApi`**.
- **Cách thiết lập**:
  1. Vào **Credentials** → **+ Add** → Chọn **OpenRouter API**.
  2. Điền:
     - **API Key**: Copy từ OpenRouter.
     - **Base URL**: `https://openrouter.ai/api/v1` (mặc định).
  3. **Không cần thay đổi model** (workflow đã cấu hình mặc định là **Claude Sonnet** và **Claude Haiku**).

##### **C. Cấu hình Webhook**
- Node **`Receive Scrape Request`** sử dụng **path `scrape-agent`** và **HTTP Method POST**.
- **Không cần thay đổi** (n8n sẽ tự động tạo URL webhook khi workflow được kích hoạt).

##### **D. Node Code (`Validate Output Schema`)**
- Node này **kiểm tra schema JSON** nhập vào.
- **Không cần chỉnh sửa** (n8n sẽ tự động sử dụng schema mặc định nếu không có).

##### **E. Node Agent (`Research & Extract Web Data`)**
- Node này **tự động scrape, search và xử lý dữ liệu** dựa trên **prompt** và **schema**.
- **Không cần cấu hình thêm**, chỉ cần **gửi yêu cầu POST** với `prompt` và `output_schema` (nếu có).

---

#### **3. Kích hoạt ⚡️**
1. **Test Run** (nếu muốn kiểm tra trước khi kích hoạt):
   - Nhấn **Run Workflow** và gửi **dữ liệu mẫu** (ví dụ:
     ```json
     {
       "prompt": "Tìm kiếm thông tin về sản phẩm iPhone 15 Pro Max của Apple, bao gồm giá cả, tính năng và đánh giá từ các trang tin tức uy tín.",
       "output_schema": {
         "type": "object",
         "properties": {
           "product_name": { "type": "string" },
           "price": { "type": "number" },
           "features": { "type": "array", "items": { "type": "string" } },
           "reviews": { "type": "array", "items": { "type": "string" } }
         }
       }
     }
     ```
   )
2. **Kích hoạt Workflow**:
   - Đánh dấu **Active** (ô vuông bên cạnh tên workflow).
   - **Copy Webhook URL** (sử dụng để gửi yêu cầu POST).

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Slack/Telegram**:
   - Sử dụng **n8n-node-slack** hoặc **n8n-node-telegram** để **báo cáo kết quả tự động** khi workflow hoàn thành.
   - Ví dụ: Sau khi **`Return Structured Results`**, thêm node **Slack Webhook** để gửi tin nhắn thông báo.

2. **Lưu log dữ liệu**:
   - Thêm **n8n-node-google-sheets** hoặc **n8n-node-database** để **lưu trữ lịch sử scrape**.
   - Có thể **tạo báo cáo định kỳ** (hàng tuần) bằng **n8n-node-email**.

3. **Tối ưu hóa prompt**:
   - Nếu kết quả không chính xác, **cập nhật `prompt`** để rõ ràng hơn.
   - Ví dụ:
     ```json
     {
       "prompt": "Tìm kiếm và so sánh giá cả của iPhone 15 Pro Max tại Việt Nam từ các trang thương mại điện tử lớn như Shopee, Lazada, Tiki trong 30 ngày qua.",
       "output_schema": {
         "type": "object",
         "properties": {
           "products": {
             "type": "array",
             "items": {
               "type": "object",
               "properties": {
                 "name": { "type": "string" },
                 "price": { "type": "number" },
                 "platform": { "type": "string" },
                 "last_updated": { "type": "string", "format": "date-time" }
               }
             }
           }
         }
       }
     }
     ```

4. **Sử dụng nhiều browser session**:
   - Nếu cần **scrape nhiều trang cùng lúc**, có thể **tạo nhiều session browser** và **quản lý bằng node `List browser sessions`**.

---

### 📌 **Kết luận**
Workflow này **không chỉ tiết kiệm thời gian**, mà còn **mang lại dữ liệu chính xác, cấu trúc và tự động hóa hoàn toàn** cho các công việc nghiên cứu thị trường, phân tích đối thủ và thu thập dữ liệu web.

**Hành động ngay!**
1. **Cài đặt n8n trên VPS** (để workflow hoạt động 24/7).
2. **Import workflow** và **cấu hình credentials**.
3. **Test với một yêu cầu scrape** và **nhận kết quả trong vài giây!**

👉 **[Tải workflow ngay](https://n8n.io/workflows/14167)** và **bắt đầu tự động hóa ngay hôm nay!**

---
**Chia sẻ ý kiến hoặc gặp vấn đề?** Đăng câu hỏi tại **[n8n Community](https://community.n8n.io/)** hoặc liên hệ với Firecrawl tại **[firecrawl.dev](https://www.firecrawl.dev)**.