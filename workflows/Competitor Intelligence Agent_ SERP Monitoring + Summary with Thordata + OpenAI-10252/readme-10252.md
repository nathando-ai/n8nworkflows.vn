---
title: "🔍 **AI Agent Tự Động Phân Tích SERP Thông Minh: Theo Dõi Thay Đổi Của Hàng Xóm SEO + Tóm Tắt Bằng OpenAI**"
description: "Workflow tự động hóa 100% không code giúp các sếp SEO theo dõi hàng tuần top 10 kết quả Google/Bing/Yandex của đối thủ, phân tích keyword gap, điểm mạnh/điểm yếu SEO, và tự động tóm tắt báo cáo bằng AI GPT-4.1-mini. Giúp tiết kiệm 10+ giờ/tháng và phát hiện cơ hội mới chỉ trong vài giây."
slug: "ai-agent-serp-monitoring-thordata-openai"
tags: [n8n, automation, seo, ai-summarization, market-research, thordata, openai]
keywords: [tự động hóa phân tích serp, ai agent serp, theo dõi đối thủ seo, keyword gap analyzer, openai seo analysis, workflow n8n seo]
---

# 🚀 **AI Agent Tự Động Phân Tích SERP: Theo Dõi Đối Thủ SEO & Tóm Tắt Báo Cáo Bằng AI**

## **Nỗi Đau Của Các Sếp SEO Hiện Nay**
Hàng tuần, các sếp SEO phải:
- **Tìm kiếm thủ công** top 10 kết quả Google/Bing/Yandex của đối thủ trên **5-10 keyword chính**.
- **So sánh thủ công** vị trí xếp hạng, backlink, và nội dung của đối thủ.
- **Phân tích keyword gap** bằng công cụ như Ahrefs/SEMrush (tốn tiền).
- **Tóm tắt báo cáo** bằng Excel hoặc Google Sheets (tốn thời gian).
- **Chỉnh sửa nội dung** dựa trên dữ liệu thu thập (rất dễ quên hoặc sai sót).

**Kết quả?** Thời gian mất **10-15 giờ/tuần**, dễ bị lỗi nhân sự, và **chỉ phát hiện ra 30% cơ hội** so với đối thủ.

---
### **🎯 Giải Pháp: AI Agent SERP Monitoring + OpenAI**
Workflow này **tự động hóa toàn bộ quy trình** bằng cách:
✅ **Lấy dữ liệu SERP** từ **Google, Bing, Yandex, DuckDuckGo** (thông qua API).
✅ **Phân tích AI** top 10 kết quả để trích xuất:
   - **Domain authority** (tương tự Domain Rating của Ahrefs).
   - **Keyword ranking** (vị trí hiện tại của đối thủ).
   - **Content gap** (những chủ đề đối thủ có mà bạn thiếu).
   - **SEO Strength Score** (điểm từ 0-100).
✅ **Tóm tắt báo cáo** bằng **GPT-4.1-mini** (OpenAI) với **cấu trúc JSON chuẩn**.
✅ **Xuất dữ liệu** tự động vào **Google Sheets** để theo dõi lịch sử.

**Kết quả?** Các sếp chỉ cần **nhấn 1 nút** và nhận báo cáo **cập nhật hàng tuần**, tiết kiệm **90% thời gian** so với cách làm thủ công.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[**3 Lợi Ích Cốt Lõi**]
- **Tiết kiệm 10+ giờ/tháng** so với cách làm thủ công.
- **Phát hiện keyword gap** chỉ trong vài giây (không cần Ahrefs/SEMrush).
- **Báo cáo tự động** với **AI tóm tắt** (không cần viết Excel).
- **Theo dõi đối thủ 24/7** (không phụ thuộc vào nhân viên).
- **Cập nhật liên tục** (không cần update thủ công).
:::

