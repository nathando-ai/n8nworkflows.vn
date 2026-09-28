---
title: "🚀 Tự động hóa tạo video ngắn AI từ Form với Groq, Google Sheets và Veo 3 trên n8n"
description: "Hướng dẫn chi tiết workflow n8n tự động hóa toàn bộ quy trình: nhận ý tưởng từ Form, dùng AI sinh prompt, gọi API Veo 3 tạo video, xử lý retry lỗi và lưu trữ tự động vào Google Drive & Google Sheets."
slug: "tu-dong-hoa-tao-video-ngan-ai-veo-3-groq-google-sheets"
tags: [n8n, automation, ai-video, google-sheets, google-drive, groq]
keywords: [n8n workflow, tạo video ai, veo 3, groq ai, tự động hóa marketing, google sheets, google drive]
---

# 🚀 Tự động hóa tạo video ngắn AI từ Form với Groq, Google Sheets và Veo 3

Các sếp có đang chật vật với việc lên ý tưởng, viết prompt và tạo hàng loạt video ngắn (short-form videos) thủ công cho TikTok, Reels hay YouTube Shorts không? Quá trình này ngốn rất nhiều thời gian từ khâu sáng tạo nội dung, render video cho đến quản lý file.

Bài viết này sẽ giới thiệu một siêu phẩm n8n workflow do chuyên gia **Mohan Lal Dhanwani** xây dựng. Workflow này sẽ tự động hóa **100%** quy trình: nhận chủ đề từ Form 👉 Dùng AI (Groq + Llama 3.3) lên ý tưởng & viết prompt chuẩn cho Veo 3 👉 Gửi yêu cầu tạo video 👉 Kiểm tra trạng thái & xử lý lỗi 👉 Tự động lưu video lên Google Drive và cập nhật link vào Google Sheets. Các sếp chỉ việc ngồi uống trà và nhận thành quả!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không sợ sập, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện**: Biến một dòng text từ Form thành một video hoàn chỉnh mà không cần can thiệp thủ công.
- **AI thông minh**: Sử dụng **Groq (Llama-3.3-70b-versatile)** kết hợp Structured Output để sinh ý tưởng và prompt video cực kỳ chuẩn xác, sáng tạo.
- **Cơ chế Retry thông minh**: Tự động kiểm tra lỗi API, chờ và thử lại (retry) nếu Veo 3 đang bận, đảm bảo tỷ lệ thành công cao.
- **Đồng bộ hóa dữ liệu tuyệt vời**: Mọi thông tin, ý tưởng, prompt và link video đều được quản lý gọn gàng trên Google Sheets và lưu trữ an toàn trên Google Drive.
:::

---

### 📦 Tổng quan cấu trúc Workflow (18 Nodes)
Workflow bao gồm các phân đoạn chính sau:
1. **Nhận dữ liệu**: `When Form Submitted` (Thu thập ý tưởng/chủ đề ban đầu từ người dùng).
2. **Sáng tạo nội dung AI**: Sử dụng `Idea Generation Agent`, `Video Prompt Agent`, `Groq AI Model`, `Parse Structured Output` và `Trigger Thought Process` để tạo kịch bản và prompt cho Veo 3.
3. **Lưu vết ban đầu**: `Append Content To Sheet` ghi nhận thông tin ý tưởng vào Google Sheets.
4. **Tạo & Poll Video (Vertex AI / Veo 3)**:
   - `Post to Veo 3 API` (Gửi request tạo video).
   - `Wait 60 Seconds for Video` & `Poll Video Generation Status` (Chờ và kiểm tra tiến độ).
   - `Check Video Completion`, `Check for API Error`, `Check Retry Limit`, `Wait 60 Seconds for Retry`, `Stop on Max Retries` (Hệ thống kiểm tra trạng thái và xử lý lỗi/retry tự động).
