---
title: "🚀 Tự động trích xuất Google Trends và tổng hợp bài viết vào Google Sheets với n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động bắt xu hướng từ Google Trends RSS, cào nội dung bài viết bằng Jina.ai và lưu trữ gọn gàng vào Google Sheets."
slug: "tu-dong-trich-xuat-google-trends-va-tong-hop-bai-viet-google-sheets"
tags: [n8n, automation, google-trends, google-sheets, content-marketing, jina-ai]
keywords: [n8n workflow, google trends automation, cào dữ liệu google trends, jina ai scraping, tự động hóa marketing]
---

# 🚀 Tự động trích xuất Google Trends và tổng hợp bài viết vào Google Sheets

Các anh em làm content marketing, SEO hay nghiên cứu thị trường chắc chắn hiểu cảm giác mệt mỏi cỡ nào khi phải liên tục "canh" Google Trends để bắt trend thủ công. Mỗi lần bắt được từ khóa hot lại phải click vào từng bài báo liên quan, đọc lướt và tóm tắt lại để lên ý tưởng bài viết. Quá tốn thời gian và dễ bỏ lỡ cơ hội vàng!

Đừng lo, bài viết này sẽ hướng dẫn các sếp cách thiết lập một **n8n workflow tự động 100%**: tự động đọc RSS Google Trends mỗi giờ, lọc từ khóa mới, cào nội dung từ các bài báo liên quan và gom lại thành một bản tóm tắt hoàn chỉnh ngay trong Google Sheets. Không một dòng code phức tạp, chỉ cần vài bước "lên đồ" là chạy mượt mà!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không sợ sập, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Bắt trend thần tốc:** Hệ thống tự động quét Google Trends đều đặn mỗi giờ (lệch 1 phút so với thời điểm Google cập nhật RSS).
- **Loại bỏ trùng lặp:** Tự động đối chiếu với Google Sheets hiện có, chỉ lưu các từ khóa mới tinh chưa từng xuất hiện.
- **Tóm tắt thông minh:** Tự động cào nội dung từ các URL đính kèm trong trend và tổng hợp lại vào file quản lý (Editorial plan).
- **Làm giàu dữ liệu tự động:** Trạng thái (Status) được lưu sẵn, sẵn sàng kích hoạt các chuỗi automation tiếp theo như gửi thông báo Telegram hoặc Slack.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** (Self-hosted hoặc n8n Cloud).
- **Google Sheets:** Một file Google Sheet được chuẩn bị sẵn các cột để lưu từ khóa, lượng traffic, URL và nội dung tóm tắt.
- **Google Sheets Credentials:** Kết nối tài khoản Google trong n8n.
- **Jina.ai API Key:** Dùng để cào nội dung text sạch từ các URL bài báo đi kèm với Google Trends.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể sử dụng file JSON của workflow này (lấy từ link gốc n8n.io/workflows/3132) và copy dán trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 15 nodes được thiết kế tỉ mỉ. Các sếp cần chú ý cấu hình các điểm mấu chốt sau:
- **Node `CONFIG` (Set):** Cấu hình các thông số quan trọng như `min_traffic` (lọc lượng traffic tối thiểu từ RSS), `max_result` (giới hạn số lượng RSS cần cào) và điền `jina_key` của dịch vụ Jina.ai.
- **Node `Start every hour past 11 minutes` (scheduleTrigger):** Đặt lịch chạy tự động mỗi giờ (Google Trends cập nhật RSS mỗi 10 phút, trigger này chạy lệch 1 phút để đảm bảo dữ liệu mới nhất).
- **Node `Get saved keywords` & `Google Sheets` (googleSheets):** Chọn đúng Credentials tài khoản Google của các sếp, trỏ tới đúng file Google Sheet (Editorial plan) và tên sheet cụ thể.
- **Nodes `content1`, `content2`, `content3` (httpRequest):** Sử dụng API của Jina.ai để trích xuất nội dung văn bản từ 3 URL bài báo đính kèm trong mỗi từ khóa xu hướng.
- **Node `If we have scraped min 1 url -> Save` (if) & `All scraping node failed...` (noOp):** Đảm bảo hệ thống kiểm tra kỹ dữ liệu, nếu việc cào HTML thất bại toàn tập thì sẽ không lưu rác vào database.

#### 3. Kích hoạt ⚡️
- Bấm nút **`When clicking ‘Test workflow’`** để chạy thử nghiệm xem dữ liệu từ RSS có đổ về Google Sheets thành công hay không.
- Sau khi kiểm tra dữ liệu chuẩn chỉnh, gạt công tắc sang **Active** để workflow tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm node Telegram hoặc Slack ngay sau node `Google Sheets` để nhận thông báo tức thì mỗi khi có từ khóa trend mới được ghi nhận.
- **Kết hợp AI (OpenAI / Claude):** Thay vì chỉ gom nội dung thô từ 3 trang web, các sếp có thể chèn thêm một node AI (như OpenAI) để viết sẵn bài sơ lược (brief) hoặc tiêu đề chuẩn SEO dựa trên từ khóa đó.
- **Mở rộng Editorial Plan:** Tận dụng cột `status` trong Google Sheets để làm điều kiện lọc cho các automation viết bài tự động tiếp theo.

### 📌 Kết luận
Việc bắt trend và nghiên cứu từ khóa chưa bao giờ dễ dàng đến thế khi đã có tự động hóa hỗ trợ. Hãy thiết lập ngay workflow này để tối ưu hóa quy trình sản xuất nội dung của đội ngũ, giúp các sếp luôn đi trước đối thủ một bước!