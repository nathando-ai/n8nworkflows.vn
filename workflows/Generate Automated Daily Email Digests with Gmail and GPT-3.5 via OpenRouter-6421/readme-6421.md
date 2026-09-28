---
title: "🚀 Tự động hóa tóm tắt email hàng ngày với Gmail và AI OpenRouter trong n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động gom nhóm email chưa đọc trong 24 giờ qua, dùng AI OpenRouter (GPT-3.5) tóm tắt ngắn gọn và gửi bản tin digest qua Gmail mỗi sáng."
slug: "tu-dong-hoa-tom-tat-email-hang-ngay-gmail-openrouter-n8n"
tags: [n8n, automation, gmail, openrouter, ai-summarization, productivity]
keywords: [n8n workflow, tóm tắt email tự động, gmail openrouter gpt3.5, n8n gmail ai agent, automation productivity]
---

# 🚀 Tự động hóa tóm tắt email hàng ngày với Gmail và AI OpenRouter

Mỗi sáng thức dậy, hộp thư đến (Inbox) của các sếp lại ngập tràn hàng chục, thậm chí hàng trăm email chưa đọc. Việc phải lướt qua từng thư rác, email thông báo hay các chuỗi hội thoại dài dòng ngốn rất nhiều thời gian và năng lượng quý giá trước khi ngày làm việc thực sự bắt đầu.

Thay vì đọc thủ công từng email, workflow n8n này sẽ "lên đồ" giúp các sếp tự động gom tất cả email chưa đọc từ ngày hôm trước, nhờ AI (GPT-3.5 thông qua OpenRouter) phân tích, trích xuất ý chính, hạn chót (deadline) và các việc cần làm (action items), sau đó gửi thẳng một bản tổng hợp (Daily Digest) cực kỳ súc tích vào hòm thư của các sếp đúng 7 giờ sáng mỗi ngày. Giải pháp tự động hóa 100% không cần code!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 không lo bị gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian đỉnh cao:** Thay vì mất 30-45 phút đọc email mỗi sáng, các sếp chỉ mất 2 phút đọc bản tóm tắt tinh gọn.
- **Không bỏ lỡ việc quan trọng:** AI tự động lọc ra deadline, các công việc cần phản hồi và thông tin cốt lõi.
- **Cá nhân hóa phong cách:** Dễ dàng tùy chỉnh prompt để AI viết bản tin theo đúng giọng văn mong muốn.
- **Hoạt động tự động 24/7:** Chạy ngầm mượt mà, đúng giờ hẹn là có email báo cáo trên tay.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n instance:** Đã kết nối internet và hoạt động ổn định.
- **Tài khoản Gmail:** Cần cấu hình OAuth2 Credentials trong n8n để có quyền đọc và gửi email.
- **OpenRouter API Key:** Đã liên kết với các LangChain nodes trong n8n để sử dụng mô hình AI.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể copy mã JSON của workflow từ nguồn cung cấp hoặc tải file JSON về, sau đó chọn **Import from File** hoặc dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà không lỗi, các sếp cần chú ý cấu hình kỹ các node trọng điểm sau:

- **Schedule Trigger:** Mặc định được đặt chạy vào lúc 7:00 AM mỗi ngày. Các sếp có thể đổi khung giờ này sang thời điểm thích hợp hơn với múi giờ hoặc nhu cầu cá nhân.
- **Fetch Yeasterday's Date (Code node):** Node này dùng để tạo chuỗi truy vấn (query) tìm kiếm email trong vòng 24 giờ qua. Các sếp nhớ cập nhật lại địa chỉ email mục tiêu trong code nếu muốn lọc email theo điều kiện riêng.
- **Fetch Email Which is Unread (Gmail node):** Chọn đúng Credentials tài khoản Gmail đã kết nối OAuth2, thiết lập thao tác (`operation: getAll`) để lấy các thông điệp phù hợp với query thời gian từ code node.
- **Aggregate node:** Gom nhóm dữ liệu các email thô (From, To, Subject, snippet, CC) thành một tập dữ liệu duy nhất để chuyển tiếp cho AI.
- **OpenRouter Chat Model & Summary (AI Agent):** 
  - Chọn model `openai/openai/gpt-3.5-turbo` (hoặc model tùy ý hỗ trợ qua OpenRouter).
  - Điền OpenRouter API Key vào credential của mô hình chat.
  - Tùy chỉnh Prompt trong AI Agent nếu muốn thay đổi phong cách tóm tắt (ví dụ: yêu cầu tóm tắt bằng tiếng Việt, chia theo nhóm Dự án/Khách hàng/Cá nhân).
- **Send A email of Summary (Gmail node):** Cấu hình tài khoản gửi và điền email nhận bản tin tổng hợp hàng ngày của các sếp.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Test workflow** để chạy thử nghiệm xem dữ liệu email có được kéo về và AI có trả về kết quả tóm tắt chính xác hay không.
- Sau khi test thành công, bật công tắc **Active** ở góc trên cùng bên phải để workflow tự động chạy ngầm mỗi ngày.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa kênh thông báo:** Ngoài gửi qua Gmail, các sếp có thể gắn thêm node Telegram hoặc Slack ở cuối workflow để nhận bản tóm tắt ngay trên điện thoại cho nhanh gọn.
- **Lưu trữ lịch sử:** Thêm một node Google Sheets để lưu lại các bản tóm tắt hàng ngày nhằm dễ tra cứu lại các quyết định hoặc deadline cũ khi cần.
- **Lọc thông minh:** Tinh chỉnh query trong Code node để chỉ quét email từ các khách hàng VIP hoặc các từ khóa quan trọng (như "Urgent", "Invoice", "Meeting").

### 📌 Kết luận
Workflow tự động hóa tóm tắt email bằng Gmail và OpenRouter là một "trợ lý ảo" tuyệt vời giúp giải phóng thời gian và bộ nhớ cho các sếp. Hãy cài đặt ngay hôm nay để tối ưu hóa năng suất làm việc của bản thân và doanh nghiệp!