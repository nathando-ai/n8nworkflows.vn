---
title: "🚀 Tự Động Hóa Scrape Đánh Giá Trustpilot + AI Tạo Copy Quảng Cáo Facebook Hiệu Quả (GPT-4o-mini)"
description: "Workflow tự động hóa scrape đánh giá Trustpilot của đối thủ bằng Bright Data, phân tích điểm yếu bằng AI, và tạo 3 bản copy quảng cáo Facebook tối ưu hóa từ feedback thực tế - tiết kiệm thời gian marketing 80%!"
slug: "tieu-dong-hoa-scrape-trustpilot-ai-tao-copy-quang-cao"
tags: [n8n, automation, marketing, ai, bright-data, google-sheets, openai, gpt-4o-mini]
keywords: [n8n workflow scrape trustpilot, tự động hóa marketing, tạo copy quảng cáo facebook bằng ai, phân tích đối thủ bằng ai, bright data api n8n]
---

# 🚀 **Tự Động Hóa Scrape Đánh Giá Trustpilot + AI Tạo Copy Quảng Cáo Facebook Hiệu Quả**

## **💡 Giải Pháp Cho Nỗi Đau Của Các Sếp Marketing**
Bạn đã bao giờ phải:
- **Tốn hàng giờ** để copy-paste hàng trăm đánh giá Trustpilot của đối thủ?
- **Không biết cách** chuyển feedback tiêu cực thành nội dung quảng cáo hấp dẫn?
- **Mất thời gian** phân tích điểm yếu của đối thủ để tối ưu chiến dịch?

