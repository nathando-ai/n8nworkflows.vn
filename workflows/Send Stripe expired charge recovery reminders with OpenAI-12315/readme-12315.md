---
title: "🚀 Tự Động Hóa Nhắc Nợ & Tạo Hóa Đơn Mới Với Stripe + OpenAI"
description: "Workflow n8n tự động phát hiện thanh toán thất bại trên Stripe, dùng AI viết email nhắc nợ chuyên nghiệp và tạo hóa đơn mới, giúp tăng tỷ lệ thu hồi nợ và giảm công sức vận hành."
slug: "tu-dong-hoa-nhac-no-stripe-openai"
tags: [n8n, automation, no-code, stripe, openai, finance]
keywords: [n8n workflow, tự động hóa thanh toán, stripe automation, ai email, thu hồi nợ]
---

# 🚀 Tự Động Hóa Nhắc Nợ & Tạo Hóa Đơn Mới Với Stripe + OpenAI

Trong kinh doanh online, việc khách hàng thanh toán thất bại (do hết hạn thẻ, lỗi mạng, hoặc đơn giản là quên) là một nỗi đau lớn. Nếu các sếp phải thủ công kiểm tra dashboard Stripe mỗi ngày, tìm ra các giao dịch lỗi, rồi ngồi soạn email nhắc nợ từng người một, thì không chỉ tốn thời gian mà còn dễ gây ra sự cồng kềnh trong giọng văn, dẫn đến trải nghiệm khách hàng kém.

Workflow này chính là "trợ lý thu nợ" 24/7. Nó tự động lắng nghe sự kiện thanh toán hết hạn trên Stripe, sử dụng sức mạnh của OpenAI để soạn thảo một email nhắc nợ vừa chuyên nghiệp, vừa thân thiện (không gây khó chịu cho khách), đồng thời tự động tạo hóa đơn mới để khách có thể thanh toán lại ngay lập tức. Tất cả diễn ra hoàn toàn tự động, không cần code.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tăng tỷ lệ thu hồi nợ:** Khách hàng nhận được nhắc nhở kịp thời và chuyên nghiệp, giảm thiểu tình trạng "quên" thanh toán.
- **Tiết kiệm thời gian vận hành:** Loại bỏ hoàn toàn bước kiểm tra thủ công và soạn email hàng ngày.
- **Cá nhân hóa thông điệp:** OpenAI tạo ra nội dung email tự nhiên, phù hợp với giọng văn thương hiệu, thay vì những mẫu email cứng nhắc.
- **Quy trình liền mạch:** Từ phát hiện lỗi -> Tạo hóa đơn mới -> Gửi email, tất cả diễn ra trong vài giây.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Stripe:** Đã được kích hoạt và có quyền truy cập API.
- **Tài khoản OpenAI:** Cần có API Key để sử dụng cho node LLM.
- **Tài khoản Gmail:** Đã cấu hình OAuth2 trong n8n để gửi email.
- **n8n Instance:** Chạy trên VPS hoặc Cloud.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Tải xuống file JSON của workflow từ link gốc hoặc copy toàn bộ code JSON.
2. Mở n8n Editor, chọn **Import from URL** hoặc **Import from File**.
3. Dán JSON hoặc chọn file đã tải về. Workflow sẽ hiển thị với 6 nodes chính.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

Dưới đây là các node quan trọng cần cấu hình kỹ lưỡng để workflow hoạt động chính xác:

**1. Node: `Charge Expired Event` (Stripe Trigger)**
- Đây là điểm khởi đầu. Các sếp cần đảm bảo đã kết nối **Stripe Credentials** vào node này.
- Trong phần **Events**, hãy chắc chắn rằng sự kiện `charge.expired` (hoặc `invoice.payment_failed` tùy cấu hình Stripe của bạn) được chọn.
- *Lưu ý:* Đảm bảo webhook endpoint trong Stripe đã được n8n capture chính xác.

**2. Node: `Workflow Configuration` & `Extract Customer & Payment Data` (Set Nodes)**
- Hai node này đóng vai trò chuẩn hóa dữ liệu đầu vào.
- Các sếp cần kiểm tra phần **Values** để đảm bảo các trường dữ liệu quan trọng được ánh xạ đúng từ dữ liệu Stripe:
    - `customer_name`: Tên khách hàng.
    - `customer_email`: Email nhận nhắc nợ.
    - `amount`: Số tiền (cần chú ý đơn vị, Stripe thường trả về cent, cần chia cho 100 nếu cần).
    - `currency`: Mã tiền tệ (USD, VND, EUR...).
    - `previous_invoice_id`: ID hóa đơn cũ để tham chiếu.

