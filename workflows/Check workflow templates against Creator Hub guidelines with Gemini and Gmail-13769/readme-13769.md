---
title: "🚀 Tự Động Kiểm Tra Workflow Theo Quy Định Creator Hub Với AI Gemini"
description: "Giải pháp tự động hóa 100% giúp kiểm tra tính tuân thủ của các template n8n so với quy định Creator Hub, gửi báo cáo chi tiết qua Gmail nhờ sức mạnh của AI Gemini."
slug: "kiem-tra-workflow-creator-hub-gemini"
tags: [n8n, automation, ai, gemini, google-gmail, no-code]
keywords: [n8n workflow, kiểm tra quy định, AI Gemini, tự động hóa báo cáo, creator hub]
---

# 🚀 Tự Động Kiểm Tra Workflow Theo Quy Định Creator Hub Với AI Gemini

Việc phát triển và chia sẻ các workflow n8n trên Creator Hub là một cách tuyệt vời để xây dựng cộng đồng và thể hiện kỹ năng kỹ thuật. Tuy nhiên, một trong những "nỗi đau" lớn nhất mà các nhà phát triển (developers) hay người dùng nâng cao gặp phải là việc **kiểm tra tính tuân thủ (compliance)** của workflow trước khi submit.

Quy định của Creator Hub thường xuyên thay đổi và khá khắt khe về cấu trúc, metadata, và chất lượng code. Việc kiểm tra thủ công từng dòng code, đối chiếu với tài liệu hướng dẫn, và viết báo cáo lỗi mất rất nhiều thời gian và dễ bỏ sót chi tiết.

Workflow này ra đời để giải quyết triệt để vấn đề đó. Nó sử dụng sức mạnh của **Google Gemini** (LLM) để phân tích code và cấu trúc workflow, đối chiếu với các quy tắc chuẩn, và tự động soạn thảo một email báo cáo chi tiết gửi thẳng vào hộp thư Gmail của bạn. Không cần code phức tạp, không cần đọc tài liệu hàng giờ – chỉ cần 1 click, bạn có ngay kết quả kiểm tra chuyên nghiệp.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian kiểm tra:** Thay vì mất 30-60 phút đọc tài liệu và code, AI xử lý trong vài giây.
- **Độ chính xác cao:** Gemini phân tích logic code và cấu trúc JSON theo đúng quy chuẩn kỹ thuật, giảm thiểu lỗi do con người bỏ sót.
- **Báo cáo chuyên nghiệp:** Nhận email với cấu trúc rõ ràng: Lỗi nghiêm trọng, Cảnh báo, và Gợi ý cải thiện.
- **Tích hợp liền mạch:** Kết nối trực tiếp từ Form Input -> AI Analysis -> Gmail, không cần trung gian.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản n8n:** Bản Self-hosted hoặc Cloud.
2. **Google API Key (Gemini):** Để sử dụng mô hình ngôn ngữ Gemini cho việc phân tích.
3. **Google OAuth2 Credentials:** Để kết nối và gửi email qua Gmail.
4. **Dữ liệu Workflow:** JSON của workflow cần kiểm tra (có thể dán trực tiếp vào Form hoặc gửi qua Webhook).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n Editor.
2. Chọn **Import from File** hoặc **Import from URL**.
3. Tải file JSON của workflow này (hoặc copy từ link gốc) và dán vào.
4. Lưu workflow với tên dễ nhớ, ví dụ: `Creator Hub Compliance Checker`.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Dựa trên các node chính trong workflow, các sếp cần cấu hình các điểm sau:

*   **Node: Form Trigger**
    *   Đây là điểm bắt đầu. Các sếp có thể tùy chỉnh các trường nhập liệu (ví dụ: tên workflow, mô tả, JSON code).
    *   *Mẹo:* Thêm trường "Category" hoặc "Tags" nếu muốn AI đánh giá thêm về phân loại.

