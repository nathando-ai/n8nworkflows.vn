---
title: "🍔 Tự Động Hóa Quản Lý Đơn Hàng Đồ Ăn & Theo Dõi Chi Phí Với n8n, Gmail và Slack"
description: "Hướng dẫn tự động hóa quy trình đọc email xác nhận đơn hàng đặt đồ ăn qua Gmail, trích xuất thông tin chi phí và gửi thông báo trực quan đến Slack."
slug: "tu-dong-hoa-quan-ly-don-hang-do-an-va-chi-phi-voi-n8n"
tags: [n8n, automation, no-code, gmail, slack, expense-tracking, food-delivery]
keywords: [n8n workflow, tự động hóa đơn hàng, quản lý chi phí đồ ăn, gmail trigger slack, trích xuất email n8n]
---

# 🚀 Tự Động Hóa Quản Lý Đơn Hàng Đồ Ăn & Theo Dõi Chi Phí Với n8n

Các sếp có bao giờ cảm thấy mệt mỏi mỗi khi đặt đồ ăn qua các ứng dụng giao hàng (như Grab, ShopeeFood, Baemin...) nhưng lại lười ghi chép lại chi phí, hoặc muốn đồng bộ hóa thông báo đơn hàng cho cả team trên Slack nhưng phải làm thủ công chưa? Việc kiểm soát các khoản chi tiêu nhỏ lẻ từ việc ăn uống hằng ngày đôi khi chiếm khá nhiều thời gian nếu cứ phải copy và paste qua lại.

Đừng lo, workflow n8n **"Food Delivery Notifications and Easy Expense Tracking"** do tác giả *darrell_tw* thiết kế sẽ giải quyết triệt để bài toán này. Hệ thống sẽ tự động quét hộp thư Gmail của các sếp, lọc các email xác nhận đơn hàng, bóc tách các thông tin quan trọng (giá tiền, quán ăn, ngày giờ) và bắn thông báo cực kỳ bắt mắt trực tiếp lên kênh Slack của team hoặc cá nhân một cách hoàn toàn tự động!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian:** Không cần thủ công nhập dữ liệu chi phí ăn uống hay chuyển tiếp email đơn hàng nữa.
- **Minh bạch & Rõ ràng:** Cập nhật ngay lập tức thông tin đơn hàng (Giá, Cửa hàng, Thời gian) lên Slack để team cùng nắm bắt hoặc quản lý chi tiêu cá nhân.
- **Hoạt động 24/7:** Hệ thống tự động bắt sự kiện ngay khi email vừa chui vào hộp thư đến mà không bỏ sót đơn nào.
- **Tùy biến linh hoạt:** Dễ dàng mở rộng kết nối thêm Google Sheets để lưu trữ sổ chi tiêu tự động.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **Tài khoản n8n** (Self-hosted hoặc n8n Cloud).
- **Tài khoản Gmail** (đã cấp quyền kết nối OAuth2 để đọc email).
- **Tài khoản Slack** (với quyền cấu hình và gửi tin nhắn qua Slack Bot/Webhook).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ kho lưu trữ n8n, sau đó vào giao diện n8n Editor chọn **Add workflow** -> Dấu ba chấm (...) ở góc trên bên phải -> **Import from File** (hoặc paste trực tiếp mã JSON vào).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình kỹ các node trọng điểm sau:

- **Receive certain keyword Gmail Trigger**: 
  - Chọn Credentials tài khoản Gmail của các sếp.
  - Cấu hình bộ lọc (Filters) như từ khóa tiêu đề (Subject) hoặc nhãn (Label) chứa từ khóa liên quan đến hóa đơn đặt đồ ăn để node chỉ bắt đúng email cần thiết, tránh quét nhảm tốn tài nguyên.
- **Get emails from Gmail with certain subject**: 
  - Node này dùng để lấy danh sách email theo chủ đề khi chạy thủ công hoặc quét lại lịch sử. Hãy đảm bảo các tham số tìm kiếm (Search Query) khớp với loại email đặt đồ ăn các sếp thường nhận.
- **Loop Over Items (`splitInBatches`)**: 
  - Giúp xử lý từng email một cách mượt mà, tránh bị nghẽn khi có hàng loạt đơn hàng đổ về cùng lúc (ví dụ giờ cao điểm trưa).
- **Extract Price, Shop, Date, TIme (`set`)**: 
  - Đây là "bộ não" trích xuất dữ liệu. Các sếp cần chỉnh sửa các biểu thức (Expressions) trong node này cho phù hợp với định dạng nội dung email thực tế của hãng giao đồ ăn mà các sếp hay dùng (bóc ra số tiền, tên quán, thời gian đặt).
- **Send to Slack with Block (`slack`)**: 
  - Kết nối Credentials Slack OAuth2. 
  - Chọn kênh (Channel) trên Slack mà các sếp muốn bot bắn thông báo về (ví dụ: `#chi-phi-an-uong` hoặc `#lunch-time`). Thiết kế lại Block Kit nếu muốn giao diện tin nhắn thêm phần lung linh, bắt mắt.

#### 3. Kích hoạt ⚡️
- Bấm nút **Click to Test Flow** (`manualTrigger`) để chạy thử nghiệm xem dữ liệu có bóc tách đúng và gửi về Slack thành công hay không.
- Sau khi test ngon lành, gạt công tắc sang **Active** để workflow tự động chiến đấu 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Lưu trữ sổ sách tự động:** Nối thêm node **Google Sheets** sau bước trích xuất dữ liệu để tự động ghi nhận mọi khoản chi tiêu vào một bảng tính chung, giúp các sếp tổng kết cuối tháng dễ như ăn kẹo.
- **Bổ sung trợ lý AI:** Tích hợp thêm OpenAI (ChatGPT) node vào giữa để AI tự động đọc nội dung email dạng văn bản lộn xộn và trích xuất chuẩn xác thông tin hơn mà không cần viết regex phức tạp.
- **Cảnh báo qua Telegram:** Nếu team các sếp dùng Telegram thay vì Slack, chỉ cần thay thế node Slack bằng node Telegram Bot là xong!

### 📌 Kết luận
Workflow **Food Delivery Notifications and Easy Expense Tracking** là một "vũ khí" nhỏ gọn nhưng cực kỳ lợi hại giúp tối ưu hóa những việc vặt hằng ngày. Hãy cài đặt ngay để việc quản lý chi tiêu và theo dõi đơn hàng trở nên tự động hoàn toàn, dành thời gian đó để tập trung cho những công việc kinh doanh quan trọng hơn các sếp nhé!