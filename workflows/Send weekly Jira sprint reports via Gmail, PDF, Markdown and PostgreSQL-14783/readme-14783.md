---
title: "🚀 Tự Động Gửi Báo Cáo Sprint Jira Hàng Tuần (PDF, Email & DB)"
description: "Workflow n8n tự động trích xuất dữ liệu Jira, tạo báo cáo Sprint chuyên nghiệp dạng PDF/HTML/Markdown và lưu trữ vào PostgreSQL để phân tích xu hướng hiệu suất đội nhóm."
slug: "bao-cao-sprint-jira-tu-dong-n8n"
tags: [n8n, jira, automation, project-management, postgresql, reporting]
keywords: [n8n workflow, báo cáo jira, tự động hóa sprint, jira to pdf, n8n postgres]
---

# 🚀 Tự Động Gửi Báo Cáo Sprint Jira Hàng Tuần (PDF, Email & DB)

Các sếp quản lý dự án hay Tech Lead chắc hẳn đều quen với nỗi đau: Cuối tuần hoặc đầu tuần, phải dành hàng giờ để mở Jira, lọc issue, đếm số lượng task hoàn thành, ai đang bị block, epic nào đang ì ạch... rồi ngồi gõ email báo cáo cho sếp hoặc team. Chưa kể, dữ liệu này thường bị "mất" sau khi gửi email, khiến việc nhìn lại xu hướng velocity hay lead time của team trong nhiều tuần trở nên cực kỳ khó khăn.

