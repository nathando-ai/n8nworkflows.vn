---
title: "📊 Theo Dõi Danh Mục Đầu Tư Đa Sàn & Báo Cáo P&L Tự Động Qua Telegram"
description: "Workflow n8n giúp tổng hợp dữ liệu từ nhiều sàn giao dịch (Broker) vào Google Sheets, tự động tính toán lợi nhuận (P&L) và gửi báo cáo chi tiết qua Telegram theo lịch hoặc theo lệnh."
slug: "theo-doi-danh-muc-dau-tu-da-san-telegram"
tags: [n8n, automation, investment, telegram, google-sheets, finance]
keywords: [n8n workflow, theo dõi đầu tư, telegram bot, google sheets, tự động hóa tài chính, P&L report]
---

# 📊 Theo Dõi Danh Mục Đầu Tư Đa Sàn & Báo Cáo P&L Tự Động Qua Telegram

Các sếp đầu tư thường gặp khó khăn gì khi quản lý tài sản? Đó là việc phải mở hàng chục tab trình duyệt, đăng nhập vào từng sàn giao dịch (Robinhood, E*TRADE, Charles Schwab, hoặc các sàn Crypto/FX khác nhau) để xem số dư và lợi nhuận. Việc này không chỉ tốn thời gian mà còn dễ gây nhầm lẫn, thiếu sót khi cần ra quyết định nhanh.

Workflow **"Track Multi-Broker Investment Portfolio"** được thiết kế để giải quyết triệt để vấn đề này. Nó hoạt động như một "trợ lý tài chính" cá nhân, tự động thu thập dữ liệu từ Google Sheets (nơi các sếp nhập hoặc đồng bộ dữ liệu từ các sàn), tính toán chính xác lợi nhuận (P&L), và gửi báo cáo trực tiếp vào Telegram của các sếp. Không cần code, không cần mở trình duyệt, chỉ cần nhìn điện thoại là biết ngay "hôm nay lãi hay lỗ bao nhiêu".

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, đặc biệt là các trigger theo lịch (schedule) và bot Telegram, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tổng hợp dữ liệu tập trung:** Quản lý tất cả các tài khoản đầu tư (Chứng khoán, Crypto, Forex...) trong một bảng tính duy nhất.
- **Báo cáo P&L chi tiết:** Tự động tính toán số tiền đầu tư, lợi nhuận tuyệt đối, tỷ lệ phần trăm và giá trị hiện tại.
- **Tương tác thời gian thực:** Gửi lệnh `/total` hoặc tên sàn cụ thể qua Telegram để nhận báo cáo ngay lập tức.
- **Thông báo định kỳ:** Nhận báo cáo tự động vào giờ mở cửa và đóng cửa thị trường (ví dụ: 10AM và 4PM).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Bản Self-hosted hoặc Cloud.
- **Google Sheets:** Một bảng tính chứa dữ liệu danh mục đầu tư (các sếp cần tạo sheet riêng và nhập dữ liệu mẫu).
- **Tài khoản Telegram:**
  - Tạo Bot qua @BotFather để lấy **Bot Token**.
  - Lấy **Chat ID** của các sếp (hoặc group) để nhận thông báo.
- **Credentials trong n8n:**
  - Google Sheets OAuth2.
  - Telegram API.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n Editor.
