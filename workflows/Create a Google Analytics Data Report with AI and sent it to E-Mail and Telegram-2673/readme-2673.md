---
title: "📊 Tự Động Hóa Báo Cáo Google Analytics Tuần Hàng + AI + Email & Telegram (Không Cần Code)"
description: "Tự động hóa báo cáo Google Analytics hàng tuần với AI tổng hợp dữ liệu, so sánh với cùng kỳ năm trước, gửi báo cáo chi tiết qua Email và tin nhắn Telegram. Giúp các sếp tiết kiệm 10+ giờ/tháng, phân tích nhanh chóng và cá nhân hóa thông tin."
slug: "tieu-dong-hoa-bao-cao-google-analytics-ai-email-telegram"
tags: [n8n, automation, google-analytics, ai, email, telegram, marketing, no-code, self-hosted]
keywords: [tự động hóa báo cáo google analytics, workflow n8n google analytics, báo cáo marketing tự động, ai tổng hợp dữ liệu, gửi báo cáo qua email và telegram, tiết kiệm thời gian phân tích]
---

# 🚀 **Tự Động Hóa Báo Cáo Google Analytics Tuần Hàng Với AI + Email & Telegram**

## **🔥 Nỗi Đau Của Các Sếp Trong Phân Tích Marketing**
Hàng tuần, các sếp marketing phải:
- **Tải dữ liệu Google Analytics** từ bảng điều khiển thủ công.
- **So sánh số liệu** với cùng kỳ năm trước để phát hiện xu hướng.
- **Tổng hợp và viết báo cáo** chi tiết, mất từ 2-3 giờ/lần.
- **Gửi báo cáo** cho đội ngũ hoặc khách hàng qua Email hoặc Telegram.

