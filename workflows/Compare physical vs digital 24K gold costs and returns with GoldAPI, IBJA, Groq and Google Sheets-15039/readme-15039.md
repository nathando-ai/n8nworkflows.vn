---
title: "🔍 So Sánh Giá Vàng 24K Thực Tế vs Điện Tử: Tự Động Hóa Đánh Giá Chi Phí & Tín Hiệu Thị Trường (n8n + AI)"
description: "Workflow tự động so sánh chi phí thực tế mua 1g vàng 24K giữa hình thức vật lý (IBJA) và điện tử (GoldAPI), kết hợp phân tích AI từ Groq và lưu báo cáo tự động lên Google Sheets. Giúp các nhà đầu tư và doanh nghiệp tiết kiệm thời gian lên đến 8h/tuần và đưa ra quyết định mua bán thông minh."
slug: "so-sanh-gia-vang-24k-thuc-te-va-dien-tu"
tags: [n8n, automation, market-research, ai-summarization, financial-analysis, gold-price-tracking]
keywords: [tự động hóa so sánh giá vàng, n8n workflow vàng 24k, AI phân tích thị trường vàng, so sánh chi phí vàng vật lý vs điện tử, tự động hóa báo cáo vàng]
---

# 🚀 **So Sánh Giá Vàng 24K Thực Tế vs Điện Tử: Giải Pháp Tự Động Hóa Đánh Giá Chi Phí & Tín Hiệu Thị Trường**

