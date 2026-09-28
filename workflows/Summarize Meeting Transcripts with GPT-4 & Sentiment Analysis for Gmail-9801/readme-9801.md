---
title: "🚀 Tự động hóa Cuộc họp với GPT-4: Tóm tắt & Phân tích Cảm xúc từ Gmail"
description: "Hướng dẫn tự động hóa hoàn toàn quy trình tóm tắt cuộc họp từ file PDF/TXT trong Google Drive, phân tích cảm xúc và gửi email báo cáo chuyên nghiệp bằng n8n"
slug: "tu-dong-hoa-cuoc-hop-gpt-4-tom-tat-phan-tich-cam-xuc"
tags: [n8n, automation, no-code, google-drive, openai, gmail]
keywords: [n8n workflow, tự động hóa cuộc họp, tóm tắt cuộc họp, phân tích cảm xúc, openai gpt-4]
---

# 🚀 Tự động hóa Cuộc họp với GPT-4: Tóm tắt & Phân tích Cảm xúc từ Gmail

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 2-3 giờ mỗi tuần cho việc tóm tắt thủ công
- Nhận báo cáo chuyên nghiệp với các điểm quyết định, ghi chú và nhiệm vụ được phân loại theo cảm xúc
- Tự động hóa hoàn toàn quy trình từ file đến email báo cáo
- Dễ dàng tích hợp với các hệ thống hiện tại (Google Drive, Gmail)
- Hoạt động liên tục 24/7 mà không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Drive với thư mục lưu trữ cuộc họp
- Tài khoản OpenAI với API key (đã kích hoạt GPT-4)
- Tài khoản Gmail để gửi báo cáo
- File cuộc họp ở định dạng PDF hoặc TXT
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/9801](https://n8n.io/workflows/9801)
2. Nhấn nút "Import" trên trang workflow
3. Trong n8n Editor, chọn "Import from URL" và dán link trên
4. Hoặc copy toàn bộ JSON từ trang workflow và paste vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Google Drive Trigger** (Node đầu tiên):
   - Cấu hình credentials: Chọn "googleDriveOAuth2Api"
   - Thiết lập folder theo dõi: Chỉ định thư mục chứa file cuộc họp
   - Đảm bảo tài khoản có quyền truy cập đầy đủ vào thư mục này

2. **Extract from File** (2 node):
   - Node đầu tiên: Đã cấu hình sẵn cho PDF (không cần thay đổi)
   - Node thứ hai: Đã cấu hình sẵn cho TXT (không cần thay đổi)

3. **OpenAI Chat Model**:
   - Cấu hình credentials: Chọn "openAiApi"
   - Model: Đã chọn "gpt-4.1-mini" (có thể thay đổi nếu cần)
   - Prompt: Sử dụng prompt mặc định đã được tối ưu trong workflow

4. **Send a message** (Gmail):
   - Cấu hình credentials: Chọn "gmailOAuth2"
   - Địa chỉ email nhận: Thiết lập email nhận báo cáo
   - Message: Đã cấu hình sẵn với biến `{{$json.email_html}}`

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu:
   - Tải một file cuộc họp mẫu vào thư mục Google Drive
   - Kiểm tra quá trình xử lý trong n8n Editor
2. Bật Active workflow:
   - Chọn workflow trong danh sách
   - Nhấn nút "Activate" để bắt đầu theo dõi thư mục

### ✍️ Mẹo & gợi ý nâng cao
1. **Tích hợp Slack/Teams**: Thêm node gửi báo cáo đến các kênh chat
2. **Lưu log**: Thêm node lưu trữ báo cáo vào Google Sheets hoặc Notion
3. **Báo cáo định kỳ**: Thiết lập workflow chạy theo lịch định kỳ thay vì theo sự kiện
4. **Phân tích nâng cao**: Sử dụng các model AI khác để phân tích cảm xúc chi tiết hơn

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian đáng kể trong việc xử lý cuộc họp hàng ngày. Bằng cách tự động hóa quy trình từ file đến email báo cáo, các sếp có thể tập trung vào những nhiệm vụ quan trọng hơn. Hãy thử ngay và trải nghiệm sự khác biệt trong cách làm việc của bạn!