Workflow này giải quyết triệt để vấn đề đó. Nó hoạt động như một "trợ lý ảo" chuyên trách báo cáo: **Mỗi thứ Hai lúc 8:00 sáng**, hệ thống tự động quét toàn bộ dữ liệu Jira trong 7 ngày qua, tổng hợp thành một báo cáo chuyên nghiệp (HTML + PDF đính kèm), gửi email cho các bên liên quan, đồng thời lưu trữ dữ liệu cấu trúc vào **PostgreSQL**. Điều này không chỉ giúp các sếp nhận được thông tin kịp thời mà còn xây dựng được một "kho dữ liệu lịch sử" để phân tích hiệu suất dài hạn (tích hợp PowerBI, Metabase...).

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, đặc biệt là các tác vụ nặng như convert PDF và truy vấn database, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian báo cáo:** Không cần thủ công, báo cáo tự động gửi đúng giờ, đúng người.
- **Định dạng chuyên nghiệp:** Nhận email kèm file PDF đẹp mắt, dễ đọc trên mọi thiết bị, kèm bản Markdown để lưu trữ nội bộ.
- **Dữ liệu lịch sử (Historical Data):** Mọi chỉ số KPI (Velocity, Lead Time, Assignee stats) được lưu vào PostgreSQL, cho phép trả lời các câu hỏi như: "Velocity team có tăng không?", "Ai là người xử lý issue nhanh nhất?".
- **Hỗ trợ đa dự án:** Chỉ cần thay đổi 1 cấu hình là có thể chạy song song cho nhiều dự án Jira khác nhau trên cùng một hệ thống.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Jira Cloud:** Có quyền truy cập vào Project cần báo cáo.
2. **Tài khoản Gmail:** Để gửi báo cáo (cần cấp quyền OAuth2 cho n8n).
3. **Cơ sở dữ liệu PostgreSQL:** Một instance DB (có thể dùng Supabase, Neon, hoặc VPS riêng) để lưu trữ dữ liệu lịch sử.
4. **API Key cho HTML to PDF:** Workflow sử dụng node `htmlcsstopdf`, các sếp cần tạo API key từ dịch vụ [htmlcsstopdf.com](https://htmlcsstopdf.com/) (có gói miễn phí hoặc trả phí tùy nhu cầu).
5. **n8n Instance:** Đã cài đặt và sẵn sàng.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Tải file JSON của workflow từ link gốc hoặc copy toàn bộ code JSON.
2. Mở n8n Editor, chọn **Import from URL** hoặc **Import from File**.
3. Sau khi import, các sếp sẽ thấy một workflow phức tạp với 44 nodes, được chia rõ ràng thành các khu vực: Cấu hình, Lấy dữ liệu Jira, Xử lý dữ liệu, Tạo báo cáo, và Lưu trữ DB.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Đây là phần quan trọng nhất. Workflow được thiết kế modular, nhưng có một số node "chìa khóa" các sếp bắt buộc phải cấu hình:

**🔑 Node: `CONFIGURATION NODE` (Code Node)**
Đây là "trái tim" của workflow. Các sếp chỉ cần chỉnh 3 biến số trong node này, mọi thứ còn lại sẽ tự động thích ứng:
- `PROJECT_KEY`: Mã dự án Jira (ví dụ: `PROJ`).
- `JIRA_DOMAIN`: Tên miền Jira của công ty (ví dụ: `yourcompany.atlassian.net`).
- `EMAIL_TO`: Địa chỉ email nhận báo cáo (có thể tách nhiều email bằng dấu phẩy).

**🔑 Credentials (Thông tin đăng nhập)**
Các sếp cần tạo và gắn credentials vào các node tương ứng:
1. **Jira Software Cloud API:** Gắn vào các node `Get Updated Issues`, `Get Created Issues`, `Get Completed Issues`, `Get Due Soon Issues`, `Get All Epics`, `Get All Issues`.
   - *Lưu ý:* Đảm bảo API Token có quyền đọc (Read) đối với Project.
2. **Gmail OAuth2:** Gắn vào node `Send Report Email`.
   - *Lưu ý:* Khi tạo credential Gmail, hãy đảm bảo scope `gmail.send` được cấp.
3. **PostgreSQL:** Gắn vào các node `CREATE TABLES`, `PG: Save Sprint Report`, `PG: Save Weekly KPIs`, `PG: Save Assignee KPIs`, `PG: Save Epic Snapshots`.
   - *Lưu ý:* Cần kết nối tới DB mà các sếp đã chuẩn bị.
4. **HTML to PDF API:** Gắn vào node `Convert HTML to PDF`.
   - *Lưu ý:* Điền API Key lấy từ htmlcsstopdf.com.

**🔑 Node: `CREATE TABLES` (Postgres Node)**
- Node này sẽ tự động tạo các bảng dữ liệu trong PostgreSQL nếu chưa tồn tại.
- **Lưu ý quan trọng:** Chỉ cần chạy workflow 1 lần đầu tiên (Manual Trigger) để node này tạo bảng. Sau đó, nó sẽ bỏ qua nếu bảng đã có. Các sếp không cần xóa node này, nó an toàn để chạy lại.

**🔑 Node: `Every Monday 8AM` (Schedule Trigger)**
- Mặc định workflow chạy vào thứ Hai lúc 8:00.
- Các sếp có thể chỉnh giờ chạy phù hợp với múi giờ và văn hóa làm việc của team (ví dụ: 7:30 sáng để sếp đọc trước khi họp standup).

#### 3. Kích hoạt ⚡️
1. **Test Run:**
   - Click vào node `When clicking ‘Execute workflow’` (Manual Trigger).
   - Chọn **Execute Workflow**.
   - Quan sát các node chạy lần lượt: Lấy dữ liệu Jira -> Xử lý -> Tạo HTML/PDF -> Gửi Email -> Lưu DB.
   - Kiểm tra hộp thư Gmail xem đã nhận được email báo cáo kèm file PDF chưa.
   - Kiểm tra PostgreSQL xem các bảng `sprint_reports`, `weekly_kpis`... đã có dữ liệu chưa.
2. **Bật Active:**
   - Nếu test thành công, click nút **Active** ở góc trên bên phải workflow.
   - Workflow sẽ tự động chạy vào thứ Hai hàng tuần.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Slack/Telegram:** Thay vì (hoặc song song với) Email, các sếp có thể thêm node `Slack` hoặc `Telegram` để gửi link báo cáo hoặc nội dung tóm tắt vào kênh chat của team.
- **Phân tích với PowerBI/Metabase:** Vì dữ liệu đã được lưu vào PostgreSQL một cách có cấu trúc, các sếp có thể kết nối PowerBI hoặc Metabase vào DB này để tạo các dashboard trực quan về Velocity, Burndown, và hiệu suất cá nhân theo thời gian thực.
- **Cảnh báo thông minh:** Các sếp có thể thêm logic vào node `Build Email HTML` hoặc tạo thêm một nhánh: Nếu số lượng issue "Due Soon" hoặc "Blocked" vượt quá ngưỡng nhất định, gửi một thông báo cảnh báo riêng (Red Alert) cho Tech Lead.
- **Đa dự án:** Nếu công ty có nhiều dự án, hãy copy workflow này và chỉ cần sửa `CONFIGURATION NODE` cho từng bản sao. Chúng sẽ chia sẻ cùng một PostgreSQL, giúp các sếp dễ dàng so sánh hiệu suất giữa các dự án.

### 📌 Kết luận
Việc báo cáo Sprint thủ công không chỉ tốn thời gian mà còn dễ gây sai sót và thiếu tính nhất quán. Với workflow n8n này, các sếp biến quy trình báo cáo thành một dòng chảy dữ liệu tự động, chuyên nghiệp và có khả năng phân tích sâu. Hãy dành thời gian setup 1 lần, và để hệ thống tự lo phần còn lại mỗi tuần. Chúc các sếp quản lý dự án hiệu quả hơn!