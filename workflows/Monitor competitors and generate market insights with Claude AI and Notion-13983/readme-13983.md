---
title: "🚀 Tự động theo dõi đối thủ cạnh tranh và phân tích thị trường với Claude AI & Notion"
description: "Xây dựng hệ thống tự động quét website đối thủ hàng tuần, phát hiện thay đổi nội dung, phân tích bằng Claude AI và lưu trữ vào Notion, kết hợp thông báo Slack và Gmail."
slug: "tu-dong-theo-doi-doi-thu-canh-tranh-claude-ai-notion"
tags: [n8n, automation, no-code, claude-ai, notion, market-research]
keywords: [n8n workflow, theo dõi đối thủ cạnh tranh, phân tích thị trường, claude ai, notion automation, competitive intelligence]
---

# 🚀 Tự động theo dõi đối thủ cạnh tranh và phân tích thị trường với Claude AI & Notion

Các sếp có đang tốn hàng giờ mỗi tuần để thủ công truy cập website của đối thủ, xem họ thay đổi giá cả, cập nhật tính năng gì mới hay tung ra chiến dịch nào không? Công việc này không chỉ nhàm chán mà còn cực kỳ dễ bỏ sót những thông tin quan trọng.

Giải pháp ở đây là để n8n thay các sếp làm việc đó! Workflow tuyệt vời này sẽ tự động hóa 100% quy trình quét website đối thủ định kỳ, sử dụng thuật toán hash để phát hiện thay đổi nội dung, nhờ **Claude AI** phân tích chiều sâu và lưu trữ kết quả vào **Notion**, đồng thời bắn thông báo khẩn cấp qua **Slack** hoặc tổng hợp báo cáo qua **Gmail**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không cần thủ công check website đối thủ hàng tuần nữa.
- **Phát hiện chớp nhoáng:** Nhận cảnh báo ngay lập tức qua Slack khi đối thủ có thay đổi lớn (như đổi bảng giá, tung tính năng mới).
- **Phân tích chuyên sâu:** AI đọc hiểu và tóm tắt những tác động của sự thay đổi đó đối với chiến lược kinh doanh của sếp.
- **Kho lưu trữ thông minh:** Tự động đồng bộ toàn bộ dữ liệu tình báo thị trường (Market Intelligence) vào Notion cực kỳ khoa học.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ TRƯỚC KHI "LÊN ĐỒ"]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Anthropic Claude API Key** (cho model `claude-3-5-sonnet-20241022`).
- **Notion Integration Token** và một Database được tạo sẵn.
- **Slack Workspace** và Bot Token/Webhook để bắn thông báo.
- **Gmail Account** (hoặc SMTP) để gửi báo cáo tuần.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này hoặc copy toàn bộ mã JSON và dán trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình kỹ các node sau để hệ thống chạy mượt mà:
- **Set competitor URLs (`Set competitor URLs`):** Thêm danh sách các URL website, trang bảng giá (pricing), hoặc trang tính năng của đối thủ mà các sếp muốn theo dõi.
- **Claude AI Model (`Claude AI model` & `Analyze competitor changes`):** Kết nối thông tin API Key của Anthropic và chọn model `claude-3-5-sonnet-20241022` để đảm bảo chất lượng phân tích tốt nhất.
- **Lưu Notion (`Save to Notion database`):** Chuẩn bị sẵn một Database trên Notion với các thuộc tính (properties): *Competitor (text)*, *URL (url)*, *Content Hash (text)*, *AI Analysis (text)*, *Scan Date (date)*. Sau đó map các trường này vào node Notion.
- **Kênh thông báo (`Send Slack alert` & `Email weekly report`):** Cấu hình kênh Slack nhận tin khẩn cấp và danh sách email nhận báo cáo tổng hợp hàng tuần.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (**Test run**) bằng nút thực thi để kiểm tra xem dữ liệu có đổ về Notion và Slack suôn sẻ không.
- Sau khi test OK, bật công tắc **Active** để workflow tự động chạy theo lịch hẹn (Weekly Schedule Trigger).

### ✍️ Mẹo & gợi ý nâng cao
- **Đa dạng hóa kênh thông báo:** Thay vì chỉ dùng Slack, các sếp có thể tích hợp thêm Telegram Bot hoặc Microsoft Teams để đội ngũ Sales/Marketing nắm bắt thông tin nhanh chóng.
- **Tùy biến Prompt AI:** Tinh chỉnh prompt trong node `Analyze competitor changes` để Claude tập trung khai thác sâu hơn vào khía cạnh giá cả, UI/UX hoặc thông điệp marketing của đối thủ.
- **Mở rộng tần suất:** Nếu đối thủ thường xuyên thay đổi chiến lược, các sếp có thể đổi `Weekly competitor scan` thành Daily (hàng ngày) thông qua Schedule Trigger.

### 📌 Kết luận
Với workflow này, các sếp sẽ luôn đi trước đối thủ một bước nhờ nắm bắt kịp thời mọi biến động trên thị trường mà không tốn chút sức lực thủ công nào. Hãy cài đặt ngay hôm nay để tối ưu hóa năng lực cạnh tranh cho doanh nghiệp!