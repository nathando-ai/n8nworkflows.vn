---
title: "🚀 Tự động hóa biến ảnh chụp món ăn thành gợi ý nhà hàng và sách hay với AI Vision & Google APIs"
description: "Hướng dẫn chi tiết workflow n8n kết hợp GPT Vision, Google Places, Google Books và Slack để tự động phân tích ảnh món ăn, tìm nhà hàng phù hợp và đề xuất sách đọc thú vị."
slug: "tu-dong-hoa-phan-tich-anh-mon-an-nha-hang-sach-n8n"
tags: [n8n, automation, no-code, ai-vision, google-apis, slack]
keywords: [n8n workflow, gpt vision, google places, google books, tu dong hoa anh mon an, ai recommender]
---

# 🚀 Tự động hóa biến ảnh chụp món ăn thành gợi ý nhà hàng và sách hay với AI Vision & Google APIs

Các sếp có bao giờ chụp ảnh một món ăn ngon nghẻ nhưng lại phân vân không biết quanh đây còn quán nào ngon tương tự, hay vừa ăn vừa muốn tìm một cuốn sách hay để nghiền ngẫm chưa? Việc làm này thủ công vừa tốn thời gian tìm kiếm, vừa khó kết nối cảm xúc. 

Workflow n8n này chính là giải pháp tự động hóa 100% không cần code giúp các sếp giải quyết triệt để bài toán trên: chỉ cần thả ảnh món ăn vào Google Drive, AI sẽ lo phần còn lại từ phân tích món ăn, tìm nhà hàng lân cận, gợi ý sách phù hợp cho đến gửi báo cáo gọn gàng lên Slack!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Chỉ cần bỏ ảnh vào Google Drive, quy trình tự kích hoạt mà không cần thao tác thủ công.
- **AI Đa phương thức (Multimodal AI):** Nhận diện chính xác tên món ăn, danh mục và ước tính macro từ hình ảnh qua GPT Vision (OpenRouter).
- **Gợi ý thông minh:** Tự động tìm kiếm nhà hàng xuất sắc nhất quanh khu vực dựa trên đánh giá và review thực tế từ Google Places.
- **Trải nghiệm trọn vẹn:** Đề xuất tựa sách liên quan thông qua Google Books và tổng hợp tất cả vào một thông báo Slack cực kỳ chuyên nghiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động trơn tru, các sếp cần chuẩn bị sẵn các tài khoản và credentials sau:
- Tài khoản **Google Drive** (để kích hoạt trigger khi có ảnh mới).
- API Key hoặc OAuth2 cho **Google Places API** và **Google Books API**.
- Tài khoản **OpenRouter / OpenAI** (để sử dụng các LLM nodes).
- Workspace **Slack** và quyền tích hợp **Slack OAuth2**.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể copy mã JSON của workflow từ nguồn cung cấp và paste trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp hãy cấu hình kỹ các node trọng điểm sau:
- **Google Drive Trigger**: Kết nối tài khoản Google Drive và trỏ đến thư mục chứa ảnh món ăn đầu vào.
- **Set Origin & Làms (Set Origin & Radius)**: Thiết lập tọa độ trung tâm (`originLat`, `originLng`), nhãn địa điểm (`originLabel`) và bán kính tìm kiếm (`radiusM`) phù hợp với khu vực của các sếp.
- **Search Google Places & Search Google Books**: Đảm bảo cấu hình API Key chính xác (khuyên dùng lưu trong phần Credentials của n8n thay vì hardcode trong header).
- **LLM nodes (Vision / Selection / Books)**: Chọn đúng credential OpenRouter/OpenAI và model (ví dụ: `openai/gpt-5` hoặc các model vision tương thích).
- **Post to Slack**: Chọn channel Slack đích nhận thông báo và kiểm tra cấu trúc thông điệp.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) với một vài bức ảnh món ăn mẫu để kiểm tra dữ liệu trả về ở từng bước.
- Bật công tắc **Active** để workflow tự động hoạt động 24/7.

---

### 🔍 Chi tiết từng khối xử lý trong Workflow

#### 1. Photo → Category
- **Google Drive Trigger**: Lắng nghe và phát hiện ảnh mới tải lên.
- **Fetch Image (Drive)**: Tải file ảnh về dưới dạng nhị phân.
- **Dish Classifier**: Sử dụng Vision LLM phân tích hình ảnh, trả về chuỗi JSON nghiêm ngặt gồm tên món ăn, danh mục.
- **Normalize Classification**: Node Code giúp phân tích cú pháp JSON an toàn, ánh xạ danh mục món ăn sang từ khóa thân thiện với Google Places.

#### 2. Find & Select Restaurant
- **Set Origin & Radius**: Nơi lưu trữ tọa độ và bán kính tìm kiếm trung tâm.
- **Search Google Places**: Gửi HTTP POST request tới Places API để tìm các địa điểm lân cận.
- **Summarize Place List**: Gom nhóm và làm phẳng danh sách nhà hàng tìm được.
- **Select Best Place (AI)**: Sử dụng AI để chọn ra nhà hàng xuất sắc nhất dựa trên điểm số đánh giá và review thực tế.
- **Format Best Place JSON**: Chuẩn hóa đầu ra thành định dạng JSON chứa tên nhà hàng và lý do lựa chọn.

#### 3. Book Recommendation
- **Recommend Book (AI)**: Đề xuất tựa sách, tác giả và lý do liên quan đến chủ đề ẩm thực/món ăn.
- **Normalize Book JSON**: Làm sạch định dạng JSON, đảm bảo không bị lỗi cú pháp.
- **Search Google Books**: Tìm kiếm chính xác tựa sách trên Google Books.
- **Format Book Details**: Tổng hợp thông tin chi tiết (tiêu đề, tác giả, nhà xuất bản, ngày phát hành...).

#### 4. Output
- **Post to Slack**: Tổng hợp toàn bộ thông tin về món ăn, nhà hàng được chọn và sách hay thành một tin nhắn Slack gọn gàng, đẹp mắt.

---

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo**: Thay vì chỉ gửi Slack, các sếp có thể kết hợp thêm node Telegram hoặc gửi Email tự động cho bản thân hoặc nhóm bạn thân.
- **Lưu lịch sử vào Google Sheets**: Thêm một node Google Sheets vào cuối workflow để lưu lại nhật ký các món ăn đã phân tích, nhà hàng đã ghé và sách đã đọc để tạo thành một "Food & Read Diary" cá nhân.
- **Tùy biến ngôn ngữ**: Dễ dàng tinh chỉnh prompt trong các AI Agent để nhận kết quả bằng tiếng Việt hoàn toàn thay vì tiếng Anh hoặc tiếng Nhật.

### 📌 Kết luận
Workflow này là một minh họa tuyệt vời cho sức mạnh kết hợp giữa Multimodal AI (GPT Vision) và các dịch vụ Google APIs trên nền tảng n8n. Hãy thiết lập ngay hôm nay để biến những bức ảnh chụp món ăn đơn thuần thành những trải nghiệm khám phá ẩm thực và tri thức thú vị nhé các sếp!