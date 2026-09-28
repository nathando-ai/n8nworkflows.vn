---
title: "🚀 Tự động giám sát đánh giá thương mại điện tử với MrScraper, GPT-4o-mini, Slack và Notion"
description: "Hướng dẫn xây dựng workflow n8n tự động cào dữ liệu đánh giá sản phẩm, phân tích cảm xúc bằng AI và đồng bộ kết quả về Notion, Slack để nắm bắt phản hồi khách hàng tức thì."
slug: "tu-dong-giam-sat-danh-gia-thuong-mai-dien-tu-n8n"
tags: [n8n, automation, no-code, mrscraper, openai, notion, slack, e-commerce, ai-summarization]
keywords: [n8n workflow, giám sát đánh giá e-commerce, mrscaper n8n, gpt-4o-mini n8n, tự động hóa notion slack, market research]
---

# 🚀 Tự động giám sát đánh giá thương mại điện tử với MrScraper, GPT-4o-mini, Slack và Notion

Việc theo dõi thủ công hàng trăm, hàng nghìn đánh giá (reviews) của khách hàng trên các sàn thương mại điện tử là một "cực hình" đối với các đội ngũ chăm sóc khách hàng, marketing và phát triển sản phẩm. Nếu bỏ lỡ các phản hồi tiêu cực, doanh nghiệp có thể đánh mất uy tín và khách hàng tiềm năng. 

Giải pháp? Workflow n8n tự động hóa 100% này sẽ giúp các sếp cào dữ liệu đánh giá tự động bằng **MrScraper**, dùng **GPT-4o-mini** để phân tích cảm xúc/tóm tắt, sau đó lưu trữ vào **Notion** và bắn thông báo khẩn cấp lên **Slack**. Không cần code phức tạp, vận hành 24/7!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không cần nhân sự ngày ngày đi copy/paste hoặc check từng trang sản phẩm.
- **Phản ứng chớp nhoáng:** Nhận cảnh báo ngay lập tức trên Slack khi có đánh giá tiêu cực (1-2 sao) để xử lý khủng hoảng truyền thông kịp thời.
- **Dữ liệu tập trung:** Tự động tổng hợp toàn bộ đánh giá vào Notion Database giúp dễ dàng phân tích xu hướng thị trường (Market Research).
- **Phân tích thông minh bằng AI:** GPT-4o-mini tự động lọc ý chính, phân loại cảm xúc (tích cực, trung tính, tiêu cực) của khách hàng cực kỳ chuẩn xác.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và credentials sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **MrScraper API Key:** Dùng để thu thập dữ liệu đánh giá từ trang thương mại điện tử.
- **OpenAI API Key:** Sử dụng mô hình `GPT-4o-mini` để tóm tắt và phân tích đánh giá.
- **Notion Integration:** Đã tạo sẵn một Database trong Notion để lưu trữ đánh giá.
- **Slack Bot Token / Webhook:** Để gửi tin nhắn thông báo vào kênh Slack định sẵn.
- **Google Sheets (Tùy chọn):** Nếu các sếp muốn lưu trữ danh sách link sản phẩm cần theo dõi.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow này từ nguồn gốc hoặc copy toàn bộ mã JSON.
- Trong giao diện n8n Editor, bấm vào menu ở góc trên bên phải, chọn **Import from File** hoặc **Import from Clipboard** và dán đoạn mã vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình kỹ các node trọng điểm sau:

- **Schedule Trigger Node:** 
  - Cấu hình tần suất chạy (ví dụ: Chạy mỗi ngày 1 lần vào 8 giờ sáng, hoặc chạy hàng tuần tùy thuộc vào lượng review của sản phẩm).
- **MrScraper Node:** 
  - Kết nối tài khoản thông qua MrScraper API.
  - Điền URL của trang sản phẩm thương mại điện tử cần cào đánh giá và cấu hình các trường dữ liệu mục tiêu (tên khách hàng, số sao, nội dung đánh giá, ngày tháng).
- **Split In Batches Node:** 
  - Giúp chia nhỏ lượng dữ liệu review cào về thành từng batch nhỏ để tránh quá tải API của OpenAI hoặc Notion.
- **LLM Chain & OpenAI Chat Model Nodes:** 
  - Chọn model `gpt-4o-mini`.
  - Viết System Prompt rõ ràng để AI phân tích: *"Hãy đọc đánh giá sản phẩm sau, tóm tắt ý chính trong 1 câu và phân loại cảm xúc thành: Tích cực, Trung tính hoặc Tiêu cực"*.
- **If Node:** 
  - Dùng để lọc điều kiện: Nếu cảm xúc là *Tiêu cực* hoặc số sao $\le 2$, chuyển hướng luồng dữ liệu để gửi cảnh báo khẩn cấp.
- **Notion Node:** 
  - Kết nối tài khoản Notion, chọn Database mục tiêu và map các trường dữ liệu từ MrScraper & OpenAI (Tiêu đề, Nội dung, Đánh giá sao, Kết quả phân tích của AI) vào các cột tương ứng trong Notion.
- **Slack Node:** 
  - Chọn kênh Slack (Channel) nhận thông báo. Định dạng nội dung tin nhắn cảnh báo các review tiêu cực kèm link sản phẩm để đội ngũ CSKH xử lý ngay.

#### 3. Kích hoạt ⚡️
- Bấm nút **Execute Workflow** để chạy thử nghiệm với một lượng dữ liệu nhỏ (Test run) nhằm kiểm tra xem các node truyền dữ liệu chính xác chưa.
- Kiểm tra lại Notion và Slack xem dữ liệu đã đổ về đúng ý chưa.
- Nếu mọi thứ xanh mướt (success), hãy gạt công tắc sang **Active** để hệ thống tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Ngoài Slack, các sếp có thể kết nối thêm node **Telegram** hoặc **Zalo ZNS** để bắn tin nhắn về điện thoại cá nhân khi có đánh giá 1 sao.
- **Báo cáo định kỳ:** Kết hợp thêm node **Google Calendar** hoặc **Email** để gửi báo cáo tổng hợp (Weekly/Monthly Summary) về tình hình sức khỏe thương hiệu qua email cho Ban Giám đốc vào mỗi cuối tuần.
- **Lưu log lỗi:** Thêm một nhánh xử lý lỗi (Error Trigger) để nếu MrScraper lỗi do thay đổi cấu trúc HTML của sàn TMĐT, hệ thống sẽ tự động gửi cảnh báo về Telegram cho kỹ thuật viên xử lý.

### 📌 Kết luận
Giám sát đánh giá khách hàng chưa bao giờ dễ dàng và tự động hóa đến thế. Chỉ với vài bước cấu hình trên n8n kết hợp cùng sức mạnh của AI, các sếp đã tiết kiệm được hàng chục giờ làm việc thủ công mỗi tuần và nắm thế chủ động hoàn toàn trong việc quản trị trải nghiệm khách hàng. Chúc các sếp triển khai thành công!