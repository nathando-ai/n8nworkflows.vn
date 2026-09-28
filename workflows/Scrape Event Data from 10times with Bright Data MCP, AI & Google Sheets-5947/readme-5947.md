---
title: "🚀 Tự Động Hoá Scrape Dữ Liệu Sự Kiện 10times Với AI & Google Sheets (Không Cần Code)"
description: "Workflow tự động hóa scrape dữ liệu từ trang 10times.com (như danh sách exhibitors, feedback, venue) bằng AI Agent + Bright Data MCP, sau đó tự động lưu vào Google Sheets để phân tích thị trường, nghiên cứu đối thủ hoặc xây dựng leads. Giúp tiết kiệm 10+ giờ/tháng cho các sếp marketing & sales."
slug: "tieu-dong-hoa-scrape-10times-ai-google-sheets"
tags: [n8n, automation, web-scraping, ai-agent, google-sheets, bright-data, market-research]
keywords: [n8n workflow scrape 10times, tự động hóa scrape sự kiện, AI Agent Bright Data, lưu dữ liệu vào Google Sheets, nghiên cứu thị trường sự kiện, tự động hóa không code]
---

# 🚀 **Scrape Dữ Liệu Sự Kiện 10times Tự Động Với AI & Google Sheets**

## **💡 Giải Pháp Cho Nỗi Đau Của Các Sếp Marketing & Sales**
Bạn đã từng phải:
- **Tốn thời gian** thủ công copy-paste danh sách exhibitors, feedback từ sự kiện trên 10times.com?
- **Khó khăn** khi website block bot truyền thống, dẫn đến dữ liệu không đầy đủ?
- **Không biết** cách tự động hóa để theo dõi xu hướng sự kiện, đối thủ cạnh tranh?
- **Mất hiệu quả** vì dữ liệu rải rác, không được cấu trúc hóa?

