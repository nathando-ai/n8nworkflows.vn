---
title: "🚀 Tự động hóa sáng tạo và đăng bài LinkedIn với Google Gemini & Gen-Imager trong n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động tạo nội dung bài viết chuyên nghiệp kèm hình ảnh bằng AI và đăng thẳng lên LinkedIn chỉ từ một biểu mẫu."
slug: "tu-dong-hoa-dang-bai-linkedin-google-gemini-n8n"
tags: [n8n, automation, ai, marketing, linkedin, google-gemini]
keywords: [n8n workflow, tự động hóa linkedin, google gemini, gen-imager, ai marketing, tao bai viet linkedin tu dong]
---

# 🚀 Tự động hóa sáng tạo và đăng bài LinkedIn với Google Gemini & Gen-Imager

Các sếp có bao giờ cảm thấy mệt mỏi vì phải tốn hàng giờ nghĩ ý tưởng, viết nội dung, thiết kế hình ảnh và thủ công đăng bài lên LinkedIn mỗi ngày? Việc duy trì sự hiện diện chuyên nghiệp trên mạng xã hội này đòi hỏi nguồn lực không nhỏ, nhưng nếu làm thủ công thì rất dễ bị gián đoạn.

Giải pháp ở đây là gì? Workflow n8n này sẽ giúp các sếp tự động hóa 100% quy trình: Nhận chủ đề từ một biểu mẫu đơn giản $\rightarrow$ Dùng **Google Gemini AI** viết bài và tạo prompt hình ảnh $\rightarrow$ Gọi API tạo ảnh chuyên nghiệp $\rightarrow$ Tự động đăng tải lên LinkedIn mà không cần chạm tay vào bất kỳ bước trung gian nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Biến một từ khóa/chủ đề đơn giản thành bài đăng hoàn chỉnh kèm hình ảnh chỉ trong vài giây.
- **Nội dung chuẩn chỉnh, chuyên nghiệp:** Tận dụng sức mạnh của Google Gemini để tạo ra các bài viết thu hút, đúng trọng tâm và đúng insight người đọc.
- **Hình ảnh minh họa độc quyền:** Tự động tạo ảnh minh họa thông qua Gen-Imager API dựa trên chính nội dung bài viết.
- **Hoạt động liền mạch 24/7:** Lên lịch hoặc kích hoạt tức thì qua form, duy trì kênh LinkedIn luôn sôi động và chuyên nghiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **n8n Instance:** Đã cài đặt sẵn sàng (Self-hosted hoặc n8n Cloud).
- **Google Gemini API Key:** Dành cho node AI Agent và Google Gemini Chat Model.
- **Gen-Imager API Key:** Đăng ký trên [RapidAPI - Gen-Imager](https://rapidapi.com/PrineshPatel/api/gen-imager) để lấy khóa gọi API tạo ảnh.
- **LinkedIn Account:** Tài khoản LinkedIn cá nhân hoặc trang doanh nghiệp để cấu hình quyền OAuth2 đăng bài tự động.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này và dán trực tiếp vào n8n Editor của mình (hoặc import file JSON thông qua tùy chọn `Import from File`).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 8 nodes chính, các sếp cần chú ý cấu hình kỹ các điểm sau để chạy mượt mà:
- **On form submission (Form Trigger):** Node này tạo sẵn một giao diện form đơn giản. Các sếp có thể mở node này để xem link form hoặc tùy chỉnh thêm các trường (field) nhập liệu nếu muốn người dùng cung cấp nhiều thông tin hơn ngoài chủ đề bài viết.
- **Mapper (Set Node):** Nhận dữ liệu từ form và gán vào biến chuẩn `chatInput` để chuyển tiếp vào AI Agent. Đảm bảo biến được map chính xác từ output của form.
- **Google Gemini Chat Model & AI Agent:** 
  - Thêm Credentials của Google Gemini (`googlePalmApi`).
  - Cấu hình Prompt trong AI Agent để hướng dẫn Gemini cách viết bài (văn phong, độ dài, cách dùng hashtag, và yêu cầu trả về kèm theo prompt tạo ảnh).
- **Normalizer & Decoder (Code Nodes):** Các node viết bằng JavaScript này có nhiệm vụ bóc tách kết quả dạng text và prompt ảnh từ AI, sau đó xử lý định dạng. Không cần sửa code ở đây trừ khi các sếp muốn thay đổi cách định dạng dữ liệu.
- **Text to Image (HTTP Request Node):** 
  - Cấu hình Endpoint của **Gen-Imager API** lấy từ RapidAPI.
  - Điền API Key vào phần Header xác thực của request.
  - Truyền prompt hình ảnh được bóc tách từ bước AI vào body request.
- **LinkedIn Node:** 
  - Kết nối tài khoản LinkedIn thông qua OAuth2.
  - Chọn đúng quyền đăng bài lên profile cá nhân hoặc Company Page của các sếp.
  - Map nội dung text bài viết và file binary hình ảnh từ node `Decoder` vào các trường tương ứng trong node LinkedIn.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và test thử gửi một chủ đề bất kỳ qua form để kiểm tra toàn bộ luồng chạy (từ tạo văn bản, tạo ảnh đến kết quả trên LinkedIn).
- Nếu mọi thứ trơn tru, hãy bật công tắc **Active** ở góc trên cùng bên phải để đưa workflow vào trạng thái chạy tự động hoàn toàn.

### ✍️ Mẹo & gợi ý nâng cao
Để hệ thống thông minh và phục vụ công việc tốt hơn, các sếp có thể mở rộng workflow với các ý tưởng sau:
1. **Thêm bước kiểm duyệt (Human-in-the-loop):** Thay vì đăng thẳng lên LinkedIn, hãy chuyển bài viết và ảnh vào một kênh **Telegram** hoặc **Slack** kèm 2 nút bấm "Duyệt" hoặc "Sửa lại". Chỉ khi bấm duyệt thì bài mới được đẩy lên LinkedIn.
2. **Lưu lịch sử vào Google Sheets:** Thêm một node Google Sheets để ghi lại Chủ đề, Nội dung bài viết, Link hình ảnh và thời gian đăng để dễ dàng theo dõi hiệu suất nội dung (Content Calendar).
3. **Tự động hóa theo lịch:** Thay thế `Form Trigger` bằng `Schedule Trigger` để n8n tự động chọn chủ đề từ danh sách có sẵn trong Google Sheets và đăng bài đều đặn mỗi 9h sáng hàng ngày.

### 📌 Kết luận
Với workflow n8n kết hợp giữa Google Gemini và Gen-Imager này, việc xây dựng thương hiệu cá nhân hay quảnLý kênh marketing trên LinkedIn chưa bao giờ dễ dàng đến thế. Hãy cài đặt ngay hôm nay để tiết kiệm thời gian và nâng tầm chuyên nghiệp cho kênh truyền thông của các sếp!