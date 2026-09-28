---
title: "🚀 Tự động giám sát Meta Ads của đối thủ và gửi thông báo qua Google Sheets & Telegram"
description: "Hướng dẫn xây dựng workflow n8n tự động cào dữ liệu quảng cáo từ Meta Ads Library, lưu vào Google Sheets và gửi cảnh báo thời gian thực về Telegram/Slack."
slug: "tu-dong-giam-sat-meta-ads-doi-thu-n8n"
tags: [n8n, automation, meta-ads, market-research, google-sheets, telegram]
keywords: [n8n workflow, giám sát facebook ads, competitor analysis, meta ads library api, tự động hóa n8n]
keywords: [n8n workflow, giám sát facebook ads, competitor analysis, meta ads library api, tự động hóa n8n]
---

# 🚀 Tự động giám sát Meta Ads của đối thủ và gửi thông báo qua Google Sheets & Telegram

Các sếp có đang tốn hàng giờ mỗi tuần để mò mẫm vào **Meta Ads Library** thủ công nhằm kiểm tra xem đối thủ cạnh tranh đang chạy mẫu quảng cáo (creative) nào mới không? Việc này không chỉ tốn thời gian mà còn cực kỳ dễ bỏ sót các chiến dịch chớp nhoáng của họ.

Đừng lo, bài toán này sẽ được giải quyết 100% tự động với workflow n8n cực đỉnh mang tên **Monitor Competitor Meta Ads Creatives**. Workflow này sẽ thay các sếp "canh gác" 24/7, tự động quét quảng cáo theo Page ID hoặc Từ khóa, lưu trữ dữ liệu gọn gàng vào Google Sheets và bắn thông báo nóng hổi về Telegram hoặc Slack ngay khi có creative mới xuất hiện!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Không bỏ lỡ mẫu ad nào:** Cập nhật ngay lập tức các creative mới của đối thủ ngay khi họ vừa lên chiến dịch.
- **Xây dựng Data Lake Marketing:** Tự động lưu trữ toàn bộ dữ liệu quảng cáo vào Google Sheets để phục vụ việc phân tích xu hướng (trend), góc tiếp cận (angle) và thông điệp.
- **Theo dõi dòng thời gian (Timeline):** Dễ dàng nhìn lại lịch sử thay đổi mẫu quảng cáo của đối thủ theo thời gian.
- **Cảnh báo tức thì:** Nhận thông báo trực tiếp qua Telegram hoặc Slack mà không cần mở trình duyệt kiểm tra thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản Facebook Developers**: Để tạo app, lấy Access Token truy cập Meta Marketing API.
- **Google Sheets**: Tài khoản Google để lưu trữ dữ liệu quảng cáo.
- **Telegram Bot / Slack Workspace**: Để cấu hình kênh nhận thông báo cảnh báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn JSON của workflow từ nguồn (hoặc file tải về), sau đó paste trực tiếp vào màn hình giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp cần cấu hình kỹ các node trọng điểm sau:
- **Schedule Trigger**: Thiết lập tần suất quét dữ liệu (ví dụ: Chạy mỗi 6 tiếng hoặc 1 ngày/lần tùy ngân sách và nhu cầu).
- **Facebook Ads API by page & by keywords (HTTP Request)**: Điền **Access Token** từ ứng dụng Facebook Developers của các sếp vào phần Header Authentication.
- **Add parameters (Set)**: Cấu hình các tham số quan trọng như:
  - *Creative status* (Nên chọn `ALL` hoặc `ACTIVE`).
  - *Page IDs* (ID các trang Facebook của đối thủ, cách nhau bằng dấu phẩy).
  - *Countries* (Quốc gia muốn quét, ví dụ: `VN`).
  - *Keywords* (Từ khóa cần theo dõi nếu dùng tính năng tìm kiếm theo từ khóa).
- **Read existing IDs & Add to sheet (Google Sheets)**: Kết nối tài khoản Google Sheets của các sếp, chọn đúng file Sheet và tên Tab dùng để lưu dữ liệu. Hãy đảm bảo thứ tự các cột khớp với cấu trúc node.
- **Send a text message (Telegram) / Send a message (Slack)**: Kết nối Bot Telegram hoặc Slack và điền `Chat ID` / `Channel ID` chính xác để nhận tin nhắn cảnh báo có kèm biến số lượng (`{{$json.newCount}}`).

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) thủ công một lần để kiểm tra xem dữ liệu từ Facebook có đổ về Google Sheets và bắn thông báo thành công hay không.
- Sau khi kiểm tra mọi thứ xanh mướt, hãy bật công tắc **Active workflow** lên để hệ thống tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Lưu trữ hình ảnh/video:** Thay vì chỉ lưu link, các sếp có thể kết hợp thêm node để tải trực tiếp hình ảnh/video quảng cáo của đối thủ về Google Drive hoặc AWS S3.
- **Tích hợp AI phân tích:** Nối thêm node AI (OpenAI/Anthropic) sau bước lọc creative mới để tự động phân tích điểm mạnh, thông điệp chính và ý tưởng content của đối thủ.
- **Báo cáo định kỳ:** Tạo thêm một nhánh chạy vào cuối tuần để tổng hợp số lượng creative mới phát sinh và gửi báo cáo tuần qua Telegram.

### 📌 Kết luận
Giám sát đối thủ chưa bao giờ dễ dàng đến thế khi đã có "trợ lý ảo" n8n lo trọn gói từ A-Z. Hãy thiết lập ngay workflow này để luôn đi trước đối thủ một bước trong cuộc đua nội dung quảng cáo các sếp nhé!