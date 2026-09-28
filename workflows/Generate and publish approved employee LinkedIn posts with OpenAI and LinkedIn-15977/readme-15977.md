---
title: "🚀 Tự động hóa tạo và xuất bản bài đăng LinkedIn cho nhân viên bằng OpenAI và LinkedIn"
description: "Hướng dẫn xây dựng workflow n8n tự động quét blog, dùng OpenAI viết bài đăng LinkedIn cá nhân hóa theo từng vai trò, gửi email duyệt bài và tự động đăng lên LinkedIn."
slug: "tu-dong-hoa-tao-va-dang-bai-linkedin-voi-openai-va-n8n"
tags: [n8n, automation, no-code, openai, linkedin, ai, content-marketing]
keywords: [n8n workflow, tự động hóa linkedin, openai viết bài, quét rss blog, duyệt bài qua email, n8n việt nam]
---

# 🚀 Tự động hóa tạo và xuất bản bài đăng LinkedIn cho nhân viên bằng OpenAI và LinkedIn

Các sếp có bao giờ cảm thấy mệt mỏi khi phải thủ công đi đọc blog công ty, sau đó vắt óc nghĩ cách viết lại bài chia sẻ lên LinkedIn cho từng cá nhân (CEO, HR, Developer, Marketing...) rồi lại phải copy/paste, căn giờ đăng? Công việc lặp đi lặp lại này ngốn rất nhiều thời gian mà hiệu quả đôi khi không cao do thiếu sự đều đặn.

Giải pháp đây rồi! Workflow n8n siêu cấp này sẽ giúp các sếp **tự động hóa 100% quy trình** từ việc phát hiện blog mới, dùng AI (OpenAI) cá nhân hóa nội dung theo từng "vibe" của nhân viên, gửi email xin duyệt, cho đến khi tự động xuất bản lên LinkedIn và báo cáo qua Slack nếu có lỗi. Không cần một dòng code phức tạp nào cả!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không lo gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động quét và cập nhật:** Hệ thống tự động kiểm tra RSS feed blog mới định kỳ mà không cần đụng tay.
- **AI cá nhân hóa đa phong cách:** Tự động tạo nhiều góc nhìn bài đăng khác nhau cho CEO, HR, Developer, Marketing... thông qua OpenAI.
- **Quy trình kiểm duyệt mượt mà:** Gửi email kèm nút bấm duyệt/từ chối trực quan, sếp chỉ cần click là xong.
- **Đăng bài tự động & Giám sát chặt chẽ:** Tự động đẩy lên LinkedIn API khi được duyệt, đồng thời báo động qua Slack ngay nếu có sự cố xảy ra.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ TRƯỚC KHI "LÊN ĐỒ"]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Google Sheets:** Lưu trữ log blog đã quét, danh sách bài đăng và trạng thái duyệt.
- **OpenAI API Key:** Dùng cho node `Generate AI LinkedIn Posts`.
- **Gmail Credentials:** Dùng để gửi email chứa link duyệt/từ chối.
- **LinkedIn Developer Account & OAuth2:** Để cấp quyền tự động đăng bài lên trang cá nhân/doanh nghiệp.
- **Slack Bot Token/Webhook:** Nhận thông báo lỗi khi đăng bài thất bại.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Copy toàn bộ mã JSON của workflow này và paste trực tiếp vào n8n Editor của các sếp, hoặc import file JSON tải từ nguồn gốc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 30 nodes được chia làm các phân đoạn rõ ràng. Các sếp hãy chú ý cấu hình kỹ các điểm sau:
- **Blog Scan Scheduler & Fetch Latest Blogs:** Cấu hình thời gian chạy định kỳ và đường dẫn RSS Feed blog của công ty.
- **Check Existing Blog & Save Processed Blog (Google Sheets):** Kết nối tài khoản Google Sheets của các sếp, trỏ tới file quản lý bài viết để hệ thống lưu lịch sử, tránh quét trùng lặp.
- **Create Employee Personas & Generate AI LinkedIn Posts (OpenAI):** Thiết lập prompt và vai trò nhân viên (CEO, HR, Dev...) để AI hiểu và viết đúng giọng điệu. Chọn credentials `openAiApi`.
- **Send request for approval & reject (Gmail):** Cấu hình tài khoản Gmail để gửi email phê duyệt kèm các action link trỏ về Webhook.
- **Receive Approval or Reject Decision (Webhook):** Đảm bảo Webhook path (`approve-post`) khớp với URL được cấu hình trong email duyệt bài.
- **Fetch LinkedIn Profile & Publish LinkedIn Post (HTTP Request):** Cấu hình `linkedInOAuth2Api` để hệ thống có quyền gọi LinkedIn API xuất bản bài viết.
- **Send Failure Alert (Slack):** Kết nối Slack channel để nhận thông báo cảnh báo ngay lập tức nếu API LinkedIn trả về lỗi.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** chạy thử nghiệm (Test run) với một blog mẫu để kiểm tra từ bước quét RSS đến khâu sinh nội dung AI.
- Sau khi test thành công, bật công tắc **Active** góc trên bên phải để hệ thống tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Thay vì chỉ dùng Gmail để duyệt bài, các sếp có thể tích hợp thêm node **Telegram** hoặc **Slack** để bấm nút Duyệt/Từ chối trực tiếp ngay trong chatwork của công ty.
- **Lưu trữ Media:** Kết hợp thêm các node xử lý ảnh AI (như DALL-E hoặc Midjourney API) để tự động sinh hình ảnh đính kèm bài đăng LinkedIn thay vì chỉ có text thuần túy.
- **Báo cáo định kỳ:** Tạo thêm một nhánh chạy vào cuối tuần để tổng hợp số lượng bài đã đăng lên Google Sheets và gửi báo cáo tóm tắt qua email cho ban quản lý.

### 📌 Kết luận
Với workflow n8n này, việc duy trì sự hiện diện thương hiệu cá nhân và doanh nghiệp trên LinkedIn chưa bao giờ dễ dàng đến thế. Hãy cài đặt ngay để tối ưu hóa đội ngũ content marketing và giải phóng hàng giờ làm việc thủ công mỗi tuần cho các sếp!