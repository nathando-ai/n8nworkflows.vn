---
title: "🚀 Tự động tạo video AI từ văn bản bằng Google Veo và n8n"
description: "Hướng dẫn cấu hình workflow n8n tích hợp Google Gemini (mô hình Veo) để tự động hóa quy trình tạo video chất lượng cao từ câu lệnh văn bản."
slug: "tao-video-ai-tu-van-ban-google-veo-n8n"
tags: [n8n, automation, google-veo, google-gemini, ai-video, content-creation]
keywords: [n8n workflow, tạo video ai, google veo, google gemini, tự động hóa video, ai automation]
---

# 🚀 Tự động tạo video AI từ văn bản bằng Google Veo và n8n

Các sếp có bao giờ cảm thấy mệt mỏi khi phải mất hàng giờ đồng hồ mò mẫm trên các công cụ tạo video AI thủ công, nhập từng câu lệnh rồi chờ đợi xuất file, sau đó lại lặp lại quy trình đó cho hàng chục ý tưởng khác nhau? Việc sản xuất nội dung video ngắn, B-roll hay các thước phim quảng cáo thủ công đang ngốn quá nhiều thời gian và chi phí nhân sự của doanh nghiệp.

Giải pháp là đây! Với workflow n8n tích hợp mô hình **Google Veo** thông qua **Google Gemini**, các sếp có thể tự động hóa 100% quy trình biến văn bản thành video chuyên nghiệp mà không cần viết một dòng code nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tốc độ thần tốc:** Tạo nhanh các đoạn B-roll, video quảng cáo hoặc nội dung mạng xã hội chỉ từ một đoạn mô tả ngắn.
- **Tiết kiệm chi phí:** Không cần ekip quay phim phức tạp hay các công cụ dựng hình đắt đỏ để phác thảo ý tưởng (storyboard).
- **Tích hợp liền mạch:** Biến n8n thành một xưởng sản xuất video tự động, sẵn sàng kết nối với Google Drive, Telegram hoặc các nền tảng mạng xã hội.
- **Sẵn sàng mở rộng:** Dễ dàng nâng cấp để tạo hàng loạt video tự động từ danh sách câu lệnh trong Google Sheets.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Hệ thống n8n:** Đã cài đặt n8n (Bản Cloud hoặc Self-hosted).
- **Tài khoản Google Cloud & Google AI:** Dự án Google Cloud **phải bật tính năng thanh toán (Billing enabled)** vì mô hình Veo không hỗ trợ gói miễn phí và có thể phát sinh chi phí.
- **Google AI (Gemini) Credentials:** API Key từ Google AI Studio được liên kết với dự án đã bật thanh toán.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow này và paste trực tiếp vào giao diện n8n Editor của mình, hoặc import file JSON đã tải về.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 3 nodes chính, các sếp cần chú ý cấu hình kỹ các điểm sau:
- **Node `When clicking ‘Execute workflow’` (Manual Trigger):** Dùng để kích hoạt thủ công khi các sếp muốn test nhanh ý tưởng.
- **Node `1. Set Video Prompt` (Set):** 
  - Tại trường `Value`, các sếp nhập đoạn mô tả chi tiết (prompt) về video muốn tạo. 
  - *Mẹo:* Càng miêu tả chi tiết bối cảnh, ánh sáng, chuyển động camera, chất lượng video trả về càng xuất sắc!
- **Node `2. Generate Video with Veo` (Google Gemini):**
  - **Credentials:** Chọn kết nối `Google Palm/Gemini API` và nhập API Key của các sếp.
  - **Resource:** Đặt là `Video`.
  - **Prompt:** Lấy dữ liệu động từ node trước `= {{ $json.prompt }}`.
  - *Lưu ý quan trọng:* Node này sẽ báo lỗi nếu tài khoản Google Cloud của các sếp chưa bật tính năng Billing.

#### 3. Kích hoạt ⚡️
- Nhấn nút **“Execute Workflow”** để chạy thử nghiệm và nhận file video dạng binary trả về.
- Sau khi kiểm tra thành công, các sếp có thể bật công tắc **Active** để sẵn sàng sử dụng.

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa workflow này cho doanh nghiệp, các sếp có thể nâng cấp thêm các bước sau:
- **Tự động lưu trữ:** Thêm node **Google Drive**, **Dropbox** hoặc **AWS S3** ngay sau bước tạo video để tự động lưu file xuất ra vào thư mục lưu trữ chung.
- **Đăng tải tự động:** Kết nối thêm các node mạng xã hội (YouTube Shorts, TikTok, Facebook Reels) để tự động xuất bản nội dung.
- **Tạo video hàng loạt (Bulk Generation):** Thay thế node `Set` bằng **Google Sheets** hoặc **Airtable** để n8n tự động đọc danh sách hàng trăm câu lệnh và tạo ra hàng loạt video liên tục.

### 📌 Kết luận
Việc tích hợp AI Video Generation vào hệ thống tự động hóa chưa bao giờ dễ dàng đến thế với n8n và Google Veo. Hãy "lên đồ" ngay hôm nay để tối ưu hóa quy trình sáng tạo nội dung cho doanh nghiệp của các sếp!