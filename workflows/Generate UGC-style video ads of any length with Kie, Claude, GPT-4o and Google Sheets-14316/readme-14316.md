---
title: "🚀 Tự động hóa sản xuất video quảng cáo UGC không giới hạn với n8n, Claude, GPT-4o và Google Sheets"
description: "Xây dựng hệ thống tự động hóa toàn diện quy trình tạo video quảng cáo phong cách UGC từ Google Sheets sử dụng AI đa phương thức: tạo ảnh tham chiếu, phân tích ngữ cảnh, sinh kịch bản phân cảnh, tạo video AI và ghép nối hoàn chỉnh."
slug: "tu-dong-hoa-san-xuat-video-ugc-ai-n8n-google-sheets"
tags: [n8n, automation, ai-video, content-creation, google-sheets, openrouter]
keywords: [n8n workflow, tạo video quảng cáo ugc, ai video generator, google sheets n8n, claude opus, fal.ai ffmpeg]
---

# 🚀 Tự động hóa sản xuất video quảng cáo UGC không giới hạn với AI

Các sếp có đang đau đầu vì tốn quá nhiều thời gian, nhân lực và chi phí để sản xuất hàng loạt video quảng cáo dạng UGC (User Generated Content) cho các chiến dịch marketing? Việc lên kịch bản, tạo hình ảnh, dựng cảnh và ghép nối video thủ công cực kỳ tốn kém và khó mở rộng quy mô.

Giải pháp đây rồi! Workflow n8n mạnh mẽ này sẽ tự động hóa **100% quy trình sản xuất video quảng cáo UGC** từ A-Z. Chỉ cần nhập ý tưởng vào Google Sheets, hệ thống sẽ tự động gọi các mô hình AI đỉnh cao (Claude Opus, GPT-4o, Kie, fal.ai) để tạo ra các phân cảnh, sinh video AI, ghép nối (stitch) thành video hoàn chỉnh và trả lại link thành phẩm ngay lập tức cho các sếp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Biến dòng ý tưởng thô trong Google Sheets thành video quảng cáo hoàn thiện mà không cần can thiệp thủ công.
- **Đồng bộ hình ảnh & ngữ cảnh:** AI phân tích ảnh tham chiếu (`Analyze UGC Image3`) giúp giữ vững nhân vật và phong cách xuyên suốt các phân cảnh.
- **Kịch bản chuẩn xác theo thời lượng:** Tự động chia kịch bản thành các phân cảnh 8 giây với lời thoại và hướng dẫn chuyển động chi tiết nhờ sức mạnh của Claude Opus.
- **Ghép nối video chuyên nghiệp:** Sử dụng fal.ai FFmpeg (`Generate media using AI model1`) để tự động tổng hợp và merge các clip nhỏ thành một video quảng cáo hoàn chỉnh, lưu trữ an toàn trên Google Drive.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và credentials sau trong n8n:
- **Google Sheets & Google Drive:** Tài khoản kết nối để đọc/ghi dữ liệu chiến dịch và lưu trữ file video/hình ảnh.
- **OpenRouter / Anthropic:** API key để sử dụng mô hình Claude Opus cho việc lên kịch bản (`Script Agent LLM`, `Prompt Agent LLM`).
- **OpenAI:** API key cho GPT-4o dùng để phân tích hình ảnh (`Analyze UGC Image3`).
- **Kie & fal.ai:** Tài khoản và API/Credentials để tạo ảnh tham chiếu và ghép nối video (`Generate media using AI model1`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy trực tiếp mã nguồn.
- Mở giao diện n8n Editor, chọn **Add workflow** -> **Import from File** (hoặc dán trực tiếp vào canvas).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Vì workflow này gồm tới 55 nodes xử lý đa tầng, các sếp cần chú ý cấu hình kỹ các điểm sau:
- **Google Sheets Nodes (`Get Video Ideas`, `UpdateSheet`, v.v.):** Trỏ đúng vào file Google Sheet quản lý chiến dịch của các sếp. Đảm bảo tên cột khớp với mapping: cột kích hoạt (`LAUNCH CREATION` với giá trị `Create`), `VIDEO ID`, `SCENE NO`, `SCRIPT`,...
- **Google Drive Nodes (`Upload file`, `Upload file1`, `Upload file2`):** Cấu hình chính xác ID thư mục đích (Folder ID) trên Google Drive để hệ thống tự động lưu trữ hình ảnh tham chiếu, các clip phân cảnh và video hoàn thiện.
- **AI Nodes (`Prompt Agent LLM`, `Script Agent LLM`, `Analyze UGC Image3`):** Kiểm tra lại các credential liên kết với OpenRouter và OpenAI, đảm bảo model đã được chọn đúng như `anthropic/claude-opus-4.5`.
- **Fal.ai Node (`Generate media using AI model1`):** Đảm bảo credential kết nối fal.ai hợp lệ để tiến hành merge các video clip qua FFmpeg API (`fal-ai/ffmpeg-api/merge-videos`).

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (`Test workflow`) với một hàng dữ liệu mẫu trên Google Sheets để kiểm tra toàn bộ luồng từ tạo ảnh đến ghép video.
- Sau khi test thành công, bật trạng thái **Active** để hệ thống tự động chạy theo lịch trình hoặc sự kiện kích hoạt.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Thêm node Telegram hoặc Slack ở cuối workflow để bắn thông báo ngay về máy cho team khi video được render xong.
- **Quản lý lỗi tự động:** Tận dụng các node `stopAndError` và `Switch` sẵn có để cấu hình gửi email cảnh báo nếu quá trình sinh ảnh hoặc video gặp lỗi do hết hạn mức API.
- **Tùy biến thời lượng:** Tinh chỉnh prompt trong các agent LLM nếu các sếp muốn thay đổi độ dài mỗi phân cảnh (thay vì mặc định 8 giây).

### 📌 Kết luận
Workflow "UGC Ads Factory" là một cỗ máy tự động hóa cực kỳ mạnh mẽ giúp các doanh nghiệp, agency marketing scale-up chiến dịch quảng cáo video với chi phí tối thiểu và tốc độ tối đa. Hãy triển khai ngay hôm nay để tối ưu hóa hiệu suất làm việc cho team nội dung của các sếp!