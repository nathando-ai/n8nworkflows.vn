---
title: "🤖 [Tự động hóa chuyển đổi Bot-Human trong cuộc gọi bán hàng qua Telegram]"
description: "Hướng dẫn tự động chuyển đổi giữa bot AI và nhân viên hỗ trợ trong cuộc gọi bán hàng qua Telegram, giúp tối ưu hóa quy trình và cải thiện trải nghiệm khách hàng."
slug: "tu-dong-hoa-chuyen-doi-bot-human-trong-cuoc-goi-ban-hang-qua-telegram"
tags: [n8n, automation, no-code, telegram, ai, sales, chatbot]
keywords: [n8n workflow, tự động hóa, chatbot bán hàng, telegram, ai, sales automation]
---

# 🤖 Tự động hóa chuyển đổi Bot-Human trong cuộc gọi bán hàng qua Telegram

[Khi làm thủ công, các sếp phải chuyển đổi giữa bot AI và nhân viên hỗ trợ trong các cuộc gọi bán hàng qua Telegram rất tốn thời gian và dễ gây nhầm lẫn. Workflow này giúp tự động hóa quy trình này 100% không cần code, tối ưu hóa quy trình và cải thiện trải nghiệm khách hàng.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động chuyển đổi giữa bot AI và nhân viên hỗ trợ trong các cuộc gọi bán hàng qua Telegram
- Tối ưu hóa quy trình bán hàng với các bước onboarding và after-sales tự động
- Cải thiện trải nghiệm khách hàng với các cuộc trò chuyện được quản lý tốt hơn
- Tiết kiệm thời gian và công sức cho nhân viên hỗ trợ
- Tăng độ chính xác trong việc thu thập thông tin khách hàng
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Telegram và API key cho Telegram
- Tài khoản OpenAI và API key cho OpenAI
- Redis server để quản lý trạng thái phiên
- ID của nhân viên hỗ trợ trên Telegram
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấp vào nút "Import from URL" và dán link: https://n8n.io/workflows/3350
3. Hoặc tải file JSON từ link trên và import thủ công

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Telegram Trigger**:
   - Chọn credentials cho Telegram API
   - Đảm bảo bot của bạn đã được thêm vào nhóm/channel cần theo dõi

2. **Redis Nodes**:
   - Tạo credentials cho Redis server
   - Đảm bảo Redis server đang chạy và có thể truy cập từ n8n

3. **OpenAI Nodes**:
   - Tạo credentials cho OpenAI API
   - Chọn model phù hợp (gpt-4o-mini trong workflow này)

4. **Human Handoff**:
   - Thêm ID của nhân viên hỗ trợ vào node "Human Handoff using Send and Wait"
   - Đảm bảo nhân viên có thể nhận và trả lời các tin nhắn từ bot

5. **Information Extractor**:
   - Cấu hình các trường thông tin cần thu thập từ khách hàng
   - Điều chỉnh prompt trong node "Information Extractor" nếu cần

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu để đảm bảo tất cả các node hoạt động đúng cách
2. Kiểm tra chuyển đổi giữa bot và nhân viên hỗ trợ
3. Bật Active workflow khi đã sẵn sàng triển khai

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với CRM**:
   - Thêm node để lưu trữ thông tin khách hàng vào CRM sau khi thu thập xong
   - Tự động cập nhật trạng thái khách hàng trong CRM

2. **Báo cáo và phân tích**:
   - Thêm node để gửi báo cáo hàng ngày về các cuộc trò chuyện
   - Phân tích hiệu suất của bot và nhân viên hỗ trợ

3. **Tích hợp với các kênh khác**:
   - Kết nối với Slack hoặc Email để thông báo khi có cuộc gọi cần chuyển đổi
   - Tự động chuyển đổi giữa các kênh liên lạc khác nhau

4. **Tối ưu hóa bộ nhớ**:
   - Thiết lập thời gian hết hạn cho các phiên trò chuyện trong Redis
   - Xóa các phiên trò chuyện cũ định kỳ để tiết kiệm tài nguyên

### 📌 Kết luận
Workflow này cung cấp một giải pháp toàn diện để tự động hóa chuyển đổi giữa bot AI và nhân viên hỗ trợ trong các cuộc gọi bán hàng qua Telegram. Với các tính năng quản lý trạng thái phiên, thu thập thông tin khách hàng và chuyển đổi tự động, các sếp có thể tối ưu hóa quy trình bán hàng và cải thiện trải nghiệm khách hàng một cách hiệu quả. Hãy áp dụng ngay để nâng cao hiệu suất kinh doanh của mình!