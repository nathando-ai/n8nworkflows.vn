---
title: "🎂 Tự Động Gửi Email Sinh Nhật Cá Nhân Hóa Với AI & Google Sheets"
description: "Workflow n8n tự động kiểm tra Google Sheets, dùng GPT-4o Mini tạo lời chúc sinh nhật độc đáo và gửi qua Gmail hàng ngày. Tiết kiệm thời gian, giữ kết nối với khách hàng và đồng nghiệp."
slug: "tu-dong-gui-email-sinh-nhat-ai-google-sheets"
tags: [n8n, automation, no-code, ai, gmail, google-sheets]
keywords: [n8n workflow, tự động hóa sinh nhật, email marketing, ai agent, google sheets automation]
---

# 🎂 Tự Động Gửi Email Sinh Nhật Cá Nhân Hóa Với AI & Google Sheets

Việc nhớ và gửi lời chúc sinh nhật cho hàng chục, hàng trăm khách hàng, đối tác hay đồng nghiệp là một thách thức lớn. Làm thủ công không chỉ tốn thời gian mà còn dễ bỏ sót, dẫn đến trải nghiệm khách hàng kém và mất đi cơ hội tăng cường quan hệ.

Workflow **Automated Birthday Emails** này giải quyết hoàn toàn bài toán đó. Nó hoạt động như một trợ lý ảo 24/7, tự động quét danh sách liên hệ trong Google Sheets mỗi ngày. Khi phát hiện ai đó có sinh nhật hôm nay, nó sẽ gọi AI (GPT-4o Mini) để viết một lời chúc sinh nhật **cá nhân hóa, sáng tạo và ấm áp**, sau đó tự động gửi qua Gmail. Các sếp không cần làm gì cả, chỉ cần ngồi chờ phản hồi tích cực từ người nhận!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian:** Không cần nhớ ngày sinh, không cần soạn email thủ công.
- **Cá nhân hóa tuyệt đối:** AI tạo ra lời chúc duy nhất cho từng người dựa trên tên và thông tin trong sheet, tránh cảm giác "spam" hàng loạt.
- **Tăng tương tác & Loyalty:** Khách hàng/cộng sự cảm thấy được quan tâm, từ đó tăng tỷ lệ phản hồi và giữ chân khách hàng.
- **Chính xác & Không bỏ sót:** Hệ thống tự động kiểm tra hàng ngày, đảm bảo không ai bị "quên".
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Google:** Bao gồm Google Sheets (để lưu danh sách) và Gmail (để gửi email).
2. **Tài khoản OpenRouter:** Đăng ký tại [openrouter.ai](https://openrouter.ai) để lấy API Key cho model GPT-4o Mini (hoặc các model tương thích khác).
3. **Google Sheet mẫu:** Tạo một sheet với các cột: `Name`, `Email`, `Birthday` (định dạng DD/MM/YYYY hoặc YYYY-MM-DD tùy cấu hình filter).
4. **Tài khoản n8n:** Cloud hoặc Self-hosted.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n của bạn.
2. Chọn **Import from URL** và dán link: `https://n8n.io/workflows/6201` hoặc copy JSON từ trang gốc và dán vào editor.
3. Workflow sẽ hiển thị 7 nodes chính.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

Đây là phần quan trọng nhất. Các sếp cần cấu hình từng node sau:

**1. Node: `Get row(s) in sheet` (Google Sheets)**
*   **Credentials:** Chọn hoặc tạo credentials `googleSheetsOAuth2Api`.
*   **Document ID:** Dán ID của Google Sheet chứa danh sách sinh nhật.
*   **Sheet Name:** Chọn đúng tên tab chứa dữ liệu.
*   **Operation:** Chọn `Get All` hoặc `Get`.

**2. Node: `Filter`**
*   Node này lọc ra những dòng có ngày sinh nhật trùng với ngày hiện tại.
*   **Lưu ý:** Đảm bảo cột `Birthday` trong Sheet của bạn có định dạng nhất quán. Nếu dùng định dạng `DD/MM/YYYY`, các sếp cần chỉnh logic filter để so sánh ngày và tháng hiện tại.
*   *Mẹo:* Nếu filter mặc định không hoạt động đúng với múi giờ Việt Nam, các sếp có thể thêm một node `Code` trước Filter để chuẩn hóa ngày tháng.

**3. Node: `AI Agent` & `OpenRouter Chat Model`**
*   **Credentials (OpenRouter):** Tạo credentials mới, chọn `OpenRouter API`, dán API Key của bạn.
*   **Model:** Mặc định là `openai/gpt-4o-mini`. Các sếp có thể đổi sang `anthropic/claude-3-haiku` hoặc model khác nếu muốn thay đổi giọng văn.
*   **System Prompt (Trong AI Agent):** Đây là "linh hồn" của email. Các sếp nên chỉnh sửa prompt để phù hợp với thương hiệu.
    *   *Ví dụ prompt:* "Bạn là một trợ lý quan hệ khách hàng thân thiện. Hãy viết một email chúc mừng sinh nhật ngắn gọn, ấm áp và chuyên nghiệp cho [Tên khách hàng]. Nhắc đến tên họ và gửi lời chúc tốt đẹp nhất. Kết thúc bằng chữ ký của [Tên công ty/bạn]."

**4. Node: `Send a message` (Gmail)**
*   **Credentials:** Chọn hoặc tạo credentials `gmailOAuth2`.
*   **To:** Chọn trường `Email` từ output của node trước đó.
*   **Subject:** Có thể để AI gợi ý hoặc đặt tĩnh như `Chúc mừng sinh nhật [Tên]!`.
*   **Message:** Chọn trường `output` từ node `AI Agent`.

**5. Node: `Structured Output Parser`**
*   Node này đảm bảo AI trả về dữ liệu ở định dạng JSON chuẩn (ví dụ: `{ "email_body": "..." }`) để node Gmail có thể đọc dễ dàng.
*   Đảm bảo schema trong node này khớp với prompt của AI Agent.

#### 3. Kích hoạt ⚡️
1. **Test Run:**
    *   Thêm một dòng dữ liệu mẫu vào Google Sheet với ngày sinh nhật là **hôm nay**.
    *   Chạy workflow (Execute Workflow).
    *   Kiểm tra hộp thư Gmail xem email đã được gửi chưa và nội dung AI tạo ra có ổn không.
2. **Bật Active:**
    *   Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải.
    *   Workflow sẽ tự động chạy mỗi ngày theo cấu hình của `Schedule Trigger` (mặc định thường là 00:00 hoặc 09:00).

### ✍️ Mẹo & gợi ý nâng cao
- **Gửi qua Telegram/Slack:** Thay vì chỉ gửi Gmail, các sếp có thể thêm node `Telegram` hoặc `Slack` để gửi lời chúc trực tiếp, tăng tỷ lệ đọc.
- **Đính kèm quà tặng:** Nếu có ngân sách, các sếp có thể tích hợp thêm node `Shopify` hoặc `Voucher API` để tự động tạo mã giảm giá sinh nhật và đính kèm vào email.
- **Lưu Log:** Thêm node `Google Sheets` (Append) sau khi gửi email thành công để ghi lại trạng thái "Đã gửi" vào cột `LastSentDate`, tránh gửi trùng lặp nếu chạy lại.
- **Đa ngôn ngữ:** Chỉnh prompt của AI Agent để yêu cầu viết lời chúc bằng tiếng Anh, Nhật, Hàn... tùy theo quốc gia của khách hàng.

### 📌 Kết luận
Việc duy trì mối quan hệ với khách hàng và đối tác là yếu tố sống còn trong kinh doanh. Với workflow này, các sếp có thể tự động hóa hoàn toàn quy trình chúc mừng sinh nhật một cách chuyên nghiệp và cá nhân hóa, mà không tốn bất kỳ công sức nào. Hãy import, cấu hình và để AI làm việc thay cho bạn ngay hôm nay!