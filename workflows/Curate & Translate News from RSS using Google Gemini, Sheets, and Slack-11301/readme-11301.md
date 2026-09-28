---
title: "🚀 Tự động hóa tổng hợp, viết lại và dịch tin tức từ RSS bằng Google Gemini, Google Sheets và Slack"
description: "Xây dựng hệ thống biên tập và dịch tin tức tự động 100% từ RSS feed sử dụng AI Google Gemini, lưu trữ vào Google Sheets và thông báo qua Slack."
slug: "tu-dong-hoa-tong-hop-dich-tin-tuc-rss-gemini-sheets-slack"
tags: [n8n, automation, google-gemini, content-creation, google-sheets, slack]
keywords: [n8n workflow, dịch tin tức tự động, google gemini n8n, rss to slack, tự động hóa nội dung]
---

# 🚀 Tự động hóa tổng hợp, viết lại và dịch tin tức từ RSS với Google Gemini, Google Sheets và Slack

Các sếp làm trong lĩnh vực sáng tạo nội dung, truyền thông hay bản địa hóa chắc chắn luôn đau đầu với việc phải cập nhật tin tức liên tục từ các trang RSS, lọc bài viết thủ công, viết lại cho hấp dẫn và dịch ra nhiều ngôn ngữ khác nhau (Anh, Trung, Hàn...). Quá trình này ngốn hàng giờ đồng hồ mỗi ngày và rất dễ bỏ sót thông tin quan trọng.

Giải pháp ở đây là gì? Workflow n8n này sẽ tự động hóa toàn bộ quy trình trên: từ việc quét tin RSS, lọc từ khóa thông minh, nhờ **Google Gemini** viết lại/trích xuất địa điểm/dịch thuật, cho đến việc lưu trữ vào **Google Sheets** và bắn thông báo trực tiếp lên **Slack**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không cần đọc và dịch thủ công từng bản tin RSS.
- **AI Đa ngôn ngữ thông minh:** Tự động viết lại nội dung hấp dẫn và dịch đồng thời sang nhiều ngôn ngữ (Anh, Trung, Hàn...) nhờ Google Gemini.
- **Lưu trữ bài bản:** Tự động đồng bộ dữ liệu chuẩn chỉnh vào Google Sheets để làm kho tư liệu.
- **Thông báo thời gian thực:** Cập nhật ngay lập tức các bài viết mới hoặc trạng thái bỏ qua lên kênh Slack của team.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Google Gemini API Key:** Cấp quyền cho các Agent AI xử lý ngôn ngữ.
- **Google Sheets:** Chuẩn bị sẵn một file Google Sheet để lưu trữ dữ liệu tin tức.
- **Slack Workspace:** Tạo Webhook hoặc kết nối OAuth2 để gửi tin nhắn thông báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow hoặc copy toàn bộ JSON từ nguồn, sau đó dán trực tiếp vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình các node quan trọng sau:
- **Schedule Trigger:** Cài đặt lịch chạy tự động theo khung giờ mong muốn (ví dụ: mỗi tiếng chạy 1 lần).
- **Fetch RSS Feed:** Điền đường dẫn RSS feed (ví dụ: NHK News hoặc bất kỳ nguồn báo nào các sếp muốn theo dõi).
- **Filter Keywords (Node IF):** Thiết lập từ khóa lọc mong muốn (ví dụ: "Tokyo" hoặc "Season") để loại bỏ các bài viết không liên quan.
- **Gemini Chat Model & Gemini Chat Model1:** Kết nối credentials bằng **Google Palm API Key** của các sếp.
- **Rewrite Article / Extract Location / Translate Content (Agent Nodes):** Tinh chỉnh Prompt bên trong các AI Agent nếu muốn thay đổi phong cách viết hoặc ngôn ngữ đích.
- **Format Data (Code Node):** Xử lý và làm sạch định dạng JSON đầu ra từ AI để chuẩn bị lưu database.
- **Save to Google Sheets:** Chọn file Google Sheets và Mapping các trường dữ liệu tương ứng (Tiêu đề, Nội dung dịch, Link, Địa điểm...).
- **Notify Slack & Notify Skipped:** Kết nối tài khoản Slack và chọn kênh (Channel) nhận thông báo.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** với một vài dữ liệu mẫu để kiểm tra xem AI dịch có chuẩn và data đã vào Sheet chưa.
- Sau khi test thành công, bật công tắc **Active** góc trên cùng bên phải để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Ngoài Slack, các sếp có thể nhân bản node thông báo sang Telegram Bot để nhận tin tức trực tiếp trên điện thoại cá nhân.
- **Thêm bước kiểm duyệt (Human-in-the-loop):** Thêm node chờ phản hồi qua Slack nút bấm (Interactive Messages) trước khi chính thức lưu vào Google Sheets hoặc đăng mạng xã hội.
- **Tự động đăng Social:** Nối thêm node Facebook Page, X (Twitter) hoặc LinkedIn để tự động chia sẻ tin tức đã được AI viết lại ngay sau khi xử lý xong.

### 📌 Kết luận
Workflow này là trợ thủ đắc lực cho các nhà sáng tạo nội dung và đội ngũ truyền thông muốn tối ưu hóa quy trình sản xuất tin tức bằng AI. Hãy "lên đồ" ngay hôm nay để tiết kiệm thời gian và bứt phá hiệu suất công việc!