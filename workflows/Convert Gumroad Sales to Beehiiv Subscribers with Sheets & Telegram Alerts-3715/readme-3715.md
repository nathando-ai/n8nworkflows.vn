---
title: "🚀 Tự Động Hóa Gumroad → Beehiiv: Biến Khách Mua Thành Subscriber & Báo Cáo Telegram"
description: "Workflow n8n tự động chuyển đổi dữ liệu bán hàng từ Gumroad thành subscriber Beehiiv, lưu vào Google Sheets và gửi thông báo Telegram tức thì."
slug: "gumroad-beehiiv-telegram-automation"
tags: [n8n, gumroad, beehiiv, telegram, google-sheets, marketing-automation]
keywords: [n8n workflow gumroad, tự động hóa beehiiv, chuyển đổi khách hàng, báo cáo telegram, crm google sheets]
---

# 🚀 Tự Động Hóa Gumroad → Beehiiv: Biến Khách Mua Thành Subscriber & Báo Cáo Telegram

Các sếp đang kinh doanh sản phẩm số (e-book, template, course) trên Gumroad và xây dựng cộng đồng qua Beehiiv chắc hẳn đã từng gặp tình huống "đau đầu" này: Khi có đơn hàng mới, các sếp phải thủ công copy email khách hàng, đăng nhập vào Beehiiv để thêm subscriber, rồi lại mở Google Sheets để ghi chép doanh thu. Chưa kể, việc theo dõi đơn hàng mới thường bị chậm trễ, dẫn đến mất cơ hội tương tác ngay lập tức với khách hàng mới.

Workflow này giải quyết triệt để vấn đề đó bằng cách tự động hóa 100% quy trình: Ngay khi Gumroad ghi nhận một đơn hàng, n8n sẽ tự động lấy email khách hàng, thêm họ vào danh sách subscriber của Beehiiv, lưu chi tiết giao dịch vào Google Sheets (CRM) và gửi thông báo tức thì vào kênh Telegram của team. Không cần code, không cần thao tác thủ công, mọi thứ diễn ra trong vài giây.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian tối đa:** Loại bỏ hoàn toàn thao tác nhập liệu thủ công cho mỗi đơn hàng.
- **Tăng trưởng cộng đồng tự động:** Khách hàng mua sản phẩm Gumroad sẽ tự động trở thành subscriber Beehiiv, giúp mở rộng danh sách email marketing.
- **CRM chính xác & minh bạch:** Dữ liệu giao dịch được lưu ngay lập tức vào Google Sheets, dễ dàng phân tích và đối soát.
- **Phản hồi tức thì:** Team nhận được thông báo qua Telegram ngay khi có đơn, sẵn sàng hỗ trợ hoặc chào mừng khách hàng mới.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị các tài khoản và credentials sau:
1. **Gumroad Account:**
   - Một sản phẩm đã được liệt kê trên Gumroad.
   - Vào *Settings > Advanced*, tạo một ứng dụng mới và lấy **Access Token**.
2. **Beehiiv Account:**
   - Một tài khoản Beehiiv và một publication (tạp chí/bản tin) đã được tạo.
   - Vào phần Settings của Beehiiv, tạo một **API Key** mới.
3. **Google Sheets:**
   - Một Google Sheet trống hoặc có sẵn bảng tính để lưu dữ liệu CRM.
   - Cấu hình **Google Sheets OAuth2** credentials trong n8n (hướng dẫn chi tiết tại [docs n8n](https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.googlesheets/)).
4. **Telegram:**
   - Tạo một Telegram Bot (qua @BotFather) và lấy **Bot Token**.
   - Thêm bot vào kênh (channel) hoặc nhóm mà các sếp muốn nhận thông báo với quyền **Admin**.
   - Lấy **Chat ID** của kênh/nhóm đó.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể import workflow này vào n8n của mình bằng cách:
