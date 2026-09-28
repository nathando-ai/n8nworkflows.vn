---
title: "🚀 Tự động tạo ảnh bằng AI với APImage và lưu trực tiếp lên Google Drive qua n8n"
description: "Xây dựng hệ thống tạo ảnh AI tự động từ Form nhập liệu, gọi APImage API và tự động lưu file ảnh vào Google Drive một cách mượt mà bằng n8n."
slug: "tu-dong-tao-anh-ai-voi-apimage-google-drive-n8n"
tags: [n8n, automation, ai-images, google-drive, apimage, no-code]
keywords: [n8n workflow, tạo ảnh ai tự động, apimage api, google drive automation, n8n form trigger]
---

# 🚀 Tự động tạo ảnh bằng AI với APImage và lưu trực tiếp lên Google Drive

Các sếp có bao giờ cảm thấy mệt mỏi khi phải liên tục copy prompt, vào các trang web tạo ảnh AI, tải ảnh về máy rồi lại thủ công upload lên Google Drive để lưu trữ chưa? Quy trình lặp đi lặp lại này ngốn rất nhiều thời gian, đặc biệt là với các đội ngũ làm nội dung, EdTech hay marketing.

Giải pháp ở đây chính là tự động hóa 100% quy trình này! Với workflow n8n được chia sẻ từ đội ngũ **Gegenfeld**, các sếp chỉ cần điền một chiếc form đơn giản, hệ thống sẽ tự động gọi APImage API để vẽ tranh theo yêu cầu và cất gọn gàng vào thư mục Google Drive mơ ước. Không cần một dòng code nào cả!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không lo gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian tối đa:** Thay vì làm thủ công qua 4-5 bước, giờ đây chỉ cần vài cú click trên Form.
- **Lưu trữ tự động, khoa học:** Ảnh vừa tạo xong lập tức có mặt trên Google Drive, sẵn sàng để chia sẻ hoặc dùng cho các chiến dịch.
- **Tùy biến linh hoạt:** Dễ dàng thay đổi kích thước ảnh (`Square`, `Landscape`, `Portrait`) và mô hình (`Basic`, `Premium`) ngay từ đầu vào.
- **Hoạt động liên tục 24/7:** Bot tự động xử lý mượt mà trên nền tảng n8n tự host hoặc Cloud.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Đã hoạt động (Cloud hoặc Self-hosted).
- **Tài khoản APImage:** Lấy API Key tại [Dashboard APImage](https://apimage.org/dashboard).
- **Tài khoản Google Drive:** Để kết nối node `Upload file` và lưu ảnh.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow này và paste trực tiếp vào n8n Editor của mình là xong!

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 4 nodes chính, các sếp hãy cấu hình theo các bước sau:

- **Node `Generate Image` (Form Trigger):** Node này đóng vai trò là giao diện nhập liệu. Các sếp có thể mở ra để xem cấu trúc form (nhận `prompt`, `dimensions`, `model`) hoặc chia sẻ link form này cho team cùng sử dụng.
- **Node `APImage API` (HTTP Request):** 
  - Double-click vào node để mở.
  - Thay thế chữ `YOUR_API_KEY` bằng API Key thực tế của các sếp (giữ nguyên tiền tố `"Bearer"` ở phía trước).
- **Node `Download Image` (HTTP Request):** Nhận kết quả từ APImage API và tải file ảnh về dưới dạng dữ liệu nhị phân (binary) để chuẩn bị đẩy đi.
- **Node `Upload file` (Google Drive):** 
  - Kết nối tài khoản Google Drive của các sếp.
  - Chọn thư mục đích trên Google Drive để lưu trữ ảnh được tạo ra.

> 🐞 **Mẹo xử lý lỗi 504 Gateway Timeout:** Lỗi này có thể xảy ra nếu n8n chờ quá lâu cho một tác vụ tạo ảnh nặng. Để khắc phục, hãy tăng giá trị thông số **Timeout** trong HTTP Request node lên (ví dụ: `180000` mili-giây tương đương 3 phút). Nếu dùng bản Self-hosted, tình trạng này cực kỳ hiếm gặp vì các sếp làm chủ hoàn toàn tài nguyên.

#### 3. Kích hoạt ⚡️
- Nhấn **Test step** hoặc **Execute Workflow** trên node Form Trigger để thử nghiệm nhập một prompt bất kỳ.
- Kiểm tra xem ảnh đã được tạo và xuất hiện trên Google Drive chưa.
- Nếu mọi thứ mượt mà, gạt công tắc sang **Active** để chính thức đưa vào vận hành thực tế!

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh nhận ảnh:** Ngoài Google Drive, các sếp hoàn toàn có thể thay thế node Google Drive bằng **Dropbox**, **Notion**, **WordPress**, hoặc tự động gửi ảnh vừa tạo thẳng vào **Telegram / Slack** cá nhân của team.
- **Lưu lịch sử:** Kết nối thêm một node Google Sheets để ghi lại `Prompt`, `Thời gian tạo`, và `Link ảnh trên Drive` nhằm dễ dàng tra cứu về sau.

### 📌 Kết luận
Việc tích hợp AI vào quy trình làm việc hàng ngày chưa bao giờ dễ dàng đến thế với n8n. Hãy áp dụng ngay workflow này để tối ưu hóa thời gian sáng tạo hình ảnh cho doanh nghiệp của các sếp nhé!