Workflow này **tự động hóa toàn bộ quy trình** từ scrape dữ liệu đến tạo copy quảng cáo Facebook **chỉ trong vài phút**, giúp bạn:
✅ **Tiết kiệm 80% thời gian** so với cách làm thủ công
✅ **Nhận copy quảng cáo cá nhân hóa** từ feedback thực tế của khách hàng
✅ **Phân tích điểm yếu của đối thủ** một cách khoa học bằng AI
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Dữ liệu đánh giá Trustpilot** của đối thủ được scrape tự động, lưu vào Google Sheets.
- **Phân tích tự động** đánh giá 1-2 sao (tồi nhất) để tìm ra điểm yếu của đối thủ.
- **Tạo 3 bản copy quảng cáo Facebook** tối ưu hóa từ feedback tiêu cực, giúp tăng CTR và chuyển đổi.
- **Gửi báo cáo tự động** qua email cho team marketing, bao gồm:
  - Danh sách đánh giá tiêu cực chi tiết
  - Copy quảng cáo đề xuất
  - Link trực tiếp đến Google Sheets để phân tích sâu hơn
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản Bright Data** (để scrape Trustpilot):
   - [Đăng ký miễn phí Bright Data](https://brightdata.com/) (hoặc dùng API key đã có).
   - **Lưu ý**: Bright Data có giới hạn free tier, nên các sếp nên mua gói phù hợp nếu scrape nhiều dữ liệu.
2. **Tài khoản Google Sheets**:
   - Sử dụng **bản mẫu Google Sheets** của tác giả (liên kết dưới đây).
   - Cấp quyền cho n8n truy cập vào sheet.
3. **Tài khoản Gmail** (để gửi báo cáo tự động):
   - Cài đặt **OAuth 2.0** trong n8n để workflow có thể gửi email.
4. **API Key OpenAI** (để sử dụng GPT-4o-mini):
   - [Đăng ký API Key OpenAI](https://platform.openai.com/account/api-keys) (nếu chưa có).
   - Chọn mô hình **gpt-4o-mini** (rẻ và hiệu quả).
5. **Link Trustpilot của đối thủ**:
   - Điền vào form trigger của workflow.
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/3610](https://n8n.io/workflows/3610) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/3610) và paste vào **Import Workflow** trong n8n.
- **Cách 3**: Sử dụng **bản mẫu Google Sheets** của tác giả:
  1. [Click vào đây](https://docs.google.com/spreadsheets/d/1Zi758ds2_aWzvbDYqwuGiQNaurLgs-leS9wjLWWlbUU/edit?usp=sharing) để copy template.
  2. Điền **URL của sheet** vào node **Google Sheets - Adding All Reviews**.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **12 node**, các sếp cần chú ý cấu hình sau:

| **Node** | **Yêu Cầu Cần Chỉnh** | **Lưu Ý** |
|----------|----------------------|-----------|
| **On form submission - Discover Jobs** | Thêm **form trigger** để người dùng nhập: <br> - Link Trustpilot của đối thủ <br> - Thời gian scrape (30 ngày, 3 tháng, 6 tháng, 12 tháng) | Sử dụng **Google Forms** hoặc **n8n Form Trigger** để tạo UI đơn giản. |
| **HTTP Request - Post API call to Bright Data** | Điền **API Key Bright Data** và cấu hình header: <br> ```json { "Authorization": "Bearer YOUR_BRIGHT_DATA_API_KEY" } ``` | Tham khảo [Bright Data Docs](https://docs.brightdata.com/introduction) để lấy API key. |
| **Wait - Polling Bright Data** | Thiết lập thời gian chờ (ví dụ: 30 giây) để Bright Data hoàn thành scrape. | Nếu scrape nhiều dữ liệu, tăng thời gian chờ để tránh timeout. |
| **If - Checking status of Snapshot** | Kiểm tra trường `status` trong response Bright Data: <br> - Nếu `status === "ready"`, tiếp tục. <br> - Nếu `status === "processing"`, tiếp tục chờ. | Sử dụng **filter** để kiểm tra status chính xác. |
| **HTTP Request - Getting data from Bright Data** | Điền **URL endpoint** của Bright Data để lấy dữ liệu scrape. | Tham khảo [Bright Data API Docs](https://docs.brightdata.com/api/scraper-api). |
| **Filtering only bad reviews** | Lọc đánh giá có **rating = 1 hoặc 2 sao**. | Sử dụng **JSONPath** để lọc chính xác: `$[*]?.rating <= 2` |
| **Basic LLM Chain + OpenAI Chat Model** | Cấu hình **prompt** cho GPT-4o-mini: <br> ```json { "prompt": "Tôi có danh sách đánh giá tiêu cực của đối thủ. Hãy tạo 3 bản copy quảng cáo Facebook tối ưu hóa từ feedback này. Copy phải: <br> 1. Nhấn mạnh điểm yếu của đối thủ <br> 2. Đưa ra giải pháp của tôi <br> 3. Kêu gọi hành động mạnh mẽ <br> <br> Danh sách đánh giá: {{ $json['reviews'] }}", "model": "gpt-4o-mini" } ``` | **Tùy chỉnh prompt** để phù hợp với ngành hàng của bạn. |
| **Send Summary To Marketers** | Chọn **gmailOAuth2** và cấu hình email: <br> - **Người nhận**: Email của team marketing. <br> - **Tiêu đề email**: "Báo cáo phân tích đối thủ + Copy quảng cáo Facebook". <br> - **Nội dung email**: Gồm link Google Sheets + copy quảng cáo. | Sử dụng **HTML template** để email đẹp mắt. |
| **Google Sheets - Adding All Reviews** | Điền **URL sheet** và **tab name** (ví dụ: "Reviews"). | Sử dụng **mode: append** để thêm dữ liệu mới vào cuối sheet. |

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhập **link Trustpilot của một đối thủ** (ví dụ: [Trustpilot của Amazon](https://www.trustpilot.com/review/www.amazon.com)).
   - Chọn **thời gian scrape** (ví dụ: 30 ngày).
   - Chạy workflow và kiểm tra:
     - Dữ liệu có được scrape không?
     - AI có tạo copy quảng cáo không?
     - Email có được gửi không?
2. **Bật Active** sau khi test thành công.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::note[CÁCH TỐI ƯU HỢP]
1. **Kết hợp với Slack/Telegram**:
   - Thay vì gửi email, cấu hình node **Slack Webhook** hoặc **Telegram Bot** để thông báo kết quả ngay khi scrape xong.
   - **Cách làm**:
     ```json
     {
       "type": "httpRequest",
       "method": "POST",
       "url": "https://hooks.slack.com/services/YOUR_WEBHOOK_URL",
       "body": {
         "text": "🚀 Scrape Trustpilot hoàn tất! Copy quảng cáo đã được tạo. Link: {{ $json['sheetUrl'] }}"
       }
     }
     ```
2. **Lưu log scrape**:
   - Sử dụng node **StickyNote** hoặc **Google Drive** để lưu lịch sử scrape (ngày scrape, đối thủ, số lượng review).
3. **Tự động scrape định kỳ**:
   - Sử dụng **n8n Scheduler** để chạy workflow hàng tuần/monthly (ví dụ: scrape lại đánh giá của đối thủ mỗi tháng).
4. **Tùy chỉnh prompt AI**:
   - Nếu muốn tạo **copy cho email marketing** thay vì Facebook, thay đổi prompt:
     ```json
     "prompt": "Tôi có danh sách đánh giá tiêu cực của đối thủ. Hãy tạo 3 bản copy email marketing tối ưu hóa từ feedback này. Copy phải: <br> 1. Nhấn mạnh trải nghiệm tồi tệ của khách hàng <br> 2. Đưa ra giải pháp của tôi <br> 3. Kêu gọi hành động (CTA) mạnh mẽ <br> <br> Danh sách đánh giá: {{ $json['reviews'] }}"
     ```
5. **Phân tích sâu hơn với BigQuery**:
   - Nếu có **BigQuery**, thay thế Google Sheets bằng node **BigQuery** để phân tích dữ liệu lớn hơn.
:::

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** của các sếp marketing để tập trung vào chiến lược thay vì công việc thủ công. Bằng cách:
✔ **Scrape tự động** đánh giá Trustpilot của đối thủ
✔ **Phân tích điểm yếu** bằng AI
✔ **Tạo copy quảng cáo** tối ưu hóa từ feedback thực tế
✔ **Gửi báo cáo tự động** qua email/Slack

**Các sếp hãy áp dụng ngay** và bắt đầu **tạo quảng cáo Facebook hiệu quả hơn 300%** so với cách làm thủ công!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**🔗 Tài liệu tham khảo:**
- [Bright Data Docs](https://docs.brightdata.com/introduction)
- [OpenAI API Docs](https://platform.openai.com/docs/api-reference)
- [n8n Google Sheets Node](https://docs.n8n.io/integrations/builtins/nodes/base/googleSheets/)