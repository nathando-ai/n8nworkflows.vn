---
title: "🚀 Tự động ghi nhật ký calo món ăn qua LINE và AI Vision vào Google Sheets với n8n"
description: "Hướng dẫn xây dựng chatbot LINE tích hợp OpenAI Vision tự động nhận diện hình ảnh món ăn, tính toán calo và lưu trữ trực tiếp vào Google Sheets."
slug: "tu-dong-ghi-nhat-ky-calo-mon-an-qua-line-va-ai-vision-vao-google-sheets"
tags: [n8n, automation, line-bot, openai-vision, google-sheets, ai-agent]
keywords: [n8n workflow, tính calo món ăn, LINE bot AI, OpenAI Vision n8n, tự động hóa Google Sheets]
---

# 🚀 Tự động ghi nhật ký calo món ăn qua LINE và AI Vision vào Google Sheets

Các sếp có đang chật vật với việc ghi chép từng bữa ăn để theo dõi calo mỗi ngày? Việc nhập liệu thủ công rất dễ khiến chúng ta nản lòng chỉ sau vài ngày ngắn ngủi. Bài toán này sẽ được giải quyết triệt để với workflow n8n tự động hóa 100%: Chỉ cần chụp ảnh bữa ăn gửi qua **LINE**, trợ lý AI sẽ tự động phân tích món ăn, tính toán calo, ghi nhận vào **Google Sheets** và nhắn lại kết quả ngay lập tức!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Không cần nhập liệu thủ công, chỉ gửi ảnh hoặc tin nhắn chữ qua ứng dụng LINE quen thuộc.
- **AI thông minh đa phương thức (Multimodal)**: Nhận diện chính xác tên món ăn và ước tính lượng calo nhờ sức mạnh của OpenAI Vision.
- **Đồng bộ thời gian thực**: Dữ liệu dinh dưỡng tự động được băm vào Google Sheets để tiện theo dõi biểu đồ cân nặng/dinh dưỡng.
- **Tương tác 2 chiều**: Chatbot LINE phản hồi lại kết quả ngay lập tức cho người dùng sau khi xử lý xong.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản **n8n** (Cloud hoặc Self-hosted).
- **LINE Developers Account** (để tạo LINE Bot và lấy Channel Access Token).
- **OpenAI API Key** (hỗ trợ mô hình GPT-4o-mini hoặc các model vision tương thích).
- **Google Sheets** đã tạo sẵn file cấu trúc lưu trữ (Tên món, Calo, Thời gian...).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow (hoặc tải file) và import trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống kết nối mượt mà, các sếp chú ý cấu hình kỹ các node sau:
- **LINE webhook**: Cấu hình URL webhook nhận sự kiện từ LINE Messaging API và điền token xác thực ở node **send LINE** và **images download** (`{channel access token}`).
- **user verification**: Thiết lập điều kiện kiểm tra ID người dùng (`{your id}`) để đảm bảo chỉ có các sếp (hoặc người được cấp quyền) mới sử dụng được bot.
- **OpenAI Chat Model** & **Analyze image**: Điền thông tin **OpenAI API Key** và lựa chọn model phù hợp (ví dụ: `gpt-4o-mini` hoặc model hỗ trợ Vision).
- **Append row in sheet**: Chọn tài khoản kết nối Google Sheets (`googleSheetsOAuth2Api`), sau đó trỏ tới **Google Sheet ID** và Sheet Name tương ứng của các sếp.

#### 3. Kích hoạt ⚡️
- Thực hiện test run bằng cách gửi một bức ảnh món ăn hoặc tin nhắn văn bản vào LINE Bot vừa tạo.
- Kiểm tra dữ liệu đổ về Google Sheets và xem phản hồi trên LINE.
- Bật **Active workflow** để đưa hệ thống vào trạng thái vận hành tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo Telegram/Slack**: Gửi báo cáo tổng kết lượng calo tiêu thụ cuối ngày vào nhóm Telegram cá nhân.
- **Lưu trữ hình ảnh**: Kết hợp tải ảnh món ăn lên Google Drive hoặc AWS S3 kèm theo dòng dữ liệu trong Google Sheets để xem lại hình ảnh trực quan hơn.
- **Phân loại bữa ăn**: Mở rộng code JavaScript/Python ở node **Code** để tự động phân loại bữa Sáng, Trưa, Tối hoặc Ăn vặt dựa trên thời gian gửi tin nhắn.

### 📌 Kết luận
Một trợ lý dinh dưỡng cá nhân hoàn toàn miễn phí, tự động hóa hoàn toàn đã sẵn sàng phục vụ các sếp. Nhanh tay "lên đồ" ngay hôm nay để quản lý vóc dáng và sức khỏe tốt hơn nhé!