---
title: "🔍 **Tự Động Hóa Scrape & Phân Tích Danh Tiêu Trustpilot với AI (ScrapegraphAI + OpenAI) - Giúp Doanh Nghiệp Hiểu Thấu Được Phản Hồi Khách Hàng**"
description: "Workflow tự động hóa scrape tất cả đánh giá Trustpilot cho một doanh nghiệp cụ thể, phân tích cảm xúc (sentiment), tổng hợp chủ đề và gửi báo cáo định kỳ qua email. Giúp các sếp tiết kiệm 10+ giờ/tháng và đưa ra quyết định dựa trên dữ liệu AI."
slug: "tieu-dong-hoa-scrape-phan-tich-danh-tieu-trustpilot"
tags: [n8n, automation, no-code, market-research, ai-summarization, scrapegraphai, openai, sentiment-analysis]
keywords: [tự động hóa scrape trustpilot, phân tích cảm xúc ai, báo cáo danh tiếng doanh nghiệp, n8n workflow tự động, tự động hóa market research, scrape đánh giá khách hàng]
---

# 🚀 **Tự Động Hóa Scrape & Phân Tích Danh Tiêu Trustpilot với AI: Từ Phản Hồi Khách Hàng → Báo Cáo Chiến Lược**

### **Nỗi Đau Của Các Sếp**
Các sếp thường phải **tốn thời gian và công sức** để:
- **Scrape thủ công** hàng trăm đánh giá Trustpilot cho một doanh nghiệp.
- **Phân tích từng review** để tìm ra xu hướng, điểm mạnh/điểm yếu.
- **Tổng hợp báo cáo** để gửi cho ban lãnh đạo, nhưng lại **không có thời gian** hoặc **không có công cụ tự động hóa**.
- **Bị mất thông tin quan trọng** vì không theo dõi định kỳ.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Scrape tất cả đánh giá** từ Trustpilot (theo trang, theo thời gian).
✅ **Chuyển đổi HTML thành Markdown sạch** (dùng ScrapegraphAI).
✅ **Phân tích cảm xúc (sentiment)** của từng review (Tốt, Trung bình, Xấu).
✅ **Tổng hợp chủ đề chính** và **tạo báo cáo AI** với đề xuất cải tiến.
✅ **Gửi báo cáo qua email** tự động cho các sếp và team marketing.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**).
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đảm bảo tốc độ cao, không lag).
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tháng** so với việc scrape và phân tích thủ công.
- **Nhận báo cáo AI chi tiết** với phân tích cảm xúc, chủ đề nổi bật và đề xuất cải tiến.
- **Theo dõi danh tiếng doanh nghiệp** một cách **liên tục và tự động**.
- **Gửi báo cáo định kỳ** (ngày/tuần/tháng) cho ban lãnh đạo **không cần can thiệp**.
- **Cải thiện trải nghiệm khách hàng** bằng cách phản hồi kịp thời với những điểm yếu.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi chạy workflow, các sếp cần chuẩn bị:
✔ **API Key ScrapegraphAI** (để chuyển đổi HTML thành Markdown).
✔ **API Key OpenAI** (để phân tích cảm xúc và tổng hợp báo cáo AI).
✔ **Tài khoản Gmail OAuth2** (để gửi báo cáo tự động).
✔ **Trustpilot URL của doanh nghiệp** (ví dụ: `https://www.trustpilot.com/review/www.example.com`).
✔ **Số lượng trang scrape tối đa** (để tránh bị chặn bởi Trustpilot).

