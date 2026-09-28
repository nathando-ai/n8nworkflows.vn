---
title: "🚀 **Tự Động Hóa Theo Dõi Tin Tức Solana Hàng Ngày + Tóm Tắt Tuần Bằng GPT-4.1-mini (Google Sheets)**"
description: "Workflow tự động hóa thu thập tin tức Solana từ CryptoPanic API, loại bỏ trùng lặp, và tạo tóm tắt tuần bằng GPT-4.1-mini, lưu kết quả vào Google Sheets. Giúp các sếp tiết kiệm thời gian theo dõi thị trường crypto và nắm bắt xu hướng nhanh chóng."
slug: "tự-dộng-hoa-theo-doi-tin-tuc-solana-gpt-4-1-mini"
tags: [n8n, automation, crypto, no-code, google-sheets, ai, openai, gpt-4]
keywords: [n8n workflow crypto, tự động hóa tin tức Solana, GPT-4.1-mini tóm tắt tuần, Google Sheets tự động, CryptoPanic API, tự động hóa no-code]
---

# 🚀 **Tự Động Hóa Theo Dõi Tin Tức Solana Hàng Ngày + Tóm Tắt Tuần Bằng GPT-4.1-mini**

### **Giải pháp cho các sếp muốn theo dõi thị trường Solana một cách thông minh, không cần code**
Theo dõi tin tức Solana thủ công là một công việc tốn thời gian và dễ bỏ lỡ thông tin quan trọng. Các sếp phải:
- **Lọc qua hàng trăm bài viết** trên các nguồn tin khác nhau.
- **Loại bỏ trùng lặp** và bài viết không liên quan.
- **Tóm tắt tuần** để nắm bắt xu hướng thị trường một cách nhanh chóng.
- **Lưu trữ dữ liệu** một cách có hệ thống.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động thu thập tin tức Solana** từ CryptoPanic API (hoặc các API khác).
✅ **Loại bỏ tin tức trùng lặp** và bài viết không hợp lệ.
✅ **Tóm tắt tuần bằng GPT-4.1-mini** (chi phí thấp, hiệu quả cao).
✅ **Lưu kết quả vào Google Sheets** để theo dõi dài hạn.
✅ **Hoạt động tự động hàng ngày** (không cần can thiệp).

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần thủ công lọc tin tức hàng ngày.
- **Chính xác và toàn diện**: Lấy dữ liệu từ nguồn tin uy tín (CryptoPanic).
- **Tóm tắt tuần tự động**: GPT-4.1-mini phân tích và tổng hợp tin tức một cách logic.
- **Lưu trữ dài hạn**: Dữ liệu được lưu vào Google Sheets, dễ dàng theo dõi lịch sử.
- **Chi phí thấp**: ~$0.05/tháng (OpenAI) + API miễn phí (CryptoPanic).
- **Hoạt động liên tục**: Workflow chạy tự động hàng ngày vào 8h sáng (theo giờ PT).
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **API Key CryptoPanic**:
   - Đăng ký miễn phí tại [CryptoPanic](https://cryptopanic.com/).
   - Thay thế `[your token]` trong node **"Get Solana News"** bằng API key của mình.
   *(Lưu ý: CryptoPanic có giới hạn request, nếu quá tải, có thể thay thế bằng CoinGecko hoặc NewsAPI).*

2. **Google Sheets**:
   - Tạo **1 file Google Sheets** với **2 sheet**:
     - **Sheet 1**: "Raw Data" (cột: `date`, `title`, `description`).
     - **Sheet 2**: "Weekly Summary" (cột: `Date`, `Summary`).
   - Cấu hình **Google Sheets credential** trong n8n (cài đặt trong `Credentials` → `Add Credential` → `Google Sheets`).

3. **OpenAI API Key**:
   - Đăng ký tài khoản tại [OpenAI](https://platform.openai.com/).
   - Thêm **API Key** trong `Credentials` → `Add Credential` → `OpenAI`.
   - Chọn mô hình **GPT-4.1-mini** (rẻ và hiệu quả).

4. **n8n Workspace**:
   - Nếu chưa có, tạo **n8n Workspace** (self-hosted hoặc dùng phiên bản cloud miễn phí).
   - Cài đặt **nodes mở rộng**:
     - `@n8n/n8n-nodes-langchain` (để sử dụng OpenAI).
     - Các node cơ bản (`n8n-nodes-base` đã có sẵn).
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải workflow JSON**:
  - Tải file JSON từ [link gốc](https://n8n.io/workflows/9874) hoặc copy toàn bộ JSON từ trang này.
- **Import vào n8n Editor**:
  - Mở **n8n Editor** → Nhấn `Import` → Chọn file JSON hoặc dán JSON vào ô `Paste JSON`.
  - Nhấn `Import` để workflow xuất hiện trên canvas.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **12 node**, các sếp cần chú ý cấu hình sau:

##### **🔹 Node "Get Solana News" (HTTP Request)**
- **URL**: `https://cryptopanic.com/api/v1/sources/news/?token=[your token]&category=solana`
  *(Thay `[your token]` bằng API key CryptoPanic của mình).*
- **Headers**:
  - `Accept`: `application/json`
- **Method**: `GET`
- **Response Format**: `JSON`

##### **🔹 Node "Check For Duplicates" (Google Sheets)**
- **Sheet Name**: `"Raw Data"`
- **Range**: `"A2:B"` (cột `date` và `title` để kiểm tra trùng lặp).
- **Query**: `=ARRAYFORMULA(IF(COUNTIF(A2:A, A2)>1, TRUE, FALSE))` (để tìm trùng lặp).
- **Lưu ý**: Nếu sheet chưa có dữ liệu, node này sẽ không hoạt động. Các sếp cần **chạy test run** sau khi import.

##### **🔹 Node "Summarize News" (OpenAI)**
- **Model**: `gpt-4-1106-preview` (hoặc `gpt-4.1-mini` nếu có sẵn).
- **Prompt**:
  ```plaintext
  You are an expert crypto analyst. Summarize the following Solana news articles into a concise 2-3 sentence factual summary, followed by 1-2 key investor takeaways.

  Articles:
  {{ $json["items"].map(item => `- ${item.title}: ${item.description}`).join("\n") }}

  Summary:
  ```
- **Temperature**: `0.7` (để kết quả logic hơn).
- **Max Tokens**: `200` (đủ để tóm tắt tuần).
- **Cost**: ~$0.001/summary (rẻ và hiệu quả).

##### **🔹 Node "Append Summary" (Google Sheets)**
- **Sheet Name**: `"Weekly Summary"`
- **Range**: `"A2"` (để append vào dòng mới).
- **Columns**:
  - `Date`: `{{ $node["Process If Monday"]["json"]["date"] }}` (định dạng `dd/MM/yyyy`).
  - `Summary`: `{{ $node["Summarize News"]["json"]["choices"][0]["message"]["content"] }}`.

##### **🔹 Node "Process If Monday" (If)**
- **Condition**: `{{ $node["Schedule Trigger"]["json"]["date"].split('-')[2] === "1" }}` (kiểm tra ngày là thứ 2, tức là tóm tắt tuần kết thúc vào thứ 2).
- **Lưu ý**: Workflow chạy hàng ngày, nhưng **chỉ tóm tắt vào thứ 2** (để tổng hợp tuần trước).

##### **🔹 Node "Schedule Trigger" (Schedule Trigger)**
- **Time**: `08:00 PT` (8h sáng theo giờ Pacific Time).
- **Time Zone**: `America/Los_Angeles` (hoặc điều chỉnh theo giờ của mình).

---
#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Nhấn `Run Workflow` để kiểm tra từng node.
   - Kiểm tra **Google Sheets** để đảm bảo dữ liệu được append đúng.
   - Kiểm tra **OpenAI response** để đảm bảo tóm tắt logic.

2. **Active Workflow**:
   - Sau khi test thành công, nhấn `Active` để workflow chạy tự động hàng ngày.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Thay thế CryptoPanic bằng API khác**:
   - Nếu CryptoPanic bị giới hạn request, có thể sử dụng **CoinGecko API** hoặc **NewsAPI**.
   - Ví dụ với **CoinGecko**:
     ```plaintext
     https://api.coingecko.com/api/v3/search/news?category=solana
     ```

2. **Lưu log hoạt động**:
   - Thêm node **Slack/Telegram** để thông báo khi workflow chạy thành công/thất bại.
   - Ví dụ:
     ```javascript
     // Node Code (Slack Notification)
     return {
       text: `📢 Solana News Summary Updated! (${new Date().toLocaleDateString()})`,
       username: "Solana Bot",
       icon_emoji: ":solana:"
     };
     ```

3. **Gửi báo cáo định kỳ**:
   - Thêm node **Email** (n8n-nodes-base.email) để gửi tóm tắt tuần cho team.
   - Cấu hình:
     - **To**: Email của các sếp.
     - **Subject**: `Solana Weekly Summary - {{ $node["Schedule Trigger"]["json"]["date"].split('-')[2] }}`
     - **Body**: `{{ $node["Append Summary"]["json"]["response"]["values"][0]["Summary"] }}`

4. **Tối ưu chi phí OpenAI**:
   - Nếu chi phí tăng cao, có thể sử dụng **GPT-3.5-turbo** (rẻ hơn) với prompt tương tự.
   - Hoặc **lưu trữ dữ liệu tuần trước** để AI so sánh xu hướng.

5. **Tự động xóa dữ liệu cũ**:
   - Thêm node **Google Sheets** với **Query**:
     ```javascript
     // Node Code (Delete Old Data)
     const sheet = $input.all();
     const now = new Date();
     const oneMonthAgo = new Date(now.getTime() - 30 * 24 * 60 * 60 * 1000);
     const range = `A2:B${sheet.length}`;
     const query = `=FILTER(${range}, A2:A > "${oneMonthAgo.toISOString().split('T')[0]}")`;
     return { range: range, values: query };
     ```
   - Sau đó append kết quả vào sheet mới để giữ dữ liệu trong 1 tháng.

---

### 📌 **Kết luận**
Workflow **Daily Solana News Tracker** là giải pháp **tự động hóa hoàn chỉnh** để các sếp:
✔ **Theo dõi tin tức Solana một cách thông minh** mà không cần code.
✔ **Tóm tắt tuần bằng AI** để nắm bắt xu hướng thị trường nhanh chóng.
✔ **Lưu trữ dữ liệu dài hạn** trong Google Sheets, dễ dàng phân tích sau này.

**Bắt đầu ngay hôm nay!**
1. Import workflow vào n8n.
2. Cấu hình API và Google Sheets.
3. **Active workflow** và để nó làm việc cho bạn!

---
**💡 Cần hỗ trợ?**
- Trả lời câu hỏi trong [n8n Community](https://community.n8n.io/).
- Liên hệ với tác giả **Anatoly** qua [GitHub](https://github.com/Anatoly).
- Đăng ký **VPS n8n** để chạy workflow 24/7: [TinoHost](https://tino.vn/vps-n8n?affid=388).