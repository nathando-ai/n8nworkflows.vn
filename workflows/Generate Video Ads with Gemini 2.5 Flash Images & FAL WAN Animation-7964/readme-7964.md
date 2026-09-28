---
title: "🚀 Tự động hóa sản xuất Video Quảng cáo đỉnh cao với Gemini 2.5 Flash & FAL WAN Animation trên n8n"
description: "Khám phá workflow n8n cực khủng giúp biến ý tưởng và hình ảnh sản phẩm thành video quảng cáo hoàn chỉnh, chuyên nghiệp tự động 100% bằng AI đa phương thức."
slug: "tu-dong-hoa-tao-video-quang-cao-gemini-fal-wan-n8n"
tags: [n8n, automation, no-code, ai-video, gemini, fal-ai]
keywords: [n8n workflow, tạo video quảng cáo tự động, gemini 2.5 flash, fal wan animation, ai content creation]
---

# 🚀 Tự động hóa sản xuất Video Quảng cáo đỉnh cao với Gemini 2.5 Flash & FAL WAN Animation

Việc sản xuất video quảng cáo (Video Ads) chuyên nghiệp thường ngốn rất nhiều thời gian, chi phí thuêagency và công sức lên kịch bản, dựng hình, tạo chuyển động (animation) rồi ghép nối âm thanh. Đứng trước áp lực làm nội dung số liên tục, các nhà sáng tạo và doanh nghiệp luôn tìm kiếm một giải pháp tự động hóa toàn diện.

Workflow n8n này chính là "vũ khí tối thượng" giúp các sếp dựng lên một hệ thống sản xuất video quảng cáo tự động 100% không cần code. Chỉ cần tải lên một hình ảnh sản phẩm qua Web Form, hệ thống sẽ tự động dùng AI (Gemini 2.5 Flash) để lên storyboard, sinh ảnh chi tiết, đẩy qua FAL WAN AI để tạo chuyển động mượt mà, xử lý âm thanh và ghép nối thành một video hoàn chỉnh sẵn sàng đăng tải!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Từ khâu nhận ảnh gốc qua Form, lập kịch bản storyboard bằng AI, sinh ảnh, tạo animation, đến lồng tiếng/âm thanh và ghép video.
- **Tiết kiệm 90% chi phí:** Không cần thuê đội ngũ dựng phim hay mua các công cụ trả phí đắt đỏ thủ công.
- **Tốc độ thần tốc:** Sản xuất hàng loạt video quảng cáo chất lượng cao chỉ trong vài phút chờ đợi.
- **Chất lượng đỉnh cao:** Ứng dụng các mô hình AI tiên tiến nhất hiện nay gồm Google Gemini 2.5 Flash và FAL WAN AI.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động mượt mà, các sếp cần chuẩn bị sẵn các tài khoản và API Keys sau:
- **n8n Instance** (phiên bản cập nhật hỗ trợ các node LangChain và HTTP Request nâng cao).
- **Google Gemini API Key** (cho các node Google Gemini Chat Model).
- **FAL.ai API Key** (dùng cho các node FAL WAN i2v để tạo animation video từ ảnh).
- **ImgBB API Key** (để upload và lưu trữ tạm thời các hình ảnh sản phẩm/storyboard).
- **Thông tin API phụ trợ** (cho FFmpeg dịch vụ dựng hình hoặc các dịch vụ tạo âm thanh, upload post nếu dùng).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần tải file JSON của workflow này từ nguồn gốc (hoặc copy toàn bộ mã JSON), sau đó paste trực tiếp vào giao diện n8n Editor của mình bằng tổ hợp phím `Ctrl + V` (hoặc `Cmd + V`).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Do hệ thống sử dụng rất nhiều node tích hợp AI và API bên thứ ba (tổng cộng 61 nodes), các sếp cần chú ý cấu hình kỹ các điểm sau:
- **Node `Photo Upload Form`**: Kiểm tra lại đường dẫn `path` (mặc định là `generate-ad`) để thu thập ảnh gốc từ người dùng.
- **Node `Google Gemini Chat Model`**: Kết nối chính xác với credential Google Gemini (`googlePalmApi`) để cấp quyền cho **Storyboard Agent** và các tác vụ phân tích ngôn ngữ.
- **Các node FAL WAN i2v (Queue/Status/Result)**: Điền API key của FAL.ai vào phần `httpHeaderAuth` để hệ thống gửi yêu cầu tạo chuyển động video từ ảnh và kiểm tra trạng thái render.
- **Các node Upload Image to imgbb**: Cấu hình tài khoản ImgBB để tự động lưu ảnh sinh ra từ Gemini trước khi đưa vào hàng đợi animation của FAL.ai.
- **Node `Sequence Video (FFmpeg)` & `Create Sounds`**: Đảm bảo các endpoint xử lý video và âm thanh được cấu hình chính xác theo dịch vụ backend mà các sếp đang sử dụng.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) bằng cách điền form mẫu để kiểm tra toàn bộ chuỗi từ hình ảnh đến khi xuất video cuối cùng.
- Sau khi kiểm tra luồng chạy mượt mà không lỗi, gạt công tắc sang **Active workflow** để đưa hệ thống vào vận hành chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo Telegram/Slack**: Thêm một node Telegram hoặc Slack ở cuối workflow để bot tự động gửi link download video hoàn chỉnh về cho các sếp ngay khi render xong.
- **Lưu trữ Google Drive**: Thay vì chỉ tải về, các sếp có thể cấu hình thêm node Google Drive để tự động backup toàn bộ các frames ảnh và video quảng cáo vào thư mục riêng biệt phục vụ việc quản lý tài nguyên marketing.
- **Mở rộng kênh đăng tải tự động**: Kết hợp thêm các node mạng xã hội (TikTok, YouTube, Facebook) để tự động hóa khâu publish video quảng cáo sau khi render.

### 📌 Kết luận
Workflow tạo video quảng cáo tự động với Gemini 2.5 Flash và FAL WAN Animation là một giải pháp đỉnh cao giúp tối ưu hóa quy trình sáng tạo nội dung số cho doanh nghiệp. Hãy thiết lập ngay hôm nay để bứt phá hiệu suất kinh doanh và marketing của các sếp!