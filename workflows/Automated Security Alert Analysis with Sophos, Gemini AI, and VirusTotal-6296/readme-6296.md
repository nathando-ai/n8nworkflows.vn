---
title: "🚀 Tự Động Phân Tích Cảnh Báo Bảo Mật Sophos Với Gemini AI & VirusTotal"
description: "Workflow n8n giúp tự động hóa quy trình xử lý cảnh báo bảo mật từ Sophos, sử dụng Gemini AI và VirusTotal để phân tích sâu, giảm tải áp lực cho đội ngũ SecOps."
slug: "tu-dong-phan-tich-canh-bao-bao-mat-sophos-gemini"
tags: [n8n, automation, no-code, SecOps, AI, Cybersecurity]
keywords: [n8n workflow, tự động hóa bảo mật, Sophos, Gemini AI, VirusTotal, SecOps]
---

# 🚀 Tự Động Phân Tích Cảnh Báo Bảo Mật Sophos Với Gemini AI & VirusTotal

Trong môi trường an ninh mạng hiện đại, các đội ngũ SecOps thường xuyên phải đối mặt với "bão" cảnh báo (alert fatigue). Khi một hệ thống như Sophos phát hiện mối đe dọa, việc kiểm tra thủ công từng cảnh báo, tra cứu hash trên VirusTotal và tổng hợp thông tin có thể mất hàng giờ, dẫn đến chậm trễ trong việc ứng phó.

Workflow này giải quyết triệt để vấn đề đó bằng cách tự động hóa toàn bộ quy trình: Nhận cảnh báo từ Sophos, tra cứu thông tin chi tiết trên VirusTotal, và sử dụng sức mạnh của **Google Gemini AI** để phân tích, tóm tắt mức độ nghiêm trọng và đề xuất hành động. Kết quả được gửi ngay lập tức qua Telegram, giúp các sếp ra quyết định nhanh chóng mà không cần mở bất kỳ dashboard bảo mật nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, đặc biệt khi xử lý các request API liên tục từ Sophos và VirusTotal, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Giảm thời gian phản ứng (MTTR):** Tự động hóa việc thu thập dữ liệu và phân tích, giúp phản hồi cảnh báo trong vài giây thay vì vài phút/hour.
- **Phân tích thông minh:** Gemini AI không chỉ liệt kê dữ liệu mà còn diễn giải ngữ cảnh, đánh giá rủi ro và gợi ý bước tiếp theo.
- **Tích hợp đa nguồn:** Kết hợp liền mạch dữ liệu từ Sophos (nguồn cảnh báo) và VirusTotal (nguồn xác thực độc hại).
- **Thông báo tức thì:** Nhận cảnh báo đã được "chế biến" dễ đọc ngay trên Telegram, phù hợp để xử lý từ xa.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Sophos:** Có khả năng gửi Webhook khi có sự kiện bảo mật (cần cấu hình trong Sophos Central).
2. **Tài khoản VirusTotal:** API Key để tra cứu hash/file.
3. **Tài khoản Google AI Studio:** API Key cho Google Gemini.
4. **Tài khoản Telegram:** Bot Token và Chat ID để nhận thông báo.
5. **n8n Instance:** Chạy trên VPS hoặc local.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n Editor.
2. Chọn **Import from URL** hoặc **Import from File** và dán link workflow hoặc file JSON.
3. Workflow sẽ hiển thị với 9 nodes chính.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

Dưới đây là các node quan trọng cần cấu hình chi tiết:

*   **Node: `Webhook`**
    *   **Path:** Thay `replace-with-your-webhook-path` bằng một đường dẫn duy nhất (ví dụ: `sophos-alert`).
    *   **Cấu hình Sophos:** Trong Sophos Central, tạo một Webhook mới và chỉ định URL đầy đủ của n8n (ví dụ: `https://your-n8n-domain.com/webhook/sophos-alert`). Đảm bảo phương thức là POST.

*   **Node: `If`**
    *   Node này dùng để lọc dữ liệu. Các sếp nên kiểm tra điều kiện để đảm bảo chỉ xử lý các cảnh báo có liên quan (ví dụ: chỉ xử lý khi `severity` là `High` hoặc `Critical`) nhằm tránh spam thông báo.

