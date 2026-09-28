---
title: "🚀 Tự động hóa sáng tạo và đăng bài LinkedIn với GPT-4o-mini, Gemini AI và Phê duyệt thủ công"
description: "Xây dựng hệ thống tự động hóa toàn diện bằng n8n giúp lên ý tưởng, viết nội dung bằng GPT-4o-mini, tạo hình ảnh bằng Google Gemini, kiểm duyệt qua Gmail và tự động đăng lên LinkedIn."
slug: "tu-dong-hoa-dang-bai-linkedin-gpt4o-gemini-n8n"
tags: [n8n, automation, linkedin, ai, openai, google-gemini, content-marketing]
keywords: [n8n workflow, tự động hóa linkedin, viết bài linkedin bằng ai, openai gpt-4o-mini, google gemini image, auto publish linkedin]
---

# 🚀 Tự động hóa toàn bộ quy trình đăng bài LinkedIn: Từ Ý tưởng đến Xuất bản với AI & Kiểm duyệt Người thật

Các sếp có đang cảm thấy mệt mỏi vì tốn quá nhiều thời gian lên ý tưởng, viết bài, thiết kế hình ảnh và đăng bài thủ công lên LinkedIn mỗi ngày? Việc duy trì sự hiện diện chuyên nghiệp trên mạng xã hội này đòi hỏi nguồn lực lớn nhưng lại dễ bị ngắt quãng do bận rộn.

Workflow n8n này chính là giải pháp tự động hóa 100% không cần code (No-code) giúp các sếp giải quyết triệt để bài toán trên. Hệ thống sẽ tự động lấy ý tưởng từ Google Sheets, sử dụng **GPT-4o-mini** để viết bài cuốn hút, nhờ **Google Gemini** vẽ ảnh minh họa, gửi email xin phê duyệt qua **Gmail**, và cuối cùng là **tự động đăng lên LinkedIn** ngay khi sếp bấm nút "Phê duyệt"!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 không lo bị gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian:** Không cần tự viết nội dung hay thiết kế ảnh thủ công cho từng bài đăng.
- **Kiểm soát tuyệt đối nội dung:** Hệ thống gửi email chờ phê duyệt trước khi đăng, đảm bảo không có nội dung lỗi xuất hiện trên trang cá nhân/doanh nghiệp.
- **Đa phương tiện ấn tượng:** Kết hợp hài hòa giữa bài viết chuẩn SEO/Social từ OpenAI và hình ảnh minh họa sinh động từ Google Gemini.
- **Đồng bộ dữ liệu tự động:** Google Sheets tự động cập nhật trạng thái (Completed/Canceled) và lưu lại link bài viết thực tế trên LinkedIn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Google Sheets:** File Google Sheets chứa danh sách ý tưởng bài viết.
- **OpenAI API Key:** Để sử dụng model `gpt-4o-mini`.
- **Google Gemini (Vertex AI / Google Palm API):** Để tạo hình ảnh minh họa.
- **Gmail Account:** Cấu hình OAuth2 để gửi email xin phê duyệt và nhận phản hồi.
- **LinkedIn Account:** Kết nối OAuth2 với quyền đăng bài (Pages hoặc Profile cá nhân).
- **UploadToUrl Service:** Dịch vụ lưu trữ file tạm để tạo public URL cho hình ảnh hiển thị trong email.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow này hoặc copy đoạn mã JSON gốc.
- Trong giao diện n8n Editor, chọn **Add workflow** -> Click vào menu ba chấm (...) ở góc trên bên phải -> Chọn **Import from File** hoặc **Import from Clipboard** và dán mã JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 15 nodes thông minh, các sếp cần chú ý cấu hình kỹ các điểm sau:
- **Get Data from Sheets**: Kết nối tài khoản Google Sheets của các sếp, chọn đúng file và sheet chứa ý tưởng bài viết. Đảm bảo cấu trúc cột có các trường: `Post Description`, `Instructions`, `Generate Image (Yes/No)`, `Status` (chỉ lấy row có Status = `Ready`).
- **OpenAI Chat Model**: Chọn credentials OpenAI và xác nhận model đang dùng là `gpt-4o-mini`.
- **Generate Post Image (Google Gemini)**: Cấu hình credentials Google Palm/Gemini API, thiết lập prompt để AI hiểu rõ phong cách hình ảnh mong muốn dựa trên mô tả bài viết.
- **Upload a File & Download a File**: Cấu hình dịch vụ UploadToUrl để chuyển đổi binary image từ Gemini thành public URL (giúp hiển thị ảnh trực tiếp trong email phê duyệt).
- **Send Content Confirmation (Gmail)**: Sử dụng tính năng `sendAndWait` của Gmail để tạo nút bấm phê duyệt (Approve/Reject) gửi trực tiếp đến email của người quản lý.
- **Post With Image & Post Without Image (LinkedIn)**: Kết nối tài khoản LinkedIn của các sếp, phân quyền đăng bài thành công.
- **Update Google Sheet & Update Status to Canceled**: Cấu hình mapping dữ liệu trả về để cập nhật trạng thái `Completed`, kèm theo `Post ID` và `LinkedIn Post Link` vào đúng dòng trong Google Sheets khi bài viết được đăng thành công.

#### 3. Kích hoạt ⚡️
- Nhấp vào **Execute Workflow** chạy thử với một dòng dữ liệu mẫu (`Ready`) để kiểm tra toàn bộ luồng từ sinh nội dung, tạo ảnh, gửi email cho đến khi nhận diện nút bấm phê duyệt.
- Sau khi test thành công, gạt công tắc **Active** ở góc trên bên phải để hệ thống tự động chạy theo lịch trình (`Schedule Trigger`).

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Thay vì chỉ dùng Gmail để phê duyệt, các sếp có thể tích hợp thêm node **Slack** hoặc **Telegram** để nhận thông báo và bấm nút duyệt nhanh ngay trên điện thoại.
- **Lưu log lỗi:** Thêm node **Error Trigger** để tự động gửi tin nhắn báo động về Telegram cá nhân nếu quá trình gọi API OpenAI hoặc Gemini gặp sự cố.
- **Báo cáo định kỳ:** Tạo thêm một nhánh chạy vào cuối tuần để tổng hợp số lượng bài viết đã đăng trong tuần vào một sheet thống kê riêng.

### 📌 Kết luận
Tự động hóa quy trình sáng tạo nội dung LinkedIn chưa bao giờ dễ dàng đến thế với sự trợ giúp của AI đa phương tiện và n8n. Hãy áp dụng ngay workflow này để tối ưu hóa hiệu suất làm việc, tiết kiệm thời gian và giữ cho kênh LinkedIn của các sếp luôn sôi động, chuyên nghiệp!