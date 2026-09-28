---
title: "🚀 Tự động tạo báo cáo phân tích đối thủ bằng GPT-4, Apify và Google Docs"
description: "Hướng dẫn xây dựng workflow n8n tự động cào dữ liệu đối thủ qua Apify, phân tích chiến lược bằng OpenAI GPT-4, tạo Google Docs và gửi thông báo qua Slack."
slug: "tao-bao-cao-phan-tich-doi-thu-tu-dong-n8n-gpt4-apify"
tags: [n8n, automation, openAi, apify, googleDocs, slack, ai-summarization]
keywords: [n8n workflow, phân tích đối thủ, apify n8n, openai gpt-4, google docs automation, tự động hóa marketing]
---

# 🚀 Tự động hóa tạo báo cáo phân tích đối thủ cạnh tranh với AI, Apify và Google Docs

Trong thời2 đại số, việc nắm bắt thông tin và chiến lược của đối thủ cạnh tranh là chìa khóa sống còn. Tuy nhiên, quy trình làm thủ công như tìm kiếm, tổng hợp dữ liệu, phân tích số liệu và viết báo cáo thường tiêu tốn hàng giờ đồng hồ của đội ngũ Marketing và Sales. 

Đừng để những công việc lặp đi lặp lại làm giảm tốc độ phát triển của doanh nghiệp! Bài viết này sẽ hướng dẫn các sếp thiết lập một workflow n8n hoàn toàn tự động: cào dữ liệu đối thủ qua Apify, dùng trí tuệ nhân tạo GPT-4 để phân tích chiến lược chuyên sâu, tự động xuất file Google Docs và gửi thông báo trực tiếp lên Slack cho team.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Thay vì mất cả ngày để tổng hợp và viết báo cáo thủ công, AI sẽ thay bạn hoàn thành chỉ trong vài phút.
- **Phân tích đa chiều, sâu sắc:** Kết hợp sức mạnh của GPT-4 (`The Report Generator` và `The Strategic Analyst`) để đưa ra các nhận định chiến lược sắc bén.
- **Lưu trữ chuyên nghiệp:** Tự động tạo bản báo cáo hoàn chỉnh trên Google Docs với định dạng chuẩn mực.
- **Cập nhật tức thời:** Gửi link báo cáo trực tiếp vào kênh Slack của team ngay khi hoàn thành (`Deliver Report to Team`).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị sẵn các tài khoản và API Keys sau:
- **n8n Instance:** Đã cài đặt sẵn (Cloud hoặc Self-hosted).
- **Apify Account:** Tài khoản và API Token để cào dữ liệu web/mạng xã hội của đối thủ.
- **OpenAI Account:** API Key có quyền sử dụng GPT-4.
- **Google Account:** Kết nối OAuth2 với n8n để tạo file trên Google Docs.
- **Slack Workspace:** Token/Webhook để gửi tin nhắn thông báo vào kênh tương ứng.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow này hoặc sao chép mã nguồn JSON.
- Trong giao diện n8n Editor, chọn **Add workflow** -> **Import from File** (hoặc dán trực tiếp bằng phím tắt `Ctrl + V`).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 7 nodes chính. Các sếp cần cấu hình kỹ các điểm sau để chạy mượt mà:

- **Node `When clicking ‘Execute workflow’` (manualTrigger):** 
  - Đây là điểm khởi đầu thủ công. Các sếp có thể thay thế bằng *Schedule Trigger* nếu muốn workflow chạy định kỳ hàng tuần/hàng tháng.
- **Node `Apify` (httpRequest):** 
  - Nhập Apify API Token của các sếp vào phần Header.
  - Cấu hình URL endpoint và Actor ID của Apify để cào đúng nguồn dữ liệu đối thủ cần phân tích.
- **Node `Data Aggregation` (code):** 
  - Node này dùng mã JavaScript/Python để làm sạch và gom nhóm dữ liệu thô từ Apify trước khi đẩy sang AI.
- **Node `The Report Generator` & `The Strategic Analyst` (openAi):** 
  - Chọn Credentials OpenAI đã kết nối.
  - Tùy chỉnh System Prompt cho từng node để định hướng AI viết báo cáo theo đúng văn phong và cấu trúc mong muốn của công ty.
- **Node `Create Report` (googleDocs):** 
  - Chọn Google Docs Credentials.
  - Chỉ định thư mục lưu trữ file trên Google Drive và ánh xạ nội dung từ AI trả về vào tài liệu mới.
- **Node `Deliver Report` (slack):** 
  - Chọn Slack Credentials, chọn kênh (Channel) nhận tin nhắn và cấu hình template thông báo kèm đường dẫn Google Docs vừa tạo.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để test thử với dữ liệu mẫu xem hệ thống chạy có trơn tru không.
- Kiểm tra kết quả trên Google Docs và Slack.
- Nếu mọi thứ hoàn hảo, bật nút **Active** ở góc trên cùng bên phải để workflow tự động hóa hoạt động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Webhook/Form:** Thay vì chạy thủ công, hãy kết nối node *Webhook* hoặc *Google Forms* để đội ngũ sales/marketing chỉ cần nhập tên đối thủ vào form là hệ thống tự khởi chạy.
- **Đa kênh thông báo:** Ngoài Slack, có thể bổ sung thêm node Telegram hoặc Email để gửi báo cáo cho Ban Giám đốc.
- **Lưu lịch sử vào Database:** Thêm node *Google Sheets* hoặc *Supabase* để lưu lại lịch sử các lần phân tích đối thủ nhằm theo dõi biến động theo thời gian.

### 📌 Kết luận
Việc phân tích đối thủ cạnh tranh chưa bao giờ dễ dàng và tự động đến thế nhờ sự kết hợp giữa n8n, Apify và OpenAI. Hãy triển khai ngay template này để tối ưu hóa năng lực nghiên cứu thị trường cho doanh nghiệp của các sếp! Chúc các sếp thao tác thành công!