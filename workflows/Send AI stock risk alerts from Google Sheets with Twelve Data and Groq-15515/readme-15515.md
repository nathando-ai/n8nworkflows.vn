---
title: "🚀 Tự Động Hóa Cảnh Báo Rủi Ro Tài Chính AI Cho Cổ Phiếu - Từ Google Sheets Đến Email (Với Twelve Data & Groq)"
description: "Workflow này tự động đọc danh mục cổ phiếu từ Google Sheets, tính toán rủi ro bằng AI, và gửi cảnh báo email chỉ khi có biến động nguy hiểm. Giúp các sếp quản lý tài sản hiệu quả mà không cần code."
slug: "tieu-dong-hoa-canh-bao-rui-ro-tai-chinh-ai"
tags: [n8n, automation, ai-summarization, crypto-trading, google-sheets, email-alerts]
keywords: [n8n workflow cảnh báo rủi ro, tự động hóa tài chính AI, cảnh báo cổ phiếu nguy hiểm, Groq API, Google Sheets tự động hóa]
---

# 🚀 **Tự Động Hóa Cảnh Báo Rủi Ro Tài Chính AI Cho Cổ Phiếu - Từ Google Sheets Đến Email**

Hiện nay, việc theo dõi danh mục cổ phiếu thủ công không chỉ tốn thời gian mà còn dễ bị bỏ lỡ các biến động nguy hiểm. Các sếp thường phải mất hàng giờ mỗi tuần để kiểm tra giá trị tài sản, tính toán biến động, và quyết định khi nào cần can thiệp. **Workflow này giải quyết vấn đề đó bằng cách tự động hóa toàn bộ quy trình:**
- Đọc danh mục cổ phiếu từ **Google Sheets**.
- Tính toán **rủi ro thực thời** (giảm giá, biến động) bằng API Twelve Data.
- **Lọc và cảnh báo chỉ khi có biến động nguy hiểm** (thông qua ngưỡng tự động hóa).
- **Tóm tắt bằng AI** (Groq) và gửi email cảnh báo chi tiết.
- **Không gửi email dư thừa**, chỉ khi có rủi ro thực sự.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần theo dõi thủ công hàng ngày.
- **Cảnh báo chính xác**: Chỉ gửi email khi có rủi ro thực sự (giảm giá > ngưỡng hoặc biến động cao).
- **Tóm tắt AI**: Nội dung email được viết tự động bằng Groq, rõ ràng và chuyên nghiệp.
- **Hoạt động liên tục**: Workflow chạy tự động theo lịch hoặc khi có sự kiện mới.
- **Dễ dàng mở rộng**: Thêm ngưỡng cảnh báo mới hoặc tích hợp với Slack/Telegram.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets**:
   - Một bảng Google Sheets chứa danh mục cổ phiếu (cột: `Tên Cổ Phiếu`, `Số Lượng`, `Giá Mua`, `Ngưỡng Giảm Giá %`, `Ngưỡng Biến Động %`).
   - **Permissions**: Chia sẻ bảng với email OAuth2 của n8n (cấu hình trong `googleSheetsOAuth2Api`).

2. **Tài khoản Gmail**:
   - Email để gửi cảnh báo (ví dụ: `alerts@tênđômin.com`).
   - **Permissions**: Cấu hình OAuth2 trong `gmailOAuth2`.

