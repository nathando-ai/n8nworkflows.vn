---
title: "🚀 Kiểm tra xem link có bản preview hay không với n8n & Peekalink"
description: "Tự động phát hiện xem một URL có bản preview (thumbnail, title, description) hay không chỉ trong 1 click, giảm thời gian kiểm tra thủ công và tăng độ chính xác."
slug: "kiem-tra-preview-link-n8n"
tags: [n8n, automation, no-code, peekalink, link-preview]
keywords: [n8n workflow, tự động hóa, kiểm tra preview link, Peekalink API, no-code automation]
---

# 🚀 Kiểm tra xem link có bản preview hay không với n8n & Peekalink

Khi phải xử lý hàng chục, hàng trăm link trong quy trình marketing, content hoặc support, việc **kiểm tra thủ công** xem mỗi URL có hiển thị preview (hình ảnh, tiêu đề, mô tả) hay không là cực kỳ tốn thời gian và dễ gây sai sót.  
Workflow **“Check for preview for a link”** giúp các sếp **tự động hoá 100%** quá trình này chỉ với một click, không cần viết một dòng code nào. Khi link có preview, workflow sẽ lấy chi tiết preview; nếu không, nó sẽ bỏ qua mà không gây lỗi.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Kiểm tra hàng loạt link trong vài giây.  
- **Độ chính xác cao**: Dựa trên API Peekalink, không còn lỗi do con mắt con người.  
- **Tự động hoá liên tục**: Có thể tích hợp vào pipeline hiện có (Slack, Google Sheets, Email…).  
- **Giảm chi phí nhân lực**: Nhân viên không cần dành thời gian “copy‑paste” link để kiểm tra.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Peekalink** và **API Key** (đăng ký tại https://peekalink.io).  
- **n8n** đã được cài đặt và chạy (Self‑hosted hoặc n8n.cloud).  
- Quyền **Credentials → peekalinkApi** trong n8n để kết nối tới Peekalink.  
- (Tuỳ chọn) Kênh thông báo như Slack/Telegram nếu muốn nhận kết quả ngay lập tức.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Vào **n8n → Workflows → Import**.  
2. Tải file JSON của workflow (hoặc copy toàn bộ JSON từ trang gốc https://n8n.io/workflows/935) và nhấn **Import**.  
3. Đặt tên cho workflow (mặc định là *Check for preview for a link*).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Mô tả | Cấu hình cần thay đổi |
|------|------|-----------------------|
| **On clicking 'execute'** (manualTrigger) | Nút khởi động workflow bằng tay. | Không cần thay đổi, chỉ dùng để test hoặc gắn vào Trigger khác (Webhook, Cron). |
| **Peekalink** | Kiểm tra nhanh xem link có preview hay không. | - **Operation**: `isAvailable` (đã được set). <br> - **Credentials**: chọn `peekalinkApi` và dán **API Key** của bạn. |
| **IF** | Đánh giá kết quả từ node Peekalink. | - **Condition**: `{{$json["isAvailable"]}}` **is true**. <br> (Nếu `true` → chạy node Peekalink1, ngược lại → NoOp). |
| **Peekalink1** | Lấy chi tiết preview (title, description, image, etc.) khi link có preview. | - **Operation**: `metadata` (mặc định). <br> - **Credentials**: lại dùng `peekalinkApi`. |
| **NoOp** | Node “không làm gì” – dùng để bỏ qua khi không có preview. | Không cần cấu hình, chỉ để workflow không bị lỗi khi IF trả về false. |

> **Lưu ý:** Nếu muốn thay đổi nguồn link, bạn có thể thêm một node **Set** hoặc **HTTP Request** trước node Peekalink để đưa URL vào `{{$json["url"]}}`.

#### 3. Kích hoạt ⚡️
1. Nhấn **Execute Workflow** → nhập URL cần kiểm tra → **Run**.  
2. Kiểm tra output của **Peekalink1** (nếu có) để xác nhận dữ liệu preview.  
3. Khi mọi thứ ổn, bật **Active** ở góc phải để workflow sẵn sàng chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Gửi báo cáo Slack/Telegram**: Thêm node **Slack** hoặc **Telegram** sau Peekalink1 để gửi tiêu đề + thumbnail ngay lập tức.  
- **Lưu log vào Google Sheets**: Kết nối node **Google Sheets** sau Peekalink1, ghi lại URL, trạng thái preview, thời gian kiểm tra.  
- **Chạy định kỳ**: Thay node **manualTrigger** bằng **Cron** để tự động kiểm tra danh sách URL mỗi ngày/giờ.  
- **Kết hợp với Zapier/Integromat**: Dùng webhook để nhận URL từ các form, sau đó đưa vào workflow này.  

### 📌 Kết luận
Với workflow **Check for preview for a link**, các sếp có thể **loại bỏ công đoạn kiểm tra thủ công**, giảm lỗi và tăng tốc độ xử lý nội dung. Hãy import ngay, cấu hình API Peekalink và để n8n làm việc thay bạn – thời gian quý báu sẽ được dành cho những việc quan trọng hơn! 🚀