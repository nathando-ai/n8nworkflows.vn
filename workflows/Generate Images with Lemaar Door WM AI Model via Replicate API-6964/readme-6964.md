---
title: "🚀 Tự Động Tạo Ảnh Độc Bản Với AI Model Replicate Trong n8n"
description: "Hướng dẫn chi tiết cách xây dựng workflow n8n tự động hóa quy trình tạo ảnh nghệ thuật sử dụng mô hình AI Lemaar Door WM thông qua Replicate API."
slug: "tao-anh-tu-dong-voi-lemaar-door-wm-replicate-api-n8n"
tags: [n8n, automation, replicate, ai-image-generation, no-code, content-creation]
keywords: [n8n workflow, tạo ảnh ai, replicate api, lemaar door wm, tự động hóa n8n]
---

# 🚀 Tự Động Tạo Ảnh Độc Bản Với AI Model Replicate Trong n8n

Việc tạo ra các nội dung hình ảnh độc quyền, chất lượng cao phục vụ cho chiến dịch marketing hay sáng tạo nội dung thường ngốn rất nhiều thời gian nếu làm thủ công. Thay vì phải truy cập thủ công vào các nền tảng AI, nhập prompt và tải về từng tấm ảnh, các sếp hoàn toàn có thể tự động hóa toàn bộ quy trình này bằng n8n. 

Workflow **"Generate Images with Lemaar Door WM AI Model via Replicate API"** (được chia sẻ bởi chuyên gia Yaron Been) chính là giải pháp hoàn hảo. Workflow này sẽ kết nối trực tiếp với mô hình AI chuyên dụng trên Replicate để tự động tạo và xử lý hình ảnh một cách mượt mà, không cần can thiệp thủ công.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Gửi yêu cầu tạo ảnh và nhận lại kết quả trực tiếp trong n8n mà không cần thao tác tay.
- **Tối ưu thời gian:** Loại bỏ hoàn toàn thời gian chờ đợi và chuyển đổi tab trình duyệt rườm rà.
- **Linh hoạt tích hợp:** Dễ dàng mở rộng kết nối với Google Sheets, Telegram, Slack hoặc Email để tự động gửi ảnh vừa tạo đi các kênh mong muốn.
- **Quy trình chuẩn hóa:** Quản lý lịch sử và trạng thái tạo ảnh (Prediction) thông qua các node kiểm tra tự động.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một hệ thống n8n đang hoạt động (Cloud hoặc Self-hosted).
- Tài khoản trên [Replicate](https://replicate.com/) và lấy **Replicate API Token**.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow này và dán trực tiếp vào giao diện n8n Editor của mình, hoặc import thông qua file JSON mẫu.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 8 nodes được bố trí rất khoa học để xử lý quá trình gọi API bất đồng bộ từ Replicate. Các sếp cần chú ý cấu hình các node sau:

- **Set API Key (`Set API Key` node):** 
  - Tại đây, các sếp cần thêm biến chứa Replicate API Key của mình. Hãy thay thế giá trị mẫu bằng token thật được cấp từ tài khoản Replicate.
- **Tạo tiến trình (`Create Prediction` node - HTTP Request):** 
  - Node này sẽ gửi POST request tới Replicate API sử dụng mô hình `creativeathive/lemaar-door-wm`. 
  - Các sếp cần cấu hình **Prompt** đầu vào tùy theo ý tưởng sáng tạo hình ảnh của mình.
- **Trích xuất ID (`Extract Prediction ID` node - Code):** 
  - Node này dùng đoạn mã JS ngắn để bóc tách `Prediction ID` trả về từ bước khởi tạo, làm cơ sở để kiểm tra trạng thái ảnh.
- **Đợi và Kiểm tra trạng thái (`Wait` & `Check Prediction Status` & `Check If Complete`):** 
  - Do việc tạo ảnh bằng AI mất một khoảng thời gian ngắn, node `Wait` sẽ tạm dừng một nhịp trước khi HTTP Request gọi lại API kiểm tra xem quá trình render đã hoàn tất hay chưa (`If` node sẽ phân nhánh tiếp tục đợi hay lấy kết quả).
- **Xử lý kết quả (`Process Result` node - Code):** 
  - Trích xuất đường dẫn URL của bức ảnh hoàn chỉnh để sử dụng cho các bước tiếp theo trong hệ thống.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** tại node `On clicking 'execute'` (Manual Trigger) để chạy thử nghiệm lần đầu và kiểm tra kết quả trả về.
- Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để workflow sẵn sàng hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
Để khai thác tối đa sức mạnh của workflow này, các sếp có thể mở rộng thêm:
1. **Tích hợp Google Sheets:** Lưu lại danh sách prompt và link ảnh kết quả tự động vào một bảng tính quản lý nội dung.
2. **Gửi thông báo qua Telegram/Slack:** Tự động bắn hình ảnh vừa tạo vào nhóm chat nội bộ ngay khi AI render xong.
3. **Kết hợp AI Content:** Dùng một node OpenAI/Anthropic ở bước trước để tự động sinh prompt chi tiết, sau đó đẩy thẳng vào workflow tạo ảnh này để tạo ra một dây chuyền sản xuất nội dung tự động hoàn toàn.

### 📌 Kết luận
Việc tự động hóa tạo ảnh với AI thông qua n8n và Replicate API không chỉ giúp tiết kiệm hàng giờ đồng hồ làm việc thủ công mà còn mở ra vô số ý tưởng sáng tạo nội dung quy mô lớn cho doanh nghiệp. Hãy bắt tay vào cài đặt ngay hôm nay các sếp nhé!