---
title: "🚀 Tự động trích xuất bình luận bài viết trên X (Twitter) bằng Airtop và n8n"
description: "Hướng dẫn tự động hóa quy trình thu thập comment, tên tác giả và link profile từ bất kỳ bài viết X nào với Airtop Browser Automation API."
slug: "trich-xuat-binh-luan-x-post-airtop-n8n"
tags: [n8n, automation, airtop, twitter, x-automation, marketing]
keywords: [n8n workflow, airtop browser automation, trich xuat comment twitter, crawl x post, tu dong hoa marketing]
---

# 🚀 Tự động trích xuất bình luận bài viết trên X (Twitter) bằng Airtop và n8n

Việc theo dõi và tương tác với các cuộc hội thoại trên X (trước đây là Twitter) đóng vai trò cực kỳ quan trọng đối với các thương hiệu và cá nhân muốn nắm bắt tâm lý khách hàng, tìm kiếm khách hàng tiềm năng hay cập nhật xu hướng mới nhất. Tuy nhiên, việc thủ công copy/paste từng bình luận tốn rất nhiều thời gian. Giải pháp tự động hóa này sẽ giúp các sếp trích xuất dữ liệu bình luận một cách mượt mà, nhanh chóng và hoàn toàn không cần code!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian tuyệt đối:** Thay vì lướt và lọc comment thủ công, hệ thống tự động gom toàn bộ dữ liệu chỉ trong vài giây.
- **Dữ liệu cấu trúc sạch sẽ:** Nhận ngay thông tin chi tiết gồm tên tác giả, đường dẫn profile X và nội dung bình luận.
- **Linh hoạt kích hoạt:** Hỗ trợ chạy trực tiếp qua Web Form hoặc tích hợp như một Sub-workflow gọi từ các kịch bản khác.
- **Hoạt động thông minh:** Ứng dụng AI Browser Automation từ Airtop để xử lý các trang web có cơ chế xác thực phức tạp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản Airtop**: Lấy [Airtop API Key](https://portal.airtop.ai/api-keys) (miễn phí khởi tạo).
- **Airtop Profile**: Tạo một [Browser Profile](https://portal.airtop.ai/browser-profiles) trên Airtop và đăng nhập sẵn tài khoản X của các sếp (chỉ cần làm 1 lần duy nhất).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải mã nguồn JSON của workflow này từ kho lưu trữ n8n (Link gốc: [n8n.io/workflows/4208](https://n8n.io/workflows/4208)) và chọn **Import from File** hoặc copy/paste trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 5 nodes chính được thiết kế để xử lý linh hoạt đầu vào. Các sếp cần chú ý cấu hình các điểm sau:

- **Node `On form submission` & `When Executed by Another Workflow`**: Đây là hai điểm kích hoạt (Trigger). Các sếp chọn cách vận hành phù hợp (gửi qua Form điền URL bài viết hoặc nhận dữ liệu từ một workflow khác).
- **Node `Unify params` & `Edit Fields`**: Dùng để chuẩn hóa các tham số đầu vào như:
  - `airtop_profile`: Tên profile Airtop đã kết nối với tài khoản X.
  - `x_post_url`: Đường dẫn bài viết X cần lấy bình luận.
  - `max_number_of_comments`: Số lượng comment tối đa muốn lấy.
- **Node `Extract X Post Comments` (Airtop Node)**: 
  - Kết nối **Airtop API Credentials** của các sếp.
  - Cấu hình Prompt trích xuất sử dụng cú pháp: `=This is an x post. Extract up to {{ $json.max_number_of_comments }} comments to the post. For each comment extract the name of the author, the x profile URL of the author, and the text of the comment.`

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và test thử bằng một URL bài viết X cụ thể để kiểm tra kết quả trả về.
- Sau khi test thành công, bật nút **Active** để đưa workflow vào trạng thái vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp X Monitoring**: Tự động phát hiện các bài viết hot liên quan đến thương hiệu và tự kích hoạt luồng trích xuất này.
- **Phân tích cảm xúc (Sentiment Analysis):** Đưa dữ liệu comment qua các node LLM (như OpenAI, Anthropic) để phân tích ý kiến khen/chê của cộng đồng đối với chiến dịch.
- **Đẩy dữ liệu vào Google Sheets / CRM / Slack:** Lưu trữ danh sách người bình luận để phục vụ cho các chiến dịch Outreach, chăm sóc khách hàng hoặc báo cáo định kỳ.

### 📌 Kết luận
Workflow tích hợp Airtop Browser Automation và n8n là vũ khí cực mạnh giúp các sếp tự động hóa việc khai thác dữ liệu từ mạng xã hội X một cách thông minh và trơn tru. Bắt tay vào cài đặt ngay hôm nay để tối ưu hóa hiệu suất làm việc nào!