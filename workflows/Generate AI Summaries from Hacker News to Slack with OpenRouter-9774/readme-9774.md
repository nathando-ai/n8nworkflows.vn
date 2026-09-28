---
title: "🚀 Tự động tóm tắt tin tức Hacker News bằng AI và gửi thẳng vào Slack"
description: "Hướng dẫn xây dựng workflow n8n tự động quét tin tức công nghệ từ Hacker News theo từ khóa, tóm tắt thông minh bằng AI qua OpenRouter và gửi báo cáo trực tiếp lên kênh Slack mỗi ngày."
slug: "tu-dong-tom-tat-hacker-news-ai-slack-openrouter"
tags: [n8n, automation, ai, slack, hackernews, openrouter, no-code]
keywords: [n8n workflow, tóm tắt tin tức ai, hacker news slack automation, openrouter n8n, tự động hóa tin tức]
---

# 🚀 Tự động tóm tắt tin tức Hacker News bằng AI và gửi thẳng vào Slack

Các sếp có bao giờ cảm thấy ngập lụt trong biển thông tin công nghệ mỗi ngày? Việc phải lướt qua hàng trăm bài báo trên Hacker News để tìm ra những tin tức thực sự quan trọng về AI, Startup hay Tech cực kỳ tốn thời gian. 

Thay vì làm thủ công, workflow n8n này sẽ giúp các sếp tự động hóa 100%: quét tin tức mới nhất theo từ khóa mong muốn, sử dụng sức mạnh của AI (qua OpenRouter) để chắt lọc, tóm tắt súc tích, và gửi thẳng báo cáo vào kênh Slack của đội ngũ vào mỗi buổi sáng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian tuyệt đối:** Không cần đọc bài dài, AI đã tóm tắt sẵn những ý chính cốt lõi.
- **Bám sát xu hướng công nghệ:** Tự động lọc đúng từ khóa (AI, Web3, Cloud...) các sếp quan tâm.
- **Cập nhật đều đặn:** Lịch trình chạy tự động mỗi sáng (9 AM) giúp đội ngũ bắt đầu ngày mới với thông tin nóng hổi.
- **Tương tác nhóm mượt mà:** Báo cáo được gửi trực tiếp vào Slack giúp mọi người dễ dàng thảo luận.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt sẵn sàng (Cloud hoặc Self-hosted).
- **Tài khoản OpenRouter:** Lấy API Key để kết nối với các mô hình AI chất lượng cao.
- **Tài khoản Slack:** Quyền kết nối qua OAuth2 để bot có thể đăng tin lên kênh (channel) chỉ định.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này hoặc tải file JSON từ nguồn cung cấp, sau đó paste trực tiếp vào màn hình n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình chính xác các node sau để hệ thống chạy trơn tru:

- **Trigger Daily at 9 AM (`scheduleTrigger`):** Mặc định lịch chạy là 9 giờ sáng mỗi ngày. Các sếp có thể click vào node này để đổi khung giờ nếu muốn.
- **Configure Your Settings (`set`):** Đây là nơi các sếp định nghĩa từ khóa và kênh Slack nhận tin:
  - `keywords`: Đổi từ khóa mặc định `'AI'` thành chủ đề các sếp muốn theo dõi (ví dụ: `['AI', 'startup', 'python']`).
  - `slack_channel`: Đổi tên `'news-updates'` thành tên kênh Slack thực tế của công ty/team.
- **OpenRouter Chat Model (`lmChatOpenRouter`):** Thêm Credential chứa OpenRouter API Key của các sếp vào đây để AI có "năng lượng" hoạt động.
- **Send Summary to Slack (`slack`):** Kết nối tài khoản Slack của các sếp bằng phương thức OAuth2 và cấp quyền cho phép bot đăng bài.

#### 3. Kích hoạt ⚡️
- Bấm nút **Test step / Execute workflow** để chạy thử xem các bài báo có được fetch về, AI có tóm tắt được và Slack có nhận được tin nhắn không.
- Nếu mọi thứ mượt mà, gạt công tắc **Active** góc trên cùng bên phải để bật chế độ chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa dạng hóa nguồn tin:** Ngoài Hacker News, các sếp có thể nối thêm các node RSS Feed từ TechCrunch, VnExpress, hay Medium.
- **Lưu trữ dữ liệu:** Thêm node Google Sheets hoặc Airtable ngay sau phần AI tóm tắt để lưu lại lịch sử các tin tức đã đọc, tiện tra cứu về sau.
- **Thông báo đa kênh:** Bên cạnh Slack, có thể dùng thêm node Telegram Bot để gửi bản tóm tắt song song cho nhóm chat cá nhân hoặc nhóm dự án.

### 📌 Kết luận
Một workflow cực kỳ gọn nhẹ nhưng mang lại giá trị cực lớn cho các nhà quản lý, lập trình viên và content creator muốn cập nhật kiến thức công nghệ nhanh chóng. Hãy cài đặt ngay hôm nay để tối ưu hóa thời gian đọc tin tức của các sếp!