---
title: "🚀 Tự động tạo Cold Email cá nhân hóa từ tin tuyển dụng LinkedIn với GPT-4o và Gmail"
description: "Hướng dẫn xây dựng workflow n8n tự động quét tin tuyển dụng trên LinkedIn, sử dụng GPT-4o để viết email giới thiệu siêu cá nhân hóa và gửi qua Gmail."
slug: "tao-cold-email-tu-dong-tu-linkedin-jobs-gpt-4o-gmail"
tags: [n8n, automation, no-code, ai-agency, openai, gmail, linkedin]
keywords: [n8n workflow, tạo cold email tự động, linkedin jobs ai, gpt-4o cold email, tự động hóa gmail n8n]
---

# 🚀 Tự động tạo Cold Email cá nhân hóa từ tin tuyển dụng LinkedIn với GPT-4o và Gmail

Viết cold email thủ công để tìm kiếm khách hàng hay đối tác từ các tin tuyển dụng trên LinkedIn cực kỳ tốn thời gian: các sếp vừa phải đọc mô tả công việc, nghiên cứu công ty, vừa phải vắt óc suy nghĩ cách viết sao cho thật cá nhân hóa để tỷ lệ phản hồi cao. 

Giải pháp? Workflow n8n này sẽ tự động hóa toàn bộ quy trình từ A-Z: lấy thông tin tuyển dụng từ LinkedIn, phân tích bằng AI (GPT-4o) để viết nội dung chào hàng cực kỳ bén, và tự động gửi qua Gmail mà các sếp không cần tốn một giọt mồ hôi.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Thay vì mất hàng giờ lọc job và viết email, AI sẽ lo phần nặng nhọc này trong tích tắc.
- **Cá nhân hóa đỉnh cao:** GPT-4o phân tích sâu yêu cầu tuyển dụng để tạo ra email nhắm đúng "nỗi đau" của người nhận, tăng tỷ lệ reply (phản hồi) vượt trội.
- **Vận hành tự động 24/7:** Kết hợp Schedule Trigger và các node xử lý thông minh, workflow chạy ngầm đều đặn mỗi ngày để tìm kiếm lead mới.
- **Kiểm soát chặt chẽ:** Tích hợp bộ lọc và điều kiện (If, Filter, Remove Duplicates) để tránh gửi trùng lặp hoặc gửi nhầm đối tượng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **OpenAI API Key:** Để sử dụng sức mạnh của GPT-4o trong việc viết nội dung.
- **Gmail Account (Credentials):** Tài khoản Gmail đã kết nối với n8n để gửi email tự động.
- **Google Sheets / Nguồn dữ liệu:** Nơi lưu trữ danh sách tin tuyển dụng hoặc thông tin lead đầu vào.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ nguồn cung cấp (hoặc copy toàn bộ mã nguồn JSON) và dán trực tiếp vào n8n Editor của các sếp bằng cách chọn **New workflow** -> Dán (Ctrl+V).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp cần cấu hình chính xác các node sau:
- **Node `Google Sheets` / Nguồn Job:** Kết nối tài khoản Google Drive/Sheets của các sếp, chọn đúng file và sheet chứa danh sách tin tuyển dụng từ LinkedIn.
- **Node `Remove Duplicates` & `Filter`:** Kiểm tra lại các quy tắc lọc để đảm bảo chỉ những job mới và phù hợp nhất mới được chuyển sang bước tiếp theo.
- **Node chứa OpenAI (`@n8n/n8n-nodes-langchain.openAi` - GPT-4o):** Điền OpenAI API Key. Tùy chỉnh System Prompt nếu các sếp muốn thay đổi giọng văn (Tone of Voice) của email cho phù hợp với dịch vụ của AI Agency mình.
- **Node `Gmail`:** Chọn Credentials Gmail của các sếp, cấu hình người nhận (To), tiêu đề (Subject) và nội dung lấy từ đầu ra của AI node.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (`Execute Workflow`) với 1-2 dữ liệu mẫu để kiểm tra nội dung AI viết ra có chuẩn chỉnh hay không.
- Bật công tắc **Active** ở góc trên cùng bên phải để workflow tự động chạy theo lịch (Schedule Trigger).

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Telegram/Slack:** Thêm một node Telegram hoặc Slack ở cuối workflow để nhận thông báo ngay lập tức mỗi khi AI tạo và gửi thành công một cold email.
- **Lưu lịch sử vào Google Sheets:** Thêm bước cập nhật trạng thái "Đã gửi email" vào Google Sheets để dễ dàng theo dõi phễu outreach.
- **Chia lô (Batching):** Sử dụng node `Split In Batches` nếu các sếp quét số lượng lớn tin tuyển dụng mỗi ngày, giúp tránh việc chạm ngưỡng giới hạn (rate limit) của API OpenAI và Gmail.

### 📌 Kết luận
Workflow này là vũ khí cực kỳ lợi hại cho các anh em làm AI Agency, Freelancer hay Sales B2B muốn scale quy trình outreach mà vẫn giữ được chất lượng cá nhân hóa cao. Hãy "lên đồ" ngay hôm nay để tối ưu hóa phễu tìm kiếm khách hàng tự động!