**3. Node: `Generate Payment Reminder` (OpenAI)**
- Đây là "trái tim" của workflow.
- **Credentials:** Chọn OpenAI API Key đã tạo.
- **Model:** Chọn model phù hợp (ví dụ: `gpt-4o-mini` hoặc `gpt-3.5-turbo` để tiết kiệm chi phí).
- **Prompt:** Các sếp nên tùy chỉnh prompt để phù hợp với giọng văn thương hiệu. Ví dụ mặc định:
  > "Write a professional, friendly payment reminder for {{ $json.customer_name }} regarding their expired charge of {{ $json.amount }} {{ $json.currency }}. Mention that a new invoice has been generated. Keep it polite and concise."
- *Mẹo:* Có thể thêm yêu cầu "Đừng sử dụng các từ ngữ đe dọa, hãy giữ thái độ hỗ trợ" để tăng tỷ lệ phản hồi tích cực.

**4. Node: `Create New Invoice` (Stripe)**
- Node này tạo hóa đơn mới dựa trên dữ liệu cũ.
- **Operation:** Chọn `create`.
- **Resource:** Chọn `charge` (hoặc `invoice` tùy logic cụ thể, trong workflow gốc là tạo charge mới để khách thanh toán lại).
- Đảm bảo các trường `amount`, `currency`, và `customer` được ánh xạ đúng từ node Set trước đó.

**5. Node: `Send Reminder Email` (Gmail)**
- **Credentials:** Chọn Gmail Account đã cấu hình OAuth2.
- **To:** Ánh xạ với `{{ $json.customer_email }}`.
- **Subject:** Ví dụ: "Nhắc nhở thanh toán hóa đơn #{{ $json.previous_invoice_id }}".
- **Message:** Ánh xạ với output từ node OpenAI (`{{ $json.text }}` hoặc trường tương ứng).
- *Lưu ý quan trọng:* Kiểm tra kỹ nội dung email trước khi bật Active để tránh gửi email rác hoặc sai thông tin.

#### 3. Kích hoạt ⚡️
1. **Test Run:** Sử dụng nút "Execute Workflow" với dữ liệu mẫu (mock data) để xem email được sinh ra như thế nào và hóa đơn có được tạo không.
2. **Bật Active:** Sau khi xác nhận mọi thứ hoạt động đúng, bật công tắc **Active** ở góc trên bên phải.
3. **Kiểm tra Webhook:** Vào Stripe Dashboard, kiểm tra xem webhook `charge.expired` có đang hoạt động và gửi dữ liệu về n8n không.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Slack/Telegram:** Thêm một node Slack hoặc Telegram sau node Gmail để thông báo cho đội ngũ nội bộ khi có một giao dịch thất bại, giúp đội hỗ trợ chủ động liên hệ nếu cần.
- **Lưu Log vào Google Sheets:** Thêm node Google Sheets để ghi lại lịch sử các lần nhắc nợ, số tiền, và trạng thái thanh toán lại. Điều này giúp theo dõi hiệu quả thu hồi nợ theo thời gian.
- **Chỉnh sửa Prompt theo ngữ cảnh:** Nếu khách hàng là doanh nghiệp (B2B), hãy chỉnh prompt để giọng văn trang trọng hơn so với khách hàng cá nhân (B2C).
- **Đa kênh liên lạc:** Nếu khách hàng không phản hồi qua email sau 3 ngày, có thể thiết lập một workflow thứ hai để gửi SMS hoặc WhatsApp (qua các dịch vụ như Twilio) để tăng tỷ lệ tiếp cận.

### 📌 Kết luận
Việc tự động hóa quy trình nhắc nợ không chỉ giúp các sếp tiết kiệm hàng giờ làm việc mỗi tuần mà còn nâng cao hình ảnh chuyên nghiệp của thương hiệu. Với sự kết hợp giữa độ tin cậy của Stripe và khả năng ngôn ngữ tự nhiên của OpenAI, workflow này là một công cụ đắc lực giúp tối ưu dòng tiền và cải thiện trải nghiệm khách hàng. Hãy import và tùy chỉnh ngay hôm nay để biến quy trình thu nợ từ "món nợ" thành một quy trình tự động trơn tru!