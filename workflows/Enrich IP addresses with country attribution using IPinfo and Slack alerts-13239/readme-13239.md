---
title: "🚀 Tự động tra cứu thông tin IP & cảnh báo Slack với IPinfo và n8n"
description: "Xây dựng hệ thống SecOps tự động hóa 100% để enrich địa chỉ IP, tra cứu vị trí địa lý, ASN và gửi cảnh báo trực tiếp lên Slack."
slug: "tu-dong-tra-cuu-thong-tin-ip-slack-ipinfo"
tags: [n8n, automation, secops, slack, ipinfo, cybersecurity]
keywords: [n8n workflow, tu dong hoa secops, tra cuu ip, ipinfo api, canh bao slack, an ninh mang]
---

# 🚀 Tự động tra cứu thông tin IP & cảnh báo Slack với IPinfo

Trong công tác vận hành hệ thống và an ninh mạng (SecOps), các kỹ sư SOC thường xuyên phải đối mặt với việc kiểm tra thủ công hàng loạt địa chỉ IP đáng ngờ từ các cảnh báo bảo mật, tường lửa hoặc log hệ thống. Việc này vừa mất thời gian, vừa làm chậm trễ quá trình phản ứng sự cố (Incident Response).

Workflow này ra đời như một giải pháp tự động hóa toàn diện giúp các sếp giải quyết triệt để vấn đề trên. Hệ thống sẽ tự động tiếp nhận địa chỉ IP, kiểm tra tính hợp lệ, loại bỏ các dải IP nội bộ (private IP), tiến hành tra cứu thông tin định danh (Geographic & ASN Lookup) qua dịch vụ IPinfo và ngay lập tức gửi cảnh báo chi tiết lên kênh Slack, đồng thời trả về kết quả JSON chuẩn hóa.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Không còn cảnh phải copy từng IP tra cứu thủ công trên các trang web GeoIP.
- **Lọc thông minh**: Tự động nhận diện và loại bỏ các dải IP private (LAN) tránh làm nhiễu loạn hệ thống.
- **Cảnh báo tức thì**: Gửi thông tin chi tiết về quốc gia, nhà mạng (ISP), mã định danh mạng (ASN) và mức độ rủi ro thẳng lên Slack.
- **Tích hợp API linh hoạt**: Nhận dữ liệu đầu vào qua Webhook từ bất kỳ hệ thống, ứng dụng hoặc chatbot nào.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance**: Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Slack Account**: Tài khoản có quyền cấu hình Bot/App và kết nối Webhook hoặc Slack API trong n8n.
- **IPinfo Account (Tùy chọn)**: Chuẩn bị API Key nếu muốn tăng giới hạn tra cứu (Workflow mặc định có thể sử dụng các nguồn public/open-source IP intelligence).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy toàn bộ mã JSON từ n8n template gốc.
- Mở n8n Editor, chọn **Add workflow** -> **Import from File** hoặc dán trực tiếp vào giao diện.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần chú ý cấu hình kỹ các node sau trong workflow:
- **Weebhook - Receive IP Input**: Node này nhận request POST chứa IP. Hãy chú ý đường dẫn endpoint (`/ip-enrichment`) để trỏ các hệ thống nguồn gửi dữ liệu vào đây.
- **Validate IP Address & Check Private / Internal IP**: Các node **Code** (JavaScript) thực hiện việc validate định dạng IP và kiểm tra xem có thuộc dải private hay không. Các sếp có thể tinh chỉnh logic nếu hệ thống sử dụng các dải mạng nội bộ đặc thù.
- **Enrich IP (Geo & ASN Lookup)**: Node **HTTP Request** gọi đến dịch vụ IP intelligence để lấy thông tin địa lý và mạng. Nếu dùng IPinfo, hãy cấu hình Header kèm API Key tại đây.
- **Slack Alert: IP Enrichment Result**: Node **Slack** yêu cầu kết nối `slackApi Credentials`. Các sếp hãy chọn đúng Channel mà Bot sẽ bắn tin nhắn cảnh báo kết quả phân tích IP.

#### 3. Kích hoạt ⚡️
- Sử dụng công cụ Test trên n8n, gửi một lệnh `POST` mẫu kèm tham số `ip` qua Postman hoặc cURL tới Webhook URL.
- Kiểm tra kết quả trả về ở các nhánh `If IP is Valid` và `If IP is Private`.
- Nếu mọi thứ mượt mà, gạt công tắc sang **Active** để chính thức đưa workflow vào vận hành thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Điểm uy tín (Reputation Scores)**: Kết hợp thêm các API threat intelligence (như AbuseIPDB, VirusTotal) vào chuỗi enrich để đánh giá mức độ nguy hiểm của IP chính xác hơn.
- **Logic rủi ro theo quốc gia**: Bổ sung node Switch/If để phân loại mức độ rủi ro dựa trên quốc gia xuất xứ của IP (Ví dụ: Cảnh báo đỏ nếu IP đến từ các quốc gia ngoài vùng kinh doanh).
- **Tích hợp SIEM/Log**: Lưu trữ toàn bộ lịch sử truy vấn IP vào Google Sheets hoặc Database để phục vụ việc kiểm tra và audit bảo mật về sau.

### 📌 Kết luận
Workflow **Enrich IP addresses with country attribution using IPinfo and Slack alerts** là một mảnh ghép SecOps cực kỳ gọn nhẹ nhưng mang lại hiệu quả cao, giúp tự động hóa khâu trinh sát và định danh IP đầu vào cho đội ngũ vận hành. Hãy "lên đồ" ngay hôm nay để tiết kiệm hàng giờ thao tác thủ công mỗi tuần cho đội ngũ của các sếp!