*   **Node: `Virus_Total`**
    *   **Authentication:** Chọn hoặc tạo Credentials mới cho VirusTotal.
    *   **API Key:** Điền API Key của bạn vào phần Credentials.
    *   **URL:** Đảm bảo URL trỏ đúng endpoint tra cứu hash/file của VirusTotal.

*   **Node: `For_Gemini_Prompt` (Code Node)**
    *   Đây là node JavaScript dùng để định dạng dữ liệu thô từ Sophos và VirusTotal thành một prompt rõ ràng cho AI.
    *   **Lưu ý:** Nếu cấu trúc dữ liệu từ Sophos của bạn khác với mẫu gốc, các sếp cần chỉnh sửa code trong node này để trích xuất đúng các trường như `file_hash`, `threat_name`, `source_ip`.

*   **Node: `Google Gemini Chat Model`**
    *   **Credentials:** Chọn Credentials Google Gemini đã tạo.
    *   **Model:** Chọn model phù hợp (ví dụ: `gemini-1.5-flash` hoặc `gemini-1.5-pro`) tùy theo độ phức tạp của phân tích cần thiết.

*   **Node: `AI Agent`**
    *   **System Prompt:** Đây là "trái tim" của workflow. Hãy chỉnh sửa prompt để phù hợp với chính sách bảo mật của công ty.
    *   *Ví dụ:* "Bạn là một chuyên gia SecOps. Dựa trên dữ liệu cảnh báo từ Sophos và kết quả VirusTotal, hãy: 1. Tóm tắt mối đe dọa. 2. Đánh giá mức độ rủi ro (Thấp/Trung bình/Cao). 3. Đề xuất 3 bước xử lý khẩn cấp. Trả lời ngắn gọn, chuyên nghiệp."
    *   **Memory:** Node `Simple Memory` được gắn vào để AI có thể nhớ ngữ cảnh nếu có nhiều cảnh báo liên tiếp (tùy chọn).

*   **Node: `Send a text message` (Telegram)**
    *   **Credentials:** Chọn Credentials Telegram Bot.
    *   **Chat ID:** Điền Chat ID của kênh hoặc cá nhân nhận thông báo.
    *   **Message:** Đảm bảo tham số `text` trỏ đến output của AI Agent (ví dụ: `{{ $json.output }}` hoặc tương tự tùy cấu trúc).

#### 3. Kích hoạt ⚡️
1. **Test Run:** Gõ một cảnh báo mẫu vào Webhook (có thể dùng Postman hoặc curl) để kiểm tra luồng dữ liệu.
2. Kiểm tra xem Telegram có nhận được tin nhắn phân tích từ Gemini không.
3. Nếu ổn, bật nút **Active** ở góc trên bên phải n8n.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Ticketing:** Thêm node Jira hoặc ServiceNow để tự động tạo ticket khi AI đánh giá rủi ro là "Cao".
- **Lưu trữ Log:** Thêm node Google Sheets hoặc Database để lưu lại lịch sử các cảnh báo và kết quả phân tích của AI, phục vụ cho việc báo cáo định kỳ.
- **Cảnh báo đa kênh:** Nếu Telegram không phản hồi, có thể thêm nhánh Slack hoặc Email để đảm bảo thông báo luôn được gửi đi.
- **Tùy chỉnh Prompt:** Thử nghiệm các prompt khác nhau để Gemini AI cung cấp phân tích sâu hơn về kỹ thuật (ví dụ: phân tích chuỗi khai báo IOC - Indicators of Compromise).

### 📌 Kết luận
Workflow này là một ví dụ điển hình về việc kết hợp AI vào quy trình SecOps, giúp biến dữ liệu thô thành thông tin hành động (actionable intelligence). Bằng cách tự động hóa việc phân tích Sophos với Gemini và VirusTotal, các sếp có thể tập trung vào việc xử lý sự cố thay vì mất thời gian tra cứu thông tin. Hãy triển khai ngay để nâng cao năng lực phản ứng trước các mối đe dọa mạng!