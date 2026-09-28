---
title: "🚀 Tự Động Phân Tích Phỏng Vấn UX: Transcribe & Xuất Kết Quả Lên Google Sheets"
description: "Workflow n8n giúp tự động chuyển đổi file âm thanh phỏng vấn UX thành văn bản, tóm tắt thông tin quan trọng và xuất trực tiếp lên Google Sheets bằng OpenAI."
slug: "tu-dong-phan-tich-phong-van-ux-n8n"
tags: [n8n, automation, no-code, ux-research, openai, google-sheets]
keywords: [n8n workflow, tự động hóa phỏng vấn, transcribe audio, phân tích UX, google sheets automation]
---

# 🚀 Tự Động Phân Tích Phỏng Vấn UX: Transcribe & Xuất Kết Quả Lên Google Sheets

Trong lĩnh vực nghiên cứu người dùng (UX Research), việc xử lý dữ liệu phỏng vấn thường là một "núi" công việc khổng lồ. Các sếp phải nghe lại hàng giờ đồng hồ âm thanh, gõ lại từng lời thoại (transcribe), rồi ngồi phân tích để tìm ra insight, pain points hay nhu cầu của người dùng. Quy trình thủ công này không chỉ tốn thời gian mà còn dễ bỏ sót chi tiết quan trọng do mệt mỏi.

Workflow này chính là giải pháp "cứu tinh" giúp các sếp tự động hóa 100% quy trình từ lúc có file âm thanh đến khi có bảng báo cáo insight trên Google Sheets. Chỉ cần upload file MP3 lên Google Drive, hệ thống sẽ tự động sử dụng OpenAI để chuyển giọng nói thành văn bản, phân tích nội dung và trích xuất các thông tin cốt lõi (Persona, User Needs, Pain Points, Feature Requests) vào bảng tính một cách chính xác và nhanh chóng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, đặc biệt khi xử lý các file audio dung lượng lớn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian khổng lồ**: Biến hàng giờ nghe và gõ lại thành vài phút chờ đợi tự động.
- **Độ chính xác cao**: OpenAI đảm bảo việc transcribe và tóm tắt dựa trên ngữ cảnh, giảm thiểu sai sót do con người.
- **Cấu trúc hóa dữ liệu**: Tự động tách biệt Persona, Nhu cầu, Điểm đau và Đề xuất tính năng vào các cột riêng biệt trên Google Sheets.
- **Quy trình liền mạch**: Kết nối trực tiếp từ Google Drive (nơi lưu file) đến Google Sheets (nơi lưu kết quả), không cần can thiệp thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản n8n**: Đã cài đặt và chạy (Cloud hoặc Self-hosted).
2. **Tài khoản OpenAI**: Cần API Key để sử dụng cho việc Transcribe (Whisper) và Chat (GPT-4.1-mini).
3. **Tài khoản Google**:
   - **Google Drive**: Nơi lưu trữ các file âm thanh phỏng vấn (định dạng MP3).
   - **Google Sheets**: Nơi lưu trữ kết quả phân tích.
4. **File âm thanh**: Các file phỏng vấn ở định dạng `.mp3` (có thể chỉnh sửa để hỗ trợ định dạng khác).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể import workflow theo 2 cách:
- **Cách 1 (Khuyến nghị)**: Tải file JSON của workflow về máy, sau đó vào n8n chọn `Import from File`.
- **Cách 2**: Copy toàn bộ mã JSON của workflow và dán vào n8n Editor (chọn `Import from Clipboard`).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình các node sau để workflow hoạt động đúng:

1. **Node: Search Google Drive for interview files**
   - Chọn **Credentials**: Chọn hoặc tạo credential `googleDriveOAuth2Api`.
   - **Folder ID**: Điền ID của thư mục trên Google Drive chứa các file phỏng vấn.
     *Mẹo: Mở thư mục trên Drive, nhìn vào URL, phần sau `/folders/` chính là Folder ID.*

2. **Node: Filter by .mp3**
   - Node này mặc định lọc file `.mp3`. Nếu các sếp dùng định dạng khác (ví dụ: `.wav`, `.m4a`), hãy chỉnh sửa điều kiện lọc trong node này.

3. **Node: Download audio file**
   - Chọn **Credentials**: Cùng credential `googleDriveOAuth2Api` ở trên.
   - Node này sẽ tự động tải file audio từ Drive về để xử lý.

