---
title: "🚀 Đánh giá độ chính xác AI với String Similarity trong n8n Advanced AI"
description: "Hướng dẫn xây dựng workflow n8n đo lường độ tương đồng chuỗi ký tự (String Similarity) để đánh giá chất lượng trích xuất mã code từ hình ảnh."
slug: "danh-gia-do-chinh-xac-ai-string-similarity-n8n"
tags: [n8n, automation, ai, evaluation, openai, string-similarity]
keywords: [n8n workflow, đánh giá AI, string similarity, n8n evaluation, OCR handwriting, tự động hóa n8n]
---

# 🚀 Đánh giá độ chính xác AI với String Similarity trong n8n Advanced AI

Các sếp đang xây dựng các ứng dụng AI như trích xuất văn bản, đọc chữ viết tay hay OCR hình ảnh nhưng lại đau đầu vì không biết làm sao để đo lường chính xác chất lượng đầu ra của mô hình? Việc kiểm tra thủ công từng kết quả vừa tốn thời gian, vừa thiếu khách quan khi dữ liệu lớn.

Bài viết này sẽ hướng dẫn các sếp cách thiết lập một workflow n8n tự động hóa hoàn toàn việc đánh giá mô hình AI (Model Evaluation). Workflow này sử dụng phương pháp đo lường độ tương đồng chuỗi ký tự (**String Similarity**) để so sánh kết quả thực tế từ AI với đáp án mẫu trong dataset.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa đánh giá AI:** Không còn phải chấm điểm thủ công từng bản ghi trong dataset kiểm thử.
- **Đo lường chính xác:** Tính toán điểm số tương đồng (score từ 0 đến 1) giữa mã code trích xuất từ hình ảnh viết tay và đáp án chuẩn.
- **Tích hợp Advanced AI:** Kết hợp linh hoạt giữa OpenAI Vision (trích xuất chữ từ ảnh) và hệ thống Evaluation sẵn có của n8n.
- **Tối ưu hóa mô hình:** Dễ dàng tinh chỉnh prompt hoặc đổi model dựa trên các số liệu (metrics) cụ thể thay vì cảm tính.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Hỗ trợ tính năng Advanced AI / Evaluation (phiên bản n8n mới nhất).
- **OpenAI API Key:** Cho node **Extract code from image** (sử dụng GPT-4o hoặc model hỗ trợ Vision).
- **Google Sheets Dataset:** Tài khoản kết nối Google Sheets để đọc bộ dữ liệu kiểm thử (Test dataset).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể sử dụng file JSON của workflow mẫu từ n8n (ID: `4274`) và import trực tiếp vào giao diện n8n Editor của mình bằng cách chọn **Add workflow** -> **Import from File** hoặc dán trực tiếp chuỗi JSON.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động mượt mà với dữ liệu của các sếp, hãy lưu ý cấu hình các node sau:
- **When fetching a dataset row (`evaluationTrigger`):** Kết nối tài khoản Google Sheets của các sếp và trỏ tới [Test dataset mẫu](https://docs.google.com/spreadsheets/d/1uuPS5cHtSNZ6HNLOi75A2m8nVWZrdBZ_Ivf58osDAS8/edit?gid=1786963566#gid=1786963566) chứa danh sách hình ảnh chữ viết tay và đáp án chuẩn.
- **Extract code from image (`openAi`):** Chọn Credentials OpenAI đã thiết lập. Đảm bảo cấu hình đúng resource là `image` và operation là `analyze` để AI tiến hành đọc và bóc tách đoạn code từ URL hình ảnh.
- **Calc string distance (`code`):** Node này chứa đoạn mã JavaScript thực hiện thuật toán tính khoảng cách hoặc độ tương đồng chuỗi giữa chuỗi AI trả về và chuỗi đáp án thực tế. Điểm số hoàn hảo đạt mức `1`.
- **Set metrics & Evaluating? (`evaluation`):** Các node cốt lõi trong hệ thống Evaluation của n8n dùng để ghi nhận điểm số và thiết lập chỉ số đánh giá tổng quan cho toàn bộ quá trình chạy thử nghiệm (Evaluation Run).

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test Run**) bằng cách kích hoạt chế độ Evaluation trên n8n để hệ thống duyệt qua từng dòng trong Google Sheets dataset.
- Kiểm tra kết quả trả về ở các node metrics xem điểm số String Similarity đã chính xác chưa.
- Bật **Active** workflow nếu muốn lưu trữ và chạy định kỳ hàng loạt.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng metric:** Ngoài String Similarity, các sếp có thể viết thêm code trong node JavaScript để tính thêm các chỉ số khác như Levenshtein Distance hoặc Token Overlap.
- **Lưu lịch sử đánh giá:** Kết nối thêm một node **Google Sheets** hoặc **Notion** ở cuối luồng để lưu lại lịch sử chấm điểm qua từng lần thay đổi prompt AI, giúp dễ dàng so sánh hiệu suất (versioning prompt).
- **Thông báo qua Telegram/Slack:** Thêm node gửi thông báo tổng kết điểm số đánh giá vào nhóm chat nội bộ mỗi khi quá trình chạy evaluation hoàn tất.

### 📌 Kết luận
Việc tự động hóa đánh giá chất lượng AI bằng n8n Evaluation và String Similarity sẽ giúp các sếp tiết kiệm hàng giờ đồng hồ test thủ công, đồng thời đảm bảo sản phẩm AI luôn đạt chất lượng cao nhất trước khi đưa vào ứng dụng thực tế. Chúc các sếp "lên đồ" thành công!