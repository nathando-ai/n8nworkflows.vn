---
title: "🚀 Phân tích đối thủ chạy Facebook Ads tự động bằng AI (Gemini & OpenAI)"
description: "Tự động hóa hoàn toàn quy trình phân tích quảng cáo Facebook của đối thủ bằng AI. Cào dữ liệu, phân tích hình ảnh/video bằng Gemini & OpenAI và lưu báo cáo vào Google Sheets."
slug: "phan-tich-doi-thu-facebook-ads-tu-dong-gemini-openai"
tags: [n8n, automation, no-code, facebook-ads, openai, gemini, marketing]
keywords: [n8n workflow, phân tích facebook ads, ai marketing, openai n8n, gemini video decode, tự động hóa marketing]
---

# 🚀 Phân tích đối thủ chạy Facebook Ads tự động bằng AI (Gemini & OpenAI)

Các sếp làm marketing chắc hẳn đều đau đầu mỗi khi phải ngồi soi hàng trăm mẫu quảng cáo của đối thủ trên Facebook Ad Library. Việc xem thủ công từng hình ảnh, video, đọc từng câu headline rồi tổng hợp lại thành báo cáo tốn rất nhiều thời gian mà góc nhìn lại dễ bị chủ quan.

Đừng lo, workflow n8n cực đỉnh này sẽ giúp các sếp tự động hóa 100% quy trình "đọc vị" đối thủ: từ việc nhận yêu cầu qua form, cào dữ liệu quảng cáo, cho đến việc dùng sức mạnh của AI (OpenAI & Gemini) để phân tích chi tiết hình ảnh, video và xuất file báo cáo thẳng vào Google Sheets. Tất cả diễn ra hoàn toàn tự động!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không còn phải thủ công tải hình ảnh, video hay ghi chép thông tin quảng cáo của đối thủ.
- **Phân tích đa phương tiện thông minh:** AI tự động đọc hiểu cả nội dung chữ, hình ảnh tĩnh và giải mã cả nội dung video quảng cáo của đối thủ.
- **Bóc tách chiến lược sắc bén:** Nhận diện ngay góc tiếp cận (angle), thông điệp chính (hook) và hình thức triển khai của đối thủ để tối ưu hóa chiến dịch của chính mình.
- **Dữ liệu tập trung sẵn sàng:** Toàn bộ kết quả phân tích được đồng bộ tự động vào Google Sheets để team marketing dễ dàng xem và thảo luận.
:::

### ⚙️ Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- **n8n Instance:** Đã cài đặt sẵn sàng (bản Cloud hoặc Self-hosted).
- **OpenAI API Key:** Dành cho node `OpenAI` để phân tích text và hình ảnh.
- **Google Gemini API Key:** Dành cho node `Gemini Video Decode` để xử lý và phân tích video quảng cáo.
- **Google Sheets Credentials:** Tài khoản Google để kết nối và lưu dữ liệu vào Google Sheets.
- **Dịch vụ cào dữ liệu Ads (Scrape Ads):** API hoặc dịch vụ bên thứ ba dùng để lấy thông tin từ Facebook Ad Library.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow này hoặc copy trực tiếp mã nguồn.
- Trong giao diện n8n Editor, chọn **Add workflow** -> Nhấn vào dấu `...` ở góc trên bên phải -> Chọn **Import from File** hoặc **Import from Clipboard** và dán mã JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 13 nodes hoạt động nhịp nhàng, các sếp cần chú ý cấu hình kỹ các node trọng điểm sau:

- **On form submission (`formTrigger`):** Tạo một giao diện form đơn giản để các sếp nhập từ khóa hoặc tên trang fanpage của đối thủ cần phân tích.
- **Scrape Ads (`httpRequest`):** Điền endpoint hoặc API key của dịch vụ cào dữ liệu Facebook Ads để hệ thống lấy danh sách các mẫu quảng cáo đang chạy.
- **Switch (`switch`):** Node này dùng để phân loại loại hình quảng cáo (là dạng hình ảnh hay video) nhằm điều hướng dòng dữ liệu đi đúng nhánh xử lý phù hợp.
- **OpenAI (`openAi`):** Cấu hình Credentials OpenAI, viết prompt hướng dẫn AI đóng vai chuyên gia Marketing để phân tích nội dung chữ và hình ảnh của mẫu quảng cáo.
- **Gemini Video Decode (`httpRequest`) & Download Video (`httpRequest`):** Tải video quảng cáo của đối thủ về và gửi qua API của Gemini để AI xem video, phiên âm hoặc tóm tắt thông điệp cốt lõi.
- **Loop Over Items (`splitInBatches`) & Wait (`wait`):** Giúp xử lý danh sách quảng cáo theo từng lô nhỏ (batches) và có thời gian chờ (delay) hợp pháp để tránh bị các hệ thống API quét giới hạn tốc độ (Rate Limit).
- **Save (`googleSheets`):** Chọn file Google Sheets đích và map chính xác các trường dữ liệu (`Final Image Values`, `Final Video Values`) vào các cột tương ứng trên Sheet (Tiêu đề, Link, Phân tích của AI, Loại quảng cáo...).

#### 3. Kích hoạt ⚡️
- Nhấn **Test workflow** bằng cách gửi một form mẫu để kiểm tra xem dữ liệu có chảy qua toàn bộ các node không lỗi không.
- Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để hệ thống chính thức đi vào hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm node Telegram hoặc Slack ngay sau node `Save` để bot tự động bắn báo cáo nóng về group chat mỗi khi phân tích xong một đối thủ mới.
- **Lên lịch định kỳ (Cron):** Thay thế `formTrigger` bằng node `Schedule Trigger` để hệ thống tự động quét và báo cáo đối thủ mỗi tuần/mỗi tháng mà không cần ai phải bấm form thủ công.
- **Mở rộng nền tảng:** Có thể áp dụng mô hình tương tự để cào và phân tích quảng cáo trên TikTok Ad Library hoặc Google Ads Transparency Center.

### 📌 Kết luận
Việc nghiên cứu đối thủ (Competitive Analysis) chưa bao giờ dễ dàng và trực quan đến thế nhờ sự trợ giúp của AI kết hợp cùng n8n. Hãy thiết lập ngay workflow này để team marketing của các sếp luôn đi trước đối thủ một bước trong việc nắm bắt xu hướng quảng cáo! Chúc các sếp cài đặt thành công!