4. **Node: Transcribe a recording**
   - Chọn **Credentials**: Chọn hoặc tạo credential `openAiApi`.
   - **Model**: Mặc định là `whisper-1`. Các sếp có thể giữ nguyên hoặc chọn model khác nếu có.
   - **Language**: Có thể để trống để OpenAI tự nhận diện ngôn ngữ, hoặc chọn `vi` nếu phỏng vấn bằng tiếng Việt để tăng độ chính xác.

5. **Node: AI Agent for creating transcript**
   - Đây là node trung tâm xử lý logic.
   - **Model**: Node `OpenAI Chat Model` gắn vào đây đang sử dụng `gpt-4.1-mini`. Các sếp có thể đổi sang `gpt-4o` hoặc `gpt-4-turbo` nếu cần độ chính xác cao hơn (chi phí sẽ tăng).
   - **Prompt/System Message**: Kiểm tra prompt trong node này. Nó hướng dẫn AI trích xuất 4 trường: Persona, User Needs, Pain Points, New Feature Requests. Các sếp có thể tùy chỉnh prompt này nếu muốn thêm các trường phân tích khác.

6. **Node: Insert results to Google Sheets**
   - Chọn **Credentials**: Chọn hoặc tạo credential `googleSheetsOAuth2Api`.
   - **Document ID**: Điền ID của Google Sheet mà các sếp đã tạo.
   - **Sheet Name**: Tên sheet (ví dụ: `Sheet1`).
   - **Lưu ý quan trọng**: Google Sheet cần có đúng 4 cột tiêu đề sau (theo thứ tự hoặc tên khớp với output của AI):
     1. `Persona`
     2. `User Needs`
     3. `Pain Points`
     4. `New Feature Requests`

#### 3. Kích hoạt ⚡️
1. **Test Run**:
   - Upload 1 file MP3 mẫu vào thư mục Google Drive đã cấu hình.
   - Nhấn nút `Execute Workflow` (hoặc `Test`) trong n8n.
   - Kiểm tra xem file có được tải xuống, transcribe thành công và dữ liệu có xuất hiện trên Google Sheets không.
2. **Bật Active**:
   - Nếu test thành công, bật công tắc `Active` ở góc trên bên phải n8n.
   - *Lưu ý*: Workflow này dùng `Manual Trigger`, nên các sếp sẽ phải nhấn nút chạy thủ công mỗi khi có file mới. Nếu muốn tự động chạy khi có file mới, các sếp có thể thay thế node `Manual Trigger` bằng `Google Drive Trigger` (nếu n8n hỗ trợ webhook cho Drive) hoặc dùng Cron Job.

### ✍️ Mẹo & gợi ý nâng cao
- **Hỗ trợ đa ngôn ngữ**: Trong node `Transcribe a recording`, hãy thử nghiệm việc để trống trường Language để OpenAI tự phát hiện ngôn ngữ, đặc biệt hữu ích nếu phỏng vấn xen kẽ tiếng Anh và tiếng Việt.
- **Tùy chỉnh Prompt**: Trong node `AI Agent`, các sếp có thể yêu cầu AI đánh giá mức độ hài lòng (1-5 sao) hoặc phân loại mức độ ưu tiên của pain points (High/Medium/Low) để làm phong phú thêm dữ liệu trên Sheet.
- **Tự động hóa hoàn toàn**: Thay vì `Manual Trigger`, hãy nghiên cứu cách kết nối `Google Drive Trigger` (nếu dùng n8n cloud có hỗ trợ) hoặc dùng `Cron` để quét thư mục Drive mỗi 15 phút, phát hiện file mới và tự động chạy.
- **Gửi báo cáo qua Email/Slack**: Sau node `Insert results to Google Sheets`, các sếp có thể thêm node `Send Email` hoặc `Slack` để gửi thông báo "Đã hoàn thành phân tích phỏng vấn với [Tên File]" kèm link đến Google Sheet.

### 📌 Kết luận
Workflow này là công cụ đắc lực giúp các team UX Research và Product Manager tiết kiệm hàng chục giờ làm việc thủ công mỗi tháng. Bằng cách kết hợp sức mạnh của OpenAI và hệ sinh thái Google, các sếp có thể tập trung vào việc phân tích insight sâu hơn thay vì mất thời gian cho các tác vụ hành chính như gõ lại lời thoại. Hãy thử ngay workflow này để trải nghiệm sự khác biệt trong quy trình nghiên cứu người dùng của mình!