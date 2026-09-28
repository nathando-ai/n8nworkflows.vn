---
title: "🚀 Tự động ghép nối nhà tài trợ sự kiện thông minh với Google Sheets, GPT-4o và Gmail"
description: "Hướng dẫn xây dựng agent AI tự động phân tích nhà tài trợ, chấm điểm gói tài trợ bằng GPT-4o, gửi email cá nhân hóa và lưu log kết quả vào Google Sheets."
slug: "tu-dong-ghep-noi-nha-tai-tro-su-kien-voi-ai-gpt4o-gmail"
tags: [n8n, automation, ai, openai, google-sheets, gmail]
keywords: [n8n workflow, ai matching sponsor, tự động hóa sự kiện, gpt-4o automation, google sheets gmail n8n]
---

# 🚀 Tự động ghép nối nhà tài trợ sự kiện thông minh với Google Sheets, GPT-4o và Gmail

Các sếp tổ chức sự kiện chắc chắn hiểu rõ cảm giác "đau đầu" khi phải ngồi lọc danh sách hàng chục nhà tài trợ tiềm năng, đối chiếu ngân sách, ngành nghề và mục tiêu của họ với các gói tài trợ khác nhau. Việc này vừa mất thời gian, vừa dễ bỏ sót cơ hội vàng.

Đừng lo, workflow n8n cực đỉnh từ tác giả Milo Bravo này sẽ giúp các sếp giải quyết triệt để bài toán trên bằng cách tự động hóa 100% quy trình: Đọc dữ liệu từ Google Sheets, nhờ **GPT-4o** phân tích và chấm điểm độ phù hợp, tự động gửi email chào mời qua **Gmail** và lưu lịch sử vào bảng tính mà không cần viết một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn phải thủ công so khớp từng nhà tài trợ với từng gói tài trợ (Package).
- **Cá nhân hóa đỉnh cao:** AI tự động đề xuất top 3 gói phù hợp nhất kèm theo lý do cụ thể, giúp email gửi đi có tỷ lệ chuyển đổi cao hơn hẳn.
- **Lọc thông minh chống rác:** Chỉ gửi email khi điểm số phù hợp vượt ngưỡng tiêu chuẩn (Score > 7).
- **Quản lý tập trung:** Toàn bộ lịch sử kết quả ghép nối được tự động ghi lại vào Google Sheets để team sales dễ dàng theo dõi.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động trơn tru, các sếp cần chuẩn bị sẵn:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Google Sheets:** 2 file hoặc 2 sheet chứa danh sách Sponsors (Name, Industry, Budget, Goals, OwnerEmail) và Packages (Name, Price, Benefits).
- **OpenAI API Key:** Để sử dụng sức mạnh của GPT-4o trong việc chấm điểm và phân tích.
- **Gmail Account / OAuth2:** Để gửi email tự động tới nhà tài trợ.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow này từ kho lưu trữ n8n (Link gốc: [n8n.io/workflows/12620](https://n8n.io/workflows/12620)).
- Trong giao diện n8n Editor, chọn **Add workflow** -> **Import from File** (hoặc paste trực tiếp mã JSON vào canvas).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 14 nodes được thiết kế mạch lạc, các sếp cần chú ý cấu hình kỹ các điểm sau:
- **Workflow Configuration (Set):** Nơi khai báo các biến chung như ID của Google Sheets chứa danh sách nhà tài trợ và gói tài trợ, cùng email người gửi.
- **Fetch Sponsors Sheet & Fetch Packages Sheet (Google Sheets):** Kết nối tài khoản Google OAuth2 của sếp và trỏ đúng đến file Google Sheets chuẩn bị sẵn.
- **AI Match Packages (OpenAI):** Chọn credential OpenAI và đảm bảo model được cấu hình là `gpt-4o` để đạt hiệu quả phân tích tốt nhất.
- **Filter Low Scores (If):** Kiểm tra điều kiện điểm số (Score > 7) trước khi cho phép tiến hành gửi email.
- **Send match email summary (Gmail):** Kết nối tài khoản Gmail cá nhân/doanh nghiệp để gửi email tự động.
- **Log Match Results (Google Sheets):** Cấu hình thao tác `append` để lưu vết lịch sử match vào bảng tính analytics.

#### 3. Kích hoạt ⚡️
- Thử nghiệm dữ liệu mẫu (khoảng 3 nhà tài trợ và 5 gói tài trợ) bằng nút **Execute Workflow**.
- Kiểm tra kết quả trên Gmail và Google Sheets.
- Nếu mọi thứ mượt mà, hãy gạt công tắc sang **Active** để hệ thống tự động chạy theo lịch trình từ node **Execute to Start (Schedule Trigger)**.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh chat:** Thêm node Telegram hoặc Slack sau bước *Log Match Results* để bắn thông báo ngay cho team sales khi có nhà tài trợ tiềm năng đạt điểm cao.
- **Mở rộng báo cáo:** Tạo thêm Dashboard trên Google Looker Studio kết nối trực tiếp với sheet log kết quả để trực quan hóa dữ liệu tài trợ theo tuần/tháng.

### 📌 Kết luận
Workflow "Match sponsors to event packages" là một cỗ máy tự động hóa hoàn hảo dành cho ban tổ chức sự kiện, giúp tối ưu hóa quy trình sales B2B nhờ AI. Hãy áp dụng ngay hôm nay để bứt phá doanh thu tài trợ cho sự kiện tiếp theo của các sếp!