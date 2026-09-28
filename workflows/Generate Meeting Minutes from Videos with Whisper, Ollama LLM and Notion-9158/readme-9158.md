---
title: "🚀 Tự Động Hóa Biên Bản Cuộc Họp Từ Video Bằng AI: Whisper, Ollama & Notion"
description: "Hướng dẫn chi tiết xây dựng workflow n8n tự động phát hiện video mới, chuyển đổi giọng nói thành văn bản bằng Whisper, tóm tắt thông minh với Ollama LLM và lưu trữ chuyên nghiệp vào Notion."
slug: "tu-dong-hoa-bien-ban-cuop-hop-whisper-ollama-notion"
tags: [n8n, automation, ai, notion, whisper, ollama, local-ai]
keywords: [n8n workflow, tóm tắt cuộc họp tự động, whisper ai, ollama llm, notion automation, speech to text]
keywords: [n8n workflow, tóm tắt cuộc họp tự động, whisper ai, ollama llm, notion automation, speech to text]
---

# 🚀 Tự Động Hóa Biên Bản Cuộc Họp Từ Video Bằng AI: Whisper, Ollama & Notion

Các sếp có bao giờ cảm thấy mệt mỏi sau mỗi buổi họp dài khi phải ngồi nghe lại video, ghi chép thủ công từng ý chính rồi lọ mọ soạn thành biên bản gửi cho team? Việc này không chỉ tốn hàng giờ đồng hồ mà còn dễ bỏ sót các action items quan trọng.

Đừng lo, trong bài viết này, tui sẽ hướng dẫn các sếp dựng một workflow n8n cực kỳ "xịn sò" được chia sẻ bởi chuyên gia Facundo Cabrera. Workflow này sẽ tự động hóa **100%** quy trình: Phát hiện video mới -> Xử lý file -> Chuyển giọng nói thành văn bản (Speech-to-Text bằng Whisper) -> Phân tích & tóm tắt thông minh bằng AI cục bộ (Ollama) -> Đồng bộ trực tiếp lên Notion và gửi thông báo qua Discord!

:::info[Gợi ý hạ tầng cho n8n]
Vì workflow này chạy các tác vụ nặng như xử lý video, chạy mô hình Whisper và Ollama LLM cục bộ (Local AI), các sếp nên cài n8n trên VPS cấu hình cao để đảm bảo hiệu suất tốt nhất.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Chỉ cần ném file video vào thư mục (ví dụ thư mục quay màn hình OBS), phần còn lại để AI lo.
- **Bảo mật tuyệt đối với Local AI:** Sử dụng Whisper để transcribe và Ollama LLM (chạy local) để tóm tắt, dữ liệu cuộc họp không bị lộ ra các API bên ngoài.
- **Tổ chức khoa học trên Notion:** Tự động tạo trang mới, phân tách nội dung chi tiết kèm timestamp và gắn link video trên Google Drive.
- **Thông báo nhanh chóng:** Gửi cảnh báo/thông báo qua Discord ngay khi biên bản sẵn sàng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Hỗ trợ tính năng chạy lệnh hệ thống (`Execute Command`) và Local File Trigger (Self-hosted n8n).
- **Công cụ dòng lệnh trên Server:** `ffmpeg`, `ffprobe`, và Python 3 kèm thư viện `whisper`.
- **Ollama:** Đã cài đặt Ollama trên server chạy n8n với model mong muốn (ví dụ: `gpt-oss:20b`).
- **Tài khoản & API Credentials:** 
  - Notion API Integration (có quyền truy cập Database/Pages).
  - Google Drive OAuth2 API (để lưu trữ bản backup video).
  - Discord Webhook (tùy chọn nhận thông báo).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow và paste trực tiếp vào n8n Editor của mình, hoặc import file JSON tải từ nguồn chính thức.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 22 nodes kết hợp giữa n8n thuần và các script thực thi ngoài. Các sếp cần chú ý các điểm cốt lõi sau:

- **Node `File` (Local File Trigger):** Cấu hình lại đường dẫn thư mục `path` (mặc định trong code là `G:\OBS\videos` hoặc thư mục trên VPS của các sếp) nơi lưu các video cuộc họp mới.
- **Node `Wait` & Script `wait-for-file.ps1` / Shell tương đương:** Đảm bảo hệ thống đợi file copy hoàn tất (không bị khóa file) trước khi xử lý.
- **Node `Create Wav` & `Transcribe Local` (Execute Command):** Các node này gọi script Python (`create_wav.py` và `transcribe_return.py`). Các sếp cần đảm bảo trên môi trường chạy n8n đã cài đặt sẵn Python, thư viện OpenAI Whisper và công cụ `ffmpeg`.
- **Node `gpt-oss 4090` (lmOllama):** Kết nối tới instance Ollama của các sếp, chọn đúng Model (ví dụ: `gpt-oss:20b` hoặc model tương ứng đã tải về).
- **Node `Create a page` & `Append a block` (Notion):** Chọn đúng Credentials Notion, kết nối với Database hoặc Trang đích để hệ thống tự động đổ dữ liệu biên bản họp vào.
- **Node `Upload video file` & `Create sub-folder` (Google Drive):** Cấu hình Google Drive OAuth2 để tự động tạo thư mục và upload video gốc lên mây.
- **Node `Discord`:** Dán Webhook URL của channel muốn nhận thông báo hoàn thành.

#### 3. Kích hoạt ⚡️
- Bỏ file video mẫu vào thư mục nguồn để chạy thử (Test run) kiểm tra từng bước từ convert âm thanh -> transcribe -> AI tóm tắt -> đẩy lên Notion.
- Nếu mọi thứ mượt mà, bật **Active workflow** để hệ thống tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Thay vì chỉ dùng Discord, các sếp có thể nối thêm node Telegram hoặc Slack để gửi bản tóm tắt họp trực tiếp vào group chat của team.
- **Tùy biến Prompt AI:** Trong node `Create Notes` (chainLlm), các sếp có thể tinh chỉnh lại System Prompt để Ollama xuất ra biên bản theo đúng văn phong, cấu trúc công ty mong muốn (ví dụ: thêm phần Phân công công việc - Action Items rõ ràng).
- **Quản lý dung lượng:** Thiết lập thêm bước tự động xóa hoặc nén file video gốc trên VPS sau khi đã upload thành công lên Google Drive để tiết kiệm ổ cứng.

### 📌 Kết luận
Với workflow n8n kết hợp sức mạnh của Whisper, Ollama và Notion này, việc tổng hợp biên bản cuộc họp giờ đây chỉ là chuyện "muỗi". Hãy cài đặt ngay để giải phóng bản thân và đội ngũ khỏi những công việc hành chính thủ công nhàm chán nhé các sếp!