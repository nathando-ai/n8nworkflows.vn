---
title: "🚀 Tạo hàng loạt ảnh đại diện (Avatar) miễn phí không cần API Key với n8n"
description: "Hướng dẫn tự động tạo 12 phong cách ảnh đại diện độc đáo từ các API công cộng miễn phí bằng n8n, hiển thị dưới dạng thư viện trực quan."
slug: "tao-avatar-mien-phi-khong-can-api-key-voi-n8n"
tags: [n8n, automation, no-code, content-creation, ai-avatars, free-apis]
keywords: [n8n workflow, tạo avatar miễn phí, profile picture generator, tự động hóa n8n, free public APIs]
---

# 🚀 Tự động tạo hàng loạt Avatar cực chất không cần API Key với n8n

Các sếp có bao giờ cần tạo hàng loạt ảnh đại diện (avatar) cho hệ thống user thử nghiệm, bài viết blog, hoặc thiết kế giao diện nhưng lại ngại việc phải đăng ký tài khoản và mua các gói API đắt đỏ? Việc tìm kiếm và tải thủ công từng cái vừa tốn thời gian, vừa mất công quản lý.

Được thiết kế bởi chuyên gia Wan Dinie, workflow n8n này chính là giải pháp tự động hóa 100% không cần code giúp các sếp tạo ra **12 phong cách avatar khác nhau** từ các API công cộng hoàn toàn miễn phí chỉ bằng một cú click!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Hoàn toàn miễn phí:** Không tốn một xu tiền API keys hay đăng ký dịch vụ trả phí nào.
- **Đa dạng phong cách:** Tự động tổng hợp 12 kiểu avatar khác nhau (hoạt hình, 3D, tối giản, pixel art...) từ một seed duy nhất.
- **Giao diện trực quan:** Hiển thị kết quả dưới dạng lưới (grid) responsive cực đẹp kèm theo nút tải xuống (download) trực tiếp cho từng ảnh.
- **Tùy biến linh hoạt:** Dễ dàng thay đổi từ khóa (seed), giới tính hoặc thêm bớt các nguồn API theo sở thích.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n đang hoạt động (Cloud hoặc Self-hosted).
- **Không cần** bất kỳ tài khoản dịch vụ bên thứ ba hay API Key nào cả!
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Các sếp tải file JSON của workflow hoặc copy trực tiếp mã nguồn JSON từ trang n8n gốc.
- Mở n8n Editor, chọn **Add workflow** -> **Import from File** hoặc dán trực tiếp vào giao diện.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này được thiết kế theo dạng "Plug and Play" (Cắm và chạy), tuy nhiên các sếp có thể tinh chỉnh tại các node sau:
- **Node `Call the Profile APIs` (Code Node):** 
  - Muốn dùng từ khóa cố định thay vì ngẫu nhiên? Sửa dòng `const userInput = '';` thành `const userInput = 'ten_cua_cac_sep';`.
  - Muốn cố định giới tính? Sửa dòng xử lý `gender` thành `'male'` hoặc `'female'`.
  - Thêm bớt các nguồn API avatar bằng cách chỉnh sửa mảng `apis` trực tiếp trong đoạn code JavaScript cực kỳ dễ hiểu.
- **Node `Show the Profile Pictures` (HTML Node):** Hiển thị kết quả giao diện dạng trang web thu nhỏ với nút download sẵn sàng.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** để chạy thử nghiệm thủ công với Trigger `When clicking ‘Execute workflow’`.
- Kiểm tra kết quả hiển thị ở node HTML để xem thư viện avatar vừa được tạo.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Webhook:** Kết nối workflow này với một Webhook để các sếp có thể gọi API nội bộ tạo avatar bất cứ lúc nào qua ứng dụng web của mình.
- **Lưu trữ tự động:** Mở rộng workflow bằng cách thêm node tải ảnh và lưu tự động vào Google Drive hoặc Supabase.
- **Gửi qua Telegram/Slack:** Tự động gửi bộ ảnh avatar vừa tạo thẳng vào nhóm chat Telegram của đội ngũ thiết kế hoặc dev.

### 📌 Kết luận
Một workflow siêu nhẹ, không tốn phí nhưng mang lại giá trị thực tiễn cao cho việc tạo nội dung và lập trình. Hãy import ngay vào hệ thống n8n của các sếp để trải nghiệm sự kỳ diệu của tự động hóa!