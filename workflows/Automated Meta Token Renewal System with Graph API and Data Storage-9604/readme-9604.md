---
title: "🔄 Tự Động Gia Hạn Token Meta/Facebook Không Mất Kết Nối (n8n)"
description: "Giải pháp tự động gia hạn Access Token của Meta/Facebook Graph API mỗi 10 ngày, đảm bảo workflow không bao giờ bị lỗi do token hết hạn. Sử dụng Data Table để lưu trữ và cập nhật trạng thái."
slug: "tu-dong-gia-han-token-meta-facebook-n8n"
tags: [n8n, meta-api, facebook-automation, token-renewal, no-code]
keywords: [n8n workflow, gia hạn token facebook, meta graph api, tự động hóa token, n8n data table]
---

# 🔄 Tự Động Gia Hạn Token Meta/Facebook Không Mất Kết Nối (n8n)

Các sếp có từng trải qua cảm giác "đau đầu" khi một workflow n8n đang chạy ngon lành bỗng dưng báo lỗi `Invalid access token` hay `Token has expired` không? Đây là nỗi đau kinh điển khi làm việc với Meta Graph API (Facebook, Instagram, Messenger). Token tạm thời (Short-lived token) chỉ sống được 1-2 giờ, và ngay cả token dài hạn (Long-lived token) cũng chỉ có hạn 60 ngày. Khi token hết hạn, toàn bộ quy trình tự động hóa của các sếp sẽ "đứng hình" cho đến khi có người can thiệp thủ công.

