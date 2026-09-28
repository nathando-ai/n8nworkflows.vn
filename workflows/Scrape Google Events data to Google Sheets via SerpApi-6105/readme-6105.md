---
title: "🔍 **Tự Động Hóa Scrape Dữ Liệu Sự Kiện Google Sang Google Sheets Với SerpApi (N8n)**"
description: "Workflow tự động hóa scrape dữ liệu sự kiện từ Google Events sang Google Sheets chỉ trong 30-60 giây, giúp các sếp tiết kiệm thời gian nghiên cứu thị trường và phân tích xu hướng sự kiện một cách hiệu quả. Không cần code, chỉ cần n8n và SerpApi!"
slug: "tieu-dong-hoa-scrape-du-lieu-suckien-google-sang-google-sheets"
tags: [n8n, automation, market-research, serpapi, google-sheets, no-code]
keywords: [n8n workflow scrape google events, tự động hóa nghiên cứu thị trường, scrape sự kiện google sang google sheets, serpapi n8n, tự động hóa dữ liệu sự kiện]
---

# 🚀 **Tự Động Hóa Scrape Dữ Liệu Sự Kiện Google Sang Google Sheets Với SerpApi**

### **Giải pháp cho các sếp muốn nghiên cứu thị trường nhanh chóng mà không cần viết code**
Hiện nay, việc nghiên cứu sự kiện diễn ra tại một khu vực cụ thể (như các hội nghị, triển lãm, sự kiện văn hóa) thường phải mất nhiều thời gian để tìm kiếm thủ công trên Google. Các sếp phải tra cứu từng trang, sao chép dữ liệu vào Excel, và sau đó phân tích. **Workflow này tự động hóa toàn bộ quy trình đó chỉ trong vài giây!**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Scrape và lưu trữ dữ liệu sự kiện chỉ trong **30-60 giây** thay vì nhiều giờ làm thủ công.
- **Dữ liệu chính xác và cập nhật**: Không lo bỏ lỡ sự kiện mới vì hệ thống tự động cập nhật.
- **Dễ dàng phân tích**: Dữ liệu được lưu vào Google Sheets với định dạng rõ ràng, sẵn sàng cho báo cáo và phân tích.
- **Tùy chỉnh linh hoạt**: Thay đổi vị trí, chủ đề hoặc số lượng sự kiện một cách dễ dàng.
- **Hoạt động liên tục**: Sử dụng n8n self-hosted để chạy workflow 24/7 mà không cần can thiệp.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản SerpApi**:
   - [Đăng ký SerpApi](https://serpapi.com/) và lấy **API Key**.
   - Workflow sử dụng **gói "google_events"** để scrape dữ liệu sự kiện.
   - 💡 *Lưu ý*: SerpApi có giới hạn request, nên các sếp nên chọn gói phù hợp với nhu cầu.

2. **Tài khoản Google Sheets**:
   - Tạo một **Google Sheet mới** và chia sẻ với n8n bằng **OAuth 2.0**.
   - Link mẫu sheet: [Google Events API](https://docs.google.com/spreadsheets/d/1DQo3tI8yKzCbLn-DWN2hureHgwj1XxvM1ogES1_77ts/edit?usp=sharing).
   - **Lưu ý**: Các sếp phải **làm sao chép (Make a Copy)** sheet này để tránh bị lỗi quyền hạn.

3. **n8n Workflow**:
   - Cài đặt n8n trên máy chủ hoặc VPS (self-hosted) để chạy workflow liên tục.

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/6105).
- Mở **n8n Editor** → Nhấn **Import** → Chọn file JSON vừa tải.
- Hoặc copy toàn bộ JSON và dán vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **5 node chính**, các sếp cần cấu hình như sau:

##### **🔹 Node 1: Manual Trigger**
- **Tên node**: Manual Trigger
- **Lưu ý**: Node này dùng để kích hoạt workflow thủ công. Các sếp có thể thay thế bằng **Schedule Trigger** (nếu muốn chạy tự động định kỳ).

##### **🔹 Node 2: Set Search Parameters (Set)**
- **Tên node**: Set Search Parameters
- **Cấu hình**:
  - **Query**: Thay đổi từ `"Events in Texas"` thành **vị trí/topic** của các sếp (ví dụ: `"Events in Vietnam"`, `"Tech Conferences in Ho Chi Minh"`).
  - **Total Events**: Đặt số lượng sự kiện muốn scrape (mặc định là **20**).
  - **Start Position**: Đặt từ **0** để bắt đầu từ trang đầu tiên.
  - 💡 *Gợi ý*: Nếu muốn scrape nhiều hơn 20 sự kiện, tăng giá trị này và điều chỉnh **pagination** ở node tiếp theo.

##### **🔹 Node 3: SerpApi Events Request (HTTP Request)**
- **Tên node**: SerpApi Events Request
- **Cấu hình**:
  - **URL**: `https://serpapi.com/search`
  - **Method**: `GET`
  - **Headers**:
    - `X-API-KEY`: Điền **API Key** của SerpApi.
  - **Query Parameters**:
    - `engine`: `google_events`
    - `hl`: `en` (ngôn ngữ tiếng Anh)
    - `gl`: `us` (địa chỉ quốc gia)
    - `q`: Điền từ khóa từ **Node 2** (ví dụ: `"Events in Texas"`).
    - `num`: Số lượng sự kiện trên mỗi trang (mặc định **10**).
    - `start`: Vị trí bắt đầu (mặc định **0**).
  - **Credentials**: Chọn `httpQueryAuth` (đã được tạo khi setup SerpApi).

##### **🔹 Node 4: Process & Flatten Events (Code)**
- **Tên node**: Process & Flatten Events
- **Lưu ý**: Node này **không cần chỉnh sửa** vì đã được tối ưu hóa để:
  - **Flatten** dữ liệu sự kiện (loại bỏ cấu trúc nhúng).
  - **Thêm query** vào mỗi sự kiện (giúp phân tích dễ dàng).
  - **Gộp** dữ liệu từ nhiều request (nếu scrape nhiều trang).

##### **🔹 Node 5: Save to Google Sheets (Google Sheets)**
- **Tên node**: Save to Google Sheets
- **Cấu hình**:
  - **Credentials**: Chọn `googleSheetsOAuth2Api` (đã được setup khi chia sẻ sheet với n8n).
  - **Spreadsheet ID**: Điền **ID của sheet** (tìm trong URL của sheet, ví dụ: `1DQo3tI8yKzCbLn-DWN2hureHgwj1XxvM1ogES1_77ts`).
  - **Sheet Name**: Đặt là `"Sheet1"` (hoặc tên tab của các sếp).
  - **Operation**: Chọn `append` (thêm dữ liệu vào cuối sheet).
  - **Range**: Điền `Sheet1!A1` (để dữ liệu bắt đầu từ ô A1).
  - **Data**: Chọn `json` từ **Node 4** (dữ liệu đã được xử lý).

---

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Nhấn **Run Workflow** để kiểm tra dữ liệu scrape được không.
   - Kiểm tra **Google Sheets** xem dữ liệu đã được lưu chưa.
2. **Bật Active**:
   - Sau khi test thành công, chuyển workflow sang **Active**.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tự động hóa định kỳ**:
   - Thay thế **Manual Trigger** bằng **Schedule Trigger** để scrape dữ liệu hàng ngày/tuần.
   - Ví dụ: Scrape sự kiện mới vào mỗi sáng thứ 2.

2. **Gửi báo cáo tự động**:
   - Kết hợp với **Slack/Email** để thông báo khi có sự kiện mới.
   - Sử dụng **n8n-nodes-base.slack** hoặc **n8n-nodes-base.email** để gửi tin nhắn.

3. **Lưu log hoạt động**:
   - Thêm **n8n-nodes-base.manualTrigger** hoặc **n8n-nodes-base.dateTime** để theo dõi thời gian scrape.
   - Lưu log vào **Google Sheets** hoặc **Google Drive** để phân tích lịch sử.

4. **Tăng cường dữ liệu**:
   - Scrape thêm thông tin từ **Google Maps** (địa chỉ chi tiết) hoặc **Eventbrite API** (nếu cần).
   - Sử dụng **n8n-nodes-base.httpRequest** để gọi API khác.

5. **Tối ưu SerpApi**:
   - Nếu scrape nhiều sự kiện, tăng **delay** giữa các request để tránh bị chặn IP.
   - Sử dụng **gói SerpApi Pro** nếu cần scrape nhiều hơn 100 sự kiện/ngày.

---

### 📌 **Kết luận**
Workflow này giúp các sếp **tự động hóa scrape dữ liệu sự kiện từ Google sang Google Sheets chỉ trong vài giây**, tiết kiệm thời gian và nâng cao hiệu quả nghiên cứu thị trường. **Không cần code, chỉ cần n8n và SerpApi!**

👉 **Hãy thử ngay**:
1. Import workflow.
2. Cấu hình **SerpApi Key** và **Google Sheets OAuth**.
3. Nhấn **Run** và xem dữ liệu xuất hiện trong sheet!

**Nếu có thắc mắc, hãy để lại comment bên dưới hoặc liên hệ với tác giả [Naveen Choudhary](https://cal.com/nickchoudhary/30min) để được hỗ trợ!** 🚀