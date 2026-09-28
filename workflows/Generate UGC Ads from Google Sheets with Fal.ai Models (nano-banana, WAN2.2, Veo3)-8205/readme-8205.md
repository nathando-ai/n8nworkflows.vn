---
title: "🚀 Tự động tạo Video UGC Ads từ Google Sheets sử dụng Fal.ai Models & n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa hoàn toàn quy trình tạo hình ảnh và video UGC Ads từ Google Sheets bằng các mô hình AI tiên tiến như Fal.ai (nano-banana, WAN2.2, Veo3) và OpenAI."
slug: "tao-ugc-ads-tu-google-sheets-voi-fal-ai-n8n"
tags: [n8n, automation, no-code, ai, fal-ai, ugc-ads, google-sheets]
keywords: [n8n workflow, tao ugc ads tu dong, fal.ai api, wan2.2, veo3, google sheets automation, ai content creation]
---

# 🚀 Tự động tạo Video UGC Ads từ Google Sheets sử dụng Fal.ai Models & n8n

Việc sản xuất nội dung quảng cáo UGC (User Generated Content) hay các video ngắn hàng loạt thường ngốn rất nhiều thời gian, nhân lực và chi phí của các nhà sáng tạo nội dung cũng như đội ngũ marketing. Việc phải lên ý tưởng, thiết kế hình ảnh, sau đó chuyển đổi thành video cho từng sản phẩm một cách thủ công là nỗi đau lớn.

Workflow n8n này sinh ra để giải quyết triệt để vấn đề đó! Với sự kết hợp giữa **Google Sheets**, **OpenAI (GPT-4o)**, và các mô hình AI đỉnh cao trên **Fal.ai** (như nano-banana, WAN2.2, Veo3), hệ thống sẽ tự động hóa toàn bộ quy trình: đọc dữ liệu sản phẩm, tạo hình ảnh gốc, phân tích cảnh quay, và render ra những thước phim quảng cáo sống động 100% tự động không cần can thiệp thủ công.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Chỉ cần nhập prompt và dữ liệu sản phẩm vào Google Sheets, hệ thống tự lo phần còn lại.
- **Tận dụng AI đa mô hình:** Kết hợp linh hoạt giữa OpenRouter/OpenAI để sinh text/phân tích hình ảnh và Fal.ai (WAN2.2, Veo3, nano-banana) để tạo ra hình ảnh, video chất lượng cao.
- **Quản lý file chuyên nghiệp:** Tự động lưu trữ toàn bộ ảnh và video render vào Google Drive và cập nhật ngược đường dẫn link vào Google Sheets.
- **Tối ưu chi phí & Thời gian:** Thay vì mất hàng giờ dựng video, hệ thống xử lý hàng loạt qua các vòng lặp (`Loop Over Items`) một cách trơn tru.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API Keys sau:
- **n8n Instance** (Self-hosted hoặc Cloud).
- **Google Sheets & Google Drive Account** (để lưu trữ và đồng bộ dữ liệu).
- **OpenAI API Key** (dành cho GPT-4o và phân tích hình ảnh).
- **OpenRouter API Key** (dành cho model tạo ảnh bổ trợ).
- **Fal.ai API Key** (dành cho các model tạo video/ảnh nâng cao như WAN2.2, Veo3, nano-banana).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ nguồn cấp hoặc copy toàn bộ mã nguồn JSON, sau đó dán trực tiếp vào giao diện n8n Editor của các sếp thông qua tính năng `Import from Clipboard`.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow được chia thành 2 Zone chính tương ứng với việc tạo ảnh và tạo video. Các sếp cần chú ý cấu hình các node cốt lõi sau:

- **Get Data1 / Get Data (Google Sheets Nodes):** 
  - Chọn Credentials kết nối tài khoản Google Sheets của các sếp.
  - Trỏ đúng tới File Spreadsheet và Sheet chứa danh sách prompt sản phẩm và hình ảnh đầu vào.
- **OpenAI Chat Model1 & Analyze image (OpenAI Nodes):** 
  - Cung cấp OpenAI API Key để model `gpt-4o` hoạt động. Node này chịu trách nhiệm phân tích hình ảnh và bóc tách thành các phân cảnh chi tiết (`Describe Each Scene for Video`).
- **Call Fal.ai API (WAN2.2), Call Fal.ai API (nannoBanana), Veo3 (HTTP Request Nodes):** 
  - Các node này sử dụng phương thức `httpHeaderAuth` để gọi API trực tiếp đến Fal.ai. Các sếp nhớ điền đúng Fal.ai API Key vào phần Header Authentication.
- **uploadImagetoGdrive / uploadImagetoGdrive1 (Google Drive Nodes):** 
  - Kết nối tài khoản Google Drive và chọn thư mục (`Folder ID`) đích để lưu trữ file ảnh và video được render ra.
- **updateImageURL / updateVideoURL (Google Sheets Nodes):** 
  - Cấu hình chế độ `appendOrUpdate` để hệ thống tự động ghi đè hoặc thêm link file Media (Drive URL) vào đúng dòng tương ứng trong Google Sheets.

#### 3. Kích hoạt ⚡️
- Nhấn nút **When clicking ‘Execute workflow’** (hoặc dùng `Manual Trigger`) để test chạy thử với 1 dòng dữ liệu mẫu đầu tiên.
- Kiểm tra kết quả trả về trên Google Drive và Google Sheets.
- Nếu mọi thứ chạy mượt mà, hãy gạt công tắc sang chế độ **Active** để hệ thống sẵn sàng vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Webhook/Trigger tự động:** Thay vì dùng `Manual Trigger`, các sếp có thể đổi thành `Webhook` hoặc `Schedule Trigger` để hệ thống tự động quét Google Sheets mỗi sáng và tạo video hàng loạt.
- **Gửi thông báo qua Telegram/Slack:** Thêm một node Telegram hoặc Slack ở cuối workflow để bot gửi thông báo trực tiếp kèm link video hoàn thiện ngay khi render xong.
- **Xử lý lỗi (Error Handling):** Thêm nhánh `Error Trigger` để bắt lỗi trong trường hợp Fal.ai quá tải hoặc API trả về lỗi, giúp hệ thống không bị ngắt quãng bất ngờ.

### 📌 Kết luận
Với workflow n8n này, việc sản xuất hàng loạt video UGC Ads phục vụ cho các chiến dịch Marketing, Dropshipping hay TikTok Shop đã trở nên đơn giản hơn bao giờ hết. Hãy setup ngay hôm nay để tối ưu hóa hiệu suất làm việc cho đội ngũ của các sếp nhé!