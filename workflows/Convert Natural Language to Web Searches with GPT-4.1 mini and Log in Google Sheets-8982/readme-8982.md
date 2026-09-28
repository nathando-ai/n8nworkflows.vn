---
title: "🔍 Tự Động Hóa Tìm Kiếm Web Bằng GPT-4.1 Mini + Log Lịch Sử Tìm Kiếm Trên Google Sheets"
description: "Workflow tự động hóa chuyển đổi yêu cầu tìm kiếm bằng ngôn ngữ tự nhiên thành các query chuyên nghiệp, thực hiện tìm kiếm đa dạng trên Firecrawl và lưu kết quả vào Google Sheets. Giúp tiết kiệm thời gian lên đến 80% cho công việc nghiên cứu nội dung và SEO."
slug: "tieu-dong-hoa-tim-kiem-web-bang-gpt-4-1-mini"
tags: [n8n, automation, ai, content-creation, seo, google-sheets, openrouter, firecrawl]
keywords: [n8n workflow tìm kiếm web, tự động hóa tìm kiếm bằng GPT-4, lưu lịch sử tìm kiếm Google Sheets, công cụ nghiên cứu SEO tự động, AI tìm kiếm đa dạng]
---

# 🚀 Tự Động Hóa Tìm Kiếm Web Bằng GPT-4.1 Mini + Log Lịch Sử Trên Google Sheets

### 📌 **Nỗi Đau Của Các Sếp**
Các sếp thường phải mất **giờ đồng hồ** để:
- **Nhập thủ công** các query tìm kiếm phức tạp trên Google, Bing hay các công cụ chuyên dụng như Firecrawl.
- **Lặp đi lặp lại** các từ khóa liên quan để đảm bảo không bỏ sót thông tin quan trọng.
- **Lưu trữ kết quả** một cách rối ren, không thể theo dõi lịch sử tìm kiếm trong tương lai.
- **Phân tích không đầy đủ** do chỉ dựa vào kết quả từ một góc độ duy nhất.

**Workflow này giải quyết tất cả đó bằng cách:**
✅ **Chuyển đổi yêu cầu ngôn ngữ tự nhiên** thành các query tìm kiếm chuyên nghiệp (ví dụ: `"Tìm kiếm về Nate Herk trên Geeky Gadgets"` → `nate herk site:geeky-gadgets.com`).
✅ **Thực hiện tìm kiếm song song** trên nhiều facet (trang web, URL, từ khóa trừ, YouTube...) để **tăng độ phủ** và tránh bỏ sót.
✅ **Lưu tất cả kết quả** vào **Google Sheets** với định dạng rõ ràng (tiêu đề, URL, snippet, screenshot).
✅ **Trả về kết quả ngay lập tức** cho người dùng qua Webhook, giúp **tiết kiệm thời gian lên đến 80%** so với cách làm thủ công.

---

## 🎯 Kết Quả Các Sếp Nhận Được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Thay vì mất 30 phút để tìm kiếm thủ công, chỉ cần **nhập yêu cầu bằng tiếng Việt** và workflow sẽ xử lý trong giây lát.
- **Tìm kiếm toàn diện**: **4 facet tìm kiếm song song** (trang web, URL, từ khóa trừ, YouTube) đảm bảo không bỏ sót bất kỳ thông tin nào.
- **Lưu trữ chuyên nghiệp**: Tất cả kết quả được **ghi vào Google Sheets** với định dạng chuẩn, dễ dàng phân tích sau này.
- **Hoạt động 24/7**: Cài đặt trên **VPS tự host**, workflow chạy liên tục mà không cần can thiệp.
- **Cá nhân hóa**: Dễ dàng **mở rộng** cho nhiều dự án khác nhau bằng cách thay đổi query mặc định.
:::

---

## 🔧 Yêu Cầu Cần Thiết

:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản OpenRouter API**:
   - Đăng ký tại [OpenRouter](https://openrouter.ai/) và lấy **API Key** (sử dụng cho GPT-4.1 mini).
   - **Mô hình khuyến nghị**: `openrouter/gpt-4.1-mini` (giá rẻ và hiệu quả).
   - **Ngân sách**: ~$0.0005/1K tokens (phù hợp cho tìm kiếm).

2. **Tài khoản Google Sheets**:
   - **Bảng tính** đã sẵn sàng để lưu kết quả (các sếp có thể tạo mới hoặc chọn bảng đã có).
   - **Quản lý quyền**: Cung cấp **OAuth 2.0 API Key** cho n8n truy cập.

3. **Tài khoản Firecrawl API** (miễn phí):
   - Đăng ký tại [Firecrawl](https://www.firecrawl.ai/) để lấy **API Key** (dùng cho tìm kiếm web).
   - **Lưu ý**: Firecrawl có giới hạn miễn phí (500 credit/tháng), phù hợp cho thử nghiệm.

4. **VPS tự host n8n** (khuyến nghị):
   - Để workflow chạy **liên tục 24/7**, các sếp nên cài đặt n8n trên **VPS** thay vì phiên bản cloud.
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).

5. **Webhook URL** (của ứng dụng hoặc chatbot):
   - Để nhận yêu cầu tìm kiếm từ người dùng (ví dụ: Slack, Telegram, hoặc một trang web cá nhân).
---

## 🚀 Cách Import & Lưu Ý Khi "Lên Đồ"

### 1. Import Workflow 📥
#### **Cách 1: Từ File JSON**
1. Tải workflow từ [n8n.io/workflows/8982](https://n8n.io/workflows/8982) (ấn **Export**).
2. Trong **n8n Editor**, nhấn **Import** và chọn file JSON tải xuống.
3. Chọn **Create new workflow** và nhấn **Import**.

#### **Cách 2: Copy/Paste JSON**
1. Mở **n8n Editor** và tạo workflow mới.
2. Nhấn **Import** → **Paste JSON** và dán nội dung từ [n8n.io/workflows/8982](https://n8n.io/workflows/8982) (ấn **Export** → **Copy JSON**).
3. Chọn **Create new workflow** và nhấn **Import**.

---

### 2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌

#### **A. Cấu Hình Credentials**
| Node               | Tham Số Cần Chỉnh                          | Hướng Dẫn                          |
|--------------------|--------------------------------------------|-------------------------------------|
| **GPT 4.1 mini**   | `openRouterApi` (API Key OpenRouter)       | Điền vào **Credentials** của node.  |
| **Google Sheets**  | `googleSheetsOAuth2Api` (OAuth 2.0)        | Tạo **OAuth 2.0 Credential** trong n8n và liên kết với Google Sheets. |
| **Firecrawl Search**| API Key Firecrawl                          | Điền vào **Headers** của node (`Authorization: Bearer YOUR_API_KEY`). |

#### **B. Cấu Hình Query Mặc Định (STEP 3)**
Workflow mặc định sử dụng các query cho **"Nate Herk"**, nhưng các sếp có thể **thay đổi** để phù hợp với dự án:
- **Site**: `nate herk site:DOMAIN.com` (ví dụ: `geeky-gadgets.com`).
- **In URL**: `nate herk inurl:KEYWORD` (ví dụ: `skool`).
- **Exclusion**: `nate herk -inurl:KEYWORD` (loại trừ kết quả không mong muốn).
- **Pro (YouTube)**: `Nate Herk site:youtube.com -shorts intitle:KEYWORD` (ví dụ: `automation`).

**Cách thay đổi**:
1. Mở node **Search Agent** → **Configuration**.
2. Thay đổi **Prompt** để điều chỉnh query mặc định:
   ```json
   "prompt": "Tìm kiếm về {query} trên các facet sau:\n1. Trang web chính thức: site:{query} site:DOMAIN.com\n2. URL chứa từ khóa: inurl:{query} inurl:KEYWORD\n3. Loại trừ URL cụ thể: {query} -inurl:KEYWORD\n4. YouTube (không phải shorts): {query} site:youtube.com -shorts intitle:{query}"
   ```

#### **C. Cấu Hình Google Sheets**
1. Mở node **Append row in sheet**.
2. Chọn **Google Sheets Credential** đã tạo.
3. Điền **Sheet Name** (tên bảng tính) và **Range** (ví dụ: `Sheet1!A1`).
4. **Bật "Append"** để thêm dữ liệu vào cuối bảng.

#### **D. Webhook URL**
1. Mở node **Webhook** và kiểm tra **Key Parameters**:
   - `path`: `0d916768-023f-4d0e-8b76-4cbd5ffa07ee` (có thể thay đổi nếu cần).
2. **Lưu ý**: Các sếp phải cung cấp **URL Webhook** này cho ứng dụng/chatbot để gửi yêu cầu tìm kiếm.

---

### 3. Kích Hoạt ⚡️
1. **Test Run** với dữ liệu mẫu:
   - Gửi yêu cầu tìm kiếm qua Webhook (ví dụ: từ Postman hoặc Slack).
   - Kiểm tra kết quả trong **Google Sheets** và **Respond to Webhook**.
2. **Bật Active**:
   - Nhấn **Active** trên workflow trong n8n Editor.

---

## ✍️ Mẹo & Gợi Ý Nâng Cao

### 1. Kết Nối Với Slack/Telegram
- Sử dụng **node Slack** hoặc **Telegram Bot** để người dùng gửi yêu cầu tìm kiếm qua chat.
- **Cách làm**:
  1. Thêm node **Slack** (hoặc **Telegram**) trước **Webhook**.
  2. Cấu hình **Webhook URL** của node Slack/Telegram để trỏ đến Webhook trong workflow.

### 2. Lưu Log Tìm Kiếm
- Thêm node **HTTP Request** để gửi kết quả đến **Google Drive** hoặc **Notion** để lưu trữ lâu dài.
- **Cách làm**:
  1. Thêm node **HTTP Request** sau **Respond to Webhook**.
  2. Gửi dữ liệu JSON đến API của Google Drive/Notion để lưu log.

### 3. Báo Cáo Định Kỳ
- Sử dụng **node Schedule** (n8n Pro) để chạy workflow hàng ngày/tuần và gửi báo cáo qua email.
- **Cách làm**:
  1. Thêm node **Schedule** (n8n Pro) và cấu hình lịch chạy.
  2. Sử dụng node **Email** (n8n-nodes-base.email) để gửi báo cáo.

### 4. Tối Ưu Hóa Query
- **Thêm từ khóa liên quan** vào prompt để tăng độ chính xác.
- **Ví dụ**:
  ```json
  "prompt": "Tìm kiếm về {query} và các từ khóa liên quan như: SEO, automation, tech news, {query} tutorial."
  ```

### 5. Sử Dụng Mô Hình GPT Lớn Khác
- Thay thế **GPT-4.1 mini** bằng **GPT-4** (nếu ngân sách cho phép) để tăng độ chính xác.
- **Cách làm**:
  1. Mở node **GPT 4.1 mini** → **Configuration**.
  2. Thay đổi mô hình thành `openrouter/gpt-4` (nếu có API Key cho mô hình này).

---

## 📌 Kết Luận

Workflow này là **giải pháp hoàn hảo** cho các sếp cần:
✔ **Tìm kiếm web tự động** từ yêu cầu ngôn ngữ tự nhiên.
✔ **Lưu trữ kết quả** một cách chuyên nghiệp trên Google Sheets.
✔ **Tiết kiệm thời gian** và tăng hiệu suất nghiên cứu nội dung/SEO.

**Hành động ngay hôm nay**:
1. **Cài đặt n8n trên VPS** (khuyến nghị) và import workflow.
2. **Cấu hình credentials** (OpenRouter, Google Sheets, Firecrawl).
3. **Test với yêu cầu tìm kiếm đầu tiên** và theo dõi kết quả!

**🚀 Cài đặt ngay và tự động hóa công việc tìm kiếm của mình!** 🚀