3. **API Key Twelve Data** (miễn phí hoặc trả phí):
   - Đăng ký tại [Twelve Data](https://twelvedata.com/) và lấy API Key.
   - **Lưu ý**: API này có giới hạn request/phút (workflow có delay 8s giữa các request để tránh bị chặn).

4. **API Key Groq**:
   - Đăng ký tại [Groq](https://groq.com/) và lấy API Key.
   - **Model sử dụng**: `openai/gpt-oss-120b` (miễn phí trong giới hạn).

5. **Thông tin ngưỡng cảnh báo**:
   - **Giảm giá %**: Ví dụ, cảnh báo khi giá giảm > 5%.
   - **Biến động %**: Ví dụ, cảnh báo khi biến động > 10% trong 1 ngày.

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### 1. **Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/15515](https://n8n.io/workflows/15515) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ link trên và dán vào **Import Workflow** trong n8n.
- **Cách 3**: Sử dụng **n8n CLI** (nếu tự host):
  ```bash
  n8n import workflow.json --name "AI Stock Risk Alerts"
  ```

#### 2. **Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này gồm **13 node** quan trọng, các sếp cần cấu hình kỹ như sau:

##### **A. Node `Read Portfolio from Google Sheets`**
- **Credentials**: Chọn `googleSheetsOAuth2Api` (đã cấu hình trước).
- **Sheet Name**: Tên bảng chứa danh mục cổ phiếu (ví dụ: `"Portfolio"`).
- **Range**: Phần dữ liệu cần đọc (ví dụ: `"A1:D100"`).
- **Lưu ý**: Cột phải có tên chính xác (`Tên Cổ Phiếu`, `Số Lượng`, `Giá Mua`, `Ngưỡng Giảm Giá %`, `Ngưỡng Biến Động %`).

##### **B. Node `Edit Fields – Config & Thresholds` (Set)**
- **Tham số cần điền**:
  - `dropThreshold`: Ngưỡng giảm giá % để cảnh báo (ví dụ: `5`).
  - `volatilityThreshold`: Ngưỡng biến động % (ví dụ: `10`).
  - `apiKey`: API Key Twelve Data (điền vào `headers` của node `httpRequest`).

##### **C. Node `Filter – Only Flagged Risks` (If)**
- **Condition**: Kiểm tra nếu `isRisk` = `true` (được tính toán sau).
- **Lưu ý**: Node này chỉ cho phép dữ liệu có rủi ro đi tiếp.

##### **D. Node `Compute Risk Logic` (Function)**
- **Code mặc định**: Không cần chỉnh (tính toán % giảm giá và biến động).
- **Lưu ý**: Node này sử dụng dữ liệu từ `Twelve Data` để so sánh với giá mua ban đầu.

##### **E. Node `Groq Chat Model` (lmChatGroq)**
- **Credentials**: Chọn `groqApi`.
- **Prompt mẫu** (có thể chỉnh sửa):
  ```plaintext
  Tóm tắt cảnh báo rủi ro cho danh mục cổ phiếu:
  - Danh sách cổ phiếu có biến động nguy hiểm: {{{$json["flaggedStocks"]}}}
  - Giải thích: {{{$json["explanation"]}}}
  - Đề xuất hành động: {{{$json["recommendation"]}}}
  ```
- **Model**: Đảm bảo chọn `openai/gpt-oss-120b`.

##### **F. Node `Send Risk Alert Notification` (Gmail)**
- **Credentials**: Chọn `gmailOAuth2`.
- **Email To**: Điền email nhận cảnh báo (ví dụ: `sếp@tênđômin.com`).
- **Subject**: `🚨 Cảnh báo Rủi Ro Tài Chính: {{{$json["date"]}}}`.
- **Body**: Sử dụng nội dung từ Groq (node trước).

##### **G. Node `Loop: Fetch Current Prices` (SplitInBatches)**
- **Delay**: 8 giây giữa các request (tránh bị Twelve Data chặn).
- **API Endpoint**: `https://api.twelvedata.com/price?symbol={{{$node["Read Portfolio from Google Sheets"].json()["symbol"]}}}&apikey={{{$json["apiKey"]}}}`.

##### **H. Node `Merge Portfolio & Prices`**
- **Lưu ý**: Node này kết hợp dữ liệu cổ phiếu với giá thực thời để tính toán rủi ro.

---

#### 3. **Kích hoạt ⚡️**
1. **Test Run**:
   - Chọn node `When clicking ‘Execute workflow’` và nhấn **Run Workflow**.
   - Kiểm tra email nhận được có nội dung AI hay không.
2. **Bật Active**:
   - Sau khi test thành công, chuyển workflow sang **Active**.
   - **Lịch trình tự động**:
     - Sử dụng **n8n Cron Trigger** để chạy hàng ngày (ví dụ: `0 9 * * *` - 9h sáng hàng ngày).

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tích hợp với Slack/Telegram**:
   - Thay thế node `gmail` bằng `slack` hoặc `telegramBot` để cảnh báo tức thời.
   - **Cách làm**: Thêm node `slack` và cấu hình webhook từ Slack.

2. **Lưu log cảnh báo**:
   - Thêm node `googleSheets` sau `gmail` để ghi lại lịch sử cảnh báo vào bảng mới.
   - **Cột cần thêm**: `Ngày Cảnh Báo`, `Tên Cổ Phiếu`, `Giá Hiện Tại`, `Giá Mua`, `Nội Dung Cảnh Báo`.

3. **Cảnh báo đa ngưỡng**:
   - Chỉnh sửa node `Edit Fields` để thêm nhiều ngưỡng (ví dụ: cảnh báo khi giảm >3% hoặc >7%).

4. **Tự động cập nhật danh mục**:
   - Sử dụng **n8n Webhook** để cho phép cập nhật danh mục cổ phiếu từ ứng dụng khác (ví dụ: Excel Online).

5. **Báo cáo định kỳ**:
   - Tạo workflow riêng để gửi **báo cáo tuần/month** tổng hợp tất cả cổ phiếu (không chỉ rủi ro).

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc theo dõi tài sản thủ công, đồng thời **giảm thiểu rủi ro** bằng cách tự động cảnh báo khi có biến động nguy hiểm. Với **AI Groq** tóm tắt thông tin chi tiết và **Twelve Data** cung cấp dữ liệu thực thời, các sếp có thể **quản lý danh mục cổ phiếu như chuyên gia** mà không cần kiến thức code.

**Bắt đầu ngay!**
1. Import workflow và cấu hình các credentials.
2. Test với một số cổ phiếu mẫu.
3. Bật chế độ tự động và **quên đi lo lắng về rủi ro tài chính!**

---
**💡 Gợi ý tiếp theo**:
- Xem thêm workflow tự động hóa tài chính khác: [Tự động hóa báo cáo thu chi Excel](link-workflow).
- Cần hỗ trợ cấu hình? Đăng ký **hỗ trợ chuyên sâu** tại [n8n Community](https://community.n8n.io/).