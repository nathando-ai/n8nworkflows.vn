---
title: "🛡️ Tự động kiểm tra danh tiếng IP và cảnh báo SOC với Splunk, VirusTotal và AlienVault trên n8n"
description: "Hướng dẫn xây dựng hệ thống SecOps tự động hóa quy trình phân tích mối đe dọa (Threat Intel), tích hợp Splunk, VirusTotal, AlienVault, Slack và ServiceNow."
slug: "tu-dong-kiem-tra-danh-tieu-ip-soc-alerts-splunk-virustotal-alienvault"
tags: [n8n, automation, secops, cybersecurity, splunk, virustotal, incident-response]
keywords: [n8n workflow, SecOps automation, kiểm tra danh tiếng IP, Splunk webhook, VirusTotal API, AlienVault OTX, ServiceNow incident]
---

# 🛡️ Tự động hóa SecOps: Kiểm tra danh tiếng IP & Cảnh báo SOC với Splunk, VirusTotal và AlienVault

Trong môi trường vận hành an ninh mạng (SOC), việc các kỹ sư phải liên tục tra cứu thủ công danh tiếng của một địa chỉ IP đáng ngờ từ các hệ thống SIEM (như Splunk) lên các nền tảng Threat Intel (như VirusTotal, AlienVault) gây mất rất nhiều thời gian. Quy trình thủ công này làm chậm trễ thời gian phản hồi sự cố (Incident Response Time).

Workflow n8n này sẽ giúp các sếp tự động hóa 100% quy trình SecOps: Nhận cảnh báo từ Splunk, trích xuất IOC (Indicators of Compromise), làm giàu dữ liệu từ nhiều nguồn, đánh giá mức độ nguy hiểm, tự động tạo Incident trên ServiceNow và bắn cảnh báo ngay lập tức qua Slack cùng Gmail.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Chuyển đổi quy trình thủ công 15-30 phút thành vài giây ngay khi có cảnh báo từ SIEM.
- **Làm giàu dữ liệu thông minh (Threat Enrichment):** Kết hợp đồng thời dữ liệu từ VirusTotal và AlienVault OTX để có cái nhìn toàn diện về IP độc hại.
- **Phản hồi sự cố tức thì:** Tự động tạo ticket trên ServiceNow, đồng thời đẩy thông báo đỏ qua Slack và gửi báo cáo HTML chi tiết qua Gmail cho đội ngũ SOC.
- **Hoạt động liên tục 24/7:** Đảm bảo không bỏ sót bất kỳ mối đe dọa nào ngay cả ngoài giờ hành chính.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Hệ thống **Splunk** (hoặc SIEM tương đương) có khả năng cấu hình Webhook.
- Tài khoản và API Key của **VirusTotal**.
- Tài khoản và API Key của **AlienVault OTX**.
- Tài khoản **ServiceNow** (dùng cho việc tạo Incident tự động).
- Workspace **Slack** (để gửi thông báo cảnh báo kênh SOC).
- Tài khoản **Gmail / Google Workspace** (để gửi báo cáo tổng hợp dạng HTML).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể sao chép đoạn mã JSON của workflow này và dán trực tiếp vào n8n Editor của mình, hoặc import file JSON tải từ kho lưu trữ n8n chính thức (`Workflow ID: 6037`).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống hoạt động trơn tru, các sếp cần cấu hình chính xác các node sau:

- **Splunk Alert (`webhook`):** 
  - Cấu hình endpoint webhook trong Splunk trỏ tới URL Webhook của node này (`/webhook/e645d98e-f80c-47e5-b96e-762c96f3db76`).
- **Extract IOCs (`code`):** 
  - Kiểm tra lại đoạn mã trích xuất để đảm bảo cấu trúc JSON payload gửi từ Splunk khớp với trường `source IP` và `event reason` mà node này đang bóc tách.
- **VirusTotal IP reputation check (`httpRequest`):** 
  - Chọn credential `virusTotalApi` và điền API Key hợp lệ của VirusTotal.
- **AlienVault Lookup (`httpRequest`):** 
  - Chọn credential `alienVaultApi` và cấu hình khóa API của AlienVault OTX.
- **Filter Suspicious IPs (`switch`):** 
  - Thiết lập điều kiện lọc dựa trên điểm số đánh giá từ node xử lý dữ liệu trước đó (ví dụ: số lượng engine phát hiện độc hại trên VirusTotal > ngưỡng cho phép).
- **Create IP Incident (`serviceNow`):** 
  - Chọn credential `serviceNowBasicApi`, cấu hình đúng instance ServiceNow của doanh nghiệp và thiết lập `operation: create`, `resource: incident`.
- **Slack IP Alert (`slack`):** 
  - Chọn credential `slackOAuth2Api` và chọn kênh (channel) nhận cảnh báo SOC chuyên dụng.
- **Gmail (`gmail`):** 
  - Chọn credential `gmailOAuth2` và cấu hình người nhận là hòm thư trực trực chiến của đội ngũ SOC.

#### 3. Kích hoạt ⚡️
- Gửi một sự kiện giả lập (Test payload) từ Splunk hoặc dùng tính năng **Execute Node** tại node Webhook để kiểm tra luồng dữ liệu.
- Kiểm tra kết quả trả về ở các nhánh Slack, ServiceNow và Gmail.
- Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để workflow chính thức trực chiến 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Có thể bổ sung thêm node Telegram hoặc Microsoft Teams để đa dạng hóa kênh nhận cảnh báo cho các kỹ sư trực ca.
- **Lưu trữ lịch sử Threat Intel:** Thêm node Google Sheets hoặc cơ sở dữ liệu (PostgreSQL/MongoDB) để lưu lại toàn bộ lịch sử các IP độc hại nhằm phục vụ công tác điều tra chuyên sâu (Forensics) về sau.
- **Tự động chặn IP (Auto-Mitigation):** Kết hợp thêm API của Firewall (như Palo Alto, Cloudflare, hoặc AWS Security Groups) để tự động block IP độc hại ngay lập tức nếu điểm số nguy hiểm đạt mức tối đa.

### 📌 Kết luận
Việc tự động hóa quy trình phân tích mối đe dọa với n8n, Splunk, VirusTotal và AlienVault không chỉ giúp tối ưu hóa thời gian xử lý sự cố của đội ngũ SOC mà còn nâng cao tư thế chủ động phòng thủ trước các cuộc tấn công mạng ngày càng tinh vi. Hãy triển khai ngay hôm nay để giải phóng sức lao động cho các kỹ sư an ninh mạng của các sếp!