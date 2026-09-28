---
title: "🚀 Tự động tạo Cold Email cá nhân hóa bằng GPT-4o-mini và Google Sheets"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình viết cold email tiếp cận khách hàng tiềm năng cực kỳ cá nhân hóa với AI GPT-4o-mini và Google Sheets."
slug: "tu-dong-tao-cold-email-ca-nhan-hoa-gpt-4o-mini-google-sheets"
tags: [n8n, automation, no-code, lead-nurturing, ai, openai, google-sheets]
keywords: [n8n workflow, cold email automation, GPT-4o-mini, tự động hóa email, google sheets n8n]
---

# 🚀 Tự động tạo Cold Email cá nhân hóa bằng GPT-4o-mini và Google Sheets

Viết cold email thủ công cho từng khách hàng tiềm năng (prospects) là một công việc cực kỳ tốn thời gian, nhàm chán nhưng lại đóng vai trò quyết định trong việc chốt sale. Nếu gửi email chung chung (mass email), tỷ lệ phản hồi sẽ vô cùng thấp. 

Được thiết kế bởi chuyên gia tự động hóa **Rana Tamure** (Founder & CEO của LetsAutomate), workflow n8n này sẽ giải quyết trọn vẹn bài toán trên. Hệ thống tự động đọc danh sách khách hàng từ Google Sheets, sử dụng sức mạnh của AI (**GPT-4o-mini**) để viết email chào hàng cực kỳ cá nhân hóa dựa trên mô tả doanh nghiệp của họ, sau đó tự động cập nhật kết quả ngược lại vào bảng tính. Tất cả diễn ra tự động 100% không cần code!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn cảnh cặm cụi nghiên cứu từng công ty và tự soạn từng nội dung email.
- **Cá nhân hóa đỉnh cao:** AI tự động phân tích thông tin/mô tả doanh nghiệp của từng khách hàng để viết tiêu đề (Subject) và nội dung (Body) phù hợp nhất.
- **Đồng bộ dữ liệu mượt mà:** Mọi email được tạo ra sẽ tự động điền lại vào Google Sheets để các sếp dễ dàng kiểm duyệt hoặc chuyển qua chiến dịch gửi mail.
- **Vận hành tự động:** Xử lý danh sách hàng loạt với cơ chế chia lô thông minh (`Loop Over Items`).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Đã cài đặt hoặc sử dụng n8n Cloud.
- **Google Sheets:** Chuẩn bị sẵn một file Google Sheet chứa thông tin khách hàng (bao gồm các cột cơ bản như: Tên, Email, Mô tả doanh nghiệp/Prospect description).
- **OpenAI API Key:** Tài khoản OpenAI có tích hợp model `GPT-4o-mini` để AI tiến hành viết email.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ hệ thống n8n (Link gốc: [n8n.io/workflows/7583](https://n8n.io/workflows/7583)) và chọn **Import from File** hoặc copy trực tiếp mã JSON dán vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 6 nodes chính, các sếp cần tập trung cấu hình kỹ các điểm sau:

- **Node `When clicking ‘Test workflow’` (`manualTrigger`):** Dùng để kích hoạt thủ công khi test hệ thống.
- **Node `Add Row1` & `Update row in sheet` (`googleSheets`):** 
  - Kết nối tài khoản Google thông qua `Google Sheets OAuth2 API`.
  - Chọn đúng file Google Sheet và Sheet Name mà các sếp đã chuẩn bị chứa danh sách khách hàng (lưu ý cột chứa email, tên và mô tả doanh nghiệp).
  - Ở node `Update row in sheet`, cấu hình Operation là `Update` để ghi đè hoặc bổ sung nội dung email AI vừa tạo vào dòng tương ứng của khách hàng đó.
- **Node `Loop Over Items` (`splitInBatches`):** Giúp chia nhỏ danh sách khách hàng thành từng batch để AI xử lý lần lượt, tránh quá tải request.
- **Node `email writer` (`openAi`):**
  - Kết nối `OpenAI API`.
  - Chọn model **GPT-4o-mini**.
  - **Prompt Customization:** Các sếp cần tùy chỉnh lại câu lệnh (Prompt) trong node này sao cho phù hợp với dịch vụ/sản phẩm của doanh nghiệp mình, hướng dẫn AI cách xưng hô và phong cách viết email chào hàng (Cold email).
- **Node `Code1` (`code`):** Node JavaScript nhỏ này có nhiệm vụ bóc tách kết quả trả về từ AI thành 2 phần riêng biệt: **Subject (Tiêu đề)** và **Body (Nội dung email)** để dễ dàng đẩy về Google Sheets.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để chạy thử với vài dòng dữ liệu mẫu xem AI viết email có mượt mà không.
- Sau khi kiểm tra dữ liệu trong Google Sheets đã được cập nhật chính xác, các sếp có thể thay thế Trigger thủ công bằng Schedule Trigger (nếu muốn chạy định kỳ) và bật **Active** workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp gửi mail tự động:** Kết hợp thêm node Gmail hoặc Resend ngay sau bước tạo email để hệ thống tự động gửi đi thay vì chỉ lưu vào Google Sheets.
- **Thêm bước duyệt qua Slack/Telegram:** Tạo thông báo đẩy về nhóm chat để đội ngũ Sale duyệt (Approve) nội dung email trước khi hệ thống chính thức gửi đi.
- **Lưu log & theo dõi trạng thái:** Thêm cột "Status" trong Google Sheets để đánh dấu các khách hàng đã được "Generated Email" hoặc "Sent".

### 📌 Kết luận
Workflow tạo Cold Email cá nhân hóa bằng GPT-4o-mini và Google Sheets là trợ thủ đắc lực giúp tối ưu hóa phễu tiếp cận khách hàng. Hãy áp dụng ngay để tăng tốc chiến dịch outbound sales của doanh nghiệp các sếp ngày hôm nay!