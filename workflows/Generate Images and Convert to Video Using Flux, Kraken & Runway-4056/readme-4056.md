---
title: "🚀 Tự động hóa tạo ảnh bằng Flux và chuyển thành video với Runway trong n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình tạo ảnh nghệ thuật bằng Flux AI và chuyển đổi thành video chất lượng cao qua Runway kết hợp Kraken."
slug: "tu-dong-hoa-tao-anh-flux-va-video-runway-n8n"
tags: [n8n, automation, ai, flux, runway, kraken, image-to-video]
keywords: [n8n workflow, tạo ảnh flux, runway ai, chuyển ảnh thành video, tự động hóa ai, kraken io]
---

# 🚀 Tự động hóa tạo ảnh bằng Flux và chuyển thành video với Runway trong n8n

Việc tạo ra hình ảnh bằng AI rồi tiếp tục đưa sang các công cụ chuyển đổi thành video thủ công thường ngốn rất nhiều thời gian của các nhà sáng tạo nội dung và doanh nghiệp. Quá trình tải ảnh lên, chờ đợi render, tải xuống rồi lại upload lên nền tảng tạo video tiếp theo vô cùng nhàm chán và dễ xảy ra sai sót.

Được thiết kế bởi chuyên gia Joseph (`joseph@uppfy.com`), workflow n8n này sẽ giải quyết triệt để bài toán trên bằng cách tự động hóa 100% quy trình: **Từ tạo ảnh bằng Flux (Black Forest Labs/Rapid API) -> tối ưu hình ảnh qua Kraken -> chuyển đổi thành video động bằng Runway AI**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow xử lý các tác vụ AI và render video nặng chạy ổn định 24/7 mà không sợ gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Xâu chuỗi mượt mà giữa các AI mạnh mẽ nhất hiện nay (Flux và Runway) mà không cần can thiệp thủ công.
- **Tối ưu tài nguyên:** Sử dụng Kraken để nén và tối ưu hóa hình ảnh trước khi đẩy vào pipeline tạo video.
- **Xử lý bất đồng bộ thông minh:** Tích hợp các node `Wait` và `Switch` để kiểm tra trạng thái render video định kỳ cho đến khi hoàn thành.
- **Linh hoạt lựa chọn:** Hỗ trợ cả API chính thức (Official APIs) lẫn Rapid API endpoints tùy thuộc vào nhu cầu và ngân sách của các sếp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- **n8n instance** (phiên bản cloud hoặc self-hosted).
- **Flux API Key** (hoặc tài khoản Rapid API đăng ký gói Flux).
- **Runway API Key** (hoặc Rapid API Endpoint cho Runway).
- **Kraken.io API Key** (dùng để tối ưu và lấy link công khai cho hình ảnh).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow từ nguồn cấp hoặc copy toàn bộ mã JSON.
- Trong giao diện n8n Editor, bấm vào menu **Workflows** -> **Import from File** (hoặc dán trực tiếp vào canvas).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 16 nodes được chia thành các nhánh xử lý khác nhau (hỗ trợ cả API gốc và Rapid API). Các sếp cần chú ý cấu hình các node cốt lõi sau:

- **Node `generate image (flux)` hoặc `generate image (flux-rapid-api)`**: 
  - Chọn đúng credentials cho Flux/Rapid API.
  - Tùy chỉnh tham số câu lệnh (`prompt`) đầu vào để tạo ra bức ảnh theo đúng ý muốn.
- **Node `upload to kraken` / `upload to kraken1`**: 
  - Điền Kraken API Key để hệ thống upload ảnh vừa tạo lên cloud, trả về URL công khai phục vụ cho bước làm video.
- **Node `image to video (runway)` hoặc `image to video (runway-rapid-api)`**: 
  - Cấu hình API Key của Runway.
  - Đưa URL hình ảnh từ bước Kraken vào payload để bắt đầu quá trình tạo video.
- **Hệ thống kiểm tra trạng thái (`Get Video Generation Status1`, `Confirm Generation Status`, `1 minute3`)**: 
  - Do quá trình tạo video cần thời gian render, hệ thống sử dụng node `Wait` (1 phút) và node `Switch` để kiểm tra liên tục trạng thái video. Các sếp có thể giữ nguyên cấu hình này để đảm bảo workflow không bị lỗi timeout.
- **Node `Download Video`**: 
  - Cấu hình đích lưu trữ (có thể nối thêm node Google Drive, Telegram hoặc Slack để tự động tải video về máy hoặc gửi thông báo).

#### 3. Kích hoạt ⚡️
- Bấm **‘Test workflow’** bằng tay thông qua node `When clicking ‘Test workflow’` để kiểm tra xem Flux có tạo ảnh và Runway có render video thành công hay không.
- Kiểm tra lại các kết quả trả về, nếu mọi thứ chạy trơn tru, hãy chuyển trạng thái sang **Active** để đưa vào vận hành thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm node Telegram Bot hoặc Slack vào cuối chuỗi `Download Video` để nhận thông báo kèm file video ngay lập tức khi render xong.
- **Mở rộng nguồn Prompt:** Thay vì dùng trigger thủ công, các sếp có thể kết hợp với Google Sheets hoặc Airtable để nhập danh sách prompt hàng loạt, giúp n8n tự động chạy chuỗi sản xuất video hàng loạt.
- **Lưu trữ đám mây:** Thêm node Google Drive hoặc Dropbox để tự động lưu các video đã tạo vào thư mục phân loại rõ ràng.

### 📌 Kết luận
Workflow "Generate Images and Convert to Video Using Flux, Kraken & Runway" là một cỗ máy tự động hóa đỉnh cao dành cho các nhà sáng tạo nội dung AI. Hãy áp dụng ngay để tiết kiệm hàng giờ thao tác thủ công mỗi ngày và bứt phá hiệu suất công việc!