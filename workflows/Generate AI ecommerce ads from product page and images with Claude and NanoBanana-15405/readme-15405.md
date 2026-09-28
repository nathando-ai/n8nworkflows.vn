---
title: "🚀 Tự Động Tạo Quảng Cáo Thương Mại Điện Tử Bằng AI Từ Trang Sản Phẩm Và Hình Ảnh"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa hoàn toàn việc tạo nội dung và hình ảnh quảng cáo ecommerce chuyên nghiệp bằng Claude AI và NanoBanana."
slug: "tao-quang-cao-ecommerce-tu-dong-voi-claude-va-nanobanana-n8n"
tags: [n8n, automation, ai, claude, ecommerce, openrouter]
keywords: [n8n workflow, tạo quảng cáo tự động, claude sonnet, nanobanana, openrouter, ai marketing]
---

# 🚀 Tự Động Tạo Quảng Cáo Thương Mại Điện Tử Bằng AI Từ Trang Sản Phẩm Và Hình Ảnh

Việc thiết kế và viết nội dung quảng cáo cho các sản phẩm thương mại điện tử (e-commerce) thường tốn rất nhiều thời gian của các nhàω marketing. Từ việc nghiên cứu trang sản phẩm, viết copy chuẩn sale cho đến thiết kế hình ảnh bắt mắt. Workflow n8n này sẽ giải quyết triệt để nỗi đau đó bằng cách tự động hóa 100% quy trình: Nhận diện URL sản phẩm, phân tích hình ảnh, viết nội dung content sắc bén và tạo hình ảnh quảng cáo hoàn chỉnh nhờ sức mạnh của **Claude AI** và **NanoBanana** qua **OpenRouter**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Chuyển đổi một URL sản phẩm, logo và ảnh gốc thành một mẫu quảng cáo hoàn chỉnh chỉ trong vài phút.
- **Hiểu sâu về sản phẩm:** Trích xuất thông tin chi tiết từ trang web, kết hợp phân tích hình ảnh đa phương thức (multimodal) để quảng cáo không bị chung chung.
- **Nội dung chuẩn chiến lược:** Tự động tạo tiêu đề, thông điệp chính, microcopy, nút kêu gọi hành động (CTA) và định hướng hình ảnh rõ ràng.
- **Đa kênh & Lưu trữ thông minh:** Tự động tạo file ảnh kết quả và lưu trữ trực tiếp lên Google Drive (tùy chọn).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Phiên bản khuyến nghị mới nhất hỗ trợ LangChain nodes).
- **Anthropic API Credentials:** Dùng cho các node `Anthropic Chat Model` (Sử dụng model `Claude Sonnet 4.5`).
- **OpenRouter API Credentials:** Dùng cho các node `Call Claude - Photo Evaluation` và `Generate Ad Image` (NanoBanana).
- **Google Drive OAuth2 API:** (Tùy chọn) Dùng nếu muốn tự động lưu file quảng cáo xuất ra vào Drive.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này hoặc copy đoạn mã JSON, sau đó paste trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Form Input (`Form Input`):** Node khởi chạy giao diện để người dùng nhập URL sản phẩm, tải lên Logo và Ảnh sản phẩm gốc (.jpg, .png, .webp).
- **Anthropic Chat Models (`Anthropic Chat Model1`, `Anthropic Chat Model2`, `Anthropic Chat Model3`):** Cần cấu hình kết nối tài khoản Anthropic API. Đảm bảo model được chọn là `claude-sonnet-4-5-20250929`.
- **API Call & Image Generation (`Call Claude - Photo Evaluation`, `Generate Ad Image`):** Cấu hình credentials cho OpenRouter để tiến hành phân tích ảnh sản phẩm và gọi model tạo ảnh quảng cáo (NanoBanana).
- **Google Drive (`Upload file`):** Chọn credentials Google Drive nếu muốn lưu ảnh quảng cáo. Nếu không cần xuất file lên Drive, các sếp có thể vô hiệu hóa node này.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và test thử bằng một URL sản phẩm thật cùng hình ảnh kèm theo để kiểm tra kết quả đầu ra.
- Sau khi kiểm tra mọi thứ hoạt động trơn tru, hãy chuyển trạng thái sang **Active** để đưa vào sử dụng thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Chatbot Telegram/Slack:** Thay vì xem kết quả thủ công trên form, các sếp có thể cấu hình để workflow tự động gửi mẫu quảng cáo hoàn thiện vào group Telegram hoặc Slack của team MKT.
- **Lưu trữ Google Sheets:** Thêm một node Google Sheets để lưu lại lịch sử các ad concept và link hình ảnh đã tạo để tiện theo dõi chiến dịch.
- **Mở rộng Đa ngôn ngữ:** Tinh chỉnh prompt trong các agent phân tích để tự động dịch và tạo nội dung quảng cáo bằng nhiều thứ tiếng khác nhau (Anh, Trung, Thái...).

### 📌 Kết luận
Workflow này là một cỗ máy tự động hóa hoàn hảo cho cácội ngũ e-commerce muốn scale-up số lượng nội dung quảng cáo mà vẫn đảm bảo tính độc đáo và chuyên nghiệp. Hãy áp dụng ngay vào hệ thống của các sếp để tối ưu hóa chi phí nhân sự và thời gian làm content!