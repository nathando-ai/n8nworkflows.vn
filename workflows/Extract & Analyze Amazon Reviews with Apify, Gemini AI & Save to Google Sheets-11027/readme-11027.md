---
title: "🚀 Tự động cào và phân tích đánh giá Amazon bằng Apify, Gemini AI & Google Sheets"
description: "Hướng dẫn xây dựng workflow n8n tự động trích xuất đánh giá Amazon, dùng Gemini AI phân tích lỗi, lưu vào Google Sheets và gửi thông báo Slack."
slug: "tu-dong-cao-va-phan-tich-danh-gia-amazon-voi-n8n"
tags: [n8n, automation, ai, apify, google-sheets, gemini, e-commerce]
keywords: [n8n workflow, phân tích đánh giá amazon, apify amazon reviews, gemini ai n8n, tự động hóa e-commerce]
---

# 🚀 Tự động hóa phân tích đánh giá Amazon với Gemini AI & n8n

Việc thủ công đọc hàng trăm, hàng ngàn đánh giá tiêu cực (1-2 sao) trên Amazon để tìm ra điểm yếu sản phẩm tốn rất nhiều thời gian của các Product Manager, nhà bán hàng FBA hay đội ngũ nghiên cứu thị trường. Phải mất bao nhiêu ngày để phân loại lỗi, tóm tắt khiếu nại và đưa ra giải pháp?

Quên cách làm thủ công đó đi! Workflow n8n này sẽ giúp các sếp tự động hóa 100% quy trình: Cào dữ liệu đánh giá từ Amazon qua **Apify**, nhờ **Google Gemini AI** mổ xẻ nguyên nhân gốc rễ và đề xuất cải tiến, tự động lưu trữ vào **Google Sheets**, đồng thời hú tin nhắn báo cáo qua **Slack** ngay khi hoàn thành. Không cần code, chỉ cần cấu hình một lần và chạy mãi mãi!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn cảnh copy/paste hay đọc từng review thủ công.
- **Thấu hiểu khách hàng (Voice of Customer):** AI tự động phân loại vấn đề (Chất lượng, Thiết kế, Vận chuyển...) và chấm điểm cảm xúc chính xác.
- **Đề xuất hành động thực tế:** Gemini AI không chỉ tóm tắt mà còn đưa ra kế hoạch cải tiến sản phẩm cụ thể.
- **Báo cáo tức thì:** Tự động hóa đồng bộ vào Google Sheets và thông báo qua Slack cho toàn bộ team.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n:** Đã cài đặt phiên bản Cloud hoặc Self-hosted.
- **Apify Account:** Tài khoản Apify để chạy actor `junglee/amazon-reviews-scraper`.
- **Google Cloud / Gemini API:** Tài khoản truy cập Google Gemini API và Google Sheets API.
- **Slack Workspace:** Tài khoản Slack để nhận thông báo hoàn tất batch.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ n8n template hoặc copy trực tiếp mã nguồn JSON, sau đó paste vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình các node cốt lõi sau:

- **Workflow Configuration (`Set`):** Khởi tạo các thông số cơ bản cho chu trình chạy.
- **Run an Actor and get dataset (`@apify/n8n-nodes-apify.apify`):** Điền Apify API Token vào mục credentials. Trong node này, hãy trỏ `startUrls` đến URL trang sản phẩm Amazon mà các sếp muốn phân tích (mặc định đang lọc các review 1 và 2 sao để tập trung vào phàn nàn).
- **Loop Over Reviews (`Split In Batches`):** Quản lý việc chia nhỏ dữ liệu review để xử lý tuần tự qua AI, tránh quá tải API.
- **Message a model (`Google Gemini`):** Kết nối tài khoản Google Gemini. **Lưu ý cực kỳ quan trọng:** Prompt trong node này hiện đang được cài đặt để trả kết quả bằng tiếng Nhật. Nếu các sếp muốn nhận kết quả bằng tiếng Việt hoặc tiếng Anh, hãy dịch lại đoạn prompt bên trong node này cho phù hợp.
- **Code (Parse JSON)1 (`Code`):** Node này dùng đoạn script nhỏ để bóc tách và định dạng lại cấu trúc JSON trả về từ Gemini AI, đảm bảo dữ liệu sạch trước khi đẩy vào Google Sheets.
- **Create spreadsheet (`Google Sheets`):** Kết nối tài khoản Google. Tạo trước một Google Sheet với các tiêu đề cột: `sentiment_score`, `category`, `summary`, `improvement`. Sau đó, dán Spreadsheet ID vào cấu hình của node.
- **Slack - Send Completion Notification (`Slack`):** Chọn kênh Slack (Channel) mà các sếp muốn nhận thông báo khi workflow hoàn tất việc quét và phân tích.

#### 3. Kích hoạt ⚡️
- Nhấn **Manual Trigger** hoặc chạy thử thủ công (Test step/Test workflow) với một vài dữ liệu mẫu để kiểm tra kết quả trên Google Sheets.
- Sau khi test thành công, bật công tắc **Active** góc trên cùng bên phải để workflow chạy tự động theo lịch hoặc trigger mong muốn.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm Telegram/Discord:** Ngoài Slack, các sếp có thể nhân bản node thông báo để bắn tin nhắn thẳng về nhóm Telegram cá nhân.
- **Lưu log lỗi:** Thêm nhánh Error Trigger để bắt lỗi nếu Apify không cào được dữ liệu hoặc API Gemini bị lỗi mạng.
- **Chạy tự động định kỳ:** Thay thế node Manual Trigger bằng Schedule Trigger để tự động quét đánh giá sản phẩm đối thủ mỗi tuần một lần, giúp các sếp cập nhật thị trường liên tục.

### 📌 Kết luận
Workflow này là "vũ khí bí mật" giúp các nhà bán hàng Amazon, D2C và các Product Manager nắm bắt nhanh chóng phản hồi tiêu cực của khách hàng để tối ưu hóa sản phẩm. Hãy cài đặt ngay hôm nay để tự động hóa toàn bộ quy trình nghiên cứu thị trường của các sếp!