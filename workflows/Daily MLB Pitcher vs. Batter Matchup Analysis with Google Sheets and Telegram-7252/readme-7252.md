---
title: "🏟️ **Tự Động Hóa Phân Tích Trận Đấu MLB: So Sánh Pitcher vs. Batter Hàng Ngày Với Google Sheets & Telegram**"
description: "Workflow tự động hóa phân tích các trận đấu MLB hàng ngày, lọc ra các cặp đấu pitcher vs. batter có hiệu suất cao nhất (ERA > 3.33, OPS cao nhất), và gửi báo cáo định kỳ lên Google Sheets và Telegram. Giúp các sếp MLB fan hoặc nhà đầu tư thể thao tiết kiệm thời gian và tối ưu hóa quyết định theo dữ liệu thực tế."
slug: "tieu-dong-hoa-phan-tich-tran-dau-mlb-pitcher-vs-batter"
tags: [n8n, automation, no-code, mlb, google-sheets, telegram-bot, data-analysis, sports-analytics]
keywords: [tự động hóa MLB, phân tích pitcher vs batter, google sheets automation, telegram bot n8n, workflow MLB stats, tự động hóa thể thao]
---

# 🚀 **Tự Động Hóa Phân Tích Trận Đấu MLB: Pitcher vs. Batter Hàng Ngày**

### **Giải pháp cho ai?**
Các sếp **MLB fan**, nhà đầu tư thể thao, hoặc những người yêu thích **phân tích dữ liệu thể thao** đang mệt mỏi với việc **tìm kiếm thủ công** thông tin về các trận đấu MLB hàng ngày, so sánh hiệu suất của pitcher và batter, hoặc theo dõi các cặp đấu có tiềm năng cao nhất? **Workflow này sẽ tự động hóa toàn bộ quá trình** cho bạn!

Bằng cách kết hợp **API MLB Stats API**, **Google Sheets** và **Telegram Bot**, workflow này sẽ:
✅ **Lấy lịch trận MLB hàng ngày** (kèm pitcher dự kiến và lineup).
✅ **Tải dữ liệu thống kê toàn mùa** của tất cả các cầu thủ tham gia.
✅ **Phân tích và lọc** ra **top 27 cặp đấu pitcher vs. batter** có ERA > 3.33 và OPS cao nhất.
✅ **Sắp xếp theo thời gian bắt đầu trận** (ET) và ghi dữ liệu vào **Google Sheets**.
✅ **Gửi báo cáo định kỳ** lên **Telegram** với **top 21 batter có OPS cao nhất**.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để tránh giới hạn của phiên bản cloud.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần tìm kiếm thủ công dữ liệu trên MLB.com hoặc các trang thống kê.
- **Dữ liệu chính xác và cập nhật**: Lấy trực tiếp từ **MLB Stats API**, không phụ thuộc vào nguồn thứ ba.
- **Tối ưu hóa quyết định**: Nhận **top cặp đấu pitcher vs. batter** có hiệu suất cao nhất mỗi ngày.
- **Theo dõi dễ dàng**: Dữ liệu được ghi vào **Google Sheets** và gửi báo cáo lên **Telegram** định kỳ.
- **Hoạt động liên tục**: Workflow chạy tự động hàng ngày, kể cả khi các sếp **ngủ hoặc đi làm**.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets**:
   - Một **Google Sheet** để lưu trữ dữ liệu (các sếp có thể tạo một sheet mới và chia sẻ cho n8n).
   - **OAuth 2.0 Credentials** cho Google Sheets (cài đặt trong n8n dưới **Credentials** → **Add New Credential** → **Google Sheets OAuth2 API**).
   - **Tên tab** trong Google Sheet (các sếp sẽ nhập vào node **Update Your Sheet**).

