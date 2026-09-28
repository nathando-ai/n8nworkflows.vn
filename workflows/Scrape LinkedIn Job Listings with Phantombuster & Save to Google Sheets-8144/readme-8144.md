---
title: "🚀 Tự Động Hoàn Thành Scrape LinkedIn Job Listings Với Phantombuster & Lưu Trữ Trên Google Sheets (Không Cần Code)"
description: "Workflow tự động hóa scrape danh sách việc làm LinkedIn hàng tuần, xử lý dữ liệu và lưu trữ vào Google Sheets với định dạng chuẩn - tiết kiệm 10+ giờ công mỗi tháng cho các sếp HR và market research."
slug: "scrape-linkedin-job-listings-phantombuster-google-sheets"
tags: [n8n, automation, market-research, no-code, phantombuster, google-sheets, ai-agent]
keywords: [scrape linkedin jobs n8n, tự động hóa tìm việc làm linkedin, lưu dữ liệu google sheets, phantombuster api, market research tự động]
---

# 🚀 **Scrape LinkedIn Job Listings Với Phantombuster & Lưu Trữ Trên Google Sheets**

### **Giải pháp tự động hóa cho các sếp HR, Recruiter và Market Researcher**
Bạn đã từng phải **quét thủ công hàng trăm trang LinkedIn** để tìm kiếm thông tin việc làm mới nhất? Hay phải **lặp lại công việc này hàng tuần** để theo dõi xu hướng thị trường? Với workflow này, các sếp sẽ **tự động scrape danh sách việc làm LinkedIn hàng tuần**, xử lý dữ liệu và lưu trữ vào Google Sheets với định dạng chuẩn - **không cần viết một dòng code nào!**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ công/tháng**: Không cần quét LinkedIn thủ công hàng tuần.
- **Dữ liệu chuẩn hóa**: Job data được format vào các cột: **Tên Công Ty, Tiêu Đề Việc Làm, Mô Tả, Link, Ngày Đăng, Địa Điểm, Loại Hợp Đồng**.
- **Theo dõi lịch sử**: Mỗi scrape được ghi ngày tháng, giúp phân tích xu hướng thị trường.
- **Hoạt động tự động**: Workflow chạy **tự động hàng tuần** vào 9h sáng (thời gian có thể điều chỉnh).
- **Kết hợp với AI**: Dữ liệu có thể được phân tích thêm bằng **LLM** (OpenAI, Mistral...) để trích xuất thông tin chi tiết.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Phantombuster**:
   - API Key của Phantombuster (đăng ký tại [phantombuster.com](https://phantombuster.com/)).
   - **Container ID** của scraper LinkedIn Job Listings (có thể tạo mới hoặc sử dụng container đã có).
2. **Google Sheets OAuth2**:
   - **Tài khoản Google Workspace** (hoặc cá nhân) để kết nối với Google Sheets.
   - **File Google Sheets** có 2 sheet:
     - **Companies Sheet**: Danh sách công ty với cột `Status = "Pending"` (để workflow biết scrape những công ty nào).
     - **Job Results Sheet**: Sheet để lưu kết quả scrape (các sếp có thể tạo mới hoặc sử dụng sheet đã có).
3. **VPS n8n** (nếu không dùng n8n Cloud):
   - Đã cài đặt và chạy n8n trên VPS (hướng dẫn tại [docs.n8n.io](https://docs.n8n.io/)).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/8144](https://n8n.io/workflows/8144) hoặc copy JSON từ canvas.
- **Import vào n8n Editor**:
  - Mở n8n Editor → Nhấn `+` → Chọn `Import Workflow` → Dán JSON hoặc tải file `.json`.
  - **Tên workflow**: Giữ nguyên hoặc đổi thành `Scrape LinkedIn Jobs Weekly`.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
##### **🔹 Node 1: ⏰ Schedule Trigger**
- **Thời gian chạy**: Đặt thành **9:00 AM hàng tuần** (thời gian UTC hoặc theo múi giờ của các sếp).
- **Lưu ý**: Nếu dùng VPS ở Việt Nam, hãy chọn **múi giờ UTC+7**.

##### **🔹 Node 2 & 3: 🚀 Trigger Phantombuster Scraper & ⏳ Wait for Scraper to Finish**
- **Phantombuster API Key**:
  - Trong node `Trigger Phantombuster Scraper`, đi đến tab **Credentials** → Chọn `phantombusterApi` (nếu chưa có, tạo mới tại `Settings → Credentials`).
  - Điền **API Key** từ Phantombuster vào `apiKey`.
- **Container ID**:
  - Trong cùng node, tìm `containerId` → Điền **ID của container LinkedIn Job Listings** của các sếp (có thể tìm trong Phantombuster Dashboard).
- **Thời gian chờ**:
  - Node `Wait for Scraper to Finish` có thời gian mặc định **3 phút**. Nếu scraper chạy lâu hơn, tăng thời gian lên **5-10 phút**.

##### **🔹 Node 4: 📄 Read Companies Sheet**
- **Google Sheets Credentials**:
  - Đi đến `Settings → Credentials` → Tạo mới `googleSheetsOAuth2Api`.
  - Theo hướng dẫn OAuth2 để kết nối với Google Sheets.
- **Sheet Name**:
  - Điền tên sheet chứa danh sách công ty (ví dụ: `Companies`).
  - **Lọc dữ liệu**: Workflow sẽ tự động lấy chỉ những hàng có `Status = "Pending"`.

##### **🔹 Node 5: 🛠️ Format Job Data**
- **Không cần chỉnh sửa**: Node này tự động format dữ liệu theo cấu trúc chuẩn (Company Name, Job Title, Description, Link, Date Posted, Location, Employment Type).
- **Lưu ý**: Nếu dữ liệu từ Phantombuster không đầy đủ, các sếp có thể mở node này và chỉnh sửa **JSON Path** trong tab **Advanced**.

##### **🔹 Node 6: 📊 Write to Results Sheet**
- **Sheet Name**:
  - Điền tên sheet lưu kết quả (ví dụ: `Job Results`).
  - **Chọn `append`** để thêm dữ liệu mới vào cuối sheet.
- **Header Row**:
  - Đảm bảo sheet có **header row** (cột tiêu đề) để workflow biết định dạng dữ liệu.

#### **3. Kích hoạt ⚡️**
- **Test Run**:
  - Nhấn `Run Workflow` để kiểm tra.
  - Kiểm tra **Google Sheets** xem dữ liệu có được append đúng không.
- **Bật Active**:
  - Sau khi test thành công, nhấn `Active` để workflow chạy tự động hàng tuần.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với AI để phân tích dữ liệu**:
   - Sau khi scrape xong, các sếp có thể thêm node **OpenAI** hoặc **Mistral** để:
     - **Trích xuất skill yêu cầu** từ mô tả việc làm.
     - **Phân loại công việc** theo ngành nghề.
     - **Tự động gửi báo cáo** qua Slack/Email với phân tích xu hướng.

2. **Lưu log scrape**:
   - Thêm node **Google Sheets** hoặc **Notion** để ghi lại **lịch sử scrape** (ngày scrape, số lượng job, công ty nào đã được update status).

3. **Gửi báo cáo định kỳ**:
   - Sử dụng node **Email** hoặc **Slack** để tự động gửi **báo cáo hàng tuần** với:
     - Danh sách công ty mới có việc làm.
     - Số lượng việc làm tăng/giảm so với tuần trước.

4. **Tối ưu scraper**:
   - Nếu Phantombuster có **container khác** (ví dụ: scrape theo keyword), các sếp có thể thay đổi `containerId` trong node `Trigger Phantombuster Scraper`.

5. **Xử lý lỗi**:
   - Thêm node **Set** sau `Wait for Scraper` để kiểm tra **status code** của API Phantombuster. Nếu lỗi, có thể gửi thông báo qua **Slack/Email**.

---

### 📌 **Kết luận**
Workflow này **giải phóng các sếp khỏi công việc quét LinkedIn thủ công**, đồng thời **cung cấp dữ liệu sạch và chuẩn hóa** để phân tích thị trường. Với **tỉ lệ tự động hóa 100%**, các sếp có thể tập trung vào **strategy recruitment** hoặc **market research** thay vì làm việc lặp lại.

**Bắt đầu ngay!**
1. Import workflow vào n8n.
2. Cấu hình **Phantombuster API Key** và **Google Sheets**.
3. Bật **Schedule Trigger** và để workflow làm việc cho các sếp.

🚀 **Hãy tự động hóa hôm nay - tiết kiệm thời gian và tăng hiệu suất!**

---
**💡 Cần hỗ trợ?**
- Liên hệ với **Avkash Kakdiya** (Founder iTechNotion) qua [LinkedIn](https://www.linkedin.com/in/avkashkakdiya/) hoặc [website](https://itechnotion.com/).
- **Cộng đồng n8n Việt Nam**: [Facebook Group](https://www.facebook.com/groups/n8nvietnam/) | [Discord](https://discord.gg/n8n).