5. **Lưu trữ kết quả**:
   - `Convert Video to File` (Chuyển đổi dữ liệu trả về thành file binary).
   - `Upload File to Google Drive` (Đưa file lên Drive).
   - `Update Sheet with URL` (Cập nhật link video hoàn chỉnh về Google Sheets).

---

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ TRƯỚC KHI "LÊN ĐỒ"]
- **n8n Instance**: Phiên bản n8n hỗ trợ LangChain Agents (khuyến nghị bản mới nhất).
- **Groq API Key**: Tài khoản và API key để kết nối với model `llama-3.3-70b-versatile`.
- **Google Cloud Platform (GCP)**: 
  - Dự án GCP đã bật **Veo 3 API / Vertex AI API** (Model Garden → Veo).
  - Credentials dạng **Google Service Account** (cần có quyền Vertex AI User).
- **Google Sheets & Google Drive**: Tài khoản Google có quyền truy cập Drive và Sheets để cấu hình OAuth2 Credentials.
:::

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Copy mã JSON của workflow từ nguồn gốc hoặc tải file JSON về máy.
- Mở n8n Editor, chọn **Add workflow** -> Nhấn vào menu ba chấm (...) ở góc trên bên phải -> Chọn **Import from File** hoặc dán trực tiếp JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node sau:

* **Groq AI Model**:
  - Kết nối **Groq API Credentials** của các sếp.
  - Đảm bảo model được chọn là `llama-3.3-70b-versatile`.
* **Append Content to Sheet & Update Sheet with URL (Google Sheets)**:
  - Kết nối **Google Sheets OAuth2** credentials.
  - Tạo sẵn một Google Sheet với các cột bắt buộc: `Idea`, `Captions`, `Environment`, `Status`, `Prompt`, `Video URL`.
  - Thay thế Sheet ID mặc định trong các node Google Sheets bằng ID file của các sếp (lấy đoạn mã dài trên URL của Google Sheet).
* **Post to Veo 3 API & Poll Video Generation Status (HTTP Request)**:
  - Kết nối **Google Service Account** credentials (cần phân quyền Vertex AI User).
  - Thay thế chuỗi `YOUR_GCP_PROJECT_ID` trong URL của cả hai node này bằng Project ID thực tế trên Google Cloud của các sếp.
* **Upload File to Google Drive (Google Drive)**:
  - Kết nối **Google Drive OAuth2** credentials.
  - Lấy Folder ID từ thư mục chứa video trên Google Drive của các sếp và dán vào node này.

#### 3. Kích hoạt ⚡️
- Chạy thử (Test run) bằng cách submit thử một form mẫu để kiểm tra từ bước sinh prompt cho đến khi nhận được link video trên Google Drive.
- Sau khi test thành công, gạt nút **Active** ở góc trên bên phải để bật workflow chạy tự động 24/7.

---

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo qua Telegram / Slack**: Thêm một node Telegram hoặc Slack ngay sau node `Update Sheet with URL` để gửi thông báo kèm link video trực tiếp cho sếp hoặc team khi video render xong.
- **Mở rộng nguồn input**: Thay vì dùng Form Trigger mặc định của n8n, các sếp có thể đổi thành Webhook nhận dữ liệu từ Typeform, Airtable hoặc Google Forms.
- **Tối ưu thời gian chờ**: Nếu video Veo 3 mất nhiều thời gian hơn, có thể điều chỉnh thời gian trong các node `Wait` cho phù hợp với dung lượng và độ phức tạp của video.

---

### 📌 Kết luận
Workflow tạo video ngắn tự động sử dụng Groq và Veo 3 này là một trợ thủ đắc lực giúp tối ưu hóa quy trình sản xuất nội dung đa phương tiện cho các nhà sáng tạo và doanh nghiệp. Hãy áp dụng ngay để tiết kiệm hàng giờ đồng hồ làm việc thủ công mỗi ngày! Chúc các sếp cài đặt thành công!