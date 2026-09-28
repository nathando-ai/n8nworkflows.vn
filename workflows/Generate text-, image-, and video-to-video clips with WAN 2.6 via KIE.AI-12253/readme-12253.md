---
title: "🚀 Tự động tạo Video từ Text, Image và Video bằng WAN 2.6 qua KIE.AI trên n8n"
description: "Hướng dẫn cấu hình workflow n8n tích hợp KIE.AI và WAN 2.6 giúp tự động hóa tạo video chất lượng cao từ văn bản, hình ảnh và biến đổi video gốc."
slug: "tao-video-tu-dong-wan-2-6-kie-ai-n8n"
tags: [n8n, automation, ai-video, wan-2.6, kie-ai, content-creation]
keywords: [n8n workflow, tạo video ai, wan 2.6, kie ai api, text to video automation]
---

# 🚀 Tự động tạo Video từ Text, Image và Video bằng WAN 2.6 qua KIE.AI

Các sếp đang tốn bao nhiêu thời gian để tạo ra các đoạn video ngắn cho chiến dịch marketing, TikTok hay Reels? Việc phải thao tác thủ công trên các công cụ AI tạo video, chờ đợi render rồi tải về máy tốn rất nhiều công sức và gián đoạn luồng sáng tạo.

Giải pháp đây rồi! Workflow n8n siêu việt này giúp các sếp tự động hóa 100% quy trình gọi API **KIE.AI** sử dụng mô hình **WAN 2.6**. Hệ thống sẽ tự động gửi yêu cầu, liên tục kiểm tra tiến độ (polling) và tự động tải video hoàn thiện về cho các sếp mà không cần đụng tay chân.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và render video không bị gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Đa dạng định dạng đầu vào**: Hỗ trợ đồng thời 3 tính năng: Text-to-Video (Tạo video từ văn bản), Image-to-Video (Biến ảnh tĩnh thành video), và Video-to-Video (Biến đổi video gốc).
- **Tự động hóa hoàn toàn**: Không cần canh chừng thời gian render, workflow tự động lặp (polling) kiểm tra trạng thái mỗi vài giây.
- **Tối ưu thời gian**: Tự động tải file video về ngay khi AI xử lý xong.
- **Linh hoạt cấu hình**: Dễ dàng tùy chỉnh thông số độ dài, độ phân giải và prompt ngay trong các node cài đặt sẵn.
:::

### Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản và API Key tại [KIE.AI](https://kie.ai/)
- n8n instance (Cloud hoặc Self-hosted)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã nguồn JSON của workflow (hoặc tải file JSON từ nguồn gốc) và dán trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 22 nodes được chia thành 3 nhánh xử lý độc lập cho 3 nhu cầu khác nhau:

*   **Cấu hình chung Credentials**: 
    - Các node yêu cầu xác thực như `Submit Video Generation Request`, `Check Video Generation Status`, `Submit Video Generation`, `Check Video Generation`, `Submit Video Generation a`, `Check Video Status` cần được gắn Credential loại **HTTP Bearer Auth** với tên gợi nhớ là **KIE.AI** chứa API Key của các sếp.
*   **Nhánh Text-to-Video**:
    - `Set Video Parameters`: Chỉnh sửa prompt, thời lượng (5s / 10s / 15s), độ phân giải (720p / 1080p).
    - Kích hoạt qua nút `When clicking ‘Execute workflow’`.
*   **Nhánh Video-to-Video**:
    - `Set Video URL and Prompt`: Cung cấp link video gốc (`video_urls`), prompt mô tả biến đổi, độ dài và độ phân giải mong muốn.
*   **Nhánh Image-to-Video**:
    - `Set Prompt & Image Url`: Cung cấp link ảnh gốc (`image_url`), prompt chuyển động, độ dài và độ phân giải.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** trên từng nhánh để test thử quá trình gửi request -> chờ (`Wait nodes`) -> kiểm tra trạng thái (`Switch & HTTP Request nodes`) -> trích xuất URL (`Code nodes`) -> tải video (`Download nodes`).
- Sau khi test thành công, các sếp có thể đổi trigger thành Webhook hoặc Schedule nếu muốn tự động hóa theo lịch trình.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp lưu trữ Cloud**: Thay thế các node `Download Video` bằng node Google Drive hoặc AWS S3 để tự động lưu trữ video lên mây.
- **Gửi thông báo**: Thêm node Telegram hoặc Slack ở cuối luồng để nhận thông báo kèm file video ngay khi render xong.
- **Quản lý hàng đợi (Queue)**: Kết hợp Google Sheets để nạp danh sách prompt hàng loạt và chạy vòng lặp tự động tạo hàng chục video mỗi ngày.

### 📌 Kết luận
Workflow tích hợp KIE.AI và WAN 2.6 này là trợ thủ đắc lực cho các nhà sáng tạo nội dung muốn tối ưu hóa sản xuất video bằng AI. Hãy cài đặt ngay hôm nay để tiết kiệm hàng giờ làm việc thủ công các sếp nhé!