---
### **🔧 Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI SỬ DỤNG**]
Để workflow hoạt động, các sếp cần:
1. **Tài khoản API SERP**:
   - **Thordata API** (đăng ký tại [thordata.com](https://thordata.com/)) với **API Key**.
   - *Lưu ý*: Workflow gốc sử dụng **HTTP Bearer Auth** cho các engine search (Google/Bing/Yandex/DuckDuckGo), nhưng **Thordata là giải pháp tối ưu** vì:
     - **Dữ liệu chính xác** (không bị chặn IP).
     - **Tốc độ nhanh** (phù hợp với AI).
     - **Giá hợp lý** (~$20/tháng cho 1000 request).

2. **Tài khoản OpenAI**:
   - **API Key** từ [OpenAI](https://platform.openai.com/) (đăng ký miễn phí).
   - **Model**: `gpt-4.1-mini` (được cấu hình sẵn trong workflow).

3. **Google Sheets**:
   - **File Google Sheets** để lưu kết quả (cấu trúc sheet sẽ được tự động tạo).
   - **OAuth 2.0 Credentials** cho Google Sheets (cài đặt trong n8n).

4. **N8n Self-Hosted**:
   - Workflow này **phải chạy 24/7** để theo dõi SERP hàng tuần.
   - **Không khuyến cáo** sử dụng n8n Cloud (do giới hạn request API).
   - 👉 **Đăng ký VPS TinoHost** (Self-hosted) với mã giảm giá **VPSN8N** (giảm 39%):
     - [VPS Xeon 4GB chỉ 50k/tháng](https://tino.vn/vps-n8n?affid=388)
     - [Hướng dẫn cài n8n trên VPS](https://docs.n8n.io/hosting/self-hosting-on-a-vps/)
:::

---
## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/10252](https://n8n.io/workflows/10252) (chọn **Export JSON**).
2. **Mở n8n Editor** (trên VPS hoặc n8n Cloud).
3. **Nhấn "Import"** và chọn file JSON vừa tải.
4. **Chọn "Create new workflow"** và đặt tên (ví dụ: **"AI SERP Monitor"**).

#### **Phương pháp 2: Copy/Paste JSON**
1. **Copy toàn bộ mã JSON** từ [n8n.io/workflows/10252](https://n8n.io/workflows/10252).
2. **Mở n8n Editor** → **Create new workflow** → **Paste JSON**.
3. **Nhấn "Import"** và tiếp tục cấu hình.

---
### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này **không hoạt động ngay** sau khi import. Các sếp cần **cấu hình chi tiết** các node sau:

#### **🔹 Node 1: "When clicking ‘Execute workflow’" (Manual Trigger)**
- **Không cần chỉnh gì**, nhưng để **tự động hóa hàng tuần**, các sếp nên:
  - **Thay bằng "Schedule Node"** (n8n-nodes-base.schedule).
  - **Cấu hình**: Chạy **mỗi thứ 2 hàng tuần** (hoặc tùy chọn của các sếp).
  - *Hướng dẫn*: [Schedule Node Documentation](https://docs.n8n.io/integrations/builtins/nodes/Base/Schedule/)

#### **🔹 Node 2: "Set the Input Fields" (Set Node)**
- **Thêm các tham số cần thiết**:
  - **Keyword 1**: `keyword1` (ví dụ: "tự động hóa n8n")
  - **Keyword 2**: `keyword2` (ví dụ: "seo tự động")
  - **Domain Competitor**: `competitorDomain` (ví dụ: `ahrefs.com`)
  - **Country**: `country` (ví dụ: `US` hoặc `VN`)
  - **Search Engine**: `engine` (lựa chọn: `google`, `bing`, `yandex`, `duckduckgo`)

#### **🔹 Node 3: "Bing Search / Google Search / Yandex Search / DuckDuckGo Search" (HTTP Request Tool)**
- **Thay thế bằng API Thordata** (không sử dụng HTTP Bearer Auth):
  1. **Xóa tất cả node HTTP Request Tool** (Google/Bing/Yandex/DuckDuckGo).
  2. **Thêm node "HTTP Request"** mới (n8n-nodes-base.httpRequest).
  3. **Cấu hình**:
     - **Method**: `POST`
     - **URL**: `https://api.thordata.com/v1/search`
     - **Headers**:
       ```json
       {
         "Authorization": "Bearer YOUR_THORDATA_API_KEY",
         "Content-Type": "application/json"
       }
       ```
     - **Body**:
       ```json
       {
         "query": "{{ $node["Set the Input Fields"].json["keyword1"] }}",
         "country": "{{ $node["Set the Input Fields"].json["country"] }}",
         "engine": "google",
         "limit": 10
       }
       ```
  4. **Lặp lại cho từng engine** (Google, Bing, Yandex, DuckDuckGo).

#### **🔹 Node 4: "OpenAI Chat Model" (lmChatOpenAi)**
- **Không cần chỉnh gì**, nhưng **đảm bảo**:
  - **API Key** đã được thêm trong **Credentials** (n8n → Credentials → Add → OpenAI).
  - **Model**: `gpt-4.1-mini` (được cấu hình sẵn).

#### **🔹 Node 5: "Append or update row in sheet" (Google Sheets)**
- **Chọn sheet và range**:
  - **Sheet Name**: `SERP_Analysis` (hoặc tùy chỉnh).
  - **Range**: `A1` (n8n sẽ tự động tạo header).
- **Cấu hình "Operation"**: `appendOrUpdate` (đã có sẵn).

#### **🔹 Node 6: "Merge" (Merge Node)**
- **Không cần chỉnh gì**, nhưng **đảm bảo**:
  - **Input**: Liên kết từ **AI Agent** và **Google Sheets**.

---
### **3. Kích Hoạt ⚡️**
1. **Test Run với dữ liệu mẫu**:
   - Điền vào **Set the Input Fields**:
     - `keyword1`: `tự động hóa n8n`
     - `competitorDomain`: `ahrefs.com`
     - `country`: `US`
   - **Nhấn "Execute"** và kiểm tra kết quả:
     - **AI Agent** nên trả về **JSON** với:
       ```json
       {
         "competitorDomains": ["ahrefs.com", "semrush.com"],
         "rankingPositions": { "ahrefs.com": 1 },
         "keywordGaps": ["n8n automation", "seo automation"],
         "seoStrengthScore": 85,
         "summary": "Ahrefs đang dẫn đầu về keyword 'tự động hóa n8n'..."
       }
       ```
2. **Bật Active**:
   - Sau khi test thành công, **nhấn "Active"** để workflow chạy tự động.

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**
### **1. Tự Động Hóa Hàng Tuần (Schedule)**
- Thay **Manual Trigger** bằng **Schedule Node**:
  ```yaml
  - node:
      id: "schedule"
      type: "n8n-nodes-base.schedule"
      parameters:
        cron: "0 0 * * 2"  # Chạy mỗi thứ 2 hàng tuần lúc 00:00
  ```
- *Hướng dẫn*: [n8n Schedule Node](https://docs.n8n.io/integrations/builtins/nodes/Base/Schedule/)

### **2. Gửi Báo Cáo Sang Slack/Telegram**
- **Thêm node "Webhook"** (n8n-nodes-base.httpRequest) để gửi kết quả:
  ```json
  {
    "text": "🚀 **Báo cáo SERP mới** đã hoàn thành!\n\n{{ $node["Merge"].json }}"
  }
  ```
- **Kết nối với Slack/Telegram** bằng **Incoming Webhook**.

### **3. Lưu Log Lịch Sử**
- **Thêm node "Set"** trước **Google Sheets** để lưu thêm metadata:
  ```json
  {
    "timestamp": "{{ $node["Schedule"].json["date"] }}",
    "status": "completed"
  }
  ```
- **Xuất vào Google Sheets** cùng với dữ liệu SERP.

### **4. Phân Tích Keyword Cụ Thể**
- **Thêm node "Information Extractor"** để phân tích **keyword long-tail**:
  ```json
  {
    "prompt": "Extract all long-tail keywords from the following SERP results: {{ $node["AI Agent"].json }}"
  }
  ```

---
## **📌 Kết Luận**
Workflow **AI Agent SERP Monitoring** là **giải pháp hoàn hảo** cho các sếp SEO muốn:
✔ **Tiết kiệm thời gian** (không cần làm thủ công).
✔ **Phát hiện keyword gap** chỉ trong vài giây.
✔ **Tự động hóa báo cáo** bằng AI.
✔ **Theo dõi đối thủ 24/7** (không phụ thuộc vào nhân viên).

**Bước đầu tiên?** **Import workflow, cấu hình API Thordata + OpenAI, và bật Schedule Node!**
👉 **Đăng ký VPS TinoHost** để chạy workflow 24/7:
[VPS Xeon 4GB chỉ 50k/tháng](https://tino.vn/vps-n8n?affid=388)

---
### **💡 Câu Hỏi Thường Gặp**
#### **1. Tại sao không dùng API Google/Bing miễn phí?**
- **Google/Bing API miễn phí** (CSE) **không ổn định** (bị chặn IP, giới hạn request).
- **Thordata** là giải pháp **chính xác, nhanh chóng, và giá hợp lý**.

#### **2. Có thể chạy workflow trên n8n Cloud không?**
- **Không khuyến cáo**, vì:
  - **Giới hạn request API** (Thordata/OpenAI).
  - **Không tự động hóa được** (cần Manual Trigger).
- **Lựa chọn tốt nhất**: **Self-hosted trên VPS** (TinoHost).

#### **3. Có thể thêm engine search khác không?**
- **Có**, chỉ cần thêm **node HTTP Request** mới với URL API của engine mới (ví dụ: Baidu, Naver).

#### **4. Làm sao để AI tóm tắt báo cáo chi tiết hơn?**
- **Cập nhật Prompt** trong node **chainLlm**:
  ```json
  {
    "prompt": "Tóm tắt chi tiết về SERP của {{ $node