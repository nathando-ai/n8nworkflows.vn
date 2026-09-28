---
title: "🚀 Hướng dẫn tự động giám sát Uptime Website & Cảnh báo đa kênh với n8n"
description: "Xây dựng hệ thống tự động kiểm tra trạng thái website 24/7, ghi log Google Sheets và cảnh báo tức thì qua Slack, Gmail, cuộc gọi tự động khi có sự cố."
slug: "giam-sat-uptime-website-tu-dong-n8n"
tags: [n8n, automation, devops, monitoring, google-sheets, slack, gmail]
keywords: [n8n workflow, giám sát website, uptime monitor, tự động hóa devops, cảnh báo sập web, google sheets n8n]
---

# 🚀 Tự động giám sát Uptime Website & Cảnh báo đa kênh (Slack, Gmail, Phone)

Các sếp có bao giờ gặp cảnh website công ty sập giữa đêm, khách hàng không thể truy cập mà sáng hôm sau mới ngớ người biết chuyện? Việc kiểm tra thủ công từng đường link mỗi ngày vừa mất thời gian vừa không hiệu quả. 

Được phát triển bởi **Pixcels Themes** — Agency chuyên cung cấp giải pháp tự động hóa AI và tối ưu quy trình doanh nghiệp, workflow n8n này sẽ giúp các sếp giải quyết triệt để bài toán trên. Hệ thống sẽ tự động kiểm tra danh sách website định kỳ, ghi nhận lịch sử hoạt động vào Google Sheets và ngay lập tức "bắn tín hiệu cứu hộ" qua Slack, Gmail lẫn cuộc gọi tự động khi phát hiện website gặp sự cố.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Giám sát 24/7 không nghỉ:** Chủ động quét danh sách website theo lịch trình cài đặt sẵn mà không cần con người can thiệp.
- **Cảnh báo đa kênh tức thì:** Gửi tin nhắn Slack, Email qua Gmail và kích hoạt cuộc gọi điện thoại khẩn cấp ngay khi website "chết".
- **Lưu trữ dữ liệu minh bạch:** Mọi trạng thái Up/Down đều được ghi log chi tiết kèm thời gian vào Google Sheets để làm báo cáo SLA.
- **Tiết kiệm nguồn lực:** Thay vì tốn tiền mua các bên thứ ba đắt đỏ, tự xây dựng hệ thống giám sát riêng linh hoạt và bảo mật.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản **n8n** (Cloud hoặc Self-hosted).
- **Google Sheets**: 1 file chứa danh sách URL cần check và 1 file/sheet dùng để log lịch sử uptime.
- **Slack Account**: Cấu hình Bot/Webhook để gửi tin nhắn cảnh báo.
- **Gmail Account**: Kết nối OAuth2 để gửi email thông báo sự cố.
- **Vapi.ai API Key** (hoặc dịch vụ gọi điện tương tự): Dùng để cấu hình cuộc gọi tự động khi website sập.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Copy toàn bộ mã JSON của workflow này.
- Vào giao diện n8n Editor, chọn **Add workflow** -> **Import from Clipboard** và dán đoạn JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các node quan trọng sau để hệ thống chạy mượt mà:

- **Schedule Trigger**: Thiết lập khoảng thời gian chạy kiểm tra (ví dụ: chạy mỗi 5 phút, 15 phút hoặc 1 tiếng tùy nhu cầu).
- **Get row(s) in sheet**: Kết nối tài khoản Google Sheets của các sếp và chọn đúng file/sheet chứa danh sách URL website cần theo dõi.
- **Loop Over Items** (`splitInBatches`): Node này giúp duyệt qua từng URL một cách tuần tự để hệ thống không bị quá tải.
- **`htttps request` & HTTP Request1**: Node thực hiện gửi request HTTP để kiểm tra mã trạng thái (status code) của website lấy từ Google Sheets.
- **If website up?**: Kiểm tra xem phản hồi từ website có thành công hay không để phân luồng (Up hay Down).
- **Append row in sheet / Append row in sheet1**: Cấu hình ghi log kết quả (thời gian, URL, trạng thái) vào Google Sheets tương ứng cho trường hợp Website Up hoặc Website Down.
- **Send a message** (`slack`) & **Send a message1** (`gmail`): Kết nối credentials Slack và Gmail, cài đặt người nhận hoặc kênh nhận cảnh báo khi website sập.
- **Edit Fields / Edit Fields1** (`set`): Tinh chỉnh dữ liệu đầu ra cho gọn gàng trước khi đẩy qua các bước tiếp theo (như thông tin tích hợp gọi điện qua Vapi.ai).

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** chạy thử thủ công với dữ liệu mẫu để kiểm tra kết nối Google Sheets, Slack và Gmail xem có hoạt động trơn tru không.
- Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để workflow tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Telegram/Discord:** Ngoài Slack và Gmail, các sếp có thể add thêm node Telegram Bot để nhận cảnh báo ngay trên điện thoại cá nhân tiện lợi hơn.
- **Báo cáo tổng hợp hàng tuần:** Thêm một Schedule Trigger chạy vào thứ Hai hàng tuần để tổng hợp tỷ lệ Uptime từ Google Sheets và gửi email báo cáo sức khỏe hạ tầng cho sếp lớn.
- **Xử lý ngoại lệ (Error Handling):** Thêm Error Trigger vào workflow để nếu bản thân n8n gặp lỗi kết nối mạng, hệ thống sẽ tự động thông báo qua kênh phụ.

### 📌 Kết luận
Với workflow giám sát uptime này, các sếp hoàn toàn có thể yên tâm đi ngủ ngon mà không lo website đột ngột "tàng hình" trước mắt khách hàng. Hãy import ngay vào hệ thống n8n của mình và tối ưu hóa quy trình DevOps ngay hôm nay!