---
title: "🚀 Tự động tạo hình ảnh AI chất lượng cao từ Text Prompt với Replicate và Lemaar Model trên n8n"
description: "Hướng dẫn chi tiết xây dựng workflow n8n tự động hóa quy trình gọi Replicate API để tạo hình ảnh AI từ văn bản (Text-to-Image) với mô hình Lemaar, tích hợp sẵn cơ chế kiểm tra trạng thái và xử lý lỗi."
slug: "tao-hinh-anh-ai-replicate-lemaar-n8n"
tags: [n8n, automation, ai-generation, replicate, text-to-image]
keywords: [n8n workflow, replicate api, ai image generation, lemaar model, tu dong hoa n8n]
---

# 🚀 Tự động tạo hình ảnh AI chất lượng cao với Replicate và Lemaar Model trên n8n

Các sếp có bao giờ cảm thấy mệt mỏi khi phải thao tác thủ công trên các nền tảng AI để tạo hình ảnh, sau đó lại phải chờ đợi, kiểm tra trạng thái render rồi tải về? Quy trình thủ công này vừa tốn thời gian, vừa đứt đoạn mạch sáng tạo khi làm nội dung số hoặc thiết kế sản phẩm.

Giải pháp ở đây là gì? Đó chính là tự động hóa toàn bộ quá trình này bằng một workflow n8n tích hợp Replicate API sử dụng mô hình **Lemaar (`creativeathive/lemaar-doorhandle-newset`)**. Các sếp chỉ cần nhập prompt, n8n sẽ lo phần còn lại từ gửi yêu cầu, theo dõi tiến trình cho đến khi trả về kết quả hoàn chỉnh!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Bỏ qua thao tác bấm máy thủ công, gọi API và nhận kết quả trực tiếp qua workflow.
- **Cơ chế thông minh (Polling Loop):** Tự động chờ và kiểm tra trạng thái xử lý của AI (với các node `Wait` và `If`) cho đến khi hình ảnh được render xong.
- **Kiểm soát lỗi tối ưu:** Xử lý mượt mà các trường hợp API lỗi hoặc thất bại nhờ nhánh `Has Failed?` và trả về kết quả chi tiết.
- **Sẵn sàng mở rộng:** Dễ dàng kết nối thêm Google Sheets, Telegram hoặc Slack để lưu trữ và gửi hình ảnh tự động.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một hệ thống n8n đang hoạt động (Cloud hoặc Self-hosted).
- Tài khoản [Replicate](https://replicate.com) và **API Token** cá nhân.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ nguồn cấp và import trực tiếp vào giao diện n8n Editor (chọn **Add workflow** -> **Import from File**).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 13 nodes, trong đó các sếp cần chú ý cấu hình kỹ các điểm sau:

- **Node `Set API Token`**: 
  - Tại đây chứa biến định danh xác thực. Các sếp cần thay thế giá trị mẫu `'YOUR_REPLICATE_API_TOKEN'` bằng **API Token thực tế** lấy từ tài khoản Replicate của mình.
- **Node `Set Other Parameters`**: 
  - Nơi thiết lập các thông số đầu vào cho mô hình Lemaar. Các sếp có thể thay đổi `prompt` theo ý tưởng sáng tạo của mình, đồng thời tùy chỉnh các thông số tùy chọn như `width`, `height`, `seed` hoặc `go_fast`.
- **Node `Create Other Prediction` & `Check Status` (HTTP Request)**: 
  - Đảm bảo endpoint API của Replicate (`https://api.replicate.com/v1/predictions`) được cấu hình chính xác kèm Header Authorization chứa token.
- **Các node `Wait 5s`, `Wait 10s`, `Is Complete?`, `Has Failed?`**: 
  - Đóng vai trò là vòng lặp kiểm tra (polling). Không cần chỉnh sửa logic ở đây trừ khi các sếp muốn rút ngắn hoặc kéo dài thời gian chờ giữa các lần check trạng thái.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** từ `Manual Trigger` để test thử với prompt mặc định.
- Theo dõi log chạy trên giao diện n8n để đảm bảo hình ảnh được render thành công.
- Sau khi test ngon lành, hãy bật nút **Active** ở góc trên bên phải để sẵn sàng đưa vào vận hành thực tế.

---

### ✍️ Mẹo & gợi ý nâng cao
Để workflow trở thành một "trợ lý ảo" đắc lực thực thụ, các sếp có thể mở rộng thêm:
1. **Tích hợp Google Sheets / Airtable**: Tự động lưu lại lịch sử các prompt đã chạy và link hình ảnh kết quả tương ứng.
2. **Gửi thông báo qua Telegram/Slack**: Nhận ngay hình ảnh vừa tạo trực tiếp trên điện thoại hoặc nhóm chat làm việc ngay khi AI render xong.
3. **Webhook Trigger**: Thay vì dùng `Manual Trigger`, hãy kết nối webhook để nhận prompt từ một Form đăng ký hoặc chatbot bán hàng.

### 📌 Kết luận
Việc tích hợp Replicate AI thông qua n8n mở ra khả năng tự động hóa không giới hạn cho việc sáng tạo nội dung hình ảnh. Hãy bắt tay vào setup ngay hôm nay để tiết kiệm hàng giờ thao tác thủ công cho đội ngũ của các sếp!