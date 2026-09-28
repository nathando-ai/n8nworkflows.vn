---
title: "🚀 Tạo ảnh AI giữ nguyên nhân vật đồng nhất với KIE.AI Nano Banana API trên n8n"
description: "Hướng dẫn chi tiết cách tự động hóa quy trình tạo ảnh AI chất lượng cao, giữ đồng nhất nhân vật bằng KIE.AI Nano Banana API tích hợp trực tiếp qua n8n Form."
slug: "tao-anh-ai-giu-nguyen-nhan-vat-kie-ai-nano-banana-n8n"
tags: [n8n, automation, no-code, AI Image Generation, KIE.AI, Nano Banana]
keywords: [n8n workflow, tạo ảnh AI, character-consistent images, KIE.AI Nano Banana API, text-to-image, image-to-image]
---

# 🚀 Tự động hóa tạo ảnh AI đồng nhất nhân vật với KIE.AI Nano Banana API

Các sếp đang gặp khó khăn khi tạo hàng loạt ảnh AI nhưng nhân vật cứ bị "biến đổi" qua mỗi lần generate? Việc làm thủ công trên các web app vừa tốn kém, vừa mất thời gian nhập lại thông số liên tục? 

Giải pháp hoàn hảo đây rồi! Bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực xịn xò, tích hợp **KIE.AI Nano Banana API** thông qua một giao diện Form trực quan. Giúp các sếp tạo ra các bức ảnh chất lượng cao, giữ vững độ đồng nhất của nhân vật (character-consistent) với chi phí cực rẻ (rẻ hơn 50% so với các nền tảng thông thường).

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Linh hoạt đa chế độ:** Hỗ trợ cả 2 chế độ Text-to-Image (văn bản thành ảnh) và Image-to-Image (ảnh thành ảnh).
- **Đồng nhất nhân vật:** Duy trì nét mặt, đặc điểm nhân vật xuyên suốt qua các lần tạo ảnh khác nhau.
- **Tự động hóa toàn diện:** Cơ chế vòng lặp kiểm tra trạng thái (polling) tự động sau mỗi 5 giây, trả kết quả trực tiếp không cần thao tác tay phức tạp.
- **Tối ưu chi phí:** Giá thành siêu rẻ, tiết kiệm đến 50% so với các nền tảng tạo ảnh AI mainstream.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một **n8n instance** đang hoạt động (có tính năng Form Trigger).
- Tài khoản và **API Key** từ [KIE.AI Nano Banana](https://kie.ai/nano-banana).
- Ý tưởng prompt hoặc link ảnh gốc (nếu dùng chế độ Image-to-Image).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này về máy, sau đó vào giao diện n8n của các sếp, chọn **Add workflow** -> **Import from File** (hoặc copy toàn bộ JSON và dán trực tiếp vào Editor).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 6 nodes chính hoạt động nhịp nhàng với nhau. Các sếp cần chú ý các điểm sau:

- **Submit Text Prompt for image Generation (`formTrigger`):** 
  - Đây là điểm khởi đầu, tạo ra giao diện Web Form cho người dùng nhập liệu. Các sếp cấu hình các trường dữ liệu thu thập gồm:
    - `model`: Chọn `google/nano-banana` (Text-to-Image) hoặc `google/nano-banana-edit` (Image-to-Image).
    - `prompt`: Mô tả chi tiết bức ảnh muốn tạo.
    - `img_url`: Đường dẫn ảnh gốc (chỉ bắt buộc nếu dùng model `-edit`, có thể bỏ trống nếu tạo từ văn bản).
    - `api_key`: Nhập khóa API lấy từ tài khoản KIE.AI của các sếp.

- **Send image Generation Request to KIE.AI API (`httpRequest`):**
  - Node này nhận thông tin từ Form và gửi yêu cầu tạo ảnh đến hệ thống của KIE.AI sử dụng API Key người dùng cung cấp.

- **Wait for image Processing Completion (`wait`) & Obtain the generated status (`httpRequest`) & Check if image Generation is Complete (`if`):**
  - Bộ ba này đóng vai trò "kiểm tra tiến độ". Node `Wait` sẽ tạm dừng 5 giây, sau đó gọi API kiểm tra xem ảnh đã render xong chưa. Node `If` sẽ check điều kiện: nếu xong rồi thì chuyển sang bước xuất kết quả, chưa xong thì vòng lại chờ tiếp.

- **Format and Display image Results (`set`):**
  - Định dạng lại dữ liệu trả về và hiển thị kết quả trực tiếp lên giao diện màn hình cho các sếp.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** để chạy thử lần đầu.
- Truy cập vào URL Form do n8n cung cấp, điền thông tin test thử nghiệm.
- Sau khi kiểm tra mọi thứ mượt mà, gạt công tắc sang **Active** để đưa workflow vào vận hành chính thức 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tối ưu Prompt:** Hãy kết hợp phong cách (realistic, anime, cyberpunk), góc máy (close-up, wide shot), ánh sáng (dramatic, soft) để có bức ảnh nghệ thuật nhất.
- **Mở rộng thông báo:** Có thể nối thêm node Telegram hoặc Slack vào cuối luồng (`Format and Display image Results`) để hệ thống bắn thông báo và gửi ảnh trực tiếp về chat nhóm ngay khi render xong.
- **Lưu trữ tự động:** Gắn thêm node Google Sheets để lưu lại lịch sử prompt và URL hình ảnh đã tạo phục vụ cho việc quản lý nội dung sau này.

### 📌 Kết luận
Với workflow n8n tích hợp KIE.AI Nano Banana API này, việc tạo ra một hệ thống sản xuất hình ảnh AI cá nhân hóa chưa bao giờ dễ dàng đến thế. Hãy triển khai ngay hôm nay để tối ưu hóa năng suất làm việc của các sếp nhé!