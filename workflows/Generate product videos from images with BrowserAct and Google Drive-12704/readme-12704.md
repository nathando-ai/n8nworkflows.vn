---
title: "🚀 Tự động tạo video sản phẩm từ hình ảnh với BrowserAct và Google Drive trên n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình thu thập dữ liệu sản phẩm, biến hình ảnh thành video ngắn bằng AI và đồng bộ hóa kết quả lên Google Drive."
slug: "tu-dong-tao-video-san-pham-browseract-google-drive-n8n"
tags: [n8n, automation, no-code, browseract, google-drive, ai-video]
keywords: [n8n workflow, tạo video sản phẩm tự động, browseract, google drive automation, ai video generation]
---

# 🚀 Tự động hóa sản xuất video sản phẩm bằng AI với BrowserAct & Google Drive

Các sếp làm trong ngành thương mại điện tử hoặc sáng tạo nội dung chắc chắn đều hiểu nỗi đau: Mỗi khi có danh mục sản phẩm mới, việc phải tải hình ảnh thủ công, tìm kiếm công cụ tạo video ngắn (AI video) cho từng món hàng, rồi lại tải về và sắp xếp vào Google Drive tốn hàng giờ đồng hồ mệt mỏi.

Đừng tốn thời gian cho những việc lặp đi lặp lại đó nữa! Bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ mạnh mẽ, giúp tự động hóa toàn bộ quy trình: từ thu thập dữ liệu hình ảnh sản phẩm bằng **BrowserAct**, xử lý và tạo video qua API AI, cho đến việc tự động lưu trữ gọn gàng vào **Google Drive**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Không cần thao tác thủ công từ khâu lấy ảnh sản phẩm đến khi ra lò video ngắn.
- **Xử lý hàng loạt mượt mà:** Sử dụng cơ chế phân lô (`splitInBatches`) giúp xử lý từng sản phẩm độc lập, tránh quá tải API.
- **Đồng bộ hóa khoa học:** Ảnh gốc và video được tạo ra tự động phân loại và lưu trữ an toàn trên Google Drive.
- **Tích hợp AI thông minh:** Kết hợp BrowserAct để cào dữ liệu web thực tế và các API tạo video bằng AI tiên tiến.
:::

### Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một hệ thống n8n đã sẵn sàng (Self-hosted hoặc n8n Cloud).
- Tài khoản và API Key của **BrowserAct** (`browserActApi`).
- Tài khoản **Google Drive** để cấu hình OAuth2 kết nối lưu trữ.
- Các API Endpoint và Header xác thực (`httpHeaderAuth`) cho dịch vụ gọi AI tạo video.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ kho lưu trữ n8n (ID: `12704`) và tiến hành Import trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 16 nodes hoạt động nhịp nhàng, các sếp cần chú ý cấu hình kỹ các điểm sau:

- **When clicking ‘Execute workflow’ (`manualTrigger`):** Điểm khởi chạy thủ công để test. Có thể thay thế bằng `Schedule Trigger` nếu muốn chạy tự động định kỳ.
- **Run a workflow (`browserActApi`):** Kết nối tài khoản BrowserAct của các sếp. Node này chịu trách nhiệm cào dữ liệu, thu thập URL hình ảnh sản phẩm và metadata từ trang web mục tiêu.
- **limit_products & iterate_products (`limit` & `splitInBatches`):** Điều chỉnh số lượng sản phẩm giới hạn và kích thước batch xử lý để kiểm soát thời gian chạy tránh vượt quá giới hạn API.
- **fetch_image & download_video (`httpRequest`):** Tải hình ảnh nguồn về và tải file video hoàn thiện sau khi AI xử lý xong.
- **Submit video generation request & Check video generation status:** Gửi prompt và hình ảnh sang hệ thống tạo video AI. Node `Wait for video generation` đóng vai trò cực kỳ quan trọng để chờ xử lý bất đồng bộ, **tuyệt đối không xóa node Wait này**.
- **upload_source_image & upload_output_video (`googleDrive`):** Kết nối tài khoản `googleDriveOAuth2Api` để chỉ định thư mục lưu trữ ảnh gốc và video thành phẩm trên Drive của các sếp.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để chạy thử với một lượng sản phẩm nhỏ (thông qua node `limit_products`).
- Kiểm tra kết quả trả về trên Google Drive và các log trong n8n.
- Sau khi mọi thứ chạy trơn tru, hãy bật **Active** để workflow tự động làm việc thay các sếp.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm thông báo:** Tích hợp thêm node Telegram hoặc Slack vào cuối chuỗi xử lý để nhận thông báo ngay khi video của sản phẩm mới được tạo xong và đẩy lên Drive.
- **Lưu log vào Google Sheets:** Thêm một node Google Sheets để ghi lại trạng thái sản phẩm, link ảnh và link video tương ứng để dễ dàng quản lý chiến dịch marketing.
- **Tùy biến Prompt:** Tinh chỉnh prompt tại node `set_prompt` để phong cách video AI phù hợp hơn với thương hiệu của sản phẩm.

### 📌 Kết luận
Với workflow n8n kết hợp BrowserAct và Google Drive này, việc sản xuất hàng loạt video ngắn quảng cáo sản phẩm từ hình ảnh tĩnh nay đã trở nên tự động hoàn toàn. Hãy thiết lập ngay hôm nay để tiết kiệm thời gian và tối ưu hóa hiệu suất kinh doanh cho đội ngũ của các sếp!