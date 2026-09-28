---
title: "🐾 [Tự động hóa 100% không code] Gửi tin nhắn sức khỏe thú cưng cá nhân hóa hàng tuần với GPT-4o-mini, Gmail và Google Sheets"
description: "Hướng dẫn chi tiết cách tự động gửi tin nhắn sức khỏe thú cưng cá nhân hóa hàng tuần cho chủ sở hữu bằng cách kết hợp GPT-4o-mini, Gmail và Google Sheets trong n8n"
slug: "tu-dong-hoa-gui-tin-nhan-suc-khoe-thu-cung-hang-tuan"
tags: [n8n, automation, no-code, google-sheets, gmail, ai, openai]
keywords: [n8n workflow, tự động hóa, google sheets, gmail, openai, sức khỏe thú cưng]
---

# 🐾 [Tự động hóa 100% không code] Gửi tin nhắn sức khỏe thú cưng cá nhân hóa hàng tuần với GPT-4o-mini, Gmail và Google Sheets

[Các sếp đang làm việc với thú cưng thường gặp khó khăn khi phải gửi tin nhắn sức khỏe cá nhân hóa hàng tuần cho hàng trăm chủ sở hữu. Việc này tốn thời gian và công sức đáng kể, đồng thời dễ gây lỗi và không nhất quán. Workflow này giúp các sếp tự động hóa toàn bộ quy trình này chỉ trong vài phút, đảm bảo tin nhắn được cá nhân hóa, chính xác và gửi đúng thời gian.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động gửi tin nhắn hàng tuần mà không cần can thiệp thủ công.
- **Cá nhân hóa hoàn hảo**: Tin nhắn được tạo ra dựa trên thông tin cụ thể của từng thú cưng (loại, tuổi, quốc gia).
- **Chính xác và nhất quán**: Dữ liệu được xử lý và gửi một cách tự động, giảm thiểu lỗi.
- **Hoạt động liên tục**: Workflow được kích hoạt tự động vào mỗi thứ Hai lúc 9 giờ sáng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Google Sheets**: Bảng dữ liệu chứa thông tin thú cưng (Email, Owner_Name, Pet_Name, Pet_Type, Date_of_Birth, Country, Status, Last_Email_Sent).
- **OpenAI API**: Tài khoản OpenAI để sử dụng GPT-4o-mini.
- **Gmail OAuth2**: Tài khoản Gmail để gửi email.
- **SendGrid (tùy chọn)**: Tài khoản SendGrid để gửi email (nếu không sử dụng Gmail).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/9714](https://n8n.io/workflows/9714).
2. Nhấn nút **Download** để tải file JSON.
3. Trong n8n Editor, nhấn vào **Import from File** và chọn file JSON vừa tải về.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Load Pet Info"**:
   - Chọn **Google Sheets OAuth2 API** credentials.
   - Điền **Spreadsheet ID** và **Sheet Name** chứa thông tin thú cưng.

2. **Node "Generate Personalized Tip"**:
   - Chọn **OpenAI API** credentials.
   - Đảm bảo **Model** được đặt là **gpt-4o-mini**.

3. **Node "Send Health Tip using Gmail"**:
   - Chọn **Gmail OAuth2** credentials.
   - Điền **From Email** và **Subject** cho email.

4. **Node "Update Last_Email_Sent Date"**:
   - Chọn **Google Sheets OAuth2 API** credentials.
   - Điền **Spreadsheet ID** và **Sheet Name** để cập nhật ngày gửi email.

5. **Node "Log to Email_Log Sheet"**:
   - Chọn **Google Sheets OAuth2 API** credentials.
   - Điền **Spreadsheet ID** và **Sheet Name** để lưu log email.

6. **Node "Weekly Trigger (Mondays 9am)"**:
   - Đảm bảo **Timezone** được đặt đúng.
   - Có thể điều chỉnh **Schedule** nếu cần gửi vào thời gian khác.

#### 3. Kích hoạt ⚡️
1. **Test run dữ liệu mẫu**:
   - Chạy workflow với dữ liệu mẫu để kiểm tra tính năng.
2. **Bật Active workflow**:
   - Nhấn **Activate** để kích hoạt workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Telegram**: Thêm node để gửi thông báo qua Slack hoặc Telegram khi workflow hoàn thành.
- **Lưu log chi tiết**: Thêm node để lưu log chi tiết hơn vào Google Sheets.
- **Gửi báo cáo định kỳ**: Thêm node để gửi báo cáo tổng hợp hàng tháng về số lượng email đã gửi.
- **Tích hợp với các dịch vụ khác**: Kết hợp với Airtable, Typeform hoặc các dịch vụ tương tự để quản lý dữ liệu.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quy trình gửi tin nhắn sức khỏe thú cưng hàng tuần một cách dễ dàng và hiệu quả. Với việc kết hợp GPT-4o-mini, Gmail và Google Sheets, các sếp có thể đảm bảo tin nhắn được cá nhân hóa, chính xác và gửi đúng thời gian. Hãy áp dụng ngay để tiết kiệm thời gian và công sức cho công việc hàng ngày!