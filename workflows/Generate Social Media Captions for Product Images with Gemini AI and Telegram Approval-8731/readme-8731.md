---
title: "🚀 Tự động tạo Caption mạng xã hội từ hình ảnh sản phẩm bằng Gemini AI và Phê duyệt qua Telegram"
description: "Khám phá workflow n8n tự động phân tích ảnh sản phẩm bằng Google Gemini, tạo caption và hashtag, gửi qua Telegram để phê duyệt thủ công trước khi tự động đăng lên Twitter."
slug: "tu-dong-tao-caption-anh-san-pham-gemini-telegram-twitter"
tags: [n8n, automation, no-code, gemini-ai, telegram, twitter, content-creation]
keywords: [n8n workflow, ai caption, google gemini ai, telegram approval bot, auto tweet, tu dong hoa content]
---

# 🚀 Tự động tạo Caption mạng xã hội từ hình ảnh sản phẩm bằng Gemini AI và Phê duyệt qua Telegram

Các sếp có đang cảm thấy mệt mỏi khi mỗi lần ra mắt sản phẩm mới lại phải hì hục tải ảnh lên, nghĩ caption, viết hashtag rồi căn chỉnh để đăng lên Twitter (X) hay các mạng xã hội khác? Việc làm thủ công này vừa tốn thời gian, vừa dễ bỏ sót khung giờ vàng đăng bài.

Giải pháp ở đây là gì? Một hệ thống tự động hóa 100% không cần code (No-code) với **n8n** sẽ giúp các sếp giải quyết triệt để vấn đề này. Workflow này sẽ tự động "soi" ảnh sản phẩm, nhờ **Google Gemini AI** viết content cực cuốn, gửi thẳng vào **Telegram** để các sếp duyệt (hoặc yêu cầu viết lại), và tự động "lên sóng" Twitter ngay khi nhận được cái gật đầu.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không lo gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không còn cảnh nghĩ caption vắt óc hay thao tác thủ công từng bước.
- **AI thông minh, đa phương thức:** Google Gemini tự động nhận diện chi tiết sản phẩm từ hình ảnh để tạo ra nội dung chuẩn chỉnh, kèm hashtag bắt trend.
- **Kiểm soát tuyệt đối:** Tích hợp nút duyệt bài trực tiếp trên Telegram (Phê duyệt ✅, Viết lại 🔄, hoặc Hủy bỏ ❌) trước khi nội dung chính thức xuất hiện trên mạng xã hội.
- **Vận hành tự động 24/7:** Chỉ cần ném ảnh vào kho lưu trữ, mọi việc còn lại cứ để bot lo.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow chạy mượt mà, các sếp cần chuẩn bị sẵn các tài khoản và credentials sau:
1. **Google Drive Account:** Nơi lưu trữ hình ảnh sản phẩm đầu vào.
2. **Google Gemini API Key:** Để AI phân tích ảnh và sinh nội dung (caption + hashtag).
3. **Telegram Bot Token:** Dùng để gửi thông báo, hình ảnh và nhận lệnh phê duyệt.
4. **Twitter (X) Developer Account:** Cung cấp API credentials để bot tự động đăng bài.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow từ nguồn cung cấp, sau đó vào giao diện n8n Editor chọn **Add workflow** -> Dán (Paste) trực tiếp vào bảng làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống không báo lỗi, các sếp cần cấu hình chính xác các node sau:

- **Google Drive Trigger:** Kết nối tài khoản Google Drive và chọn thư mục nguồn chuyên chứa ảnh sản phẩm. Khi có ảnh mới tải lên, trigger sẽ kích hoạt.
- **Product_Img, Product_Img_1, Product_Img2:** Các node tải tệp hình ảnh từ Google Drive để chuyển tiếp dữ liệu xử lý.
- **Analyze image & Message a model (Google Gemini):** Điền thông tin Google Gemini API credentials. Tại đây, AI sẽ phân tích hình ảnh sản phẩm (`analyze image`) và viết nội dung caption kèm 5 hashtag phù hợp (`message a model`).
- **Send_Photo & Ask_For_Approval / Regenerate_Discard (Telegram):** Kết nối Telegram Bot Credentials. Node `Ask_For_Approval` sử dụng tính năng `sendAndWait` độc đáo của n8n để dừng workflow chờ các sếp bấm nút tương tác trên Telegram.
- **Request_Media_ID (HTTP Request):** Node quan trọng giúp upload hình ảnh trực tiếp lên server Twitter nhằm lấy mã `Media_ID`, giúp bài đăng Twitter hiển thị kèm hình ảnh sản phẩm sinh động.
- **Create Tweet (Twitter):** Cấu hình tài khoản Twitter OAuth2 để đăng bài viết chính thức sau khi nhận lệnh duyệt từ Telegram.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và tải thử một tấm ảnh lên thư mục Google Drive đã chọn để test luồng chạy.
- Kiểm tra tin nhắn Telegram xem bot đã gửi ảnh và bảng lựa chọn duyệt bài chưa.
- Nếu mọi thứ hoạt động trơn tru, hãy bật công tắc **Active** ở góc trên cùng bên phải để workflow tự động hóa toàn thời gian.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng đa kênh:** Ngoài Twitter, các sếp có thể nhân bản nhánh phía sau để đăng đồng thời lên LinkedIn, Facebook Page hoặc Instagram thông qua các node tương ứng.
- **Lưu log duyệt bài:** Thêm một node Google Sheets hoặc Airtable vào sau bước xác nhận để ghi lại lịch sử các sản phẩm đã được đăng bài, phục vụ việc thống kê content.
- **Phê duyệt theo nhóm:** Thay vì gửi cho 1 cá nhân, cấu hình Telegram Bot chat vào một nhóm Telegram nội bộ của team Marketing để mọi người cùng vote/duyệt bài.

### 📌 Kết luận
Tự động hóa sáng tạo nội dung chưa bao giờ dễ dàng đến thế! Với sự kết hợp hoàn hảo giữa Google Gemini AI, Google Drive, Telegram và Twitter, các sếp vừa tiết kiệm được nguồn lực, vừa đảm bảo chất lượng hình ảnh thương hiệu luôn chuyên nghiệp. Chúc các sếp cài đặt thành công và "lên đồ" mượt mà!