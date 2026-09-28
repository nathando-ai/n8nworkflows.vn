---
title: "🚀 Tự động hóa Báo cáo Xu hướng YouTube bằng GPT-4o, Google Sheets và PDF.co"
description: "Hướng dẫn xây dựng workflow n8n tự động tổng hợp xu hướng YouTube với AI GPT-4o, lưu trữ vào Google Sheets và xuất bản báo cáo PDF chuyên nghiệp gửi qua Gmail."
slug: "tu-dong-hoa-bao-cao-xu-huong-youtube-gpt4o-pdfco"
tags: [n8n, automation, no-code, youtube, ai, gpt-4o, pdf.co, google-sheets]
keywords: [n8n workflow, tao bao cao youtube ai, gpt-4o n8n, pdf.co automation, tu dong hoa nghien cuu thi truong]
---

# 🚀 Tự động hóa Báo cáo Xu hướng YouTube với GPT-4o, Google Sheets và PDF.co

Việc nghiên cứu thị trường và cập nhật các xu hướng mới nhất trên YouTube thủ công ngốn của các sếp hàng giờ đồng hồ mỗi tuần. Chưa kể việc phải tổng hợp số liệu, viết báo cáo phân tích và thiết kế file PDF gửi sếp lớn hoặc đội ngũ marketing cực kỳ mất thời gian.

Với workflow n8n này, mọi quy trình từ quét dữ liệu, phân tích thông minh bằng AI cho đến xuất báo cáo PDF và gửi email sẽ được tự động hóa 100% mà không tốn một giọt mồ hôi. Giải pháp này giúp các sếp luôn dẫn đầu xu hướng thị trường một cách chuyên nghiệp và tiết kiệm tối đa nhân lực.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động 100%:** Lên lịch chạy định kỳ (Schedule Trigger) mà không cần can thiệp thủ công.
- **Phân tích thông minh:** Sử dụng sức mạnh của GPT-4o (@n8n/n8n-nodes-langchain.openAi) để cô đọng xu hướng, đưa ra insight đắt giá.
- **Lưu trữ bài bản:** Tự động ghi nhận toàn bộ dữ liệu phân tích vào Google Sheets để tiện theo dõi lịch sử.
- **Báo cáo chuyên nghiệp:** Biến dữ liệu thành file PDF đẹp mắt bằng PDF.co API và tự động gửi thẳng vào Gmail.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Self-hosted hoặc Cloud).
- **OpenAI API Key:** Tài khoản OpenAI có quyền truy cập mô hình GPT-4o.
- **Google Sheets:** Tài khoản Google để tạo bảng tính lưu dữ liệu xu hướng.
- **PDF.co Account:** Tài khoản PDF.co để xử lý việc tạo file PDF từ dữ liệu.
- **Gmail Account:** Cấu hình credentials Gmail để gửi báo cáo tự động.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ trang chủ n8n (Link gốc: [n8n Workflow #13659](https://n8n.io/workflows/13659)) hoặc copy đoạn JSON trực tiếp và dán vào màn hình làm việc của n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Khi import xong, các sếp cần cấu hình các node cốt lõi sau để hệ thống chạy mượt mà:
- **Schedule Trigger:** Thiết lập lịch chạy mong muốn (ví dụ: Chạy mỗi thứ Hai hàng tuần lúc 8:00 sáng).
- **OpenAI Node (@n8n/n8n-nodes-langchain.openAi):** Chọn đúng credential OpenAI và cấu hình Prompt cho GPT-4o để yêu cầu phân tích các xu hướng YouTube theo đúng định dạng mong muốn.
- **Google Sheets Node:** Kết nối tài khoản Google, chọn file bảng tính (Spreadsheet) và Sheet Name để lưu thông tin báo cáo.
- **PDF.co Api Node:** Nhấp vào node này, điền API Key từ tài khoản PDF.co của các sếp để hệ thống tiến hành convert nội dung thành file PDF hoàn chỉnh.
- **Gmail Node:** Kết nối tài khoản Gmail cá nhân hoặc của công ty để gửi email chứa file PDF báo cáo đến người nhận định sẵn.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Node** hoặc **Test workflow** trên từng bước để kiểm tra kết quả dữ liệu trả về (đặc biệt kiểm tra kỹ phần gọi API của OpenAI và PDF.co).
- Sau khi test thành công không báo lỗi, gạt công tắc **Active** ở góc trên bên phải để workflow tự động vận hành.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh thông báo:** Bổ sung thêm node Telegram hoặc Slack để bắn thông báo nhanh ngay khi báo cáo PDF được tạo thành công.
- **Mở rộng nguồn dữ liệu:** Kết hợp thêm các node HTTP Request để kéo thêm dữ liệu từ các nền tảng mạng xã hội khác trước khi đưa vào GPT-4o tổng hợp.
- **Lưu trữ Cloud:** Thay vì chỉ gửi Gmail, các sếp có thể cấu hình lưu tự động file PDF vào Google Drive hoặc OneDrive để làm thư viện tài liệu nghiên cứu.

### 📌 Kết luận
Workflow tự động hóa báo cáo xu hướng YouTube với GPT-4o và PDF.co là trợ thủ đắc lực cho các nhà sáng tạo nội dung, marketer và các đội ngũ B2B. Hãy cài đặt ngay hôm nay để tối ưu hóa thời gian nghiên cứu và nâng tầm chuyên nghiệp cho doanh nghiệp của các sếp!