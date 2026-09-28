---
title: "🚀 Tự động hóa tạo video AI từ văn bản với HeyGen và Voice Cloning trong n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình tạo video AI sử dụng HeyGen API, tích hợp avatar tùy chỉnh và giọng đọc nhân bản vô cùng chuyên nghiệp."
slug: "tao-video-ai-tu-van-ban-voi-heygen-va-n8n"
tags: [n8n, automation, no-code, heygen, ai-video, content-marketing]
keywords: [n8n workflow, tạo video ai, heygen api, tự động hóa marketing, voice cloning n8n]
use_as_blog_post: true
---

# 🚀 Tự động hóa tạo video AI từ văn bản với HeyGen và Voice Cloning

Các sếp có bao giờ cảm thấy mệt mỏi khi phải quay video thủ công, chỉnh sửa từng khung hình, lồng tiếng cho hàng loạt chiến dịch Marketing hoặc video cá nhân hóa chưa? Quá trình này ngốn rất nhiều thời gian, chi phí thuê studio và nhân sự.

Đừng lo, bài toán đó sẽ được giải quyết triệt để với workflow n8n cực kỳ mạnh mẽ này. Bằng cách kết hợp n8n và **HeyGen**, hệ thống sẽ tự động biến văn bản thành các video AI sinh động với avatar và giọng đọc (voice cloning) giống hệt người thật hoàn toàn tự động 100% không cần code!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không còn cảnh ngồi dựng video thủ công, chỉ cần nhập text là có ngay video hoàn chỉnh.
- **Cá nhân hóa hàng loạt:** Dễ dàng tạo hàng trăm video với nội dung khác nhau cho từng khách hàng hoặc chiến dịch chỉ trong nháy mắt.
- **Tự động hóa hoàn toàn:** Workflow tự động gửi yêu cầu khởi tạo, theo dõi trạng thái render video (Polling) và trả về kết quả khi hoàn thành.
- **Hoạt động 24/7:** Chạy ngầm trên server, sẵn sàng sản xuất video bất cứ lúc nào các sếp cần.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt sẵn sàng (Self-hosted hoặc n8n Cloud).
- **HeyGen Account:** Tài khoản HeyGen (lưu ý cần mua API credits của HeyGen vì API yêu cầu gói trả phí).
- **Avatar ID & Voice ID:** ID của nhân vật AI và giọng đọc mà các sếp muốn sử dụng từ HeyGen.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ thư viện n8n, sau đó chọn **Import from File** hoặc copy toàn bộ mã nguồn JSON rồi dán trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần chú ý cấu hình kỹ các node sau:

- **Node `Config` (Set):** Nơi các sếp cấu hình các thông số đầu vào cho video bao gồm:
  - `Avatar ID`: Mã định danh nhân vật AI.
  - `Voice ID`: Mã định danh giọng nói.
  - `Text`: Nội dung kịch bản văn bản mà các sếp muốn avatar nói.
- **Node `Create Video` (HTTP Request) & `Get Video Status` (HTTP Request):** 
  - Cần tạo credentials loại **Custom Auth** trong n8n.
  - Tên Header Name điền: `X-Api-Key`
  - Giá trị Header Value: Dán **API Key** lấy từ phần cài đặt tài khoản HeyGen của các sếp.
  - Gắn credentials này vào cả 2 node HTTP Request (`Create Video` và `Get Video Status`).
- **Node `is Completed` (If):** Kiểm tra trạng thái render video từ HeyGen. Nếu video đã render xong (Completed), workflow sẽ đi tiếp tới node `Output`; nếu chưa, node `Wait` sẽ tạm dừng một chút trước khi gọi lại API kiểm tra tiếp.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Test workflow** ở node `When clicking ‘Test workflow’` để chạy thử nghiệm với kịch bản mẫu.
- Kiểm tra kết quả trả về ở node `Output`.
- Khi mọi thứ đã chạy trơn tru, hãy gạt công tắc sang chế độ **Active** để đưa workflow vào vận hành chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp Google Sheets / Airtable:** Thay vì nhập text thủ công trong node Config, các sếp có thể kết nối với Google Sheets để n8n tự động đọc danh sách kịch bản và sản xuất hàng loạt video.
- **Tích hợp Telegram / Slack Bot:** Thiết lập thêm node gửi thông báo về Telegram hoặc Slack ngay khi video render xong kèm link tải video, giúp các sếp quản lý tiến độ dễ dàng.
- **Lưu trữ tự động:** Tự động tải file video hoàn thiện và lưu trữ thẳng lên Google Drive hoặc OneDrive.

### 📌 Kết luận
Tự động hóa sản xuất video bằng AI chưa bao giờ dễ dàng đến thế với sự trợ giúp của n8n và HeyGen. Hãy áp dụng ngay workflow này vào quy trình Marketing của doanh nghiệp các sếp để tối ưu hóa hiệu suất và đón đầu xu hướng công nghệ!