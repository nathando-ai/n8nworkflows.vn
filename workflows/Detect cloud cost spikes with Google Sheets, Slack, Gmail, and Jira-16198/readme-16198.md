---
title: "🚀 Tự động phát hiện chi phí Cloud tăng vọt với n8n, Google Sheets, Slack và Jira"
description: "Hướng dẫn cài đặt và sử dụng workflow n8n giúp giám sát chi phí cloud hàng ngày, so sánh với baseline, tự động tạo Jira ticket và gửi cảnh báo qua Slack, Gmail."
slug: "tu-dong-phat-hien-chi-phi-cloud-tang-vot-n8n"
tags: [n8n, automation, devops, cloud-cost, slack, jira, google-sheets]
keywords: [n8n workflow, cloud cost spike detector, giám sát chi phí aws gcp, tự động hóa devops, n8n viet nam]
---

# 🚀 Tự động phát hiện chi phí Cloud tăng vọt với n8n, Google Sheets, Slack và Jira

Các sếp có bao giờ tá hoả khi cuối tháng nhận hoá đơn tiền Cloud (AWS, GCP, Azure) tăng đột biến mà không rõ nguyên nhân? Việc kiểm tra thủ công hàng ngày rất dễ bỏ sót, và khi phát hiện ra thì hóa đơn đã "phình to" vượt ngân sách. 

Bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n tự động hoàn toàn: giám sát chi phí cloud mỗi ngày, so sánh với mức trung bình lịch sử, phân loại mức độ nghiêm trọng, tự động tạo ticket trên Jira, đồng thời bắn cảnh báo tức thì qua Slack cho đội DevOps và Gmail cho bộ phận Tài chính. Không còn nỗi lo hóa đơn "gây sốc" cuối tháng!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Chặn đứng chi phí bất thường:** Phát hiện ngay lập tức các tài nguyên chạy lãng phí hoặc bị chiếm dụng trước khi hóa đơn cuối tháng bùng nổ.
- **Tự động hóa toàn diện:** Không cần ai phải ngồi check bảng tính hay hóa đơn mỗi ngày.
- **Phối hợp đa kênh hiệu quả:** Tự động tạo incident trên Jira cho dev xử lý, gửi cảnh báo nhanh qua Slack và tổng hợp báo cáo tài chính qua Gmail.
- **Minh bạch và lưu vết:** Mọi dữ liệu chi phí và các lần chạy đều được ghi log chi tiết vào Google Sheets để làm baseline cho các ngày tiếp theo.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Hệ thống n8n (Self-hosted hoặc Cloud).
- Tài khoản **Google Sheets** (chứa dữ liệu baseline chi phí và log).
- Tài khoản **Slack** (để gửi cảnh báo đến channel DevOps/FinOps).
- Tài khoản **Gmail** (gửi bản tổng hợp cho phòng tài chính).
- Tài khoản **Jira** (để tự động tạo ticket sự cố khi có spike).
- API Key của dịch vụ Cloud Billing (hoặc Endpoint HTTP API lấy chi phí).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể sử dụng file JSON của workflow này, copy và paste trực tiếp vào n8n Editor của mình. Workflow bao gồm 11 nodes chính được chia làm 3 giai đoạn: Lấy dữ liệu, Phân tích & Phát hiện Spike, Cảnh báo & Ghi log.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động mượt mà, các sếp cần cấu hình chính xác các node sau:
- **Daily Schedule (`scheduleTrigger`):** Thiết lập thời gian chạy tự động mỗi buổi sáng (khớp với chu kỳ cập nhật billing của nhà cung cấp cloud).
- **Fetch Daily Cost (`httpRequest`):** Thêm API Key của cloud billing vào HTTP header credentials và trỏ tới endpoint lấy chi phí ngày gần nhất.
- **Read Cost Baseline & Log Run to Sheet (`googleSheets`):** Kết nối tài khoản Google Sheets, chọn đúng file bảng tính chứa lịch sử chi phí và sheet ghi log (`append`).
- **Calculate Spike (`code`):** Tùy chỉnh tỷ lệ ngưỡng phần trăm (%) tăng trưởng được coi là "spike" tại đây.
- **Classify Severity (`set`):** Cấu hình phân loại mức độ nghiêm trọng (Watch, High, Critical) dựa trên biên độ tăng chi phí.
- **Create Jira Incident (`jira`):** Chọn project và loại ticket (Issue type) sẽ tự động khởi tạo khi phát hiện chi phí tăng vọt.
- **Slack FinOps Alert (`slack`):** Kết nối workspace Slack và chọn channel nhận thông báo (ví dụ: `#devops-alerts` hoặc `#finops`).
- **Email Finance Summary (`gmail`):** Cấu hình tài khoản Gmail gửi báo cáo tổng hợp cho đội tài chính/kế toán.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (**Test run**) với dữ liệu mẫu để kiểm tra từng nhánh `Valid Data` và `Is Spike`.
- Sau khi mọi thứ hoạt động trơn tru, bật công tắc **Active** để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm Telegram/Discord:** Nếu công ty dùng Telegram thay vì Slack, có thể thay thế node Slack bằng node Telegram để bắn tin nhắn alert cực kỳ tiện lợi.
- **Thêm Dashboard trực quan:** Kết nối Google Sheets với Google Looker Studio (Data Studio) để vẽ biểu đồ chi phí cloud theo thời gian thực cho sếp lớn xem.
- **Tự động tắt tài nguyên:** Mở rộng workflow bằng cách gọi API của AWS/GCP để tự động tạm dừng các instance chạy ngầm khi mức độ cảnh báo đạt cấp độ *Critical*.

### 📌 Kết luận
Quản lý chi phí cloud chưa bao giờ là bài toán dễ dàng nếu làm thủ công. Với workflow n8n này, các sếp hoàn toàn có thể chủ động kiểm soát ngân sách, "bóp chết" các chi phí phát sinh vô lý trước khi chúng kịp làm rỗng ví công ty. Cài đặt ngay hôm nay để thảnh thơi tận hưởng giấc ngủ ngon!