---
title: "🚀 Tự động gửi báo cáo danh sách thuê bao Mailchimp hàng ngày lên Slack"
description: "Hướng dẫn thiết lập workflow n8n tự động lấy dữ liệu thuê bao từ Mailchimp và gửi báo cáo tổng hợp vào Slack mỗi ngày một cách nhanh chóng, chính xác."
slug: "tu-dong-gui-bao-cao-mailchimp-len-slack-hang-ngay"
tags: [n8n, automation, no-code, mailchimp, slack, marketing-automation]
keywords: [n8n workflow, mailchimp to slack, tự động hóa marketing, báo cáo mailchimp hàng ngày, n8n việt nam]
---

# 🚀 Tự động gửi báo cáo danh sách thuê bao Mailchimp hàng ngày lên Slack

Các sếp làm marketing chắc chắn hiểu cảm giác mỗi sáng mở mắt ra là phải truy cập vào hàng loạt dashboard để kiểm tra số liệu: danh sách thuê bao Mailchimp tăng giảm ra sao, chiến dịch hôm qua có hiệu quả không? Việc kiểm tra thủ công này vừa tốn thời gian, vừa dễ bỏ quên các mốc tăng trưởng quan trọng của đội ngũ.

Đừng lo, bài toán này sẽ được giải quyết gọn gàng với workflow n8n cực kỳ tinh gọn do chuyên gia **Ziad Adel** xây dựng. Workflow này sẽ tự động hóa 100% quy trình: kéo dữ liệu thuê bao từ Mailchimp và bắn thẳng báo cáo tổng hợp vào kênh Slack của team mỗi sáng mà không cần bất kỳ thao tác thủ công nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian:** Đội ngũ Marketing không cần phải đăng nhập thủ công vào Mailchimp mỗi ngày để xem số liệu.
- **Cập nhật tức thì:** Số liệu thuê bao mới nhất được gửi trực tiếp vào Slack vào đúng 9:00 sáng hàng ngày.
- **Tăng tính minh bạch:** Giúp cả team (Growth, Marketing, Sales) nắm bắt sát sao tốc độ tăng trưởng danhσh sách khách hàng tiềm năng.
- **Hoạt động tự động 24/7:** Chạy ngầm ổn định trên hệ thống n8n của các sếp mà không cần bận tâm can thiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một hệ thống **n8n** đang hoạt động (Cloud hoặc Self-hosted).
- Tài khoản và API Credentials của **Mailchimp** (kèm theo Audience/List ID cần theo dõi).
- Tài khoản và Bot/App tích hợp của **Slack** (đã cấp quyền đăng bài vào kênh mong muốn).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trên n8n Editor, sau đó copy và paste mã JSON của workflow (hoặc tải file JSON từ nguồn cung cấp) trực tiếp vào giao diện làm việc của n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm có 3 nodes chính, các sếp cần cấu hình cẩn thận các điểm sau:

- **Start: Daily at 09:00 (`cron`):** 
  - Mặc định lịch chạy là 9:00 sáng mỗi ngày. Các sếp có thể click vào node này để thay đổi thời gian kích hoạt (Cron Expression) nếu muốn nhận báo cáo vào khung giờ khác phù hợp hơn với múi giờ hoặc lịch họp của team.
- **Mailchimp: Get Subscribers (`mailchimp`):** 
  - Cần kết nối tài khoản Mailchimp bằng API Key/Credentials của sếp.
  - Chọn thao tác `getAll` (lấy toàn bộ danh sách) và cấu hình đúng `{{MAILCHIMP_LIST_ID}}` (ID danh sách người nhận/audience mà sếp muốn theo dõi số lượng).
- **Daily Mailchimp Report Message (`slack`):** 
  - Kết nối tài khoản Slack thông qua `slackApi` credentials.
  - Chỉ định kênh Slack nhận tin nhắn (ví dụ: `#marketing`, `#growth-team`, hoặc một kênh private tùy chọn).
  - Tùy chỉnh nội dung tin nhắn kết hợp với dữ liệu đầu ra từ node Mailchimp để hiển thị tổng số lượng thuê bao một cách sinh động nhất.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** để chạy thử (Test run) và kiểm tra xem dữ liệu có được đẩy lên Slack thành công hay chưa.
- Sau khi test thành công, gạt công tắc sang chế độ **Active** để hệ thống tự động chạy theo lịch hẹn.

---

### ✍️ Mẹo & gợi ý nâng cao
Để workflow trở nên "lợi hại" hơn nữa, các sếp có thể mở rộng thêm một vài ý tưởng sau:
1. **Mở rộng kênh thông báo:** Kết hợp thêm node Telegram hoặc Discord để gửi báo cáo song song cho các sếp quản lý không dùng Slack.
2. **Lưu trữ lịch sử:** Thêm node Google Sheets để ghi lại số lượng thuê bao mỗi ngày, giúp vẽ biểu đồ tăng trưởng theo tuần/tháng.
3. **Cảnh báo thông minh (Alert):** Thêm điều kiện (If Node) nếu số lượng thuê bao tăng vọt hoặcụt giảm bất thường thì gắn thẻ (mention) tên trưởng nhóm trực tiếp trên Slack.

### 📌 Kết luận
Chỉ với 3 nodes đơn giản trong n8n, các sếp đã có ngay một trợ lý tự động hóa đắc lực giúp cập nhật số liệu Mailchimp mỗi ngày mà không tốn một phút thao tác tay. Triển khai ngay hôm nay để tối ưu hóa vận hành đội ngũ marketing nhé các sếp!