**Kết quả?** Thời gian bị "chôn" trong công việc lặp đi lặp lại, mất tập trung vào chiến lược thực sự. **Workflow này giải quyết tất cả!**

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 10+ giờ/tháng** – Dữ liệu tự động thu thập, tổng hợp và gửi.
✅ **So sánh tự động** với cùng kỳ năm trước để phát hiện xu hướng tăng/giảm.
✅ **Báo cáo cá nhân hóa** với phân tích AI chi tiết, dễ hiểu.
✅ **Gửi báo cáo 24/7** qua Email và Telegram (tùy chọn).
✅ **Hoạt động liên tục** – Không cần can thiệp thủ công.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Analytics** (và **API Key OAuth2** đã cấu hình trong n8n).
   - [Hướng dẫn tạo OAuth2 cho Google Analytics](https://docs.n8n.io/integrations/builtin/credentials/google/)
2. **API Key cho AI** (OpenAI, Anthropic, Google Vertex AI, hoặc Ollama).
   - [Hướng dẫn cấu hình OpenAI API](https://docs.n8n.io/integrations/builtin/credentials/openai/)
3. **Thông tin SMTP** để gửi Email (tên miền, mật khẩu ứng dụng, port).
   - [Hướng dẫn cấu hình SMTP](https://docs.n8n.io/integrations/builtin/credentials/smtp/)
4. **Token Telegram Bot** (nếu muốn gửi báo cáo qua Telegram).
   - [Hướng dẫn tạo Bot Telegram](https://docs.n8n.io/integrations/builtin/credentials/telegram/)
5. **n8n Self-hosted** (không dùng phiên bản cloud để đảm bảo dữ liệu an toàn).
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Từ File JSON**
1. Tải file JSON của workflow từ [đây](https://n8n.io/workflows/2673) (hoặc copy JSON từ trang gốc).
2. Trên **n8n Editor**, nhấn **Import** → **Paste JSON** và dán nội dung.
3. Chọn **Import** để thêm workflow vào canvas.

#### **Phương pháp 2: Copy/Paste JSON**
1. Mở **n8n Editor** → Tạo workflow mới.
2. Nhấn **Import** → **Paste JSON** và dán toàn bộ mã JSON từ workflow.
3. Nhấn **Import** để hoàn tất.

---
### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**

#### **🔹 Node 1: Schedule Trigger (Động cơ kích hoạt)**
- **Cấu hình:**
  - **Cron Expression:** `0 7 * * 1` (chạy hàng tuần thứ 2 lúc 7h sáng).
  - **Time Zone:** Chọn múi giờ phù hợp (ví dụ: `Asia/Ho_Chi_Minh`).
- **Lưu ý:** Đảm bảo thời gian kích hoạt phù hợp với nhu cầu báo cáo của doanh nghiệp.

#### **🔹 Node 2 & 7: Google Analytics (Lấy dữ liệu)**
- **Cấu hình chung:**
  - **Credentials:** Chọn `googleAnalyticsOAuth2` (đã cấu hình trước).
  - **View ID:** Nhập ID View của Google Analytics (tìm trong `Admin` → `View`).
  - **Metrics:** Chọn các chỉ số cần theo dõi (ví dụ: `sessions`, `bounces`, `conversions`).
  - **Dimensions:** Thêm các chiều phân tích (ví dụ: `date`, `country`).
- **Node "Google Analytics Letzte 7 Tage":**
  - **Date Range:** `last 7 days` (7 ngày gần nhất).
- **Node "Google Analytics: Past 7 days of the previous year":**
  - **Date Range:** `last 7 days of the previous year` (so sánh cùng kỳ năm trước).

#### **🔹 Node 3 & 8: Summarize (Tổng hợp dữ liệu bằng AI)**
- **Cấu hình:**
  - **Credentials:** Chọn `openAiApi` (hoặc AI khác đã cấu hình).
  - **Prompt:** Sử dụng mặc định hoặc tùy chỉnh:
    ```
    Analyze the following Google Analytics data and summarize key insights:
    - Total sessions: {totalSessions}
    - Bounce rate: {bounceRate}%
    - Conversion rate: {conversionRate}%
    - Top traffic sources: {topSources}
    Provide a concise analysis with trends compared to the previous year.
    ```
  - **Model:** Chọn mô hình phù hợp (ví dụ: `gpt-3.5-turbo`).

#### **🔹 Node 4 & 9: Processing for Email/Telegram (Xử lý AI cho Email & Telegram)**
- **Cấu hình chung:**
  - **Credentials:** `openAiApi`.
  - **Prompt Email:**
    ```
    Create a detailed email report for marketing team based on the following data:
    {data}
    Include:
    1. Executive summary
    2. Key metrics with year-over-year comparison
    3. Traffic sources analysis
    4. Recommendations for next steps
    Format as HTML with clear tables and charts.
    ```
  - **Prompt Telegram:**
    ```
    Summarize the key insights from the Google Analytics report in a concise Telegram message:
    {data}
    Keep it under 1000 characters and highlight:
    - Top 3 trends
    - Biggest improvements/declines
    - One actionable recommendation
    ```

#### **🔹 Node 5 & 10: Calculator & Code (Tính toán so sánh)**
- **Node "Calculator":**
  - Sử dụng để tính toán các chỉ số như **tỷ lệ tăng/giảm** giữa hai kỳ.
  - Ví dụ: `(currentValue - previousValue) / previousValue * 100`.
- **Node "Calculation same period previous year":**
  - **Code JavaScript:**
    ```javascript
    // Ví dụ: Tính toán tỷ lệ tăng trưởng
    const currentData = $input.all();
    const previousData = $input.previousYearData;

    const growthRate = (currentData.totalSessions - previousData.totalSessions) / previousData.totalSessions * 100;

    return {
      growthRate: growthRate.toFixed(2) + "%",
      currentSessions: currentData.totalSessions,
      previousSessions: previousData.totalSessions
    };
    ```

#### **🔹 Node 6 & 11: Assign Data (Gán dữ liệu)**
- **Cấu hình:**
  - **Set:** Chọn `data` (dữ liệu từ Google Analytics) và gán vào biến `currentData`.
  - **Set (previous year):** Gán dữ liệu năm trước vào `previousYearData`.

#### **🔹 Node 12: EmailSend (Gửi Email)**
- **Cấu hình:**
  - **Credentials:** Chọn `smtp` (đã cấu hình trước).
  - **To:** Nhập Email nhận báo cáo (ví dụ: `marketing@doanhnghiep.com`).
  - **Subject:** `📊 Báo Cáo Google Analytics Tuần {date}`.
  - **HTML Content:** Sử dụng kết quả từ `Processing for email` (biến `emailContent`).

#### **🔹 Node 13: Telegram (Gửi tin nhắn Telegram - tùy chọn)**
- **Cấu hình:**
  - **Credentials:** Chọn `telegramApi`.
  - **Chat ID:** Nhập ID chat của Bot Telegram (tìm bằng cách gửi `/start` và copy link).
  - **Message:** Sử dụng kết quả từ `Processing for Telegram` (biến `telegramMessage`).

---
### **3. Kích Hoạt ⚡️**
1. **Test Run:**
   - Nhấn **Run Workflow** để kiểm tra dữ liệu mẫu.
   - Kiểm tra Email và Telegram xem có nhận được báo cáo không.
2. **Bật Active:**
   - Sau khi kiểm tra thành công, chuyển trạng thái workflow sang **Active**.

---

## **✍️ Mẹo & Gợi Ý Nâng Cao**

### **1. Tùy Chỉnh Báo Cáo Theo Nhóm Người Dùng**
- **Sử dụng Node `Set`** để phân loại dữ liệu cho từng nhóm (ví dụ: `marketingTeam`, `salesTeam`).
- **Tạo nhiều Email/Telegram** với nội dung khác nhau bằng **Node `Switch`**.

### **2. Lưu Log Dữ Liệu**
- **Thêm Node `StickyNote`** để lưu dữ liệu vào Google Sheets hoặc Notion.
- **Cấu hình Node `Google Sheets`** để ghi lại lịch sử báo cáo.

### **3. Gửi Báo Cáo Định Kỳ (Hàng Tháng/Nửa Năm)**
- **Chỉnh Cron Expression** trong `Schedule Trigger`:
  - **Hàng tháng:** `0 8 1 * *` (lúc 8h sáng ngày 1 hàng tháng).
  - **Nửa năm:** `0 8 1 6 *` (lúc 8h sáng ngày 1 tháng 6 và tháng 12).

### **4. Kết Hợp Với Slack**
- **Thêm Node `Slack`** để gửi báo cáo qua kênh Slack.
- **Cấu hình:**
  - **Credentials:** `slackApi`.
  - **Channel:** `#marketing-reports`.
  - **Message:** Sử dụng kết quả từ `Processing for email` (định dạng ngắn gọn).

### **5. Cập Nhật API Key An Toàn**
- **Sử dụng Node `Code`** để kiểm tra và cập nhật API Key tự động nếu hết hạn.
- **Ví dụ:**
  ```javascript
  // Kiểm tra OpenAI API Key
  const response = await fetch('https://api.openai.com/v1/models', {
    headers: { 'Authorization': `Bearer ${$input.openAiApi.apiKey}` }
  });
  if (response.status !== 200) {
    throw new Error("API Key hết hạn!");
  }
  ```

---

## **📌 Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp marketing để tập trung vào chiến lược chứ không phải mắc kẹt trong công việc lặp đi lặp lại. Với **AI tổng hợp dữ liệu**, **so sánh tự động** và **gửi báo cáo qua Email/Telegram**, doanh nghiệp sẽ có **báo cáo chuyên nghiệp, chính xác và cá nhân hóa** chỉ trong vài giây mỗi tuần.

**🚀 Hành động ngay!**
1. **Cài đặt n8n Self-hosted** trên VPS (sử dụng mã giảm giá **VPSN8N**).
2. **Import workflow** và cấu hình các API Key.
3. **Bật Active** và theo dõi báo cáo tự động hàng tuần!

**Có thắc mắc?** Đừng ngại liên hệ với tác giả Friedemann Schuetz qua [LinkedIn](https://www.linkedin.com/in/friedemann-schuetz) hoặc comment bên dưới. 😊

---
**💡 Lưu ý cuối cùng:**
- **N8n Self-hosted** là lựa chọn an toàn nhất để tránh rò rỉ dữ liệu.
- **Kiểm tra log** trong n8n để phát hiện lỗi nếu workflow không hoạt động.
- **Tùy chỉnh Prompt** để phù hợp với ngôn ngữ và nhu cầu cụ thể của doanh nghiệp.