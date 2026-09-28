---
title: "🚀 Tự động trích xuất thông tin cuộc họp từ Google Sheets với Groq AI và Gmail"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình phân tích biên bản cuộc họp, trích xuất action items bằng Groq AI và gửi thông báo qua Gmail."
slug: "tu-dong-trich-xuat-thong-tin-cuoc-hop-google-sheets-groq-gmail"
tags: [n8n, automation, no-code, groq, google-sheets, gmail, ai-summarization]
keywords: [n8n workflow, tự động hóa cuộc họp, groq ai, google sheets automation, trích xuất action items]
---

# 🚀 Tự động trích xuất thông tin cuộc họp từ Google Sheets với Groq AI và Gmail

Các sếp có bao giờ cảm thấy ngợp trước đống biên bản cuộc họp (meeting notes) dài dằng dặc, mất hàng giờ đồng hồ để đọc lại, lọc ra danh sách việc cần làm (action items), rủi ro và gửi email tổng hợp cho team? Việc làm thủ công này vừa tẻ nhạt, dễ bỏ sót nhiệm vụ quan trọng lại vừa tốn kém thời gian nhân sự.

Giải pháp ở đây là gì? Workflow n8n này sẽ tự động hóa 100% quy trình: lấy ghi chú từ Google Sheets, sử dụng sức mạnh siêu tốc của **Groq AI** để phân tích, trích xuất thông tin cốt lõi, lưu trữ lại kết quả có cấu trúc và tự động gửi email tóm tắt qua **Gmail**. Các sếp chỉ việc ngồi nhâm nhi cà phê và nhận báo cáo!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không cần đọc lại biên bản dài dòng, AI tự động lọc ra các điểm chính trong tích tắc.
- **Không bỏ sót việc:** Các action items, việc cần theo dõi (follow-ups) và rủi ro (risks) được phân loại rõ ràng, minh bạch.
- **Đồng bộ dữ liệu mượt mà:** Tự động lưu vào Google Sheets, đánh dấu trạng thái đã xử lý để tránh trùng lặp.
- **Cải thiện giao tiếp:** Gửi email tóm tắt chuyên nghiệp ngay lập tức cho người dùng hoặc các bên liên quan.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản sau:
- **n8n Instance** (Cloud hoặc Self-hosted).
- **Tài khoản Google** (để kết nối Google Sheets và Gmail).
- **Groq API Key** (Đăng ký miễn phí tại [Groq Console](https://console.groq.com/)).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã JSON của workflow (hoặc tải file JSON từ nguồn) và dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 10 nodes phối hợp nhịp nhàng. Các sếp chú ý cấu hình các điểm mấu chốt sau:
- **Groq Chat Model (`lmChatGroq`)**: Kết nối tài khoản bằng Groq API Key và chọn model phù hợp (ví dụ: `openai/gpt-oss-120b` hoặc các model LLM hỗ trợ xử lý text nhanh của Groq).
- **Fetch Meeting Notes (`googleSheets`)**: Kết nối tài khoản Google Sheets của các sếp, chọn đúng File ID và Sheet chứa dữ liệu ghi chú cuộc họp đầu vào.
- **Check Unprocessed Records (`if`)**: Node điều kiện này giúp lọc ra các dòng dữ liệu chưa được xử lý (tránh chạy lại các bản ghi cũ).
- **Extract Insights using AI (`agent`)**: Cấu hình prompt cho AI agent để hướng dẫn nó trích xuất chính xác các trường thông tin: Action Items, Follow-ups và Risks dưới dạng JSON cấu trúc.
- **Format Extracted Data (`code`)**: Node Javascript code giúp parse kết quả JSON từ AI thành các text field gọn gàng, dễ đọc.
- **Mark Record as Processed (`googleSheets`)**: Cấu hình chế độ `update` để đánh dấu dòng dữ liệu trên Google Sheets là "đã xử lý" sau khi chạy xong.
- **Store Extracted Insights (`googleSheets`)**: Cấu hình chế độ `append` để lưu các insights đã trích xuất vào một sheet đích quản lý kết quả.
- **Summary Email (`gmail`)**: Kết nối tài khoản Gmail và thiết lập địa chỉ người nhận, tiêu đề cũng như định dạng nội dung email tóm tắt.

#### 3. Kích hoạt ⚡️
- Bấm nút **Execute Workflow** chạy thử với một dòng dữ liệu mẫu thông qua node **Starting Trigger (`manualTrigger`)** để kiểm tra xem email và dữ liệu Sheets có trả về chuẩn chỉnh không.
- Nếu mọi thứ mượt mà, gạt công tắc sang **Active** để workflow tự động hoạt động!

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Chatbot:** Kết hợp thêm node Telegram hoặc Slack để bắn thông báo tóm tắt cuộc họp ngay vào group chat của team thay vì chỉ gửi qua email.
- **Định kỳ tự động hóa:** Thay thế `manualTrigger` bằng `Schedule Trigger` (Cron node) để n8n tự quét Google Sheets kiểm tra bản ghi mới mỗi giờ hoặc mỗi ngày.
- **Quản lý lỗi (Error Handling):** Thêm Error Trigger để nếu Groq API gặp sự cố gián đoạn, hệ thống sẽ tự động gửi cảnh báo về Telegram cho quản trị viên.

### 📌 Kết luận
Với workflow n8n kết hợp giữa Google Sheets, Groq AI và Gmail này, việc tổng hợp và quản lý biên bản cuộc họp sẽ không còn là gánh nặng thủ công. Hãy triển khai ngay hôm nay để tối ưu hóa năng suất vận hành cho đội ngũ của các sếp!