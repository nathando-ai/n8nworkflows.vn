---
title: "🚀 Tự Động Phân Loại Email Hỗ Trợ Với GPT-4, Gmail & Trello"
description: "Giải pháp tự động hóa 100% quy trình xử lý email hỗ trợ khách hàng: Phân loại ưu tiên bằng AI, tạo ticket Trello, cảnh báo Slack và gửi phản hồi tự động."
slug: "tu-dong-phan-loai-email-ho-tro-gpt4-gmail-trello"
tags: [n8n, automation, no-code, ai-agent, customer-support, trello]
keywords: [n8n workflow, tự động hóa email, AI support, trello automation, gmail trigger]
---

# 🚀 Tự Động Phân Loại Email Hỗ Trợ Với GPT-4, Gmail & Trello

Trong môi trường kinh doanh hiện đại, hộp thư đến (inbox) của bộ phận hỗ trợ khách hàng thường xuyên bị quá tải. Việc đọc từng email, xác định mức độ khẩn cấp, tạo ticket thủ công và soạn thảo phản hồi không chỉ tốn thời gian mà còn dễ dẫn đến sai sót hoặc bỏ lỡ các vấn đề nghiêm trọng.

Workflow này là giải pháp "chìa khóa trao tay" giúp các sếp tự động hóa toàn bộ quy trình triage (phân loại) email hỗ trợ. Sử dụng sức mạnh của **GPT-4** (qua OpenAI), workflow sẽ tự động đọc nội dung email, phân tích cảm xúc, xác định mức độ ưu tiên, tạo ticket trên **Trello**, gửi cảnh báo khẩn cấp qua **Slack** cho các vấn đề nghiêm trọng, và thậm chí soạn thảo email phản hồi tự động. Tất cả đều diễn ra tức thì, không cần một dòng code nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian xử lý:** Loại bỏ hoàn toàn thao tác thủ công trong việc đọc, phân loại và tạo ticket.
- **Phản ứng nhanh với sự cố nghiêm trọng:** Hệ thống tự động gửi cảnh báo Slack ngay lập tức khi phát hiện email có tính chất khẩn cấp (Critical).
- **Chuẩn hóa quy trình hỗ trợ:** Mọi email đều được ghi log vào Google Sheets và tạo ticket Trello thống nhất, dễ dàng truy vết.
- **Cá nhân hóa phản hồi:** AI soạn thảo email phản hồi dựa trên ngữ cảnh cụ thể của khách hàng, tăng trải nghiệm người dùng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị các tài khoản và credentials sau:
- **Gmail Account:** Tài khoản Gmail dùng để nhận email hỗ trợ (cần bật OAuth2).
- **OpenAI API Key:** Key để gọi mô hình GPT-4 (hoặc GPT-3.5) cho việc phân tích và soạn thảo.
- **Trello API Key & Token:** Để tạo thẻ (card) tự động trên board hỗ trợ.
- **Slack Webhook URL:** Để gửi thông báo cảnh báo vào kênh Slack nội bộ.
- **Google Sheets:** Một bảng tính (Sheet) đã được tạo sẵn với các cột phù hợp để lưu log dữ liệu.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập trang [n8n.io/workflows/6552](https://n8n.io/workflows/6552).
2. Copy toàn bộ mã JSON của workflow.
3. Mở n8n Editor của bạn, vào **Workflows** -> **Import from URL** hoặc **Import from File** (nếu đã tải file JSON).
4. Dán mã JSON vào và nhấn **Import**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình lại các node sau để khớp với hạ tầng của mình:

1. **Node: Gmail Trigger**
   - Chọn **Credentials** Gmail của bạn.
   - Cấu hình **Filter**: Chỉ kích hoạt khi nhận được email mới (New Email) và có thể lọc theo tiêu đề hoặc người gửi nếu cần.

2. **Node: AI Agent for Triage, Sentiment & Drafting**
   - Chọn **OpenAI Credentials** (API Key).
   - Kiểm tra **System Prompt**: Đây là "bộ não" của workflow. Prompt hiện tại yêu cầu AI trả về JSON chứa: `priority` (Low/Medium/High/Critical), `sentiment`, `summary`, và `draft_response`. Các sếp có thể tùy chỉnh prompt này để phù hợp với giọng văn thương hiệu của mình.

3. **Node: Parse AI Output**
   - Node Code này dùng để tách JSON từ phản hồi của AI. Đảm bảo cấu trúc JSON trả về từ AI khớp với logic parse ở đây.

4. **Node: Check for Critical Issues**
   - Node If này kiểm tra trường `priority` từ bước trước.
   - **True Branch:** Nếu ưu tiên là "Critical" hoặc "High", nó sẽ đi tới node Slack.
   - **False Branch:** Đi tiếp vào quy trình tạo ticket thông thường.

5. **Node: High-Priority Alert (Slack)**
   - Chọn **Slack Credentials**.
   - Điền **Channel ID** (ví dụ: `#support-alerts`).
   - Chỉnh sửa nội dung tin nhắn để bao gồm tên khách hàng và tóm tắt vấn đề.

6. **Node: Create Support Ticket (Trello)**
   - Chọn **Trello Credentials**.
   - Chọn **Board ID** và **List ID** (ví dụ: List "To Do" hoặc "In Progress").
   - Cấu hình **Card Title** và **Card Description** để lấy dữ liệu từ output của AI (Summary, Email content, Priority).

7. **Node: Automate Response (If)**
   - Logic ở đây thường kiểm tra xem có nên gửi email tự động không (ví dụ: chỉ gửi cho các vấn đề Low/Medium, hoặc gửi cho tất cả). Các sếp có thể điều chỉnh điều kiện này.

8. **Node: Send a message (Gmail)**
   - Chọn **Gmail Credentials** (tài khoản gửi email).
   - Điền **To**: Lấy từ email gốc.
   - **Subject**: Có thể thêm prefix như `[Auto-Reply]`.
   - **Message**: Lấy trường `draft_response` từ output của AI.

9. **Node: Log Data (Google Sheets)**
   - Chọn **Google Sheets Credentials**.
   - Chọn **Spreadsheet ID** và **Sheet Name**.
   - Ánh xạ các cột: Timestamp, Email From, Subject, Priority, Sentiment, Summary, Ticket ID (nếu có).

#### 3. Kích hoạt ⚡️
1. Nhấn **Execute Workflow** để chạy thử với dữ liệu mẫu (nếu có) hoặc gửi một email test vào hộp thư Gmail đã cấu hình.
2. Kiểm tra xem:
   - Email có được phân loại đúng không?
   - Ticket Trello có được tạo không?
   - Slack có nhận cảnh báo không (nếu là email khẩn)?
   - Email phản hồi có được gửi đi không?
3. Nếu mọi thứ ổn, bật công tắc **Active** ở góc trên bên phải để workflow chạy liên tục.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp CRM:** Thay vì chỉ lưu vào Google Sheets, các sếp có thể thêm node để cập nhật trạng thái khách hàng trong CRM (HubSpot, Salesforce) để đồng bộ dữ liệu.
- **Phân loại theo sản phẩm:** Mở rộng prompt AI để nhận diện loại sản phẩm/dịch vụ khách hàng đang gặp vấn đề, từ đó tạo ticket vào các List Trello riêng biệt.
- **Gửi báo cáo định kỳ:** Thêm một workflow khác chạy hàng tuần để tổng hợp dữ liệu từ Google Sheets và gửi báo cáo thống kê (số lượng ticket, tỷ lệ ưu tiên cao, v.v.) cho quản lý.
- **Học hỏi từ phản hồi:** Lưu trữ các trường hợp AI phản hồi sai hoặc khách hàng không hài lòng để cải thiện prompt trong tương lai.

### 📌 Kết luận
Với workflow **Automated Email Support Triage**, các sếp có thể biến hộp thư hỗ trợ từ một "điểm nghẽn" thành một cỗ máy tự động thông minh. Không chỉ tiết kiệm hàng giờ làm việc mỗi tuần, hệ thống còn đảm bảo không có khách hàng nào bị bỏ rơi, đặc biệt là những trường hợp khẩn cấp. Hãy import và tùy chỉnh ngay hôm nay để nâng tầm dịch vụ khách hàng của doanh nghiệp bạn!