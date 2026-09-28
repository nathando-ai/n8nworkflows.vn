---
title: "🚀 Xuất lịch sử trò chuyện của AI Agent từ Postgres sang Google Sheets tự động"
description: "Hướng dẫn tự động hóa đồng bộ log hội thoại của AI Agent từ cơ sở dữ liệu Postgres/Supabase sang Google Sheets, tạo riêng từng tab cho mỗi session."
slug: "xuat-lich-su-ai-agent-tu-postgres-sang-google-sheets"
tags: [n8n, automation, ai-agent, postgres, google-sheets, no-code]
keywords: [n8n workflow, ai agent logs, postgres to google sheets, tu dong hoa n8n, quan ly chat memory n8n]
---

# 🚀 Xuất lịch sử trò chuyện của AI Agent từ Postgres sang Google Sheets tự động

Các sếp đang xây dựng AI Agent trên n8n và lưu trữ lịch sử trò chuyện (chat memory) vào cơ sở dữ liệu Postgres hoặc Supabase? Chắc các sếp sẽ gặp khó khăn khi muốn đọc, kiểm tra (review) hoặc phân tích các đoạn hội thoại này một cách trực quan cùng team mà không phải chui vào database tra cứu thủ công.

Bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ xịn sò được thiết kế bởi *Agent Studio*. Workflow này sẽ tự động lấy toàn bộ lịch sử chat từ Postgres, tạo riêng một tab (sheet) tương ứng cho từng `session_id` trên Google Sheets, và cập nhật nội dung đồng bộ liên tục.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%**: Không cần copy/paste dữ liệu thủ công từ DB ra file Excel.
- **Trực quan hóa dữ liệu**: Mỗi phiên chat (`session_id`) sẽ được lưu vào một tab riêng biệt trên Google Sheets với các trường rõ ràng: Người nói (`Who`), Nội dung (`Message`), Thời gian (`Date`).
- **Luôn cập nhật mới nhất**: Dữ liệu được làm mới tự động theo lịch hẹn (Schedule) hoặc chạy thủ công.
- **Dễ dàng cộng tác**: Team sản phẩm, chăm sóc khách hàng có thể dễ dàng đọc, phân tích và đánh giá chất lượng trả lời của AI Agent ngay trên Google Sheets.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n đang hoạt động.
- Cơ sở dữ liệu Postgres (hoặc Supabase) có bảng lưu trữ lịch sử chat của n8n AI Agent (thường là bảng `n8n_chat_histories`).
- Tài khoản Google Drive / Google Sheets và thông tin kết nối OAuth2 đã được tích hợp vào n8n.
- Sử dụng file mẫu Google Sheets chuẩn: 👉 [Google Sheets Template Mẫu](https://docs.google.com/spreadsheets/d/14bKI5J0h18Nv48jbe1IXpZWma6EtqYLFWnpKoCB5Bgc/edit?usp=sharing)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy mã JSON của workflow này hoặc import file JSON trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà không gặp lỗi, các sếp cần chú ý cấu hình kỹ các node sau:

- **Node `add create_at column` (Postgres)**: 
  - Nếu bảng chat history của các sếp chưa có cột `created_at` để lưu thời gian tin nhắn, hãy chạy lệnh SQL bổ sung cột này trước khi thực thi workflow.
  - Nhớ thay đổi tên bảng chat memory trong câu lệnh SQL cho khớp với hệ thống của sếp (ví dụ: `n8n_chat_histories`).
  - *Dành cho người dùng Supabase*: Hãy lấy thông tin kết nối từ phần "Transaction pooler" > "View parameters" trong Supabase để cấu hình credentials Postgres trên n8n cho ổn định lâu dài.

- **Node `Postgres - Get session ids`**:
  - Kiểm tra lại câu lệnh SQL truy vấn danh sách `session_id` để đảm bảo nó lấy đúng các phiên chat cần xuất dữ liệu.

- **Các node Google Sheets (`Duplicate template sheet`, `Clear Sheet Content`, `Rename Sheet`, `Add conversations`)**:
  - Thay thế **Document ID** mặc định của file template bằng Google Sheet ID của chính các sếp.
  - Đảm bảo tab đầu tiên (index 0) của file Google Sheets có các tiêu đề cột (headers) ở hàng đầu tiên gồm: `Who`, `Message`, `Date`.
  - *Lưu ý về lỗi ẩn*: Node `Clear Sheet Content` có thể báo lỗi đỏ nếu `session_id` chưa tồn tại trên file Sheets (do đây là lần đầu xuất phiên chat đó). Đừng hoảng hốt, đây là cơ chế bình thường vì workflow sẽ tự tạo tab mới ngay sau đó.

#### 3. Kích hoạt ⚡️
- Bấm nút **‘Test workflow’** để chạy thử nghiệm xem dữ liệu từ Postgres có đổ về các tab Google Sheets chính xác chưa.
- Sau khi test thành công, bật trạng thái **Active** ở góc trên bên phải màn hình n8n để workflow tự động chạy theo lịch trình (Schedule Trigger).

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp thông báo Telegram/Slack**: Thêm một node Telegram hoặc Slack vào cuối workflow để nhận thông báo tổng kết mỗi khi quá trình đồng bộ log hoàn tất.
- **Tùy biến lịch chạy (Schedule Trigger)**: Có thể chỉnh lịch chạy tự động hàng ngày vào lúc nửa đêm hoặc chạy hàng tuần tùy vào lượng hội thoại của AI Agent.
- **Gom nhóm User**: Nếu cấu hình AI Agent ghi đè `session_id` bằng một `user_id` cố định, các sếp có thể dễ dàng theo dõi toàn bộ lịch sử trò chuyện của một khách hàng xuyên suốt nhiều phiên khác nhau trên cùng một tab.

### 📌 Kết luận
Việc kiểm soát và phân tích lịch sử trò chuyện của AI Agent là chìa khóa quan trọng để cải thiện chất lượng câu trả lời và trải nghiệm người dùng. Với workflow n8n này, các sếp đã có ngay một hệ thống tự động hóa gọn nhẹ, chuyên nghiệp mà không tốn một đồng chi phí phần mềm bên thứ ba nào. Áp dụng ngay thôi các sếp ơi!