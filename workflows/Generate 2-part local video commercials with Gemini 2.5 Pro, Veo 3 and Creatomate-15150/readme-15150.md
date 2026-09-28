---
title: "🚀 Tự động tạo Video Quảng cáo Địa phương 2 phần bằng Gemini, Veo và Creatomate trong n8n"
description: "Hướng dẫn xây dựng workflow n8n cực đỉnh giúp tự động lên chiến lược, tạo video AI bằng Google Veo, xử lý đa phương thức với Gemini và dựng phim tự động qua Creatomate, gửi trực tiếp về Telegram."
slug: "tu-dong-tao-video-quang-cao-dia-phuong-gemini-veo-creatomate"
tags: [n8n, automation, ai-video, gemini, google-veo, creatomate]
keywords: [n8n workflow, tạo video AI tự động, Google Veo, Gemini AI, Creatomate, tự động hóa marketing]
---

# 🚀 Tự động tạo Video Quảng cáo Địa phương 2 phần bằng Gemini, Veo và Creatomate

Việc sản xuất video quảng cáo (đặc biệt là video ngắn đa phần gồm nhiều phần cho các doanh nghiệp địa phương) thường tốn rất nhiều thời gian, chi phí thuêagency và công sức lên kịch bản, dựng hình. Các sếp có bao giờ nghĩ đến việc chỉ cần nhập thông tin cơ bản về doanh nghiệp, hệ thống sẽ tự động lên chiến lược, sinh kịch bản, tạo video AI, ghép nối chuyên nghiệp và bắn thẳng kết quả về Telegram chưa?

Workflow siêu khủng với 43 nodes này do tác giả **Koulikas Giannis** (Founder & CEO tại Coreflow Automation) xây dựng sẽ giúp các sếp giải quyết trọn gói bài toán này hoàn toàn tự động bằng sức mạnh của AI đa phương thức (Gemini, DeepSeek, Google Veo và Creatomate).

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và xử lý các tập tin video nặng, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100% quy trình sáng tạo:** Từ khâu lên ý tưởng, chiến lược quảng cáo, sinh video từng phần cho đến hậu kỳ dựng phim.
- **Ứng dụng AI đỉnh cao:** Kết hợp nhịp nhàng giữa Gemini (Google AI), DeepSeek và Google Veo để tạo ra các thước phim chất lượng cao, đúng insight khách hàng.
- **Tiết kiệm chi phí nhân sự & thời gian:** Thay vì mất hàng tuần, hệ thống chỉ mất vài phút để hoàn thiện một video quảng cáo hoàn chỉnh.
- **Nhận kết quả tức thì:** Video sau khi render xong sẽ được tự động gửi qua **Telegram** để các sếp kiểm tra và tải xuống ngay lập tức.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API Keys sau:
- **n8n instance** (phiên bản mới tích hợp LangChain nodes).
- **Google Gemini API Key** (cho các node Gemini Chat Model và phân tích video).
- **DeepSeek API Key** (cho các chuỗi xử lý logic, cấu trúc dữ liệu).
- **Google Cloud Platform (GCP) / Google Drive / Google Cloud Storage** (để lưu trữ và xử lý video trung gian).
- **Creatomate API Key** (để thực hiện render và ghép nối video).
- **Telegram Bot Token** (để nhận thông báo và video trả về).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy toàn bộ mã nguồn JSON từ nguồn cấp.
- Trong giao diện n8n Editor, chọn **Add workflow** -> Nhấp vào biểu tượng 3 chấm ở góc trên bên phải -> Chọn **Import from File** hoặc dán trực tiếp JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Do workflow có cấu trúc phức tạp với 43 nodes, các sếp cần chú ý cấu hình kỹ các nhóm node cốt lõi sau:
- **Set Business Details:** Điền thông tin chi tiết về doanh nghiệp địa phương của các sếp (tên, lĩnh vực, dịch vụ, tệp khách hàng...) để làm đầu vào cho AI lên kịch bản.
- **Nhóm LLM Models (`Gemini Chat Model 1/2/3`, `DeepSeek Chat Model 1/2/3`):** Thiết lập Credentials cho Google Gemini và DeepSeek để các chuỗi `Ad Planning Chain`, `Ad Strategy Chain Part 1 & 2` hoạt động trơn tru.
- **Nhóm Google Drive & Google Cloud Storage (`Upload Vid to Google Drive`, `GCS Video Part 1 & 2`):** Kết nối tài khoản Google Cloud và Google Drive để hệ thống tải lên, lưu trữ và gọi lại các tệp video phần 1, phần 2 phục vụ cho việc kiểm tra chất lượng.
- **Nhóm HTTP Request & JWT (`Generate JWT Token`, `Post Generate Video`, `Post Merge to Creatomate`):** Điền chính xác API Keys và endpoint của dịch vụ tạo video (Google Veo) và công cụ dựng hình Creatomate.
- **Telegram Send Video:** Cấu hình **Chat ID** và **Bot Token** của Telegram để hệ thống biết nơi gửi video hoàn thiện về cho các sếp.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** tại node `When Execute Workflow Clicked` để chạy thử với dữ liệu mẫu.
- Kiểm tra kỹ các vòng lặp chờ (`Wait 20 Seconds`, `Wait for Rendering Complete`) xem thờigian phản hồi từ các API video đã chuẩn xác chưa.
- Sau khi test thành công, gạt công tắc sang **Active** để chính thức vận hành hệ thống tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Google Sheets:** Thay vì dùng node `Set Business Details` thủ công, các sếp có thể kết nối với Google Sheets để nhập danh sách hàng loạt doanh nghiệp và chạy chiến dịch video hàng loạt (Batch Processing).
- **Lưu lịch sử vào Airtable/Notion:** Thêm các node lưu trữ thông tin kịch bản và link video vào cơ sở dữ liệu để dễ dàng quản lý kho content quảng cáo.
- **Mở rộng kênh thông báo:** Ngoài Telegram, có thể kết nối thêm Slack hoặc Email để gửi báo cáo cho team Marketing ngay khi video được xuất bản.

### 📌 Kết luận
Workflow này là một "vũ khí tối thượng" cho các Agency hoặc nhà làm Marketing hiện đại muốn tận dụng sức mạnh của Generative AI để sản xuất video quy mô lớn. Hãy cài đặt ngay lên VPS của các sếp và bắt đầu tạo ra những chiến dịch video triệu view một cách tự động!