---
title: "🚀 Tự động giám sát rủi ro chuỗi cung ứng với Claude Sonnet 4.5 và Telegram"
description: "Xây dựng hệ thống cảnh báo rủi ro chuỗi cung ứng tự động 24/7 từ 12 nguồn RSS miễn phí, phân tích thông minh bằng Claude AI và gửi thông báo trực tiếp qua Telegram."
slug: "giam-sat-rui-ro-chuoi-cung-ung-claude-ai-telegram"
tags: [n8n, automation, no-code, claude-ai, telegram, supply-chain, ai-agent]
keywords: [n8n workflow, tự động hóa chuỗi cung ứng, Claude Sonnet 4.5, cảnh báo rủi ro logistics, Telegram alert n8n]
---

# 🚀 Tự động giám sát rủi ro chuỗi cung ứng với Claude Sonnet 4.5 và Telegram

Trong ngành vận tải, logistics và quản lý chuỗi cung ứng, việc cập nhật chậm trễ các sự cố về hàng hải, thời tiết cực đoan, thay đổi chính sách thương mại hoặc gián đoạn hãng tàu có thể gây thiệt hại hàng đống tiền. Các đội ngũ vận hành thường mất rất nhiều thời gian thủ công để rà soát tin tức từ hàng chục nguồn khác nhau.

Workflow này giải quyết trọn vẹn bài toán trên bằng cách tự động hóa 100%: cào tin tức từ các nguồn uy tín, nhờ **Claude Sonnet 4.5** phân tích mức độ nguy hiểm, lọc theo tiêu chí cấu hình và bắn cảnh báo trực quan thẳng vào Telegram của các sếp. Hoàn toàn không cần database phức tạp hay code rườm rà!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Cảnh báo sớm 24/7**: Tự động quét 12 nguồn tin lớn mỗi 6 tiếng (Hàng hải, Hãng tàu, Địa chính trị, Thiên tai).
- **AI thông minh phân tích sâu**: Claude Sonnet 4.5 tự động gán nhãn mức độ rủi ro (1-5), xác định khu vực ảnh hưởng và đề xuất hành động (Theo dõi / Cảnh báo / Leo thang).
- **Lọc thông minh không nhiễu**: Chỉ gửi tin khi đạt ngưỡng rủi ro cấu hình trước, loại bỏ hoàn toàn tin rác.
- **Tiết kiệm tối đa**: Sử dụng dữ liệu static có sẵn của n8n, không tốn chi phí thuê database ngoài hay các API cào dữ liệu đắt đỏ.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Anthropic API Key**: Để sử dụng mô hình Claude Sonnet 4.5 phân tích tin tức.
- **Telegram Bot Token**: Lấy từ `@BotFather` trên Telegram.
- **Telegram Chat ID**: ID của cá nhân hoặc nhóm nhận thông tin cảnh báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ nguồn cung cấp hoặc copy toàn bộ JSON, sau đó paste trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Claude Sonnet (Analyst) & Claude Sonnet (Reporter)**: Kết nối Anthropic API Credential cho cả 2 node AI sub-nodes này (có thể dùng chung 1 credential).
- **Configuration (Node Set)**: Mở node này để tinh chỉnh `severity_threshold` (ngưỡng nghiêm trọng từ 1-5), `watched_dimensions` (các khía cạnh cần theo dõi) và `watched_regions` (khu vực quan tâm) cho phù hợp với doanh nghiệp của các sếp.
- **Send Telegram Alert (Node Telegram)**: Kết nối Telegram Bot Credential và điền `TELEGRAM_CHAT_ID` vào cấu hình node hoặc cài biến môi trường (environment variable) tương ứng trong n8n.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** để chạy thử nghiệm thủ công với dữ liệu mẫu từ các nguồn RSS.
- Kiểm tra kết quả trả về trên Telegram, nếu mọi thứ mượt mà, hãy gạt công tắc sang **Active** để hệ thống tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa kênh thông báo**: Thay vì chỉ dùng Telegram, các sếp có thể nhân bản node cuối để bắn thêm thông báo qua Slack, Discord hoặc Email.
- **Lưu trữ lịch sử**: Kết nối thêm một node Google Sheets hoặc Airtable ngay trước bước gửi Telegram để lưu lại toàn bộ lịch sử rủi ro phục vụ việc lập báo cáo định kỳ hàng tháng.
- **Mở rộng nguồn tin**: Dễ dàng thêm các RSS feed chuyên ngành mới vào nhóm nguồn tin hiện có (Hàng hải, Cảng biển, Địa chính trị) để tăng độ phủ thông tin.

### 📌 Kết luận
Workflow này là một "trợ lý AI" đắc lực giúp các nhà quản lý chuỗi cung ứng nắm bắt rủi ro trước khi chúng trở thành khủng hoảng. Hãy import ngay vào n8n và tối ưu hóa hệ thống cảnh báo của doanh nghiệp các sếp ngày hôm nay!