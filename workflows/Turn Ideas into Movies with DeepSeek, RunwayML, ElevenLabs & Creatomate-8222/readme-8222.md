---
title: "🎬 Tự động hóa sáng tạo phim với DeepSeek, RunwayML, ElevenLabs & Creatomate"
description: "Hướng dẫn chi tiết cách tự động hóa quy trình sáng tạo phim từ ý tưởng đến sản phẩm hoàn chỉnh với n8n, DeepSeek, RunwayML và ElevenLabs"
slug: "tu-dong-hoa-san-xuat-phim-voi-n8n"
tags: [n8n, automation, content-creation, ai, multimedia]
keywords: [n8n workflow, tự động hóa phim, AI sáng tạo, RunwayML, ElevenLabs]
---

# 🎬 Tự động hóa sáng tạo phim với DeepSeek, RunwayML, ElevenLabs & Creatomate

[Các sếp] có bao giờ mơ ước được biến những ý tưởng sáng tạo thành phim hoàn chỉnh mà không cần phải làm thủ công từng bước một? Với workflow này, chúng ta sẽ tự động hóa toàn bộ quy trình từ ý tưởng ban đầu đến sản phẩm phim hoàn chỉnh, từ viết kịch bản đến tạo hình, âm thanh và biên tập - tất cả đều được thực hiện bởi trí tuệ nhân tạo và được điều phối bởi n8n.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa quy trình sáng tạo phim từ 3-5 ngày xuống còn vài giờ.
- **Chất lượng nhất quán**: Các công cụ AI tạo ra nội dung chuyên nghiệp với độ chính xác cao.
- **Tính cá nhân hóa**: Có thể điều chỉnh từng phần của quy trình để phù hợp với phong cách riêng.
- **Hoạt động liên tục**: Workflow có thể chạy 24/7 mà không cần can thiệp thủ công.
- **Tích hợp đa nền tảng**: Kết nối dễ dàng với các công cụ sáng tạo khác như Notion, Slack và Dropbox.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản DeepSeek API (để tạo kịch bản và nội dung văn bản)
- Tài khoản RunwayML (để tạo hình ảnh và video)
- Tài khoản ElevenLabs (để tạo giọng nói)
- Tài khoản Notion (để lưu trữ dữ liệu dự án)
- Tài khoản Slack (để kích hoạt workflow)
- Tài khoản Dropbox (để lưu trữ các tệp âm thanh và video)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấn vào nút "Import from URL" và dán link sau: [https://n8n.io/workflows/8222](https://n8n.io/workflows/8222)
3. Hoặc tải file JSON về và import từ máy tính của bạn

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Narrative Director** (lmChatDeepSeek):
   - Cấu hình credentials cho DeepSeek API
   - Đặt prompt để tạo kịch bản phim từ ý tưởng ban đầu

2. **Visual Art Director** (lmChatDeepSeek):
   - Cấu hình credentials cho DeepSeek API
   - Đặt prompt để chuyển đổi kịch bản thành prompt hình ảnh

3. **Concept Art Studio** (httpRequest):
   - Cấu hình credentials cho RunwayML API
   - Đặt endpoint và tham số cho việc tạo hình ảnh

4. **Voice Synthesis Studio** (httpRequest):
   - Cấu hình credentials cho ElevenLabs API
   - Đặt giọng nói và các tham số âm thanh

5. **Creative Archive** (notion):
   - Cấu hình credentials cho Notion API
   - Tạo database để lưu trữ thông tin dự án

6. **Creative Brief Intake** (webhook):
   - Cấu hình webhook để nhận ý tưởng ban đầu
   - Đặt path và phương thức HTTP (POST)

7. **Release Announcement** (slack):
   - Cấu hình credentials cho Slack API
   - Đặt kênh và thông báo khi phim hoàn thành

8. **Dropbox Uploader** (dropbox):
   - Cấu hình credentials cho Dropbox API
   - Đặt đường dẫn lưu trữ cho các tệp âm thanh và video

#### 3. Kích hoạt ⚡️
1. Kiểm tra kết nối với tất cả các API và dịch vụ bên ngoài
2. Chạy test với dữ liệu mẫu để đảm bảo workflow hoạt động đúng
3. Bật chế độ Active cho workflow

### ✍️ Mẹo & gợi ý nâng cao
1. **Tích hợp với các công cụ khác**: Kết nối workflow với các công cụ quản lý dự án như Asana hoặc Trello để theo dõi tiến độ.
2. **Tùy chỉnh phong cách**: Điều chỉnh các prompt trong các node LLM để phù hợp với phong cách sáng tạo riêng của bạn.
3. **Tự động hóa phân phối**: Kết nối với các nền tảng phân phối phim như Vimeo hoặc YouTube để tự động tải lên phim hoàn thành.
4. **Tích hợp với các công cụ chỉnh sửa video**: Kết nối với các công cụ chỉnh sửa video như Adobe Premiere Pro hoặc Final Cut Pro để tự động hóa quy trình biên tập.

### 📌 Kết luận
Workflow này mang đến giải pháp toàn diện cho việc tự động hóa quy trình sáng tạo phim, từ ý tưởng đến sản phẩm hoàn chỉnh. Bằng cách kết hợp sức mạnh của trí tuệ nhân tạo với khả năng điều phối của n8n, các sếp có thể tiết kiệm thời gian và tạo ra những tác phẩm phim chất lượng cao một cách hiệu quả. Hãy thử nghiệm và tùy chỉnh workflow này để phù hợp với nhu cầu sáng tạo của bạn ngay hôm nay!