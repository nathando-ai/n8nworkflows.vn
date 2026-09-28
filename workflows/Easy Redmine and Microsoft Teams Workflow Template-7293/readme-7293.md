---
title: "🚀 Tự động gửi báo cáo công việc hàng ngày từ Easy Redmine lên Microsoft Teams với n8n"
description: "Hướng dẫn cấu hình workflow n8n giúp tự động tổng hợp task từ Easy Redmine theo filter và gửi thông báo trực tiếp vào kênh Microsoft Teams mỗi sáng."
slug: "tu-dong-easy-redmine-va-microsoft-teams-voi-n8n"
tags: [n8n, automation, project-management, easy-redmine, microsoft-teams, no-code]
keywords: [n8n workflow, easy redmine microsoft teams, tu dong hoa quan ly du an, n8n easy redmine, tich hop microsoft teams]
---

# 🚀 Tự động gửi báo cáo công việc hàng ngày từ Easy Redmine lên Microsoft Teams

Các sếp có đang gặp tình trạng mỗi sáng phải mất hàng giờ đồng hồ để lọc task, kiểm tra tiến độ trong Easy Redmine rồi thủ công copy-paste vào Microsoft Teams để họp team? Việc này vừa tốn thời gian, dễ bỏ sót công việc, lại khiến đội ngũ chậm trễ trong việc cập nhật thông tin.

Giải pháp ở đây là gì? Hãy để workflow n8n này "gánh" thay các sếp! Workflow sẽ tự động kết nối Easy Redmine, quét danh sách task theo bộ lọc (filter) có sẵn, và bắn thông tin chi tiết (kèm link trực tiếp) thẳng vào kênh Microsoft Teams đúng 8:30 sáng mỗi ngày làm việc. Hoàn toàn tự động, không tốn một giọt mồ hôi thủ công nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian họp nhóm:** Không cần mất thời gian điểm danh task đầu ngày hay chuẩn bị báo cáo thủ công.
- **Không bỏ sót việc:** Đảm bảo mọi task mới, task mở (Open) đều được team nhìn thấy và xử lý đúng hạn.
- **Cá nhân hóa thông tin:** Chỉ lọc đúng các task quan trọng (theo filter định sẵn như team phụ trách, trạng thái, thời gian cập nhật).
- **Hoạt động tự động 24/7:** Chạyđúng lịch hẹn mỗi sáng làm việc mà không cần ai phải bấm nút kích hoạt.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Đã sẵn sàng hoạt động (Self-hosted hoặc Cloud).
- **Easy Redmine:** Tài khoản truy cập và API Key (nên dùng tài khoản kỹ thuật - technical user với quyền phù hợp).
- **Microsoft Teams:** Tài khoản hoặc Bot có quyền gửi tin nhắn vào Channel hoặc Chat mong muốn.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow từ [n8n template gốc](https://n8n.io/workflows/7293) hoặc tải file JSON về, sau đó paste trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình chính xác các node quan trọng sau đây:

- **Daily Trigger (8:30 work-days):** Node kiểu `scheduleTrigger` mặc định đặt lịch chạy lúc 8:30 các ngày làm việc. Các sếp có thể tùy chỉnh lại múi giờ hoặc tần suất nếu muốn.
- **Get Issues by Query (`@easysoftware/n8n-nodes-easy-redmine.easyRedmine`):** 
  - Kết nối `easyRedmineApi`.
  - Chọn Filter đã được lưu sẵn trên hệ thống Easy Redmine của công ty (Ví dụ: Assignee là "Consulting Team", Status là "Open", cập nhật trong "last 3 days").
- **Split Out Issues (`splitOut`):** Node này giúp tách mảng chứa nhiều task thành các item riêng lẻ để hệ thống xử lý từng task một.
- **Keep Relevant Fields & Add Link (`set`):** 
  - Lọc lại các trường dữ liệu cần thiết: `ID`, `Author`, `Subject`, `Description`.
  - Tạo URL link gắn trực tiếp đến task bằng biểu thức dạng: `https://easyredmineapp.com/issues/{{ $json.id }}`.
- **Run for Each Task (`splitInBatches`):** Vòng lặp để gửi từng task đi một cách mượt mà, tránh tình trạng tràn API.
- **Message into Team Channel (`microsoftTeams`):**
  - Kết nối `microsoftTeamsOAuth2Api`.
  - Chọn mục `chatMessage` -> `Create`.
  - Chọn kênh (Channel) hoặc đoạn chat trên MS Teams nhận thông tin và map nội dung định dạng HTML từ node trước đó.

#### 3. Kích hoạt ⚡️
- Bấm nút **Execute Workflow** để chạy thử nghiệm (Test run) với dữ liệu mẫu xem tin nhắn có bắn về Microsoft Teams chuẩn form chưa.
- Nếu mọi thứ mượt mà, các sếp gạt công tắc **Active** ở góc trên cùng bên phải để workflow chính thức tự động vận hành!

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Ngoài Microsoft Teams, các sếp có thể nhân bản nhánh cuối để bắn thêm bản tin tương tự về kênh Telegram của công ty hoặc Slack.
- **Lưu lịch sử báo cáo:** Thêm một node Google Sheets hoặc Airtable vào sau bước xử lý task để lưu lại lịch sử các task đã được điểm danh mỗi ngày.
- **Tùy chỉnh nội dung:** Tận dụng HTML trong node MS Teams để làm nổi bật tên task, độ ưu tiên (Priority) hoặc deadline bằng màu sắc bắt mắt.

### 📌 Kết luận
Với workflow n8n tích hợp giữa Easy Redmine và Microsoft Teams này, việc quản lý và đốc thúc công việc hàng ngày sẽ trở nên tự động hoàn toàn, giúp đội ngũ tập trung tối đa vào chuyên môn thay vì các thao tác thủ công nhàm chán. Cài đặt ngay để tối ưu hóa quy trình cho doanh nghiệp các sếp nhé!