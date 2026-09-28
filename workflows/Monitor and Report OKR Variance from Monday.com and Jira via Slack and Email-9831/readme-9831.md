---
title: "🚀 Tự Động Theo Dõi & Báo Cáo Chênh Lệch OKR Giữa Monday.com và Jira"
description: "Hướng dẫn xây dựng workflow n8n tự động đồng bộ OKR, tính toán tiến độ chênh lệch từ Monday.com và Jira, sau đó gửi báo cáo qua Slack và Email."
slug: "tu-dong-theo-doi-va-bao-cao-chenh-lech-okr-monday-jira"
tags: [n8n, automation, monday, jira, slack, outlook]
keywords: [n8n workflow, tu dong hoa okr, monday.com jira sync, bao cao okr slack, n8n automation]
---

# 🚀 Tự Động Theo Dõi & Báo Cáo Chênh Lệch OKR Giữa Monday.com và Jira

Các sếp có đang gặp khó khăn trong việc cập nhật tiến độ OKR (Objectives and Key Results) thủ công? Việc phải liên tục "nhảy" qua lại giữa Monday.com để xem mục tiêu và Jira để check tiến độ công việc của team, sau đó tính toán độ lệch (variance) và làm báo cáo gửi sếp lớn thực sự là một "cực hình" ngốn rất nhiều thời gian, lại dễ xảy ra sai sót.

Được thiết kế bởi chuyên gia **Rahul Joshi**, workflow n8n này chính là giải pháp tự động hóa 100% giúp các doanh nghiệp giải quyết triệt để bài toán trên. Hệ thống sẽ tự động đồng bộ dữ liệu từ Monday.com và Jira, tính toán tiến độ thực tế, cập nhật ngược lại lên bảng quản lý và bắn báo cáo trực quan qua Slack lẫn Email hàng ngày/hàng tuần.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian tổng hợp:** Không còn cảnh copy-paste dữ liệu từ Jira sang Monday.com rồi ngồi tính toán thủ công.
- **Minh bạch tiến độ real-time:** Tự động tính toán độ chênh lệch (Variance) dựa trên trạng thái thực tế của Epic bên Jira.
- **Cảnh báo sớm rủi ro:** Tự động phân loại trạng thái (Ví dụ: "At Risk") nếu tiến độ chậm hơn mục tiêu đề ra.
- **Đa kênh thông báo:** Báo cáo được gửi thẳng đến kênh Slack của team và hộp thư Microsoft Outlook của ban quản lý.
:::

### 📦 Các Nodes chính trong Workflow
Workflow gồm tổng cộng **12 nodes** phối hợp nhịp nhàng:
1. **Daily OKR Sync Trigger (`scheduleTrigger`):** Lên lịch chạy tự động hàng ngày/hàng tuần.
2. **Fetch OKRs from Monday.com (`mondayCom`):** Lấy danh sách Key Results từ bảng quản lý.
3. **Map Monday Fields → Standard KR Schema (`set`):** Chuẩn hóa cấu trúc dữ liệu đầu vào.
4. **Split KR → Epics Mapper (`code`):** Tách các chuỗi Jira Epic (cách nhau bởi dấu phẩy) thành các item riêng biệt để xử lý song song.
5. **Fetch Jira Epic Details (`jira`):** Lấy thông tin chi tiết từng Epic từ Jira.
6. **Normalize Jira Response (`code`):** Làm sạch và trích xuất các trường cần thiết từ response của Jira.
7. **Join KR + Epic Data (SQL Merge) (`merge`):** Kết hợp dữ liệu từ Monday và Jira.
8. **Compute KR Progress & Variance (`code`):** Tính toán tiến độ thực tế dựa trên trọng số công việc và độ chênh lệch.
9. **Update KR Status on Monday (`mondayCom`):** Cập nhật ngược kết quả tính toán lên Monday.com.
10. **Aggregate Final Results for Reporting (`aggregate`):** Tổng hợp dữ liệu toàn bộ KR để chuẩn bị gửi báo cáo.
11. **Post Slack Variance Report (`slack`):** Gửi báo cáo tóm tắt lên kênh Slack.
12. **Email Variance Digest (`microsoftOutlook`):** Gửi báo cáo chi tiết qua Outlook.

---

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Monday.com** (Đã thiết lập board OKR với các cột chuẩn).
- **Tài khoản Jira Cloud** (Có quyền truy cập đọc các Epic liên quan).
- **Slack Workspace** (Để cấu hình bot gửi thông báo).
- **Microsoft Outlook Account** (Để gửi email báo cáo tổng hợp).
- **n8n Instance** (Self-hosted hoặc Cloud).
:::

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy toàn bộ mã nguồn JSON.
- Trong giao diện n8n Editor, chọn **Add workflow** -> Click vào menu ba chấm (...) ở góc trên bên phải -> **Import from File / Clipboard** và dán mã JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động trơn tru với hệ thống của công ty các sếp, hãy cấu hình các node sau:

- **Daily OKR Sync Trigger:** Mở node này và cấu hình lại khung giờ chạy (ví dụ: 9:00 AM mỗi ngày) phù hợp với múi giờ của doanh nghiệp.
- **Fetch OKRs from Monday.com & Update KR Status on Monday:** Kết nối tài khoản Monday.com Credentials (`mondayComApi`). Thay thế `boardId` và `groupId` bằng ID bảng thực tế của công ty. Đảm bảo ánh xạ đúng các ID cột (`MONDAY_COL_ACTUAL_PROGRESS`, `MONDAY_COL_VARIANCE`, `MONDAY_COL_STATUS`).
- **Fetch Jira Epic Details:** Kết nối tài khoản Jira Cloud API Credentials. Đảm bảo tài khoản có quyền đọc các Epic được trỏ tới từ Monday.com.
- **Post Slack Variance Report:** Kết nối Slack API, thay thế `channelId` bằng ID kênh Slack nhận thông báo của team.
- **Email Variance Digest (Outlook):** Kết nối tài khoản Microsoft Outlook qua OAuth2 và thiết lập địa chỉ email nhận báo cáo.

#### 3. Kích hoạt ⚡️
- Click nút **Test workflow** để chạy thử nghiệm với dữ liệu thực tế và kiểm tra kết quả trả về ở từng node.
- Nếu không có lỗi xuất hiện, bật công tắc **Active** ở góc trên bên phải để workflow tự động chạy ngầm 24/7.

---

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Có thể bổ sung thêm node Telegram hoặc Microsoft Teams để tăng độ phủ thông tin cho các quản lý thích dùng app khác.
- **Lưu lịch sử vào Google Sheets/Database:** Thêm một node ghi nhận lịch sử (Log) sau bước tính toán variance để vẽ biểu đồ tăng trưởng OKR theo thời gian thực.
- **Tinh chỉnh công thức trọng số:** Trong node `Compute KR Progress & Variance`, các sếp có thể thay đổi trọng số mặc định (To Do = 0%, In Progress = 50%, Done = 100%) cho phù hợp với quy trình quản lý thực tế của công ty.

---

### 📌 Kết luận
Việc tự động hóa quy trình theo dõi OKR giữa Monday.com và Jira không chỉ giúp tiết kiệm hàng chục giờ làm việc thủ công mỗi tuần mà còn nâng cao tính minh bạch và tinh thần trách nhiệm trong các phòng ban. Hãy import workflow này ngay hôm nay để tối ưu hóa năng suất vận hành cho đội ngũ của các sếp!