Workflow **"Automated Meta Token Renewal System"** do Geoffroy phát triển chính là "cứu tinh" cho vấn đề này. Nó hoạt động như một "người gác cổng" thầm lặng, tự động kiểm tra hạn sử dụng của token và thực hiện gia hạn (renewal) thông qua Graph API trước khi token kịp hết hạn. Điểm đặc biệt là workflow này sử dụng tính năng **Data Table** mới của n8n để lưu trữ và theo dõi trạng thái token một cách gọn gàng, không cần database bên ngoài.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Hoạt động liên tục 24/7:** Workflow tự động chạy theo lịch (mặc định 10 ngày/lần), đảm bảo token luôn trong trạng thái hợp lệ.
- **Không cần Code:** Toàn bộ logic gia hạn token được xử lý qua các node HTTP Request và Set, không cần viết script Python/Node.js phức tạp.
- **Quản lý tập trung:** Sử dụng Data Table của n8n để lưu trữ Token và ngày hết hạn, dễ dàng xem lịch sử và trạng thái hiện tại.
- **Tiết kiệm chi phí:** Cron được tối ưu để chạy 10 ngày/lần (thay vì hàng ngày), giúp tiết kiệm credits n8n mà vẫn an toàn (token Meta thường có hạn 60 ngày).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Phiên bản n8n hỗ trợ tính năng **Data Table** (phiên bản mới).
- **Meta Developer App:** Các sếp cần có một ứng dụng trên [Meta for Developers](https://developers.facebook.com/) với quyền truy cập Graph API.
- **Access Token ban đầu:** Một Access Token hợp lệ (Long-lived token) của người dùng hoặc Page.
- **App Credentials:**
  - `client_id` (App ID)
  - `client_secret` (App Secret)
- **Data Table:** Tạo sẵn một Data Table trong n8n với tên `Meta credential` (chi tiết cấu trúc bên dưới).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Tải xuống file JSON của workflow từ [link gốc](https://n8n.io/workflows/9604) hoặc copy toàn bộ code JSON.
2. Mở n8n Editor, chọn **Import from URL** hoặc **Import from File**.
3. Sau khi import, các sếp sẽ thấy 9 nodes được kết nối sẵn.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

Đây là phần quan trọng nhất. Workflow này phụ thuộc vào cấu hình Data Table và thông tin App của Meta.

**Bước 1: Tạo Data Table `Meta credential`**
Trước khi chạy workflow, các sếp cần tạo một Data Table trong n8n (vào tab **Data Tables** ở thanh bên trái):
- **Tên Table:** `Meta credential`
- **Các trường (Fields) bắt buộc:**
  1. `Token`: Kiểu **String** (Lưu trữ Access Token).
  2. `expires_at`: Kiểu **Datetime** (Lưu trữ ngày giờ token hết hạn).

*Gợi ý:* Các sếp nên thêm trường `id` hoặc `app_id` nếu muốn quản lý nhiều token khác nhau trong cùng một table, nhưng workflow gốc chỉ tập trung vào 1 token chính.

**Bước 2: Cấu hình Node "User Exchange" (HTTP Request)**
Đây là node thực hiện việc gọi API Meta để đổi token cũ lấy token mới.
- Mở node **User Exchange**.
- Trong phần **Body** (hoặc Query Parameters tùy cấu hình cụ thể của node HTTP Request), các sếp cần tìm và thay thế các giá trị placeholder:
  - `client_id`: Thay bằng **App ID** của các sếp trên Meta Developer.
  - `client_secret`: Thay bằng **App Secret** của các sếp.
  - `grant_type`: Giữ nguyên `fb_exchange_token`.
  - `fb_exchange_token`: Node này sẽ tự động lấy giá trị từ Data Table ở bước trước, nhưng hãy đảm bảo mapping dữ liệu từ node "Carry ID & Token" vào đây chính xác.

**Bước 3: Kiểm tra Logic "Needs renewal?" (IF Node)**
- Workflow mặc định được thiết kế để chạy mỗi **10 ngày**.
- Logic trong node **Needs renewal?** sẽ kiểm tra xem ngày hết hạn (`expires_at`) còn bao nhiêu ngày nữa.
- Mặc định: Nếu token còn ít hơn **15 ngày** nữa là hết hạn, nó sẽ thực hiện gia hạn.
- ⚠️ **Lưu ý quan trọng:** Nếu các sếp thay đổi tần suất chạy cron (ví dụ: chạy hàng ngày), hãy kiểm tra lại điều kiện trong node IF này để tránh gia hạn quá sớm hoặc quá muộn.

**Bước 4: Cập nhật Data Table**
- Node **Update Record** sẽ tự động ghi đè lên dòng dữ liệu trong Data Table `Meta credential` với Token mới và ngày hết hạn mới.
- Đảm bảo rằng ID của dòng dữ liệu trong Data Table khớp với ID mà node **Get token expiration date** đọc được.

#### 3. Kích hoạt ⚡️

1. **Test Run:**
   - Nhấn nút **Execute Workflow** (hoặc dùng Manual Trigger).
   - Quan sát node **Get token expiration date**: Nó phải đọc được dữ liệu từ Data Table.
   - Quan sát node **Needs renewal?**: Nếu token của các sếp còn hạn > 15 ngày, nó sẽ đi nhánh "No" (không làm gì). Nếu < 15 ngày, nó sẽ đi nhánh "Yes" và gọi API.
   - *Mẹo test:* Các sếp có thể chỉnh sửa ngày `expires_at` trong Data Table thành một ngày trong quá khứ hoặc gần tương lai (dưới 15 ngày) để ép workflow thực hiện bước gia hạn.

2. **Bật Active:**
   - Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải.
   - Workflow sẽ tự động chạy theo lịch Schedule Trigger (mặc định 10 ngày/lần).

### ✍️ Mẹo & gợi ý nâng cao

- **Cảnh báo qua Telegram/Slack:** Các sếp có thể thêm một nhánh sau node **Update Record** để gửi thông báo "Token đã được gia hạn thành công" hoặc "Lỗi gia hạn token" qua Telegram/Slack. Điều này giúp các sếp nắm bắt tình trạng hệ thống mà không cần vào n8n kiểm tra.
- **Quản lý nhiều Token:** Nếu các sếp có nhiều App hoặc nhiều Page cần quản lý, hãy mở rộng Data Table bằng cách thêm trường `app_id` và sửa logic trong node **Get token expiration date** để lọc theo từng app.
- **Log lịch sử:** Thay vì chỉ cập nhật (Update), các sếp có thể thêm một node **Insert** vào một Data Table khác (ví dụ: `Token History`) để lưu lại lịch sử các lần gia hạn, giúp debug khi có sự cố.
- **Tối ưu Cron:** Mặc định là 10 ngày. Nếu các sếp lo lắng về độ trễ, có thể chỉnh xuống 5 ngày. Tuy nhiên, nhớ cân nhắc số lượng credits n8n tiêu thụ nếu các sếp đang dùng bản Cloud.

### 📌 Kết luận

Việc quản lý vòng đời của Access Token Meta luôn là một thách thức kỹ thuật nhỏ nhưng gây ra hậu quả lớn nếu bị bỏ sót. Với workflow **Automated Meta Token Renewal System**, các sếp có thể hoàn toàn yên tâm rằng các quy trình tự động hóa của mình sẽ không bao giờ bị "chết yểu" chỉ vì lý do token hết hạn.

Hãy import workflow, cấu hình Data Table và App Credentials của các sếp, và để n8n lo phần còn lại. Chúc các sếp có một hệ thống tự động hóa bền bỉ và hiệu quả! 🚀