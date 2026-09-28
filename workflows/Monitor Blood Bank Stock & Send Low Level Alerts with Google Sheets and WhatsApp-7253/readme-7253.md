---
title: "🚀 Tự Động Theo Dõi Kho Máu & Cảnh Báo Sức Khỏe Khẩn Cấp với Google Sheets và WhatsApp"
description: "Xây dựng hệ thống tự động kiểm tra lượng máu tồn kho hằng ngày từ Google Sheets và gửi tin nhắn cảnh báo khẩn cấp qua WhatsApp khi vượt ngưỡng an toàn bằng n8n."
slug: "tu-dong-theo-doi-kho-mau-va-canh-bao-whatsapp-n8n"
tags: [n8n, automation, no-code, google-sheets, whatsapp, healthcare]
keywords: [n8n workflow, tự động hóa kho máu, Google Sheets WhatsApp, cảnh báo tồn kho tự động, Oneclick AI Squad]
---

# 🚀 Tự Động Theo Dõi Kho Máu & Cảnh Báo Sức Khấp Khẩn Cấp qua WhatsApp

Việc quản lý kho máu thủ công tại các cơ sở y tế thường đối mặt với rủi ro lớn: nhân sự quên kiểm tra định kỳ, lượng máu dự trữ chạm ngưỡng tối thiểu mà không hay biết, dẫn đến những tình huống thiếu hụt máu khẩn cấp cho người bệnh. 

Giải pháp? Workflow n8n tự động hóa 100% này sẽ thay thế hoàn toàn quy trình thủ công. Hệ thống sẽ tự động quét dữ liệu kho máu từ Google Sheets mỗi ngày, phân tích mức tồn kho và lập tức bắn tin nhắn cảnh báo qua WhatsApp đến đội ngũ quản lý nếu phát hiện nhóm máu nào sắp cạn kiệt.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 24/7**: Không bao giờ bỏ lỡ lịch kiểm tra kho nhờ lịch chạy tự động hàng ngày.
- **Cảnh báo tức thì**: Gửi tin nhắn WhatsApp trực tiếp đến điện thoại quản lý ngay khi nhóm máu chạm ngưỡng nguy hiểm.
- **Giảm thiểu rủi ro**: Đảm bảo nguồn máu dự trữ luôn ở mức an toàn, kịp thời kêu gọi hiến máu bổ sung.
- **Tiết kiệm thời gian**: Loại bỏ hoàn toàn công việc kiểm tra bảng tính thủ công mỗi ngày cho nhân sự.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance**: Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Google Sheets**: Tài khoản Google chứa bảng dữ liệu kho máu.
- **WhatsApp Business API**: Tài khoản và thông tin cấu hình API của WhatsApp để gửi tin nhắn tự động.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ nguồn hoặc sao chép toàn bộ mã JSON, sau đó dán trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 5 nodes chính, các sếp cần cấu hình chính xác các điểm sau:

- **Daily Check Blood Stock (Cron Node)**: 
  - Cấu hình tần suất chạy tự động (mặc định là chạy hằng ngày vào một khung giờ cố định, ví dụ 8:00 sáng).
- **Fetch Blood Stock (Google Sheets Node)**: 
  - Kết nối tài khoản Google của các sếp (`googleApi`).
  - Chọn đúng file Google Sheet quản lý kho máu và chỉ định Sheet Name tương ứng.
  - Cấu trúc cột trong Sheet yêu cầu chuẩn bị sẵn:
    - **Blood Type**: Nhóm máu (Ví dụ: A+, O-).
    - **Quantity**: Số lượng tồn kho hiện tại.
    - **Threshold**: Ngưỡng tối thiểu chấp nhận được.
    - **Last Updated**: Thời gian cập nhật gần nhất.
    - **Status**: Trạng thái (Ví dụ: Low, Sufficient).
- **Get All Stock (Split In Batches Node)**: 
  - Node này giúp duyệt qua từng dòng dữ liệu nhóm máu để hệ thống xử lý logic lần lượt mà không bị nghẽn.
- **Check Stock Availability (Code Node)**: 
  - Kiểm tra logic so sánh giữa `Quantity` và `Threshold`. Nếu lượng tồn kho thấp hơn ngưỡng quy định, node sẽ gán cờ cảnh báo.
- **Send Alert Message (WhatsApp Node)**: 
  - Cấu hình thông tin kết nối WhatsApp API (`whatsAppApi`).
  - Thiết lập số điện thoại nhận tin nhắn khẩn cấp và nội dung mẫu (template) cảnh báo nhóm máu nào đang thiếu hụt để kịp thời xử lý.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để test thử với dữ liệu mẫu xem tin nhắn WhatsApp có đổ về điện thoại hay không.
- Nếu mọi thứ mượt mà, hãy gạt công tắc sang **Active** để hệ thống tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa kênh thông báo**: Kết hợp thêm node Telegram hoặc Slack để bắn tin nhắn đồng thời vào nhóm chat nội bộ của đội ngũ y tế.
- **Tự động ghi Log**: Thiết lập thêm nhánh ghi lại lịch sử các lần cảnh báo vào một Sheet riêng để tiện kiểm toán và báo cáo hàng tháng.
- **Báo cáo định kỳ**: Tạo thêm một lịch trình chạy vào cuối tuần để gửi tổng quan tình hình kho máu qua Email cho cấp quản lý.

### 📌 Kết luận
Việc tự động hóa quy trình theo dõi kho máu với n8n, Google Sheets và WhatsApp không chỉ giúp tiết kiệm thời gian nhân sự mà còn bảo vệ tính mạng người bệnh nhờ sự chính xác và tốc độ phản ứng tức thì. Hãy triển khai ngay hôm nay để tối ưu hóa vận hành cho cơ sở y tế của các sếp!