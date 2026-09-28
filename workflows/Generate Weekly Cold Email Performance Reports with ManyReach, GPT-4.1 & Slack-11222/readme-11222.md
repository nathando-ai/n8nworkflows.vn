---
title: "🚀 Tự động hóa báo cáo Cold Email hàng tuần với ManyReach, GPT-4 và Slack"
description: "Hướng dẫn xây dựng workflow n8n tự động lấy dữ liệu chiến dịch Cold Email từ ManyReach, dùng GPT-4 phân tích hiệu suất, tạo Google Doc báo cáo và gửi thông báo qua Slack."
slug: "tu-dong-hoa-bao-cao-cold-email-nhieu-reach-gpt4-slack"
tags: [n8n, automation, no-code, ai, email-marketing, slack]
keywords: [n8n workflow, ManyReach automation, cold email reporting, GPT-4 AI agent, tự động hóa n8n]
---

# 🚀 Tự động hóa báo cáo Cold Email hàng tuần với ManyReach, GPT-4 & Slack

Việc tổng hợp số liệu chiến dịch cold email (tỷ lệ mở, tỷ lệ trả lời, tỷ lệ chuyển đổi) và viết báo cáo thủ công mỗi tuần thường ngốn rất nhiều thời gian của các đội ngũ Sales và Marketing. Chưa kể việc phân tích sâu các chỉ số này so với benchmark ngành để tìm ra điểm nghẽn không phải ai cũng làm tốt.

Workflow n8n này sẽ giải quyết trọn gói bài toán trên: tự động lấy dữ liệu từ ManyReach, nhờ AI thông minh (GPT-4) phân tích và đưa ra đề xuất chiến lược, tự động xuất thành file Google Docs chuyên nghiệp và bắn link trực tiếp về Slack cho team vào mỗi đầu tuần.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian thủ công**: Không cần copy/paste số liệu hay viết báo cáo hàng tuần nữa.
- **Phân tích chuyên sâu chuẩn chuyên gia**: GPT-4 thay mặt team đánh giá tỷ lệ Open, Reply, chuyển đổi và đưa ra lời khuyên cải thiện thực tế.
- **Báo cáo trực quan, chuyên nghiệp**: Tự động sinh Google Doc đẹp mắt lưu trữ trên Google Drive.
- **Cập nhật liền mạch**: Gửi thẳng kết quả vào kênh Slack của đội ngũ để mọi người cùng nắm bắt tiến độ.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance** (Cloud hoặc Self-hosted).
- Tài khoản và API Key của **ManyReach**.
- Tài khoản **OpenAI API** (sử dụng model `gpt-4.1`).
- Tài khoản **Google Drive** (để lưu trữ file báo cáo).
- Tài khoản **Slack** (để gửi thông báo).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này hoặc copy đoạn JSON và dán trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình các node quan trọng sau đây để workflow chạy mượt mà:

- **Schedule Trigger**: Thiết lập thời gian chạy định kỳ (Ví dụ: 8:00 sáng thứ Hai hàng tuần).
- **Fetch All Campaign** & **Fetch One Campaign** (HTTP Request nodes): Cấu hình thông tin xác thực (`httpQueryAuth`) với API Key của tài khoản ManyReach.
- **Filter Active & Completed Campaign**: Node này lọc ra các chiến dịch đang chạy nhưng đã hoàn thành chuỗi gửi (Completed) để tiến hành làm báo cáo.
- **4.1** (OpenAI Chat Model) & **Campaign Report Agent**: Chọn credentials OpenAI và đảm bảo model được cấu hình là `gpt-4.1`.
- **Set Details** (Set Node): Mở node này và điền `drive_folder_id` của thư mục Google Drive nơi các sếp muốn lưu trữ các file báo cáo tự động.
- **Upload Doc** (HTTP Request): Cấu hình kết nối `googleDriveOAuth2Api` để upload file HTML/Doc lên Drive.
- **Send a Doc Link** (Slack Node): Kết nối `slackOAuth2Api` và chọn kênh Slack (Slack Channel) mà team sẽ nhận được báo cáo hàng tuần.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) bằng tay để kiểm tra xem dữ liệu từ ManyReach có trả về đúng không và AI có sinh nội dung chính xác không.
- Sau khi test thành công, bật công tắc **Active** để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa kênh thông báo**: Ngoài Slack, các sếp có thể nối thêm node Telegram hoặc Email để gửi bản tóm tắt báo cáo cho sếp lớn.
- **Lưu trữ Log vào Google Sheets**: Thêm một node Google Sheets để ghi lại lịch sử các chiến dịch đã được báo cáo nhằm theo dõi dài hạn.
- **Tùy chỉnh Prompt cho AI**: Tinh chỉnh prompt bên trong AI Agent để phù hợp hơn với văn phong báo cáo riêng của công ty các sếp (tiếng Việt hoặc tiếng Anh).

### 📌 Kết luận
Workflow này là một "vũ khí" cực kỳ lợi hại giúp tự động hóa khâu báo cáo chiến dịch Cold Email, giúp đội ngũ Marketing/Sales tập trung vào việc tối ưu nội dung thay vì loay hoay với những con số. Hãy áp dụng ngay vào hệ thống n8n của các sếp nhé!