*   **Node: HTTP Request (Tùy chọn)**
    *   Nếu workflow lấy dữ liệu từ nguồn bên ngoài (ví dụ: đọc file từ GitHub hoặc S3), các sếp cần cấu hình URL và Authentication (API Key/Token) tại đây.

*   **Node: Code (Pre-processing)**
    *   Node này thường dùng để làm sạch dữ liệu JSON trước khi đưa vào LLM.
    *   *Lưu ý:* Kiểm tra lại logic trong Code Node để đảm bảo nó xử lý đúng định dạng JSON mà Gemini nhận vào. Nếu JSON quá dài, cân nhắc cắt bớt các phần không liên quan (như metadata thừa) để tiết kiệm token.

*   **Node: Chain LLM (Gemini)**
    *   **Model:** Chọn model Gemini phù hợp (ví dụ: `gemini-1.5-flash` hoặc `gemini-1.5-pro` tùy độ phức tạp).
    *   **System Prompt:** Đây là "trái tim" của workflow. Các sếp cần đảm bảo prompt chứa đầy đủ **Quy định Creator Hub** (Guidelines).
        *   *Ví dụ prompt:* "Bạn là một chuyên gia kỹ thuật n8n. Hãy kiểm tra workflow JSON sau dựa trên các quy định: 1. Không có credentials hardcoded. 2. Tên node rõ ràng. 3. Có sticky note mô tả. 4. Xử lý lỗi (Error Workflow). Trả về kết quả dạng Markdown..."
    *   **Credentials:** Chọn Google Gemini API Key đã tạo.

*   **Node: Aggregate**
    *   Nếu workflow xử lý nhiều phần tử hoặc nhiều lần gọi API, node này giúp gộp kết quả lại thành một khối dữ liệu duy nhất trước khi gửi email.

*   **Node: Gmail**
    *   **Action:** Chọn `Send Email`.
    *   **To:** Địa chỉ email nhận báo cáo.
    *   **Subject:** Có thể động hóa, ví dụ: `Báo cáo kiểm tra: {{ $json.workflowName }}`.
    *   **Body:** Dán kết quả từ node LLM (thường là Markdown). Gmail hỗ trợ hiển thị Markdown khá tốt, hoặc các sếp có thể thêm một Code Node nhỏ để convert Markdown sang HTML nếu muốn email đẹp hơn.
    *   **Credentials:** Chọn Google OAuth2 đã kết nối.

#### 3. Kích hoạt ⚡️
1. **Test Run:** Dán một workflow JSON mẫu (có thể cố ý để 1 lỗi nhỏ) vào Form Trigger và chạy thử.
2. Kiểm tra email nhận được: Nội dung có chính xác không? Định dạng có dễ đọc không?
3. Nếu ổn, bật **Active** workflow để sẵn sàng sử dụng.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Telegram/Slack:** Thay vì chỉ gửi Gmail, các sếp có thể thêm node Telegram hoặc Slack để nhận thông báo nhanh trên điện thoại.
- **Lưu Log vào Google Sheets:** Thêm node Google Sheets để lưu lịch sử các lần kiểm tra, tên workflow, và trạng thái (Pass/Fail) để theo dõi xu hướng.
- **Tự động Fix (Auto-fix):** Với các lỗi đơn giản (như thiếu Sticky Note), các sếp có thể thêm một bước Code Node để AI không chỉ báo lỗi mà còn gợi ý code sửa, thậm chí tự động chèn vào JSON.
- **Định kỳ kiểm tra:** Nếu các sếp có nhiều workflow, có thể dùng Cron Trigger để tự động kiểm tra tất cả các workflow trong thư mục n8n hàng tuần.

### 📌 Kết luận
Việc tuân thủ quy định Creator Hub không còn là gánh nặng nếu các sếp biết tận dụng sức mạnh của AI. Workflow này giúp các sếp tiết kiệm hàng giờ làm việc thủ công, đảm bảo chất lượng sản phẩm trước khi công bố, và tập trung vào việc sáng tạo những workflow đột phá hơn. Hãy import và thử ngay hôm nay để trải nghiệm sự khác biệt!