---
title: "🚀 Tạo ảnh phong cách Polaroid cổ điển cực chất bằng Gemini AI và n8n"
description: "Tự động hóa quy trình biến ảnh kỹ thuật số thành những bức ảnh phong cách Polaroid vintage độc đáo sử dụng Gemini AI qua Defapi API."
slug: "tao-anh-polaroid-co-dien-bang-gemini-ai-n8n"
tags: [n8n, automation, no-code, gemini-ai, image-generation]
keywords: [n8n workflow, tao anh polaroid, gemini ai, defapi, tu dong hoa xu ly anh]
---

# 🚀 Tạo ảnh phong cách Polaroid cổ điển cực chất bằng Gemini AI

Các sếp có muốn biến những bức ảnh kỹ thuật số thông thường thành những thước ảnh phong cách Polaroid hoài niệm (vintage) mà không cần dùng đến Photoshop phức tạp? Việc chỉnh sửa thủ công từng tấm ảnh, thêm hiệu ứng hạt phim (film grain), cân chỉnh màu sắc và thay phông nền tốn rất nhiều thời gian. 

Với workflow n8n này, các sếp sẽ sở hữu ngay một hệ thống tự động hóa 100%: Người dùng chỉ cần tải ảnh lên form giao diện, nhập câu lệnh (prompt) và hệ thống sẽ tự động gọi **Gemini AI** qua Defapi API để cho ra đời những bức ảnh Polaroid cổ điển cực kỳ nghệ thuật!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Gom tất cả thao tác từ upload ảnh, chuyển đổi dữ liệu, gửi API đến kiểm tra trạng thái vào một quy trình duy nhất.
- **Giao diện Form thân thiện:** Cho phép khách hàng hoặc team tự động upload 2 ảnh đầu vào, nhập prompt và API key trực tiếp qua web form.
- **Hiệu ứng độc bản:** Ứng dụng sức mạnh của Gemini AI để tạo ra các bức ảnh Polaroid với màu sắc vintage, hạt phim chân thực và giữ nguyên khuôn mặt gốc.
- **Tiết kiệm thời gian:** Không cần mở các phần mềm đồ họa nặng nhọc, nhận kết quả chỉ trong vòng vài giây đến vài phút.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Một hệ thống n8n đang hoạt động (Cloud hoặc Self-hosted).
- **Defapi Account:** Tài khoản và API Key tại [Defapi.org](https://defapi.org/model/google/gemini-2.5-flash-image).
- **Ảnh đầu vào:** Chuẩn bị sẵn 2 bức ảnh kỹ thuật số (ảnh chụp đủ sáng, rõ mặt sẽ cho kết quả tốt nhất).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Copy mã JSON của workflow hoặc tải file JSON về máy.
- Mở giao diện n8n Editor, chọn **Add workflow** -> **Import from File** (hoặc dán trực tiếp vào màn hình làm việc).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 7 nodes chính phối hợp nhịp nhàng với nhau. Các sếp cần chú ý cấu hình kỹ các node sau:
- **Upload 2 Images (Form Trigger):** Cấu hình form thu thập dữ liệu đầu người dùng gồm: 2 trường tải file ảnh (Image 01 & Image 02), trường nhập API Key và trường nhập Prompt sáng tạo.
- **Convert to JSON (Code Node):** Node này có nhiệm vụ chuyển đổi dữ liệu nhị phân (binary) của 2 bức ảnh sang định dạng base64-style data URL để API có thể đọc được.
- **Send Image Generation Request to Defapi.org API (HTTP Request):** Gửi yêu cầu tạo ảnh tới endpoint `https://api.defapi.org/api/image/gen` sử dụng phương thức POST với mô hình `google/gemini` và xác thực bằng Bearer Token từ API Key của người dùng.
- **Wait for Image Processing Completion (Wait Node):** Thiết lập thời gian chờ (khoảng 10 giây) để AI tiến hành xử lý hình ảnh trước khi gọi kiểm tra trạng thái.
- **Obtain the generated status & Check if Image Generation is Complete:** Kiểm tra trạng thái xử lý qua API `https://api.defapi.org/api/task/query` (GET request) và dùng node IF để lọc xem trạng thái đã trả về `success` hay chưa.
- **Format and Display Image Results (Set Node):** Tổng hợp và hiển thị URL hình ảnh hoàn thiện để người dùng tải về hoặc chia sẻ.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để test thử với dữ liệu mẫu.
- Truy cập vào đường dẫn Form do n8n cung cấp, tải ảnh lên, nhập prompt và chạy thử nghiệm.
- Sau khi kiểm tra mọi thứ hoạt động trơn tru, hãy bật **Active workflow** để đưa hệ thống vào vận hành chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Tối ưu Prompt:** Hãy miêu tả chi tiết về độ bão hòa màu, hiệu ứng hạt phim (film grain), góc tối viền ảnh (vignetting), điều kiện ánh sáng phòng tối hoặc hiệu ứng flash để AI tạo ra bức ảnh có chiều sâu nhất.
- **Gửi thông báo qua Telegram/Slack:** Thay vì chỉ hiển thị trên form, các sếp có thể nối thêm node Telegram hoặc Slack để gửi thẳng bức ảnh Polaroid vừa tạo về máy cá nhân hoặc nhóm làm việc ngay khi hoàn tất.
- **Lưu trữ tự động:** Tích hợp thêm Google Drive hoặc Airtable để lưu trữ lại tất cả các bức ảnh gốc và ảnh thành phẩm phục vụ cho việc quản lý tài nguyên.

### 📌 Kết luận
Workflow tạo ảnh phong cách Polaroid bằng Gemini AI trên n8n không chỉ mang lại trải nghiệm thú vị mà còn mở ra cơ ứng dụng tuyệt vời cho các nhà sáng tạo nội dung, Studio ảnh hoặc các chiến dịch Marketing tương tác. Hãy triển khai ngay hôm nay để tự động hóa quy trình sáng tạo nghệ thuật của các sếp!