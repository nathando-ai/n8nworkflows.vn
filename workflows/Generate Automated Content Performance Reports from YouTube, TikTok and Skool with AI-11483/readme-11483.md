---
title: "🚀 Tự động hóa báo cáo hiệu suất nội dung YouTube, TikTok & Skool với AI"
description: "Hướng dẫn cài đặt workflow n8n giúp gom nhóm số liệu kênh mạng xã hội, dùng AI phân tích và gửi báo cáo HTML hàng tuần qua Email tự động 100%."
slug: "tu-dong-hoa-bao-cao-hieu-suat-noi-dung-youtube-tiktok-skool-ai"
tags: [n8n, automation, ai-summarization, market-research, youtube, tiktok, airtable]
keywords: [n8n workflow, tu dong hoa bao cao, youtube analytics, tiktok stats, skool automation, ai content report]
---

# 🚀 Tự động hóa báo cáo hiệu suất nội dung YouTube, TikTok & Skool với AI

Các sếp có đang mệt mỏi mỗi cuối tuần phải ngồi lọ mọ mở từng nền tảng (YouTube, TikTok, cộng đồng Skool) để copy số liệu views, subscribers, likes, comments rồi nhập vào Excel hay Google Sheets để làm báo cáo? Vừa mất thời gian, dễ sai sót lại chẳng có thời gian để sáng tạo nội dung mới!

Đừng lo nữa các sếp ơi! Workflow n8n siêu cấp này sẽ thay các sếp làm trọn gói từ A-Z: tự động thu thập số liệu, lọc video mới trong 7 ngày, tính toán tăng trưởng, nhờ AI (Gemini qua OpenRouter) phân tích chiến lược và gửi thẳng một bản báo cáo HTML cực kỳ đẹp mắt vào Gmail vào mỗi cuối tuần. 

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian:** Không cần thủ công thống kê dữ liệu từ nhiều nền tảng khác nhau mỗi tuần.
- **Báo cáo chuyên nghiệp:** Nhận báo cáo định dạng HTML trực quan, sắc nét ngay trong hòm thư Gmail cá nhân.
- **AI tư vấn chiến lược:** LLM tự động tổng hợp nội dung, transcript video để đánh giá điểm sáng và góp ý cải thiện.
- **Lưu trữ dữ liệu tự động:** Mọi chỉ số quan trọng được cập nhật liên tục vào Airtable để dễ dàng theo dõi historical data.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động trơn tru, các sếp cần chuẩn bị sẵn các tài khoản và credentials sau:
- **Tài khoản n8n** (Self-hosted hoặc Cloud).
- **Tài khoản Airtable** (để lưu trữ database số liệu).
- **Tài khoản Apify** (sử dụng Actor để lấy transcript video YouTube và dữ liệu TikTok).
- **Google Cloud Console Credentials** (YouTube Data API & Gmail OAuth2).
- **OpenRouter API Key** (hoặc OpenAI để chạy model `google/gemini-2.5-flash`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ n8n.io (Link gốc: [Workflow #11483](https://n8n.io/workflows/11483)), sau đó vào giao diện n8n Editor chọn **Add workflow** -> **Import from File** hoặc copy/paste trực tiếp đoạn JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Nodes Airtable (`Create a record`, `Update record`, `Search records`, v.v.):** 
  - Các sếp cần clone Base mẫu của tác giả tại đây: [AI Content Hub Template](https://airtable.com/appkessfths2QABG9/shr1ceynxbhDcTSxB).
  - Kết nối `airtableTokenApi` credential của mình và cập nhật lại Base ID, Table ID cho tất cả các node tương tác với Airtable trong workflow.
- **Nodes HTTP Request & YouTube:** 
  - Điền chính xác các biến URL/ID kênh YouTube, hồ sơ TikTok, và link nhóm Skool của các sếp vào các node thu thập dữ liệu đầu nguồn.
  - Kết nối các credentials cho Apify, YouTube OAuth2, OpenRouter (`openRouterApi`) và Gmail OAuth2 (`gmailOAuth2`).
- **⚠️ LƯU Ý QUAN TRỌNG CHO LẦN CHẠY ĐẦU TIÊN (Baseline Setup):**
  - Hệ thống tính toán tăng trưởng bằng cách đối chiếu với dữ liệu **của tuần trước**. Vì đây là setup mới, dữ liệu tuần trước chưa có.
  - Các sếp cần vào bảng **"Weekly Content KPIs"** trên Airtable của mình, tạo thủ công một dòng mới:
    1. **Cột Week:** Nhập nhãn tuần trước theo chuẩn ISO (Ví dụ hiện tại là tuần 46, hãy nhập `2025-W45`).
    2. **Cột Totals:** Điền thủ công tổng số lượng `YT subs`, `TT followers`, và `Skool members` hiện tại của các sếp làm mốc cơ sở.
    3. Khi workflow chạy tự động vào Chủ Nhật tới, nó sẽ tìm thấy mốc này để tính toán tăng trưởng chính xác!

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (**Test run**) từng nhánh nhỏ (nhánh cập nhật số liệu mỗi 5 phút và nhánh báo cáo hàng tuần qua `Schedule Trigger`) để kiểm tra dữ liệu trả về từ YouTube, TikTok, Skool và Airtable.
- Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để workflow tự động vận hành.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh Chat:** Thêm node **Telegram** hoặc **Slack** ngay sau node AI phân tích (`Generate analysis report`) để nhận ngay bản tóm tắt nhanh trên điện thoại thay vì chỉ đợi email.
- **Lưu trữ Cloud mở rộng:** Ngoài Airtable, các sếp có thể đồng bộ thêm vào **Google Sheets** thông qua node `Google Sheets` để tiện cho việc vẽ biểu đồ trực quan hóa dữ liệu (Data Visualization).
- **Tùy chỉnh Prompt AI:** Vào node `Generate analysis report` (Chain LLM) để tinh chỉnh system prompt theo văn phong mong muốn (ví dụ: chuyên gia marketing nghiêm túc, hoặc phong cách hài hước, thực chiến).

### 📌 Kết luận
Workflow này là một mảnh ghép hoàn hảo giúp tiết kiệm hàng giờ đồng hồ làm báo cáo thủ công mỗi tuần, đồng thời giúp các sếp có cái nhìn sâu sắc dựa trên AI về hiệu suất nội dung của mình. Hãy setup ngay hôm nay để tối ưu hóa quy trình làm sáng tạo nội dung của các sếp nhé!