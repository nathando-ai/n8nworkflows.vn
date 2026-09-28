---
title: "🚀 Tự động trích xuất hóa đơn từ Gmail bằng GPT-4o và gửi thông báo qua Slack"
description: "Hướng dẫn xây dựng workflow n8n tự động quét email chưa đọc trong Gmail, sử dụng AI Agent với mô hình GPT-4o để phân tích, trích xuất dữ liệu hóa đơn và gửi thông báo trực tiếp lên Slack."
slug: "trich-xuat-hoa-don-gmail-gpt-4o-slack"
tags: [n8n, automation, no-code, openai, gmail, slack, ai-agent]
keywords: [n8n workflow, tự động hóa hóa đơn, trích xuất hóa đơn gmail, gpt-4o ai agent, n8n slack notification]
---

# 🚀 Tự động trích xuất hóa đơn từ Gmail bằng GPT-4o và gửi thông báo qua Slack

Các sếp có bao giờ cảm thấy mệt mỏi khi phải thủ công kiểm tra hàng đống email đến mỗi ngày, lọc ra các hóa đơn (invoice), đọc từng dòng để lấy số tiền, hạn thanh toán và nhập liệu hay chưa? Việc làm thủ công này không chỉ tốn thời gian mà còn rất dễ bỏ sót hoặc nhầm lẫn hạn thanh toán.

Đừng lo, bài toán này sẽ được giải quyết triệt để với workflow n8n tự động hóa 100%. Sự kết hợp mạnh mẽ giữa **Gmail**, **AI Agent (GPT-4o)** và **Slack** sẽ giúp các sếp tự động săn lùng hóa đơn, phân tích thông tin cực kỳ thông minh và bắn thông báo ngay lập tức lên kênh Slack của team.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Quét email định kỳ mỗi giờ, không cần bận tâm click thủ công.
- **Trích xuất thông minh bằng AI:** Sử dụng GPT-4o để nhận diện chính xác email nào là hóa đơn và bóc tách các trường dữ liệu quan trọng (số tiền, ngày đáo hạn, tên nhà cung cấp...).
- **Cảnh báo tức thì:** Gửi thông báo chi tiết thẳng vào Slack, giúp team kế toán hoặc quản lý nắm bắt kịp thời để thanh toán đúng hạn.
- **Tùy biến linh hoạt:** Dễ dàng mở rộng prompt để AI nhận diện thêm các loại tài liệu khác như biên nhận (receipts) hay hợp đồng (contracts).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **n8n Instance:** Đã cài đặt sẵn sàng (Cloud hoặc Self-hosted).
- **Tài khoản Gmail:** Có quyền cấu hình OAuth2 kết nối với n8n để đọc email.
- **Tài khoản Slack:** Có quyền kết nối OAuth2 để gửi tin nhắn thông báo.
- **OpenAI API Key:** Đã có sẵn số dư hoặc tài khoản để gọi mô hình `gpt-4o`.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trên giao diện n8n, sau đó copy toàn bộ mã JSON của workflow này dán trực tiếp vào Editor, hoặc import file JSON theo tài liệu gốc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động trơn tru, hãy chú ý cấu hình kỹ các node sau:

- **Schedule Trigger:** Node này mặc định chạy mỗi giờ một lần (`every hour`). Các sếp có thể bấm vào node này để thay đổi chu kỳ chạy (ví dụ: 30 phút/lần hoặc chạy theo khung giờ cố định) tùy thuộc vào nhu cầu thực tế của doanh nghiệp.
- **Get Unread Emails (Gmail):** Kết nối tài khoản Gmail của các sếp qua OAuth2 và thiết lập operation lấy tất cả email chưa đọc (`getAll`).
- **Check If Email is Invoice (If):** Node điều kiện giúp lọc các email thực sự liên quan đến hóa đơn dựa trên kết quả phân tích từ bước trước.
- **AI Agent & OpenAI Chat Model:** 
  - Chọn model `gpt-4o` trong node `OpenAI Chat Model`.
  - Cấu hình API Key của OpenAI.
  - Node `AI Agent` sẽ đóng vai trò đọc nội dung email, nhận diện xem có phải hóa đơn hay không, kết hợp cùng **Structured Output Parser** để trả về dữ liệu đúng định dạng cấu trúc JSON mong muốn. Các sếp có thể tùy chỉnh prompt trong AI Agent nếu muốn phát hiện thêm các loại email khác (biên lai, hợp đồng...).
- **Notify Slack User (Slack):** Kết nối tài khoản Slack của team qua OAuth2. Các sếp có thể tùy chỉnh lại định dạng tin nhắn thông báo (Ví dụ: `Thanh toán hóa đơn từ {{sender}} hạn chót vào ngày {{due_date}}`) và đưa thêm các chi tiết vào phần nội dung notes.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** chạy thử với dữ liệu mẫu (hoặc email thực tế) để kiểm tra xem AI bóc tách dữ liệu và Slack nhận thông báo đã chuẩn form chưa.
- Sau khi test thành công, bật công tắc **Active** ở góc trên cùng bên phải để workflow tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Lưu trữ tự động:** Kết hợp thêm node **Google Sheets** hoặc **Airtable** ngay sau bước AI Agent để tự động lưu toàn bộ thông tin hóa đơn vào bảng tính, phục vụ việc quản lý tài chính cuối tháng.
- **Nhóm thông báo:** Thay vì gửi cho cá nhân, hãy đẩy thông báo vào một Channel Slack riêng biệt của phòng Kế toán (`#finance-alerts`) để mọi người cùng theo dõi.
- **Xử lý file đính kèm:** Mở rộng workflow bằng cách tải xuống các file PDF hóa đơn đính kèm trong email và lưu trực tiếp lên Google Drive.

### 📌 Kết luận
Workflow tích hợp GPT-4o và Gmail này là một "vũ khí" cực kỳ lợi hại giúp tối ưu hóa quy trình kế toán, loại bỏ hoàn toàn các thao tác nhập liệu thủ công nhàm chán. Hãy triển khai ngay hôm nay để tiết kiệm thời gian và không bao giờ bỏ lỡ bất kỳ hạn thanh toán nào của doanh nghiệp!