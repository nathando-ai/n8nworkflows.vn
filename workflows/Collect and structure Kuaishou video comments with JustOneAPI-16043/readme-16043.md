---
title: "🚀 Tự Động Thu Thập & Phân Tích Comment Kuaishou Với JustOneAPI"
description: "Hướng dẫn chi tiết workflow n8n giúp các sếp tự động lấy dữ liệu comment từ video Kuaishou, xử lý và chuẩn hóa thành bộ dữ liệu sạch để phục vụ nghiên cứu thị trường và phân tích hành vi người dùng."
slug: "thu-thap-comment-kuaishou-justoneapi"
tags: [n8n, automation, no-code, kuaishou, market-research, data-scraping]
keywords: [n8n workflow, thu thập comment kuaishou, justoneapi, tự động hóa nghiên cứu thị trường, phân tích dữ liệu social]
---

# 🚀 Tự Động Thu Thập & Phân Tích Comment Kuaishou Với JustOneAPI

Trong kỷ nguyên của video ngắn, Kuaishou không chỉ là một nền tảng giải trí mà còn là mỏ vàng dữ liệu khổng lồ cho các nhà làm marketing và nghiên cứu thị trường. Tuy nhiên, việc thủ công copy-paste từng comment, lưu vào Excel hay Google Sheets là một quy trình cực kỳ tốn thời gian, dễ sai sót và không thể mở rộng quy mô (scale).

