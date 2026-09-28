---
title: "🚀 Tự động giám sát trạng thái GitHub Fork và cảnh báo qua Telegram"
description: "Hướng dẫn xây dựng workflow n8n tự động kiểm tra các repository fork trên GitHub, so sánh với upstream và gửi cảnh báo trực tiếp qua Telegram."
slug: "tu-dong-giam-sat-trang-thai-github-fork-qua-telegram"
tags: [n8n, automation, no-code, github, telegram, devops]
keywords: [n8n workflow, github fork monitor, tự động hóa github, telegram bot n8n, quan ly fork github]
---

# 🚀 Tự động giám sát trạng thái GitHub Fork và cảnh báo qua Telegram

Các lập trình viên và DevOps thường fork rất nhiều repository trên GitHub để đóng góp hoặc thử nghiệm. Nỗi đau lớn nhất là các repository fork này rất dễ bị **"lạc trôi" (fall behind hoặc ahead)** so với bản gốc (upstream) mà chúng ta không hề hay biết. Việc kiểm tra thủ công từng cái một thì vô cùng mất thời gian.

Giải pháp ở đây là gì? Một hệ thống tự động hóa 100% không cần code với n8n giúp quét toàn bộ các fork repository của bạn, so sánh trạng thái với upstream và gửi báo cáo chi tiết ngay lập tức qua Telegram bot!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Dăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Không cần kiểm tra thủ công từng repository fork.
- **Cảnh báo thông minh:** Nhận thông báo ngay lập tức qua Telegram khi repository bị lệch nhánh (behind/ahead).
- **Linh hoạt theo yêu cầu:** Kích hoạt thủ công hoặc qua lệnh chat `/forkcheck` trên Telegram với số lượng tùy chỉnh.
- **Tiết kiệm thời gian:** Quản lý hàng trăm repository chỉ với một câu lệnh đơn giản.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **GitHub Account & Personal Access Token (PAT):** Để gọi GitHub API lấy danh sách repo và thông tin chi tiết.
- **Telegram Bot Token:** Tạo bot thông qua `@BotFather` để nhận lệnh và gửi tin nhắn cảnh báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trong n8n, sau đó copy toàn bộ JSON của workflow (từ nguồn cấp) và dán trực tiếp vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động trơn tru, các sếp cần cấu hình chính xác các thành phần sau:

- **Node `Get repos` & `get-repo-details` (GitHub):** 
  - Chọn hoặc tạo mới `githubApi` credentials bằng GitHub Personal Access Token của các sếp (đảm bảo token có quyền đọc repo).
- **Node `Telegram Trigger` & `Telegram`:** 
  - Kết nối với `telegramApi` credentials sử dụng Token của Bot Telegram đã tạo từ `@BotFather`.
  - Bot này sẽ lắng nghe lệnh `/forkcheck` (hỗ trợ truyền tham số số lượng repo tối đa hoặc mặc định 1000 repo).
- **Node `Compare Branches API Call` (HTTP Request):** 
  - Node này sử dụng `httpHeaderAuth` để gọi GitHub API so sánh giữa nhánh của fork và upstream. Đảm bảo cấu hình đúng Header xác thực GitHub.
- **Các node `Code`, `Prepare Upstream URL`, `Process Comparison Result`, `Format for Telegram`:** 
  - Các đoạn mã JavaScript xử lý logic logic bóc tách dữ liệu JSON, ghép URL upstream và định dạng tin nhắn đã được viết sẵn, các sếp chỉ cần giữ nguyên và kiểm tra luồng dữ liệu.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và test thử bằng node `When clicking ‘Execute workflow’` hoặc mở ứng dụng Telegram chat với Bot bằng lệnh `/forkcheck`.
- Sau khi kiểm tra mọi thứ chạy mượt mà, hãy gạt công tắc sang **Active** để bot hoạt động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Lên lịch định kỳ (Cron):** Thay vì chỉ dùng Telegram Trigger, các sếp có thể gắn thêm node `Schedule Trigger` để bot tự động quét trạng thái fork vào mỗi đầu tuần (ví dụ: Thứ Hai hàng tuần).
- **Mở rộng kênh thông báo:** Kết hợp thêm node `Slack` hoặc `Discord` để gửi cảnh báo vào kênh chat chung của team kỹ thuật.
- **Lưu log vào Google Sheets:** Thêm bước ghi lại lịch sử các repository bị lệch nhánh vào Google Sheets để tiện theo dõi tiến độ cập nhật.

### 📌 Kết luận
Với GitHub Fork Status Monitor, việc quản lý và đồng bộ các repository fork chưa bao giờ dễ dàng đến thế. Hãy áp dụng ngay vào hệ thống của các sếp để giữ cho các dự án luôn cập nhật và sạch sẽ!