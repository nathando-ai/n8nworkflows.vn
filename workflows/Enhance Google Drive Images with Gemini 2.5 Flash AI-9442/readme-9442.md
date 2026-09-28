---
title: "🚀 Tự động xử lý và cải thiện hình ảnh trên Google Drive bằng Gemini AI"
description: "Hướng dẫn xây dựng workflow n8n tự động quét ảnh từ Google Drive, phân tích và xử lý qua Google Gemini 2.5 Flash AI rồi lưu vào thư mục đích."
slug: "tu-dong-xu-ly-hinh-anh-google-drive-voi-gemini-ai"
tags: [n8n, automation, google-drive, google-gemini, ai, image-processing]
keywords: [n8n workflow, tự động hóa google drive, gemini ai xử lý ảnh, google palm api, n8n image processing]
---

# 🚀 Tự động xử lý và cải thiện hình ảnh trên Google Drive bằng Gemini AI

Các sếp có bao giờ cảm thấy mệt mỏi khi phải xử lý, chỉnh sửa hoặc phân tích hàng loạt hình ảnh thủ công trên Google Drive? Việc tải xuống, gọi AI phân tích rồi upload lại tốn rất nhiều thời gian và công sức.

Đừng lo, với workflow n8n cực xịn sò được chia sẻ bởi tác giả **Edisson Garcia**, toàn bộ quy trình này sẽ được tự động hóa 100%. Workflow sẽ tự động quét ảnh trong thư mục nguồn, chuyển đổi sang Base64, gửi đến **Google Gemini AI** xử lý theo yêu cầu của các sếp, sau đó chuyển đổi kết quả thành file ảnh mới và lưu tự động vào thư mục đích trên Google Drive.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Không cần thao tác thủ công, quy trình từ lấy file, xử lý AI đến lưu trữ diễn ra liền mạch.
- **Sức mạnh từ Gemini AI:** Tận dụng khả năng phân tích và xử lý hình ảnh đỉnh cao của Google Gemini 2.5 Flash thông qua API.
- **Xử lý hàng loạt thông minh:** Sử dụng cơ chế phân lô (`Split In Batches`) giúp xử lý nhiều ảnh mà không lo vượt quá giới hạn tài nguyên.
- **Lưu trữ gọn gàng:** Tách biệt rõ ràng thư mục ảnh gốc (`origin_folder`) và thư mục ảnh đã xử lý (`destination_folder`).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Self-hosted hoặc Cloud).
- **Google Drive Account:** Tài khoản Google Drive chứa thư mục ảnh nguồn và thư mục đích.
- **Google Gemini API Key / Google Palm API:** Credentials để kết nối với Google AI.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ [n8n Template gốc](https://n8n.io/workflows/9442) và import trực tiếp vào giao diện n8n của mình, hoặc copy/paste toàn bộ mã JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động trơn tru với dữ liệu của các sếp, hãy chú ý cấu hình các node quan trọng sau:

- **`promt` (Node Type: Set):** Mở node này và chỉnh sửa lại đoạn văn bản (prompt) hướng dẫn cho Gemini theo ý muốn của các sếp (ví dụ: yêu cầu phong cách xử lý, mô tả, hoặc chuyển đổi hình ảnh).
- **`origin_folder` (Node Type: Google Drive):** Trong phần tham số tìm kiếm (`Search Query`), điền chính xác tên thư mục nguồn chứa các hình ảnh cần xử lý trên Google Drive của các sếp.
- **`destination_folder` (Node Type: Google Drive):** Trong phần tham số tìm kiếm (`Search Query`), điền tên thư mục đích nơi sẽ lưu trữ các hình ảnh sau khi đã được Gemini AI xử lý.
- **Credentials:** 
  - Kết nối tài khoản **Google Drive OAuth2 API** cho các node `download-file`, `upload-result`, `get files`, `origin_folder`, và `destination_folder`.
  - Kết nối **Google Palm API / Gemini API** cho node `banana-request` (`httpRequest`).

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** tại node `init` (`manualTrigger`) để test thử với một vài hình ảnh mẫu.
- Kiểm tra kết quả trong thư mục đích trên Google Drive.
- Nếu mọi thứ chạy mượt mà, hãy gạt công tắc sang **Active** để workflow tự động hoạt động theo lịch trình hoặc sự kiện kích hoạt.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp thông báo:** Thêm node **Telegram** hoặc **Slack** ở cuối luồng để nhận thông báo ngay khi AI xử lý xong một batch hình ảnh.
- **Lưu Log:** Đẩy thông tin tên file, trạng thái xử lý vào **Google Sheets** để dễ dàng quản lý và kiểm tra lịch sử chạy.
- **Mở rộng định dạng:** Điều kiện ở node `Filter` hiện tại đang lọc các file có `mimeType` chứa chữ "image". Các sếp có thể tùy chỉnh thêm để chỉ định rõ `.jpg`, `.png` tùy theo nhu cầu.

### 📌 Kết luận
Workflow xử lý hình ảnh với Gemini AI là một trợ thủ đắc lực cho những ai thường xuyên làm việc với nội dung số, thiết kế hay marketing. Hãy triển khai ngay hôm nay để tiết kiệm hàng giờ đồng hồ làm việc thủ công!