## **💡 Nỗi Đau Của Các Nhà Đầu Tư Vàng**
Mua bán vàng 24K là một trong những quyết định tài chính quan trọng nhất của nhiều gia đình và doanh nghiệp tại Việt Nam. Tuy nhiên, hiện nay các sếp phải mất **từ 2-3 tiếng/ngày** để:
- **So sánh giá** giữa vàng vật lý (IBJA) và vàng điện tử (GoldAPI) với các chi phí phụ thêm (thuế, phí làm, phí giao dịch).
- **Lọc tin tức thị trường** từ nguồn tin không chính thức, dễ bị lừa đảo.
- **Phân tích hiệu quả** mua bán dựa trên cảm xúc thị trường (bullish/bearish) mà không có công cụ hỗ trợ tự động.
- **Lưu trữ dữ liệu** để theo dõi xu hướng dài hạn mà phải thủ công nhập liệu.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động so sánh chi phí thực tế** (bao gồm thuế, phí làm, phí giao dịch) giữa vàng vật lý và điện tử.
✅ **Trích xuất tin tức thị trường** từ RSS và phân tích bằng AI để đưa ra **đánh giá "Buy/Wait"** và **điểm hiệu quả (1-100)**.
✅ **Lưu báo cáo hàng ngày** tự động lên Google Sheets với định dạng chuyên nghiệp.
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Giảm **8h/tuần** so sánh giá và phân tích thị trường thủ công.
- **Đánh giá chính xác**: So sánh **chi phí thực tế** (bao gồm thuế, phí làm, phí giao dịch) chứ không chỉ giá mặt bảng.
- **Quản lý rủi ro**: Nhận **đánh giá AI** về tình hình thị trường (Bullish/Bearish/Neutral) và **điểm hiệu quả** (1-100).
- **Lưu trữ dữ liệu**: Báo cáo tự động lưu vào Google Sheets, dễ theo dõi xu hướng dài hạn.
- **Cá nhân hóa**: Thiết lập cảnh báo cho giá vàng phù hợp với ngân sách của mình.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản GoldAPI**:
   - Đăng ký tại [GoldAPI.io](https://www.goldapi.io/) và lấy **API Key**.
   - Cần **$10/month** (miễn phí 30 ngày đầu).
2. **Tài khoản Groq API** (hoặc OpenAI/GPT-4):
   - Đăng ký tại [Groq](https://groq.com/) và lấy **API Key**.
   - Model sử dụng: `openai/gpt-oss-20b` (tương đương GPT-4 nhưng rẻ hơn).
3. **Tài khoản Google Sheets**:
   - Tạo một **Google Sheet mới** để lưu báo cáo.
   - Cấu hình **OAuth 2.0** trong n8n với quyền chỉnh sửa.
4. **Tài khoản IBJA** (không cần API, chỉ dùng để scraping):
   - Website: [ibjarates.com](https://ibjarates.com/).

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/15039](https://n8n.io/workflows/15039) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ [đây](https://github.com/n8n-io/workflows/blob/main/workflows/15039.json) và dán vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
##### **A. Cấu Hình API GoldAPI (Node: "Get Digital Price")**
- **Tham số Header**:
  ```json
  {
    "X-GoldAPI-API-KEY": "API_KEY_CỦA_BẠN"
  }
  ```
- **URL**: `https://www.goldapi.io/api/XAU/INR`
- **Lưu ý**: Nếu API Key sai hoặc hết hạn, workflow sẽ **dừng lại** tại node này.

##### **B. Cấu Hình Groq AI (Node: "Groq Chat Model")**
- **Credentials**: Chọn `groqApi` (đã cấu hình trước).
- **Model**: Đặt là `openai/gpt-oss-20b`.
- **Prompt Example** (nếu cần chỉnh sửa):
  ```json
  {
    "role": "user",
    "content": "Analyze the following gold price data and market news, then provide a sentiment score (Bullish/Bearish/Neutral) and efficiency score (1-100). Data: {{ $json["data"] }}"
  }
  ```

##### **C. Cấu Hình Google Sheets (Node: "Add Report")**
- **Credentials**: Chọn `googleSheetsOAuth2Api`.
- **Sheet Name**: Đặt tên sheet (ví dụ: `Báo cáo giá vàng hàng ngày`).
- **Range**: `Sheet1!A1` (hoặc tùy chỉnh).
- **Lưu ý**: Cần **quyền chỉnh sửa** sheet để workflow ghi dữ liệu.

##### **D. Cấu Hình Scraping IBJA (Node: "Extract Physical Price")**
- **URL**: `https://ibjarates.com/`
- **CSS Selector**: `#GoldRatesCompare999` (để trích xuất giá 1g vàng 24K).
- **Lưu ý**: Nếu website thay đổi cấu trúc HTML, cần **cập nhật selector**.

##### **E. Node "Comparator" (Code)**
- **Lógica tính toán**:
  - **Vàng điện tử**: Giá API + 3% GST + 3% phí platform.
  - **Vàng vật lý**: Giá IBJA + 3% GST + 8% phí làm.
  - **Kết quả**: So sánh và tính **sự chênh lệch (arbitrage)**.

##### **F. Node "AI Agent"**
- **Input**: Dữ liệu từ `Comparator` + tin tức thị trường.
- **Output**: JSON với:
  ```json
  {
    "sentiment": "Bullish/Neutral/Bearish",
    "efficiencyScore": 85,
    "recommendation": "Buy/Wait/Sell"
  }
  ```

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhấn **Execute Workflow** và kiểm tra:
     - Giá vàng điện tử vs vật lý có hợp lý không?
     - AI có phân tích sentiment đúng không?
     - Dữ liệu có ghi vào Google Sheets không?
2. **Bật Active**:
   - Sau khi test thành công, **bật Active** và chọn **Manual Trigger** (hoặc tự động hóa bằng cron).

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Thêm Cảnh Báo Slack/Telegram**:
   - Sử dụng node `n8n-nodes-base.slack` hoặc `n8n-nodes-base.telegram` để gửi **tin nhắn cảnh báo** khi giá vàng đạt ngưỡng mong muốn.
   - **Ví dụ**:
     ```json
     {
       "text": `🚨 Giá vàng điện tử đã xuống dưới {{ $json["digitalPrice"] }} INR! Giá vật lý: {{ $json["physicalPrice"] }} INR. Sentiment: {{ $json["sentiment"] }}`
     }
     ```

2. **Lưu Log Dữ Liệu**:
   - Thêm node `n8n-nodes-base.fileSystem` để lưu **tất cả báo cáo** vào một folder trên VPS.

3. **Tự Động Hóa Theo Dõi Giá**:
   - Sử dụng **Cron Job** (n8n Pro) để chạy workflow **hàng ngày lúc 9h sáng** (thời gian mở cửa thị trường vàng).

4. **Kết Hợp với Notion/ClickUp**:
   - Thay vì Google Sheets, các sếp có thể lưu báo cáo vào **Notion** hoặc **ClickUp** bằng node `n8n-nodes-base.notion`.

5. **Phân Tích Xu Hướng Dài Hạn**:
   - Sử dụng node `n8n-nodes-base.aggregate` để **tính trung bình giá vàng trong 30 ngày** và vẽ biểu đồ.

---

### 📌 **Kết Luận**
Workflow này không chỉ **giải phóng thời gian** cho các sếp khỏi công việc thủ công mệt mỏi, mà còn **cung cấp quyết định đầu tư thông minh** dựa trên dữ liệu thực tế và phân tích AI. Bằng cách **so sánh chi phí thực tế** (bao gồm thuế, phí làm) và **đánh giá tình hình thị trường**, các sếp có thể:
✔ **Mua vàng ở thời điểm hợp lý nhất**.
✔ **Tránh rủi ro từ tin tức không chính thức**.
✔ **Theo dõi xu hướng dài hạn một cách tự động**.

**Hành động ngay hôm nay**:
1. **Import workflow** và cấu hình API.
2. **Test run** để đảm bảo dữ liệu chính xác.
3. **Bật Active** và bắt đầu tự động hóa!

---
**💬 Cần hỗ trợ thêm?**
- Trả lời comment dưới đây hoặc liên hệ **WeblineIndia** (tác giả workflow) qua [website](https://www.weblineindia.com/).
- **Góp ý cải tiến**: Các sếp có thể chia sẻ ý kiến để workflow được tối ưu hơn!