Workflow n8n này được thiết kế để giải quyết triệt để nỗi đau đó. Bằng cách kết hợp với **JustOneAPI**, các sếp có thể tự động hóa 100% quy trình: từ việc gửi yêu cầu API, nhận dữ liệu thô, xử lý và chuẩn hóa thành một bộ sưu tập comment sạch sẽ, sẵn sàng để phân tích sentiment, tìm kiếm từ khóa hay xây dựng persona khách hàng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, đặc biệt khi cần thu thập dữ liệu hàng loạt hoặc chạy theo lịch (cron), các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian tối đa:** Thay vì mất hàng giờ để copy comment thủ công, workflow hoàn tất trong vài giây.
- **Dữ liệu chuẩn hóa:** Comment được xử lý qua node Code, loại bỏ nhiễu, định dạng thống nhất, dễ dàng import vào Excel/Database.
- **Nghiên cứu thị trường sâu hơn:** Có dữ liệu sạch để chạy phân tích sentiment (cảm xúc), tìm insight từ phản hồi của người dùng.
- **Không cần code phức tạp:** Logic xử lý dữ liệu đã được viết sẵn trong node Code, các sếp chỉ cần cấu hình tham số.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Bản Cloud hoặc Self-hosted.
- **Tài khoản JustOneAPI:** Các sếp cần có API Key từ JustOneAPI để gọi endpoint lấy dữ liệu Kuaishou.
- **ID Video Kuaishou:** ID của video cụ thể mà các sếp muốn thu thập comment.
- **Kiến thức cơ bản về n8n:** Biết cách import workflow và cấu hình credentials.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Vào trang [n8n.io/workflows/16043](https://n8n.io/workflows/16043).
2. Copy toàn bộ đoạn JSON của workflow.
3. Mở n8n Editor, chọn **Import from URL** hoặc **Import from Clipboard**.
4. Workflow sẽ hiện ra với 6 nodes chính.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

Dưới đây là các node quan trọng mà các sếp cần kiểm tra và cấu hình lại:

**1. Node: `Set API Request Parameters` (Loại: Set)**
Đây là node thiết lập các biến đầu vào cho yêu cầu API.
- **Action:** Chọn "Edit Fields".
- **Fields:** Các sếp cần điền:
    - `video_id`: ID của video Kuaishou cần lấy comment.
    - `api_key`: API Key của JustOneAPI (hoặc cấu hình qua Credentials nếu muốn bảo mật hơn).
    - Các tham số khác như `count` (số lượng comment muốn lấy) nếu có.

**2. Node: `Fetch Kuaishou Video Comments API` (Loại: HTTP Request)**
Node này thực hiện việc gọi API.
- **Method:** GET (hoặc POST tùy cấu hình API).
- **URL:** Đảm bảo URL trỏ đúng endpoint của JustOneAPI cho Kuaishou comments.
- **Headers/Query Params:** Kiểm tra xem các tham số từ node `Set API Request Parameters` đã được map đúng vào đây chưa.
- **Credentials:** Nếu JustOneAPI yêu cầu xác thực qua Header (ví dụ: `Authorization: Bearer <key>`), các sếp cần tạo một **Header Auth** credential trong n8n và gắn vào node này.

**3. Node: `Process Comment Data Collection` (Loại: Code)**
Đây là "trái tim" của workflow, nơi dữ liệu thô được làm sạch.
- **Mode:** Run Once for All Items.
- **JavaScript Code:** Các sếp nên đọc kỹ đoạn code này. Nó thường thực hiện các bước:
    - Duyệt qua mảng comment từ API.
    - Trích xuất các trường quan trọng: `user_name`, `comment_text`, `like_count`, `timestamp`.
    - Định dạng lại dữ liệu thành một array đối tượng sạch sẽ.
- **Lưu ý:** Nếu cấu trúc dữ liệu trả về từ JustOneAPI thay đổi, các sếp có thể cần chỉnh sửa logic trong node Code này để map đúng các field.

**4. Node: `Output Final Comment Collection` (Loại: Set)**
Node này chuẩn bị dữ liệu cuối cùng để xuất ra.
- Các sếp có thể thêm các trường metadata vào đây, ví dụ: `video_title`, `collection_date`, `source_url`.

#### 3. Kích hoạt ⚡️
1. **Test Run:** Nhấn nút **Execute Workflow** (hoặc Test Workflow) ở góc trên bên phải.
2. Kiểm tra output của node `Output Final Comment Collection`. Đảm bảo dữ liệu comment hiển thị đúng, không bị lỗi format.
3. Nếu mọi thứ ổn, nhấn nút **Active** (góc trên bên phải) để bật workflow.
4. *Mẹo:* Nếu muốn chạy tự động theo lịch, các sếp có thể thay thế node `Manual Trigger` bằng `Cron` hoặc `Schedule Trigger`.

### ✍️ Mẹo & gợi ý nâng cao

- **Kết hợp với Google Sheets/Excel:** Thêm node `Google Sheets` hoặc `Excel` sau node `Output Final Comment Collection` để tự động lưu dữ liệu vào bảng tính. Đây là cách phổ biến nhất để lưu trữ và phân tích.
- **Phân tích Sentiment với AI:** Thêm node `OpenAI` hoặc `Anthropic` sau khi có dữ liệu comment. Prompt: "Phân tích cảm xúc (tích cực/tiêu cực/trung tính) của comment này: {{ $json.comment_text }}". Kết quả sẽ giúp các sếp đo lường mức độ hài lòng của khách hàng.
- **Lọc từ khóa:** Trong node `Code`, các sếp có thể thêm logic để chỉ giữ lại các comment chứa từ khóa cụ thể (ví dụ: "giá", "chất lượng", "giao hàng") để tập trung vào insight quan trọng.
- **Gửi báo cáo qua Telegram/Slack:** Thêm node `Telegram` hoặc `Slack` để gửi thông báo khi việc thu thập dữ liệu hoàn tất, kèm theo số lượng comment đã lấy được.

### 📌 Kết luận

Workflow này là công cụ đắc lực cho bất kỳ ai đang làm nghiên cứu thị trường, quản lý cộng đồng hay phân tích đối thủ trên Kuaishou. Thay vì mất thời gian cho những công việc lặp đi lặp lại, hãy để n8n và JustOneAPI lo phần "lấy dữ liệu", còn các sếp tập trung vào việc "khai thác insight" từ dữ liệu đó.

Hãy import workflow, cấu hình API Key và bắt đầu thu thập dữ liệu ngay hôm nay! 🚀