2. **Telegram Bot**:
   - Một **bot Telegram** để gửi báo cáo (các sếp tạo bot trên [@BotFather](https://t.me/BotFather) và lấy **API Token**).
   - **Chat ID** của nhóm hoặc cá nhân muốn nhận báo cáo (các sếp có thể lấy bằng cách gửi tin nhắn cho bot và copy link chat, sau đó trích xuất Chat ID từ URL).

3. **API Key (nếu cần)**:
   - Workflow sử dụng **MLB Stats API** (miễn phí cho các sếp có nhu cầu phân tích cơ bản). Các sếp không cần API Key riêng vì workflow đã tích hợp URL API công khai.

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Tải file JSON từ [link gốc](https://n8n.io/workflows/7252) hoặc copy toàn bộ JSON từ trang này.
2. Mở **n8n Editor** và nhấn **Import Workflow** → Dán JSON vào và nhấn **Import**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này có **12 node**, nhưng các node quan trọng nhất cần cấu hình kỹ lưỡng:

##### **A. Cấu hình Google Sheets**
- **Node "Clear your Sheet"**:
  - Chọn **credentials**: `googleSheetsOAuth2Api` (phải tạo trước trong **Credentials**).
  - Điền **Sheet URL** và **Tab Name** (tên tab trong Google Sheet mà các sếp muốn lưu dữ liệu).

- **Node "Update Your Sheet"**:
  - Chọn **credentials**: `googleSheetsOAuth2Api` (giống node trên).
  - Đảm bảo **Tab Name** khớp với tab trong Google Sheet.

##### **B. Cấu hình Telegram Bot**
- **Node "sendToTelegramChatbot"**:
  - Chọn **credentials**: `telegramApi` (tạo trong **Credentials** → **Add New Credential** → **Telegram**).
  - Điền **Chat ID** (lấy từ URL Telegram của nhóm/cá nhân).
  - **Message Template**: Workflow đã định sẵn, các sếp chỉ cần đảm bảo **Chat ID** đúng.

##### **C. Cấu hình Schedule Trigger**
- **Node "9am Clear"**:
  - Đặt thời gian **9:00 AM** (server time) để **xóa dữ liệu cũ** trước khi cập nhật mới.
- **Node "11:02 - 8:02"**:
  - Đặt thời gian **11:02 AM đến 8:02 PM** (server time) để **chạy phân tích hàng ngày** (lưu ý: cron chạy theo server time, không phải giờ địa phương).

##### **D. Node Code (cần giữ nguyên tên)**
- **Node "3. Extract All Player IDs"**:
  - **Không được đổi tên**, vì workflow sử dụng `$()` để trích xuất **personIds** từ node này.
- **Node "5. Create Final Matchup Rows" và "6. Filter for Top Matchups"**:
  - Các sếp có thể **tweak ERA/OPS thresholds** hoặc **Top N** trong code nếu muốn thay đổi tiêu chí lọc.

##### **E. Node "21 Hitters"**
- Node này **tự động tạo báo cáo Telegram** với **top 21 batter có OPS cao nhất**. Các sếp không cần chỉnh sửa, trừ khi muốn thay đổi nội dung message.

---

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Nhấn **Run Workflow** và chọn **Test Execution** để kiểm tra dữ liệu đầu ra.
   - Kiểm tra **Google Sheets** và **Telegram** để đảm bảo dữ liệu được ghi và gửi đúng.

2. **Bật Active**:
   - Sau khi test thành công, nhấn **Active** để workflow chạy tự động theo lịch trình.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tăng cường báo cáo Telegram**:
   - Thêm **đính kèm hình ảnh** (ví dụ: biểu đồ OPS của top batters) bằng cách kết hợp với **node Image Processing** hoặc **node HTML Template**.

2. **Lưu log hoạt động**:
   - Sử dụng **node StickyNote** để ghi lại **lịch sử chạy workflow**, giúp theo dõi lỗi hoặc thay đổi dữ liệu.

3. **Kết hợp với Slack**:
   - Thay vì Telegram, các sếp có thể **gửi báo cáo lên Slack** bằng **node Slack Webhook** để tích hợp với công cụ quản lý dự án.

4. **Tùy chỉnh tiêu chí lọc**:
   - Trong **node "6. Filter for Top Matchups"**, các sếp có thể thay đổi **ERA/OPS thresholds** hoặc **Top N** để phù hợp với chiến lược phân tích cá nhân.

5. **Chuyển đổi giờ theo múi giờ địa phương**:
   - Nếu server không ở múi giờ Eastern Time (ET), các sếp cần **chỉnh sửa code trong node "6. Filter for Top Matchups"** để chuyển đổi giờ đúng.

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn **tự động hóa phân tích MLB**, tiết kiệm thời gian và nhận **dữ liệu phân tích chất lượng cao** hàng ngày. Bằng cách kết hợp **Google Sheets** và **Telegram**, các sếp có thể **theo dõi top cặp đấu pitcher vs. batter** một cách dễ dàng và hiệu quả.

**Hãy áp dụng ngay và trở thành nhà phân tích MLB chuyên nghiệp!** 🏆
Nếu có bất kỳ vấn đề hoặc cần hỗ trợ, các sếp có thể tham khảo [trang hỗ trợ n8n](https://docs.n8n.io/) hoặc liên hệ cộng đồng n8n trên [Discord](https://n8n.io/discord).