**Workflow này giải quyết tất cả!** Nó tự động scrape dữ liệu từ trang 10times.com (như danh sách exhibitors, feedback, venue, featured events) bằng **AI Agent + Bright Data MCP** (mô phỏng thiết bị di động để tránh bị block), sau đó **tự động lưu vào Google Sheets** với định dạng sạch sẽ. Dữ liệu này có thể được sử dụng để:
✅ **Nghiên cứu thị trường** (xem xu hướng sự kiện nào hot)
✅ **Xây dựng leads** (lấy thông tin exhibitors để outreach)
✅ **Theo dõi đối thủ** (biết họ tham gia sự kiện nào)
✅ **Tối ưu hóa chiến dịch marketing** (lựa chọn sự kiện phù hợp)

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tháng** so với scrape thủ công.
- **Dữ liệu chính xác & đầy đủ** (AI + MCP tránh bị block).
- **Cấu trúc hóa tự động** (dữ liệu được phân loại thành `categories`, `venues`, `feedback`...).
- **Hoạt động liên tục** (cấu hình chạy hàng ngày/tuần).
- **Sẵn sàng cho phân tích** (dữ liệu lưu vào Google Sheets, có thể export Excel/Power BI).
- **Không cần kỹ thuật** (cấu hình đơn giản, chỉ cần drag & drop).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Bright Data MCP** (để scrape website mà không bị block):
   - [Tạo tài khoản Bright Data](https://get.brightdata.com/1tndi4600b25) (sử dụng mã **1tndi4600b25** để hỗ trợ tạo nội dung miễn phí).
   - **Lưu ý**: Các sếp cần **API Key** của Bright Data MCP (được gọi là `mcpClientApi` trong workflow).

2. **Tài khoản Google Sheets** (để lưu dữ liệu scrape):
   - Tạo một **Google Sheet mới** và chia sẻ cho workflow (sẽ tự động append dữ liệu).

3. **Tài khoản OpenAI API** (để AI Agent hoạt động):
   - [Tạo tài khoản OpenAI](https://platform.openai.com/) và lấy **API Key** (được gọi là `openAiApi` trong workflow).
   - **Model**: Workflow sử dụng `gpt-4o-mini` (miễn phí, hiệu suất cao).

4. **URL của sự kiện 10times** (ví dụ: `https://10times.com/ces/exhibitors`).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/5947](https://n8n.io/workflows/5947) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/5947) và paste vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow gồm **9 node**, các sếp cần chú ý cấu hình các node sau:

##### **🕒 Schedule Scraper (Trigger)**
- **Cấu hình**:
  - Chọn **Interval** (ví dụ: chạy hàng ngày lúc 8h sáng).
  - Hoặc chọn **Manual** (để test trước khi chạy tự động).
- **Lưu ý**: Nếu muốn chạy định kỳ, các sếp có thể chỉnh lại thời gian phù hợp với nhu cầu.

##### **⚙️ Input URL & Params**
- **Cấu hình**:
  - Điền **URL của sự kiện 10times** (ví dụ: `https://10times.com/ces/exhibitors`).
  - **Customize Prompt** (nếu muốn scrape thông tin cụ thể hơn, ví dụ: chỉ lấy exhibitors từ một danh mục nhất định).
- **Lưu ý**:
  - Nếu muốn scrape nhiều sự kiện, các sếp có thể **lưu URL vào một danh sách** (ví dụ: Google Sheets hoặc Airtable) và kết nối với node này bằng **Webhook** hoặc **HTTP Request**.

##### **🤖 Bright Data AI Agent**
- **Cấu hình**:
  - **Tool**: `mcpClientTool` (đã được cấu hình sẵn với `mcpClientApi`).
  - **Prompt**: Workflow đã tự động cấu hình để scrape thông tin như:
    ```json
    {
      "categories": [],
      "featured_events": [],
      "attendee_feedback": [],
      "venues": []
    }
    ```
  - **Lưu ý**: Nếu muốn scrape thông tin khác, các sếp có thể chỉnh sửa **prompt** trong node này.

##### **🕷️ MCP Scraper: 10times**
- **Cấu hình**:
  - **Credentials**: Chọn `mcpClientApi` (đã được cấu hình trong n8n).
  - **Lưu ý**: Nếu Bright Data MCP bị lỗi, các sếp cần **kiểm tra API Key** và **quota** (Bright Data có giới hạn scrape/month).

##### **📥 Save to Google Sheets**
- **Cấu hình**:
  - **Credentials**: Chọn `googleSheetsOAuth2Api`.
  - **Sheet Name**: Điền tên **Google Sheet** muốn lưu dữ liệu (ví dụ: `10times_scraped_data`).
  - **Range**: Chọn **Sheet mới** hoặc **Sheet đã tồn tại** (workflow sẽ tự động append dữ liệu).
  - **Lưu ý**:
    - Các sếp cần **chia sẻ Google Sheet** cho n8n (quyền **Editor**).
    - Cột đầu tiên sẽ tự động được đặt tên là `type` (phân loại dữ liệu).

##### **🧠 Agent Memory Model & OpenAI Chat Model**
- **Cấu hình**:
  - **Credentials**: Chọn `openAiApi`.
  - **Model**: Đã sử dụng `gpt-4o-mini` (không cần chỉnh sửa).
  - **Lưu ý**: Nếu OpenAI API bị lỗi, các sếp cần **kiểm tra API Key** và **quota**.

##### **🧾 Auto-fixing Output Parser & Structured Output Parser**
- **Cấu hình**:
  - Workflow đã tự động cấu hình để **chuyển dữ liệu thô** thành **JSON sạch**.
  - **Lưu ý**: Nếu dữ liệu scrape không đúng định dạng, các sếp có thể chỉnh sửa **schema** trong node này.

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Chạy **Manual Execution** để kiểm tra dữ liệu scrape có đúng không.
  - Kiểm tra **Google Sheets** xem dữ liệu đã được lưu chưa.
- **Bật Active**:
  - Sau khi test thành công, **bật Active** cho workflow.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Scrape Nhiều Sự Kiện Tự Động**:
   - Lưu danh sách URL sự kiện vào **Google Sheets** hoặc **Airtable**.
   - Sử dụng **node `set`** kết hợp với **loop** để scrape tất cả sự kiện.

2. **Gửi Báo Cáo Định Kỳ**:
   - Kết nối với **Slack/Telegram** để nhận thông báo khi scrape hoàn tất.
   - Sử dụng **node `slack`** hoặc **`telegram`** để gửi tin nhắn tự động.

3. **Lưu Log Dữ Liệu**:
   - Kết nối với **Google Drive** hoặc **AWS S3** để lưu bản sao dữ liệu scrape.
   - Sử dụng **node `googleDrive`** hoặc **`awsS3`** để backup.

4. **Tối Ưu Hóa AI Agent**:
   - Nếu muốn scrape thông tin cụ thể hơn, chỉnh sửa **prompt** trong node `Bright Data AI Agent`.
   - Ví dụ: Nếu muốn lấy **feedback từ exhibitors**, cập nhật prompt như sau:
     ```json
     {
       "task": "Extract all attendee feedback from the exhibitors section",
       "output_format": {
         "feedback": [],
         "exhibitor_name": "",
         "event_name": ""
       }
     }
     ```

5. **Xây Dựng Dashboard**:
   - Export dữ liệu từ Google Sheets vào **Power BI** hoặc **Tableau** để tạo **dashboard** theo dõi xu hướng sự kiện.

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp marketing & sales muốn:
✔ **Tiết kiệm thời gian** scrape dữ liệu từ 10times.com.
✔ **Tránh bị block** nhờ Bright Data MCP + AI Agent.
✔ **Lưu dữ liệu sạch** vào Google Sheets để phân tích.
✔ **Tự động hóa hoàn toàn** (không cần code).

**Hành động ngay!**
1. **Import workflow** vào n8n của mình.
2. **Cấu hình các node** theo hướng dẫn trên.
3. **Bật Active** và bắt đầu scrape dữ liệu tự động hàng ngày!

**Nếu gặp vấn đề**, các sếp có thể liên hệ với tác giả Yaron Been qua:
- [LinkedIn](https://www.linkedin.com/in/yaronbeen/)
- [YouTube](https://www.youtube.com/@YaronBeen/videos)

---
**🎁 Bonus**: Nếu các sếp sử dụng **Bright Data MCP** qua link này, tác giả sẽ nhận một phần commission nhỏ để hỗ trợ tạo nội dung miễn phí hơn!
👉 [Tạo tài khoản Bright Data](https://get.brightdata.com/1tndi4600b25)