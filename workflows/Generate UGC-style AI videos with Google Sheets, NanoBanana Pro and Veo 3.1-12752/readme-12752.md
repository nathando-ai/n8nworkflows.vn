---
title: "🚀 Tự động hóa tạo video UGC chân thực với Google Sheets, NanoBanana Pro và Veo 3.1"
description: "Hướng dẫn xây dựng workflow n8n tự động kết hợp hình ảnh sản phẩm, nhân vật và phông nền thành ảnh UGC chân thực rồi biến chúng thành video AI đỉnh cao."
slug: "tao-video-ugc-tu-dong-google-sheets-nanobanana-veo"
tags: [n8n, automation, ai-video, ugc, google-sheets, content-creation]
keywords: [n8n workflow, tao video ugc, google sheets ai, nanobanana pro, veo 3.1, tu dong hoa content]
---

# 🚀 Tự động hóa tạo video UGC chân thực với Google Sheets, NanoBanana Pro và Veo 3.1

Việc sản xuất hàng loạt video UGC (User Generated Content) hay các nội dung quảng cáo ngắn cho TikTok Reels, YouTube Shorts và Instagram thường ngốn rất nhiều thời gian của các nhà sáng tạo nội dung và đội ngũ marketing. Bạn phải loay hoay ghép ảnh sản phẩm, tìm kiếm người mẫu, tạo bối cảnh rồi dựng phim thủ công. 

Workflow n8n này do tác giả **Kristian Ekachandra** thiết kế sẽ giải quyết hoàn toàn bài toán trên bằng cách tự động hóa 100%: Lấy dữ liệu từ Google Sheets, kết hợp 3 hình ảnh riêng biệt (Sản phẩm + Nhân vật + Phông nền) thông qua **NanoBanana Pro**, phân tích bằng AI Agents, và cuối cùng xuất ra các video chất lượng cao dài 8 giây bằng công nghệ **Veo 3.1** mà không cần đụng tay viết code phức tạp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn quy trình làm nội dung:** Biến dữ liệu thô trong Google Sheets thành ảnh UGC và video hoàn chỉnh.
- **Kết hợp thông minh đa thành phần:** Tự động ghép 3 ảnh (Product, Character, Background) thành một bức ảnh selfie UGC cực kỳ chân thực.
- **Tích hợp AI tiên tiến:** Sử dụng các AI Agent mạnh mẽ (OpenAI, Groq) để tạo prompt hình ảnh và video tự động.
- **Hoạt động liên tục:** Sử dụng `Schedule Trigger` để định kỳ xử lý hàng loạt tác vụ mà không cần giám sát thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt sẵn sàng (Cloud hoặc Self-hosted).
- **Google Sheets Credentials:** Tài khoản OAuth2 để kết nối và đọc/ghi dữ liệu bảng tính.
- **AI API Keys:** 
  - OpenAI API Key (cho node GPT-5-Mini và Analyze Image)
  - Hoặc Groq API Key (cho node GPT-OSS-120b)
- **Atlas Cloud API Key:** Tài khoản tại [Atlas Cloud](https://goto.atlascloud.ai/Kristian?ref=TM2L4K) để sử dụng các node `NanoBanana Pro Edit` và `Veo 3.1`.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow hoặc copy trực tiếp mã nguồn workflow từ n8n.io và paste vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình kỹ các phần sau để workflow chạy mượt mà:
- **Google Sheets Template:** 
  1. [Copy Google Sheets Template tại đây](https://docs.google.com/spreadsheets/d/1wVz-tvvAuYi9sHtHj40i4yeOFZMbdwmuaQR5N5wRg08/copy)
  2. Cập nhật lại Link Google Sheets trong tất cả các node liên quan như `Get Ready Task`, `Get Edited Task`, `Update Edit Task [SUCCESS/ERROR]`, `Update Video Task [SUCCESS/ERROR]`.
- **Credentials:**
  - Kết nối **Google Sheets OAuth2 API** cho các node Google Sheets.
  - Thêm **OpenAI API Key** hoặc **Groq API Key** cho các LLM Nodes (`GPT-5-Mini`, `GPT-OSS-120b`, `Analyze image`).
  - Thêm **Bearer Token (Atlas Cloud API Key)** vào phần Credentials của các node `NanoBanana Pro Edit`, `Veo 3.1`, và `Get a Video`.

#### 3. Kích hoạt ⚡️
- **Test chạy thử phần ảnh:** Thêm một dòng tác vụ mới vào Google Sheets với trạng thái (`Status`) là "Ready". Bấm nút chạy thủ công node `Schedule Trigger Edit Images` để kiểm tra kết quả trả về cột Image Result.
- **Test chạy thử phần video:** Sau khi ảnh đã được chỉnh sửa xong, chạy thủ công node `Schedule Trigger Make Videos` để tạo video AI.
- Sau khi test thành công, các sếp chỉ cần bật **Active** workflow để hệ thống tự động chạy theo lịch trình.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo Telegram/Slack:** Thêm một node Telegram sau các node `Update Video Task [SUCCESS]` để nhận thông báo trực tiếp khi video được tạo xong.
- **Tự động hóa đăng bài:** Kết nối thêm các API của TikTok hoặc Instagram để tự động xuất bản video ngay sau khi hoàn thành.
- **Mở rộng kho lưu trữ:** Thay vì chỉ lưu link trên Google Sheets, các sếp có thể cấu hình đẩy trực tiếp file video/ảnh về Google Drive hoặc AWS S3 để lưu trữ lâu dài.

### 📌 Kết luận
Workflow này là một "vũ khí tối thượng" cho các nhà sáng tạo nội dung, giúp tiết kiệm hàng chục giờ làm việc thủ công mỗi tuần. Hãy thiết lập ngay hôm nay để tự động hóa hoàn toàn dây chuyền sản xuất video UGC của doanh nghiệp các sếp nhé!