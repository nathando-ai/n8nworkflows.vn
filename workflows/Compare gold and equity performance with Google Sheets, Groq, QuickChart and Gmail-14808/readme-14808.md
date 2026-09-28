---
title: "📈 Tự Động So Sánh Giá Trị Vốn Vàng & Chứng Khoán Với AI + Báo Cáo Email Tự Động - N8n"
description: "Workflow tự động so sánh hiệu suất đầu tư giữa vàng và chứng khoán, phân tích bằng AI Groq, tạo biểu đồ QuickChart và gửi báo cáo định kỳ qua email - tiết kiệm 10+ giờ công/tháng cho các sếp đầu tư."
slug: "tieu-dong-so-sanh-gia-tri-von-vang-chung-khoan"
tags: [n8n, automation, ai-groq, google-sheets, gmail, crypto-trading, investment-analysis]
keywords: [n8n workflow so sánh vàng chứng khoán, tự động hóa đầu tư, AI phân tích tài chính, báo cáo hiệu suất đầu tư, QuickChart biểu đồ, Groq AI]
---

# 🚀 **Tự Động So Sánh Hiệu Suất Vàng & Chứng Khoán - Từ Dữ Liệu → AI → Báo Cáo Email**

### **Nỗi Đau Của Các Sếp Đầu Tư**
- **Thủ công so sánh giá vàng vs chứng khoán**: Tốn thời gian, dễ sai sót khi tính toán thủ công.
- **Không có phân tích sâu**: Chỉ nhìn giá mà không hiểu xu hướng, cơ hội đầu tư.
- **Báo cáo không chuyên nghiệp**: Dữ liệu rời rạc, không có hình ảnh trực quan.
- **Không cảnh báo kịp thời**: Bỏ lỡ cơ hội khi hiệu suất chênh lệch quá lớn.

**Workflow này giải quyết tất cả!** Với **AI Groq** phân tích, **Google Sheets** lấy dữ liệu, **QuickChart** vẽ biểu đồ, và **Gmail** gửi báo cáo tự động - **các sếp chỉ cần nhấn 1 nút**.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 10+ giờ/tháng**: Không cần tính toán thủ công, so sánh tự động.
✅ **Phân tích AI chuyên nghiệp**: Groq AI đưa ra **cơ hội đầu tư** và **strategy allocation** dựa trên dữ liệu thực tế.
✅ **Biểu đồ trực quan**: QuickChart tạo **biểu đồ đường** so sánh giá vàng vs chứng khoán trong 1 click.
✅ **Báo cáo email tự động**: Gửi **báo cáo HTML đẹp** và **cảnh báo khẩn cấp** nếu hiệu suất chênh lệch quá ngưỡng.
✅ **Lịch sử đầu tư**: Lưu tất cả báo cáo vào **Google Sheets** để theo dõi dài hạn.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Google Sheets**:
   - **2 bảng dữ liệu**:
     - **Gold Prices** (cột: `Date`, `Price`).
     - **Equity Prices** (cột: `Date`, `Price`).
   - **Credentials**: [Cài đặt OAuth2 cho Google Sheets](https://developers.google.com/sheets/api/quickstart/python) và thêm vào n8n dưới tên `googleSheetsOAuth2Api`.

2. **Groq API**:
   - **API Key**: [Đăng ký tại Groq](https://console.groq.com/) và thêm vào n8n dưới tên `groqApi`.
   - **Model**: `llama-3.3-70b-versatile` (đã cấu hình sẵn).

3. **Gmail**:
   - **Credentials OAuth2**: [Cài đặt tại đây](https://developers.google.com/gmail/api/quickstart/python) và thêm vào n8n dưới tên `gmailOAuth2`.
   - **Email gửi**: Điền địa chỉ email muốn nhận báo cáo.

4. **QuickChart** (sử dụng URL API miễn phí):
   - Không cần API key, chỉ cần cấu hình trong node `Generate Chart`.
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/14808](https://n8n.io/workflows/14808) hoặc copy toàn bộ JSON từ [đây](https://github.com/n8n-io/n8n-workflows/blob/master/workflows/14808.json).
- **Dán vào n8n Editor**:
  - Mở n8n Studio → **Import Workflow** → Chọn `From JSON` → Dán và nhấn **Import**.

#### **2. Các Lưu Ý BẮT BUỘC Chỉnh 📌**
Workflow có **16 node**, nhưng **5 node quan trọng nhất** cần cấu hình kỹ:

##### **A. Node `Set Analysis Parameters` (type: set)**
- **Cấu hình tham số đầu vào**:
  ```json
  {
    "startDate": "2024-01-01",  // Ngày bắt đầu phân tích
    "endDate": "2024-06-30",    // Ngày kết thúc
    "performanceThreshold": 10 // Ngưỡng cảnh báo (%) khi hiệu suất chênh lệch
  }
  ```
  - **Gợi ý**: Đặt `startDate` và `endDate` theo kỳ đầu tư của các sếp.

##### **B. Node `Fetch Gold Prices` & `Fetch Equity Prices` (type: googleSheets)**
- **Chọn credentials**: `googleSheetsOAuth2Api` (đã cài đặt trước).
- **Cấu hình sheet**:
  - **Sheet Name**: `Gold Prices` (cho node vàng) và `Equity Prices` (cho node chứng khoán).
  - **Range**: `Sheet1!A2:B1000` (đảm bảo bao gồm tất cả dữ liệu).

##### **C. Node `Insights` (type: lmChatGroq)**
- **Model**: Đã mặc định là `llama-3.3-70b-versatile`.
- **Prompt mẫu** (nếu cần chỉnh sửa):
  ```plaintext
  Analyze the performance gap between gold and equity from {startDate} to {endDate}.
  Provide:
  1. Winning asset (gold or equity).
  2. Market context (e.g., inflation, interest rates).
  3. Portfolio allocation recommendation (e.g., 70% gold, 30% equity).
  ```
- **Credentials**: `groqApi` (đã thêm API key).

##### **D. Node `Generate Chart` (type: code)**
- **Mã JavaScript** (không cần chỉnh, nhưng hiểu logic):
  ```javascript
  // Tạo URL biểu đồ QuickChart từ dữ liệu
  const chartUrl = `https://quickchart.io/chart?c=${encodeURIComponent(JSON.stringify({
    type: 'line',
    data: {
      labels: goldData.map(item => item.Date),
      datasets: [
        { label: 'Gold Price', data: goldData.map(item => item.Price) },
        { label: 'Equity Price', data: equityData.map(item => item.Price) }
      ]
    }
  }))}`;
  return { chartUrl };
  ```

