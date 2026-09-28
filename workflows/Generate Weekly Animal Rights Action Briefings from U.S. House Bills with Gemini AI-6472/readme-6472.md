---
title: "🚀 Tự động hóa tóm tắt dự luật quyền động vật tại Hạ viện Mỹ hàng tuần bằng Gemini AI"
description: "Xây dựng hệ thống n8n tự động lấy danh sách dự luật Hạ viện Mỹ, phân tích bằng Gemini AI dưới góc độ quyền động vật, và gửi email báo cáo chi tiết hàng tuần."
slug: "tu-dong-hoa-tom-tat-du-luat-quyen-dong-vat-gemini-ai"
tags: [n8n, automation, no-code, gemini-ai, openrouter, ai-summarization]
keywords: [n8n workflow, tự động hóa dự luật, quyền động vật, gemini ai, openrouter, email automation]
---

# 🚀 Tự động hóa tóm tắt dự luật quyền động vật tại Hạ viện Mỹ hàng tuần bằng Gemini AI

Việc theo dõi, đọc hiểu và phân tích hàng chục dự luật mới được trình lên Hạ viện Mỹ mỗi tuần là một gánh nặng lớn đối với các tổ chức phi lợi nhuận và nhà hoạt động vì quyền động vật. Việc làm thủ công này không chỉ tốn hàng giờ đồng hồ mà còn dễ bỏ sót các điều khoản quan trọng. 

Workflow n8n này do **Open Paws** phát triển sẽ tự động hóa 100% quy trình: quét dự luật hàng tuần, tải file PDF, sử dụng sức mạnh của **Gemini AI** (qua OpenRouter) để phân tích chuyên sâu dưới góc độ quyền động vật, tổng hợp thông tin, và gửi bản tin (briefing) hoàn chỉnh qua email. Giải pháp giúp các nhà hoạt động nắm bắt thông tin nhanh chóng và đưa ra hành động kịp thời mà không cần tốn một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Tự động lấy, đọc, phân tích hàng loạt dự luật dài hàng trăm trang chỉ trong vài phút.
- **Phân tích chuyên sâu thông minh:** Đánh giá chính xác tác động của dự luật đến quyền lợi động vật, tính điểm ưu tiên (`action_priority`) và lập trường đề xuất (`support`, `oppose`, `monitor`).
- **Báo cáo tự động hàng tuần:** Tổng hợp thành bản tin HTML đẹp mắt, sẵn sàng gửi đến danh sách email của nhà hoạt động đúng 8 giờ sáng thứ Hai hàng tuần.
- **Hoạt động liên tục 24/7:** Chạy ngầm hoàn toàn tự động, không lo bỏ sót bất kỳ văn bản lập pháp nào.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (phiên bản Cloud hoặc Self-hosted).
- **Tài khoản OpenRouter API:** Để kết nối với các mô hình AI (`google/gemini-2.5-flash` và `anthropic/claude-sonnet-4`).
- **SMTP Server / Email Credentials:** Để cấu hình node gửi email (Gmail, SendGrid, Resend, v.v.).
- **Subworkflow Research Agent:** Cần tải và import thêm workflow phụ [Multi-Tool Research Agent for Animal Advocacy](https://n8n.io/workflows/5588-multi-tool-research-agent-for-animal-advocacy-with-openrouter-serper-and-open-paws-db/).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc sao chép toàn bộ mã nguồn JSON.
- Mở giao diện n8n Editor, chọn **Add workflow** -> **Import from File / Clipboard** và dán dữ liệu vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 18 nodes được thiết kế mạch lạc. Các sếp cần chú ý cấu hình các điểm mấu chốt sau:
- **Schedule Trigger:** Mặc định chạy vào lúc 8:00 AM mỗi thứ Hai hàng tuần. Các sếp có thể điều chỉnh lại lịch chạy nếu muốn thay đổi thời gian nhận báo cáo.
- **OpenRouter Chat Model & OpenRouter Chat Model1:** Chọn credentials OpenRouter và kiểm tra lại việc gán model (`google/gemini-2.5-flash` cho việc phân tích và `anthropic/claude-sonnet-4` cho việc viết email).
- **Analyze Bill with Gemini:** Nơi thiết lập prompt phân tích dự luật. Các sếp có thể tùy chỉnh prompt trong node này để thay đổi tiêu chí đánh giá (ví dụ: tập trung vào động vật trang trại, động vật hoang dã hoặc ảnh hưởng khí hậu).
- **Research Bills (Execute Workflow):** Node này gọi đến một subworkflow bổ trợ. Các sếp bắt buộc phải import workflow phụ [Multi-Tool Research Agent](https://n8n.io/workflows/5588-multi-tool-research-agent-for-animal-advocacy-with-openrouter-serper-and-open-paws-db/) trước, sau đó trỏ node này về subworkflow đó.
- **Send email:** Kết nối credentials SMTP của các sếp và điền địa chỉ email nhận bản tin (mailing list của hội nhóm/tổ chức).

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** để test thử nghiệm với dữ liệu mẫu xem hệ thống đọc PDF và phân tích chạy mượt mà chưa.
- Sau khi test thành công, bật công tắc **Active** ở góc trên cùng bên phải để workflow tự động chạy ngầm hàng tuần.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh liên lạc nội bộ:** Thay vì chỉ gửi email, các sếp có thể nối thêm node **Slack** hoặc **Telegram** để bắn thông báo nhanh cho ban cố định ngay khi có dự luật khẩn cấp (`action_priority` cao).
- **Lưu trữ dữ liệu lịch sử:** Thêm node **Google Sheets** hoặc **Supabase** trước bước gửi email để lưu lại toàn bộ lịch sử phân tích dự luật, phục vụ cho việc tra cứu về sau.
- **Tùy biến ngưỡng lọc (Filtering):** Tinh chỉnh node **Check If Response Needed / IF** để tự động lọc bỏ các dự luật không liên quan, chỉ giữ lại những văn bản có điểm số tác động cao.

### 📌 Kết luận
Workflow từ **Open Paws** thực sự là một "vũ khí tối tân" giúp tối ưu hóa công tác vận động chính sách và bảo vệ quyền động vật bằng sức mạnh của AI. Hãy cài đặt ngay hôm nay để tự động hóa toàn bộ quy trình nghiên cứu lập pháp cho tổ chức của các sếp!