2. Chọn **Import from File** hoặc **Import from URL**.
3. Tải file JSON workflow từ link gốc: [n8n.io/workflows/6317](https://n8n.io/workflows/6317) hoặc copy JSON từ nguồn.
4. Sau khi import, các sếp sẽ thấy một workflow với các node chính: Schedule Trigger, Telegram Trigger, Google Sheets, Code, và Telegram.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

Đây là phần quan trọng nhất. Workflow này dựa vào dữ liệu trong Google Sheets và cấu hình Telegram.

**A. Cấu hình Google Sheets (Nodes: `Get row(s) in sheet`, `Get row(s) in sheet2`)**
- Các sếp cần tạo một Google Sheet mới.
- **Sheet 1 (Danh mục tổng):** Chứa danh sách các sàn giao dịch (Broker) và mã tài khoản.
- **Sheet 2 (Dữ liệu chi tiết):** Chứa các cột như: `Broker Name`, `Invested Amount` (Vốn đầu tư), `Current Value` (Giá trị hiện tại), `Date` (Ngày cập nhật).
- Trong node `Get row(s) in sheet`, các sếp cần:
  - Chọn đúng **Credential** Google Sheets.
  - Chọn đúng **Document ID** và **Sheet Name** (ví dụ: `Sheet1`).
  - Đảm bảo dữ liệu trong Sheet có định dạng số (Number) cho các cột tiền tệ để node `Code` tính toán chính xác.

**B. Cấu hình Logic Tính Toán (Nodes: `Code`, `Code1`, `Aggregate`, `Switch`)**
- Node `Code` và `Code1` chứa logic JavaScript để tính P&L:
  - `P&L = Current Value - Invested Amount`
  - `P&L % = (P&L / Invested Amount) * 100`
- Node `Switch` dùng để phân loại lệnh từ Telegram:
  - Nếu lệnh là `/total`: Tổng hợp tất cả các sàn.
  - Nếu lệnh là tên sàn cụ thể (ví dụ: `/Robinhood`): Chỉ lấy dữ liệu của sàn đó.
- **Lưu ý:** Nếu các sếp đổi tên cột trong Google Sheet, phải cập nhật lại tên biến trong node `Code` cho khớp.

**C. Cấu hình Telegram (Nodes: `Telegram Trigger`, `Broker PNL Update`, `Total PNL Update`)**
- **Node `Telegram Trigger`:**
  - Chọn **Credential** Telegram Bot.
  - Chọn **Update Type** là `Message`.
  - Trong phần **Allowed Chat IDs**, các sếp cần điền Chat ID của mình. *Đây là bước bảo mật quan trọng để tránh người lạ spam bot.*
- **Node `Broker PNL Update` & `Total PNL Update`:**
  - Chọn **Credential** Telegram Bot.
  - **Chat ID:** Điền lại Chat ID nhận báo cáo.
  - **Text:** Node này đã được code sẵn để format text đẹp mắt với emoji (📊, 💰, 📈). Các sếp có thể chỉnh sửa template string trong node này nếu muốn thay đổi cách hiển thị (ví dụ: đổi tiền tệ từ USD sang VND, hoặc thêm tên riêng).

**D. Cấu hình Lịch (Node: `Auto Update at 10AM and 4PM`)**
- Mặc định workflow chạy vào 10AM và 4PM.
- Các sếp nên chỉnh lại giờ này cho phù hợp với **múi giờ của thị trường** mà các sếp đang đầu tư (ví dụ: Thị trường Mỹ đóng cửa lúc 4PM EST, thị trường Crypto chạy 24/7 nên có thể chọn giờ khác).
- Chọn đúng **Timezone** trong node Schedule Trigger.

#### 3. Kích hoạt ⚡️
1. **Test Run:**
   - Nhấn nút **Execute Workflow** để chạy thử.
   - Mở Telegram, gửi lệnh `/total` cho Bot.
   - Kiểm tra xem Bot có trả về báo cáo tổng hợp không.
   - Gửi tên một sàn cụ thể (ví dụ: `/Robinhood`) để kiểm tra báo cáo chi tiết.
2. **Bật Active:**
   - Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải.
   - Workflow sẽ tự động gửi báo cáo vào các khung giờ đã định và phản hồi các lệnh từ Telegram.

### ✍️ Mẹo & gợi ý nâng cao

1. **Tự động cập nhật dữ liệu từ API:**
   - Hiện tại, workflow giả định dữ liệu đã có trong Google Sheets. Để nâng cao, các sếp có thể thêm các node **HTTP Request** trước node Google Sheets để gọi API từ các sàn giao dịch (nếu họ có API key) và tự động ghi đè dữ liệu vào Sheet.
2. **Thêm cảnh báo Lỗ/Lãi lớn:**
   - Thêm một node `If` sau bước tính toán P&L.
   - Nếu `P&L % < -5%` (lỗ hơn 5%), gửi một thông báo Telegram khẩn cấp với icon ⚠️ để các sếp kịp thời xử lý.
3. **Gửi báo cáo tuần/tháng:**
   - Tạo thêm một Schedule Trigger khác chạy vào Chủ nhật hàng tuần.
   - Dùng node `Code` để tính toán trung bình P&L trong tuần và gửi báo cáo tổng kết tuần qua.
4. **Đa tiền tệ:**
   - Nếu các sếp đầu tư bằng nhiều loại tiền (USD, EUR, VND), hãy thêm cột `Currency` vào Google Sheet.
   - Trong node `Code`, thêm logic quy đổi sang một tiền tệ chung (ví dụ: USD) trước khi tính tổng, hoặc hiển thị riêng biệt từng loại tiền.

### 📌 Kết luận

Workflow **"Track Multi-Broker Investment Portfolio"** là công cụ không thể thiếu cho bất kỳ nhà đầu tư nào đang quản lý nhiều tài khoản. Thay vì loay hoay với các con số rời rạc, các sếp sẽ có một "trung tâm điều khiển" tài chính trực tiếp trên điện thoại.

Việc thiết lập chỉ mất khoảng 15-20 phút, nhưng lợi ích là sự an tâm và khả năng ra quyết định nhanh chóng mỗi ngày. Hãy import workflow, cấu hình Google Sheet và Telegram, và bắt đầu trải nghiệm sự tiện lợi của việc tự động hóa tài chính ngay hôm nay! 🚀