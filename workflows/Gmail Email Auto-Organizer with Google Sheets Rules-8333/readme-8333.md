---
title: "🚀 Tự động phân loại và quản lý email Gmail thông minh với Google Sheets và n8n"
description: "Xây dựng hệ thống tự động lọc, gắn nhãn, dọn dẹp hộp thư đến Gmail dựa trên các quy tắc tùy chỉnh từ Google Sheets và thông báo qua Slack bằng n8n."
slug: "tu-dong-phan-loai-email-gmail-voi-google-sheets-va-n8n"
tags: [n8n, automation, no-code, gmail, google-sheets, slack]
keywords: [n8n workflow, tu dong hoa gmail, google sheets rules, quan ly email tu dong, loc email gmail]
---

# 🚀 Tự động phân loại và quản lý email Gmail thông minh với Google Sheets và n8n

Mỗi ngày, các sếp phải đối mặt với hàng chục, thậm chí hàng trăm email rác, email marketing, newsletter chen chúc trong hộp thư đến (Inbox). Việc lọc thủ công, gắn nhãn hay đánh dấu đã đọc ngốn rất nhiều thời gian quý báu mà lẽ ra nên dành cho các quyết định kinh doanh cốt lõi. 

Giải pháp là đây! Workflow n8n **Gmail Email Auto-Organizer with Google Sheets Rules** sẽ giúp các sếp tự động hóa 100% quy trình đọc, kiểm tra quy tắc từ Google Sheets, tự động gắn nhãn, dọn dẹp Inbox và gửi báo cáo tóm tắt về Slack. Không cần code phức tạp, chỉ cần thiết lập một lần và hệ thống sẽ tự chạy ngầm 24/7!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Hộp thư luôn sạch sẽ (Inbox Zero):** Tự động lọc và chuyển email marketing, quảng cáo ra khỏi hộp thư chính.
- **Tùy biến quy tắc linh hoạt:** Dễ dàng thêm, sửa, xóa các quy tắc phân loại email ngay trên Google Sheets mà không cần đụng tới n8n workflow.
- **Tự động hóa thông minh:** Tự động đánh dấu đã đọc, gắn nhãn phù hợp và tạo nhãn mới nếu chưa tồn tại trên Gmail.
- **Cập nhật tức thì:** Nhận thông báo hoàn tất quá trình xử lý trực tiếp qua Slack để nắm bắt tình hình.
:::

### ✕ Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và kết nối sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản Gmail** (với quyền OAuth2 để n8n đọc/ghi email và nhãn).
- **Google Sheets** (tạo sẵn một bảng tính chứa các quy tắc lọc email).
- **Slack Workspace** (để nhận thông báo tổng kết).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này hoặc tải file từ kho lưu trữ n8n, sau đó dán trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 17 nodes hoạt động nhịp nhàng. Các sếp cần chú ý cấu hình kỹ các node trọng điểm sau:

- **Schedule Trigger:** Cấu hình thời gian chạy tự động (ví dụ: chạy mỗi 30 phút hoặc 1 tiếng quét email một lần).
- **Get many messages:** Kết nối tài khoản Gmail OAuth2 để lấy danh sách email chưa đọc hoặc theo điều kiện.
- **Sheet Rules (Google Sheets):** Kết nối tài khoản Google Sheets, trỏ tới file Google Sheets chứa bảng quy tắc phân loại email của các sếp (ví dụ: cột chứa từ khóa người gửi, tiêu đề và nhãn tương ứng).
- **Parse Sender Email, Apply Sheet Rules, Map Label Name (Code Nodes):** Các node xử lý dữ liệu bằng Javascript giúp bóc tách email người gửi, so khớp với quy tắc trong Sheet và map ra đúng tên nhãn.
- **Promotional, Add Label, Remove From Inbox, Mark as read (Gmail Nodes):** Cấu hình các thao tác thực thi trên Gmail dựa trên kết quả so khớp quy tắc.
- **Completed Notification (Slack):** Kết nối tài khoản Slack và chọn channel để nhận thông báo sau khi workflow chạy xong.

#### 3. Kích hoạt ⚡️
- Bấm nút **Execute Workflow** để test thủ công với vài email mẫu xem hệ thống chạy có mượt không.
- Sau khi kiểm tra mọi thứ chạy êm ái, gạt công tắc sang **Active** để hệ thống tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp AI (OpenAI/Claude):** Các sếp có thể nâng cấp node Code bằng AI để tự động phân tích ngữ nội dung email phức tạp thay vì chỉ dựa vào từ khóa thông thường trong Google Sheets.
- **Lưu log vào Google Sheets:** Thêm một node Google Sheets ở cuối để lưu lại lịch sử các email đã được xử lý nhằm dễ dàng tra cứu về sau.
- **Báo cáo định kỳ qua Telegram:** Ngoài Slack, có thể bắn thêm một nhánh sang Telegram Bot để nhận thông báo trên điện thoại cá nhân mọi lúc mọi nơi.

### 📌 Kết luận
Workflow **Gmail Email Auto-Organizer with Google Sheets Rules** là trợ thủ đắc lực giúp các sếp giải quyết triệt để tình trạng quá tải email, tự động hóa việc phân loại và tối ưu hóa thời gian làm việc mỗi ngày. Hãy cài đặt ngay hôm nay để tận hưởng sự thảnh thơi mà tự động hóa mang lại!