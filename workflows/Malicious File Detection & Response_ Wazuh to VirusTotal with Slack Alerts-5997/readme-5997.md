---
title: "🚀 Tự động phát hiện và ứng phó mã độc: Tích hợp Wazuh, VirusTotal và Slack qua n8n"
description: "Hướng dẫn xây dựng hệ thống SecOps tự động hóa 100% giúp nhận cảnh báo từ Wazuh SIEM, kiểm tra mã độc trên VirusTotal, tạo Incident trên ServiceNow và cảnh báo lập tức qua Slack, Gmail."
slug: "phat-hien-ma-doc-wazuh-virustotal-slack-n8n"
tags: [n8n, automation, secops, wazuh, virustotal, cybersecurity]
keywords: [n8n workflow, wazuh siem, virustotal api, tu dong hoa an ninh mang, secops automation]
keywords: [n8n workflow, wazuh siem, virustotal api, tự động hóa an ninh mạng, secops automation]
---

# 🚀 Tự động phát hiện và ứng phó mã độc: Tích hợp Wazuh, VirusTotal và Slack qua n8n

Trong môi trường vận hành an ninh mạng (SecOps), việc xử lý thủ công các cảnh báo tính toàn vẹn tệp tin (File Integrity Monitoring - FIM) từ SIEM tiêu tốn rất nhiều thời gian của các kỹ sư SOC. Khi một tệp lạ xuất hiện, các sếp thường phải mất thời gian tra cứu hash trên VirusTotal, tạo ticket báo cáo và ping đội ngũ. Workflow này sinh ra để giải quyết triệt để nỗi đau đó bằng cách tự động hóa toàn bộ quy trình từ lúc nhận cảnh báo đến khi phân tích và cô lập sự cố.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tốc độ phản ứng chớp nhoáng**: Tự động kiểm tra file hash với VirusTotal ngay khi Wazuh phát hiện bất thường.
- **Giảm tải cho đội ngũ SOC**: Tự động hóa việc phân loại mức độ nguy hiểm, tạo Incident trên ServiceNow và gửi cảnh báo trực quan qua Slack.
- **Báo cáo chi tiết chuyên nghiệp**: Tự động tổng hợp thông tin, định dạng HTML và gửi báo cáo qua Gmail cho các chuyên gia phân tích.
- **Hoạt động 24/7 không nghỉ**: Hệ thống túc trực liên tục, không bỏ sót bất kỳ mối đe dọa tiềm ẩn nào.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Hệ thống Wazuh SIEM**: Đã cấu hình để bắn Webhook cảnh báo.
- **Tài khoản / API Key VirusTotal**: Để truy vấn độ uy tín của file hash.
- **Workspace Slack**: Để nhận tin nhắn cảnh báo thời gian thực.
- **ServiceNow**: Tài khoản API để tự động tạo ticket sự cố (Incident).
- **Gmail Account (OAuth2)**: Để gửi email tóm tắt cho đội ngũ phân tích.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy mã JSON của workflow từ nguồn cung cấp, sau đó paste trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống hoạt động trơn tru, các sếp cần cấu hình chính xác các node trọng điểm sau:
- **Wazuh Alert (Webhook)**: Lấy endpoint URL của node này cấu hình ngược lại vào Wazuh SIEM để bắt đầu nhận các tín hiệu cảnh báo FIM qua phương thức `POST` tại đường dẫn `/file_validation`.
- **Extract IOCs & Generate File Summary (Code)**: Các node JavaScript chạy ngầm để bóc tách các thông số quan trọng như SHA256, MD5, tên file, đường dẫn và thông tin agent từ payload của Wazuh, sau đó chuẩn hóa thành dữ liệu JSON sạch.
- **VirusTotal File Hash Validation (HTTP Request)**: Cấu hình kết nối `virusTotalApi` sử dụng API Key cá nhân để gửi request kiểm tra mã hash SHA256/MD5 của tệp tin.
- **Filter Suspicious Files (Switch)**: Thiết lập điều kiện phân loại dựa trên kết quả trả về từ VirusTotal (chia thành luồng an toàn hoặc đáng ngờ).
- **Create File Incident (ServiceNow)**: Chọn credentials `serviceNowBasicApi` và cấu hình thao tác tạo Incident tự động khi phát hiện mã độc.
- **Slack File Alert (Slack)**: Kết nối tài khoản `slackOAuth2Api` để chỉ định kênh (channel) nhận cảnh báo chi tiết.
- **Gmail1 (Gmail)** và **file summary display (HTML)**: Thiết lập tài khoản `gmailOAuth2` để gửi bản tóm tắt định dạng HTML trực quan cho phân tích viên.

#### 3. Kích hoạt ⚡️
- Thực hiện **Test run** với một bản tin cảnh báo mẫu từ Wazuh để kiểm tra thông suốt dữ liệu qua các luồng.
- Sau khi kiểm tra mọi thứ hoạt động hoàn hảo, các sếp bật công tắc **Active** để hệ thống chính thức trực chiến.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm Telegram**: Ngoài Slack, các sếp có thể nhân bản luồng thông báo sang Telegram Bot để nhận cảnh báo ngay trên điện thoại cá nhân.
- **Lưu log vào Google Sheets**: Thêm node Google Sheets để lưu trữ lịch sử mọi cảnh báo phục vụ cho việc kiểm toán định kỳ hàng tháng.
- **Mở rộng Playbook**: Tích hợp thêm bước tự động cô lập (isolate) máy chủ bị nhiễm mã độc thông qua API của EDR hoặc Wazuh Active Response.

### 📌 Kết luận
Workflow này là một mảnh ghép hoàn hảo để tự động hóa quy trình SecOps, giúp tiết kiệm hàng giờ thao tác thủ công mỗi ngày và nâng cao năng lực ứng phó sự cố của tổ chức. Hãy "lên đồ" ngay cho hệ thống của mình để tối ưu hóa an ninh mạng từ hôm nay các sếp nhé!