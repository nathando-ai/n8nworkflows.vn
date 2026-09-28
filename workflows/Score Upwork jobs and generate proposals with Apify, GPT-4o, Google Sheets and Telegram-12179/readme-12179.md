---
title: "🚀 Tự Động Hóa Tìm Kiếm & Đánh Giá Công Việc Upwork + Tạo Đề Xuất AI (GPT-4o + Google Sheets + Telegram)"
description: "Workflow tự động hóa 100% không code giúp các sếp tìm kiếm, đánh giá và tạo đề xuất cá nhân hóa cho công việc Upwork hàng ngày, tiết kiệm thời gian lên đến 10 giờ/tuần. Kết hợp AI (GPT-4o), Google Sheets và Telegram để tối ưu hóa quy trình lead generation."
slug: "tieu-dong-hoa-upwork-ai-gpt4o"
tags: [n8n, automation, upwork, ai-summarization, lead-generation, gpt-4o, google-sheets, telegram-bot]
keywords: [tự động hóa upwork, tìm kiếm công việc upwork, đánh giá công việc ai, tạo đề xuất upwork bằng ai, n8n workflow upwork, tự động hóa lead generation]
---

# 🚀 **Tự Động Hóa Tìm Kiếm & Đánh Giá Công Việc Upwork + Tạo Đề Xuất AI (GPT-4o + Google Sheets + Telegram)**

### **Giải pháp cho nỗi đau của các sếp freelancer/agency:**
- **Thời gian vô cùng tốn kém:** Phải thủ công tìm kiếm, lọc và đánh giá hàng trăm công việc Upwork mỗi ngày.
- **Rủi ro bỏ lỡ cơ hội:** Do phải refresh liên tục, nhiều công việc "hot" bị bỏ qua khi bạn chưa kịp phản hồi.
- **Đề xuất không cá nhân hóa:** Các mẫu đề xuất sẵn có thường chung chung, không phù hợp với từng công việc cụ thể.
- **Không theo dõi được hiệu quả:** Không biết công việc nào có tiềm năng cao, không có báo cáo tự động.

**Workflow này giải quyết tất cả đó!** Với công nghệ **Apify** (scraper), **GPT-4o** (AI đánh giá & tạo đề xuất), **Google Sheets** (lưu trữ & theo dõi) và **Telegram** (báo cáo tự động), bạn sẽ:
✅ **Tìm kiếm tự động** công việc mới trên Upwork theo keyword của mình.
✅ **Đánh giá AI** tiềm năng của mỗi công việc (Fit Score 0-100).
✅ **Lọc ra công việc chất lượng** (score ≥ 60) và tạo **đề xuất cá nhân hóa** bằng GPT-4o.
✅ **Lưu trữ & theo dõi** tất cả công việc trong Google Sheets.
✅ **Nhận báo cáo hàng ngày** qua Telegram, bao gồm thống kê và đề xuất mới.

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tuần** (không cần refresh thủ công).
- **Tăng tỷ lệ thành công** với đề xuất AI cá nhân hóa (tăng 30-50% so với mẫu chung).
- **Không bỏ lỡ công việc** nhờ hệ thống deduplicate tự động.
- **Quản lý lead hiệu quả** với báo cáo tự động qua Telegram.
- **Giảm chi phí** với GPT-4o-mini (rẻ hơn GPT-4).
:::

---

## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Upwork** (để scraper lấy dữ liệu).
2. **Tài khoản Apify** (để sử dụng Actor Upwork Scraper):
   - [Tạo tài khoản Apify miễn phí](https://apify.com/) và lấy:
     - **Actor ID** (ví dụ: `upwork-jobs-scraper`).
     - **API Token** (tạo ở [Apify Console](https://apify.com/console/tokens)).
3. **Tài khoản Google Sheets**:
   - Tạo một **Google Sheet** mới với **cột đầu tiên tên chính xác là `Job ID`** (dùng để deduplicate).
   - Chia sẻ với n8n bằng quyền **Editor**.
4. **Tài khoản OpenAI** (để sử dụng GPT-4o):
   - [Đăng ký API Key](https://platform.openai.com/account/api-keys) và chọn mô hình **gpt-4o-mini** (rẻ hơn).
5. **Bot Telegram** (để nhận báo cáo tự động):
   - Tạo bot qua [@BotFather](https://t.me/BotFather) và lấy **Chat ID** (dùng [tool này](https://api.telegram.org/bot<BOT_TOKEN>/getUpdates)).
6. **n8n Self-hosted** (khuyến nghị để workflow chạy 24/7):
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).
7. **Các biến môi trường (Environment Variables)** trong n8n:
   - `GOOGLE_SHEETS_DOC_ID`: ID của Google Sheet (lấy từ URL: `https://docs.google.com/spreadsheets/d/[ID]/edit`).
   - `APIFY_ACTOR_ID`: ID Actor Upwork Scraper (ví dụ: `upwork-jobs-scraper`).
   - `APIFY_API_TOKEN`: Token API của Apify.
   - `TELEGRAM_CHAT_ID`: Chat ID của bot Telegram.
   - `OPEN_AI_API_KEY`: API Key của OpenAI.
   - `MINIMUM_SCORE`: Ngưỡng điểm tối thiểu (mặc định là `60`).
   - `SYSTEM_PROMPT`: Nội dung hệ thống cho AI tạo đề xuất (xem hướng dẫn dưới đây).
:::

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Bước 1: Tải file JSON của workflow từ [n8n.io/workflows/12179](https://n8n.io/workflows/12179).
Bước 2: Trong **n8n Editor**, nhấn **Import** và chọn file JSON đã tải.
**Hoặc** copy toàn bộ JSON từ file và dán vào **Import Workflow** trong n8n.

:::warning[LƯU Ý]
- **Không chỉnh sửa trực tiếp JSON** nếu chưa hiểu rõ logic. Thay vào đó, chỉnh sửa trong **n8n Editor**.
- Nếu workflow không hoạt động, kiểm tra **log error** trong tab **Execution**.
:::

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **A. Cấu hình Schedule Trigger**
- Node này chạy **mỗi 6 giờ** (thời gian mặc định). Các sếp có thể điều chỉnh ở:
  - **Cron Expression**: Ví dụ `0 0 */6 * * *` (lúc 00:00, 06:00, 12:00, 18:00 hàng ngày).
  - **Time Zone**: Chọn timezone phù hợp (ví dụ: `Asia/Ho_Chi_Minh`).

#### **B. Cấu hình Apify Scraper**
- Node **"Run Apify Scraper"** và **"Get Dataset Items"** cần thiết lập:
  - **URL**: `https://api.apify.com/v2/act/[APIFY_ACTOR_ID]/runs`
  - **Headers**:
    ```json
    {
      "Authorization": "Bearer [APIFY_API_TOKEN]",
      "Content-Type": "application/json"
    }
    ```
  - **Body** (dùng node **Code** sau đó):
    ```json
    {
      "userAgent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36",
      "input": {
        "keywords": ["web developer", "python developer", "seo specialist"], // Thay đổi keyword theo nhu cầu
        "budget": {
          "hourly": {
            "min": 25,
            "max": 150
          },
          "fixed": {
            "min": 200,
            "max": 50000
          }
        }
      }
    }
    ```

#### **C. Cấu hình Google Sheets**
- Node **"Read Existing Job IDs"** và **"Log to Google Sheet"** cần:
  - **Credentials**: Chọn **Google Sheets** đã kết nối trước đó.
  - **Sheet Name**: Tên tab trong Google Sheet (mặc định là `Sheet1`).
  - **Range**: `Job ID!A:A` (để đọc/ghi vào cột `Job ID`).
  - **Operation**: `append` (để thêm dữ liệu mới vào cuối sheet).

#### **D. Cấu hình AI Scoring & Generate Proposal**
- Node **"AI Scoring"** và **"Generate Proposal"** sử dụng **OpenAI**:
  - **Model**: `gpt-4o-mini` (rẻ hơn `gpt-4`).
  - **Prompt** (cần chỉnh sửa theo chuyên môn của bạn):
    ```json
    {
      "role": "system",
      "content": "Bạn là một chuyên gia đánh giá công việc freelance trên Upwork. Đánh giá tiềm năng của công việc dựa trên:
      1. Phù hợp với kỹ năng của tôi (0-50 điểm).
      2. Chất lượng khách hàng (0-30 điểm, dựa trên đánh giá và số lượng công việc đã hoàn thành).
      3. Ngân sách phù hợp (0-20 điểm).
      Trả về kết quả dưới dạng JSON: {'fit_score': số_điểm, 'reason': 'lý do'}"
    }
    ```
  - **Prompt Generate Proposal** (cần thay đổi theo portfolio của bạn):
    ```json
    {
      "role": "system",
      "content": "Bạn là một chuyên gia tạo đề xuất freelance. Tạo một đề xuất cá nhân hóa cho công việc Upwork sau:
      - Tiêu đề công việc: $job_title
      - Mô tả công việc: $job_description
      - Ngân sách: $budget
      - Thông tin khách hàng: $client_info
      Đề xuất phải bao gồm:
      1. Giới thiệu ngắn về bạn.
      2. Kế hoạch chi tiết (bước 1, 2, 3).
      3. Lý do bạn phù hợp với công việc này.
      4. Tham khảo portfolio: [LINK_PORTFOLIO_BẠN].
      Trả về dưới dạng markdown."
    }
    ```

#### **E. Cấu hình Telegram Alert**
- Node **"Send Summary"** và **"Send Error Alert"** cần:
  - **Credentials**: Chọn **Telegram Bot** đã kết nối.
  - **Message Template**:
    ```json
    {
      "text": "📌 **Tổng kết công việc mới (${newDate})**\n\n" +
      "- **Tổng công việc mới**: ${newJobsCount}\n" +
      "- **Công việc score ≥ 60**: ${highScoreJobsCount}\n" +
      "- **Đề xuất mới**: ${proposalsGenerated}\n\n" +
      "📌 **Công việc top**:\n${topJobs}"
    }
    ```

---

### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **Run Workflow** và chọn **Test Execution**.
   - Kiểm tra **log** để đảm bảo tất cả node hoạt động.
2. **Bật Active**:
   - Sau khi kiểm tra thành công, chuyển **Status** từ **Inactive** sang **Active**.

---

## ✍️ **Mẹo & gợi ý nâng cao**
:::info[TIPS THỰC TIỆN]
1. **Tối ưu keyword**:
   - Thay đổi `keywords` trong **Apify Input** để lọc ra công việc phù hợp nhất với chuyên môn của bạn.
2. **Lưu log chi tiết**:
   - Thêm node **Google Sheets** để lưu **tất cả dữ liệu** (không chỉ Job ID), bao gồm:
     - `Job Title`, `Client Name`, `Budget`, `Fit Score`, `Proposal Draft`.
3. **Báo cáo định kỳ**:
   - Sử dụng **n8n Schedule Trigger** để gửi báo cáo **từng tháng** (ví dụ: ngày 1 hàng tháng).
4. **Kết hợp với Slack**:
   - Thay vì Telegram, các sếp có thể sử dụng **Slack Webhook** để nhận báo cáo.
5. **Cập nhật hệ thống prompt**:
   - Sau mỗi tháng, review và cập nhật **SYSTEM_PROMPT** để AI tạo đề xuất tốt hơn.
6. **Dùng GPT-4o-mini**:
   - Để tiết kiệm chi phí, hãy luôn chọn mô hình `gpt-4o-mini` thay vì `gpt-4`.
7. **Monitoring lỗi**:
   - Kiểm tra **Error Trigger** thường xuyên để đảm bảo workflow không bị ngắt.
:::

---

## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp freelancer, agency hoặc consultant muốn tự động hóa quy trình tìm kiếm và đề xuất công việc trên Upwork. Với **AI đánh giá tiềm năng**, **tạo đề xuất cá nhân hóa** và **báo cáo tự động**, bạn sẽ:
✔ **Tiết kiệm thời gian** để tập trung vào công việc thực sự quan trọng.
✔ **Tăng tỷ lệ thành công** với đề xuất AI chất lượng cao.
✔ **Không bỏ lỡ cơ hội** nhờ hệ thống deduplicate và báo cáo 24/7.

**Hành động ngay hôm nay!**
1. **Chuẩn bị tài khoản** (Apify, Google Sheets, OpenAI, Telegram).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Bật Active** và bắt đầu tự động hóa!

👉 **Nếu gặp vấn đề**, hãy để lại comment dưới đây hoặc liên hệ với cộng đồng n8n tại [n8n Community](https://community.n8n.io/). Chúc các sếp thành công! 🚀