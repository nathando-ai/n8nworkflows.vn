---
title: "🚀 Tự động hóa tạo bài viết X (Twitter) & LinkedIn từ Reddit Threads với Google Gemini & Human Review"
description: "Biến mọi Reddit thread thành nội dung mạng xã hội chuyên nghiệp trên X và LinkedIn bằng AI Gemini, kết hợp cổng kiểm duyệt thủ công an toàn."
slug: "tu-dong-hoa-tao-bai-viet-x-linkedin-tu-reddit-gemini"
tags: [n8n, automation, no-code, ai, google-gemini, social-media, reddit]
keywords: [n8n workflow, tự động hóa reddit, gemini ai, đăng bài linkedin x twitter, no-code automation]
---

# 🚀 Tự động hóa tạo bài viết X & LinkedIn từ Reddit Threads với Google Gemini

Việc sáng tạo nội dung đều đặn trên nhiều nền tảng mạng xã hội như **X (Twitter)** và **LinkedIn** ngốn rất nhiều thời gian của các nhà sáng tạo và doanh nghiệp. Thay vì phải đọc hàng trăm bình luận trên một chủ đề hot ở Reddit rồi tự viết lại, workflow n8n này sẽ thay các sếp làm toàn bộ công việc nặng nhọc đó nhờ sức mạnh của **Google Gemini AI**, đồng thời có chốt kiểm duyệt thủ công (**Human-in-the-loop**) trước khi đăng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Tự động tóm tắt thread Reddit dài dòng, chắt lọc ý hay và chuyển hóa thành bài viết chuẩn chỉnh.
- **Tối ưu hóa đa nền tảng:** Tự động tạo bài viết ngắn gọn, giật tít cho X (≤280 ký tự) và bài viết chuyên sâu, chuyên nghiệp cho LinkedIn (150-300 từ).
- **Kiểm soát tuyệt đối:** Tích hợp bước duyệt bài (Human Approval) qua form n8n giúp các sếp chỉnh sửa, thêm thắt nội dung trước khi bấm nút xuất bản.
- **Loại bỏ rủi ro:** Chế độ từ chối thông minh đảm bảo không có nội dung rác hoặc nhầm lẫn nào được đăng tự động.
:::

### 🔑 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Google Gemini API Key:** Dùng cho các node AI tóm tắt và sinh nội dung (`googlePalmApi` credentials).
- **Tài khoản X (Twitter):** Cần kết nối OAuth2 API để đăng bài tự động.
- **Tài khoản LinkedIn:** Cần kết nối OAuth2 API để đăng bài cá nhân hoặc doanh nghiệp.
- **Reddit:** Không cần API key vì workflow sử dụng Reddit Public JSON API.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc sao chép mã nguồn JSON.
- Mở n8n Editor, tạo workflow mới và dán (Paste) trực tiếp vào giao diện.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Trong workflow này, các sếp cần chú ý cấu hình các node quan trọng sau:
- **Summarize Thread & Generate Social Posts (Google Gemini):** Kết nối tài khoản Google Gemini bằng API Key của sếp và chọn model phù hợp (ví dụ: `gemini-1.5-flash` hoặc tương đương).
- **Post to X (Twitter):** Xác thực tài khoản X qua **OAuth2 API** để cho phép n8n đăng bài thay mặt tài khoản.
- **Post to LinkedIn:** Xác thực tài khoản LinkedIn qua **OAuth2 API**.
- **Human Approval (Wait Node):** Node này sẽ tạo ra một form web tạm thời để các sếp duyệt bài. Hãy kiểm tra URL form do n8n cung cấp sau khi trigger chạy để truy cập vào giao diện duyệt nội dung.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test workflow**) bằng cách điền một URL bài viết trên Reddit vào form trigger (`Reddit URL Input`).
- Kiểm tra kết quả ở node **Human Approval**, duyệt bài và xác nhận xem bài đăng có lên đúng X và LinkedIn hay không.
- Sau khi test thành công, bật công tắc **Active** để đưa workflow vào vận hành chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Lưu trữ Log:** Thêm một node Google Sheets hoặc Airtable vào nhánh thành công/thất bại để lưu lại lịch sử các bài đã đăng và nguồn Reddit tương ứng.
- **Thông báo qua Telegram/Slack:** Thêm node thông báo khi có bài viết mới chờ duyệt (`Human Approval`) để các sếp không bỏ lỡ nội dung hot.
- **Mở rộng nền tảng:** Tích hợp thêm các node Facebook Pages hoặc Threads để xuất bản đa kênh cùng lúc.

### 📌 Kết luận
Workflow tự động hóa kết hợp giữa Reddit, Google Gemini và Human-in-the-loop này là trợ thủ đắc lực cho bất kỳ ai làm content marketing. Hãy "lên đồ" ngay hôm nay để tối ưu hóa quy trình sản xuất nội dung mạng xã hội của các sếp!