---
:::note[LƯU Ý QUAN TRỌNG]
- **ScrapegraphAI** có giới hạn scrape (thường là **1000 request/tháng** miễn phí). Nếu scrape nhiều trang, cần nâng cấp plan.
- **OpenAI** cũng có giới hạn token (tối đa **4096 token** cho mỗi request). Workflow đã tối ưu để tránh bị lỗi.
- **Trustpilot có thể chặn scrape** nếu request quá nhanh. Workflow đã thêm **delay tự động** để tránh bị block.
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow bằng **2 cách**:
- **Tải file JSON** từ [n8n.io/workflows/12654](https://n8n.io/workflows/12654) và import vào **n8n Editor**.
- **Copy JSON** từ link trên và **paste vào n8n Editor** (tab "Import").

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflows này có **20 node**, nhưng chỉ có **5 node quan trọng** cần cấu hình kỹ:

##### **A. Node "Set Parameters" (Cấu Hình Tham Số)**
- **Tham số cần điền:**
  - `company_id`: **Trustpilot URL** của doanh nghiệp (ví dụ: `https://www.trustpilot.com/review/www.example.com`).
  - `max_page`: **Số trang scrape tối đa** (gợi ý: **5-10 trang** để tránh bị chặn).
  - `delay`: **Thời gian chờ giữa các request** (gợi ý: **2000ms** để tránh bị block).

##### **B. Node "ScrapegraphAI" (Chuyển HTML → Markdown)**
- **Credentials:** Chọn `scrapegraphAIApi` (đã cấu hình trước).
- **Tham số cần kiểm tra:**
  - `resource`: Đảm bảo là `"markdownify"` (chuyển HTML thành Markdown).
  - **Input:** Đảm bảo dữ liệu từ node `Extract` (HTML) được truyền vào.

##### **C. Node "OpenAI Chat Model" (Phân Tích Cảm Xúc & Tổng Hợp)**
- **Credentials:** Chọn `openAiApi` (đã cấu hình trước).
- **Tham số cần chỉnh:**
  - `model`: Chọn `"gpt-4o-mini"` (nếu có) hoặc `"gpt-5-mini"` (nếu không).
  - **Prompt:** Workflow đã tự động cấu hình, nhưng các sếp có thể **tùy chỉnh** để phù hợp với ngành nghề:
    ```json
    "prompt": "Analyze the following customer reviews and provide a structured report with:
    1. Sentiment distribution (Positive/Neutral/Negative).
    2. Key themes and pain points.
    3. Actionable recommendations for improvement."
    ```

##### **D. Node "Send a message" (Gửi Báo Cáo qua Email)**
- **Credentials:** Chọn `gmailOAuth2` (đã cấu hình trước).
- **Tham số cần điền:**
  - `to`: **Email của người nhận** (ví dụ: `team@doanhnghiep.com`).
  - `subject`: **Tiêu đề email** (gợi ý: `"Báo Cáo Danh Tiêu Trustpilot - [Tên Doanh Nghiệp]"`).
  - **HTML Content:** Workflow sẽ tự động tạo **báo cáo HTML** từ node `QuickChart` và `Aggregate reviews`.

##### **E. Node "Limit" (Giới Hạn Số Lượng Review)**
- **Tham số cần chỉnh:**
  - `maxItems`: **Số review tối đa** để phân tích (gợi ý: **50-100 review** để tránh quá tải OpenAI).

#### **3. Kích Hoạt ⚡️**
- **Test Run:** Chọn **node "When clicking ‘Test workflow’"** và nhấn **"Execute Workflow"**.
- **Kiểm tra kết quả:**
  - **Email:** Kiểm tra hộp thư của người nhận để xem báo cáo đã được gửi chưa.
  - **Log n8n:** Kiểm tra **tab "Executions"** để xem workflow có lỗi nào không.
- **Bật Active:** Nếu test thành công, **bật workflow** để chạy tự động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tự động chạy hàng tuần/tháng**
   - Sử dụng **n8n Cron Trigger** để chạy workflow **tự động** vào ngày/mồng tháng nào đó.
   - Ví dụ: `0 0 * * 1` (chạy vào thứ Hai hàng tuần).

2. **Gửi báo cáo lên Slack/Telegram**
   - Thay vì email, các sếp có thể **gửi báo cáo lên Slack/Telegram** bằng node `webhook` hoặc `slack`.
   - Cài đặt **webhook Slack** và cấu hình node `httpRequest` để gửi thông báo.

3. **Lưu log vào Google Sheets/Notion**
   - Sử dụng node `googleSheets` hoặc `notion` để **lưu tất cả review và phân tích** vào bảng tính hoặc Notion.
   - Có thể **tự động cập nhật** khi có review mới.

4. **Phân tích so sánh với đối thủ**
   - Sử dụng **cùng một workflow** để scrape và phân tích **nhiều doanh nghiệp** và so sánh kết quả.
   - Có thể **tạo dashboard** bằng Power BI hoặc Google Data Studio.

5. **Tùy chỉnh AI Agent**
   - Node `Company Reputation Analyst` (AI Agent) có thể **tùy chỉnh prompt** để phù hợp với ngành nghề:
     - **Ngành du lịch:** Nhấn mạnh vào **trải nghiệm khách hàng**.
     - **Ngành eCommerce:** Phân tích **chất lượng sản phẩm và giao hàng**.
     - **Ngành dịch vụ:** Đánh giá **tính chuyên nghiệp của nhân viên**.

---

### 📌 **Kết Luận: Áp Dụng Ngay Để Cải Thiện Danh Tiêu Doanh Nghiệp!**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào **strategy** thay vì **làm việc thủ công**. Bằng cách:
✔ **Scrape tự động** tất cả đánh giá Trustpilot.
✔ **Phân tích cảm xúc** và **tổng hợp chủ đề** bằng AI.
✔ **Gửi báo cáo định kỳ** cho ban lãnh đạo.

**Hành động ngay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test run** và kiểm tra kết quả.
3. **Bật workflow** và **quên đi việc scrape thủ công**!

**Nếu các sếp cần hỗ trợ thêm**, có thể liên hệ với tác giả Davide qua:
📧 **Email:** [info@n3w.it](mailto:info@n3w.it)
🔗 **LinkedIn:** [linkedin.com/in/davideboizza](https://linkedin.com/in/davideboizza)

---
**🎥 Xem video hướng dẫn chi tiết trên YouTube:**
👉 **[Subscribe kênh n3witalia](https://youtube.com/@n3witalia)** để nhận **FREE template n8n** và các tutorial tự động hóa khác!