##### **E. Node `Send Report Email` & `Send Alert Email` (type: gmail)**
- **Chọn credentials**: `gmailOAuth2`.
- **Điền email nhận**:
  - **Report Email**: Địa chỉ email chính của các sếp.
  - **Alert Email**: Có thể là email khác (ví dụ: `investment-alert@domain.com`).

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Nhấn **Run Workflow** với dữ liệu mẫu (đảm bảo Google Sheets có dữ liệu từ ngày `startDate` đến `endDate`).
  - Kiểm tra **email nhận** và **Google Sheets** để xác nhận lưu log.
- **Bật Active**:
  - Sau khi test thành công, chuyển trạng thái workflow sang **Active**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tự động chạy hàng tuần**:
   - Sử dụng **n8n Trigger Node** (ví dụ: `n8n-nodes-base.cron`) để chạy workflow vào **mỗi thứ 7 sáng 8h**.
   - Cấu hình trong node `Run Report` (type: manualTrigger) → Chọn **Trigger Type: Cron**.

2. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack Webhook** hoặc **Telegram Bot** sau `Send Alert Email` để thông báo tức thời.

3. **Lưu log chi tiết**:
   - Thêm node **Google Drive** hoặc **AWS S3** để lưu toàn bộ báo cáo (không chỉ Google Sheets).

4. **Tối ưu ngưỡng cảnh báo**:
   - Nếu các sếp muốn cảnh báo khi hiệu suất chênh lệch **5%** thay vì **10%**, chỉnh `performanceThreshold` trong node `Set Analysis Parameters`.

5. **Tạo dashboard**:
   - Xuất dữ liệu từ Google Sheets vào **Google Data Studio** hoặc **Power BI** để tạo dashboard theo dõi dài hạn.

---

### 📌 **Kết Luận**
Workflow này **giải phóng các sếp khỏi công việc thủ công**, đưa ra **phân tích AI chuyên nghiệp**, và **gửi báo cáo tự động** - **tất cả chỉ với 1 lần setup**. **Đừng bỏ lỡ cơ hội đầu tư** vì thiếu dữ liệu! **Áp dụng ngay** và bắt đầu so sánh hiệu suất vàng vs chứng khoán một cách thông minh.

👉 **Bắt đầu tự động hóa ngay**:
1. [Tải workflow JSON](https://github.com/n8n-io/n8n-workflows/blob/master/workflows/14808.json).
2. [Cài đặt n8n Self-hosted](https://docs.n8n.io/hosting/installation/) (để chạy 24/7).
3. [Đăng ký VPS miễn phí 30 ngày](https://tino.vn/vps-n8n?affid=388) để test.

**Hãy để AI làm việc cho bạn!** 🚀