- Tải file JSON của workflow từ [n8n.io/workflows/3715](https://n8n.io/workflows/3715).
- Trong n8n Editor, chọn **Import from File** hoặc **Import from URL**.
- Hoặc copy toàn bộ JSON và dán vào editor n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình lại các node sau để khớp với tài khoản của mình:

- **Node: `Gumroad Sale Trigger`**
  - Chọn credentials `gumroadApi` đã tạo.
  - Đảm bảo resource là `sale` để bắt sự kiện đơn hàng mới.
  - *Lưu ý:* Token Gumroad phải có quyền đọc dữ liệu đơn hàng.

- **Node: `append row in CRM` (Google Sheets)**
  - Chọn credentials `googleSheetsOAuth2Api`.
  - Chọn đúng **Spreadsheet ID** và **Sheet Name** (tên tab) mà các sếp muốn lưu dữ liệu.
  - Kiểm tra mapping cột: Đảm bảo các trường như Email, Tên sản phẩm, Giá, Ngày mua được ánh xạ đúng vào các cột tương ứng trong Sheet.

- **Node: `List publications` (HTTP Request)**
  - Node này dùng để lấy danh sách các publication trong Beehiiv.
  - Chọn credentials `httpBearerAuth` hoặc `httpHeaderAuth` tùy cấu hình API Beehiiv.
  - Đảm bảo URL và headers đúng theo tài liệu API của Beehiiv.

- **Node: `Post subscription` (HTTP Request)**
  - Node này thực hiện việc thêm subscriber vào Beehiiv.
  - Chọn credentials `httpHeaderAuth`.
  - Kiểm tra body request: Email khách hàng từ Gumroad phải được map đúng vào trường `email` trong payload gửi tới Beehiiv.
  - *Lưu ý:* Nếu khách hàng đã là subscriber, API Beehiiv có thể trả về lỗi hoặc bỏ qua, các sếp nên kiểm tra log để đảm bảo không bị lỗi.

- **Node: `Set ChatID` (Set)**
  - Đây là node để định nghĩa Chat ID của kênh Telegram.
  - Thay thế giá trị mặc định bằng **Chat ID** thực tế của kênh/nhóm Telegram mà các sếp đã lấy ở bước chuẩn bị.

- **Node: `Notify in channel` (Telegram)**
  - Chọn credentials `telegramApi` (Bot Token).
  - Kiểm tra nội dung tin nhắn (message) để đảm bảo thông tin đơn hàng (tên khách, sản phẩm, giá) được hiển thị rõ ràng.
  - Đảm bảo `chat_id` tham chiếu đúng từ node `Set ChatID`.

#### 3. Kích hoạt ⚡️
- **Test Run:** Các sếp nên tạo một đơn hàng thử nghiệm trên Gumroad (có thể dùng chế độ test hoặc mua với giá 0đ nếu Gumroad hỗ trợ) để kiểm tra toàn bộ luồng:
  - Dữ liệu có được thêm vào Google Sheets không?
  - Subscriber có được thêm vào Beehiiv không?
  - Tin nhắn có được gửi vào Telegram không?
- **Bật Active:** Sau khi test thành công, bật chế độ **Active** cho workflow để nó tự động chạy 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Cá nhân hóa tin nhắn Telegram:** Thay vì chỉ gửi thông báo đơn hàng, các sếp có thể thêm tên khách hàng và sản phẩm cụ thể để team dễ dàng tương tác cá nhân hóa.
- **Tích hợp thêm Slack/Discord:** Nếu team dùng Slack hoặc Discord, các sếp có thể thay thế hoặc bổ sung node Telegram bằng node Slack/Discord để thông báo đa kênh.
- **Gửi email chào mừng tự động:** Sau khi thêm subscriber vào Beehiiv, các sếp có thể thêm một node HTTP Request khác để gửi email chào mừng ngay lập tức thông qua API Beehiiv, tăng tỷ lệ giữ chân khách hàng.
- **Phân tích dữ liệu:** Sử dụng Google Sheets để tạo các dashboard phân tích doanh thu, sản phẩm bán chạy nhất, và nguồn gốc khách hàng, giúp ra quyết định kinh doanh chính xác hơn.

### 📌 Kết luận
Workflow Gumroad → Beehiiv → Sheets → Telegram là một giải pháp tự động hóa marketing và CRM cực kỳ hiệu quả, giúp các sếp tiết kiệm thời gian, tăng trưởng cộng đồng và quản lý dữ liệu một cách chuyên nghiệp. Hãy áp dụng ngay để tối ưu hóa quy trình kinh doanh sản phẩm số của mình và tập trung vào việc tạo ra giá trị cho khách hàng thay vì loay hoay với các thao tác thủ công.